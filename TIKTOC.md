# TIKTOC — Prompt Engineering

*Tik TOC canonical planning document · silent mode · last updated 2026-05-29*

---

## Book Concept Summary

This book teaches **prompt engineering as an engineering discipline** to **graduate students and practitioners building production LLM systems**, by **moving concrete-to-abstract from how models generate and fail, through the patterns and evaluation discipline that control them, to scaling across agents, automated optimization, and the fine-tuning stack** — filling the gap left by trick-list guides and chat-only treatments. It succeeds if the reader can **design, evaluate, and scale a prompt system as an engineered artifact with falsifiable performance claims.**

- **Title:** Prompt Engineering
- **Subtitle:** A Rigorous Framework for Designing, Evaluating, and Scaling Language Model Interactions
- **Editor / primary author:** Prof. Nik Bear Brown, Northeastern University (INFO 7375)
- **Book type:** Course textbook (graduate, 15-week semester). Chapter = week.
- **Logline:** Move from "I type things at a model and hope" to "I design, evaluate, and scale prompt systems as engineered artifacts."

## Thesis

This book argues that **prompt engineering is an empirical engineering discipline, not an art of clever phrasing** — which means that **every prompt decision should rest on a mechanism (sampling, context, training) and a falsifiable claim tested against variants** — and this matters because **systems built on intuition fail in predictable, prompt-sensitive ways that "just ask better" cannot fix.**

## Learner Profile

Northeastern graduate students in INFO 7375 and adjacent courses; practitioners building production prompt and fine-tuning pipelines; researchers wanting a mechanism-first treatment. Assumes probability, linear algebra, Python, and working LLM-API familiarity (system prompts, tool calling, structured outputs). Does **not** assume transformer internals — Part I builds the needed foundation. Common misconception to dislodge: that better wording, not better context-and-evaluation engineering, is the lever.

## Sequencing Model

**Concrete-to-abstract / problem-to-solution.** Open on documented failures (Act One) so the student needs the methods before meeting them; build patterns + evaluation (Act Two); apply at scale (Act Three). First application moment lands in Act One (Ch. 2's Fact-Check List), avoiding the front-loaded-theory failure mode.

## Three-Act Learning Arc

This book takes the reader from *"I type things at a model and hope"* to *"I engineer prompt systems as artifacts"* by first **establishing how and why models generate and fail** (Act One, Ch. 1–4), then **building the patterns and evaluation discipline that control them** (Act Two, Ch. 5–10), then **scaling to agents, automated optimization, and the fine-tuning stack in production** (Act Three, Ch. 11–15).

- **Transition 1→2:** student can name the structural failure modes (sampling variance, hallucination, semantic limits, sycophancy) and now needs methods to control them.
- **Transition 2→3:** student can build, structure, and stress-test single- and long-context prompts, and now scales to agents, automation, and weight-level methods.

---

## Chapter Set (Ch. 0 + 15 primary chapters)

### Chapter 0 — Foundations: Sampling, Logits, and the Shape of a Distribution *(optional front-load)*
- **Capability (Understand):** Read output as a sample from a distribution; define temperature/top-k/top-p mechanically.
- **Absorbs:** prerequisite math currently assumed across Part I. Fold into Ch. 1 if the course assumes it.

### ACT ONE — How Language Models Generate (and Fail)

**Ch. 1 — The Stochastic Machine: Why Output Is Sampled, Not Retrieved**
- Capability (Understand→Apply): Predict how sampling parameters change output; explain why identical prompts diverge.
- Opening: a same-prompt/different-answer reproduction. Bridge: if output is sampled, when is it *wrong* in ways we can't see? → Ch. 2.
- Absorbs: outline Ch. 1.

**Ch. 2 — Hallucination and the Plausibility–Truth Gap**
- Capability (Analyze): Diagnose why fluency and grounding are orthogonal; deploy a Fact-Check List as the architectural response.
- Absorbs: outline Ch. 2 + Fact-Check-List half of pattern draft 6C + research §1 (CoT-rationale "format over truth").
- Bridge: if the model can be fluent and wrong, can it even be said to *understand*? → Ch. 3.

**Ch. 3 — The Limits of Syntax: What a Pattern-Matcher Cannot Do**
- Capability (Analyze): Distinguish syntactic competence from semantic understanding; locate where the gap bites prompt design.
- Absorbs: drafted Ch. 3 (Chinese Room).

**Ch. 4 — Sycophancy and Computational Skepticism**
- Capability (Evaluate): Detect approval-maximization bias; build a context-isolated dissent check.
- Absorbs: drafted Ch. 4 + Helpful-Assistant/sycophancy-trap half of 6C.

### ACT TWO — Designing Prompts as Systems

**Ch. 5 — The Architect Mindset: Structured Prompt Frameworks**
- Capability (Apply→Create): Design a full prompt system (root/constraints/format) via PAST and PLFR.
- Absorbs: outline Ch. 5 + Ch. 8 (PAST/PLFR) + Ch. 7 (Constraint Engineering / negative prompts).

**Ch. 6 — Persona and Audience Patterns**
- Capability (Apply): Apply Persona vs. Audience Persona precisely; use audience as a protective constraint.
- Absorbs: drafted Ch. 6.

**Ch. 7 — Structuring and Governing Output**
- Capability (Apply): Impose output structure (Template, Recipe, Outline Expansion, Menu Actions) and govern it (Semantic Filter); anticipate slot-confabulation.
- Absorbs: pattern draft 6A + Semantic-Filter portion of 6C.

**Ch. 8 — Reasoning and Range Patterns**
- Capability (Evaluate): Decide when to elicit reasoning (CoT, few-shot) vs. widen range (Alternative Approaches, self-consistency, Game Play, Tail Generation); recognize when reasoning models make CoT redundant.
- Absorbs: outline Ch. 12 (CoT/few-shot/Meta-Language) + pattern draft 6B + research §1 (CoT conditionality).

**Ch. 9 — Prompt Brittleness and the Discipline of Evaluation**
- Capability (Evaluate→Create): Test a prompt across format variants and quantify brittleness; reject single-prompt evals.
- Absorbs: research §2. *(New chapter — the empirical spine of "engineering, not vibes.")*

**Ch. 10 — Long-Context Prompting: Position, Retrieval, and Injection**
- Capability (Apply→Analyze): Place instructions for recency; predict multi-needle collapse; defend against long-context injection.
- Absorbs: research §3. *(New chapter.)*

### ACT THREE — Scaling, Agents, and Production

**Ch. 11 — Agentic and Multi-Turn Systems**
- Capability (Create): Structure a Thought→Action→Observation loop; control tool exposure; enforce structured output; manage multi-turn context.
- Absorbs: drafted Ch. 10 (ReAct) + outline Ch. 9 (Interaction Patterns) + Ch. 11 (Prompt Stack) + research §4.

**Ch. 12 — Automated Prompt Optimization: The Post-Manual Era**
- Capability (Evaluate→Create): Express a task as a DSPy Signature; run an optimizer (MIPROv2/APE/OPRO); decide when automation beats hand-tuning.
- Absorbs: research §5. *(New chapter.)*

**Ch. 13 — Beyond Prompting: The Fine-Tuning Stack**
- Capability (Evaluate): Decide across the layered stack — prompt-optimize → SFT/RAG → RL (GRPO) — by knowledge volatility, latency, and verifiable reward.
- Absorbs: outline Ch. 13 (SFT vs RAG) + Ch. 14 (LoRA/QLoRA) + Ch. 15 (RLHF/DPO) + research §6. *(Chinchilla/forgetting → appendix or sidebar.)*

**Ch. 14 — Prompt Engineering for CLI Coding Agents: Why Context Is the Bottleneck** *(NEW — overview; full treatment in the companion volume)*
- **Capability (Understand→Apply):** Explain how prompting a stateful CLI coding agent differs from one-shot chat prompting, and apply the core context-engineering moves — persistent instruction files, the plan-then-execute split, context-budget management, and an injection-aware permission posture.
- **One-line:** The student learns to engineer an agent's *context system*, not just its prompt — and to recognize when the bottleneck is what the agent knows, not how smart it is.
- **Opening strategy:** a documented agent failure — a long session where accumulating "context rot" (failed attempts, stale reads) silently degrades behavior on a task the agent handled cleanly in a fresh session. The incident motivates the whole chapter: in agents, *context is the bottleneck, not intelligence.*
- **Core content blocks:**
  1. **Statefulness and the token budget.** Chat = one-shot; CLI agent = read→reason→act→observe loop over an accumulating context. Token budget is a first-class constraint (quality degrades near ~80% capacity). Ties back to Ch. 10 (long-context position effects, recency, context rot).
  2. **Persistent instruction files replace the system prompt.** CLAUDE.md / AGENTS.md / `.cursorrules` — auto-loaded, re-read, delivered as a *user-message* `<system-reminder>` (influential, not absolute; irrelevant sections deliberately ignored). The instruction-capacity ceiling (~150–200 followable instructions; ~50 already consumed by the agent's own system prompt) ⇒ keep the file an onboarding map (WHAT/WHY/HOW), under ~100 lines, with progressive disclosure (`agent_docs/`).
  3. **Context engineering for large codebases.** Static vs. dynamic context; directory-scoped files; pointers over copies; cache-stable layout; sub-agents over whole-repo dumps. Connects to Ch. 11 (multi-agent / operator-worker).
  4. **Plan in one session, execute in another.** Exploratory context pollutes execution; the fresh-context plan→execute split is the highest-leverage workflow change. Scope and stopping conditions; slash commands for repeated workflows; `/clear` after two failed corrections.
  5. **Multi-session continuity and injection security.** Compaction, handoff notes, work logs, registry/sub-agent patterns; then Simon Willison's "lethal trifecta" and why prompt injection through untrusted repo content is unsolvable at the model layer — architecture (sandboxing, approvals, scoping) is the defense. Ties to Ch. 4 (skepticism) and Ch. 9 (eval discipline).
- **Worked example:** turning a bloated, rule-dump CLAUDE.md into a <100-line onboarding map + `agent_docs/` index, then running a plan→execute split on a scoped refactor with explicit verification commands.
- **Assessable exercises:** (Analyze) diagnose context-rot vs. instruction-overflow vs. injection in three provided agent transcripts; (Apply) rewrite an over-long instruction file under the capacity ceiling; (Create) write a CLAUDE.md + task-prompt pair with scope, stopping condition, verification, and security posture.
- **Bridge:** if a single engineer can now direct a fleet of agents across a codebase, what are the production, ethical, and labor consequences? → Ch. 15.
- **Companion cross-reference:** This chapter is an overview. The full treatment is the companion volume *Prompt Engineering for CLI AI Coding Agents* (Claude Code, Codex CLI, Cursor, Aider, Cowork) — which develops CLAUDE.md/AGENTS.md design, instruction-capacity math, context-management patterns, multi-session continuity, tool-specific behavior, and the security/prompt-injection landscape in depth.
- **Aging risk:** HIGH (tool-specific). Structure the chapter so the stable core (statefulness, context budget, plan/execute, injection trifecta) is separated from current-state tool details (byte/line limits, file names, CVEs), which the companion book and a "current tools" sidebar carry.

**Ch. 15 — Production, Ethics, and What Comes Next**
- Capability (Evaluate→Create): Move a prompt from notebook to monitored pipeline; weigh bias/power obligations; reason about the obsolescence, self-critique, and multimodal debates.
- Absorbs: outline Ch. 18 (Ethics) + Ch. 19 (Production) + Ch. 20 (Future) + research §7. *(Cross-Module Integration woven through as synthesis.)*

---

## Bloom's Distribution (15 primary chapters)
- Understand-anchored: Ch. 1 (and Ch. 0)
- Analyze-anchored: Ch. 2, 3, 10
- Apply-anchored: Ch. 5, 6, 7, 14
- Evaluate/Create-anchored: Ch. 4, 8, 9, 11, 12, 13, 15

Twelve of fifteen chapters anchor at Apply or above.

## Companion Volumes
- *Prompt Engineering for CLI AI Coding Agents* — the depth treatment behind Ch. 14.

## Contested Claims / Aging-Risk Audit (high-risk chapters)
- **Ch. 8** — "CoT decreasing value on reasoning-tuned models" is recent and contested; separate the stable mechanism (conditional-token error compounding) from current model behavior.
- **Ch. 12** — automated-optimization figures (GEPA/DSPy/MIPRO) are 2024–2026 and fast-moving; cite specific deltas with baselines, flag preprints.
- **Ch. 14** — tool-specific details (byte/line caps, CVEs, file names) age fastest; quarantine to a current-tools sidebar + the companion book.
- **Ch. 13, 15** — RL/alignment landscape and "future" content age; structure stable-vs-current.

## Out of Scope (this edition)
- Deep transformer internals; pretraining data curation; full training pipelines (per book.md scope).
- Chinchilla scaling & catastrophic forgetting → appendix, not a chapter.
- Cross-Module Integration as a standalone chapter → woven through Act Three.

---
*Source inputs consolidated here: existing `outline.md` (20 ch.), pattern-family drafts `chapters/06a–06c`, research files `pantry/research-ch-01…07`, and the CLI-coding-agents research synthesis (Ch. 14). To pressure-test: `/g2`, `/looptest`, `/scopecheck` in interactive mode.*
