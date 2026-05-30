# Assertions Report: 02-hallucination-and-the-plausibility-truth-gap.md

**Date:** 2026-05-30
**Source file:** chapters/02-hallucination-and-the-plausibility-truth-gap.md
**Assertions flagged:** 6
**Breakdown:** STAT: 1 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 5 | SPECIALIST: 0 | CURRENT: 0

---

## ⚠️ Critical — Requires Immediate Expert Review

None found. All flagged assertions resolved to CONFIRMED.

---

## Full Findings

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Kojima et al. (2022) showed the bare phrase 'Let's think step by step' lifting one model on a multi-step arithmetic benchmark from 17.7% to 78.7%."
**Claim checked:** The specific MultiArith 17.7% → 78.7% zero-shot-CoT figure.
**Site visited:** https://arxiv.org/abs/2205.11916 (re-verified live 2026-05-30).
**Finding:** Confirmed — adding "Let's think step by step" raised MultiArith accuracy from 17.7% to 78.7% on InstructGPT (text-davinci-002). This is the paper's headline figure; quoted exactly.
**Expert review needed:** No
**Suggested reference:** Kojima, T., et al. Large Language Models are Zero-Shot Reasoners. NeurIPS 2022. arXiv:2205.11916.
**Notes:** The figure is model- and benchmark-specific (MultiArith, text-davinci-002); the chapter correctly says "one model on a multi-step arithmetic benchmark."

### EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Wei et al. (2022) showed eight reasoning exemplars taking a large model to then-state-of-the-art on grade-school mathematics, with the benefit emergent with scale — small models gained little or got worse."
**Claim checked:** Wei CoT — 8 exemplars, GSM8K SOTA, emergence with scale.
**Site visited:** arXiv:2201.11903.
**Finding:** Accurate — few-shot CoT used 8 exemplars, reached SOTA on GSM8K with PaLM 540B, and the gain was emergent with model scale. Correctly described.
**Expert review needed:** No
**Suggested reference:** Wei, J., et al. Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. NeurIPS 2022. arXiv:2201.11903.
**Notes:** None.

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Prompting with invalid reasoning steps recovered 80 to 90 percent of valid chain-of-thought performance."
**Claim checked:** Wang et al. 2023 invalid-rationale ablation (arXiv:2212.10001).
**Site visited:** arXiv:2212.10001 (confirmed prior pass + Ch.1).
**Finding:** Accurate; relevance and ordering dominate validity. Confirmed.
**Expert review needed:** No
**Suggested reference:** Wang, B., et al. Towards Understanding Chain-of-Thought Prompting. ACL 2023. arXiv:2212.10001.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "The architectural response to the plausibility–truth gap is the Fact-Check List Pattern, from the White et al. (2023) catalog of prompt patterns."
**Claim checked:** The Fact-Check List Pattern is a named pattern in White et al. 2023 (arXiv:2302.11382).
**Site visited:** https://arxiv.org/abs/2302.11382 and the Vanderbilt PDF (re-verified live 2026-05-30).
**Finding:** Confirmed — "Fact Check List" is one of the catalog's named patterns; its stated intent (have the LLM output the list of facts its answer depends on, for verification) matches the chapter's use exactly. Authors: White, Fu, Hays, Sandborn, Olea, Gilbert, Elnashar, Spencer-Smith, Schmidt.
**Expert review needed:** No
**Suggested reference:** White, J., et al. A Prompt Pattern Catalog to Enhance Prompt Engineering with ChatGPT. 2023. arXiv:2302.11382.
**Notes:** None.

### EVIDENCE / CURRENT — CONFIRMED (preprint)
**Assertion type:** BASIC
**Sentence:** "On reasoning-tuned models, Meincke and Mollick et al. (2025) report that explicit 'think step by step' sometimes adds answer-to-answer variance and can flip otherwise-correct answers."
**Claim checked:** Prompting Science Report 2 scope-condition claim (arXiv:2506.07142).
**Site visited:** arXiv:2506.07142 (confirmed prior pass).
**Finding:** Accurate characterization of the report. Preprint.
**Expert review needed:** No
**Suggested reference:** Meincke, L., Mollick, E.R., Mollick, L., & Shapiro, D. Prompting Science Report 2. Wharton GAIL, 2025. arXiv:2506.07142.
**Notes:** Preprint — chapter treats it as such.

---

## Unverified Assertions

| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| "Post-training alignment... optimizes for human approval... and can penalize the honest 'I don't have that.'" | SPECIALIST | POSITIVE | A correct, well-supported characterization of RLHF incentive structure, but a conceptual/mechanistic claim rather than a single-source finding; no web verification needed. |
| "models somewhat more often hedge an isolated claim than a buried one." | EVIDENCE | BASIC (hedged) | Explicitly hedged by the author as "a mild bonus, not a mechanism to rely on"; no specific study cited and none required. |

---

## AI-Pass Flags

- The "Mycroft" opening (a late-2025 analyst shipping a fabricated 10-K quote) is a labeled illustrative scenario, not a claim about a real documented event — correctly framed as such.
- The chapter's loss-function argument (cross-entropy has no truth term) is conceptually sound and internally consistent with Chapter 0's chain-rule treatment. No contradictions.

---

## References

(Chapter already contains a complete, accurate References section; all five entries checked and confirmed. No additions required.)
