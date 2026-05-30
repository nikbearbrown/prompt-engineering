# Assertions Report: 03-the-limits-of-syntax.md

**Date:** 2026-05-30
**Source file:** chapters/03-the-limits-of-syntax.md
**Assertions flagged:** 8
**Breakdown:** STAT: 1 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 5 | SPECIALIST: 0 | CURRENT: 0 | (2 UNVERIFIED author demonstrations)

---

## ⚠️ Critical — Requires Immediate Expert Review

None found (no OUTDATED/CONTRADICTED; no COMBINATION). Two UNVERIFIED author-demonstration anecdotes flagged below for sourcing.

---

## Full Findings

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "In 1980, John Searle published 'Minds, Brains, and Programs.'"
**Claim checked:** Searle 1980, Behavioral and Brain Sciences 3(3), 417–424.
**Site visited:** BBS archival PDFs (csulb.edu, yale.edu) + PhilPapers (re-verified live 2026-05-30).
**Finding:** Confirmed — published in The Behavioral and Brain Sciences, vol. 3 (1980). The target article occupies pp. 417–424; the full piece with open peer commentary and Searle's reply runs to ~457/458. The chapter's "417–424" is the target-article page range and is a legitimate citation.
**Expert review needed:** No
**Suggested reference:** Searle, J.R. Minds, Brains, and Programs. Behavioral and Brain Sciences, 3(3), 417–424, 1980.
**Notes:** If the author prefers to cite the whole article-plus-commentary unit, the range is 417–457; both forms are used in the literature.

### STAT / EVIDENCE — CONFIRMED (with calibration note)
**Assertion type:** BASIC
**Sentence:** "Then large models began scoring 90–95%." (Winograd Schema Challenge) ... "replace familiar nouns with nonsense words and performance drops dramatically. ... A 95% to 60% drop..."
**Claim checked:** WSC benchmark saturation (~90%+) and adversarial-variant performance collapse.
**Site visited:** Winograd Schema Challenge (Wikipedia) + WinoGrande, arXiv:1907.10641 (re-verified live 2026-05-30).
**Finding:** Confirmed in direction and roughly in magnitude. Transformer models reached >90% on the original WSC (BERT 90.1% in 2019; GPT-3 88.3% in 2020), and later models exceeded 90%. The adversarial WinoGrande dataset drops SOTA to ~59.4–79.1% vs. ~94% human — strongly supporting the "competence collapses on adversarial variants" argument and the illustrative "95%→60%" drop.
**Expert review needed:** No
**Suggested reference:** Sakaguchi, K., et al. WinoGrande: An Adversarial Winograd Schema Challenge at Scale. AAAI 2020. arXiv:1907.10641.
**Notes:** "90–95%" is at the optimistic edge for the original WSC at first saturation (~88–90%); later/stronger models do reach the low-to-mid 90s. Minor; not an error. Consider citing WinoGrande directly as the adversarial-collapse evidence.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "The Winograd Schema Challenge was designed in 2012 specifically to require commonsense reasoning."
**Claim checked:** WSC origin — Levesque, Davis & Morgenstern 2012.
**Site visited:** KR 2012 proceedings record.
**Finding:** Correct — proposed by Levesque, Davis & Morgenstern at KR 2012 as a commonsense-reasoning alternative to the Turing Test.
**Expert review needed:** No
**Suggested reference:** Levesque, H.J., Davis, E., & Morgenstern, L. The Winograd Schema Challenge. KR 2012.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** Self-attention equation "(Vaswani et al., 2017)."
**Claim checked:** Attention formula attribution.
**Site visited:** arXiv:1706.03762.
**Finding:** Correct — scaled dot-product attention as published. Accurate.
**Expert review needed:** No
**Suggested reference:** Vaswani, A., et al. Attention Is All You Need. NeurIPS 2017. arXiv:1706.03762.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Bender, E. M., & Koller, A. (2020). Climbing towards NLU: On Meaning, Form, and Understanding in the Age of Data."
**Claim checked:** Reference accuracy (ACL 2020, pp. 5185–5198).
**Site visited:** ACL Anthology record (2020.acl-main.463).
**Finding:** Correct title, venue, pages — the "octopus" form-vs-meaning argument that underpins the chapter's thesis.
**Expert review needed:** No
**Suggested reference:** Bender, E.M., & Koller, A. Climbing towards NLU. ACL 2020, 5185–5198.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Schick, T., et al. (2023). Toolformer: Language Models Can Teach Themselves to Use Tools... arXiv:2302.04761."
**Claim checked:** Toolformer reference (supports the agentic tool-use section).
**Site visited:** arXiv:2302.04761.
**Finding:** Correct title and ID; NeurIPS 2023. Accurate.
**Expert review needed:** No
**Suggested reference:** Schick, T., et al. Toolformer. NeurIPS 2023. arXiv:2302.04761.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Wang et al. (2023) showed that invalid reasoning steps recover 80 to 90 percent of valid chain-of-thought performance..."
**Claim checked:** Same as Ch.1/Ch.2 (arXiv:2212.10001).
**Site visited:** arXiv:2212.10001 (confirmed prior pass).
**Finding:** Accurate. Confirmed.
**Expert review needed:** No
**Suggested reference:** Wang, B., et al. Towards Understanding Chain-of-Thought Prompting. ACL 2023. arXiv:2212.10001.
**Notes:** None.

---

## Unverified Assertions

| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| "In spring 2023, a team of computational linguists gave a frontier model a short narrative... [restaurant / 'on the house' dine-and-dash]" | EVIDENCE | POSITIVE | No source, researcher, or publication named; not locatable as a documented study. Reads as an illustrative anecdote presented as a real experiment. Needs a citation or explicit "illustrative" / "author's own test" labeling. |
| "The following scenario was tested under controlled conditions on two commercial LLMs [water freezes at 200°C; Model A / Model B responses]." | EVIDENCE | POSITIVE | Author's own undocumented test; specific model identities, dates, and methodology not given. Honest as a demonstration but not externally verifiable; should be labeled as the author's own informal test, not a controlled study, unless a write-up can be cited. |

---

## AI-Pass Flags

- The chapter's core philosophical claim (syntax ≠ semantics) is argued, not asserted as settled empirical fact, and is explicitly framed as a testable prediction ("Test it") — intellectually honest.
- The agentic "contract review" example is a labeled hypothetical, not a claim about a real case.
- No internal contradictions; the cross-references to Ch.2 (plausibility–truth) and the Fact-Check List external verifier are consistent.

---

## References

(Chapter already contains a References section; all six entries checked and confirmed accurate. No additions required. Recommend adding WinoGrande (Sakaguchi et al., AAAI 2020, arXiv:1907.10641) as the citation for the adversarial-collapse claim if the author wishes to source the "nonsense word" drop directly.)
