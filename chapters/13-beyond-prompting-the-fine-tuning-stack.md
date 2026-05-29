> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft. Drafted against the Ch. 6 (Persona Patterns) anatomy/voice model.
>
> **Consolidation note (per TIKTOC):** this chapter is a *decision* chapter that absorbs what were separate outline chapters — SFT-vs-RAG, LoRA/QLoRA, and RLHF/DPO/GRPO. The LoRA/QLoRA *mechanism* detail is condensed here from the standalone reference draft (Ch. 14, Deshmukh) and cross-referenced rather than re-taught at full length. Chinchilla scaling / catastrophic forgetting are deferred to an appendix.
>
> **Aging-risk flag:** the RL/optimization landscape (GEPA, GRPO, MMGRPO) is 2024–2025 and fast-moving. Deltas cited with named benchmarks and corrected attributions; preprints flagged. The stable core is the *layered-stack decision rule*; current method names age fastest.

---

# Chapter 13 — Beyond Prompting: The Fine-Tuning Stack

*The Binary Is Dead — Prompting, SFT/RAG, and RL Are Layers, Not Rivals*

**Author:** Nik Bear Brown
**Editor:** Nik Bear Brown

---

## Suggested titles

1. **Beyond Prompting: The Fine-Tuning Stack**
2. **The Ladder, Not the Fork: Why "Prompt or Fine-Tune?" Is the Wrong Question**
3. **Escalating Cost, Escalating Irreversibility: A Decision Rule for the Post-Training Stack**

---

## TL;DR

Students arrive believing they must *choose* between prompting and fine-tuning. The binary is dead as an engineering frame. Prompting, supervised fine-tuning (SFT) / retrieval-augmented generation (RAG), and reinforcement learning (RL, e.g. GRPO) are **layers of a post-training stack**, distinguished by escalating cost and irreversibility — not competitors ranked by quality. The decision rule is a *ladder with checkable gates*: prompt-optimize first (cheap, fast, reversible); escalate to SFT/RAG only when the prompt-optimized ceiling is provably insufficient *and* you have a stable labeled set or volatile knowledge; escalate to RL only when you can define a *verifiable reward* and the prompt ceiling is still too low. The empirical anchors cut both ways — on agentic compound tasks, reflective prompt evolution (GEPA) *beat* RL using up to 35× fewer rollouts; on a narrow high-accuracy code task, fine-tuning *beat* every prompt method. That contradiction is not noise. It is the whole point: the answer depends on the task, and the decision rule tells you which way.

---

## Learning objectives

By the end of this chapter you should be able to:

1. **(Understand)** Explain why prompting, SFT/RAG, and RL are *parameters of one system* (prompt text and weights both being optimizable), dissolving the prompt-vs-fine-tune binary.
2. **(Apply)** Derive the LoRA weight-update decomposition $W = W_0 + BA$ and state, in one sentence each, what LoRA and QLoRA change relative to full fine-tuning.
3. **(Evaluate)** Apply a three-gate escalation ladder — prompt-optimize → SFT/RAG → RL — using knowledge volatility, latency/deployment, and verifiable-reward availability as the decision variables.
4. **(Evaluate)** Name four decision-level failure modes (premature fine-tuning, reward-hacking escalation, persona-reflex, RAG-vs-tune confusion) and match an observed mistake to the right one.
5. **(Analyze)** Read the GEPA and Monash code-review results critically, including the rollouts-vs-compute and over-which-baseline distinctions.

## Prerequisites

Ch. 12 (Automated Prompt Optimization) — tier 1 of the stack; the metric-and-eval-set precondition recurs here. Ch. 9 (Brittleness / Evaluation) — you cannot run any gate without an eval set. Ch. 4 (Sycophancy) — the alignment pressures RL inherits. Linear algebra through matrix rank and SVD for the LoRA mechanism (§13.4).

---

## 13.1 Two results that can't both be right (and both are)

Put two recent findings side by side.

**Finding A.** On a suite of compound, multi-module agentic tasks — multi-hop QA, fact verification, privacy-preserving delegation — a method called **GEPA** that does nothing but *evolve the text of prompts* outperformed reinforcement learning (specifically GRPO) by roughly **6 points on average and up to ~19 points** on the hardest benchmark, while using **up to 35× fewer rollouts** ([Agrawal et al., 2025](https://arxiv.org/abs/2507.19457), accepted ICLR 2026 Oral). Prompting beat RL, and did it far more cheaply.

**Finding B.** On a narrow code-review automation task — given an original file plus a reviewer's comment, produce the revised code, scored by Exact Match against the human-written revision — a **fine-tuned** GPT-3.5 beat *every* prompt-engineering configuration tested, by **63.91%–1,100% higher Exact Match** ([Pornprasit & Tantithamthavorn, 2024](https://arxiv.org/abs/2402.00905), Monash University; published in *Information and Software Technology*). Fine-tuning beat prompting, decisively.

A student holding the prompt-vs-fine-tune binary cannot absorb both. If prompting is "better," Finding B is impossible; if fine-tuning is "better," Finding A is impossible. The resolution is to throw out the binary. **These are different tasks in different regimes, and the right method is a function of the regime.** Finding A is a dynamic, multi-module pipeline with no clean single reward — prompting's home turf. Finding B is a static, narrow domain with a stable labeled set and a brittle high-ceiling metric (Exact Match) — fine-tuning's home turf.

The job of this chapter is to give you the decision rule that tells the two regimes apart *before* you've spent the money. Not a quality ranking — a ladder of escalating cost and irreversibility, with a checkable gate at each rung.

---

## 13.2 The reframe: prompt text and weights are both parameters

Here is the sentence that dissolves the binary. A language-model system has two sets of adjustable parameters: the **prompt text** (instructions, demonstrations, retrieved context) and the **weights** (the model's learned matrices). Prompt optimization tunes the first set. Fine-tuning tunes the second. RL tunes the second using a reward signal instead of labeled targets. **All three are ways of adjusting parameters of the same system to raise the same metric.** Stated that way, "prompt *or* fine-tune?" is as confused as asking whether to adjust the numerator *or* the denominator of a fraction. You adjust whichever moves your objective most per unit of cost.

This is not just rhetoric. The DSPy line of work makes it literal: **BetterTogether** ([Soylu et al., 2024](https://arxiv.org/abs/2407.10930)) alternates between optimizing prompts and fine-tuning weights in the *same* pipeline, and **MMGRPO** ([Soylu et al., 2025](https://arxiv.org/abs/2508.04660)) composes prompt optimization with policy-gradient RL. We return to what those papers actually measured in §13.6 — the numbers have been widely misquoted and the precision matters.

So why a *ladder* and not just "optimize everything jointly"? Because the layers differ enormously in **cost and irreversibility**, and most of the time you don't need the expensive rungs:

- **Prompt optimization** needs no GPUs, no labeled training corpus, no custom checkpoint to host. It is fast and fully reversible — change the prompt back and you're where you started.
- **SFT / RAG** needs labeled data (SFT) or a maintained retrieval index (RAG), incurs ongoing maintenance (retrain when the base model updates; keep the index fresh), and produces an artifact you now own and must serve.
- **RL (GRPO)** needs a *verifiable reward* and a training loop that samples many outputs per prompt; it is the most expensive and the hardest to debug.

The ladder is ordered by *escalating cost and irreversibility*. You climb only when the cheaper rung is provably insufficient. This is decision theory's oldest move — Abraham Wald's 1945 sequential analysis: decide to stop, continue, or escalate based on the evidence accumulated so far, rather than committing to the most expensive experiment up front.

---

## 13.3 The escalation ladder, with gates

Three gates. Each is a checkable condition, and each has a *failure mode* attached to skipping it.

```
  ┌─────────────────────────────────────────────────────────┐
  │ Step 0: Define eval set + the requirement (target metric)│
  └───────────────────────────┬─────────────────────────────┘
                              ▼
  ┌─────────────────────────────────────────────────────────┐
  │ GATE 1  Run automated prompt optimization (Ch.12).        │
  │         Does the prompt-optimized ceiling ≥ requirement?  │
  │         YES → SHIP. (cheapest, reversible)                │
  └───────────────────────────┬─────────────────────────────┘
                              │ NO
                              ▼
  ┌─────────────────────────────────────────────────────────┐
  │ GATE 2  Do you have (a) a stable labeled set + need frozen│
  │         behavior / a small deployable model, OR (b)       │
  │         volatile knowledge better served by retrieval?    │
  │         (a) → SFT (LoRA/QLoRA, §13.4)                      │
  │         (b) → RAG (retrieve, don't retrain)               │
  └───────────────────────────┬─────────────────────────────┘
                              │ still insufficient
                              ▼
  ┌─────────────────────────────────────────────────────────┐
  │ GATE 3  Can you define a VERIFIABLE reward AND is the     │
  │         prompt-optimized ceiling still too low?           │
  │         YES → RL (GRPO, §13.5).   NO → do not escalate.   │
  └─────────────────────────────────────────────────────────┘
```

Two decision variables deserve isolating, because they're the ones students get wrong:

- **Knowledge volatility (Gate 2's RAG-vs-SFT split).** If the knowledge your system needs *changes faster than you can retrain* — prices, policies, today's inventory — do **not** fine-tune it in; retrieve it. Fine-tuning bakes a snapshot into weights; the snapshot goes stale; you retrain; it goes stale again. RAG keeps the volatile knowledge in an index you can update without touching the model. Fine-tune for *stable* style/format/behavior; retrieve for *volatile* facts.

- **Verifiable reward (Gate 3).** RL needs a reward function that can score an output *automatically and correctly* — math answers you can check, code that passes tests, formats you can validate. If "good" requires human judgment you can't automate, you do not have a verifiable reward, and reaching for GRPO is reaching for a tool whose precondition you haven't met.

### The four decision-level failure modes

- **Premature fine-tuning.** Paying retraining cost (and accepting an owned checkpoint's maintenance burden) for what a better prompt would have fixed. Skipping Gate 1.
- **RAG-vs-tune confusion.** Fine-tuning to inject *volatile knowledge* that belongs in retrieval — "expensive theater" that bakes a stale snapshot into weights. Misreading Gate 2.
- **Reward-hacking escalation.** Reaching for RL without a verifiable reward, then watching the model optimize the proxy you *could* measure instead of the goal you actually wanted. Skipping Gate 3's precondition.
- **Persona-reflex.** Adding a persona because it "feels" like it should help. The Monash code-review study measured this directly: adding a persona to the prompt *hurt* Exact Match by **−1.02% to −54.17%** ([Pornprasit & Tantithamthavorn, 2024](https://arxiv.org/abs/2402.00905)). A clean, citable myth-buster — the reflex is not free, and on this task it was actively harmful. (Cross-ref Ch. 6: persona is a behavioral steering tool, not a universal accuracy lever.)

### Misconception: "fine-tuning is the advanced, better option"

The single most common student error. Fine-tuning is not *up* on a quality axis; it is *up* on a cost-and-irreversibility axis. Sometimes the expensive rung wins (Finding B). Often it is unnecessary, and the recurring practitioner warning is that *organizations overestimate the need for custom models* — fine-tuning to add knowledge that RAG serves better, or to fix behavior a better prompt fixes. The ladder ranks cost, not goodness.

---

## 13.4 The SFT rung, condensed: LoRA and QLoRA

When Gate 2 sends you to fine-tune, the question becomes *how*. Full fine-tuning updates every weight — expensive in memory and compute, and it produces an entirely new model per task. Two parameter-efficient methods change the cost structure. *(This section condenses the mechanism; the full treatment, including serving-topology failure modes, is the LoRA/QLoRA reference chapter.)*

**LoRA's mechanism (the math, visible).** For a base weight matrix $W_0 \in \mathbb{R}^{d \times k}$, full fine-tuning learns an update $\Delta W$ of the *same shape* — for $d=k=4096$, about 17 million parameters per matrix. LoRA's insight ([Hu et al., 2021](https://arxiv.org/abs/2106.09685)) is that task-specific adaptations live in a **low-dimensional subspace**, so $\Delta W$ does not need full rank. Parameterize it as a product of two thin matrices:

$$\Delta W = BA, \qquad B \in \mathbb{R}^{d \times r}, \quad A \in \mathbb{R}^{r \times k}, \quad r \ll \min(d,k)$$

The forward pass becomes:

$$h = W_0 x + \frac{\alpha}{r}\, B A x$$

with $W_0$ **frozen** and only $B, A$ trained. The trainable parameter count drops from $dk$ to $r(d+k)$. For $r=8$, $d=k=4096$: from 16,777,216 down to 65,536 — about a **256×** reduction. The scaling factor $\alpha/r$ decouples the learning rate from the rank, so you can change $r$ without re-tuning the optimizer. (The rank $r$ is a hard *capacity floor*: a rank-$r$ adapter can only express a rank-$r$ change to behavior. If the task needs more directions than $r$ provides, the adapter starves — diagnose by rank ablation, not intuition. See the LoRA/QLoRA reference chapter.)

**QLoRA, in one correction.** The common misbelief is that "QLoRA runs the model in 4-bit." It does not. QLoRA is *hybrid-precision*: the **frozen base weights are stored in 4-bit** (NF4), the **trainable adapters stay in FP16/BF16**, and **all computation happens in FP16/BF16** — the 4-bit base weights are dequantized before each matrix multiply ([Dettmers et al., 2023](https://arxiv.org/abs/2305.14314)). QLoRA buys *storage compression on the frozen part*, not faster computation. So it helps exactly when *memory* is your binding constraint (fine-tuning a 70B model on one GPU) and buys nothing when throughput is the bottleneck.

**Why this lives in a decision chapter.** Because the choice among full / LoRA / QLoRA is, like the ladder itself, a *serving-topology* decision dressed up as a cost decision. Full fine-tuning gives independent models per task. LoRA/QLoRA give one shared frozen base with routed adapters — cheaper, but introducing failure modes (adapter misrouting, rank starvation) that independent models don't have. The mechanism detail that used to be a standalone chapter compresses to this: *cheaper fine-tuning is a different architecture, and different architectures fail differently.* (RLHF/DPO mechanism detail similarly compresses into §13.5 and cross-references; the alignment-failure side — reward hacking, sycophancy amplification — connects back to Ch. 4.)

---

## 13.5 The RL rung, condensed: GRPO and verifiable reward

Gate 3 escalates to reinforcement learning only under two conditions: a verifiable reward exists, and the prompt-optimized ceiling is still insufficient. The de-facto method for this rung is **GRPO** (Group Relative Policy Optimization), introduced in DeepSeekMath ([Shao et al., 2024](https://arxiv.org/abs/2402.03300)) and later used to train DeepSeek-R1.

**The mechanism, in one paragraph.** Standard policy-gradient RL (PPO) trains a separate *critic* network to estimate how good each output is (the "advantage" baseline). That critic roughly doubles the memory and compute of training. GRPO removes it. Instead of a learned critic, GRPO samples a *group* of outputs for the same prompt, scores them all, and uses the group's standardized (mean/variance-normalized) reward as the baseline:

$$\hat{A}_i = \frac{r_i - \text{mean}(\{r_1,\dots,r_G\})}{\text{std}(\{r_1,\dots,r_G\})}$$

An output that beats its group's average gets a positive advantage and is reinforced; one below average is suppressed. Cutting the critic cuts the cost of RL post-training roughly in half — which is why GRPO became the practical default for reasoning post-training and ships in HuggingFace TRL and VERL. (Full RLHF/DPO/GRPO internals are cross-referenced from this decision chapter, not re-derived; Arthur Samuel's 1959 self-learning checkers program — improve from sampled game outcomes — is the deep ancestor of "sample outputs, adjust behavior.")

**The honest boundary on RL.** GRPO's home turf is *single-model* math/code reasoning with a clean automatic reward (the answer is right or wrong; the code passes tests or doesn't). That is precisely *not* the regime where Finding A's GEPA beat it. The two results are not in conflict because they tested different things — which is exactly why the ladder routes by regime.

---

## 13.6 Reading the anchor numbers precisely

A decision chapter is only as good as the discipline with which it reads its own evidence. Three numbers get misquoted constantly; here is what the papers actually say.

**"GEPA beats RL by 6–19 points using 35× fewer compute."** Two corrections. First, it is **rollouts, not compute** — "35× fewer rollouts" is a *sample-efficiency* claim (number of program executions), not wall-clock or dollar cost; the two don't convert one-to-one. Second, the cleanest framing of the deltas is **~6 points on average, up to ~19 on the hardest benchmark** (HotpotQA +19.0; HoVer +13.7; PUPA +5.2; IFBench +2.7), *not* a flat "6–19." And the scope: one paper, four benchmarks, all *compound/agentic* — an existence proof that prompt evolution can beat a specific GRPO setup on that regime, not a universal law ([Agrawal et al., 2025](https://arxiv.org/abs/2507.19457)).

**"The layered approach beats either alone by up to 60%."** This is the BetterTogether number, and the asymmetry is load-bearing: the 60% is the gain of joint optimization **over fine-tuning weights *alone***, and only about **6%** over prompt-optimization alone ([Soylu et al., 2024](https://arxiv.org/abs/2407.10930)). Writing "60% over either alone" misrepresents the paper. The cleaner "stack beats parts" figure is MMGRPO's: **+11% over the post-trained model, +5% over prompt-optimization alone** ([Soylu et al., 2025](https://arxiv.org/abs/2508.04660)).

**"Fine-tuning beat prompting by 63–1,100% on code review."** Verified, with caveats. It is the *few-shot* fine-tuned GPT-3.5 variant, the metric is **Exact Match** (brittle — it penalizes any correct-but-non-identical revision), and the 1,100% upper bound reflects a very low baseline denominator, not 11× absolute accuracy. The closest-to-clean figure is the zero-shot fine-tuned variant beating prior non-LLM approaches by **73.17%–74.23%** EM. And the affiliation: **Monash University**, not "University of Australia" — there is no such institution, and the error has propagated through secondary blog relays ([Pornprasit & Tantithamthavorn, 2024](https://arxiv.org/abs/2402.00905)).

The reason to belabor this: the decision rule rests on these anchors. If you carry around "prompting beats RL, full stop" or "fine-tuning is 1,100% better," you will route tasks to the wrong rung. The precise reading — *prompting wins on compound/agentic at lower sample cost; fine-tuning wins on narrow/high-accuracy with a stable labeled set; the stack composed beats any single rung* — is what makes the ladder usable.

---

## 13.7 What this chapter is really claiming

The strong claim: **prompting, SFT/RAG, and RL are complementary layers of one parameter space, and the right engineering move is a cost-ordered escalation ladder with checkable gates — not a one-time fork.** The reframe (prompt text and weights are both parameters) dissolves the binary; the empirical anchors (GEPA, Monash, BetterTogether/MMGRPO) show that *every* rung wins in its regime and that composing rungs can beat climbing them.

The honest boundaries are three. First, "prompt optimization beats RL" is demonstrated on *compound/agentic* tasks, not on GRPO's single-model-reasoning home turf — no firmly-established head-to-head exists on the *same* task at matched compute. Second, "fine-tuning wins" is demonstrated on a *narrow, high-EM-ceiling* task with a dated model and a brittle metric — generalize cautiously. Third, the boundary between *climbing* the ladder (escalate sequentially) and *composing* it (BetterTogether/MMGRPO optimize rungs jointly) is genuinely unsettled — the chapter teaches the ladder because it is the safe default, while flagging that joint optimization can beat sequential escalation when you can afford it.

The thesis connection is exact. This is the book's "engineering, not vibes" argument applied to the most expensive decision a prompt engineer makes. Each rung's precondition is *checkable in advance* — a metric and eval set (Gate 1), a stable labeled set or volatile knowledge (Gate 2), a verifiable reward (Gate 3). You do not escalate on a feeling that fine-tuning is "more serious." You escalate when the cheaper rung is *provably* insufficient and the next rung's precondition *provably* holds. That is the discipline. The fractured turbine blade of Ch. 6 had a maintenance supervisor who needed to understand a warning; the production system of this chapter has a budget owner who needs to know that the $50,000 fine-tuning run was *necessary* — and the ladder is how you know.

---

## Exercises

1. **(Understand)** Explain, in three sentences, why "prompt *or* fine-tune?" is the wrong question. Use the phrase "parameters of one system" and name the axis the ladder actually ranks (hint: it is not quality).

2. **(Apply)** For LoRA with $r=16$, $d=k=4096$, compute the trainable parameter count and the reduction factor versus a full-shape update. Then state in one sentence what would change if you used QLoRA instead — and what would *not* change about the computation precision.

3. **(Evaluate)** You are routing three **Mycroft** investment-intelligence tasks through the ladder: (a) "summarize today's earnings call in the firm's house style"; (b) "answer 'what is this company's current debt-to-equity ratio' from live filings"; (c) "given a math-heavy valuation problem with a checkable numeric answer, maximize accuracy." For each, say which rung you stop at and which decision variable (knowledge volatility / latency-deployment / verifiable reward) drove the decision.

4. **(Analyze)** Take the three anchor numbers in §13.6. For each, write the *wrong* one-line summary a careless reader would carry away, then the corrected version, and name the one word or scope-condition that flips the meaning (e.g. "rollouts" vs "compute," "over fine-tuning alone" vs "over either").

5. **(Create / Apply+)** Write a one-page **escalation memo** for a real or invented production task. It must contain: the eval set and target metric (Step 0); the Gate-1 prompt-optimized ceiling (measured or honestly estimated, with the basis stated); a Gate-2 decision (SFT vs RAG) justified by knowledge volatility; a Gate-3 decision justified by whether a verifiable reward exists; and an explicit statement of which of the four failure modes you are most at risk of and how you'll guard against it. Deliver the memo as something a budget owner could approve or reject on its stated reasoning.

---

## What would change my mind

A controlled, matched-compute head-to-head on the *same* reasoning task — where GRPO is strongest (single model, verifiable reward) — showing reflective prompt evolution (GEPA-style) matching or beating RL there too, *and* a parallel result on a narrow high-accuracy domain showing prompt optimization closing the Monash-style fine-tuning gap. The chapter routes by regime precisely because the current evidence shows prompting winning on compound/agentic tasks and fine-tuning winning on narrow/high-accuracy ones. If a single method dominated *across* regimes at matched cost, the ladder would collapse into "just use method X," and the decision rule would need rewriting around that method rather than around the gates.

## Still puzzling

- **Climb vs. compose.** The chapter teaches a sequential ladder; BetterTogether and MMGRPO show that *jointly* optimizing rungs can beat climbing them. When is the extra complexity of joint optimization worth it over the simpler escalate-only-as-needed rule? The boundary is unsettled.
- **The real cost crossover.** "35× fewer rollouts" doesn't cleanly convert to dollars; the actual compute/cost crossover between GEPA-style optimization and GRPO is unstudied. Without it, Gate-3 cost reasoning is partly guesswork.
- **Model-churn vs. fine-tuning ROI.** As base models update every few months, the maintenance cost of an owned checkpoint may dominate its accuracy benefit. The break-even is under-quantified, and the widely-repeated "~28.3% accuracy gain from fine-tuning" figure lacks a clean primary source — flagged, not cited.
- **Pre-training rank prediction.** Can rank starvation (§13.4) be predicted from task-intrinsic properties *before* training, rather than discovered by ablation? A principled estimate would let Gate 2 reason about LoRA capacity up front.

---

## References

- Shao, Z., Wang, P., Zhu, Q., Xu, R., Song, J., et al. (2024). [DeepSeekMath: Pushing the Limits of Mathematical Reasoning in Open Language Models](https://arxiv.org/abs/2402.03300). arXiv:2402.03300. *(Introduces GRPO.)*
- Agrawal, L. A., et al. (2025). [GEPA: Reflective Prompt Evolution Can Outperform Reinforcement Learning](https://arxiv.org/abs/2507.19457). arXiv:2507.19457. Accepted ICLR 2026 (Oral). *(Genetic-Pareto; up to ~19 pts / ~6 avg over GRPO, up to 35× fewer rollouts.)*
- Soylu, D., Potts, C., Khattab, O., et al. (2024). [Fine-Tuning and Prompt Optimization: Two Great Steps that Work Better Together](https://arxiv.org/abs/2407.10930). arXiv:2407.10930. *(BetterTogether; 60% is over fine-tuning alone, ~6% over prompt-opt alone.)*
- Soylu, D., et al. (2025). [Multi-module GRPO: Composing Policy Gradients and Prompt Optimization for Language Model Programs](https://arxiv.org/abs/2508.04660). arXiv:2508.04660. *(MMGRPO / dspy.GRPO; +11% over post-trained LM, +5% over prompt-opt.)*
- Pornprasit, C., & Tantithamthavorn, C. (2024). [Fine-Tuning and Prompt Engineering for Large Language Models-based Code Review Automation](https://arxiv.org/abs/2402.00905). arXiv:2402.00905; *Information and Software Technology*, DOI 10.1016/j.infsof.2024.107523. **Monash University.** *(63.91%–1,100% EM; persona −1.02% to −54.17% EM.)*
- Hu, E. J., Shen, Y., Wallis, P., Allen-Zhu, Z., Li, Y., Wang, S., Wang, L., & Chen, W. (2021). [LoRA: Low-Rank Adaptation of Large Language Models](https://arxiv.org/abs/2106.09685). arXiv:2106.09685.
- Dettmers, T., Pagnoni, A., Holtzman, A., & Zettlemoyer, L. (2023). [QLoRA: Efficient Finetuning of Quantized LLMs](https://arxiv.org/abs/2305.14314). arXiv:2305.14314.

---

**Tags:** fine-tuning-stack, prompt-optimize-sft-rl-ladder, lora-qlora-mechanism, grpo-verifiable-reward, gepa-vs-grpo, decision-chapter
