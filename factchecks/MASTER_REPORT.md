# Master Fact-Check Report

**Book folder:** prompt-engineering (The AI+1 series, Humanitarians AI)
**Date:** 2026-05-30
**Total chapters processed:** 19 content files (frontmatter, introduction, Ch.0 Foundations, Ch.1–15, back matter)
**Total files read:** 19 source files → 19 per-chapter assertion reports written to `factchecks/`
**Total assertions flagged:** ~109 (sentences in the six web-verifiable categories)

> Note: the prior drafting-pass report is preserved as `MASTER_REPORT_v1_2026-05-29.md` (with `_fc-A/B/C.md`). This file supersedes it for the freshly-rewritten chapters.

**Breakdown by content category (approx.):** STAT: 41 | GUIDELINE: 2 | APPROVAL: 0 | EVIDENCE: 95 | SPECIALIST: 6 | CURRENT: 21
*(Categories overlap — most flagged sentences are EVIDENCE attributions that are also STAT and/or CURRENT.)*

**Breakdown by assertion type:** BASIC: ~38 | EMPHATIC: 0 | POSITIVE: ~68 | I-LANGUAGE: ~3 | COMBINATION: 0

**Field-source adaptation:** This is an LLM/prompt-engineering book, so the biomedical authorities in the source workflow were replaced with the appropriate ones — arXiv, ACL Anthology, Google Scholar, and Nature for EVIDENCE/SPECIALIST; provider documentation (docs.anthropic.com, ai.google.dev, OpenAI) for GUIDELINE/capability claims; the cited papers and provider docs for STAT; recent arXiv + provider docs + security advisories (OWASP, CVE/THN) for CURRENT.

---

## Overall Critical Findings

Sorted by priority. **One CONTRADICTED finding (now resolved); zero OUTDATED; zero COMBINATION.** This book is exceptionally well-sourced — many specific figures match their papers exactly, and several chapters do their own "read the anchor numbers precisely" corrections.

### CONTRADICTED (attribution) — RESOLVED 2026-05-30

**File:** 07-structuring-and-governing-output.md
**Assertion type:** BASIC
**Category:** EVIDENCE
**Verdict:** CONTRADICTED → **RESOLVED**
**Sentence (original):** "White, J., ... (2023). A Prompt Pattern Catalog... *(Source for the Template, Recipe, Outline Expansion, Menu Actions, and Semantic Filter patterns.)*"
**Finding:** Full-text search of the cited paper (arXiv:2302.11382 / Vanderbilt PDF) confirmed **Template** and **Recipe** as named patterns but found **no named "Outline Expansion," "Menu Actions," or "Semantic Filter" pattern** — those words appear only as ordinary prose/examples.
**Resolution:** Fixed in the source. White et al. is now credited only for Template and Recipe; the other three are reframed in both the body and the References as **common practitioner patterns / rules of thumb (heuristics), not formal results from any single paper.** A framing note was added at the patterns' introduction and the inline flag removed. No remaining CONTRADICTED findings in the book.

### UNVERIFIED (flagged inline for the author)

**File:** 06-persona-and-audience-patterns.md — **Category:** STAT/CURRENT — **Verdict:** UNVERIFIED
**Sentence:** "self-consistency degrades by more than 30% after eight to twelve dialogue turns."
**Finding:** The cited paper (arXiv:2511.00222) is real and on-topic (persona drift), but its abstract does not state this exact figure (it reports a 55% *improvement* from RL). Verify the "30% / 8–12 turns" number against the paper body.

**File:** 03-the-limits-of-syntax.md — **Category:** EVIDENCE — **Verdict:** UNVERIFIED (×2)
**Sentences:** the "spring 2023 computational linguists / restaurant 'on the house'" study, and the "water freezes at 200°C, tested on two commercial LLMs" demonstration.
**Finding:** Both are the author's own undocumented demonstrations presented as experiments; no source/researcher named. Label them as illustrative / "author's own informal test," or cite a write-up.

### Calibration note (not an error)

**File:** 13-beyond-prompting-the-fine-tuning-stack.md — GEPA is cited as beating GRPO by "≈6 points on average," while the paper's abstract headlines "10% on average / up to 20%" (the 6% is a per-model/per-task figure). Reconcile which aggregation the chapter intends; the 35×-fewer-rollouts and per-benchmark deltas are otherwise sound.

---

## Chapter-by-Chapter Summary

| Chapter File | Assertions Flagged | Critical | Outdated | Contradicted | Unverified | Confirmed |
|---|---|---|---|---|---|---|
| 00-frontmatter.md | 0 | 0 | 0 | 0 | 0 | 0 |
| 00-introduction.md | 0 | 0 | 0 | 0 | 0 | 0 |
| 00-foundations-sampling-and-logits.md | 7 | 0 | 0 | 0 | 0 | 7 |
| 01-the-stochastic-machine.md | 6 | 0 | 0 | 0 | 0 | 6 |
| 02-hallucination-and-the-plausibility-truth-gap.md | 6 | 0 | 0 | 0 | 0 | 6 |
| 03-the-limits-of-syntax.md | 8 | 0 | 0 | 0 | 2 | 6 |
| 04-sycophancy-and-computational-skepticism.md | 3 | 0 | 0 | 0 | 0 | 3 |
| 05-the-architect-mindset.md | 2 | 0 | 0 | 0 | 0 | 2 |
| 06-persona-and-audience-patterns.md | 7 | 0 | 0 | 0 | 1 | 6 |
| 07-structuring-and-governing-output.md | 3 | 0 (resolved) | 0 | 0 (resolved) | 0 | 3 |
| 08-reasoning-and-range-patterns.md | 7 | 0 | 0 | 0 | 0 | 7 |
| 09-prompt-brittleness-and-evaluation.md | 8 | 0 | 0 | 0 | 0 | 8 |
| 10-long-context-prompting.md | 8 | 0 | 0 | 0 | 0 | 8 |
| 11-agentic-and-multi-turn-systems.md | 9 | 0 | 0 | 0 | 0 | 9 |
| 12-automated-prompt-optimization.md | 10 | 0 | 0 | 0 | 0 | 10 |
| 13-beyond-prompting-the-fine-tuning-stack.md | 8 | 0 | 0 | 0 | 0 | 8 |
| 14-prompt-engineering-for-cli-coding-agents.md | 8 | 0 | 0 | 0 | 0 | 8 |
| 15-production-ethics-and-whats-next.md | 9 | 0 | 0 | 0 | 0 | 9 |
| 99-back-matter.md | 0 | 0 | 0 | 0 | 0 | 0 |
| **TOTAL** | **~109** | **0 (resolved)** | **0** | **0 (resolved)** | **3** | **~105** |

---

## Recommended Next Steps

The book is in excellent factual shape — unusually so. Across roughly 100 verifiable claims spanning the LLM/prompt-engineering literature (Vaswani, Holtzman, Kojima, Wei, Wang & Zhou, Min, Sclar, Mizrahi, Liu "Lost in the Middle," Anil many-shot, Yao ReAct, Laban multi-turn, OPRO/APE/DSPy/MIPRO/GEPA, LoRA/QLoRA/GRPO, Huang self-correction, the Wharton Prompting Science series, and recent security disclosures), the overwhelming majority of attributions, arXiv IDs, and even specific benchmark figures verified **exactly** against primary sources — including correctly-handled recent and future-dated 2025–2026 papers and the chapters' own corrections of common misquotations.

**The one substantive issue — now resolved.** Chapter 7 had credited three of its five "patterns" (Outline Expansion, Menu Actions, Semantic Filter) to White et al. (2023), where they are not named patterns. This has been fixed: White et al. is now credited only for Template and Recipe, and the other three are reframed in the body and References as common practitioner patterns — rules of thumb / heuristics, not formal results from any single paper. No CONTRADICTED findings remain.

**Three lower-priority items** for the author: (1) verify the Chapter 6 "30% / 8–12 turns" persona-drift figure against the paper body; (2) label the two Chapter 3 in-text "experiments" as the author's own demonstrations or cite write-ups; (3) reconcile the Chapter 13 GEPA "average" figure with the paper's abstract. Minor housekeeping: harmonize the Prompting Science Report 2 identifier (SSRN vs arXiv) across chapters, and complete the template placeholders in the frontmatter, the introduction (its chapter-list section also mis-maps several chapter titles/numbers — see 00-introduction report), and the back matter.

**Categories that produced the most flags:** EVIDENCE (named-paper attributions) and STAT (benchmark figures) — exactly where this book invests most, and exactly where it proved most reliable. **No GUIDELINE or APPROVAL failures, no OUTDATED claims, and no emphatic-and-unhedged (COMBINATION) overclaims** were found; where the field is genuinely unsettled (mechanisms, multimodal prompting, reasoning-tuned-model behavior), the chapters say so explicitly. Overall reliability: **high.**
