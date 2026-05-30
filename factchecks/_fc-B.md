# Fact-check B — Prompt Engineering Ch. 10 & 11

| chapter | claim | verdict | resolution/source |
|---|---|---|---|
| 10 | (sourcing note) figures need PDF pass | RESOLVED | Note rewritten — all figures now verified; dropped flag. |
| 10 | TL;DR: 3-needle ~95%→~40% (multilingual NIAH) + NINJA 23.7%→58.8% | CONFIRMED | Both verified (see rows below); flag dropped, ~95% tightened to ~96%. |
| 10 | Murdock 1962 free-recall curve = canonical serial-position plot | CONFIRMED | Murdock, B.B. (1962), *J. Verbal Learning & Verbal Behavior* 64:482–488. Added journal cite. (Chapter wrongly implied JEP elsewhere is not present; link is to Wikipedia.) |
| 10 | Found-in-the-Middle: inference-time calibration recovers up to 15 pp RAG accuracy | CONFIRMED | Hsieh et al., arXiv:2406.16008, ACL 2024 Findings — "outperforming existing methods by up to 15 percentage points." Flag dropped. |
| 10 | Multilingual NIAH: ~95% single-needle → ~40% three-needle (English) | CONFIRMED (tightened) | arXiv:2409.18006 abstract: ~96% English single → 40% English three-needle (0% Somali). Dataset = mLongRR. Flag dropped; figure corrected to ~96%. |
| 10 | Silent contradiction resolution (position-driven) | UNVERIFIED | No primary citation isolating position-driven contradiction resolution. Flag replaced with honest "UNVERIFIED — reasoned prediction, not a documented finding." |
| 10 | NINJA: 23.7%→58.8% Llama-3.1-8B-Instruct on HarmBench | CONFIRMED | arXiv:2511.04707 — ASR 23.7%→58.8% Llama-3.1-8B (42.5% Qwen2.5-7B, 29% Gemini Flash). Flag dropped. |
| 11 | (sourcing note) Tam arXiv ID + LongFuncEval table need confirm | RESOLVED | Both confirmed; note rewritten, flag dropped. |
| 11 | TL;DR: tool-count degradation 7.6%–85.6% (LongFuncEval) | CONFIRMED (corrected) | arXiv:2505.10570 abstract states 7%–85% (tool count) and 7%–91% (response length). "7.6%–85.6%" not supported by abstract; corrected to 7%–85%. Flag dropped. |
| 11 | TL;DR: format restriction costs reasoning (Tam et al.) | CONFIRMED | Tam et al., arXiv:2408.02442, EMNLP 2024 Industry Track (2024.emnlp-industry.91). Flag dropped. |
| 11 | §11.3 LongFuncEval 7.6%–85.6% body figure | CONFIRMED (corrected) | Same as above; corrected to 7%–85% with the 7%–91% response-length band noted. Flag dropped. |
| 11 | Tam et al. arXiv ID (`[verify arXiv ID]` x2) | CONFIRMED | arXiv:2408.02442 confirmed; full author list added to References. Flags dropped. |
| 11 | LongFuncEval ref `[verify table numbers]` | RESOLVED | Authors + abstract band added; flag dropped. |

**Tally:** 12 verdicts — 9 CONFIRMED (3 of them with figure corrections), 2 RESOLVED (meta notes), 1 UNVERIFIED (silent contradiction resolution, honestly attributed in-text).

**Remaining UNVERIFIED:** Ch.10 silent-contradiction-resolution claim — kept as an explicitly-labeled reasoned prediction. LongFuncEval precise decimals "7.6%/85.6%" could not be confirmed from the abstract (table not fetchable); corrected to the abstract-verified 7%–85% band rather than left UNVERIFIED.
