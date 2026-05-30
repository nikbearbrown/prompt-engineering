# Assertions Report: 07-structuring-and-governing-output.md

**Date:** 2026-05-30
**Source file:** chapters/07-structuring-and-governing-output.md
**Assertions flagged:** 3
**Breakdown:** STAT: 0 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 3 | SPECIALIST: 0 | CURRENT: 0

---

## ⚠️ Critical — Requires Immediate Expert Review

**RESOLVED (2026-05-30).** The original CONTRADICTED attribution has been fixed in the source. White et al. (2023) is now credited only for **Template** and **Recipe**; **Outline Expansion, Menu Actions, and the Semantic Filter** are reframed in both the body and the References as **common practitioner patterns / rules of thumb (heuristics), not formal results from any single paper.** A framing note was added near the patterns' introduction and the inline fact-check flag was removed. The finding below is retained for the record.

---

**[Resolved] EVIDENCE — CONTRADICTED (attribution).** The References line originally stated White et al. (2023) is the "Source for the Template, Recipe, Outline Expansion, Menu Actions, and Semantic Filter patterns." Verification against the actual paper (arXiv:2302.11382 / Vanderbilt PDF) showed only **Template** and **Recipe** are named patterns there. **"Outline Expansion," "Menu Actions," and "Semantic Filter" do not appear as named patterns** in the cited paper — the words "outline," "menu," and "filter" occur only as ordinary prose/examples (e.g., "Table I outlines," "provide a menu," filtering as a *consequence* of the Template pattern). Now corrected per the resolution above.

---

## Full Findings

### EVIDENCE — CONTRADICTED (attribution)
**Assertion type:** BASIC
**Sentence:** "White, J., ... (2023). A Prompt Pattern Catalog... (Source for the Template, Recipe, Outline Expansion, Menu Actions, and Semantic Filter patterns.)" — and the body's framing of Outline Expansion, Menu Actions, and Semantic Filter as established patterns.
**Claim checked:** Whether Outline Expansion, Menu Actions, and Semantic Filter are named patterns in White et al. (2023).
**Site visited:** https://arxiv.org/abs/2302.11382 and https://www.dre.vanderbilt.edu/~schmidt/PDF/prompt-patterns.pdf (full text fetched and searched, 2026-05-30).
**Finding:** The paper's named patterns include Template (Output Template), Recipe, Output Automater, Persona, Visualization Generator, Fact Check List, Cognitive Verifier, Question Refinement, etc. A full-text search found **no named "Outline Expansion," "Menu Actions," or "Semantic Filter" pattern.** "outline" appears once as a verb ("Table I outlines…"); "menu" appears once inside an example; "filter/filtering" appears only as a *consequence* of the Template pattern, not as a standalone "Semantic Filter Pattern." So Template and Recipe are correctly attributed; the other three are not White et al. (2023) patterns under those names.
**Expert review needed:** Yes.
**Suggested reference:** White, J., et al. A Prompt Pattern Catalog to Enhance Prompt Engineering with ChatGPT. 2023. arXiv:2302.11382 — *correctly cite only for Template and Recipe.* For Outline Expansion / Menu Actions / Semantic Filter, either supply the specific source where they are named, or relabel them as this book's own (catalog-inspired) patterns.
**Notes:** The *ideas* are sound and useful; the issue is purely the attribution that these three are named White et al. patterns. A second-edition White paper or follow-on (e.g., the PLoP/SIGAda catalog expansions) could conceivably name some of them — if so, cite that work specifically; the version the chapter cites does not.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "The Template Pattern supplies a fixed output structure..." and "The Recipe Pattern asks for a complete, ordered sequence of steps... White et al.'s canonical framing: 'I am trying to achieve X...'"
**Claim checked:** Template and Recipe are White et al. (2023) patterns, framed accurately.
**Site visited:** Vanderbilt PDF (full text, 2026-05-30).
**Finding:** Confirmed — both are named patterns; the Recipe "I am trying to achieve X… provide a complete sequence of steps… fill in missing and identify unnecessary steps" framing matches the paper. Accurate.
**Expert review needed:** No
**Suggested reference:** White, J., et al. arXiv:2302.11382.
**Notes:** None.

### EVIDENCE / SPECIALIST — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Shannon, C. E. (1948)... (Source of the entropy definition underlying the 'structure reduces output entropy' claim.)" plus the autoregressive chain-rule mechanism.
**Claim checked:** Entropy/citation accuracy; chain-rule conditioning argument.
**Site visited:** BSTJ record (confirmed Ch.5); internal consistency with Ch.0/Ch.1.
**Finding:** Shannon citation correct; the "committing structural tokens early narrows later conditional distributions" argument is a correct restatement of the autoregressive chain rule from Ch.0/Ch.1. Accurate.
**Expert review needed:** No
**Suggested reference:** Shannon, C.E. A Mathematical Theory of Communication. BSTJ 27(3), 379–423, 1948.
**Notes:** None.

---

## Unverified Assertions

| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| "committing to structural tokens early narrows the conditional distribution over all later tokens." | SPECIALIST | POSITIVE | A mechanistic argument from the chain rule (Ch.0/Ch.1), not an empirical citation; internally sound. |

---

## AI-Pass Flags

- **Attribution over-reach (see Critical).** Only Template and Recipe are White et al. patterns; relabel or re-source Outline Expansion, Menu Actions, Semantic Filter.
- The "late-2024 logistics firm" opening is a labeled illustrative scenario.
- The Semantic Filter → context-isolation argument is internally consistent with Ch.4's dissenting sub-agent and "calibration drift"; cross-references are coherent.

---

## References

(Chapter already contains a References section. Template/Recipe and Shannon are correctly cited. Recommend correcting the parenthetical so White et al. is credited only for Template and Recipe, with a separate/accurate source — or a "this book's extension" label — for Outline Expansion, Menu Actions, and Semantic Filter.)
