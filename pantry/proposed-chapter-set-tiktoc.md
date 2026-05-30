# Proposed Chapter Set — *Prompt Engineering*

*Tik TOC · silent mode · 2026-05-29*
*Book type: course textbook (graduate, INFO 7375, 15-week semester). Target: 12–14 primary chapters + Chapter 0 foundations.*

This set consolidates three inputs into one course-adoptable spine: the existing 20-chapter `outline.md`, the three new pattern-family chapters (6A/6B/6C), and the seven research candidate chapters (`pantry/research-ch-01…07`). The raw union runs ~30 chapters — past the hard ceiling. What follows is the consolidation: 14 primary chapters in a concrete-to-abstract / problem-to-solution arc, every title named for a capability, not a topic.

---

## Arc statement

This book takes the reader from *"I type things at a model and hope"* to *"I design, evaluate, and scale prompt systems as engineered artifacts"* — by first establishing **how and why models generate and fail** (Act One), then building **the patterns and evaluation discipline that control them** (Act Two), then **scaling to agents, automated optimization, and the prompting↔fine-tuning stack in production** (Act Three).

---

## Chapter 0 — Foundations: Sampling, Logits, and the Shape of a Distribution
*(optional front-load; absorb into Ch.1 if the course assumes it)*
- **Capability:** Read an LLM's output as a sample from a probability distribution, and define temperature/top-k/top-p mechanically.
- **Bloom:** Understand · **Absorbs:** prerequisite math currently assumed across Part I.

---

## ACT ONE — How Language Models Generate (and Fail)
*Establish the problem before any technique. Four short, concrete chapters.*

**Ch. 1 — The Stochastic Machine: Why Output Is Sampled, Not Retrieved**
- Capability: Predict how sampling parameters change output, and explain why identical prompts diverge.
- Bloom: Understand → Apply · Absorbs: outline Ch.1.

**Ch. 2 — Hallucination and the Plausibility–Truth Gap**
- Capability: Diagnose why fluency and factual grounding are orthogonal, and deploy a Fact-Check List as the architectural response.
- Bloom: Analyze · Absorbs: outline Ch.2 + the Fact-Check-List half of new 6C + research §1 (CoT-rationale "format over truth" finding).

**Ch. 3 — The Limits of Syntax: What a Pattern-Matcher Cannot Do**
- Capability: Distinguish syntactic competence from semantic understanding and identify where that gap bites prompt design.
- Bloom: Analyze · Absorbs: drafted Ch.3 (Chinese Room).

**Ch. 4 — Sycophancy and Computational Skepticism**
- Capability: Detect approval-maximization bias and build a context-isolated dissent check.
- Bloom: Evaluate · Absorbs: drafted Ch.4 + the Helpful-Assistant/sycophancy-trap half of new 6C.

*Transition 1→2: the student can name the three structural failure modes (sampling variance, hallucination, sycophancy) and now needs methods to control them.*

---

## ACT TWO — Designing Prompts as Systems
*Build the patterns and the evaluation discipline.*

**Ch. 5 — The Architect Mindset: Structured Prompt Frameworks**
- Capability: Design a full prompt system (root/constraints/format) using PAST and PLFR rather than ad-hoc queries.
- Bloom: Apply → Create · Absorbs: outline Ch.5 + Ch.8 (PAST/PLFR) + Ch.7 (Constraint Engineering / negative prompts).

**Ch. 6 — Persona and Audience Patterns**
- Capability: Apply Persona vs. Audience Persona precisely; use audience as a protective constraint.
- Bloom: Apply · Absorbs: drafted Ch.6.

**Ch. 7 — Structuring and Governing Output**
- Capability: Impose output structure (Template, Recipe, Outline Expansion, Menu Actions) and govern it (Semantic Filter); anticipate slot-confabulation.
- Bloom: Apply · Absorbs: new 6A + the Semantic-Filter portion of new 6C.

**Ch. 8 — Reasoning and Range Patterns**
- Capability: Decide when to elicit reasoning (CoT, few-shot) and when to widen range (Alternative Approaches, self-consistency, Game Play, Tail Generation) — and when modern reasoning models make CoT redundant.
- Bloom: Evaluate · Absorbs: outline Ch.12 (CoT/few-shot/Meta-Language) + new 6B + research §1 (CoT conditionality) + Meta-Language Creation.

**Ch. 9 — Prompt Brittleness and the Discipline of Evaluation**
- Capability: Test a prompt across format variants and quantify brittleness; reject single-prompt evals.
- Bloom: Evaluate → Create · Absorbs: research §2. *(New chapter — the empirical spine of "engineering, not vibes.")*

**Ch. 10 — Long-Context Prompting: Position, Retrieval, and Injection**
- Capability: Place instructions for recency, predict multi-needle collapse, and defend against long-context injection.
- Bloom: Apply → Analyze · Absorbs: research §3. *(New chapter.)*

*Transition 2→3: the student can build, structure, and stress-test single- and long-context prompts, and now scales to agents, automation, and weight-level methods.*

---

## ACT THREE — Scaling, Agents, and Production
*Apply under production constraints.*

**Ch. 11 — Agentic and Multi-Turn Systems**
- Capability: Structure a Thought→Action→Observation loop, control tool exposure, enforce structured output, and manage multi-turn context.
- Bloom: Create · Absorbs: drafted Ch.10 (ReAct) + outline Ch.9 (Interaction Patterns: Flipped Interaction, Ask-for-Input) + Ch.11 (Prompt Stack) + research §4 (tool-count degradation, structured output, memory).

**Ch. 12 — Automated Prompt Optimization: The Post-Manual Era**
- Capability: Express a task as a DSPy Signature, run an optimizer (MIPROv2/APE/OPRO), and decide when automation beats hand-tuning.
- Bloom: Evaluate → Create · Absorbs: research §5. *(New chapter.)*

**Ch. 13 — Beyond Prompting: The Fine-Tuning Stack**
- Capability: Decide across the layered stack — prompt-optimize → SFT/RAG → RL (GRPO) — by knowledge volatility, latency, and verifiable reward.
- Bloom: Evaluate · Absorbs: outline Ch.13 (SFT vs RAG) + Ch.14 (LoRA/QLoRA) + Ch.15 (RLHF/DPO) + research §6 (decision logic). *(Ch.16 Chinchilla/forgetting → appendix or a sidebar here.)*

**Ch. 14 — Production, Ethics, and What Comes Next**
- Capability: Move a prompt from notebook to monitored pipeline; weigh bias/power obligations; reason about the obsolescence, self-critique, and multimodal debates.
- Bloom: Evaluate → Create · Absorbs: outline Ch.18 (Ethics) + Ch.19 (Production Systems) + Ch.20 (Future) + research §7 (contested/emerging). *(Ch.17 Cross-Module Integration → woven through as synthesis, not its own chapter.)*

---

## Bloom's distribution (14 primary chapters)
- Understand-anchored: Ch.1 (and Ch.0)
- Analyze-anchored: Ch.2, 3, 10
- Apply-anchored: Ch.5, 6, 7
- Evaluate/Create-anchored: Ch.4, 8, 9, 11, 12, 13, 14

Eleven of fourteen chapters anchor at Apply or above; first application moment arrives in Act One (Ch.2's Fact-Check List), avoiding the front-loaded-theory failure mode.

## What moved to appendices / out of scope
- **Chinchilla scaling & catastrophic forgetting** (old Ch.16) → Appendix or a Ch.13 sidebar; it's reference, not a capability build for a prompt-engineering course.
- **Cross-Module Integration** (old Ch.17) → not a standalone chapter; its content is the synthesis threaded through Act Three.
- **Meta-Language Creation** → folded into Ch.8 rather than its own chapter.

## What's new vs. the current outline
Three genuinely new chapters earn their place on research, not coverage: **Ch.9 Brittleness**, **Ch.10 Long-Context**, **Ch.12 Automated Optimization**. The three pattern-family drafts (6A/6B/6C) are absorbed into Ch.7 and Ch.8 rather than added as separate chapters — keeping the count at 14.

---
*Silent-mode output. To pressure-test this set: run `/g2` (7 adoption failure modes), `/looptest` (progression), or `/scopecheck` (MoSCoW) in interactive mode.*
