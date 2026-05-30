# Assertions Report: 12-automated-prompt-optimization.md

**Date:** 2026-05-30
**Source file:** chapters/12-automated-prompt-optimization.md
**Assertions flagged:** 10
**Breakdown:** STAT: 6 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 10 | SPECIALIST: 0 | CURRENT: 2

---

## ⚠️ Critical — Requires Immediate Expert Review

None found. All flagged assertions resolved to CONFIRMED (a few specific deltas are the source papers' own reported figures, re-verified at the paper level).

---

## Full Findings

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "'Take a deep breath...' reached 80.2% on GSM8K... with PaLM 2-L, versus 71.8% for the standard 'Let's think step by step' and roughly 34% with no special instruction (Yang et al., 2023)." + "beating human-designed ones by up to 8 percent on GSM8K and up to 50 percent on Big-Bench Hard."
**Claim checked:** OPRO headline figures (arXiv:2309.03409).
**Site visited:** arXiv:2309.03409 + corroborating coverage (re-verified live 2026-05-30).
**Finding:** Confirmed — "Take a deep breath and work on this problem step-by-step" = 80.2% GSM8K (PaLM 2-L); "Let's think step by step" = 71.8%; OPRO beats human-designed prompts by up to 8% on GSM8K and up to 50% on Big-Bench Hard. The "~34% no-instruction" baseline matches the paper's empty-instruction starting point.
**Expert review needed:** No
**Suggested reference:** Yang, C., et al. Large Language Models as Optimizers (OPRO). ICLR 2024. arXiv:2309.03409.
**Notes:** OPRO is Google DeepMind, Sept 2023 — matches the chapter's opening framing.

### STAT / EVIDENCE — CONFIRMED (source-paper figures)
**Assertion type:** POSITIVE
**Sentence:** "'Let's work this out in a step by step way...' which beat the human baseline on MultiArith (78.7 to 82.0) and GSM8K (40.7 to 43.0) (Zhou et al., 2023)." + "matched or beat human-annotator instructions on 19 of 24 NLP tasks."
**Claim checked:** APE results (arXiv:2211.01910).
**Site visited:** arXiv:2211.01910 (paper confirmed; deltas are APE's reported figures).
**Finding:** Confirmed at the paper level — APE ("Large Language Models Are Human-Level Prompt Engineers," ICLR 2023) discovered that improved zero-shot-CoT prompt and reports matching/beating human instructions on 19/24 tasks; the MultiArith 78.7→82.0 and GSM8K 40.7→43.0 deltas are APE's own reported numbers (built on Kojima's zero-shot-CoT baselines). Accurate.
**Expert review needed:** No
**Suggested reference:** Zhou, Y., et al. Large Language Models Are Human-Level Prompt Engineers. ICLR 2023. arXiv:2211.01910.
**Notes:** These deltas are setting-specific (APE's evaluation); a different paper (OPRO) re-scores the same prompt differently on PaLM 2-L. The chapter correctly attributes APE's own numbers.

### EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "the Signature, the central abstraction in DSPy (Khattab et al., 2023, ICLR 2024)... raising GPT-3.5 quality from 33% to 82% on GSM8K and from 32% to 46% on HotPotQA... making a Llama2-13b-chat model 'competitive with GPT-3.5 by simply compiling programs.'"
**Claim checked:** DSPy attribution and reported gains (arXiv:2310.03714).
**Site visited:** arXiv:2310.03714.
**Finding:** Confirmed — DSPy (ICLR 2024); the 33%→82% GSM8K and 32%→46% HotPotQA gains and the Llama2-13b-chat "competitive with GPT-3.5" claim are the DSPy paper's own reported results. Accurate.
**Expert review needed:** No
**Suggested reference:** Khattab, O., et al. DSPy. ICLR 2024. arXiv:2310.03714.
**Notes:** Figures are the paper's; consistent with widely-cited DSPy results.

### EVIDENCE — CONFIRMED (notable claim)
**Assertion type:** POSITIVE
**Sentence:** "TextGrad (Yuksekgonul et al., 2024; published in Nature, 2025)... backpropagate textual feedback through an arbitrary compound system."
**Claim checked:** TextGrad and its Nature 2025 publication (arXiv:2406.07496).
**Site visited:** https://www.nature.com/articles/s41586-025-08661-4 (re-verified live 2026-05-30).
**Finding:** Confirmed — TextGrad was published in Nature (2025) as "Optimizing generative AI by backpropagating language model feedback" (Yuksekgonul et al.). The distinctive "published in Nature" claim holds.
**Expert review needed:** No
**Suggested reference:** Yuksekgonul, M., et al. Optimizing generative AI by backpropagating language model feedback (TextGrad). Nature, 2025. (Preprint arXiv:2406.07496.)
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "ProTeGi / APO (Pryzant et al., 2023, EMNLP 2023)... a 'textual gradient'..." and "MIPRO (Opsahl-Ong et al., 2024, EMNLP 2024)... MIPROv2 is the implementation shipped in the DSPy library... beat baseline optimizers on 5 of 7 multi-stage programs with Llama-3-8B, by as much as 13 percent."
**Claim checked:** ProTeGi (arXiv:2305.03495) and MIPRO (arXiv:2406.11695) attributions and figures.
**Site visited:** arXiv:2305.03495, arXiv:2406.11695 (re-verified live 2026-05-30).
**Finding:** Confirmed — ProTeGi/APO "with 'Gradient Descent' and Beam Search," EMNLP 2023; MIPRO (Opsahl-Ong et al., EMNLP 2024) jointly optimizes instructions+demonstrations via Bayesian search, MIPROv2 is DSPy's default. The 5-of-7 / up-to-13% figures are the MIPRO paper's reported results.
**Expert review needed:** No
**Suggested reference:** Pryzant, R., et al. Automatic Prompt Optimization. EMNLP 2023. arXiv:2305.03495; Opsahl-Ong, K., et al. Optimizing Instructions and Demonstrations... EMNLP 2024. arXiv:2406.11695.
**Notes:** The MIPRO/MIPROv2 algorithm-vs-implementation distinction the chapter makes is correct.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Promptbreeder (Fernando et al., 2023)... EvoPrompt (Guo et al., 2023, ICLR 2024)... evolutionary..." + DSP (Khattab et al. 2022, arXiv:2212.14024) + "Revisiting OPRO" (arXiv:2405.10276) small-LLM weak-optimizer finding.
**Claim checked:** Reference accuracy for the evolutionary methods, DSP, and Revisiting OPRO.
**Site visited:** arXiv:2309.16797, arXiv:2309.08532, arXiv:2212.14024, arXiv:2405.10276.
**Finding:** All real with correct IDs and accurate one-line descriptions. Promptbreeder's self-referential mutation, EvoPrompt's LLM+EA framing, DSP as DSPy's predecessor, and "Revisiting OPRO" finding small LLMs are weak optimizers — all accurate.
**Expert review needed:** No
**Suggested reference:** (as listed in chapter)
**Notes:** None.

### STAT / CURRENT — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "A July 2025 preprint, 'Is It Time To Treat Prompts As Code?'... a prompt-evaluation criterion, 46.2% to 64.0%... routing agents, 85.0% to 90.0%, and minor or negligible gains on guardrails and on hallucination detection in code. And tellingly: optimizing a prompt and then swapping to a cheaper model did not transfer the gain."
**Claim checked:** Mixed-results case study (arXiv:2507.03620).
**Site visited:** https://arxiv.org/abs/2507.03620 (re-verified live 2026-05-30).
**Finding:** Confirmed — DSPy across five use cases (guardrails, hallucination detection in code, code generation, routing agents, prompt evaluation); prompt-evaluation rose 46.2%→64.0%; mixed/minor gains elsewhere. The honest "gains in some cases, marginal-or-none in others" framing matches the paper.
**Expert review needed:** No
**Suggested reference:** Is It Time To Treat Prompts As Code? A Multi-Use Case Study for Prompt Optimization Using DSPy. 2025. arXiv:2507.03620.
**Notes:** Recent preprint; the routing 85→90 and "cheaper model didn't transfer" are from the paper's per-case results.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Grace Hopper's 1952 argument for the compiler..." and "the expected-improvement framework formalized by Jonas Mockus in the 1970s."
**Claim checked:** Historical attributions.
**Site visited:** Standard history-of-computing / Bayesian-optimization records.
**Finding:** Correct — Grace Hopper's A-0 compiler dates to 1952; Jonas Mockus formalized the expected-improvement / Bayesian global optimization framework in the 1970s. Both accurate analogies.
**Expert review needed:** No
**Suggested reference:** Hopper, G. (A-0 compiler, 1952); Mockus, J. (Bayesian methods for global optimization, 1970s).
**Notes:** None.

---

## Unverified Assertions

| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| The "80 Days to Stay" SEC going-concern extractor worked example and its 60/40/20 split | EVIDENCE | BASIC | Labeled worked example (teaching device), not a reported experiment. |
| "how much of an optimization win is the Bayesian search, and how much is simply the discipline of being forced to write the metric. No clean ablation isolates the two." | EVIDENCE | BASIC (hedged) | Explicitly framed as an open question, not a claim; no verification needed. |

---

## AI-Pass Flags

- Exceptionally citation-dense and, where checked, uniformly accurate; the distinctive "TextGrad in Nature" and "OPRO 80.2/71.8" claims both hold.
- The chapter is unusually honest about mixed/negative results (the July 2025 case study, re-optimization debt, the attribution open question) — strong intellectual calibration.
- MIPRO vs MIPROv2 (algorithm vs shipped implementation) handled correctly.

---

## References

(Chapter contains a complete, accurate References section; all eleven entries checked and confirmed. No corrections required.)
