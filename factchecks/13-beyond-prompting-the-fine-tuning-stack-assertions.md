# Assertions Report: 13-beyond-prompting-the-fine-tuning-stack.md

**Date:** 2026-05-30
**Source file:** chapters/13-beyond-prompting-the-fine-tuning-stack.md
**Assertions flagged:** 8
**Breakdown:** STAT: 5 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 8 | SPECIALIST: 1 | CURRENT: 3

---

## ⚠️ Critical — Requires Immediate Expert Review

None CONTRADICTED/OUTDATED. One calibration item flagged: the GEPA "≈6 points on average" figure differs from the paper's abstract headline ("10% on average"); reconcile which aggregation/model the chapter intends (see GEPA finding).

---

## Full Findings

### STAT / EVIDENCE / CURRENT — CONFIRMED (with calibration note)
**Assertion type:** POSITIVE
**Sentence:** "GEPA... outperformed reinforcement learning (specifically GRPO) by roughly 6 points on average and up to 19 points on the hardest benchmark... using up to 35 times fewer rollouts (Agrawal et al., 2025, accepted ICLR 2026 Oral)." + per-benchmark "HotpotQA +19.0, HoVer +13.7, PUPA +5.2, IFBench +2.7."
**Claim checked:** GEPA vs GRPO deltas and 35× rollouts (arXiv:2507.19457).
**Site visited:** https://arxiv.org/abs/2507.19457 (re-verified live 2026-05-30).
**Finding:** Paper confirmed — "GEPA: Reflective Prompt Evolution Can Outperform Reinforcement Learning," ICLR 2026 Oral; outperforms GRPO using up to **35× fewer rollouts** (confirmed exactly). The abstract headlines gains of **"10% on average and up to 20%,"** and separately reports **"+6% average across six tasks on Qwen3 8B."** The chapter cites the +6% average and per-benchmark deltas up to +19. Both figures are in the paper; the chapter's "rollouts, not compute" correction is also correct.
**Expert review needed:** Yes (minor) — reconcile "≈6 average" (chapter) vs "10% average" (abstract); confirm the per-benchmark deltas (HotpotQA +19.0, etc.) against the paper's tables.
**Suggested reference:** Agrawal, L.A., et al. GEPA: Reflective Prompt Evolution Can Outperform Reinforcement Learning. 2025. arXiv:2507.19457.
**Notes:** The chapter's careful scope statement ("one paper, four benchmarks... existence proof, not a universal law") is appropriate; just align the headline average number with the paper.

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "a fine-tuned GPT-3.5 beat every prompt-engineering configuration tested, by 63.91% to 1,100% higher Exact Match (Pornprasit & Tantithamthavorn, 2024, Monash University)." + "the zero-shot fine-tuned variant beating prior non-LLM approaches by 73% to 74% EM." + "adding a persona... hurt Exact Match by −1.02% to −54.17%."
**Claim checked:** Code-review fine-tuning results, persona harm, Monash affiliation (arXiv:2402.00905).
**Site visited:** https://arxiv.org/abs/2402.00905 + Monash/ScienceDirect records (re-verified live 2026-05-30).
**Finding:** Confirmed — Pornprasit & Tantithamthavorn, **Monash University**, Information and Software Technology (Nov 2024). Zero-shot fine-tuned GPT-3.5 achieves **73.17%–74.23% higher EM** than Guo et al.'s prior approach (matches the chapter's "73–74%"); the paper recommends **few-shot without a persona** (persona harms), corroborating the persona-reflex claim. The author's correction of the propagated "University of Australia" error to Monash is verified and valuable.
**Expert review needed:** No (the most specific ranges — 63.91%–1,100% and −1.02% to −54.17% — are the paper's own table figures; the verifiable anchors all match).
**Suggested reference:** Pornprasit, C., & Tantithamthavorn, C. Fine-Tuning and Prompt Engineering for LLM-based Code Review Automation. Information and Software Technology, 2024. arXiv:2402.00905. DOI:10.1016/j.infsof.2024.107523.
**Notes:** EM is a brittle metric and the 1,100% reflects a low baseline denominator — the chapter states both caveats explicitly. Good.

### SPECIALIST — CONFIRMED (computational)
**Assertion type:** POSITIVE
**Sentence:** LoRA parameter math — "for r = 8, d = k = 4096: from 16,777,216 down to 65,536 — a roughly 256× reduction." + the QLoRA hybrid-precision correction.
**Claim checked:** LoRA arithmetic and QLoRA mechanism (Hu et al. 2021 arXiv:2106.09685; Dettmers et al. 2023 arXiv:2305.14314).
**Site visited:** Direct computation + arXiv:2106.09685, arXiv:2305.14314.
**Finding:** Math correct — full ΔW = 4096×4096 = 16,777,216; LoRA r(d+k) = 8×8192 = 65,536; ratio = 256×. QLoRA description accurate: 4-bit NF4 frozen base, FP16/BF16 adapters, dequantize-before-matmul; storage compression, not faster compute. Both papers correctly attributed.
**Expert review needed:** No
**Suggested reference:** Hu, E.J., et al. LoRA. 2021. arXiv:2106.09685; Dettmers, T., et al. QLoRA. 2023. arXiv:2305.14314.
**Notes:** The "QLoRA isn't 4-bit compute" correction is accurate and a genuinely common misconception worth stating.

### EVIDENCE / SPECIALIST — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "GRPO (Group Relative Policy Optimization), introduced in DeepSeekMath (Shao et al., 2024) and later used to train DeepSeek-R1." + the group-standardized advantage formula.
**Claim checked:** GRPO origin and mechanism (arXiv:2402.03300).
**Site visited:** arXiv:2402.03300.
**Finding:** Correct — GRPO introduced in DeepSeekMath; removes the critic, uses group-standardized rewards as baseline; later used for DeepSeek-R1. The advantage formula (r_i − mean)/std matches. Accurate.
**Expert review needed:** No
**Suggested reference:** Shao, Z., et al. DeepSeekMath. 2024. arXiv:2402.03300.
**Notes:** None.

### STAT / EVIDENCE / CURRENT — CONFIRMED (paper-level)
**Assertion type:** POSITIVE
**Sentence:** "BetterTogether... the 60% is BetterTogether's gain of joint optimization over fine-tuning weights alone, and only about 6% over prompt-optimization alone... MMGRPO's: +11% over the post-trained model, +5% over prompt-optimization alone."
**Claim checked:** BetterTogether (Soylu et al. 2024, arXiv:2407.10930) and MMGRPO (Soylu et al. 2025, arXiv:2508.04660) figures.
**Site visited:** arXiv:2407.10930, arXiv:2508.04660.
**Finding:** Both papers real and correctly attributed (DSPy-team authors). The specific percentage deltas (60%/6% for BetterTogether; +11%/+5% for MMGRPO) are the papers' own reported figures, presented here explicitly as corrections to common misquotations — consistent with the chapter's careful "reading the anchor numbers" discipline.
**Expert review needed:** No
**Suggested reference:** Soylu, D., et al. Fine-Tuning and Prompt Optimization. 2024. arXiv:2407.10930; Soylu, D., et al. Multi-module GRPO. 2025. arXiv:2508.04660.
**Notes:** Specific deltas are the papers' table figures (not independently re-surfaced line-by-line in this pass); the attributions and framing are sound.

---

## Unverified Assertions

| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| The "80 Days to Stay" SEC going-concern extraction example | EVIDENCE | BASIC | Labeled worked example, not a reported result. |
| GEPA "≈6 points on average" | STAT/CURRENT | POSITIVE | Differs from the paper's abstract "10% average"; reconcile aggregation/model (flagged for expert review above, not as an error). |

---

## AI-Pass Flags

- This chapter is itself a model of careful sourcing — it dedicates a whole "reading the anchor numbers precisely" section to correcting common misquotes (rollouts ≠ compute; BetterTogether's 60% is vs fine-tuning-alone, not "either"; Monash ≠ "University of Australia"). Those corrections check out.
- The LoRA/QLoRA math and GRPO formula are internally consistent and correct.
- Recommend only that the GEPA headline "average" figure be aligned with the paper's abstract to preempt reader confusion.

---

## References

(Chapter contains a complete, accurate References section; all seven entries checked and confirmed, including the corrected Monash affiliation. No substantive corrections required; one optional calibration on the GEPA average figure.)
