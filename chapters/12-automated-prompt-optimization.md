> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft. Drafted against the Ch. 6 (Persona Patterns) anatomy/voice model.
>
> **Aging-risk flag (per TIKTOC):** automated-optimization figures (DSPy / MIPRO / OPRO / APE / the July-2025 case study) are 2022–2025 and fast-moving. Deltas are cited with named baselines and benchmark; preprints flagged. The *mechanism spine* (treat prompting as metric-driven search; precondition is a labeled eval set + a scalar metric) is the stable core. Current library names (MIPROv2 as DSPy's default) age fastest — quarantined to labeled sentences.

---

# Chapter 12 — Automated Prompt Optimization: The Post-Manual Era

*When the Machine Writes a Better Prompt Than You Would Have*

**Author:** Nik Bear Brown
**Editor:** Nik Bear Brown

---

## Suggested titles

1. **Automated Prompt Optimization: The Post-Manual Era**
2. **Take a Deep Breath: How a Machine Found a Prompt No Human Would Have Written**
3. **Declare the *What*, Compile the *How*: Prompting as a Metric-Driven Search Problem**

---

## TL;DR

If you can write down (1) a *typed contract* — what goes in, what comes out — and (2) a *scalar metric* that scores an output against a labeled example set, then prompting stops being wordsmithing and becomes a search problem a machine can solve. Frameworks like DSPy let you declare the task as a **Signature** and hand a control flow to an **optimizer** (MIPROv2, APE, OPRO) that searches instruction-and-demonstration space for the prompt that maximizes your metric. The famous discovered prompts — *"Take a deep breath and work on this problem step by step"* (80.2% on GSM8K) — are the punchline: the optimum is a model-specific point in token-space no human intuition would have guessed. But the precondition is the boundary condition. **No metric, no eval set, no high-volume task to amortize the search cost — then manual prompting is correctly where you stop, not where you fail.**

---

## Learning objectives

By the end of this chapter you should be able to:

1. **(Understand)** Explain why a labeled eval set plus a scalar metric is the precondition that converts prompting from an art into an optimization problem.
2. **(Apply)** Express a task as a DSPy **Signature** (typed input → output contract) and identify the metric the optimizer will climb.
3. **(Analyze)** Place the major optimizers (APE, OPRO, ProTeGi/TextGrad, MIPRO, Promptbreeder/EvoPrompt) in a 2×2 of *search strategy* × *what is optimized*.
4. **(Evaluate)** Decide whether a given task should be hand-tuned or auto-optimized, using a four-question gate.
5. **(Evaluate)** Read a reported optimization result critically — separate the optimizer's contribution from the eval-harness discipline, and name the re-optimization-debt and overfitting failure modes.

## Prerequisites

Ch. 9 (Prompt Brittleness and the Discipline of Evaluation) — the eval-set-and-metric machinery this chapter mechanizes. Ch. 5 (Architect Mindset) — structured prompts as composable systems. Ch. 8 (Reasoning and Range Patterns) — Chain-of-Thought, the technique the discovered prompts perturb. Basic familiarity with the idea of optimizing a black-box objective (no derivatives required).

---

## 12.1 The prompt a human wouldn't have written

In September 2023, a team at Google DeepMind ran an optimization loop over the instruction text fed to a large language model on grade-school math problems. The loop was mechanical: propose a candidate instruction, score it on a held-out set of problems, feed the score back, propose again. After a number of rounds, the loop converged on a sentence. The sentence was:

> *"Take a deep breath and work on this problem step by step."*

Prefixed to the model's reasoning, that instruction reached **80.2%** on GSM8K (a grade-school math benchmark) with PaLM 2-L — versus **71.8%** for the standard *"Let's think step by step"* and roughly **34%** with no special instruction at all ([Yang et al., 2023](https://arxiv.org/abs/2309.03409)).

Stop and notice what is strange here. No human would have *reasoned their way* to "take a deep breath." A model does not have lungs. The phrase carries no logical content about arithmetic. And yet it beat the carefully-designed human prompt by more than eight points on a hard benchmark. A year earlier, a different optimization loop had found another oddly-shaped winner — *"Let's work this out in a step by step way to be sure we have the right answer"* — which beat the human baseline on MultiArith (78.7 → 82.0) and GSM8K (40.7 → 43.0) ([Zhou et al., 2023](https://arxiv.org/abs/2211.01910)).

These prompts were *found*, not *thought*. They are points in a token-space landscape that a search procedure climbed to and a human intuition would have walked right past. That is the whole chapter in one observation: **once you can score an output, prompting becomes an optimization problem, and an optimizer will sometimes beat you — by going somewhere you would not have gone.**

The rest of this chapter pulls that observation apart. What is the objective being optimized? What is the search space? What is the precondition that has to hold before any of this works — and what happens, predictably, when it doesn't? And the load-bearing decision: when is it worth handing the prompt to a machine, and when is hand-tuning still correctly the answer?

---

## 12.2 The reframe: prompting as a search problem

Consider what a human prompt engineer actually does. They write an instruction. They run it on a few examples. They eyeball the outputs. They notice a failure, edit a word, run it again. This is a loop — *write → observe → tweak → repeat* — and it is recognizably an optimization loop, just one driven by human intuition and judged by eyeball.

The reframe is to make the loop explicit and mechanical. Replace "eyeball the outputs" with a **scalar metric**: a function that takes an output and a reference and returns a number. Replace "a few examples" with a **labeled eval set**: input-output pairs you trust. Replace "edit a word" with a **proposer**: something that generates candidate prompts. Now the loop is:

$$
\text{prompt}^\* = \arg\max_{\text{prompt} \,\in\, \mathcal{P}} \; \frac{1}{|\mathcal{D}|}\sum_{(x,y)\in\mathcal{D}} \text{metric}\big(\,\text{LM}(\text{prompt}, x),\; y\,\big)
$$

In words: over the space $\mathcal{P}$ of possible prompts, find the one that maximizes the average metric across your eval set $\mathcal{D}$. That is the entire mathematical content of automated prompt optimization. Everything else — Bayesian search, evolutionary mutation, textual gradients — is a *strategy for searching $\mathcal{P}$ without evaluating every point*, because $\mathcal{P}$ is astronomically large and each evaluation costs real LLM calls.

Two things in that equation are not the optimizer's job — they are yours. You must supply $\mathcal{D}$ (the eval set) and you must supply the metric. **This is the precondition, and it is the boundary of the whole enterprise.** No metric, no $\arg\max$. We return to this in §12.6 because it is the named failure mode, not a footnote.

### The Signature: declare the *what*, let the compiler find the *how*

The clearest operationalization of the reframe is the **Signature**, the central abstraction in DSPy ([Khattab et al., 2023](https://arxiv.org/abs/2310.03714), ICLR 2024). A Signature is a *typed input → output contract* — it states what the task consumes and produces, not how to phrase the request:

```
question -> answer
```

or, with field descriptions:

```
context, question -> answer
   context:  relevant passages retrieved for the question
   question: a natural-language question
   answer:   a short factual answer grounded in the context
```

Notice what the Signature does *not* contain: no instruction string, no few-shot examples, no "you are a helpful assistant," no "let's think step by step." Those are the *how*. The Signature is the *what*. You declare the contract; a **compiler** (in DSPy's vocabulary) searches for the instruction text and the demonstrations that make some downstream metric as high as possible.

This is, almost exactly, Grace Hopper's 1952 argument for the compiler, transplanted onto language models: humans should state *what* they want and let the machine generate the low-level instructions. (The original DSPy framework paper reports compositions of its modules raising GPT-3.5 quality from **33% → 82%** on GSM8K and **32% → 46%** on HotPotQA multi-hop QA — and, strikingly, making a llama2-13b-chat "competitive with GPT-3.5 by simply compiling programs." [Khattab et al., 2023](https://arxiv.org/abs/2310.03714).) The same Signature compiles to *different* prompt strings for different model families — a terse instruction with three demonstrations for one model, a verbose instruction with six for another. Same *what*, different *how*. The lineage traces back to the DSP precursor ([Khattab et al., 2022](https://arxiv.org/abs/2212.14024)), which framed retrieval-and-language-model pipelines as "high-level programs."

### Misconception: "the optimizer writes a clever prompt; I could have written it myself"

Tempting, and mostly wrong. The discovered prompts in §12.1 are the counterexample. "Take a deep breath" is not clever in any human sense — it is a model-specific token sequence that happens to nudge the next-token distribution toward more careful arithmetic for *that model version*. The optimizer is not being a better wordsmith than you. It is doing something you structurally cannot do by hand: evaluating hundreds of candidates against a metric and keeping the empirical winner, including winners that look like nonsense.

---

## 12.3 The optimizer zoo, in one grid

Between 2022 and 2024 the field produced a cluster of optimizers. They differ along two axes: **how they search** $\mathcal{P}$, and **what part of the prompt they optimize** (the instruction text, the few-shot demonstrations, or both). The grid:

| | Optimizes **instructions** | Optimizes **demonstrations** | Optimizes **both** |
|---|---|---|---|
| **Propose-and-score (LLM-as-proposer)** | **APE** — propose candidate instructions, score each by another LLM's task performance, keep the best | — | — |
| **Trajectory-feedback (history in meta-prompt)** | **OPRO** — feed prior solutions + their scores back into a meta-prompt; the LLM proposes new candidates | — | — |
| **Textual "gradient" (criticize, then edit)** | **ProTeGi / APO**, **TextGrad** — minibatches produce natural-language criticisms ("gradients"); the prompt is edited in the opposite semantic direction | — | — |
| **Evolutionary (mutate a population)** | **Promptbreeder, EvoPrompt** — an LLM mutates a *population* of prompts; in Promptbreeder, the mutation-prompts themselves evolve | — | — |
| **Bayesian search over joint space** | — | — | **MIPRO** — jointly optimize free-form instructions *and* few-shot demonstrations per module, via Bayesian optimization over the search space |

A few entries deserve a sentence each, because their mechanisms are genuinely distinct:

- **APE** (Automatic Prompt Engineer; [Zhou et al., 2023](https://arxiv.org/abs/2211.01910), ICLR 2023) treats the instruction as a *program* to be synthesized: an LLM proposes candidate instructions, each is scored by task performance, the best survives. The paper — titled, accurately, *Large Language Models Are Human-Level Prompt Engineers* — matched or beat human-annotator instructions on **19 of 24** NLP tasks. It produced the "let's work this out in a step by step way" prompt.

- **OPRO** (Optimization by PROmpting; [Yang et al., 2023](https://arxiv.org/abs/2309.03409), ICLR 2024) puts the *optimization trajectory* — prior candidate solutions and their scores — directly into the meta-prompt, so the LLM proposing the next candidate can see what worked. It produced "take a deep breath," and reported optimized prompts beating human-designed ones by up to **8%** on GSM8K and up to **50%** on Big-Bench Hard.

- **ProTeGi/APO** ([Pryzant et al., 2023](https://arxiv.org/abs/2305.03495), EMNLP 2023) and its generalization **TextGrad** ([Yuksekgonul et al., 2024](https://arxiv.org/abs/2406.07496); published in *Nature*, 2025) borrow the *shape* of gradient descent. A minibatch of failures produces a natural-language criticism — a "textual gradient" — and the prompt is edited "in the opposite semantic direction." TextGrad generalizes this to backpropagate textual feedback through an arbitrary compound system (prompts, code, even molecules as "variables"). It is the cleanest "autodiff for LLM systems" analogy in the literature; treat the analogy as illuminating, not literal — there is no chain rule, only an LLM reading a critique and editing.

- **Promptbreeder** ([Fernando et al., 2023](https://arxiv.org/abs/2309.16797)) and **EvoPrompt** ([Guo et al., 2023](https://arxiv.org/abs/2309.08532), ICLR 2024) are evolutionary: maintain a *population* of prompts, mutate, select the fittest. Promptbreeder's twist is self-referential — the mutation-prompts themselves evolve.

- **MIPRO** ([Opsahl-Ong et al., 2024](https://arxiv.org/abs/2406.11695), EMNLP 2024) is the one most readers will actually run, because it is DSPy's recommended optimizer. **An attribution point worth getting right:** the *paper's* algorithm is named **MIPRO** (Multi-prompt Instruction PRoposal Optimizer); **MIPROv2** is the *implementation* shipped in the DSPy library as its default. It is not a Databricks-owned flagship product — DSPy remains the open-source, Stanford-rooted project. (Omar Khattab joined Databricks personally in 2024; Databricks backs the ecosystem, including DSPy 3.0 in 2025. That is sponsorship, not acquisition. `[verify ongoing]`) Mechanism: MIPRO jointly optimizes instructions *and* demonstrations per module — *without module-level labels or gradients* — using program-and-data-aware instruction proposal, a stochastic mini-batch evaluation surrogate, and **Bayesian optimization** over the search space. It beat baseline optimizers on **5 of 7** multi-stage programs with Llama-3-8B, by as much as **13%** accuracy.

The Bayesian engine inside MIPRO has a deep ancestor: the expected-improvement framework formalized by the Lithuanian mathematician **Jonas Mockus** in the 1970s–80s, for finding the best setting of a system you can only probe a few times, expensively. That is precisely the optimization regime here — each "probe" is a batch of LLM calls that costs money, so you want a surrogate model that says where to probe next.

### Misconception: "these are all basically the same; pick whichever"

They are not. The axis that matters in practice is *cost per useful step*. Evolutionary methods evaluate many candidates and are sample-hungry. Bayesian methods (MIPRO) spend modeling effort to evaluate fewer candidates. Textual-gradient methods get a directed edit from each failure, which can be efficient when the metric exposes *why* an output failed, and useless when it only exposes *that* it failed. There is no apples-to-apples leaderboard across these methods — each paper evaluates on different tasks — so treat the choice as a function of your eval budget and how informative your metric's failures are.

---

## 12.4 A worked example: optimizing a "80 Days to Stay" extractor

Our running SEC-data case, **"80 Days to Stay,"** needs to pull a single number from filings: *given the text of a 10-K risk-factors section, what is the company's stated going-concern runway in days?* This is a good automation candidate, and walking through *why* makes the precondition concrete.

**Step 1 — the Signature (the *what*).**

```
filing_text -> runway_days
   filing_text: the risk-factors section of a 10-K
   runway_days: integer number of days of stated going-concern runway, or -1 if not stated
```

**Step 2 — the metric (the part that is yours).** We need a function returning a number. The brittle version is exact match: `1 if predicted == gold else 0`. A better version tolerates near-misses and penalizes confident wrong answers:

```
def metric(pred, gold):
    if gold == -1:                      # filing states no runway
        return 1.0 if pred == -1 else 0.0
    if pred == -1:                      # model said "not stated" but it was
        return 0.0
    err = abs(pred - gold) / gold
    return max(0.0, 1.0 - err)          # 1.0 at exact, decaying with relative error
```

Writing this metric *is the work*. Notice what it forced us to decide: how to handle "not stated," whether a 5%-off answer is partially credited, whether confident-and-wrong is worse than abstaining. These are task-decomposition decisions that hand-prompting lets you avoid (and therefore lets you get silently wrong). One open empirical question in the field is exactly this: how much of an "optimization win" is the Bayesian search, and how much is simply the *discipline of being forced to write the metric*? No clean ablation isolates the two ([see §12.7]).

**Step 3 — the eval set (also yours).** Assemble, say, 60 labeled filings: 40 for the optimizer to train against, 20 held out to measure overfitting. Without these, Step 4 has nothing to climb.

**Step 4 — run the optimizer.** Hand the Signature, the metric, and the trainset to MIPROv2. It proposes instructions ("Extract the going-concern runway... return -1 if the filing does not state one..."), draws candidate few-shot demonstrations from the trainset, and uses Bayesian search to find the instruction + demonstration set that maximizes the average metric. It emits a compiled prompt.

**Step 5 — measure on the held-out 20.** If the held-out score is much lower than the trainset score, the optimizer overfit — it found a prompt tuned to the 40 training filings, not to going-concern extraction in general. This is the overfitting failure mode, and it is why you keep a holdout.

The payoff: you ran this loop *once*, and now "80 Days to Stay" extracts runways from thousands of filings on a compiled prompt that beats what you'd have hand-written — *and* you have a number that says so. That is the regime where automation pays.

---

## 12.5 The decision gate: when to optimize, when to hand-tune

Here is the chapter's load-bearing decision, as four questions. Answer all four "yes" and automate; any "no" sends you to the manual lane.

1. **Can you write a scalar metric?** A function that scores an output against a reference and returns a number. If your objective is "good writing" or "tasteful tone" and you cannot reduce it to a number, the optimizer has nothing to climb.
2. **Can you assemble a labeled eval set?** Even 30–60 trustworthy examples. No examples, nothing to evaluate candidates against.
3. **Will you run this task many times?** Optimization burns hundreds-to-thousands of LLM calls. A one-off task does not amortize that cost; just prompt it by hand.
4. **Is the task and model stable enough to amortize?** If you will swap models next month, the optimized prompt may not transfer (§12.6), and you pay the search cost again.

```
                  ┌─────────────────────────────────────┐
   task  ───────► │ Metric? Eval set? High volume? Stable?│
                  └───────────────┬─────────────┬─────────┘
                            all yes│             │any no
                                   ▼             ▼
                        AUTOMATED lane     MANUAL lane
                   Signature → metric →    write prompt → eyeball
                   optimizer → compiled    outputs → tweak → repeat
                   prompt → measure        (human intuition, no metric)
```

This gate is not a confession of automation's weakness. It is the same falsifiable-claim discipline the whole book argues for, applied to the meta-decision: *the conditions under which the method works are stated in advance and are checkable.*

### The honest case study: gains are real but mixed

A July-2025 preprint, *Is It Time To Treat Prompts As Code?*, ran DSPy optimization across five practitioner use cases ([arXiv:2507.03620](https://arxiv.org/abs/2507.03620) — label this a **practitioner empirical case study, preprint**). The results are the right antidote to hype. Optimization produced a **large** gain on one case (a prompt-evaluation criterion, 46.2% → 64.0%), a **moderate** gain on routing agents (85.0% → 90.0%), and **minor or negligible** gains on guardrails and on hallucination detection in code. And tellingly: optimizing a prompt and then swapping to a *cheaper* model did **not** transfer the gain. The honest summary is *"gains in some cases, marginal-or-none in others"* — not "consistent improvement over manual."

This is the texture you should expect. Automated optimization is a production-systems tool that pays off on metricizable, high-volume, stable tasks. It is not a general-purpose replacement for thinking about your prompt.

---

## 12.6 Two named failure modes

The decision gate guards against using automation where it can't help. Two failure modes bite even when you use it correctly.

**Re-optimization debt.** Optimized prompts are tuned to a specific model version. The discovered prompts in §12.1 are model-specific token sequences — "take a deep breath" worked for PaLM 2-L, and there is no guarantee it transfers to a different model or a later checkpoint. The July-2025 study's "cheaper model didn't inherit the gain" is a concrete instance. **Consequence:** every base-model upgrade potentially incurs a re-optimization cost. This cost is real, recurring, and badly under-reported in the literature — papers report the win, rarely the maintenance.

**Overfitting to the eval set.** The optimizer maximizes the metric *on your eval set*. If your eval set is small or unrepresentative, the compiled prompt can be excellent on those examples and mediocre in production. The defense is the held-out split from §12.4 Step 5, and a healthy suspicion when trainset and holdout scores diverge.

A third, subtler caveat: the *optimizer's own model capability matters*. "Revisiting OPRO" ([arXiv:2405.10276](https://arxiv.org/abs/2405.10276)) reports that small-scale LLMs are weak optimizers — the meta-model proposing candidates needs enough capability to propose good ones. If your proposer is too weak, the search stalls.

### Misconception: "automated optimization removes the human from prompting"

It relocates the human. You stop wordsmithing and start *specifying the objective* — writing the metric, curating the eval set, choosing the holdout. The skill doesn't vanish; it moves up a level of abstraction, from "phrase the request well" to "define what 'good' means as a number." That relocation is the post-manual era: not the absence of human judgment, but its concentration on the objective rather than the wording.

---

## 12.7 What this chapter is really claiming

The strong claim is the reframe: **prompting, on any task you can score, is a metric-driven search problem, and a search procedure can find prompts no human would write.** The discovered prompts prove the existence half. DSPy, MIPRO, APE, OPRO prove the practicality half on benchmarked tasks.

The honest boundary is the precondition. The reframe holds *exactly where the precondition holds* — where a metric and an eval set exist and the task runs often enough and stays stable enough to amortize the search. Outside that region — open-ended generation, taste, one-off requests, fuzzy objectives — there is, as far as the current evidence shows, no automated path, and manual prompting is correctly dominant. That is not the method failing. That is the method's boundary, stated honestly, which is the only way an engineering discipline ever states anything.

The deepest open question is attribution: when DSPy "wins," how much is the Bayesian search and how much is the *discipline of writing the metric*? Building the metric forces task decomposition and surfaces ambiguity you'd otherwise paper over. It is entirely possible that a meaningful share of the reported gains comes from the human being made to think clearly about the objective — which, if true, would only deepen the book's thesis rather than undercut it. The mechanized loop's first and most valuable output may be the clarity it forces *before* the search even begins.

---

## Exercises

1. **(Understand)** In your own words, explain why the equation $\text{prompt}^\* = \arg\max_{\text{prompt}} \frac{1}{|\mathcal{D}|}\sum \text{metric}(\cdot)$ contains two terms the optimizer cannot supply for you. Name them and say what happens to the whole enterprise if either is missing.

2. **(Apply)** Write a DSPy-style Signature for the **Madison** marketing-intelligence task: *given a product description and a target persona, produce three subject-line variants.* Then state honestly whether this task passes the §12.5 decision gate — and if it fails any question, say which and why.

3. **(Analyze)** Take the optimizer grid in §12.3. Pick one task you actually run (or would). For that task, argue which *search strategy* (propose-and-score / trajectory / textual-gradient / evolutionary / Bayesian) fits best, grounding the argument in (a) your eval budget and (b) how informative your metric's failures are.

4. **(Evaluate)** Read the abstract of the July-2025 case study ([arXiv:2507.03620](https://arxiv.org/abs/2507.03620)). For each of its five use cases, classify the reported gain as large / moderate / minor-or-none, and propose one hypothesis for *why* the high-gain cases gained and the low-gain cases didn't. (Hint: think about how cleanly each task's success can be reduced to a number.)

5. **(Create / Apply+)** Implement the §12.4 worked example end to end on any small dataset you can label (it need not be SEC filings — pick any task with checkable answers). Write the metric, assemble a 30/15 train/holdout split, run an optimizer (or, if you lack tooling, *simulate* one by hand-proposing five candidate prompts and scoring them), and report: the trainset-best score, the holdout score, and whether the gap suggests overfitting. Deliver the metric code, the compiled/chosen prompt, and a one-paragraph reading of the numbers.

---

## What would change my mind

A controlled ablation that holds the eval set and metric fixed, then compares (a) the best prompt found by a sophisticated optimizer (MIPRO/OPRO) against (b) the best prompt a skilled human writes *after being forced to write the same metric and inspect the same eval set* — across a representative task suite, including open-ended ones. The chapter claims the optimizer's search does real work beyond the discipline of metric-writing. If the human-with-metric closes most of the gap on most tasks, then the load-bearing value is the *metric discipline*, not the search, and the chapter should be reframed around "write the metric" with the optimizer demoted to a convenience.

## Still puzzling

- **Attribution of the gain.** No clean experiment separates "the Bayesian/evolutionary search found something" from "being forced to write a metric made the human think clearly." Both are plausibly doing work; the field reports their sum.
- **Re-optimization cadence.** As base models update every few months, how often must compiled prompts be re-optimized to hold their gains — and at what cumulative cost? The maintenance side of the ledger is almost never reported.
- **The fuzzy-objective frontier.** For genuinely un-metricizable tasks (taste, voice, nuanced judgment), is manual prompting *permanently* dominant, or is there an automated path through learned/judge-based metrics that the field simply hasn't matured yet?
- **Why "take a deep breath."** We have no mechanistic account of *why* that specific string nudges a specific model toward better arithmetic. We have the empirical result and a plausible "it shifts the next-token distribution" story. The interpretability question — what does that phrase activate — is open.

---

## References

- Khattab, O., Santhanam, K., Li, X. L., Hall, D., Liang, P., Potts, C., & Zaharia, M. (2022). [Demonstrate-Search-Predict: Composing Retrieval and Language Models for Knowledge-Intensive NLP](https://arxiv.org/abs/2212.14024). arXiv:2212.14024.
- Khattab, O., Singhvi, A., Maheshwari, P., Zhang, Z., Santhanam, K., et al. (2023). [DSPy: Compiling Declarative Language Model Calls into Self-Improving Pipelines](https://arxiv.org/abs/2310.03714). arXiv:2310.03714. Accepted ICLR 2024.
- Opsahl-Ong, K., Ryan, M. J., Purtell, J., Broman, D., Potts, C., Zaharia, M., & Khattab, O. (2024). [Optimizing Instructions and Demonstrations for Multi-Stage Language Model Programs](https://arxiv.org/abs/2406.11695). arXiv:2406.11695. EMNLP 2024 (main). *(Paper's algorithm: MIPRO; DSPy implementation: MIPROv2.)*
- Zhou, Y., Muresanu, A. I., Han, Z., Paster, K., Pitis, S., Chan, H., & Ba, J. (2023). [Large Language Models Are Human-Level Prompt Engineers](https://arxiv.org/abs/2211.01910). arXiv:2211.01910. ICLR 2023. *(APE; "let's work this out in a step by step way.")*
- Yang, C., Wang, X., Lu, Y., Liu, H., Le, Q. V., Zhou, D., & Chen, X. (2023). [Large Language Models as Optimizers](https://arxiv.org/abs/2309.03409). arXiv:2309.03409. ICLR 2024. *(OPRO; "take a deep breath," 80.2% GSM8K.)*
- Pryzant, R., Iter, D., Li, J., Lee, Y. T., Zhu, C., & Zeng, M. (2023). [Automatic Prompt Optimization with "Gradient Descent" and Beam Search](https://arxiv.org/abs/2305.03495). arXiv:2305.03495. EMNLP 2023 (main).
- Yuksekgonul, M., Bianchi, F., Boen, J., Liu, S., Huang, Z., Guestrin, C., & Zou, J. (2024). [TextGrad: Automatic "Differentiation" via Text](https://arxiv.org/abs/2406.07496). arXiv:2406.07496. Published in *Nature* (2025).
- Fernando, C., Banarse, D., Michalewski, H., Osindero, S., & Rocktäschel, T. (2023). [Promptbreeder: Self-Referential Self-Improvement Via Prompt Evolution](https://arxiv.org/abs/2309.16797). arXiv:2309.16797.
- Guo, Q., Wang, R., Guo, J., Li, B., Song, K., et al. (2023). [Connecting Large Language Models with Evolutionary Algorithms Yields Powerful Prompt Optimizers](https://arxiv.org/abs/2309.08532). arXiv:2309.08532. ICLR 2024. *(EvoPrompt.)*
- *Is It Time To Treat Prompts As Code? A Multi-Use Case Study For Prompt Optimization Using DSPy* (2025). [arXiv:2507.03620](https://arxiv.org/abs/2507.03620). *(Practitioner empirical case study, preprint; mixed results.)*
- *Revisiting OPRO: The Limitations of Small-Scale LLMs as Optimizers* (2024). [arXiv:2405.10276](https://arxiv.org/abs/2405.10276). `[verify exact title]`

---

**Tags:** automated-prompt-optimization, dspy-signature, mipro-ope-opro, metric-and-eval-set-precondition, discovered-prompts, re-optimization-debt
