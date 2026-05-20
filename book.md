# Prompt Engineering with LLMs

*A Rigorous Framework for Designing, Evaluating, and Scaling Language Model Interactions*

**Editor and primary author:** Professor Nik Bear Brown, Northeastern University
**Course lineage:** INFO 7375 — Prompt Engineering for Generative AI

---

## One-sentence description

A theory-first textbook teaching prompt engineering as an engineering discipline — covering the mechanics of LLM output generation, structured prompt frameworks, advanced interaction patterns, fine-tuning and alignment, and the professional practice of building production prompt systems — with a growing case-study layer contributed by students across cohorts.

## Audience

Northeastern graduate students in INFO 7375 and related courses; practitioners building production prompt and fine-tuning pipelines; researchers who want a rigorous, mechanism-first treatment of what LLMs do and why. Assumes basic probability, linear algebra, and Python; does *not* assume prior exposure to transformer internals — Part I builds that foundation.

## Scope

**In:** LLM output-generation mechanics (sampling, logits, temperature); hallucination and alignment failure modes; prompt frameworks (Persona, PAST, PLFR, ReAct, Chain-of-Thought, Flipped Interaction); production prompt-stack architecture; fine-tuning (SFT, RAG, LoRA, QLoRA); RLHF and DPO alignment; Chinchilla scaling and catastrophic forgetting; ethical and production-lifecycle concerns.

**Out:** Deep transformer internals (the attention math is used but not derived from scratch); pretraining data curation; model-internal interpretability research beyond what's needed for alignment discussion; full LLM training pipelines.

## Prerequisites

- Calculus and linear algebra through matrix multiplication and singular-value decomposition
- Basic probability (conditional probability, distributions, expectation)
- Python at the level of reading and modifying a training loop
- Working familiarity with using an LLM via API (system prompts, tool calling, structured outputs)

## Authorship convention

This book uses a **theory-case split**:

- **Parts I–V (Chapters 1–20)** — *Nik-authored theory*. Written by Professor Brown. Stable across cohorts. These chapters establish the framework, vocabulary, and mechanism-first treatment the rest of the book depends on.
- **Part VI — Production Case Studies** (planned, student-authored) — case-length chapters in which students apply the Part I–V frameworks to named real-world projects. Renewed each semester. Primary sources required; anonymized/composite cases labeled as such at first mention.

Some student contributions may land in the theory layer during the course's early run (Ch. 14 is one such example). When that happens, the student byline remains on the chapter and a `theory-authored-by-student` flag appears in the chapter's header for editor review. In the stable long-term state, Parts I–V are Prof. Brown's; Part VI is the student case-study layer.

## Drafting policy: always ship a draft

`/chapter` runs for this book **always produce a full chapter draft**, even when source material has gaps or referenced assets don't yet exist. Use `[TODO: ...]` and `[verify]` placeholders inline. Students refine the drafts; placeholders give them something to push against.

## Voice notes (book-specific)

- **Math visible.** Prompt engineering only reads as an engineering discipline when the math is on the page. Loss functions, sampling probabilities, low-rank decompositions — show them. Appendices can carry derivations, but the key equations live in the chapter body.
- **Mechanism before name.** Each concept is explained through its mechanism before its formal name is introduced. The "Feynman Standard" — if you can't explain it without the jargon, you don't yet understand it.
- **Claims are falsifiable.** Every substantive claim in a chapter should be either mathematical (provable), empirical (grounded in cited experiments), or labeled as judgment. No "it is generally accepted" — name the source.
- **Running examples where they pay off.** Wordsville (prompt architecture case), "80 Days to Stay" (SEC data retrieval case), Mycroft (investment intelligence case), Madison (marketing intelligence case), Humanitarians AI (volunteer onboarding case). These recur across chapters to provide continuity.

## Case-study convention (for Part VI)

Student case studies follow a shared template (to be anchored at the workspace root once the first Part VI cases are drafted):

1. **Named source** — a specific project, product, or documented incident; anonymized/composite only if explicitly labeled.
2. **Problem specification** — what the system was built to do, what prompts or fine-tuning strategies were applied.
3. **Architectural analysis** — which Part I–V frameworks apply; which ones were used vs. skipped vs. misapplied.
4. **Failure mode or evaluation result** — what broke, or what the measured outcome was, and why.
5. **Generalizable lesson** — the architectural principle the case teaches that a reader can carry forward.

## Voice ground truth

*Empty as of initial setup. First drafted chapters here will set the voice. Drafts produced before `style/` is populated are flagged `voice-unanchored`.*

---

*Initial version: 2026-04-21.*
*Book is read by `/chapter`, `/bookmap`, and `/mega` every run.*
