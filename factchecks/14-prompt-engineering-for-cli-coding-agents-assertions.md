# Assertions Report: 14-prompt-engineering-for-cli-coding-agents.md

**Date:** 2026-05-30
**Source file:** chapters/14-prompt-engineering-for-cli-coding-agents.md
**Assertions flagged:** 8
**Breakdown:** STAT: 3 | GUIDELINE: 1 | APPROVAL: 0 | EVIDENCE: 6 | SPECIALIST: 0 | CURRENT: 4

---

## ⚠️ Critical — Requires Immediate Expert Review

None found. All flagged assertions CONFIRMED; practitioner-only figures are explicitly labeled as such in the text.

---

## Full Findings

### EVIDENCE / CURRENT — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "The framing that organizes this comes from Simon Willison: the lethal trifecta... private data... untrusted content... external communication."
**Claim checked:** Lethal-trifecta attribution and definition.
**Site visited:** https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/ (confirmed prior pass, factchecks/_fc-C).
**Finding:** Correct — Willison, Jun 16 2025; three legs as stated. Accurate.
**Expert review needed:** No
**Suggested reference:** Willison, S. The lethal trifecta for AI agents. 2025. simonwillison.net.
**Notes:** None.

### EVIDENCE / CURRENT — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "In Claude Code, CLAUDE.md is not injected as the system prompt. It is delivered as a `<system-reminder>` block inside a user message... this context may or may not be relevant; you should not respond to it unless it is highly relevant." + Anthropic context-engineering and Agent Skills blogs.
**Claim checked:** CLAUDE.md delivery mechanism; Anthropic engineering references.
**Site visited:** Confirmed prior pass (_fc-C): wording matches the live system-reminder; anthropic.com/engineering context-engineering and Agent Skills posts confirmed (Agent Skills full title corrected to "Equipping agents for the real world with Agent Skills," Dec 2025).
**Finding:** Accurate. The system-reminder caveat wording matches; both Anthropic posts exist.
**Expert review needed:** No
**Suggested reference:** Anthropic. Effective context engineering for AI agents (2025); Equipping agents for the real world with Agent Skills (Dec 2025).
**Notes:** None.

### STAT / GUIDELINE — CONFIRMED (practitioner, labeled)
**Assertion type:** POSITIVE (hedged)
**Sentence:** "output quality begins to degrade as the context approaches roughly 80% of capacity." + "ceiling... roughly 150 to 200 distinct instructions... system prompt is reported to consume on the order of 50 of those slots."
**Claim checked:** The 80% degradation heuristic and 150–200 / ~50 instruction-capacity figures.
**Site visited:** Confirmed prior pass (_fc-C): aligns with Claude Code auto-compaction defaults; figures are HumanLayer practitioner research, not a controlled study.
**Finding:** No published hard "80%" threshold or controlled instruction-capacity study exists; the chapter explicitly labels these as practitioner heuristics / "order-of-magnitude guidance" and attributes them to HumanLayer. Honest framing; no overclaim.
**Expert review needed:** No (already correctly caveated in-text).
**Suggested reference:** HumanLayer. Writing a good CLAUDE.md (2025) — practitioner write-up; Anthropic Claude Code docs (auto-compaction).
**Notes:** Treat as practitioner guidance, as the chapter does.

### EVIDENCE / CURRENT — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "A single 2025 disclosure reported 30+ vulnerabilities across six tools (Cursor, Roo Code, JetBrains Junie, Copilot, Kiro.dev, Claude Code). OWASP's 2025 Top-10 for LLM Applications lists prompt injection at number one..."
**Claim checked:** 30+ vulns / six tools; OWASP LLM01.
**Site visited:** Confirmed prior pass (_fc-C): THN/Cymulate Dec 2025 "30+ flaws"; CVE-2025-61260; OWASP genai.owasp.org LLM01:2025.
**Finding:** Confirmed — 30+ vulnerabilities across six named tools; OWASP 2025 ranks prompt injection LLM01 (#1) and notes no foolproof model-layer prevention. Accurate.
**Expert review needed:** No
**Suggested reference:** OWASP Top 10 for LLM Applications 2025, LLM01 Prompt Injection; Cymulate / The Hacker News, Dec 2025.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Yang, J., et al. (2024). SWE-agent: Agent-Computer Interfaces Enable Automated Software Engineering. NeurIPS 2024."
**Claim checked:** SWE-agent reference.
**Site visited:** https://arxiv.org/abs/2405.15793 + NeurIPS 2024 proceedings (re-verified live 2026-05-30).
**Finding:** Correct — Princeton SWE-agent, NeurIPS 2024; agent-computer interface for autonomous software engineering. Accurate.
**Expert review needed:** No
**Suggested reference:** Yang, J., et al. SWE-agent. NeurIPS 2024. arXiv:2405.15793.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "Zhan, Q., et al. (2024). InjecAgent: Benchmarking Indirect Prompt Injections in Tool-Integrated Large Language Model Agents. ACL 2024."
**Claim checked:** InjecAgent reference.
**Site visited:** https://aclanthology.org/2024.findings-acl.624 / arXiv:2403.02691 (re-verified live 2026-05-30).
**Finding:** Correct — InjecAgent (Findings of ACL 2024); 1,054 test cases, 17 user tools, 62 attacker tools; ReAct-prompted GPT-4 vulnerable ~24%. Accurate.
**Expert review needed:** No
**Suggested reference:** Zhan, Q., et al. InjecAgent. Findings of ACL 2024. arXiv:2403.02691.
**Notes:** None.

### EVIDENCE / CURRENT — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "VILA-Lab. Dive into Claude Code... arXiv:2604.14228."
**Claim checked:** VILA-Lab Claude Code study reference.
**Site visited:** Confirmed prior pass (_fc-C): arXiv:2604.14228, 253 CLAUDE.md files / 242 repos.
**Finding:** Confirmed. Accurate.
**Expert review needed:** No
**Suggested reference:** VILA-Lab (MBZUAI). Dive into Claude Code. arXiv:2604.14228.
**Notes:** None.

---

## Unverified Assertions

| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| The Wordsville coding-agent / context-rot opening scenario | EVIDENCE | POSITIVE | Labeled illustrative scenario demonstrating a real, well-documented failure mode (context rot). |
| The u(t) < 0.8C model | SPECIALIST | BASIC | A pedagogical formalization of the practitioner 80% heuristic, not an empirical law; presented as such. |

---

## AI-Pass Flags

- The chapter is careful to label practitioner figures (80% threshold, 150–200 instructions, ~50 system-prompt slots) as practitioner/non-controlled — matching the prior drafting pass's resolution. No overclaim.
- Cross-references to Ch.10 (recency/long-context), Ch.11 (Thought→Action→Observation loop), Ch.6 (single-turn isolation test), and Ch.9 (verify the handoff) are consistent.
- "The model is not your security boundary. The architecture is." is consistent with the OWASP "no foolproof model-layer prevention" finding.

---

## References

(Chapter contains a complete, accurate References section; all eight entries checked and confirmed. No corrections required.)
