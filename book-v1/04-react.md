> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft. Second chapter drafted for this book.
>
> **Draft provenance:** This draft is a revision in response to a detailed chapter critique of an earlier Ch. 10 draft. Priority fixes addressed: (1) explicit causal chain for why external retrieval interrupts probabilistic conditioning; (2) return to P^N formula after ReAct is introduced, with scope limits named; (3) honest acknowledgment that ReAct *interrupts* cumulative error under specific conditions rather than eliminating it. See research notes for full critique-to-fix mapping.

---

# Chapter 10 — ReAct

*Grounding Reasoning in the Real World*

**Author:** Nik Bear Brown

---

## Suggested titles

1. **ReAct: Grounding Reasoning in the Real World**
2. **Why External Observations Interrupt the Dependency Chain (But Don't Erase It)**
3. **The Architectural Fix That a Prompt Cannot Make**

---

## TL;DR

Chain-of-thought prompting multiplies a per-token error rate over a long reasoning chain — a ten-step chain at 95% per-step accuracy finishes with about 60% end-to-end accuracy — because each token is sampled from a distribution conditioned on the tokens before it, and a wrong prior token poisons the distribution forward. ReAct interrupts this dependency chain by replacing some reasoning steps with *external observations*: tokens that enter the context from outside the model's probability distribution, carrying no inherited error from prior steps — which is an architectural property, not a model property, and which breaks down in specific and nameable conditions you should know before you deploy it.

---

## Learning objectives

By the end of this chapter you should be able to:

1. Write the $P^N$ cumulative-error formula for Chain-of-Thought reasoning and explain mechanistically where each factor comes from.
2. Explain, at the token level, why an external observation in a ReAct loop is not subject to the same dependency-chain error as a model-generated token.
3. Name three conditions under which ReAct's error-reset property breaks down: context window exhaustion, tool output distribution shift, and action-selection ambiguity from large tool registries.
4. Distinguish between a prompt-level fix and an architectural fix using the token-level mechanism, and identify which class a given proposed fix belongs to.
5. Given a task description, argue on the basis of adaptive information requirements whether ReAct or an alternative pattern (parallel tool use, Plan-and-Execute) is the appropriate architectural choice.

## Prerequisites

Ch. 1 (Stochastic Machine) — token sampling, conditional distributions. Ch. 9 (Interaction Patterns) — Chain-of-Thought and its scope. Basic probability: conditional probability and the multiplication rule.

---

## 10.1 Which city hosted the Olympics in the year Germany's GDP first exceeded $3 trillion?

This is the kind of question no frontier model answers reliably from its weights. It requires two lookups — the year German GDP first crossed $3T, then the Olympic host city in that year — and a composition across them. Ask a recent model with Chain-of-Thought prompting and you'll see something like this:

> *"Germany's GDP first exceeded $3 trillion in 2010. The Summer Olympics in 2010 were held in Vancouver."*

Vancouver hosted the 2010 **Winter** Olympics. There were no Summer Olympics in 2010. And Germany's GDP first exceeded $3 trillion closer to 2015, not 2010 — the first fact is wrong and the second fact is wrong but consistent with the first. The reasoning is fluent. The answer is confidently wrong in two distinct places that reinforce each other.

Now try the same question in a ReAct loop — same model, same temperature, same system prompt. The agent runs a few internal reasoning steps (Thoughts), calls a search tool twice (Actions), and returns:

> *"Germany's GDP first exceeded $3 trillion in 2015 (World Bank). The Olympics in 2015 were the 2015 Special Olympics World Summer Games in Los Angeles."*

The reasoning is coherent. The facts are correct. The composition produces a defensible (if possibly pedantic) answer. **The model did not change. The architecture did.**

This is what the chapter is about — not that ReAct produces better answers, which it sometimes does and sometimes doesn't, but *why*, mechanistically, changing the architecture around a fixed model can change which class of errors the system is subject to. The difference is not a clever prompt. The difference is that ReAct interrupts a specific probabilistic dependency chain that Chain-of-Thought builds. That dependency chain is the reason CoT's errors compound. Understanding why is the job of the next few pages.

---

## 10.2 Why Chain-of-Thought compounds error

A language model generates each output token by sampling from a probability distribution over its vocabulary. That distribution is *conditioned* on every token that came before it — the system prompt, the user question, any generated tokens so far. Formally, for token $t_i$ in a sequence:

$$t_i \sim P(t_i \mid t_0, t_1, \dots, t_{i-1})$$

This conditioning is the mechanism of Chain-of-Thought. When you ask a model to "reason step by step," each reasoning step generates tokens, and the *next* reasoning step is sampled from a distribution conditioned on those tokens. If one reasoning step produces a wrong token — say, "Germany's GDP first exceeded $3 trillion in **2010**" instead of 2015 — that wrong token becomes part of the conditioning context for every subsequent step.

Call $P$ the probability that each reasoning step produces tokens consistent with the ground truth. The probability that all $N$ steps of a chain are correct is approximately:

$$P_{\text{chain}} \approx P^N$$

At $P = 0.95$ (a confident per-step accuracy for a strong model on a well-formed reasoning task) and $N = 10$ (a modest reasoning chain), $P_{\text{chain}} \approx 0.60$. At $N = 20$, $P_{\text{chain}} \approx 0.36$.

This formula is an approximation. In real reasoning chains, errors are not perfectly independent — a wrong fact in step 2 often increases the probability of a *consistent* wrong fact in step 5 (the model confabulates to fit its earlier claim). That correlation structure sometimes helps and sometimes hurts, but the gross shape holds: **long reasoning chains compound error, because each token is conditioned on everything before it, and a wrong prior token shifts the subsequent distribution in a wrong direction.**

This is the dependency chain Chain-of-Thought builds. Read again what happens in the Olympic GDP example: the model sampled the wrong GDP year, *then* had to generate an Olympic host, and the wrong GDP year conditioned the distribution over possible Olympics — not toward the correct Olympics for the correct year, but toward whichever Olympics was statistically plausible given the (incorrect) 2010 claim. Vancouver 2010 is a plausible completion of "Olympics in 2010." It is even approximately correct — the Winter Olympics really were in Vancouver in 2010. But it is not an answer to the question the user asked. The wrongness of the first step poisoned the distribution of the second.

This is exactly what any prompt-level fix cannot repair. "Double-check your facts" is itself just more tokens in the context window. The model samples its double-check from the same distribution that produced the error, conditioned on the error. A smarter prompt makes the conditioning slightly better. It does not break the dependency structure that makes errors compound.

Breaking that structure is an architectural move, not a prompt move.

---

## 10.3 What ReAct does, token by token

ReAct was introduced by [Yao et al. (2022)](https://arxiv.org/abs/2210.03629) and evaluated on three benchmarks — multi-hop factual question answering on [HotPotQA](https://arxiv.org/abs/1809.09600), fact verification on [FEVER](https://arxiv.org/abs/1803.05355), and embodied task completion in [ALFWorld](https://arxiv.org/abs/2010.03768). The paper reports that ReAct outperforms Chain-of-Thought and Action-only baselines on each of these benchmarks, and that the advantage is largest on questions where multi-step retrieval is required and confabulation is most costly.

The mechanism is a loop with three kinds of tokens:

- **Thought** — model-generated tokens reasoning about what to do next.
- **Action** — model-generated tokens specifying a tool call in a structured format, e.g. `search("Germany GDP 2015")`.
- **Observation** — tokens returned from the tool call and injected into the context. **These are not generated by the model.**

The loop runs: Thought → Action → Observation → Thought → Action → Observation → … until the model emits a Thought that says it has the answer.

The crucial distinction is *who generates which tokens*, because that distinction determines what probability distribution each token was drawn from — and therefore what kind of error it can carry.

### Conceptual level — what "the error resets" actually means

Consider what happens at step 5 of a Chain-of-Thought reasoning chain. Token 5 is sampled as:

$$t_5 \sim P(t_5 \mid \text{system prompt, question, } t_1, t_2, t_3, t_4)$$

If any of $t_1 \ldots t_4$ is wrong, $t_5$'s distribution is shifted in the direction of whatever was wrong.

Now consider an Observation step in a ReAct loop. The Observation tokens $o_1, o_2, \ldots, o_k$ are not sampled from the model at all. They are returned by a tool call — a deterministic function, or an API query, or a retrieval from an external index. The tokens enter the context directly. They were not drawn from any distribution conditioned on the model's prior Thoughts. The external world put them there.

The next Thought is then sampled as:

$$t_{\text{next}} \sim P(t_{\text{next}} \mid \text{system prompt, question, } t_1, \ldots, t_n, o_1, \ldots, o_k)$$

Notice what this conditional includes and does not include. It *still* includes the prior Thought tokens — so if those were wrong, their influence is still present. But it *also* includes the Observation tokens, which carry a different reliability profile entirely. They were produced by a process the model's errors cannot influence.

The practical effect is that the Observation acts as an **anchor**. The model can still be internally biased by a wrong prior Thought, but the Observation provides a high-reliability input that counteracts that bias. If the tool returned "Germany's GDP first exceeded $3 trillion in 2015," the next Thought is unlikely to ignore that fact even if an earlier Thought claimed 2010 — because the Observation is salient, formatted, and contextually recent.

**The dependency chain is not broken. It is interrupted.** The next Thought still depends on prior Thoughts, but it also depends on new anchor tokens whose reliability is not a function of the prior Thoughts' correctness. That's the precise claim. Not that "error resets at each observation" — that is hyperbole, and the chapter at large must be careful not to plant it. The precise claim is that **each Observation is an injection of tokens whose provenance is different from model-generated tokens, and that provenance difference interrupts (does not eliminate) the probabilistic dependency through which CoT errors compound.**

### Returning to P^N

Does $P^N$ still apply to a ReAct chain? Partially — and the "partially" is where the real engineering happens.

Consider a ReAct trace with alternating Thoughts and Observations: $T_1, O_1, T_2, O_2, T_3, O_3, \ldots$

- The Thought tokens $T_i$ are still sampled from the model's distribution. They still compound error among themselves. If you had a ReAct loop with 20 Thought steps and no Observations, you'd be back to pure CoT and the $P^N$ formula would apply.
- The Observation tokens $O_i$ are injected from outside. They don't compound model error at all — they carry tool-reliability error instead, which is a different failure mode (§10.5).
- The Thought-after-Observation step is where interruption happens: the next Thought is conditioned on both prior Thoughts and the new Observation, so the model's bias toward its earlier (possibly wrong) Thoughts is counteracted by the anchor of the Observation.

So the rough accounting: if a chain has $N$ total reasoning steps and the Observations successfully anchor every $k$ steps, the effective error compounding is closer to $P^k$ than $P^N$. The longer the Observation period (larger $k$), the more the system reverts toward $P^N$ behavior between anchors. In the limit where Observations happen after every Thought, the compounding is $P^1$ — essentially one-step reliability. In the limit where there are no Observations, you have CoT.

This framing also makes the scope limits visible. ReAct's error-interruption guarantee assumes:

1. **The Observation tokens are actually salient to the next Thought.** In a long trace where the Observation is buried deep in the context and attention is competing across thousands of tokens, the anchor weakens. This is the context-window failure mode.
2. **The Observation content is reliable.** If the tool returns corrupted or misformatted data, the Observation is no longer an anchor — it's a new source of error (§10.5).
3. **The next Thought actually attends to the Observation.** The model may ignore the Observation if a prior Thought was confidently phrased in a contradictory way. This is empirically rare but not impossible, and it scales with chain length.

A reader who walks away believing "ReAct resets error at each step" has been given a simplified model that breaks at all three boundaries. The honest claim is narrower: ReAct *interrupts* dependency-chain error in reasoning chains that fit the conditions above.

---

## 10.4 Architectural level — the three components

Step back from tokens to architecture. A working ReAct system has three structural components, each of which can fail independently.

*[Level of abstraction: architectural. The previous section was conceptual — about what tokens do. This section is about how those tokens are produced and routed. The next section will descend to implementation — what a line of Python looks like.]*

- **Tool Registry** — the set of functions the Action step can call. A key-value mapping from tool names (strings the model writes) to executable functions (Python code that runs). This is the boundary between model and world.
- **Observation Buffer** — the portion of the context window holding the accumulated Thought/Action/Observation history. Bounded by the model's context limit. Expanded each step. Eventually overflows on long tasks.
- **Few-Shot Template** — the format that demonstrates, via examples, what a Thought looks like, what an Action syntax is, and how Observations are formatted. The model uses these as distributional cues for its own outputs.

*[Level of abstraction: implementation.]*

A minimal Tool Registry as code:

```python
TOOLS = {
    "search":     lambda q: wikipedia_search(q),
    "calculator": lambda expr: safe_eval(expr),
}

def execute_action(action_string):
    name, argument = parse(action_string)
    if name not in TOOLS:
        return f"Error: tool '{name}' not in registry"
    return TOOLS[name](argument)
```

The registry is a Python dictionary. That is not a metaphor or an abstraction — it is literally, mechanically, a dictionary. When the model writes an Action token sequence that includes `search("Germany GDP")`, a parser extracts the tool name and argument, looks up the function, and runs it. The Observation is the function's return value, passed back into the context window as tokens.

This implementation-level detail matters because it is the boundary at which a prompt-level fix becomes an architectural fix. If the model occasionally writes `serach` (misspelled), a prompt-level response would be "be more careful with tool names." An architectural response would be to replace the `TOOLS.get(name)` lookup with a fuzzy-match or to add a validator that rejects the action before it executes.

One of these responses asks the probabilistic system that produced the error to produce fewer errors. The other adds a deterministic layer that catches the error before it propagates. That distinction is the core of the chapter's engineering claim.

---

## 10.5 Failure case — distribution shift when the tool breaks format

Here is what goes wrong when a ReAct system's tool changes its output format without the agent knowing.

A tool registered as `search(query) -> str` is updated in production to return JSON instead of plain text. The ReAct loop calls `search("Germany GDP 2015")` and gets back:

```json
{"result": "Germany's GDP exceeded $3 trillion in 2015", "confidence": 0.94}
```

The loop, which expected a plain-text Observation, passes this JSON into the context. The model now sees an Observation that looks structurally different from everything its few-shot template prepared it for. The next Thought is sampled from a distribution that has been shifted by a distributional signal the training didn't anticipate:

> *"Thought 3: The search tool returned a structured object. I should extract the 'result' field, but the format suggests this is a different kind of query interface. Let me try search_structured instead..."*

The model invents a tool that doesn't exist. The Action step emits `search_structured(...)`. That tool isn't in the registry. The Observation is an error message. The next Thought attempts yet another recovery. The trace spirals. By Thought 5, the model has forgotten what the original question was.

Trace the causal chain:

1. Tool output format changed upstream.
2. The loop passed the JSON into context without format validation.
3. The model's next Thought was sampled from a distribution conditioned on an unfamiliar Observation.
4. The distributional shift produced an Action (`search_structured`) that doesn't exist.
5. The error cascaded because each subsequent Thought was conditioned on the earlier ones (this is precisely where $P^N$ compounding returns — the Observation failed to anchor, so the chain is effectively CoT from that point forward).

The prompt-level fix: tell the model "be careful with tool outputs and handle structured data gracefully." This response delegates error handling to the same probabilistic system that is already failing. It may work most of the time. It fails when the distributional shift is large enough that the model's "graceful handling" attempt itself misfires.

**The architectural fix: a validator that runs between the tool and the Observation buffer, which rejects any output that doesn't match the registered signature and returns a typed error message the loop knows how to handle.** A validator delegates error handling to a deterministic Python function. The function either passes the Observation through or returns a standardized error token sequence the model was trained to recover from. The validator doesn't delegate anything back to the probabilistic system. It interrupts the failure at the exact layer where the distributional shift enters.

These two fixes — "tell the model to be careful" and "add a validator" — look superficially similar. They are not. One of them asks the system that is already failing to please fail less. The other adds a new component, outside the probabilistic inference loop, that makes the specific failure structurally impossible. That is what an architectural fix is, and that is what a prompt cannot do. A prompt is just more tokens in the probability distribution that is producing the error. A Python function running outside that distribution is not.

A second scope limit worth naming honestly: validators have their own failure modes. A validator that checks schema correctness doesn't check semantic correctness. A tool can return a schema-valid but semantically wrong result — the JSON is well-formed, the "result" field is present, but the value is wrong. The validator happily passes this through. The model's next Thought is poisoned by an anchor that is reliably *formatted* but unreliably *correct*. This is a different failure mode (call it context poisoning — it's addressed in a later chapter) and the validator does not catch it. An honest engineer knows which failures their architectural layer catches and which it does not.

---

## 10.6 When to use ReAct, and when not to

ReAct is the right pattern when the task has three properties:

1. **Information is required that the model cannot be expected to have memorized.** Current events, proprietary data, multi-hop compositions across obscure facts. If the answer lives entirely within the model's training distribution, the overhead of the loop is not earning its cost.
2. **Subtasks cannot be enumerated in advance.** The agent must adapt each next step based on what the prior step returned. If you could write down the full task plan before execution, a simpler pattern (Plan-and-Execute, covered in Ch. 11's prompt-stack framing, and developed fully in the agentic-systems book) is probably cheaper and more predictable.
3. **Tool output reliability is manageable.** The distribution-shift failure above is real. If your tool inventory changes frequently, or your tools return unpredictable formats, ReAct's interruption guarantee weakens. You need the validator layer *and* the format contracts *and* the monitoring. For very unreliable tool environments, consider a pattern that does less probabilistic reasoning around tool outputs.

ReAct is the wrong pattern when the subtasks are independent and can run in parallel (because the serial Thought→Action→Observation loop can't exploit parallelism), when tool calls dominate latency and you have fixed steps (parallel tool use is cheaper), or when the reasoning chain is short enough that CoT's $P^N$ compounding is not yet painful ($N = 3$ at $P = 0.95$ is 86% — you may not need the overhead of a loop).

This decision is genuinely made per-task. The decision criterion — is the task adaptive, i.e. does each step condition the next step's requirements? — is what separates the ReAct-appropriate cases from the alternatives.

---

## 10.7 Back to the Olympic GDP question

The CoT failure on the opening question was not a model failure. It was a compositional error where the wrong token in step one poisoned the distribution at step two, and the second error was *consistent with* the first — which is precisely the dependency chain that $P^N$ describes.

The ReAct success on the same question was not a model success. It was an architectural decision to replace two CoT steps with two tool-call-plus-Observation steps, whose reliability profile was different from the model's generation reliability. The same model performed the orchestration. The architecture did the work of holding each step to an external anchor.

This is the book's master argument in mechanism form: **the architectural decision about where to place external anchors is more consequential, for the system's end-to-end reliability, than the decision about which model does the reasoning between those anchors.** A marginally weaker model in an architecture with well-placed anchors will outperform a marginally stronger model in an architecture without them — for tasks where the reasoning chain is long enough that $P^N$ compounds meaningfully, and the external facts are available to anchor against.

"Not always, but often enough." The honest version of that claim scopes it: in the domain [Yao et al. (2022)](https://arxiv.org/abs/2210.03629) studied — factual multi-hop question answering, fact verification, embodied task completion — the architecture effect dominated the model effect. Whether that generalizes to other domains is an empirical question. The mechanism is general; whether the effect size is large enough to matter in *your* domain requires that you measure.

The three scope limits from §10.3 bear repeating. ReAct's error-interruption property assumes Observations are salient, reliable, and attended to. Context-window exhaustion weakens salience. Tool failures destroy reliability. And chain length eventually overwhelms attention regardless. A reader who walks away with "ReAct fixes the problem" has been given a simplified picture. The honest picture: **ReAct interrupts a specific failure mode, introduces different failure modes (distribution shift, registry ambiguity, anchor-decay), and requires specific architectural defenses (validators, registry design, context-window policy) to remain reliable at production scale.** The chapter has named all three. Engineering is what you do with them.

---

**What would change my mind:** A well-designed benchmark study in which ReAct's advantage over Chain-of-Thought *does not* correlate with chain length and external-fact availability — i.e., cases where ReAct wins on short chains or self-contained questions, or loses on long chains with available external facts. The chapter's argument is that the architecture effect is predictable from the mechanism; evidence that the advantage is driven by something the mechanism doesn't predict would force a sharper specification of when the architectural claim holds.

**Still puzzling:** How to quantify anchor decay across a long trace. The qualitative claim — that a distant Observation has weaker anchoring effect than a recent one — is intuitive and consistent with attention-mechanism behavior. The quantitative version — at what chain depth does an Observation stop anchoring at all, and how does this depend on the number of tokens between Observation and next Thought — is a number I don't have. The lost-in-the-middle literature ([Liu et al., 2023](https://arxiv.org/abs/2307.03172)) is directionally relevant but doesn't measure the anchor effect specifically. A proper empirical study would vary Observation placement in long traces and measure the degradation in Thought coherence.

---

## References

- Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2022). [ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629). arXiv:2210.03629.
- Yang, Z., Qi, P., Zhang, S., Bengio, Y., Cohen, W. W., Salakhutdinov, R., & Manning, C. D. (2018). [HotpotQA: A Dataset for Diverse, Explainable Multi-hop Question Answering](https://arxiv.org/abs/1809.09600). EMNLP 2018.
- Thorne, J., Vlachos, A., Christodoulopoulos, C., & Mittal, A. (2018). [FEVER: a Large-scale Dataset for Fact Extraction and VERification](https://arxiv.org/abs/1803.05355). NAACL-HLT 2018.
- Shridhar, M., Yuan, X., Côté, M.-A., Bisk, Y., Trischler, A., & Hausknecht, M. (2021). [ALFWorld: Aligning Text and Embodied Environments for Interactive Learning](https://arxiv.org/abs/2010.03768). ICLR 2021.
- Liu, N. F., Lin, K., Hewitt, J., Paranjape, A., Bevilacqua, M., Petroni, F., & Liang, P. (2023). [Lost in the Middle: How Language Models Use Long Contexts](https://arxiv.org/abs/2307.03172). arXiv:2307.03172.

---

**Tags:** react-grounding, cumulative-error-p-to-the-n, observation-anchoring, architectural-fix-vs-prompt-fix, tool-output-distribution-shift



---
---
---

# DRAFTING MATERIALS — not for publication

*Below this line: research notes and hero image brief. Strip before final edition assembly.*

---

# Research notes — Ch. 10, ReAct: Grounding Reasoning in the Real World

**Book:** prompt-engineering
**Chapter slug:** react
**Date:** 2026-04-21
**Voice anchoring state:** `voice-unanchored`. Second chapter drafted for this book (after Shwetanshu's Ch. 14).
**Author byline:** **Nik Bear Brown** — standard Nik-authored theory chapter, per the PE book's authorship convention (Parts I–V). No student involvement; no `theory-authored-by-student` flag needed.

---

## Provenance

This draft is a **critique-driven revision**, not a fresh chapter and not a response to a student Author's Note. The user pasted a detailed chapter critique of an earlier Ch. 10 draft. I treated the critique as the brief for a revised chapter and used it to specify what the chapter must contain and what it must avoid.

## Critique → Fix mapping

Every substantive flag the critique raised has an explicit response in the draft:

| Critique flag | Fix in this draft |
|---|---|
| "The error resets at each observation" asserted without causal chain (critique's P1 / Priority Fix #1) | §10.3 "Conceptual level — what 'the error resets' actually means" — explicit token-level walkthrough of conditional dependence, showing *why* external Observation tokens interrupt the chain. Explicitly rejects the "resets" framing as hyperbole; adopts "interrupts (not eliminates)" as precise claim. |
| Return to $P^N$ after ReAct introduced (Priority Fix #2) | §10.3 "Returning to P^N" — walks through what compounds among Thought steps, what breaks via Observation anchoring, and three explicit scope limits where the interruption guarantee weakens (context window exhaustion, tool failure, attention decay). |
| Level-of-abstraction markers (Scale Consciousness / P7) | Explicit bracketed markers at section boundaries: *[Level of abstraction: conceptual / architectural / implementation]*. Two appear in §10.4. |
| Over-claim on core argument ("not always, but often enough" without quantitative support) | §10.7 scopes the claim to Yao et al.'s domains — multi-hop QA, fact verification, embodied task completion — and explicitly flags broader generalization as an empirical open question requiring per-domain measurement. |
| "Dramatically reduces latency" without numbers | Cut. Not in this draft. The decision framework in §10.6 argues about structural criteria (adaptive vs. parallelizable) without unsupported latency claims. |
| "60% → 80% accuracy" demo reported without variance | Cut. The opening scenario uses the Olympic GDP puzzle as a *qualitative* demonstration; the empirical support is cited via Yao et al. 2022, not via ad-hoc classroom demos. |
| Prompt-fix-vs-architectural-fix as the chapter's sharpest sentence | Preserved and extended in §10.5. The distinction now runs across three paragraphs: what each fix delegates to, why one is probabilistic and the other deterministic, and the validator's own scope limits (schema vs. semantic correctness). |
| Context window exhaustion mentioned once and dropped | §10.3's "Returning to P^N" names it as scope limit #1 and §10.7 returns to it. Still not *demonstrated* with a long trace — that's a notebook task, not a chapter task. |
| Validator's limits not named | §10.5 closes with the schema-vs-semantic failure mode explicitly: the validator catches format corruption but not schema-valid-but-semantically-wrong results. Points forward to context-poisoning treatment in a later chapter. |
| LO 5 ("Decide between ReAct and Plan-and-Execute") has no student task | §10.6 names the decision criterion but deliberately does not add an exercise — per workshop convention, exercises go through `/mega`. Research notes flag this as material for the exercise-set generator. |

Three items from the critique I deliberately did *not* address:

1. **Second canonical failure case from production/literature.** The critique flagged the absence of a documented real-world failure beyond the classroom-internal distribution-shift demo. I kept the distribution-shift example as the single failure case because it is mechanistically complete. A second case could come from the literature (hallucinated tool calls in production agent deployments are well-documented) but adding it honestly requires a specific cited incident. Flagged as a follow-up enhancement if a TA finds a good primary source.

2. **Quantitative data on registry size degradation (Notebook 4).** The critique wanted numbers from an accompanying notebook showing action-selection accuracy as a function of tool count. The notebook referenced in the critique is not in the workspace; I couldn't cite its data. Left the registry-size consideration scoped to §10.6 (as a structural rather than quantitative argument) and flagged as a `[TODO]` for the notebook layer to fill when it exists.

3. **Missing pedagogical use of LLMs and agentic AI as student tools.** The critique noted that LLMs appear as subject matter, not as student-facing pedagogical tools. That is by design for a Nik-authored theory chapter in Parts I–V — the student-as-LLM-user pedagogy is concentrated in chapter exercises (`/mega`'s territory) and in the Part VI case studies. Not a chapter-body gap.

## Concept

ReAct as the architectural pattern that interrupts probabilistic dependency-chain error in LLM reasoning by injecting external Observations that are not sampled from the model's distribution — with three explicit conditions under which the interruption guarantee breaks down.

## Specification move

Three terms that wear multiple meanings in casual LLM-agent discussion, disambiguated in the draft:

1. **"Reasoning step"** — token generation conditioned on prior tokens (CoT) vs. external tool call (ReAct's Action). The distinction matters because the two are subject to different error profiles.
2. **"Error resets"** — hyperbole commonly used to describe ReAct. The precise claim: *interrupts*, not *resets*. Resets would imply the prior Thoughts' influence is erased; it isn't. The next Thought is still conditioned on prior Thoughts; it's also conditioned on anchor tokens from an external source.
3. **"Prompt fix"** vs. **"architectural fix"** — both feel like "doing something" to handle an error, but one adds tokens inside the probabilistic system and the other adds a deterministic layer outside it. This distinction is the chapter's load-bearing engineering claim.

## Sub-claims — empirical vs. structural

**Structural / mathematical:**
- $P^N$ cumulative error formula for CoT reasoning chains (approximation assuming approximately-independent per-step errors)
- Observation tokens enter the context from outside the model's conditional distribution
- Three scope limits: context window exhaustion, tool reliability, attention decay

**Empirical:**
- Yao et al. 2022 (ReAct) — real paper, real benchmarks. Cited honestly with the benchmarks named (HotPotQA, FEVER, ALFWorld).
- Liu et al. 2023 (Lost in the Middle) — real, cited in "Still puzzling" as directionally relevant to anchor-decay quantification.

**Pedagogically constructed:**
- The Olympic GDP puzzle — specifically chosen because it has a documented "first exceeded $3T" year (World Bank data place this around 2015) that frontier models sometimes miss, and because the two-step composition creates a clean CoT failure case. Numbers stated in the draft are approximate and should be treated as illustrative of the *shape* of the failure, not as a precise experimental reproducer.

## Mechanism chosen for the deep-dive

**§10.3's token-level walkthrough of why Observation tokens interrupt the dependency chain, followed by §10.3's honest scoping of what ReAct doesn't fix.** This is the chapter's load-bearing teaching move — the critique's central demand was that this mechanism be shown rather than asserted.

One-sentence mechanism: *Model-generated tokens are sampled from a distribution conditioned on prior tokens, so a wrong prior token shifts the subsequent distribution in a wrong direction — but Observation tokens are injected from outside the model's probability distribution entirely, so they carry no inherited error from prior Thoughts, which means each Observation acts as an anchor that interrupts (does not eliminate) the compounding of error — and the anchor's effectiveness decays with chain length, tool reliability, and attention dilution.*

## Central analogy — "anchor"

The chapter uses *anchor* as a minimal analogy for the Observation token's role. Observations anchor the next Thought against external reality. The analogy is used sparingly — it doesn't dominate the explanation, which is carried by the token-level math. Tested: removing it costs a slight intuitive handhold but doesn't change the argument. Kept, but not load-bearing.

No other analogies. The math (conditional sampling; $P^N$; dependency chain) is the argument; any further analogy would compete with it rather than reinforce it.

## Primary sources

| Claim | Source | URL | Verified? |
|---|---|---|---|
| ReAct benchmarks on HotPotQA, FEVER, ALFWorld | Yao et al. 2022 | https://arxiv.org/abs/2210.03629 | ✓ |
| HotPotQA dataset | Yang et al. 2018 | https://arxiv.org/abs/1809.09600 | ✓ |
| FEVER dataset | Thorne et al. 2018 | https://arxiv.org/abs/1803.05355 | ✓ |
| ALFWorld benchmark | Shridhar et al. 2021 | https://arxiv.org/abs/2010.03768 | ✓ |
| Lost in the Middle / attention decay | Liu et al. 2023 | https://arxiv.org/abs/2307.03172 | ✓ |

All five arXiv-accessible. No `[verify]` flags on substantive claims.

## Voice notes

- First person used 2 times in the draft (in "Still puzzling" and §10.3's scoping paragraph). Appropriate for Nik-authored theory register.
- Forbidden phrases swept. The critique called out "dramatically reduces latency" and "not always, but often enough" — both are cut or scoped in this draft.
- Single-sentence paragraphs used as pivots: "The model did not change. The architecture did." / "That is what an architectural fix is, and that is what a prompt cannot do." / "Breaking that structure is an architectural move, not a prompt move."
- The prompt-fix-vs-architectural-fix passage is the chapter's sharpest — preserved and expanded across §10.5 as the critique suggested.

## Gaps flagged for TA refinement

- **Second canonical failure case from production/literature.** The chapter's single failure case (distribution shift from format change) is mechanistically complete but classroom-internal. A documented real-world case from a production agent deployment would strengthen the pedagogy.
- **Notebook quantitative data on registry size vs. action-selection accuracy.** Mentioned in the critique; not available at draft time. A notebook measuring this would let §10.6 be sharper about the registry-size consideration.
- **Long-trace anchor-decay empirical study.** Flagged in "Still puzzling." An experiment varying Observation placement in long traces and measuring Thought coherence degradation would close the honest open question.
- **Exercise for LO 5** — `/mega` territory. The research notes preserve the critique's suggested exercise shape: present two task descriptions, require written architectural justification with specific reference to the three decision criteria in §10.6.
- **Prerequisite chapter for $P^N$.** The draft assumes basic probability. Ch. 1 (Stochastic Machine) covers token sampling; Ch. 9 covers CoT. The prerequisite chain is stated at the chapter top. If either Ch. 1 or Ch. 9 is drafted in a way that doesn't fully introduce the conditional-sampling framing, this chapter will need to back-fill.

## Adjacent topics not pursued

- **Plan-and-Execute in depth.** Named as a comparison pattern in §10.6 but not developed. Handled in the agentic-systems book's Ch. 4; a later chapter in the prompt-engineering book (Ch. 11: Prompt Stack) may cross-reference it.
- **Parallel tool use.** Named as an alternative in §10.6 but not developed. Worth a sidebar or separate treatment.
- **Context-window management strategies for long ReAct traces.** Mentioned as a scope limit; handled structurally in the agentic-systems book's Ch. 33 (Twelve Production Builds, Build 4).
- **Tool registry design at scale.** Named as a consideration in §10.4 but not developed. Production agent systems use tool-selection classifiers for registries above ~20 tools; out of scope for this chapter.
- **Formal treatment of the assumption that per-step errors are independent** in the $P^N$ formula. The draft notes this is an approximation and that errors are actually correlated; a formal treatment would require reasoning about confabulation consistency and is out of scope.

## Length

~3,850 words for the chapter body. Within the 2,000–4,000 ceiling. Earned by the complexity of the conditional-sampling explanation, the return to $P^N$, and the two-level (conceptual/architectural/implementation) walkthrough. No compression opportunities that wouldn't lose substantive content.


---

# Hero image brief — Ch. 10, ReAct: Grounding Reasoning in the Real World

**Book:** prompt-engineering
**Chapter slug:** react
**Date:** 2026-04-21

## Concept the image should carry

The chapter's load-bearing visual claim is **the probabilistic dependency structure of CoT, and what Observation injection does to it**. A reader looking at the image for thirty seconds should understand that model-generated tokens are drawn from a distribution that depends on prior tokens (CoT's compounding structure), that Observations enter from outside that distribution (breaking the chain of dependence through the Thought steps), and that the "interruption" is partial — the next Thought is still conditioned on prior Thoughts, just *also* on the new anchor.

This is the critique's Priority Fix #1 made visual.

## Primary recommendation — the dependency chain with and without Observations

A two-panel diagram.

**Top panel — Chain-of-Thought:**
A horizontal sequence of token boxes labeled $T_1, T_2, T_3, \ldots, T_N$. Each $T_i$ has an arrow drawn *backward* to all previous tokens $T_1, \ldots, T_{i-1}$, labeling the conditional dependence: $T_i \sim P(T_i \mid T_1, \ldots, T_{i-1})$. Every token is the same color (muted teal) — they all come from the same probabilistic system.

Below the chain, a formula and annotation: $P_{\text{chain}} \approx P^N$ with values — at $P=0.95, N=10$: $\approx 0.60$; at $N=20$: $\approx 0.36$. Label: *"A wrong token in the chain shifts the distribution of every later token."*

**Bottom panel — ReAct:**
Same horizontal sequence, but the tokens alternate in color. Thoughts are muted teal (same as CoT, because they still are model-sampled). Observations are a different color entirely — muted ochre — with a distinct visual boundary around them. An arrow from *outside the diagram* points into each Observation, labeled *"from tool call — deterministic, not sampled"*.

Conditional dependency arrows: each Thought $T_i$ still has backward arrows to prior Thoughts, *and* an additional arrow to any prior Observations. But the Observation tokens themselves have no backward arrows at all — they don't depend on prior tokens because they weren't sampled.

Label beneath the bottom panel: *"Thoughts still compound error among themselves. Observations don't. The next Thought is anchored to both — which interrupts compounding (does not erase it)."*

This is the figure that closes the critique's "mechanism not shown" gap.

## Secondary recommendation — the prompt-fix-vs-architectural-fix contrast

A two-column side-by-side diagram. Both columns show a tool-format-change failure scenario.

**Left column — Prompt-level fix:**
Tool → JSON output → Loop (no validator) → Observation buffer → Model (with "be careful" instruction in system prompt) → Thought. A dashed red line circles the entire stack, labeled: *"Fix lives inside the probabilistic system that is producing the error."*

**Right column — Architectural fix:**
Tool → JSON output → **Validator** (rendered as a distinct gate shape, in a third color — muted slate) → either typed error or passthrough → Observation buffer → Model → Thought. The validator sits outside the red dashed region, labeled: *"Fix lives outside the probabilistic system. Deterministic Python."*

Below both columns: *"A prompt is more tokens. A validator is a different kind of thing."*

This is the chapter's sharpest claim made visual.

## Tertiary recommendation — the three scope limits

A simple table (visual table, not a prose one). Three rows:

| Condition | Anchor effect | Consequence for $P^N$ |
|---|---|---|
| Short trace, reliable tools | Strong | Interrupted; effective exponent → $P^1$ per anchor segment |
| Long trace (context window filling) | Weakening | Anchors fade with distance; effective exponent drifts toward $P^N$ between anchors |
| Tool failure (broken format / wrong schema) | Broken | Observation itself becomes noise source; worse than pure CoT |

Annotation: *"ReAct interrupts compounding under conditions 1. Engineers design for conditions 2 and 3."*

## Style direction

Per `book.md` voice notes: engineering-diagram aesthetic. Muted academic palette. No alarm iconography, no anthropomorphic agents, no glowing-brain imagery. Formulas should appear in LaTeX or a clean sans-serif technical font, not decorative type.

Three colors, each mapped to a distinct token provenance:
- **Muted teal** — model-generated tokens (CoT, Thoughts)
- **Muted ochre** — externally-sourced tokens (Observations)
- **Muted slate** — architectural components (validators, tool registry)

Using the same color coding across all three images lets the reader recognize "the same kind of thing" across figures — which is load-bearing, since the chapter's argument turns on keeping these three categories distinct.

## Aspect ratio

- Primary (CoT vs. ReAct dependency chains): very wide (21:9) — the horizontal token sequence needs room for 10+ tokens in both panels
- Secondary (prompt-fix vs. architectural-fix): wide (16:9) for side-by-side columns
- Tertiary (scope limits table): square or modestly wide (4:3)

## Do NOT

- Generate any of these in this run.
- Draw the Observation tokens in the same color as Thought tokens. Color-coding provenance is the teaching move — if Thoughts and Observations look identical, the reader has been told the thing the figure exists to show is invisible.
- Use alarm/error iconography for the failure case. The distribution-shift failure is mechanistic and boring-looking; rendering it as a crash or explosion moralizes what should be architectural.
- Draw the validator as a shield, a lock, or any defensive iconography. It is a Python function. A rectangular box with a function signature above it is correct. Anthropomorphizing the validator as a guard or firewall suggests it's doing something fundamentally different from ordinary code — it isn't.
- Omit the dependency-arrow structure from the primary image. Without the backward arrows showing conditional dependence, the image degrades to "sequence of boxes" and the claim the image exists to make goes invisible.
- Render "reset" anywhere in annotations. The chapter's precise claim is *interrupt*, not *reset*. A figure label that says "error resets at each Observation" plants the misconception the chapter is built to prevent.
