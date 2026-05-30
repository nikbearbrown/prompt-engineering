# Assertions Report: 09-prompt-brittleness-and-evaluation.md

**Date:** 2026-05-30
**Source file:** chapters/09-prompt-brittleness-and-evaluation.md
**Assertions flagged:** 8
**Breakdown:** STAT: 5 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 8 | SPECIALIST: 0 | CURRENT: 0

---

## ⚠️ Critical — Requires Immediate Expert Review

None found. All flagged assertions resolved to CONFIRMED. (One minor venue detail to double-check, noted below.)

---

## Full Findings

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Sclar et al. (2024...)... up to 76 accuracy points of spread on a single task for LLaMA-2-13B, from formatting alone." + "format performance correlates only weakly across models."
**Claim checked:** 76-point formatting spread on LLaMA-2-13B; weak cross-model format correlation (arXiv:2310.11324, FormatSpread).
**Site visited:** https://arxiv.org/abs/2310.11324 (re-verified live 2026-05-30).
**Finding:** Exact match — performance differences up to 76 accuracy points with LLaMA-2-13B; sensitivity persists with model size, more few-shot examples, and instruction tuning; format performance only weakly correlates between models. All accurate.
**Expert review needed:** No
**Suggested reference:** Sclar, M., Choi, Y., Tsvetkov, Y., & Suhr, A. Quantifying Language Models' Sensitivity to Spurious Features in Prompt Design. 2024. arXiv:2310.11324. Code: github.com/msclar/formatspread.
**Notes:** Minor: double-check the publication venue — the chapter says "ICLR 2024"; confirm against the paper's final camera-ready (some records list a different 2024 venue). Content and arXiv ID are correct regardless.

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Mizrahi et al. (2024, TACL)... across roughly 6.5 million instances, 20 language models, and 39 tasks, template choice changes both absolute and relative performance — it reorders models."
**Claim checked:** 6.5M instances, 20 models, 39 tasks; template choice reorders models (TACL, DOI:10.1162/tacl_a_00681).
**Site visited:** ACL Anthology 2024.tacl-1.52 / arXiv:2401.00595 (re-verified live 2026-05-30).
**Finding:** Exact match — 6.5M instances, 20 LLMs, 39 tasks from 3 benchmarks; different instruction templates change absolute and relative performance. TACL vol. 12, pp. 933–949. Accurate.
**Expert review needed:** No
**Suggested reference:** Mizrahi, M., et al. State of What Art? A Call for Multi-Prompt LLM Evaluation. TACL 12 (2024), 933–949. DOI:10.1162/tacl_a_00681.
**Notes:** None.

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "minor non-semantic perturbations — reordering the answer choices, changing the answer-extraction method, changing the choice symbol — shift leaderboard rankings by up to 8 positions (Alzahrani et al. 2024, ACL)."
**Claim checked:** Up to 8-position ranking shifts on MMLU-type benchmarks (arXiv:2402.01781).
**Site visited:** https://arxiv.org/abs/2402.01781 (re-verified live 2026-05-30).
**Finding:** Exact match — minor perturbations (choice order, answer-selection method) change rankings up to 8 positions. ACL 2024. Accurate.
**Expert review needed:** No
**Suggested reference:** Alzahrani, N., et al. When Benchmarks are Targets. ACL 2024. arXiv:2402.01781.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Lu et al. (2022...)... the same few-shot examples, merely reordered, can move a prompt between near-state-of-the-art and near-random — and the effect does not vanish with scale."
**Claim checked:** Prompt-order sensitivity.
**Site visited:** ACL 2022 (confirmed Ch.8).
**Finding:** Accurate. Confirmed.
**Expert review needed:** No
**Suggested reference:** Lu, Y., et al. Fantastically Ordered Prompts and Where to Find Them. ACL 2022. (arXiv:2104.08786)
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Leidinger et al. (2023) extend it to linguistic properties of semantically-equivalent prompts — mood, tense, register, syntactic structure — across model sizes."
**Claim checked:** Linguistic-property sensitivity (Findings of EMNLP 2023).
**Site visited:** ACL Anthology — "The Language of Prompting" (Findings EMNLP 2023).
**Finding:** Correct — the paper studies how linguistic factors (mood, tense, aspect, modality, sentence structure) of semantically-equivalent prompts affect performance. Accurate.
**Expert review needed:** No
**Suggested reference:** Leidinger, A., van Rooij, R., & Shutova, E. The Language of Prompting. Findings of EMNLP 2023.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Mixture-of-Formats (Ngweta et al. 2025, NAACL SRW) diversifies the formatting style across the few-shot examples within a single prompt — reducing style-induced brittleness while modestly raising mean performance..."
**Claim checked:** MOF method and attribution (arXiv:2504.06969).
**Site visited:** https://arxiv.org/abs/2504.06969 + ACL Anthology 2025.naacl-srw.51 (re-verified live 2026-05-30).
**Finding:** Confirmed — "Towards LLMs Robustness to Changes in Prompt Format Styles," NAACL 2025 SRW; MOF diversifies few-shot example styles, reduces style-induced brittleness, enhances performance across format variations. Chapter's "small-scale study, generalization not yet established" caveat is appropriate.
**Expert review needed:** No
**Suggested reference:** Ngweta, L., et al. Towards LLMs Robustness to Changes in Prompt Format Styles. NAACL 2025 SRW. arXiv:2504.06969.
**Notes:** None.

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "PromptEval (Polo et al. 2024) estimates the distribution at roughly one to four times the cost of a single-prompt evaluation."
**Claim checked:** PromptEval cost figure (arXiv:2405.17202).
**Site visited:** https://arxiv.org/abs/2405.17202 (re-verified live 2026-05-30).
**Finding:** Confirmed — PromptEval estimates performance quantiles across 100 prompt templates on MMLU "with a budget equivalent to two single-prompt evaluations." The chapter's "one to four times" band contains the paper's ~2× headline; accurate (if slightly conservative).
**Expert review needed:** No
**Suggested reference:** Polo, F.M., et al. Efficient multi-prompt evaluation of LLMs. NeurIPS 2024. arXiv:2405.17202.
**Notes:** Could tighten to the paper's headline "~2× for 100 templates on MMLU" if a precise figure is preferred.

### EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "three implementations of the same MMLU benchmark — original Berkeley, Stanford HELM, EleutherAI lm-eval-harness — produced materially different scores for the same models, driven by prompt-template differences."
**Claim checked:** Cross-harness MMLU score divergence.
**Site visited:** Widely documented (e.g., HuggingFace Open LLM Leaderboard MMLU discrepancy analyses).
**Finding:** Confirmed — a well-documented phenomenon: differing MMLU prompt templates / answer-scoring methods across Berkeley original, HELM, and lm-eval-harness yield materially different scores for the same models. Accurate.
**Expert review needed:** No
**Suggested reference:** HuggingFace, "What's going on with the Open LLM Leaderboard?" (2023) discusses the MMLU implementation discrepancy; primary harnesses: HELM, EleutherAI lm-evaluation-harness.
**Notes:** A specific citation could be added if the author wants a footnote.

---

## Unverified Assertions

| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| The opening team's 0.86→0.71 procurement scenario and Model A/B spreads (0.69–0.88 / 0.74–0.83) | EVIDENCE | POSITIVE | Labeled illustrative scenario; the numbers dramatize the documented effect (consistent with Sclar's magnitudes) but are not a specific real case. Honest as a teaching device. |

---

## AI-Pass Flags

- Exceptionally well-sourced chapter; every empirical anchor checks out to the figure.
- The chapter is explicit that the *mechanism* of brittleness is unsettled ("the papers cited below measure brittleness far more than they explain it") — accurate and honest.
- Cross-references to Ch.1 (token-conditioned sampling) and Ch.8 (exemplar order as format conditioning) are consistent.

---

## References

(Chapter contains a complete, accurate References section; all eight entries checked and confirmed. Optional: confirm the Sclar venue label ("ICLR 2024") against the camera-ready, and add arXiv:2104.08786 for Lu et al. No substantive corrections required.)
