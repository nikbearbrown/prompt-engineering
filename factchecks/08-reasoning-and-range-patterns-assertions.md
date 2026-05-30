# Assertions Report: 08-reasoning-and-range-patterns.md

**Date:** 2026-05-30
**Source file:** chapters/08-reasoning-and-range-patterns.md
**Assertions flagged:** 7
**Breakdown:** STAT: 3 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 4 | SPECIALIST: 0 | CURRENT: 1

---

## ⚠️ Critical — Requires Immediate Expert Review

None found. All flagged assertions resolved to CONFIRMED.

---

## Full Findings

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Kojima et al. (2022) measured exactly this jump on text-davinci-002: MultiArith went from 17.7% to 78.7%, GSM8K from 10.4% to 40.7%..."
**Claim checked:** MultiArith 17.7→78.7 and GSM8K 10.4→40.7 zero-shot-CoT figures.
**Site visited:** arXiv:2205.11916 (MultiArith figure re-verified Ch.2; GSM8K figure from same results table).
**Finding:** MultiArith 17.7→78.7 confirmed exactly (Ch.2). GSM8K 10.4%→40.7% is the companion figure from the same Kojima results table for text-davinci-002. Consistent and accurate.
**Expert review needed:** No
**Suggested reference:** Kojima, T., et al. Large Language Models are Zero-Shot Reasoners. NeurIPS 2022. arXiv:2205.11916.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Min et al. (2022, 'Rethinking the Role of Demonstrations')... randomizing the labels barely dented performance — while the label space, the input distribution, and the format did the work."
**Claim checked:** Random-label finding and the three drivers (label space, input distribution, format), arXiv:2202.12837.
**Site visited:** https://arxiv.org/abs/2202.12837 (re-verified live 2026-05-30).
**Finding:** Exact match — randomly replacing labels barely hurts performance across 12 models including GPT-3; label space, input-text distribution, and sequence format are the drivers. EMNLP 2022.
**Expert review needed:** No
**Suggested reference:** Min, S., et al. Rethinking the Role of Demonstrations. EMNLP 2022. arXiv:2202.12837.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Self-consistency (Wang et al. 2022, 'Self-Consistency Improves Chain of Thought Reasoning')... sample many CoT trajectories at non-zero temperature, then take the majority-vote answer."
**Claim checked:** Self-consistency method and attribution, arXiv:2203.11171.
**Site visited:** arXiv:2203.11171.
**Finding:** Correct — sample diverse reasoning paths, marginalize by majority vote. ICLR 2023. Accurate description.
**Expert review needed:** No
**Suggested reference:** Wang, X., et al. Self-Consistency Improves Chain of Thought Reasoning. ICLR 2023. arXiv:2203.11171.
**Notes:** None.

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Wang and Zhou (2024...) showed that inspecting the top-k alternative first tokens... yielding roughly ten to thirty absolute GSM8K points across the PaLM-2 family with no prompt change."
**Claim checked:** CoT-decoding mechanism and ~10–30 absolute-point GSM8K gains (arXiv:2402.10200).
**Site visited:** arXiv:2402.10200 (paper confirmed Ch.1).
**Finding:** Mechanism (top-k first-token inspection surfaces latent CoT) confirmed. The "10–30 absolute points across PaLM-2" is a reasonable characterization of the paper's reported gains; magnitude is consistent with the paper's results tables.
**Expert review needed:** No
**Suggested reference:** Wang, X., & Zhou, D. Chain-of-Thought Reasoning Without Prompting. NeurIPS 2024. arXiv:2402.10200.
**Notes:** Exact per-model deltas vary by task; the band is a fair summary.

### EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Wei et al. (2022) reported that chain-of-thought's benefit appears in large models and is negligible or negative in small ones... 540B PaLM with eight CoT exemplars reached state-of-the-art on GSM8K." + Wang et al. (2023) invalid-steps 80–90%.
**Claim checked:** Emergence with scale; 8 exemplars; GSM8K SOTA (arXiv:2201.11903) and invalid-rationale result (arXiv:2212.10001).
**Site visited:** arXiv:2201.11903, arXiv:2212.10001 (confirmed Ch.2).
**Finding:** Accurate (see Ch.2 report). Confirmed.
**Expert review needed:** No
**Suggested reference:** Wei, J., et al. arXiv:2201.11903; Wang, B., et al. arXiv:2212.10001.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "the order of those exemplars is itself a brittleness surface that can swing accuracy dramatically (Lu et al. 2022)."
**Claim checked:** Prompt-order sensitivity attribution.
**Site visited:** ACL Anthology — Lu et al., "Fantastically Ordered Prompts and Where to Find Them," ACL 2022.
**Finding:** Correct — exemplar ordering can swing accuracy from near-SOTA to near-random; the paper documents this and proposes entropy-based ordering selection. Accurate.
**Expert review needed:** No
**Suggested reference:** Lu, Y., et al. Fantastically Ordered Prompts and Where to Find Them. ACL 2022. (arXiv:2104.08786)
**Notes:** Chapter omits the arXiv ID; 2104.08786 if the author wants it.

### CURRENT / EVIDENCE — CONFIRMED (preprint)
**Assertion type:** POSITIVE
**Sentence:** "Meincke et al. (2025...) report that for non-reasoning models explicit CoT still gives small average gains, but for reasoning-tuned models the gains are marginal and CoT adds answer-to-answer variance, sometimes flipping otherwise-correct answers."
**Claim checked:** Prompting Science Report 2 scope-condition (arXiv:2506.07142).
**Site visited:** arXiv:2506.07142 (confirmed prior pass / Ch.1 / Ch.2).
**Finding:** Accurate characterization. Preprint; the chapter explicitly says to re-verify against current model tiers. Good practice.
**Expert review needed:** No
**Suggested reference:** Meincke, L., et al. Prompting Science Report 2. Wharton GAIL, 2025. arXiv:2506.07142.
**Notes:** None.

---

## Unverified Assertions

| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| The tighten/widen "operation on the output distribution" framing, attention-salience claims | SPECIALIST | BASIC | Mechanistic intuition built on Ch.1; the chapter explicitly flags it as intuition not interpretability-grounded. No external claim to verify. |

---

## AI-Pass Flags

- Citations are reused consistently with Chapters 1–2 (same arXiv IDs); no drift or contradiction.
- The chapter is careful to separate "stable mechanism" from "current model behavior" and to flag the reasoning-tuned-model finding as time-sensitive — good calibration for a fast-moving area.
- Body text calls the Meincke work "The Decreasing Value of Chain of Thought in Prompting" while References give the fuller "Prompting Science Report 2: The Decreasing Value of Chain of Thought in Prompting" — same work; consistent.

---

## References

(Chapter contains a complete, accurate References section; all ten entries checked and confirmed. Optional: add arXiv:2104.08786 for Lu et al. No corrections required.)
