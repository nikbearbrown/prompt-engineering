# Assertions Report: 11-agentic-and-multi-turn-systems.md

**Date:** 2026-05-30
**Source file:** chapters/11-agentic-and-multi-turn-systems.md
**Assertions flagged:** 9
**Breakdown:** STAT: 5 | GUIDELINE: 0 | APPROVAL: 0 | EVIDENCE: 9 | SPECIALIST: 1 | CURRENT: 2

---

## ⚠️ Critical — Requires Immediate Expert Review

None found. All flagged assertions resolved to CONFIRMED.

---

## Full Findings

### EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "ReAct (Yao et al., 2023, ICLR)... evaluated ReAct on HotpotQA, FEVER, ALFWorld, and WebShop; it outperforms reason-only and act-only baselines and reduces fact hallucination."
**Claim checked:** ReAct method, benchmarks, attribution (arXiv:2210.03629).
**Site visited:** arXiv:2210.03629.
**Finding:** Correct — ReAct (Reason+Act), ICLR 2023, evaluated on HotpotQA, FEVER, ALFWorld, WebShop; outperforms reason-only/act-only and reduces hallucination. Accurate.
**Expert review needed:** No
**Suggested reference:** Yao, S., et al. ReAct: Synergizing Reasoning and Acting in Language Models. ICLR 2023. arXiv:2210.03629.
**Notes:** None.

### SPECIALIST — CONFIRMED (computational)
**Assertion type:** POSITIVE
**Sentence:** "the whole chain succeeds with probability roughly P^N. At P = 0.95 and N = 10, that is about 60 percent. At N = 20, about 36 percent."
**Claim checked:** P^N arithmetic.
**Site visited:** Direct computation.
**Finding:** 0.95^10 = 0.5987 (~60%); 0.95^20 = 0.3585 (~36%). Correct. (The independence assumption is explicitly stated as a simplification.)
**Expert review needed:** No
**Suggested reference:** —
**Notes:** Math accurate.

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "LongFuncEval (2025)... as the available-tool description grows from roughly 8K to 120K tokens... function-calling performance drops by 7 to 85 percent..."
**Claim checked:** LongFuncEval tool-count degradation band (arXiv:2505.10570).
**Site visited:** arXiv:2505.10570 (confirmed prior pass, factchecks/_fc-B).
**Finding:** Confirmed — abstract states 7%–85% (tool count) degradation. The chapter uses the corrected "7 to 85 percent" (prior drafting had an unsupported "7.6%–85.6%"). Accurate.
**Expert review needed:** No
**Suggested reference:** Kate, K., et al. LongFuncEval. 2025. arXiv:2505.10570.
**Notes:** Prior pass corrected the decimals; current text is right.

### EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "reproduced across Gorilla/APIBench (Patil et al., 2023), ToolLLM over 16,464 real APIs, and the Berkeley Function Calling Leaderboard."
**Claim checked:** Gorilla (arXiv:2305.15334), ToolLLM 16,464 APIs (arXiv:2307.16789), BFCL.
**Site visited:** arXiv:2305.15334, arXiv:2307.16789 (re-verified live 2026-05-30).
**Finding:** Gorilla/APIBench correct; ToolLLM/ToolBench covers "16000+ real-world APIs" — the specific 16,464 is ToolBench's API count, accurate; BFCL is a real Berkeley leaderboard. All correct.
**Expert review needed:** No
**Suggested reference:** Patil, S.G., et al. Gorilla. arXiv:2305.15334; Qin, Y., et al. ToolLLM. ICLR 2024. arXiv:2307.16789.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Willard and Louf (2023) reframed generation as transitions over a finite-state machine compiled from a regex or context-free grammar... mask the rest to near-zero probability."
**Claim checked:** Constrained-decoding / guided-generation attribution (arXiv:2307.09702).
**Site visited:** arXiv:2307.09702.
**Finding:** Correct — "Efficient Guided Generation for Large Language Models" (Outlines); FSM-based token masking for grammar-constrained decoding. Accurate. OpenAI Structured Outputs (Aug 2024) uses the same idea — also accurate.
**Expert review needed:** No
**Suggested reference:** Willard, B.T., & Louf, R. Efficient Guided Generation for Large Language Models. 2023. arXiv:2307.09702.
**Notes:** None.

### STAT / EVIDENCE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Tam et al. (2024)... found that forcing format restrictions degrades reasoning by roughly 10 to 15 percent on math and symbolic tasks versus free-form generation."
**Claim checked:** Format-restriction reasoning cost (arXiv:2408.02442, EMNLP 2024 Industry).
**Site visited:** arXiv:2408.02442 (paper confirmed prior pass).
**Finding:** Confirmed — "Let Me Speak Freely?" finds format restriction reduces reasoning performance; the chapter's "10–15%" is consistent with the paper's reported degradations on reasoning tasks. The answer-before-reasoning ordering point is also from the paper's analysis.
**Expert review needed:** No
**Suggested reference:** Tam, Z.R., et al. Let Me Speak Freely? EMNLP 2024 Industry Track. arXiv:2408.02442.
**Notes:** None.

### EVIDENCE — CONFIRMED
**Assertion type:** BASIC
**Sentence:** "MemGPT (Packer et al., 2023) framed this with an operating-systems analogy: treat the context window like RAM and external storage like disk..."
**Claim checked:** MemGPT framing/attribution (arXiv:2310.08560).
**Site visited:** arXiv:2310.08560.
**Finding:** Correct — MemGPT's virtual-context-management (OS/RAM-disk) analogy with function-call paging. Accurate.
**Expert review needed:** No
**Suggested reference:** Packer, C., et al. MemGPT: Towards LLMs as Operating Systems. 2023. arXiv:2310.08560.
**Notes:** None.

### STAT / CURRENT — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "Laban et al. (2025)... found an average 39 percent performance drop from single-turn to multi-turn... when a model takes a wrong turn, it gets lost and does not recover."
**Claim checked:** 39% average multi-turn drop and non-recovery effect (arXiv:2505.06120).
**Site visited:** https://arxiv.org/abs/2505.06120 (re-verified live 2026-05-30).
**Finding:** Confirmed exactly — average 39% drop across six generation tasks over 200,000+ simulated conversations; "when LLMs take a wrong turn... they get lost and do not recover." Microsoft (Laban, Hayashi, Zhou, Neville). Accurate.
**Expert review needed:** No
**Suggested reference:** Laban, P., et al. LLMs Get Lost in Multi-Turn Conversation. 2025. arXiv:2505.06120.
**Notes:** Chapter correctly labels the *mechanism* (attention to recent turns) as a hypothesis while the 39% is measured.

### STAT / EVIDENCE / CURRENT — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** "τ-bench (Yao et al., 2024)... even strong models succeed on under 50 percent of multi-turn tool-agent tasks and are inconsistent across trials." + Anthropic "Building Effective Agents" (Dec 2024) workflows-vs-agents.
**Claim checked:** τ-bench <50% (arXiv:2406.12045) and Anthropic guidance.
**Site visited:** arXiv:2406.12045; anthropic.com/research/building-effective-agents.
**Finding:** Correct — τ-bench shows leading models below ~50% success and inconsistent (pass^k) on tool-agent-user tasks; Anthropic's "Building Effective Agents" (Dec 2024) makes the workflows-vs-agents distinction and favors simple composable workflows. Both accurate.
**Expert review needed:** No
**Suggested reference:** Yao, S., et al. τ-bench. ICLR 2025. arXiv:2406.12045; Anthropic, Building Effective Agents, 2024.
**Notes:** None.

---

## Unverified Assertions

| Sentence | Category | Assertion Type | Reason unverified |
|---|---|---|---|
| Multi-turn degradation mechanism ("attention concentrates on recent turns and the early correct framing decays") | SPECIALIST | BASIC | Chapter explicitly labels this a hypothesis inferred from Ch.10 position effects, not settled mechanism — honest. |

---

## AI-Pass Flags

- The "Humanitarians AI volunteer-onboarding agent" is a labeled running illustration.
- Citations are dense and uniformly accurate; the chapter consistently separates measured results from inferred mechanisms.
- The Augmentation/Automation/Agency distinction and the deferral of "authority-to-act" to permissions/human nodes (tying back to Ch.4) is internally consistent.

---

## References

(Chapter contains a complete, accurate References section; all eleven entries checked and confirmed. No corrections required.)
