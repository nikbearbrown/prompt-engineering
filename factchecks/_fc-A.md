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
