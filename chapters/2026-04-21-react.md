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

## A note about AI

ReAct is a reasoning pattern, and patterns are exactly the kind of thing the model can imitate without using. A chain-of-thought trace that looks like ReAct may not be one.

Where the model genuinely helps: walking through the difference between an action that gathers new information and an action that restates known information, on a specific worked example. The model is good at producing clean instances of each, which makes the contrast visible.

Where the model does damage: producing reasoning traces that look like ReAct but do not actually interleave action with reasoning — the trace fakes the structure without performing the function. Models are particularly fluent at producing this kind of pseudo-trace, and downstream evaluators (including you) can be fooled by the texture.

The rule: a ReAct trace is only ReAct if removing the action steps would change the conclusion. Test that property when you read traces, including the ones the model produces for you.

---

## AI Wayback Machine

**Allen Newell** was co-built Logic Theorist with Herbert Simon in 1956 — and developed the "problem space" framework that ReAct-style reasoning patterns descend from.

**Run this:**

```
Who is Allen Newell, and how does their work connect to ReAct reasoning we covered in this chapter? Keep it to three paragraphs. End with the single most surprising thing about their career or ideas.
```

→ Search **"Allen Newell"** on Wikipedia.

**Now make the prompt better.** Try one of these:

- Ask it to apply Allen Newell's framework to a specific prompt-engineering decision.
- Add a constraint: "Answer including criticisms or limits of Allen Newell's framework."

What changes? What gets better? What gets worse?
