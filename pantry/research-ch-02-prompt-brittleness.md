# Research: Candidate Chapter §2 — The Brittleness Problem
## Prompt Engineering with LLMs
**Chapter one-line:** Why semantically-neutral prompt changes move model outputs, and what that means for evaluation.
**Research date:** 2026-05-29
---

## 1. Primary Sources

### Foundational papers and texts

- **Sclar, M., Choi, Y., Tsvetkov, Y., & Suhr, A. (2024). "Quantifying Language Models' Sensitivity to Spurious Features in Prompt Design or: How I learned to start worrying about prompt formatting." ICLR 2024.** arXiv:2310.11324 (v2). OpenReview id RIu5lyNXjT. Code: github.com/msclar/formatspread.
  The anchor empirical paper for this chapter. Introduces **FormatSpread**, an algorithm that samples plausible *semantically-equivalent* format variants (separators, casing, spacing, item formatting, e.g. `Q:`/`A:` vs `Question -`/`Answer -`) and reports a performance *interval* rather than a point. Headline finding: up to **76 accuracy points** of spread on a single task for LLaMA-2-13B from formatting alone; sensitivity persists with larger models, more few-shot examples, and instruction tuning. Format performance correlates only weakly *across* models — so a format favoring model A may hurt model B, undermining single-format model comparisons. This is the chapter's "discrete-output flips" / ">20% swing" claim, stated precisely. Spine claim is correct.

- **Mizrahi, M., Kaplan, G., Malkin, D., Dror, R., Shahaf, D., & Stanovsky, G. (2024). "State of What Art? A Call for Multi-Prompt LLM Evaluation." TACL, vol. 12.** ACL Anthology 2024.tacl-1.52; DOI 10.1162/tacl_a_00681.
  The evaluation-discipline backbone. Builds a large collection of instruction *paraphrases* (semantically equivalent rewordings, not just formatting) and analyzes brittleness over ~6.5M instances, 20 LLMs, 39 tasks across 3 benchmarks. Finds template choice changes both absolute and *relative* performance — i.e. it reorders models. Proposes use-case-tailored multi-prompt metrics (max-performance for "can the model do it"; average/quantile for "what will a user typically see"). Use this to ground the chapter's claim that single-prompt evals overestimate reliability and can flip rankings.

- **Lu, Y., Bartolo, M., Moore, A., Riedel, S., & Stenetorp, P. (2022). "Fantastically Ordered Prompts and Where to Find Them: Overcoming Few-Shot Prompt Order Sensitivity." ACL 2022 (Long), pp. 8086–8098.** ACL Anthology 2022.acl-long.556. Code: github.com/yaolu/ordered-prompt.
  The canonical few-shot **ordering** result and the most dramatic single demonstration: the *same* examples, merely reordered, can move a prompt between near-SOTA and near-random. Crucially shows the effect does not vanish with scale. Introduces entropy-based selection (GlobalE / LocalE) that builds an artificial probing set by sampling from the model itself — an early "the model can help you pick a robust format" move that prefigures automated optimization. Directly supports the spine's "few-shot example ordering" item.

- **Ngweta, L., Kate, K., Tsay, J., & Rizk, Y. (2025). "Towards LLMs Robustness to Changes in Prompt Format Styles." NAACL 2025 Student Research Workshop.** arXiv:2504.06969; ACL Anthology 2025.naacl-srw.51. *(IBM Research / RPI.)*
  The **Mixture of Formats (MOF)** mitigation. NOTE: spine dated this 2024; the published venue is **2025 NAACL SRW** (arXiv April 2025). MOF *diversifies the formatting style across the few-shot examples in a single prompt* (rather than using one uniform style), inspired by computer-vision style-augmentation that stops models keying on style rather than content. Reported to reduce style-induced brittleness and modestly raise mean performance across format variations. This is a "partial mitigation" — frame it as a robustness hedge, not a fix; the underlying sensitivity remains.

- **Leidinger, A., van Rooij, R., & Shutova, E. (2023). "The language of prompting: What linguistic properties make a prompt successful?" Findings of EMNLP 2023.** ACL Anthology 2023.findings-emnlp.618.
  Extends brittleness from *formatting* to *linguistic* properties of semantically-equivalent prompts (mood, tense, register, syntactic structure), across model sizes and pre-trained vs instruction-tuned. Useful for the "specificity / instruction-richness as a robustness hedge" thread and to show the sensitivity surface is broader than punctuation.

### Key empirical cases

- **Leaderboard reordering (DOCUMENTED). Alzahrani, N. et al. (2024). "When Benchmarks are Targets: Revealing the Sensitivity of Large Language Model Leaderboards." ACL 2024 (Long).** arXiv:2402.01781; ACL Anthology 2024.acl-long.744. *(National Center for AI / SDAIA, Riyadh.)*
  On MMLU and similar MCQ benchmarks, minor *non-semantic* perturbations — reordering answer choices, changing the answer-extraction method, changing the choice symbol — shift leaderboard rankings by **up to 8 positions**. A real, published case where brittleness corrupted a public model comparison, not a hypothetical.

- **Divergent MMLU implementations (DOCUMENTED). Hugging Face Open LLM Leaderboard / MMLU investigation (2023).** HF blog "What's going on with the Open LLM Leaderboard?".
  Three implementations of *the same* MMLU benchmark (original Berkeley, Stanford HELM, EleutherAI lm-eval-harness) produced *materially different* scores for the same models — driven by prompt-template differences (e.g. `Question:` prefix, how choices are labeled, whether the harness scores the letter or the answer text). A practitioner-facing case showing brittleness leaks into "official" numbers.

- **Structured-prompt ranking shifts (DOCUMENTED, supporting).** Recent work reports that switching to structured prompting raises accuracy ~6% on average and shifts rankings on 5 of 7 benchmarks (arXiv:2511.20836). Corroborates that format choice changes comparative conclusions, not just absolute scores. *(Use as corroboration; verify exact framing before quoting.)*

---

## 2. The Core Concept — State of the Field

### What is settled
- LLMs are measurably sensitive to **semantically-neutral** prompt changes: separators, casing, spacing, colon-vs-dash, item delimiters, few-shot example order, and equivalent paraphrases. The effect is large enough to flip discrete outputs and to reorder model rankings (Sclar 2024; Lu 2022; Mizrahi 2024; Alzahrani 2024).
- The magnitude can be extreme on some tasks/models (tens of accuracy points; ~76 pts for LLaMA-2-13B in Sclar 2024).
- **Single-format / single-prompt evaluation overestimates reliability and can mislead model comparison.** Reporting a distribution over plausible prompts is the field's recommended correction (Sclar 2024; Mizrahi 2024; Polo 2024 PromptEval, NeurIPS 2024, arXiv:2405.17202).
- Scale **reduces but does not eliminate** brittleness — larger and instruction-tuned models are still sensitive (Sclar 2024; Leidinger 2023).

### What is disputed
- *Why* brittleness happens at the mechanism level — surface-feature shortcut learning vs tokenization artifacts vs decision-boundary proximity vs training-distribution format priors — is not settled; papers measure it more than they explain it.
- Whether richer specification *reliably* lowers variance or merely *shifts* the sensitive surface (formatting vs wording vs ordering) is partly open; Leidinger (2023) shows linguistic factors matter too.
- Whether mitigations like MOF generalize across task types and larger models, or are partial patches, is unsettled (Ngweta 2025 is an SRW-scale study).
- For demonstrations specifically, Min et al. (2022, "Rethinking the Role of Demonstrations," EMNLP) found *label correctness* in few-shot examples matters surprisingly little — what matters is label space, input distribution, and **format** — which sharpens the claim that format, not content, often drives few-shot behavior.

### What has changed recently (last 5 years)
- 2022: ordering sensitivity formalized (Lu); role-of-demonstrations reframed around format (Min).
- 2023: sensitivity broadened to linguistic properties (Leidinger); FormatSpread preprint.
- 2024: brittleness moves from curiosity to **evaluation methodology problem** — FormatSpread (ICLR), multi-prompt evaluation call (Mizrahi, TACL), leaderboard-sensitivity exposé (Alzahrani, ACL), and efficient distribution-estimation (Polo, PromptEval, NeurIPS).
- 2025: targeted mitigations (MOF, Ngweta, NAACL SRW) and continued structured-prompting / standardization efforts (lm-eval-harness YAML templating).

---

## 3. Application Domain Examples

1. **Model selection / procurement evals (DOCUMENTED).** A team picking between models on MMLU can get different winners depending on choice ordering and answer-extraction (Alzahrani 2024). Lesson: report multi-prompt distributions before signing a vendor.
2. **Reproducing a published benchmark number (DOCUMENTED).** Same model + same benchmark + different harness template ⇒ different score (HF MMLU investigation). Lesson: pin the exact prompt template, not just the dataset.
3. **Few-shot classification in production (DOCUMENTED mechanism, illustrative deployment).** Reordering or restyling few-shot exemplars during a prompt refactor can silently shift a classifier's accuracy/operating point (Lu 2022; Min 2022). Lesson: treat the prompt template as a versioned artifact under regression testing.
4. **Structured-output extraction (DOCUMENTED mechanism).** Switching delimiters (JSON vs key-value vs markdown) or list formatting changes parse success and content (Sclar 2024 covers item-formatting variants). Lesson: choose a format empirically and test variants, don't assume neutrality.
5. **Regression-safe prompt edits (DECISION PROCEDURE).** Before shipping a "cosmetic" prompt change, run the candidate against held-out cases under several format variants (FormatSpread-style) or estimate the distribution cheaply (PromptEval). Lesson: cosmetic edits are not cosmetic.

---

## 4. The Book's Thesis Connection

Brittleness is the empirical refutation of "just ask better." If a semantically-neutral edit — a colon for a dash, a reordering of identical examples — can swing a discrete metric by 20%+ (or 76 points in the extreme), then prompt quality is **not** a property you can intuit and declare; it is a property you must *measure*, with confidence intervals over plausible variants. This is the mechanism-first, falsifiable spine in miniature:

- **Falsifiable claim:** "Prompt P performs at accuracy a." The brittleness literature shows this is ill-posed; the defensible claim is "Prompt *family* P has performance distribution with median *m* and spread *s* over plausible format variants" (Sclar; Mizrahi; Polo).
- **Named failure mode:** *single-format optimism* — reporting one format's number as the model's capability, and *format-confounded comparison* — declaring model A > B when the result is an artifact of the shared fixed format.
- **Decision procedure:** test format variants; report a range; only then optimize. Brittleness is therefore the core motivation for **automated prompt optimization** (the book's later chapters) — if humans can't reliably tell good formats from bad, and the surface is high-dimensional, you search it systematically. It also justifies *eval discipline* as a first-class engineering activity rather than an afterthought.

---

## 5. The AI Wayback Machine — Candidate Figures

- **Frank Yates (1902–1994), statistician.** Co-developer (with Fisher) of factorial experimental design and analysis of variance for designed experiments. *Connection:* format variants × tasks × models is a factorial design; brittleness is "the main effect of a nuisance factor is large." Anchor prompt: *"Treat prompt formatting as a designed experiment: lay out a factorial of separators, casing, and exemplar order, and estimate the variance attributable to format."* Skew flag: classical agricultural-statistics framing predates and ignores adaptive/ML evaluation; use as conceptual scaffold, not method.

- **Gertrude Mary Cox (1900–1978), statistician.** Pioneer of experimental design (co-author *Experimental Designs*, 1950); founder of major statistics departments. Lesser-known relative to Fisher; good diversity choice. *Connection:* her insistence that *how you sample conditions* determines what conclusions are licensed maps onto "which format variants you test determines what you can claim about the model." Anchor prompt: *"Design a sampling plan over plausible prompt formats so the estimated performance interval is trustworthy under a fixed eval budget."* Skew flag: pre-computational; no notion of automated search like FormatSpread/PromptEval.

- **Donald T. Campbell (1916–1996), methodologist.** Originator (with Stanley) of **construct validity** and threats-to-validity analysis, and of the dictum later called Campbell's Law (when a measure becomes a target it ceases to be a good measure). *Connection:* brittleness is a *validity* problem — a single-format score is a construct-invalid proxy for "capability," and leaderboards illustrate Campbell's Law directly (cf. Alzahrani's title "When Benchmarks are Targets"). Anchor prompt: *"Audit this LLM eval for threats to construct validity: which observed differences are real capability and which are artifacts of a single fixed prompt format?"* Skew flag: social-science origin; the formalism is qualitative, not the quantitative spread machinery the chapter needs.

---

## 6. Pedagogical Delivery Research

- **Prior knowledge to activate:** sampling variance vs systematic bias; the difference between a point estimate and a distribution; factorial/nuisance factors; the idea of a confounder. Students with stats background grasp brittleness fast once it's framed as "format is a confounding factor."
- **Predicted misconceptions:**
  1. *"Semantically equivalent ⇒ behaviorally equivalent."* The core thing to break. Demonstrate live with a colon-vs-dash flip.
  2. *"It only affects small/weak models."* False — scale attenuates, doesn't remove (Sclar; Lu). Show persistence at larger sizes.
  3. *"My one good prompt proves the model can do X."* Conflates max-of-distribution with the distribution; tie to Mizrahi's metric taxonomy.
  4. *"More detail always reduces variance."* Partly true, but specificity can move the sensitive surface (Leidinger). Hedge, not cure.
  5. *"MOF / a trick fixes it."* It mitigates; underlying sensitivity persists.
- **What teaches it well:** a single reproducible demo — take one task, run 10–20 format variants, plot the accuracy histogram, show the spread. The histogram *is* the lesson. FormatSpread and PromptEval repos give ready scaffolding.
- **Teaching failure mode:** presenting brittleness as a list of "tips to avoid" (use this delimiter, not that). That re-installs the intuition-first error the chapter is trying to kill. Keep it measurement-first.
- **Understand vs memorize:** students should *understand* that format is a high-dimensional nuisance factor requiring distributional evaluation, and the *procedure* (sample variants → report interval). They need not memorize which specific separator wins on which task — that's exactly the brittle, non-generalizing knowledge the chapter warns against.

---

## 7. Representation and Display Research

A **format-variant-vs-accuracy table/figure is recommended** as the chapter's central artifact:
- A small **format-variant matrix**: rows = format variants (e.g. `Q:/A:`, `Question -/Answer -`, JSON, all-caps, reordered exemplars); columns = a couple of tasks and/or models; cells = accuracy. The visual point is the *range within a column*.
- A companion **performance-distribution histogram** (accuracy across N sampled formats, à la FormatSpread Fig.) annotated with median and 95% interval — this directly visualizes "report a range, not a point."
- Optional **ranking-instability strip**: model ranking under format A vs format B with crossing lines (à la Alzahrani / Mizrahi) to dramatize relative-order flips.

---

## 8. Open Questions and Research Gaps

- **Mechanism.** No settled first-principles account of *why* neutral edits move outputs (shortcut features vs tokenization vs decision-boundary geometry vs format priors from pretraining). The chapter can state this honestly as open.
- **Predictability.** Can we predict, a priori, which prompts/tasks are brittle, instead of measuring post hoc? Largely unsolved.
- **Generalization of mitigations.** Do MOF, ensembling, or robust-format search transfer across model families and task types, or overfit the eval? (Ngweta 2025 is small-scale.)
- **Eval-budget tradeoffs.** PromptEval estimates distributions at 1–4× single-prompt cost; what's the right standard for "enough" variants in production gating? No consensus.
- **Frontier/aligned models.** Does heavy RLHF/instruction tuning meaningfully shrink brittleness on agentic/long-form tasks, or just on MCQ? Evidence is mostly MCQ-centric.
- **Interaction with chain-of-thought / reasoning models.** Whether explicit reasoning traces dampen format sensitivity is under-studied.

---

## 9. Sourcing Notes

- **Verified (author/title/year/venue/ID):** Sclar et al. 2024 (ICLR 2024, arXiv:2310.11324, OpenReview RIu5lyNXjT) — "76 accuracy points" and persistence-with-scale claims confirmed from the abstract. Mizrahi et al. 2024 (TACL, 2024.tacl-1.52, DOI 10.1162/tacl_a_00681; ~6.5M instances / 20 LLMs / 39 tasks). Lu et al. 2022 (ACL 2022.acl-long.556; GlobalE/LocalE). Leidinger et al. 2023 (Findings EMNLP 2023.findings-emnlp.618). Polo et al. 2024 (PromptEval, NeurIPS 2024, arXiv:2405.17202). Alzahrani et al. 2024 (ACL 2024.acl-long.744, arXiv:2402.01781; "up to 8 positions"). Min et al. 2022 (EMNLP 2022.emnlp-main.759).
- **CORRECTED spine error:** MOF paper (Ngweta et al.) is **2025 NAACL Student Research Workshop** (arXiv:2504.06969, 2025.naacl-srw.51), *not* 2024. Affiliation IBM Research / RPI confirmed; authors Ngweta, Kate, Tsay, Rizk.
- **Spine claims confirmed as stated:** non-semantic changes cause measurable swings; discrete flips >20% on some tasks (FormatSpread's 76 pts is the strong form); smaller models more brittle but larger not immune; single-prompt evals overestimate reliability; multi-prompt evaluation is the recommended correction.
- **Verify-before-quote:** the "structured prompting +6%, 5/7 benchmark ranking shifts" figure (arXiv:2511.20836) is corroborating but I did not fetch the full paper; treat as supporting, not load-bearing.
- **No fetches were blocked.** All sourcing via web search of arXiv / ACL Anthology / OpenReview / HF blog; no full-text PDF parsing was required for the verified numbers, which appear in abstracts/landing pages.
