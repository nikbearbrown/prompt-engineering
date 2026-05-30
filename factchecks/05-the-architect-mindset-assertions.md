# Assertions Report: 05-the-architect-mindset.md

**Date:** 2026-05-30
**Source file:** chapters/05-the-architect-mindset.md
**Assertions flagged:** 2
**Breakdown:** STAT: 0 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 2 | SPECIALIST: 0 | CURRENT: 0

---

## ⚠️ Critical — Requires Immediate Expert Review

None found. All flagged assertions resolved to CONFIRMED.

---

## Full Findings

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "White, J., ... & Schmidt, D. C. (2023). A Prompt Pattern Catalog to Enhance Prompt Engineering with ChatGPT. arXiv:2302.11382."
**Claim checked:** Reference accuracy (also underpins the layered-prompt framing).
**Site visited:** https://arxiv.org/abs/2302.11382 (confirmed in Ch.2 pass, 2026-05-30).
**Finding:** Correct authors, title, ID. Accurate.
**Expert review needed:** No
**Suggested reference:** White, J., et al. A Prompt Pattern Catalog to Enhance Prompt Engineering with ChatGPT. 2023. arXiv:2302.11382.
**Notes:** None.

### EVIDENCE / SPECIALIST — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Shannon, C. E. (1948). A Mathematical Theory of Communication. Bell System Technical Journal, 27(3), 379–423." (and the entropy formula H(Y|prompt) = −Σ p log p)
**Claim checked:** Source of the entropy definition; citation accuracy.
**Site visited:** Bell System Technical Journal archival record.
**Finding:** Correct — Shannon's paper appeared in BSTJ vol. 27, part 1 at 379–423 (July 1948) and part 2 at 623–656 (October 1948). The chapter cites part 1, which is standard. The Shannon-entropy formula is stated correctly.
**Expert review needed:** No
**Suggested reference:** Shannon, C.E. A Mathematical Theory of Communication. Bell System Technical Journal, 27(3), 379–423, 1948.
**Notes:** Applying Shannon entropy to an LLM's conditional output distribution is the author's pedagogical framing, used qualitatively (not asserting a measured entropy value); appropriate.

---

## Unverified Assertions

| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| The PAST (Problem–Action–Steps–Task) and PLFR (Prompt–Logic–Format–Result) scaffolds | Framework (out of scope) | BASIC | These are the book's own/practitioner mnemonic scaffolds, not claims about external literature. The prior drafting pass (factchecks/_fc-A) already noted they have no single authoritative source and added honest provenance parentheticals. No external verification applicable. |
| "a negative constraint... lowers the entropy... deleting a failure region is a stronger operation than reweighting" | SPECIALIST | POSITIVE | A mechanistic/mathematical argument from the entropy definition, not an empirical finding with a citable number. Internally sound; the chapter itself flags the "honest limit" that constraints are conditioning, not hard guarantees. Prior pass labeled the quantitative version UNVERIFIED; the chapter now presents it as an argument, not a measured result. |

---

## AI-Pass Flags

- The "Wordsville" platform and its Tuesday/Wednesday "trial"/"shoot" failures are a labeled running illustration, not a documented real incident — consistent throughout.
- The entropy argument is internally consistent with Chapter 1's "output as a sample from a conditional distribution." The chapter is careful to state that constraints lower the *rate* of violations, not bound them to zero, and defers the residual to the PLFR Result-layer validator — no overclaim.

---

## References

(Chapter already contains an accurate References section; both entries checked and confirmed. No additions required.)
