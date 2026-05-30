# Assertions Report: 00-foundations-sampling-and-logits.md

**Date:** 2026-05-30
**Source file:** chapters/00-foundations-sampling-and-logits.md
**Assertions flagged:** 7
**Breakdown:** STAT: 1 | GUIDELINE: 1 | APPROVAL: 0 | EVIDENCE: 4 | SPECIALIST: 1 | CURRENT: (1, overlaps GUIDELINE)

---

## ⚠️ Critical — Requires Immediate Expert Review

None found. All flagged assertions resolved to CONFIRMED; no OUTDATED, CONTRADICTED, or COMBINATION (emphatic+positive) assertions.

---

## Full Findings

### STAT — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Modern vocabularies run to roughly 100,000 entries (GPT-4's tokenizer sits near there; Llama 3 uses 128,256; GPT-4o's tokenizer reaches about 200,000)..."
**Claim checked:** Tokenizer vocabulary sizes for GPT-4 (~100k), Llama 3 (128,256), GPT-4o (~200k).
**Site visited:** OpenAI tiktoken repo (cl100k_base / o200k_base) and Meta Llama 3 model card; corroborated by prior-pass live check (factchecks/_fc-A).
**Finding:** GPT-4 uses cl100k_base (100,277 tokens); Llama 3 uses a 128,256-token vocabulary; GPT-4o uses o200k_base (~200,019 tokens). The stated figures are accurate. This figure was corrected during the prior drafting pass from an earlier "~50k–130k."
**Expert review needed:** No
**Suggested reference:** OpenAI, tiktoken (cl100k_base, o200k_base); Meta, Llama 3 model card, 2024.
**Notes:** "Roughly/about" framing is appropriate; exact counts vary by special-token additions.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Top-p sampling, also called nucleus sampling, was introduced by Holtzman et al. in their 2020 paper 'The Curious Case of Neural Text Degeneration' (arXiv:1904.09751)."
**Claim checked:** Attribution of nucleus (top-p) sampling to Holtzman et al., arXiv:1904.09751, ICLR 2020.
**Site visited:** https://arxiv.org/abs/1904.09751 (corroborated by prior-pass live check).
**Finding:** Paper exists with that exact title and arXiv ID; introduces nucleus sampling; presented at ICLR 2020 (preprint posted 2019). Attribution accurate.
**Expert review needed:** No
**Suggested reference:** Holtzman, A., Buys, J., Du, L., Forbes, M., & Choi, Y. The Curious Case of Neural Text Degeneration. ICLR 2020. arXiv:1904.09751.
**Notes:** arXiv year (2019) vs publication year (2020) — the chapter's "2020 paper" tracks the ICLR publication; fine.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "The name is borrowed from statistical physics: the Boltzmann distribution... and $T$ is the system's temperature."
**Claim checked:** Statistical-physics origin of the temperature parameter (Ackley, Hinton & Sejnowski 1985).
**Site visited:** Cognitive Science 9(1):147–169 (prior-pass confirmation).
**Finding:** "A Learning Algorithm for Boltzmann Machines," Cognitive Science 9(1), 147–169 (1985) — the cited origin is accurate; softmax/temperature does have the Boltzmann form.
**Expert review needed:** No
**Suggested reference:** Ackley, D.H., Hinton, G.E., & Sejnowski, T.J. A Learning Algorithm for Boltzmann Machines. Cognitive Science 9(1), 147–169, 1985.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Fan, A., Lewis, M., & Dauphin, Y. (2018). Hierarchical Neural Story Generation... arXiv:1805.04833 — early top-k sampling."
**Claim checked:** Top-k sampling attribution, arXiv:1805.04833, ACL 2018.
**Site visited:** https://arxiv.org/abs/1805.04833 (prior-pass confirmation).
**Finding:** Paper exists with that ID/title, ACL 2018; popularized top-k sampling for generation. Accurate.
**Expert review needed:** No
**Suggested reference:** Fan, A., Lewis, M., & Dauphin, Y. Hierarchical Neural Story Generation. ACL 2018. arXiv:1805.04833.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Vaswani, A., et al. (2017). Attention Is All You Need... arXiv:1706.03762."
**Claim checked:** Transformer attribution, arXiv:1706.03762, NeurIPS 2017.
**Site visited:** https://arxiv.org/abs/1706.03762 (prior-pass confirmation).
**Finding:** Correct title, ID, venue. Accurate.
**Expert review needed:** No
**Suggested reference:** Vaswani, A., et al. Attention Is All You Need. NeurIPS 2017. arXiv:1706.03762.
**Notes:** None.

### GUIDELINE / CURRENT — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Google's developer guidance for Gemini 3 explicitly recommends keeping temperature at the default 1.0 on complex reasoning tasks because lowering it can induce exactly this degradation."
**Claim checked:** That current Gemini 3 docs recommend temperature 1.0 and warn lowering it causes looping/degraded reasoning.
**Site visited:** https://ai.google.dev/gemini-api/docs/gemini-3 (re-verified live 2026-05-30).
**Finding:** The Gemini 3 Developer Guide states Google "strongly recommends keeping the temperature parameter at its default value of 1.0," and warns that setting it below 1.0 "may lead to unexpected behavior, such as looping or degraded performance, particularly in complex mathematical or reasoning tasks." Claim is accurate and current.
**Expert review needed:** No
**Suggested reference:** Google. Gemini 3 Developer Guide (generateContent API). https://ai.google.dev/gemini-api/docs/gemini-3
**Notes:** This is a CURRENT/rapidly-evolving guidance claim tied to a specific model version; re-verify at each printing. Still accurate as of 2026-05-30.

### SPECIALIST — CONFIRMED (computational)
**Assertion type:** BASIC
**Sentence:** The softmax / temperature / top-k / top-p worked examples (logits (2.0,1.0,0.1) → p≈(0.659,0.242,0.099); T=0.5 → (0.864,0.117,0.019); T=2 → (0.502,0.304,0.194); top-k and top-p nucleus examples).
**Claim checked:** Arithmetic correctness of every worked decoding example.
**Site visited:** Direct computation (no web source needed).
**Finding:** Recomputed all examples — softmax at T=1, 0.5, 2; top-k k=3 renormalization (0.471,0.294,0.235); top-p p=0.80 nucleus selection on peaked, flat, and standard distributions. Every figure is correct to the digits shown.
**Expert review needed:** No
**Suggested reference:** Goodfellow, Bengio & Courville. Deep Learning, MIT Press 2016, Ch. 6 §6.2.2.3 (softmax).
**Notes:** Math is internally consistent and correct.

---

## Unverified Assertions

| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| "On some models it triggers pathological looping..." | SPECIALIST | POSITIVE | True in general and consistent with the Gemini 3 warning, but "some models" is non-specific; treat as an accurate practitioner-level generalization rather than a single-source claim. |

---

## AI-Pass Flags

- All worked arithmetic verified internally consistent (see SPECIALIST finding).
- The chapter is unusually well-sourced (complete References section already present) and self-aware about uncertainty ("Still puzzling," "What would change my mind"). No internal contradictions found.

---

## References

(Chapter already contains a complete, accurate References section. No additions required — all six listed references were checked and confirmed.)
