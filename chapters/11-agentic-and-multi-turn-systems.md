> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft.
>
> **Sourcing note:** ReAct loop content condensed from the prior Ch. 10 (ReAct) draft — the $P^N$ derivation lives there in full; this chapter treats it as a given primitive and builds outward onto tool scaling, structured output, and multi-turn memory. `[verify]` flags mark two figures attested only via secondary sources on the research run (Tam et al. arXiv ID; LongFuncEval arXiv:2505.10570 table).

---

# Chapter 11 — Agentic and Multi-Turn Systems

*The loop is the architectural response to single-shot limits*

**Author:** Nik Bear Brown
**Editor:** Nik Bear Brown

---

## Suggested titles

1. **Agentic and Multi-Turn Systems**
2. **The Loop, the Tool Catalog, the Schema, and the Window That Forgets**
3. **More Tools, More Errors: Why Agent Reliability Lives in the Architecture**

---

## TL;DR

A single-shot prompt compounds error across a long reasoning chain — a ten-step chain at 95% per-step accuracy finishes near 60%, because each token is sampled conditioned on the (possibly wrong) tokens before it. The **agent loop** — Thought → Action → Observation, formalized as ReAct ([Yao et al., 2023](https://arxiv.org/abs/2210.03629)) — is the architectural response: it injects Observation tokens from *outside* the model's distribution, interrupting (not erasing) the dependency chain. But the loop introduces three new control problems, each with a measurable mechanism and a falsifiable rule. **Tool count degrades performance** — error/hallucination rises as the tool catalog grows from 8K to 120K tokens, by 7.6%–85.6% ([LongFuncEval, 2025](https://arxiv.org/abs/2505.10570)) `[verify]` — so expose few scoped tools and route. **Structured output** is a control problem: prompted JSON *requests* conformance; constrained decoding ([Willard & Louf, 2023](https://arxiv.org/abs/2307.09702)) *guarantees* it by masking the vocabulary against a compiled grammar — but format restriction can cost reasoning ([Tam et al., 2024](https://arxiv.org/abs/2408.02442)) `[verify]`, so constrain the shape, free the reasoning, order fields reasoning-first. **There is no memory beyond the window** ([MemGPT, 2023](https://arxiv.org/abs/2310.08560)); multi-turn threads drift and, once derailed, do not recover ([Laban et al., 2025](https://arxiv.org/abs/2505.06120)) — so summarize-and-restart rather than repair.

---

## Learning objectives

By the end of this chapter you should be able to:

1. **(Understand→Create)** Structure a Thought → Action → Observation loop and explain, at the token level, why an injected Observation interrupts the $P^N$ dependency chain that single-shot reasoning builds.
2. **(Apply)** Control tool exposure: state the mechanism behind tool-count degradation and apply the routing rule (expose ≤N scoped tools; route by similarity above that).
3. **(Apply→Create)** Enforce structured output with constrained decoding, and order schema fields to avoid the reasoning cost of format restriction.
4. **(Evaluate)** Manage multi-turn context under a fixed-window constraint — choose among resupply, summarize-before-drop, and paging — and recognize non-recoverable derailment as the signal to restart clean.
5. **(Create)** Given a task, assemble an agent design that specifies the loop, the tool set, the output schema, and the memory strategy, and justify each choice from its mechanism.

## Prerequisites

Ch. 1 (Stochastic Machine) — token sampling and conditional distributions. Ch. 7 (Structuring and Governing Output) — templates, schemas, and slot-confabulation, which this chapter enforces at decode time. Ch. 9 (Brittleness) — reliability measured across trials, not a single run. Ch. 10 (Long-Context) — the position effects that govern what an agent's accumulating context actually attends to. Basic probability: the multiplication rule.

---

## 11.1 The onboarding agent that ran out of room

Meet the **Humanitarians AI** volunteer-onboarding agent. Its job sounds simple: walk a new volunteer through intake — collect their skills, match them to an open project, file the paperwork, schedule an orientation. It has tools: a skills database, a project roster, a calendar API, a form-filler. It is meant to run across a multi-turn conversation, holding the thread while the volunteer asks questions, changes their mind, uploads a résumé.

In a fresh session it handles all of this cleanly. Twenty turns later, on a harder case — a volunteer with an unusual skill mix and a scheduling conflict — it falls apart. It re-asks for the skills it already collected. It calls `schedule_orientation` before the project match is confirmed. At one point it confidently invokes a `send_welcome_packet` tool that does not exist. Re-run the *same* hard case as turn one of a fresh session and it succeeds.

Three distinct failures are tangled in that transcript, and the rest of this chapter is the untangling:

1. The thing *runs as a loop* — read, reason, act, observe — and the loop is what lets it act in the world at all. (§11.2)
2. It has *too many tools*, and as the catalog and history fill the context, it hallucinates a tool and mis-selects among the real ones. (§11.3)
3. Its *output is unstructured* where it needs to be structured — the form-filler gets prose where it needs typed fields. (§11.4)
4. It has *no memory beyond the window*, so by turn 20 the early intake has scrolled into the lost-in-the-middle trough (Ch. 10), and once it took a wrong turn it never recovered. (§11.5)

Each failure has a mechanism and a falsifiable fix. None of them is fixed by "use a better model." This is the chapter's spine: **the agent loop is the architectural response to single-shot limits, and the new failures it introduces — tool count, output shape, multi-turn memory — are themselves architectural problems with measurable mechanisms.**

> **A note on scope.** The taxonomy of multi-turn *interaction patterns* (flipped interaction, menu actions, and the rest) was developed in earlier material on interaction patterns and is folded into the output-governing discussion of Ch. 7. This chapter does not re-catalog those patterns. It supplies the quantitative degradation data and the memory-management mechanisms that sit underneath them.

---

## 11.2 The loop, condensed

The mechanism was derived in full in the ReAct chapter; here is the load-bearing summary, because everything downstream builds on it.

A language model generates each token by sampling from a distribution conditioned on the tokens before it: $t_i \sim P(t_i \mid t_0, \dots, t_{i-1})$. Chain a long reasoning trace and the errors compound. If $P$ is the probability each step is correct and the steps were independent, the whole chain is correct with probability

$$P_{\text{chain}} \approx P^N.$$

At $P = 0.95$, $N = 10$, that is about 60%; at $N = 20$, about 36%. A wrong token early poisons the conditioning for every token after it. No prompt fixes this, because a prompt is just more tokens drawn from the same poisoned distribution.

**ReAct** ([Yao, Zhao, Yu, Du, Shafran, Narasimhan, & Cao, 2023](https://arxiv.org/abs/2210.03629), ICLR 2023, arXiv:2210.03629) breaks the chain architecturally. The loop has three kinds of tokens:

- **Thought** — model-generated reasoning about what to do next.
- **Action** — model-generated tokens specifying a tool call, e.g. `match_project(skills=["python","grant-writing"])`.
- **Observation** — tokens *returned by the tool* and injected into the context. **These are not generated by the model.**

The loop runs Thought → Action → Observation → Thought → … until a Thought declares the answer. The crucial property: the Observation tokens were not sampled from any distribution conditioned on the model's prior Thoughts. The external world put them there. So they carry no inherited reasoning error. The next Thought is conditioned on both the prior Thoughts (still possibly wrong) *and* the Observation (a high-reliability anchor), which **interrupts** — does not erase — the dependency chain. If Observations anchor every $k$ steps, effective compounding is closer to $P^k$ than $P^N$.

Yao et al. evaluated ReAct on HotpotQA, FEVER, ALFWorld, and WebShop; it outperforms reason-only (Chain-of-Thought) and act-only baselines and reduces fact hallucination. The self-supervised cousin, [Toolformer (Schick et al., 2023)](https://arxiv.org/abs/2302.04761) (NeurIPS 2023), established the framing that underlies modern function calling: deciding *which* API to call, *when*, and with *what* arguments is itself token prediction.

The ReAct chapter named three conditions under which the error-interruption property breaks down — Observation salience (the anchor buried deep in a long context), Observation reliability (the tool returns garbage), and action-selection ambiguity (a large tool registry). This chapter takes those three failure conditions and makes them the agenda: §11.3 is action-selection ambiguity, §11.4 is one slice of Observation reliability (output shape), §11.5 is salience decay under multi-turn accumulation.

---

## 11.3 Controlling tool exposure: more tools, more errors

Here is the result that surprises people. You might expect that giving an agent more tools can only help — worst case, it ignores the ones it does not need. The data says the opposite: **performance degrades as the tool catalog grows.**

**The empirical spine.** [LongFuncEval (2025)](https://arxiv.org/abs/2505.10570) (arXiv:2505.10570) quantifies it directly: as the available-tool description grows from roughly 8K to 120K tokens — and as the correct tool's *position* in the catalog varies — function-calling performance drops by **7.6% to 85.6%** `[verify]`, driven by formatting failures and tool hallucination. The wide band is the point: the degradation is real and its size depends on how big the catalog is and where the right tool sits. (Note the Ch. 10 connection — *position in the catalog* matters, the same U-curve at work.) The phenomenon is reproduced across [Gorilla/APIBench (Patil et al., 2023)](https://arxiv.org/abs/2305.15334), [ToolLLM/ToolBench (Qin et al., 2023)](https://arxiv.org/abs/2307.16789) over 16,464 real APIs, and the [Berkeley Function Calling Leaderboard (Patil et al., 2025)](https://proceedings.mlr.press/v267/patil25a.html).

**The mechanism, two parts.** Why does adding tools hurt?

1. **Context consumption.** Every tool's name, description, and argument schema lives in the context window. A large catalog spends tokens — sometimes the majority of the window — on descriptions of tools the current task will never use. Those tokens are not free; they crowd out reasoning, and (Ch. 10) they push the relevant tool's description toward the lost-in-the-middle trough.
2. **Selection ambiguity.** With 5 tools, the model picks among 5 options. With 50, the option space is ten times larger, the descriptions overlap more, and the probability of selecting a near-miss (or hallucinating one that "should" exist, like the onboarding agent's `send_welcome_packet`) rises combinatorially. Gorilla's central contribution was showing that a tool-aware approach "substantially mitigates hallucination commonly encountered when prompting LLMs directly" — naming tool hallucination as a first-class failure mode.

**The falsifiable rule.** Expose a *small, scoped* set of tools per task; if the full inventory is large, put a **router** in front that surfaces only the relevant subset (retrieve tool descriptions by similarity to the task, rather than registering all of them upfront). The rule of thumb that follows from the data: scope to the task, and if more than ~10 tools are plausibly relevant, route rather than register.
*Falsifiable test:* run the same agent on the same task set with 5 vs. 50 tools available and measure the error/hallucination rate. If error does not rise with catalog size, the degradation is not biting your setup — measure it, do not assume it.

For the onboarding agent, the fix is not a smarter model. It is to stop handing the model the entire platform API on every turn. Intake needs the skills DB and the form-filler; scheduling needs the calendar. A router that exposes the four-or-five tools relevant to the *current* sub-task removes both the context bloat and most of the selection ambiguity — and `send_welcome_packet` never gets hallucinated because there is no crowded, ambiguous catalog inviting the confabulation.

> **A deflationary aside worth keeping.** Anthropic's "Building Effective Agents" (Dec 2024) draws a sharp line between *workflows* (LLMs orchestrated by predefined code paths) and *agents* (LLMs directing their own process), and argues most production value comes from simple composable workflows, not maximal autonomy. The routing rule is in that spirit: the most reliable agent is often the one you have given the least to decide.

---

## 11.4 Enforcing structured output

The onboarding agent's form-filler needs typed fields: `{name: str, skills: list[str], project_id: int, orientation_date: date}`. The model, left to itself, returns a friendly paragraph. Parsing prose into a typed record is exactly the brittleness Ch. 9 warns about. Structured output is the fix — and it is a *control* problem, not a phrasing problem.

**Prompted JSON requests; constrained decoding guarantees.** You can ask the model to "respond in JSON." That is a *request*: the model samples tokens that usually look like JSON and sometimes do not — a trailing comma, a missing brace, a stray apologetic sentence before the object. The reliable approach is to enforce the schema at the decoder. [Willard and Louf (2023)](https://arxiv.org/abs/2307.09702) ("Efficient Guided Generation," arXiv:2307.09702 — the mechanism behind the **Outlines** library) reframe generation as transitions over a finite-state machine compiled from a regex or context-free grammar. At each step they precompute which vocabulary tokens are *legal* given the grammar state and mask the rest to near-zero probability. The model literally cannot emit an invalid token; conformance is a guarantee, not a hope, and the masking adds near-zero overhead. Native provider features (OpenAI's Structured Outputs, Aug 2024) use the same constrained-decoding idea.

There is a precise caveat to carry: **constrained decoding guarantees shape, not truth.** The fields will be the right type; the *values* can still be wrong. A schema-valid `project_id: 4` can be the wrong project. This is the same lesson as Ch. 10's validator caveat — a deterministic layer catches the failures it is built to catch and silently passes the ones it is not.

**The counter-mechanism: format restriction can cost reasoning.** Here is the nuance that separates a careful engineer from a careless one. [Tam et al. (2024)](https://arxiv.org/abs/2408.02442) ("Let Me Speak Freely?", EMNLP 2024 Industry Track) `[verify arXiv ID]` found that forcing JSON/format restrictions *degrades* reasoning by roughly 10–15% on math and symbolic tasks versus free-form generation. Two distinct causes, and they matter for the fix:

1. The *format-requesting instruction itself* costs accuracy — before any decoder constraint is applied, telling the model "answer only in JSON" already shifts its distribution away from good reasoning.
2. If the schema puts the **answer field before the reasoning field**, the model commits to an answer before it has reasoned — it fills `answer` first, then rationalizes in `reasoning`, which is backwards.

**The falsifiable rule.** *Constrain the shape, free the reasoning, order fields reasoning-first.* Concretely: either (a) let the model reason in free-form first and reformat into the schema in a second pass, or (b) put the reasoning field *before* the answer field in the schema so the constrained decode still lets reasoning condition the answer.
*Falsifiable test:* run the same task in three modes — free-form, JSON-mode answer-first, JSON-mode reasoning-first — and measure reasoning accuracy. If reasoning-first does not recover most of the gap, your task is not in the regime Tam et al. describe.

(Whether this degradation survives in 2025–2026 reasoning models with extended thinking is unresolved; early evidence suggests thinking tokens recover most of the lost accuracy, but it needs replication. Treat the rule as well-supported on non-thinking models and as a hypothesis to test on thinking models.)

---

## 11.5 Managing multi-turn context

Now the failure that took down the onboarding agent at turn 20.

**The hard constraint: there is no memory beyond the window.** A transformer has no persistent state between calls. Everything the agent "remembers" is whatever is in the context window *right now*. [MemGPT (Packer et al., 2023)](https://arxiv.org/abs/2310.08560) (arXiv:2310.08560) framed this with an operating-systems analogy: treat the context window like RAM and external storage like disk, and let the LLM issue function calls to *page* relevant history in and evict the rest. The framing fixes the right mental model — **state must be resupplied each turn; the only questions are *what* to resupply and *how compressed*.**

**Why it degrades.** Three strategies compete, with no consensus default:

- **Resupply raw history.** Simple, but the window fills; by turn 20 the intake data is buried in the middle (Ch. 10's trough) and under-attended.
- **Summarize before dropping.** A running summary (e.g., a summary-buffer memory) compresses old turns. Lossy: whatever the summary omits is gone, and *which* functional context gets dropped is poorly mapped.
- **Page / retrieve.** Keep history in an external store, retrieve the relevant slice each turn (MemGPT-style). Adds a retrieval step that can itself surface the wrong slice.

**The sharpest empirical finding.** [Laban et al. (2025)](https://arxiv.org/abs/2505.06120) ("LLMs Get Lost in Multi-Turn Conversation," arXiv:2505.06120) tested top open and closed models across six generation tasks and found an **average 39% performance drop** from single-turn to multi-turn. They decompose it: a *minor* loss of raw aptitude and a *large* rise in unreliability. The named effects are exactly the onboarding transcript — "answer bloat" (later attempts run 20–300% longer), a "lost-in-middle-turns" effect, and the decisive one: **when a model takes a wrong turn, it gets lost and does not recover.** [τ-bench (Yao et al., 2024)](https://arxiv.org/abs/2406.12045) reinforces it: even strong models succeed on under 50% of multi-turn tool-agent tasks and are *inconsistent* across trials (pass^8 < 25% in retail) — the bottleneck is the *consistency* layer, not the capability layer.

**The falsifiable rule.** When a multi-turn thread goes wrong, **summarize and restart clean** — do not patch the derailed thread. The mechanism behind the rule: a wrong turn is now in the context, conditioning every subsequent turn (this is $P^N$ from §11.2 re-entering through conversation history); repairing in place reasons *from* the contamination, while restarting with a clean summary drops it.
*Falsifiable test:* on a set of derailed transcripts, compare continued-repair vs. summarize-and-restart on task success. If repair matches restart, the non-recovery effect is not biting your domain.

(Honest caveat: Laban et al.'s causal account — that attention concentrates on recent turns and the early correct framing decays — is a *hypothesis*, not settled mechanism. The 39% drop is measured; the *why* is partly inferred from the Ch. 10 position effects. Label it as such.)

For the onboarding agent: scope each sub-task (intake, match, schedule) to its own short context with a clean summary handoff between them, rather than accumulating one ever-growing thread. When the hard case derails, the agent should detect the loop, summarize what is confirmed (skills collected, no project matched yet), and restart the match step fresh — not keep arguing with its own contaminated history.

---

## 11.6 Putting it together

The four pieces are one design, and they interlock. Step back and read the onboarding agent as a single architecture:

- **The loop** lets it act in the world and interrupts single-shot error compounding — but only as well as its Observations are salient, reliable, and attended to.
- **Tool scoping** keeps Observation *selection* clean: few scoped tools, routed, so the action step is not drowning in a 50-tool catalog.
- **Structured output** keeps Observation *consumption* clean: constrained decoding guarantees the form-filler gets typed fields, with reasoning ordered before the answer so the schema does not strangle the reasoning.
- **Memory management** keeps Observation *salience* alive across turns: summarize-and-restart so the early intake never rots in the middle of a 20-turn window, and a wrong turn never compounds.

This is the book's master argument in agentic form: **architecture is the leverage point, not the model.** The same model, in a loop with a scoped tool router, a reasoning-first schema, and a summarize-and-restart memory policy, is a different *system* from the same model handed forty tools, asked politely for JSON, and left to accumulate a 20-turn thread. The first ships. The second re-asks for skills it already has and invents a welcome-packet tool. The weights did not change. The architecture did.

One honest caveat to carry forward, and it is the field's current frontier. Evaluation has shifted from "can the model do this in one call" to "can it do this *reliably* across many turns" (BFCL v1→v4, τ-bench's pass^k, "LLMs Get Lost"). The mechanisms in this chapter are well-attested; the *magnitudes* are model- and task-dependent and the field is moving fast. Tool-count degradation, format-restriction cost, and non-recovery are real and predictable in *direction*. Their *size* in your system is something you measure, not assume — which is the Ch. 9 discipline applied to agents.

---

## Exercises

1. **(Understand)** In one paragraph, explain why an Observation token injected by a tool does *not* compound $P^N$ error the way a model-generated Thought token does — and name the one condition under which the Observation fails to interrupt the chain.

2. **(Apply)** Your enterprise platform exposes 80 internal functions. A teammate registers all 80 with the agent "so it has everything it might need." State the mechanism by which this degrades performance (both parts), and design the two-condition experiment (5 tools vs. 80 tools) that would measure the degradation, including the metric you record.

3. **(Apply)** You are given a schema `{answer: str, reasoning: str}` and asked why the agent's math accuracy dropped after the team "added structured output." Identify the specific design error, rewrite the schema, and state which of Tam et al.'s two causes your rewrite addresses (and which it does not).

4. **(Evaluate)** Given two transcripts of the onboarding agent — one where it took a wrong turn at turn 6 and was "corrected" in place through turn 20, one where it was summarized-and-restarted at turn 7 — predict which performs better at turn 20 and justify the prediction from the $P^N$ mechanism and Laban et al.'s non-recovery finding.

5. **(Create — produce)** Design the full Humanitarians AI onboarding agent as a one-page spec: the Thought→Action→Observation loop, the tool set per sub-task (and where you route), the output schema (with field ordering justified), and the multi-turn memory policy (with the restart trigger defined). For each of the four choices, write the one-sentence mechanism that justifies it. Then name the single failure mode your design does *not* defend against.

---

## What would change my mind

A controlled study showing that, on current frontier models, registering a large tool catalog (50+ tools) does **not** degrade performance relative to a scoped subset on matched tasks — i.e., that the model reliably ignores irrelevant tools without context-bloat or selection-ambiguity cost. The chapter argues tool-count degradation is mechanistic (context consumption + selection ambiguity) and therefore general; evidence that frontier models have solved tool selection at scale would force the routing rule down to a class of weaker or smaller-window models rather than stating it generally. A second, narrower thing that would move me: replication showing that 2025–2026 reasoning models with extended thinking fully erase the format-restriction reasoning cost (Tam et al.), which would retire the "reasoning-first field ordering" rule for those models.

## Still puzzling

- **No agreed default memory strategy.** Summarize vs. retrieve vs. page (MemGPT) — when each wins is under-characterized, and lossy summarization's failure modes (what functional context silently drops) are poorly mapped.
- **Why models don't recover after a wrong turn.** Laban et al. measure the non-recovery; the attention-to-recent-turns explanation is a hypothesis, not settled mechanism. A study isolating *why* the early correct framing stops being attended to would settle it.
- **Tool routing's own failure mode.** Vector-retrieval over tool descriptions is the proposed fix for large catalogs, but retrieval errors that surface the *wrong* tool subset are themselves unstudied — a router that confidently hands the agent the wrong five tools may fail worse than no router.
- **Does the format-restriction cost survive thinking models?** Early evidence says thinking tokens recover most lost accuracy, but it needs replication before the field can retire field-ordering hygiene.

---

## References

- Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2023). [ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629). ICLR 2023. arXiv:2210.03629.
- Schick, T., Dwivedi-Yu, J., Dessì, R., Raileanu, R., Lomeli, M., Zettlemoyer, L., Cancedda, N., & Scialom, T. (2023). [Toolformer: Language Models Can Teach Themselves to Use Tools](https://arxiv.org/abs/2302.04761). NeurIPS 2023. arXiv:2302.04761.
- Patil, S. G., Zhang, T., Wang, X., & Gonzalez, J. E. (2023). [Gorilla: Large Language Model Connected with Massive APIs](https://arxiv.org/abs/2305.15334). NeurIPS 2024. arXiv:2305.15334.
- Qin, Y., Liang, S., Ye, Y., et al. (2023). [ToolLLM: Facilitating Large Language Models to Master 16000+ Real-world APIs](https://arxiv.org/abs/2307.16789). ICLR 2024 (spotlight). arXiv:2307.16789.
- Patil, S. G., et al. (2025). [The Berkeley Function Calling Leaderboard (BFCL): From Tool Use to Agentic Evaluation of Large Language Models](https://proceedings.mlr.press/v267/patil25a.html). ICML 2025.
- Willard, B. T., & Louf, R. (2023). [Efficient Guided Generation for Large Language Models](https://arxiv.org/abs/2307.09702). arXiv:2307.09702. (Outlines.)
- Tam, Z. R., et al. (2024). Let Me Speak Freely? A Study on the Impact of Format Restrictions on Performance of Large Language Models. EMNLP 2024 (Industry Track). arXiv:2408.02442. `[verify arXiv ID]`
- OpenAI (2024). [Introducing Structured Outputs in the API](https://openai.com/index/introducing-structured-outputs-in-the-api). (Vendor "100% reliability" claim is shape-conformance, not correctness.)
- Packer, C., Fang, V., Patil, S. G., Lin, K., Wooders, S., & Gonzalez, J. E. (2023). [MemGPT: Towards LLMs as Operating Systems](https://arxiv.org/abs/2310.08560). arXiv:2310.08560.
- Laban, P., et al. (2025). [LLMs Get Lost in Multi-Turn Conversation](https://arxiv.org/abs/2505.06120). arXiv:2505.06120.
- Yao, S., Shinn, N., Razavi, P., & Narasimhan, K. (2024). [τ-bench: A Benchmark for Tool-Agent-User Interaction in Real-World Domains](https://arxiv.org/abs/2406.12045). ICLR 2025. arXiv:2406.12045.
- LongFuncEval: Measuring the effectiveness of long context models for function calling (2025). [arXiv:2505.10570](https://arxiv.org/abs/2505.10570). `[verify table numbers against PDF]`

---

**Tags:** agent-loop, react-thought-action-observation, tool-count-degradation, constrained-decoding, multi-turn-non-recovery, summarize-and-restart

---

## A note about AI

Agentic prompting is where "give it tools and let it figure it out" meets the wall. The model will happily accept fifty tools and a twenty-turn thread. It will also hallucinate a fifty-first tool and forget turn three.

Where the model genuinely helps: drafting the *scoped* tool set for a sub-task. Describe the sub-task and ask the model which 4–6 tools are actually needed and which of your full catalog are noise. It is good at this triage, and the triage is the routing rule in action.

Where the model does damage: producing an agent trace that *looks* like a clean Thought→Action→Observation loop but where the Actions never actually change the conclusion — the trace fakes the structure without doing the work, exactly the pseudo-ReAct failure. It will also "remember" things from earlier turns that it is in fact reconstructing from the recent context, confidently and wrongly.

The rule: an agent's reliability lives in its architecture — the loop, the tool scope, the schema, the memory policy — not in the model's eagerness. Test the loop by deleting an Action and checking whether the answer changes; test the memory by derailing the thread and seeing whether it recovers.

---

##  AI Wayback Machine
**Charles Forgy** was the computer scientist who invented the Rete algorithm (1974/1979) and the OPS5 production-system language at Carnegie Mellon — production systems matched working memory against rules that fired actions updating that memory, the direct symbolic ancestor of the Observation → Thought → Action loop.

**Run this:**

```
Who is Charles Forgy, and how does their work on production systems and the Rete algorithm connect to the Thought-Action-Observation agent loop we covered in this chapter? Keep it to three paragraphs. End with the single most surprising thing about their career or ideas.
```

→ Search **"Charles Forgy"** on Wikipedia.

**Now make the prompt better.** Try one of these:

- Ask it to map a production-system rule (condition → action → updated working memory) onto one turn of a ReAct loop, and say where the analogy is tight and where the LLM breaks it.
- Add a constraint: "Answer including what production systems had that LLM agents lack — and what LLM agents have that production systems lacked."

What changes? What gets better? What gets worse?
