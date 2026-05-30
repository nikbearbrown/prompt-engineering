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
