# Master Fact-Check Report — Prompt Engineering

**Date:** 2026-05-29  ·  **Author:** Nik Bear Brown
**Scope:** all `[verify]` flags placed during drafting, resolved against the pantry research files and live web sources.

Verdicts: CONFIRMED (source verified) · CORRECTED (figure/attribution fixed inline) · PREPRINT (real but not yet peer-reviewed; labeled in text) · UNVERIFIABLE (no primary source; attributed honestly, never asserted as fact).

---

## Batch: A

# Fact-check verdict — PE batch A (Ch00, 02, 05, 06)

| chapter | claim (short) | verdict | resolution / source |
|---|---|---|---|
| 00 | Modern vocab sizes ~50k–130k | OUTDATED | Corrected to ~100k (GPT-4 cl100k; Llama 3 = 128,256) up to ~200k (GPT-4o o200k). |
| 00 | Gemini 3 guidance: keep temp 1.0, low temp loops; "Gemini 2.5 incidents early 2026" | CONFIRMED (guidance) / UNVERIFIED (incidents) | Guidance confirmed (ai.google.dev/gemini-api/docs/gemini-3). Unverifiable "2.5 production incidents/dates" claim removed; kept the documented guidance. |
| 00 | Holtzman et al. 2020 introduced nucleus/top-p, arXiv:1904.09751 | CONFIRMED | arXiv:1904.09751, ICLR 2020. Inline + reference fixed. |
| 00 | Vaswani et al. 2017 transformer, arXiv:1706.03762 | CONFIRMED | arXiv:1706.03762, NeurIPS 2017. |
| 00 | Goodfellow et al. 2016 softmax ref, Ch. 6 | CONFIRMED | *Deep Learning*, Ch. 6 "Deep Feedforward Networks," §6.2.2.3. |
| 00 | Ackley/Hinton/Sejnowski 1985 Boltzmann temperature origin | CONFIRMED | *Cognitive Science* 9(1), 147–169. Page range added. |
| 00 | Fan et al. 2018 top-k, arXiv:1805.04833 | CONFIRMED | arXiv:1805.04833, ACL 2018. |
| 00 | Gemini API generation-config ref URL | CONFIRMED | https://ai.google.dev/gemini-api/docs/gemini-3 (Gemini 3 Developer Guide). |
| 02 | meta-note convention token | n/a | Bare `[verify]` token removed from absorption note (flags now resolved). |
| 02 | CoT 80–90% figure from Wang et al. 2023 ACL, arXiv:2212.10001 | CONFIRMED | arXiv:2212.10001; already in chapter References. Inline marker deleted. |
| 02 | Meincke/Mollick "Prompting Science Report 2," arXiv:2506.07142, 2025 preprint | CONFIRMED | arXiv:2506.07142, Wharton GAIL 2025, not peer-reviewed. Softened inline; in References. |
| 02 | Weak uncertainty-surfacing effect | UNVERIFIED | Kept claim; softened to "suggestive but underpowered; not independently confirmed." |
| 05 | meta-note convention token | n/a | Bare `[verify]` token rephrased in provenance note. |
| 05 | PAST acronym provenance | UNVERIFIED | Practitioner mnemonic, no single authoritative source; honest parenthetical added. |
| 05 | PLFR acronym provenance | UNVERIFIED | Practitioner mnemonic, no single authoritative source; honest parenthetical added. |
| 05 | Negative-constraint entropy reduction | UNVERIFIED | Mechanism-plus-judgment, no clean published number; honest parenthetical added. |
| 05 | PAST/PLFR References entry | UNVERIFIED | Reworded as practitioner mnemonics, no primary source. |
| 06 | ELI5 simplification suppresses information | UNVERIFIED | Practitioner-reported; honest parenthetical added (no single controlled study cited). |
| 06 | ExpertPrompting (Xu et al. 2023), arXiv:2305.14688 | CONFIRMED | arXiv:2305.14688, Xu et al. 2023. Inline scope note added (answer quality, not factual recall); full reference added. |
| 06 | Zheng et al. "Helpful Assistant," 162 personas / 2,410 Qs / 4 families | CONFIRMED + DATE CORRECTED | arXiv:2311.10054; year corrected 2023 → 2024 (Findings of EMNLP 2024); authors expanded (Zheng, Pei, Logeswaran, Lee, Jurgens). |
| 06 | Expert persona reduces MMLU 71.6% → 66.3% (PRISM) | CONFIRMED | arXiv:2603.18507 "Expert Personas Improve LLM Alignment but Damage Accuracy." Citation added inline + References. |
| 06 | Li et al. persona drift: >30% degradation after 8–12 turns, self-consistency metric | CONFIRMED | Metrics (prompt-to-line / line-to-line / Q&A consistency) and >30%/8–12-turn figure from arXiv:2511.00222 (2025). Marker deleted; reference added. |
| 06 | Persona bleeding: conformity/confabulation/impersonation rates | UNVERIFIED | Pathways documented qualitatively; quantitative rates not established. Honest parenthetical added. |

**Tally:** CONFIRMED 12 · OUTDATED 1 · DATE-CORRECTED 1 (counted under CONFIRMED for Zheng) · UNVERIFIED 8 · meta-note tokens 2.

**Remaining UNVERIFIED (kept with honest parentheticals, no bare `[verify]`):** Gemini 2.5 incident claim (removed entirely), weak uncertainty-surfacing effect, PAST acronym, PLFR acronym, negative-constraint entropy number, ELI5 information-loss study, persona-bleeding contamination rates.

---

## Batch: B

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

---

## Batch: C

# Fact-check _fc-C: PE Ch14 + Ch15 [verify] resolution

| chapter | claim | verdict | resolution/source |
|---|---|---|---|
| 14 | Output quality degrades as context approaches ~80% of capacity (Anthropic best-practices) | PARTLY-CONFIRMED / practitioner heuristic | No published hard "80%" threshold; aligns with Claude Code auto-compaction defaults and practitioner consensus. Reframed as practitioner heuristic, not asserted as Anthropic-published number. (code.claude.com/docs best-practices) |
| 14 | CLAUDE.md delivered as `<system-reminder>` in a user message with "may or may not be relevant... not respond unless highly relevant" caveat | CONFIRMED | Wording matches the actual live system-reminder block. Flag dropped. |
| 14 | Instruction-capacity ceiling ~150–200 instructions; ~50 slots consumed by system prompt (HumanLayer) | UNVERIFIABLE practitioner figure | Practitioner research via HumanLayer; no controlled study. Chapter already attributes "via HumanLayer"; existing "[verify all figures]" left as-is per instruction not to touch that line — see note. |
| 14 | HumanLayer runs a production CLAUDE.md under 60 lines | UNVERIFIABLE practitioner figure | Attributed as "[practitioner report, not a controlled study]"; bare [verify] dropped. |
| 14 | Willison "lethal trifecta" ref | CONFIRMED | simonwillison.net, Jun 16 2025. https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/ |
| 14 | Anthropic "Effective context engineering for AI agents" (Sep 2025) | CONFIRMED | anthropic.com/engineering/effective-context-engineering-for-ai-agents |
| 14 | Anthropic "Equipping agents with Agent Skills" (Dec 2025) | CONFIRMED + corrected title | Full title "Equipping agents for the real world with Agent Skills," Dec 18 2025. anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills |
| 14 | Anthropic Claude Code documentation ref | CONFIRMED | code.claude.com/docs best-practices. |
| 14 | HumanLayer "Writing a good CLAUDE.md" (Nov 2025) ref | CONFIRMED-as-practitioner | Cited; tagged as practitioner write-up, not peer-reviewed. |
| 14 | OWASP Top 10 for LLM Apps — prompt injection #1 | CONFIRMED | LLM01:2025 Prompt Injection, #1 for second consecutive edition. genai.owasp.org/llmrisk/llm01-prompt-injection/ |
| 14 | VILA-Lab "Dive into Claude Code," 253 CLAUDE.md / 242 repos, arXiv:2604.14228 | CONFIRMED | Liu, Zhao, Shang, Shen (MBZUAI VILA Lab). 253 files / 242 repos confirmed. arXiv:2604.14228 |
| 14 | Cymulate/THN: 30+ vulns across six tools; CVE-2025-61260 (Codex CLI MCP) | CONFIRMED | THN Dec 2025 "30+ flaws"; CVE-2025-61260 = Codex CLI auto-exec of MCP server entries w/o approval, patched in 0.23.0. thehackernews.com/2025/12; cymulate.com blog |
| 15 | Prompting Science Report 4 (Expert Personas) exact date | CONFIRMED | "Playing Pretend: Expert Personas Don't Improve Factual Accuracy," arXiv:2512.05858 (Dec 2025); SSRN 5879722; authors Basil, Shapiro, Shapiro, Mollick, Mollick, Meincke. |
| 15 | CorrectBench arXiv:2510.16062, recent preprint, percentages pending review | CONFIRMED | "Can LLMs Correct Themselves?" submitted Oct 17 2025; intrinsic/external/fine-tuned taxonomy confirmed; percentage claims cited as single-preprint. arxiv.org/abs/2510.16062 |

---

