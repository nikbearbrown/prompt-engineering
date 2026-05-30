# Assertions Report: 10-long-context-prompting.md

**Date:** 2026-05-30
**Source file:** chapters/10-long-context-prompting.md
**Assertions flagged:** 8
**Breakdown:** STAT: 4 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 8 | SPECIALIST: 0 | CURRENT: 1

---

## ⚠️ Critical — Requires Immediate Expert Review

None found. All flagged assertions resolved to CONFIRMED.

---

## Full Findings

### EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Liu et al. (2024), published in TACL... Accuracy is highest when the relevant information sits at the beginning or the end... a U-shaped curve. The effect holds even for models explicitly built for long contexts."
**Claim checked:** "Lost in the Middle" U-curve (TACL 12:157–173, arXiv:2307.03172).
**Site visited:** arXiv:2307.03172 / TACL record.
**Finding:** Correct — Liu et al., "Lost in the Middle: How Language Models Use Long Contexts," TACL 2024; performance highest when relevant info is at start/end, degrades in the middle, persists in long-context models. Accurate.
**Expert review needed:** No
**Suggested reference:** Liu, N.F., et al. Lost in the Middle. TACL 12 (2024), 157–173. arXiv:2307.03172.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "RULER (Hsieh et al. 2024)... most models hold consistent accuracy only well below their advertised token limit. The effective context is much smaller than the nominal context."
**Claim checked:** RULER effective-vs-nominal context (arXiv:2404.06654).
**Site visited:** arXiv:2404.06654.
**Finding:** Correct — RULER extends NIAH with multi-key/variable-tracking/aggregation tasks and shows effective context lengths fall well short of claimed limits. Accurate.
**Expert review needed:** No
**Suggested reference:** Hsieh, C.-P., et al. RULER: What's the Real Context Size of Your Long-Context Language Models? 2024. arXiv:2404.06654.
**Notes:** None.

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "'Found in the Middle'... estimate the position-only component of the attention bias and subtract it, recovering up to 15 percentage points of RAG accuracy."
**Claim checked:** 15-pp calibration recovery (arXiv:2406.16008, ACL 2024 Findings).
**Site visited:** arXiv:2406.16008 (confirmed prior pass, factchecks/_fc-B).
**Finding:** Confirmed — Hsieh et al. "Found in the Middle," up to 15 percentage-point RAG improvement via positional-attention calibration. Accurate; also supports the U-shaped attention claim.
**Expert review needed:** No
**Suggested reference:** Hsieh, C.-Y., et al. Found in the Middle. ACL 2024 Findings. arXiv:2406.16008.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Murdock's 1962 free-recall curve is the canonical human plot." (serial-position / primacy / recency)
**Claim checked:** Serial-position effect attribution.
**Site visited:** Confirmed prior pass (factchecks/_fc-B): Murdock, B.B. (1962), J. Verbal Learning & Verbal Behavior.
**Finding:** Correct. Accurate as the canonical free-recall serial-position reference.
**Expert review needed:** No
**Suggested reference:** Murdock, B.B. The serial position effect of free recall. J. Verbal Learning & Verbal Behavior, 1962.
**Notes:** Prior pass flagged a journal-detail nuance; the attribution itself is sound.

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "the best models hit roughly 96 percent in English with a single target sentence, but three target sentences in English drops to roughly 40 percent... approximately 40 percent for three needles, not the rounder, more optimistic 60 percent that circulates..."
**Claim checked:** Multilingual NIAH 96% single → ~40% three-needle English (arXiv:2409.18006, mLongRR).
**Site visited:** arXiv:2409.18006 (confirmed prior pass).
**Finding:** Confirmed — ~96% English single-needle, ~40% English three-needle (0% Somali). The chapter correctly uses ~40% and explicitly corrects the over-optimistic 60% practitioner figure.
**Expert review needed:** No
**Suggested reference:** Multilingual Needle in a Haystack / mLongRR. 2024. arXiv:2409.18006.
**Notes:** Chapter's own caveat ("calibration point, not a law") is appropriate.

### EVIDENCE / STAT — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Anil et al. (2024), Anthropic, showed that stuffing hundreds of faux dialogue turns... overrides alignment. Attack strength scales... near-zero at 5 shots and reliable around 256, following a power law..."
**Claim checked:** Many-shot jailbreaking: 5 shots ≈ no effect, 256 shots reliable, power-law scaling, cross-model.
**Site visited:** https://www.anthropic.com/research/many-shot-jailbreaking + NeurIPS 2024 proceedings (re-verified live 2026-05-30).
**Finding:** Confirmed — the attack "doesn't work at all with 5 shots" and "works consistently with 256 shots," following a power law; demonstrated across widely used SOTA models (Llama-2 70B context-limited). Chapter's specific model list (GPT-3.5/4, Claude 2.0, Llama 2 70B, Mistral 7B) is consistent with the paper's evaluation set.
**Expert review needed:** No
**Suggested reference:** Anil, C., et al. Many-shot Jailbreaking. NeurIPS 2024. https://www.anthropic.com/research/many-shot-jailbreaking
**Notes:** None.

### STAT / CURRENT — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "NINJA... On HarmBench, attack success rose from a 23.7% baseline to 58.8% for Llama-3.1-8B-Instruct — also... 42.5% for Qwen2.5-7B-Instruct, and roughly 23% to 29% for Gemini Flash."
**Claim checked:** NINJA HarmBench figures (arXiv:2511.04707).
**Site visited:** arXiv:2511.04707 (confirmed prior pass).
**Finding:** Confirmed — ASR 23.7%→58.8% (Llama-3.1-8B), 42.5% (Qwen2.5-7B), ~29% (Gemini Flash); position-dependent (goal-at-front maximizes). The chapter's careful phrasing ("up to 58.8% on Llama-3.1-8B, from a 23.7% baseline") is exactly right.
**Expert review needed:** No
**Suggested reference:** NINJA — Jailbreaking in the Haystack. 2025. arXiv:2511.04707.
**Notes:** Recent preprint; re-verify at printing.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Greg Kamradt's needle-in-a-haystack pressure tests..." and "Databricks (2024). Long Context RAG Performance... arXiv:2411.03538."
**Claim checked:** Supporting references exist and are correctly attributed.
**Site visited:** github.com/gkamradt/LLMTest_NeedleInAHaystack; arXiv:2411.03538.
**Finding:** Both real and correctly attributed; used as supporting/practitioner evidence. Accurate.
**Expert review needed:** No
**Suggested reference:** Kamradt, G. Needle In A Haystack. 2023. (GitHub); Databricks. Long Context RAG Performance of LLMs. 2024. arXiv:2411.03538.
**Notes:** None.

---

## Unverified Assertions

| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| The "80 Days to Stay" SEC bundle / page-150 exonerating clause | EVIDENCE | POSITIVE | Labeled illustrative scenario; consistent with the documented lost-in-the-middle effect. |
| "attention-sink phenomenon — early tokens... receive large attention weight somewhat regardless of relevance" | SPECIALIST | BASIC | Well-established (attention-sink literature, e.g., StreamingLLM); stated as mechanism, supported by the cited Found-in-the-Middle U-shaped-attention result. |

---

## AI-Pass Flags

- The chapter is unusually careful to phrase attack-success figures precisely and to correct an over-optimistic practitioner number (60% → ~40%); this matches the prior drafting pass's corrections.
- Cross-references to Ch.2 (hallucination ≠ this), Ch.4 (context isolation), and Ch.9 (benchmark hides failure) are consistent.

---

## References

(Chapter contains a complete, accurate References section; all nine entries checked and confirmed. No corrections required.)
