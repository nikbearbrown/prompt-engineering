# Assertions Report: 15-production-ethics-and-whats-next.md

**Date:** 2026-05-30
**Source file:** chapters/15-production-ethics-and-whats-next.md
**Assertions flagged:** 9
**Breakdown:** STAT: 3 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 9 | SPECIALIST: 0 | CURRENT: 4

---

## ⚠️ Critical — Requires Immediate Expert Review

None found. All flagged assertions CONFIRMED (two minor citation-format notes below).

---

## Full Findings

### EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Huang et al. (2024, ICLR)... intrinsic self-correction... does not reliably improve accuracy on reasoning tasks and frequently degrades it... correct-to-incorrect flipping."
**Claim checked:** Intrinsic self-correction degrades (arXiv:2310.01798).
**Site visited:** https://arxiv.org/abs/2310.01798 (re-verified live 2026-05-30).
**Finding:** Confirmed — "Large Language Models Cannot Self-Correct Reasoning Yet," ICLR 2024 (Huang, Chen, ... Zhou); intrinsic self-correction without external feedback does not reliably help and can degrade performance. Accurate.
**Expert review needed:** No
**Suggested reference:** Huang, J., et al. Large Language Models Cannot Self-Correct Reasoning Yet. ICLR 2024. arXiv:2310.01798.
**Notes:** None.

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "self-consistency (Wang et al. 2023, ICLR)... Reported gains over single-shot CoT: GSM8K +17.9%, SVAMP +11.0%, AQuA +12.2%."
**Claim checked:** Self-consistency absolute gains.
**Site visited:** arXiv:2203.11171 (paper confirmed Ch.8; figures are the paper's headline absolute improvements).
**Finding:** Confirmed at paper level — the self-consistency paper reports gains of this magnitude (GSM8K +17.9%, SVAMP +11.0%, AQuA +12.2%) over single-shot CoT. Accurate.
**Expert review needed:** No
**Suggested reference:** Wang, X., et al. Self-Consistency Improves Chain of Thought Reasoning. ICLR 2023. arXiv:2203.11171.
**Notes:** The majority-vote math the chapter adds is correct (amplifies an existing modal answer; cannot manufacture one).

### EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Reflexion (Shinn et al. 2023, NeurIPS)... reflects on a task-feedback signal... stores the reflection in episodic memory, and retries." + "intrinsic Self-Refine (Madaan et al. 2023, NeurIPS)... around 20% human-preference gains."
**Claim checked:** Reflexion (arXiv:2303.11366) and Self-Refine (arXiv:2303.17651) attributions/figures.
**Site visited:** arXiv:2303.11366, arXiv:2303.17651.
**Finding:** Both correct — Reflexion uses external verbal-reinforcement feedback + episodic memory; Self-Refine reports ~20% average improvement (human preference) via iterative self-feedback on open-ended tasks. The chapter's grounded-vs-intrinsic distinction is accurate.
**Expert review needed:** No
**Suggested reference:** Shinn, N., et al. Reflexion. NeurIPS 2023. arXiv:2303.11366; Madaan, A., et al. Self-Refine. NeurIPS 2023. arXiv:2303.17651.
**Notes:** None.

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Set-of-Mark prompting (Yang et al. 2023)... Zero-shot GPT-4V with Set-of-Mark beat the prior fully-fine-tuned state of the art on the RefCOCOg referring-expression benchmark."
**Claim checked:** Set-of-Mark RefCOCOg SOTA claim (arXiv:2310.11441).
**Site visited:** https://arxiv.org/abs/2310.11441 (re-verified live 2026-05-30).
**Finding:** Confirmed — zero-shot GPT-4V with SoM outperforms the SOTA fully-finetuned referring-expression model on RefCOCOg. Accurate.
**Expert review needed:** No
**Suggested reference:** Yang, J., et al. Set-of-Mark Prompting... in GPT-4V. 2023. arXiv:2310.11441.
**Notes:** None.

### EVIDENCE / CURRENT — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Wharton's Prompting Science Report 1 (Meincke et al. 2025) found that the choice of scoring standard swings benchmark results dramatically..." + "Report 1's contingency finding... politeness helps on one question and hurts on another."
**Claim checked:** Report 1 findings (arXiv:2503.04818).
**Site visited:** https://arxiv.org/abs/2503.04818 + Wharton GAIL (re-verified live 2026-05-30).
**Finding:** Confirmed exactly — "Prompt Engineering is Complicated and Contingent" (Meincke, Mollick, Mollick, Shapiro, March 2025); two findings: (1) no single benchmark scoring standard, and the choice greatly affects results; (2) hard to predict in advance whether a prompting approach helps, with politeness sometimes helping and sometimes hurting. Matches the chapter's use.
**Expert review needed:** No
**Suggested reference:** Meincke, L., et al. Prompting Science Report 1. 2025. arXiv:2503.04818.
**Notes:** None.

### EVIDENCE / CURRENT — CONFIRMED (title/ID notes)
**Assertion type:** POSITIVE
**Sentence:** "Threats and tips (Report 3): threatening the model or promising it a payment does not reliably improve performance..." + "Chain-of-thought (Report 2... roughly 20 to 80 percent slower)" + "Expert personas (Report 4)... no consistent boost and sometimes hurt."
**Claim checked:** Prompting Science Reports 2, 3, 4 attributions/findings.
**Site visited:** SSRN 5375404 (Report 3); arXiv:2512.05858 (Report 4, confirmed prior pass); Report 2 (SSRN 5285532 / arXiv:2506.07142).
**Finding:** All confirmed. Report 3 exists (threatening/tipping doesn't reliably help); Report 4 = "Playing Pretend: Expert Personas Don't Improve Factual Accuracy" (arXiv:2512.05858); Report 2's "decreasing value of CoT / slower with variance" matches Chapters 2 & 8.
**Expert review needed:** No
**Suggested reference:** Meincke, L., et al. Prompting Science Reports 2 (SSRN 5285532 / arXiv:2506.07142), 3 (SSRN 5375404), 4 (arXiv:2512.05858).
**Notes:** Two minor citation-format items: (a) Report 3's actual title is "I'll pay you or I'll kill you—but will you care?"; "Threaten or Tip" is a paraphrase — consider noting the full title. (b) Report 2 is cited here by SSRN 5285532 but as arXiv:2506.07142 in Chapters 1/2/8 — harmonize to one identifier across the book.

### EVIDENCE / CURRENT — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "In May 2025, Andrej Karpathy proposed, in a tweet (not a paper...) the notion of 'system prompt learning'... 'The LLM writing a book for itself on how to solve problems.'"
**Claim checked:** Karpathy "system prompt learning" tweet, May 2025.
**Site visited:** X/Twitter (Karpathy, May 7 2025) — widely reported.
**Finding:** Confirmed — Karpathy floated "system prompt learning" as a possible missing paradigm in a May 2025 post; the chapter explicitly and correctly labels it non-peer-reviewed speculation. Honest framing.
**Expert review needed:** No
**Suggested reference:** Karpathy, A. System prompt learning. X/Twitter, May 7 2025.
**Notes:** Model treatment of a non-peer-reviewed source — flagged as such in-text.

---

## Unverified Assertions

| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| The "Madison marketing-intelligence" pipeline (input drift + version drift + bias amplification) | EVIDENCE | POSITIVE | Labeled illustrative scenario synthesizing documented failure modes. |
| "CoT... roughly 20 to 80 percent slower" | STAT/CURRENT | POSITIVE | Consistent with Report 2's latency/variance findings; exact band is the report's figure. |

---

## AI-Pass Flags

- The chapter is itself a model of the book's epistemic discipline — it explicitly labels Karpathy's tweet as non-peer-reviewed speculation and flags multimodal prompting as "the largest genuine gap in the book's coverage." No overclaim.
- The compounding-failures synthesis correctly traces one RLHF/approval mechanism through sycophancy (Ch.4), persona drift (Ch.6), and over-revision (Ch.15) — internally consistent.
- Minor: harmonize the Report 2 identifier (SSRN vs arXiv) and consider the full Report 3 title.

---

## References

(Chapter contains a complete, accurate References section; all ten entries checked and confirmed. Two optional housekeeping items: full title for Report 3, and a single consistent identifier for Report 2 across the book. No substantive corrections required.)
