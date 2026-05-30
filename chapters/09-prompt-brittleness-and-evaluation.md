> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft.

---

# Chapter 9 — Prompt Brittleness and the Discipline of Evaluation

*Why a Single-Prompt Number Is Not a Capability Claim*

**Author:** Nik Bear Brown
**Editor:** Nik Bear Brown

---

## Suggested titles

1. **Prompt Brittleness and the Discipline of Evaluation: Why a Single-Prompt Number Is Not a Capability Claim**
2. **Semantically Neutral, Behaviorally Catastrophic: Measuring How Much Your Prompt's Surface Is Doing**
3. **Report a Range, Not a Point: The Empirical Spine of Engineering, Not Vibes**

---

## TL;DR

A model conditions on the *surface form* of a prompt, not just its meaning. So changes you would swear are semantically neutral — a colon for a dash, `Q:`/`A:` for `Question -`/`Answer -`, reordering identical few-shot examples — move outputs measurably, and on some tasks *catastrophically*: Sclar et al. (2024) document up to a **76-accuracy-point** spread on a single task from formatting alone. The damage is not just to your accuracy; it corrupts *comparison*. Format choice reorders model leaderboards (Alzahrani et al. 2024: rankings shift up to 8 positions; Mizrahi et al. 2024: template choice flips which model "wins"). The discipline this forces: **reject single-prompt evaluation.** A claim like "Prompt P scores 0.82" is ill-posed. The defensible claim is "Prompt *family* P has a performance *distribution* — median *m*, spread *s* — over plausible semantically-equivalent variants." You test format variants, report an interval, and only then optimize. Specificity helps partly because it is a robustness hedge — but it shifts the sensitive surface rather than eliminating it (Leidinger et al. 2023; mitigations like Mixture-of-Formats, Ngweta et al. 2025, are partial). Brittleness is the empirical refutation of "just ask better," and the reason eval discipline is a first-class engineering activity, not an afterthought.

---

## Learning objectives

By the end of this chapter you should be able to:

1. **(Understand)** Explain mechanistically why a *semantically neutral* prompt change moves outputs — the model conditions on surface form — and why that makes a single-prompt score a construct-invalid proxy for capability.
2. **(Analyze)** Distinguish *single-format optimism* (overstating one prompt's number as the model's capability) from *format-confounded comparison* (declaring model A > B when the result is an artifact of a shared fixed format).
3. **(Evaluate)** Given an evaluation report, identify whether it commits single-prompt evaluation and what claim it is actually licensed to make.
4. **(Create)** Design and run a format-variant evaluation: enumerate plausible semantically-equivalent variants, sample them, and report a performance *distribution* (median and interval) rather than a point.
5. **(Evaluate)** Decide when richer specification is a worthwhile robustness hedge versus when it merely moves the sensitive surface — and reason about how many variants are "enough" under a fixed eval budget.

## Prerequisites

Ch. 0 / Ch. 1 (The Stochastic Machine) — output as a sample from a distribution conditioned on the full prompt token sequence. Ch. 5 (The Architect Mindset) — specificity and constraint as design moves. Ch. 8 (Reasoning and Range) — the distinction between a reasoning/range failure and a surface-form failure, so you know this chapter is a *different* layer.

---

## 9.1 The eval that overstated the model

The following is a composite, assembled from documented brittleness patterns and labeled as such. The mechanism is real — every effect below is reproduced in the cited literature; the specific team is not.

A platform team was choosing between two models for a classification feature. They wrote one careful prompt — a clean instruction, four few-shot exemplars, a `Question:` / `Answer:` scaffold — and ran it against a held-out set of 500 labeled cases. Model A scored 0.86, Model B scored 0.79. The decision wrote itself: ship Model A. The number went into the procurement deck as "Model A: 86% accuracy." The team felt they had done the empirical thing. They had a held-out set. They had a number.

Two weeks after launch, accuracy in production sat closer to 0.71, and nobody could explain the gap. The held-out set had not drifted. The model had not changed. What had changed was nothing anyone thought of as substantive: a downstream refactor had reformatted the prompt — swapped the `Question:` / `Answer:` scaffold for a markdown bullet layout, and (because someone alphabetized a config) reordered the four few-shot exemplars. Semantically identical. Behaviorally, a different prompt.

When the team finally did the experiment they should have done first — run the *same task* across a sweep of plausible formatting variants — the histogram was the whole story. Model A's accuracy ranged from 0.69 to 0.88 across formats. Model B's ranged from 0.74 to 0.83. The single number 0.86 was not Model A's capability. It was the *top* of Model A's distribution, and they had reported it as a point. Worse: at the *median* format, Model B was the better model. The original comparison had not measured which model was better. It had measured which model happened to like that one prompt format — and then made a six-figure decision on the artifact.

The team made no knowledge error and no reasoning error. They made an *evaluation* error, and it is the most common one in the field: they treated a single prompt's score as a property of the model. This chapter is about why that is ill-posed, what the defensible claim looks like instead, and how to produce it. The thesis of the whole book lands here with more force than anywhere else — **prompt engineering is an empirical engineering discipline, not an art of clever phrasing** — because brittleness is the empirical fact that makes "just ask better" not merely insufficient but *unmeasurable* without distributional evaluation.

---

## 9.2 The mechanism: the model conditions on surface form

Why should a colon-for-dash swap move anything? Because of exactly the Chapter 1 picture, taken seriously. The model assigns a probability to the next token *conditioned on the entire preceding token sequence* — and the surface form *is part of that sequence*. `Q:` and `Question -` are not the same tokens. They occupy different positions in the model's learned distribution over how prompts-of-this-shape are continued, because during pretraining different surface forms co-occurred with different continuations. The model never learned a clean separation between "the meaning of the instruction" and "the punctuation, casing, spacing, and ordering it arrived in." It learned a conditional distribution over token sequences, and the surface is in the conditioning set.

So a semantically-neutral edit is not behaviorally neutral, because *semantic* neutrality is a fact about human reading and *behavioral* output is a fact about token-conditioned sampling. There is no theorem connecting the two. This is the single misconception the chapter exists to break.

> **Misconception to dislodge.** "Semantically equivalent ⇒ behaviorally equivalent." This is the intuition that produces single-prompt evaluation, and it is false. The model conditions on form, not just meaning; two prompts you read as identical are, to the sampler, two different points in the conditioning space, and they can land on different sides of a decision boundary. Demonstrate it to yourself live: take one task, flip a colon to a dash, watch a discrete output change.

The *why-at-the-mechanism-level* — surface-feature shortcut learning, tokenization artifacts, decision-boundary proximity, training-distribution format priors — is **not settled**. The papers below *measure* brittleness far more than they *explain* it. The book states that honestly: the behavioral fact (neutral edits move outputs, sometimes enormously) is rock-solid and reproducible; the deep cause is open. You do not need the deep cause to do the engineering. You need to accept that surface form is a high-dimensional *nuisance factor* — a variable that affects your measurement without being the thing you care about — and that the response to a nuisance factor is the same as it has always been in experimental science: vary it on purpose and report the variance.

---

## 9.3 How big, and how it corrupts comparison

### The magnitude: up to 76 points

The anchor result is Sclar et al. (2024, ICLR), "Quantifying Language Models' Sensitivity to Spurious Features in Prompt Design." They built **FormatSpread**, an algorithm that samples plausible *semantically-equivalent* format variants — separators, casing, spacing, item formatting, `Q:`/`A:` versus `Question -`/`Answer -` and so on — and reports a performance *interval* instead of a point. The headline: up to **76 accuracy points** of spread on a single task for LLaMA-2-13B *from formatting alone.* Not noise; not a weak model only. The sensitivity *persists* with larger models, with more few-shot examples, and with instruction tuning. Scale **attenuates** brittleness; it does not remove it.

> **Misconception to dislodge.** "It only affects small or weak models, so frontier models are fine." False. Sclar et al. and Lu et al. both show the effect survives scale and instruction tuning. A bigger model is a *smaller* spread, not a *zero* spread — and "smaller" can still be tens of points.

A second, semantically deeper layer: brittleness is not confined to punctuation. Leidinger et al. (2023) extend it to *linguistic* properties of semantically-equivalent prompts — mood, tense, register, syntactic structure — across model sizes and pre-trained-vs-instruction-tuned models. The sensitive surface is broader than formatting; rewording in ways that preserve meaning also moves outputs. This matters for §9.5's claim about specificity.

And the ordering effect is its own dramatic demonstration. Lu et al. (2022, ACL), "Fantastically Ordered Prompts," showed that the *same* few-shot examples, merely *reordered*, can move a prompt between near-state-of-the-art and near-random — and, again, the effect does not vanish with scale. The examples are identical. Only their sequence changed. (Note the link back to Ch. 8: few-shot teaches *format*; here we see that even the *order* of the format-teaching examples is a brittleness surface.)

### The corruption: format reorders the leaderboard

The accuracy hit to *your* prompt is the smaller problem. The larger one is that brittleness corrupts *comparison*, because nothing guarantees that the format favoring Model A also favors Model B. Sclar et al. found format performance correlates only *weakly across models* — so a fixed shared format does not give a fair fight; it gives whichever model happens to like that format a handicap.

Two documented cases make this concrete rather than hypothetical:

- **Leaderboard reordering (Alzahrani et al. 2024, ACL — "When Benchmarks are Targets").** On MMLU and similar multiple-choice benchmarks, minor *non-semantic* perturbations — reordering the answer choices, changing the answer-extraction method, changing the choice symbol — shift leaderboard *rankings* by **up to 8 positions.** A published, real case where brittleness corrupted a public model comparison.
- **Divergent MMLU implementations (Hugging Face Open LLM Leaderboard investigation, 2023).** Three implementations of *the same* MMLU benchmark — original Berkeley, Stanford HELM, EleutherAI lm-eval-harness — produced *materially different* scores for the same models, driven by prompt-template differences (a `Question:` prefix, how choices are labeled, whether the harness scores the answer *letter* or the answer *text*). Brittleness leaks into "official" numbers.

Mizrahi et al. (2024, TACL — "State of What Art?") put a number on the comparison problem at scale: across ~6.5M instances, 20 LLMs, 39 tasks, they show template choice changes both *absolute* and *relative* performance — i.e., it *reorders models.* This is the §9.1 composite's real-world backbone.

So the two named failure modes:

| Failure mode | What it is | What it costs |
|---|---|---|
| **Single-format optimism** | Reporting one format's score as the model's capability | Overstates reliability; the production gap in §9.1 |
| **Format-confounded comparison** | Declaring A > B on a shared fixed format | Picks the wrong model; the procurement error in §9.1 |

---

## 9.4 The discipline: report a distribution, not a point

The fix is not a better format. There is no universally best format to find — which format wins is task- and model-specific and does not generalize, so memorizing "use XML, not markdown" reinstalls exactly the brittle, non-transferable folk knowledge this chapter is built to kill. The fix is a change in *what you measure and report.*

**Reframe the claim.** "Prompt P performs at accuracy *a*" is ill-posed. The defensible claim is:

> Prompt *family* P has a performance distribution with median *m* and spread *s* over plausible semantically-equivalent variants.

This is the brittleness literature's recommended correction (Sclar et al. 2024; Mizrahi et al. 2024; Polo et al. 2024, PromptEval, NeurIPS 2024). It treats format as the nuisance factor it is and reports the variance attributable to it — which is exactly the move classical experimental design makes for any nuisance factor.

**The procedure (Create-level — this is the chapter's produced artifact):**

1. **Enumerate plausible variants.** Take your prompt and generate a sweep of semantically-equivalent forms: separator style, casing, spacing, item/list formatting, the `Q:`/`A:`-vs-`Question -`/`Answer -` axis, and — if few-shot — exemplar *order*. FormatSpread (github.com/msclar/formatspread) gives ready scaffolding; for a hand-rolled sweep, vary one factor family at a time so you can attribute spread to a cause.
2. **Run all variants on the same held-out set.** Same data, same model; only the format changes. This is a small factorial design: variants × items.
3. **Plot the histogram.** Accuracy across N variants. **The histogram is the lesson.** Annotate the median and a 95% interval.
4. **Pick the metric to your use case (Mizrahi's taxonomy).** *Max-over-formats* answers "*can* the model do this?" (a capability ceiling). *Average* or a *quantile* answers "what will a typical user, who did not tune the format, actually see?" — usually the production-relevant number. Reporting only the max is single-format optimism wearing a histogram.
5. **Only then optimize, and gate edits.** Once you know the distribution, you can search for a robust format — but treat the prompt template as a *versioned artifact under regression testing.* Before shipping any "cosmetic" edit, re-run it across the variant sweep. **Cosmetic edits are not cosmetic** (§9.1 is the proof). PromptEval (Polo et al. 2024) estimates the distribution at roughly 1–4× the cost of a single-prompt eval, which makes distributional gating affordable rather than aspirational.

> **Misconception to dislodge.** "My one good prompt proves the model can do X." It proves the model can do X *under that prompt* — it conflates the max of the distribution with the distribution. Whether your *users* will see X depends on the median and spread, not the max you found by hunting.

This is, in miniature, the *construct validity* problem from research methodology (Campbell & Stanley): a single-format score is a construct-invalid proxy for "capability," and a leaderboard built on one format is a textbook illustration of Campbell's Law — *when a measure becomes a target it ceases to be a good measure* (which is, not coincidentally, the title sentiment of Alzahrani et al., "When Benchmarks are Targets"). The factorial framing — format variants × tasks × models, estimate the variance attributable to the nuisance factor format — is the experimental-design move (Fisher, Yates, Cox) applied to prompts. Brittleness is a *validity* problem, and the response is a *measurement* discipline.

The variant sweep is, in the vocabulary of [Brown's *Computational Skepticism for AI*](#references) — a companion volume — a *verification budget*: producing a single prompt's number is cheap, and establishing what that number *means* is the expensive part you must explicitly fund. The book's blunt formulation generalizes the §9.1 failure: *if you do not budget for verification, you will not get verification.* The team that reported 0.86 did not refuse to verify; they verified at the cheapest level (one held-out run) and mistook it for the expensive one (a distribution). The PromptEval 1–4× figure is what makes the real verification budget affordable rather than aspirational — which is exactly why the cheap version is no longer an excuse.

---

## 9.5 Specificity as a robustness hedge — and its limit

A reasonable reaction to all this is: *so write richer, more specific prompts — pin down format, give detailed instructions, leave less to surface chance.* That reaction is partly right and instructively incomplete, and getting the nuance correct is what separates an engineer from a tip-collector.

Specificity *is* partly a robustness hedge. The more of the output you constrain explicitly, the less is left to be decided by surface features the model is keying on incidentally. A prompt that fixes the output schema, the label space, and the format leaves fewer degrees of freedom for a colon-vs-dash to swing. This is a real reason the structured-prompt and constraint-engineering moves of Ch. 5 and Ch. 7 buy reliability, not just tidiness — part of what they buy is *lower variance under format perturbation.*

But specificity is a hedge, not a cure, and the literature is honest about the limit: richer specification often **shifts the sensitive surface rather than eliminating it.** Leidinger et al. (2023) show that linguistic properties — mood, tense, register, syntax — of semantically-equivalent prompts move outputs too. So when you pin down the formatting, you may simply relocate the sensitivity into the *wording* of your now-longer, more-specific instruction. You have not removed the nuisance factor; you have moved where it lives.

Targeted mitigations exist and should be framed the same way — *partial.* Mixture-of-Formats (Ngweta et al. 2025, NAACL SRW) diversifies the formatting style *across* the few-shot examples within a single prompt — inspired by computer-vision style-augmentation that stops a model keying on style rather than content — and reduces style-induced brittleness while modestly raising mean performance across format variants. It is a robustness *hedge*, not a fix; the underlying sensitivity remains, and it is a small-scale (student-research-workshop) study whose generalization across model families and task types is not yet established. `[verify generalization claims as the literature matures.]`

> **Misconception to dislodge.** "More detail always reduces variance" and "a trick (MOF, ensembling, robust-format search) fixes it." Detail helps but can relocate the sensitive surface (Leidinger). Mitigations mitigate; none eliminate the conditioning-on-surface-form that causes brittleness. The only robust *claim* you can make is still distributional — which returns you to §9.4. Specificity reduces the spread you must report; it does not let you go back to reporting a point.

---

## Exercises

1. **(Understand / Analyze)** Take this evaluation report verbatim: *"We tested Claude and GPT on our extraction task with a carefully designed prompt. Claude scored 91%, GPT scored 88%, so we selected Claude."* (a) Name the two failure modes from §9.3 it commits or risks. (b) State precisely what claim this evaluation is *licensed* to make. (c) Rewrite the report's conclusion as a distributional claim with the information that *would* be needed to support it.

2. **(Create, produce-something)** Run a real format-variant evaluation. Pick one task with a held-out labeled set of at least ~50 items. Generate 10–20 semantically-equivalent prompt variants spanning at least three factor families (separator style, casing, exemplar order). Run all variants. Produce: a histogram of accuracy across variants annotated with median and 95% interval; a one-paragraph statement of the *spread* and which metric (max / average / quantile) you'd report to (a) a research claim and (b) a production decision, and why they differ.

3. **(Evaluate)** Design a *regression gate* for prompt edits in a hypothetical production pipeline. Specify: which format variants the gate runs, what statistic of the resulting distribution must not regress (and by how much) for an edit to ship, and what eval budget (in multiples of a single-prompt run) you'd allocate — defending the budget against the PromptEval 1–4× figure. Then state explicitly what kind of "cosmetic" edit your gate would have *caught* in the §9.1 composite.

4. **(Analyze)** Take a single multiple-choice question and produce three *non-semantic* perturbations (reorder the choices, change the choice symbols A/B/C → 1/2/3, change whether you score the letter or the answer text). Predict, before running, which perturbation you expect to move the answer most, citing the mechanism (§9.2) and Alzahrani et al. Report whether the prediction held.

---

## What would change my mind

A robust demonstration that, for current frontier models on realistic *agentic and long-form* tasks (not multiple-choice benchmarks), semantically-neutral format and ordering perturbations produce spreads small enough (say, within run-to-run sampling noise) that a single well-formed prompt *is* a defensible capability estimate. The chapter's claim is that brittleness persists through scale and instruction tuning and that single-prompt evaluation is therefore ill-posed; most of the strong evidence (Sclar, Lu, Alzahrani) is MCQ-centric, and whether heavy RLHF meaningfully shrinks brittleness on open-ended agentic work is genuinely under-studied (§ open questions). If the spread on real tasks turned out to be negligible for frontier models, the distributional-reporting discipline would still be *good practice* but would lose its status as a *necessity*, and "report a range" would soften to "report a range when the spread is non-trivial — and here is how to cheaply check whether it is."

## Still puzzling

- **The mechanism.** No settled first-principles account of *why* neutral edits move outputs — shortcut features vs. tokenization artifacts vs. decision-boundary geometry vs. pretraining format priors. The chapter is honest that it measures more than it explains.
- **Predictability.** Can we predict *a priori* which prompts and tasks are brittle, instead of measuring it post hoc? Largely unsolved. If we could, the eval budget would collapse — you'd sweep only the prompts you predicted to be fragile.
- **Eval-budget standard.** PromptEval gets a distribution at 1–4× single-prompt cost, but there is no consensus on how many variants are "enough" to gate a production change. The right number almost certainly depends on the spread itself, which you don't know until you've sampled — a chicken-and-egg the field has not resolved.
- **Interaction with reasoning (Ch. 8).** Whether explicit reasoning traces dampen or amplify format sensitivity is under-studied — a reasoning trace could stabilize the surface the answer conditions on, or add a new sensitive surface of its own.

---

## References

- Sclar, M., Choi, Y., Tsvetkov, Y., & Suhr, A. (2024). [Quantifying Language Models' Sensitivity to Spurious Features in Prompt Design, or: How I learned to start worrying about prompt formatting](https://arxiv.org/abs/2310.11324). *ICLR 2024.* arXiv:2310.11324. Code: github.com/msclar/formatspread.
- Lu, Y., Bartolo, M., Moore, A., Riedel, S., & Stenetorp, P. (2022). [Fantastically Ordered Prompts and Where to Find Them: Overcoming Few-Shot Prompt Order Sensitivity](https://aclanthology.org/2022.acl-long.556/). *ACL 2022.*
- Mizrahi, M., Kaplan, G., Malkin, D., Dror, R., Shahaf, D., & Stanovsky, G. (2024). [State of What Art? A Call for Multi-Prompt LLM Evaluation](https://aclanthology.org/2024.tacl-1.52/). *TACL* 12. DOI:10.1162/tacl_a_00681.
- Ngweta, L., Kate, K., Tsay, J., & Rizk, Y. (2025). [Towards LLMs Robustness to Changes in Prompt Format Styles](https://arxiv.org/abs/2504.06969). *NAACL 2025 Student Research Workshop* (IBM Research / RPI). arXiv:2504.06969.
- Alzahrani, N., et al. (2024). [When Benchmarks are Targets: Revealing the Sensitivity of Large Language Model Leaderboards](https://arxiv.org/abs/2402.01781). *ACL 2024.* arXiv:2402.01781.
- Leidinger, A., van Rooij, R., & Shutova, E. (2023). [The Language of Prompting: What Linguistic Properties Make a Prompt Successful?](https://aclanthology.org/2023.findings-emnlp.618/) *Findings of EMNLP 2023.*
- Min, S., Lyu, X., Holtzman, A., Artetxe, M., Lewis, M., Hajishirzi, H., & Zettlemoyer, L. (2022). [Rethinking the Role of Demonstrations: What Makes In-Context Learning Work?](https://arxiv.org/abs/2202.12837) *EMNLP 2022.* arXiv:2202.12837. `[verify arXiv ID]`
- Polo, F. M., Weber, L., Choshen, L., Sun, Y., Xu, G., & Yurochkin, M. (2024). [Efficient multi-prompt evaluation of LLMs (PromptEval)](https://arxiv.org/abs/2405.17202). *NeurIPS 2024.* arXiv:2405.17202. `[verify author list / title before quoting]`
- Hugging Face (2023). [What's going on with the Open LLM Leaderboard?](https://huggingface.co/blog/open-llm-leaderboard-mmlu) (MMLU implementation-divergence investigation). `[verify exact URL]`
- Brown, N. B. *Computational Skepticism for AI.* Companion volume. *(Source of the solve-verify asymmetry and the "verification budget" framing — "if you do not budget for verification, you will not get verification.")*

---

**Tags:** prompt-brittleness, format-sensitivity, formatspread, multi-prompt-evaluation, single-format-optimism, format-confounded-comparison, construct-validity, report-a-distribution, engineering-not-vibes, mixture-of-formats
