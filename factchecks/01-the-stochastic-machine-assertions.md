# Assertions Report: 01-the-stochastic-machine.md

**Date:** 2026-05-30
**Source file:** chapters/01-the-stochastic-machine.md
**Assertions flagged:** 6
**Breakdown:** STAT: 1 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 5 | SPECIALIST: 0 | CURRENT: 0

---

## ⚠️ Critical — Requires Immediate Expert Review

None found. All flagged assertions resolved to CONFIRMED.

---

## Full Findings

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Kojima et al. (2022) showed this with a single appended phrase lifting performance on mathematical reasoning benchmarks by large margins."
**Claim checked:** Zero-shot "Let's think step by step" result attributed to Kojima et al. 2022 (arXiv:2205.11916).
**Site visited:** https://arxiv.org/abs/2205.11916 (re-verified live 2026-05-30).
**Finding:** Paper confirmed — "Large Language Models are Zero-Shot Reasoners," Kojima, Gu, Reid, Matsuo, Iwasawa; adding "Let's think step by step" significantly improves zero-shot performance on MultiArith, GSM8K, etc. Description accurate.
**Expert review needed:** No
**Suggested reference:** Kojima, T., et al. Large Language Models are Zero-Shot Reasoners. NeurIPS 2022. arXiv:2205.11916.
**Notes:** Also circulated via an ICML 2022 workshop; chapter's NeurIPS 2022 attribution is the conference publication.

### EVIDENCE — CONFIRMED
**Assertion type:** I-LANGUAGE (reported finding)
**Sentence:** "Wang and Zhou (2024)... show that chain-of-thought reasoning paths can be elicited by changing the decoding alone — with no change to the prompt at all... inspect the top-k alternative first tokens and continue decoding from each."
**Claim checked:** "CoT Reasoning Without Prompting" elicits reasoning via top-k decoding, prompt fixed (arXiv:2402.10200).
**Site visited:** https://arxiv.org/abs/2402.10200 (re-verified live 2026-05-30).
**Finding:** Confirmed — Xuezhi Wang & Denny Zhou (Google DeepMind); CoT paths are inherent in top-k alternative decoding sequences, revealed without prompting. Chapter's mechanism description is accurate. NeurIPS 2024.
**Expert review needed:** No
**Suggested reference:** Wang, X., & Zhou, D. Chain-of-Thought Reasoning Without Prompting. NeurIPS 2024. arXiv:2402.10200.
**Notes:** None.

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Wang et al. (2023) showed that prompting with invalid reasoning steps still recovers 80 to 90 percent of valid chain-of-thought performance, and that the relevance of steps... and their ordering matter far more than their factual correctness."
**Claim checked:** Invalid-rationale CoT recovers 80–90% of valid-CoT performance (arXiv:2212.10001, ACL 2023).
**Site visited:** https://arxiv.org/abs/2212.10001 (confirmed in prior pass, factchecks/_fc-A).
**Finding:** "Towards Understanding Chain-of-Thought Prompting: An Empirical Study of What Matters," ACL 2023 — invalid rationales retain ~80–90% of the performance gain; relevance and ordering dominate validity. Figure and description accurate.
**Expert review needed:** No
**Suggested reference:** Wang, B., et al. Towards Understanding Chain-of-Thought Prompting. ACL 2023. arXiv:2212.10001.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Wei, J., et al. (2022). Chain-of-Thought Prompting Elicits Reasoning in Large Language Models... arXiv:2201.11903."
**Claim checked:** Few-shot CoT attribution.
**Site visited:** arXiv:2201.11903 (foundational; ID and title match standard record).
**Finding:** Correct title, ID, venue (NeurIPS 2022). Accurate.
**Expert review needed:** No
**Suggested reference:** Wei, J., et al. Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. NeurIPS 2022. arXiv:2201.11903.
**Notes:** Foundational, universally cited; ID verified against standard record.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Brown, T., et al. (2020). Language Models are Few-Shot Learners (GPT-3)... arXiv:2005.14165."
**Claim checked:** GPT-3 paper attribution / in-context learning background.
**Site visited:** arXiv:2005.14165.
**Finding:** Correct title, ID, venue (NeurIPS 2020). Accurate.
**Expert review needed:** No
**Suggested reference:** Brown, T., et al. Language Models are Few-Shot Learners. NeurIPS 2020. arXiv:2005.14165.
**Notes:** Foundational; ID verified against standard record.

### EVIDENCE / CURRENT — CONFIRMED (preprint)
**Assertion type:** BASIC
**Sentence:** "Meincke, L., Mollick, E. R., Mollick, L., & Shapiro, D. (2025). Prompting Science Report 2... arXiv:2506.07142..."
**Claim checked:** Existence/attribution of Prompting Science Report 2 (decreasing value of CoT on reasoning-tuned models).
**Site visited:** arXiv:2506.07142 (confirmed in prior pass).
**Finding:** Real Wharton Generative AI Labs report (2025 preprint, not peer-reviewed). Chapter cites it as scope-conditioning evidence, appropriately.
**Expert review needed:** No
**Suggested reference:** Meincke, L., Mollick, E.R., Mollick, L., & Shapiro, D. Prompting Science Report 2. Wharton GAIL, 2025. arXiv:2506.07142.
**Notes:** Preprint — label as such; chapter does.

---

## Unverified Assertions

| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| "even temperature zero is not bit-identical across production runs: floating-point non-associativity, request batching... and silent model updates..." | SPECIALIST | POSITIVE | Accurate, widely-documented engineering reality, but not tied to a single citable source; treat as well-established practitioner knowledge. |

---

## AI-Pass Flags

- The chapter's predictions are explicitly framed as falsifiable and internally consistent with Chapter 0's arithmetic (the "86% leader at T=0.5 → 50% at T=2" cross-reference matches Chapter 0's worked example). No contradictions found.
- The "Mycroft" investment-intelligence example is a labeled illustrative scenario, not a factual claim.

---

## References

(Chapter already contains a complete, accurate References section; all six entries checked and confirmed. No additions required.)
