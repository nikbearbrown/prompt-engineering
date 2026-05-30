# Assertions Report: 06-persona-and-audience-patterns.md

**Date:** 2026-05-30
**Source file:** chapters/06-persona-and-audience-patterns.md
**Assertions flagged:** 7
**Breakdown:** STAT: 4 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 3 | SPECIALIST: 0 | CURRENT: 1

---

## ⚠️ Critical — Requires Immediate Expert Review

None CONTRADICTED/OUTDATED. One UNVERIFIED specific figure (the ">30% persona-consistency degradation over 8–12 turns") flagged below — the cited paper is real and on-topic, but the precise figure could not be confirmed from its abstract.

---

## Full Findings

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Kong et al. (2023) tested role-play prompting... Accuracy on one algebra benchmark rose from 53.5% to 63.8%; on a letter-concatenation task it jumped from 23.8% to 84.2%."
**Claim checked:** Role-play prompting AQuA 53.5→63.8 and Last Letter 23.8→84.2 (arXiv:2308.07702).
**Site visited:** https://arxiv.org/abs/2308.07702 (re-verified live 2026-05-30).
**Finding:** Exact match — on ChatGPT, AQuA rose 53.5%→63.8% and Last Letter Concatenation 23.8%→84.2%. NAACL 2024. Figures quoted correctly.
**Expert review needed:** No
**Suggested reference:** Kong, A., et al. Better Zero-Shot Reasoning with Role-Play Prompting. NAACL 2024. arXiv:2308.07702.
**Notes:** Figures are ChatGPT results; the chapter's "held across scales" refers to the paper's multi-model robustness, which it does test.

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Zheng et al. (2024) tested 162 personas across four model families on over two thousand knowledge questions and found that persona assignment produced no improvement on factual questions."
**Claim checked:** 162 personas, 4 model families, ~2,400 factual questions, no improvement (arXiv:2311.10054).
**Site visited:** https://arxiv.org/abs/2311.10054 (re-verified live 2026-05-30).
**Finding:** Exact match — 162 personas (6 interpersonal types, 8 domains), 4 LLM families, 2,410 factual questions; adding personas does not improve performance vs. no-persona control. Findings of EMNLP 2024.
**Expert review needed:** No
**Suggested reference:** Zheng, M., et al. When "A Helpful Assistant" Is Not Really Helpful. Findings of EMNLP 2024. arXiv:2311.10054.
**Notes:** "over two thousand" = 2,410; accurate.

### STAT / CURRENT — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "detailed expert personas were documented to reduce accuracy — one study found MMLU performance dropping from 71.6% to 66.3% when a specific expert persona was applied."
**Claim checked:** MMLU 71.6% → 66.3% under expert persona (PRISM, arXiv:2603.18507).
**Site visited:** https://arxiv.org/abs/2603.18507 + corroborating press (The Register, TechXplore) (re-verified live 2026-05-30).
**Finding:** Confirmed — USC PRISM paper reports MMLU dropping from a 71.6% baseline to 68.0% (minimum persona) and 66.3% (long persona). The chapter's 71.6%→66.3% matches the "long persona" condition.
**Expert review needed:** No
**Suggested reference:** Expert Personas Improve LLM Alignment but Damage Accuracy: ... with PRISM. 2026. arXiv:2603.18507.
**Notes:** Recent (March 2026) preprint; CURRENT/rapidly-evolving — re-verify at each printing. Consider noting the intermediate 68.0% (minimum persona) for completeness.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "The distinction was formalized by White et al. (2023) in a catalog of prompt patterns..." and "Xu, B., et al. (2023). ExpertPrompting... arXiv:2305.14688."
**Claim checked:** White et al. catalog (Persona / Audience Persona patterns) and ExpertPrompting reference.
**Site visited:** arXiv:2302.11382 (confirmed Ch.2) and arXiv:2305.14688.
**Finding:** Both correct. White et al. defines the Persona and Audience Persona patterns; ExpertPrompting (Xu et al. 2023) is correctly cited for detailed-expert prompting. Accurate.
**Expert review needed:** No
**Suggested reference:** White, J., et al. arXiv:2302.11382; Xu, B., et al. ExpertPrompting. arXiv:2305.14688.
**Notes:** The chapter's bibliographic note that the Audience Persona Pattern appears in the expanded/conference version and Vanderbilt site but not the original preprint is plausible and consistent with the catalog's publication history; not independently re-verified line-by-line in this pass (low priority).

### EVIDENCE / CURRENT — CONFIRMED (paper) / figure UNVERIFIED
**Assertion type:** POSITIVE
**Sentence:** "Measured quantitatively using persona-consistency metrics, self-consistency degrades by more than 30% after eight to twelve dialogue turns, even with context intact."
**Claim checked:** The >30% degradation over 8–12 turns figure, attributed to arXiv:2511.00222.
**Site visited:** https://arxiv.org/abs/2511.00222 (re-verified live 2026-05-30).
**Finding:** The paper is real and on-topic — "Consistently Simulating Human Personas with Multi-Turn Reinforcement Learning" (Abdulhai et al., Oct 2025); it defines persona-consistency metrics and documents drift. However, its abstract reports *reducing inconsistency by over 55%* via RL and does not state the specific ">30% degradation after 8–12 turns" baseline figure. That precise number could not be confirmed from the abstract/landing page; it may appear in the paper body or may be a paraphrase.
**Expert review needed:** Yes — verify the exact "30% / 8–12 turns" figure against the paper's body.
**Suggested reference:** Abdulhai, M., et al. Consistently Simulating Human Personas with Multi-Turn Reinforcement Learning. 2025. arXiv:2511.00222.
**Notes:** Attribution of the phenomenon is sound; only the exact magnitude/turn-range needs confirmation against the full text.

---

## Unverified Assertions

| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| "self-consistency degrades by more than 30% after eight to twelve dialogue turns" | STAT / CURRENT | POSITIVE | Cited paper (2511.00222) is real and on-topic but its abstract does not state this exact figure; needs confirmation against the paper body. Flagged inline. |
| "This information-loss effect is reported consistently in practitioner accounts." (Audience Persona suppressing detail) | EVIDENCE | BASIC | Attributed to "practitioner accounts," no specific source; plausible and the chapter frames it honestly as practitioner-reported. |

---

## AI-Pass Flags

- The March 2024 fracture-analysis / aircraft-fleet opening is a labeled illustrative scenario, not a documented event.
- The chapter is admirably explicit that the *behavioral* effects are reliable while the *mechanism* (co-occurrence hypothesis) is unconfirmed — this matches the literature and avoids overclaiming.
- No internal contradictions; the four failure modes and diagnostic protocol are self-consistent and tie correctly to Ch.2 (plausibility–truth) and Ch.4 (context isolation).

---

## References

(Chapter already contains a References section; six entries. Five confirmed accurate (White, Kong, Zheng, Xu, PRISM). The sixth (arXiv:2511.00222) is a real paper correctly cited for the persona-drift phenomenon, but the specific ">30%/8–12 turns" figure it is cited for needs verification against the paper body. No additions required.)
