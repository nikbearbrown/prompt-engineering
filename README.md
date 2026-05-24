# Prompt Engineering with LLMs

*A Rigorous Framework for Designing, Evaluating, and Scaling Language Model Interactions*

**Author:** Humanitarians AI

**Folder:** `books/prompt-engineering/`

---

## Overview

A theory-first textbook teaching prompt engineering as an engineering discipline — covering the mechanics of LLM output generation, structured prompt frameworks, advanced interaction patterns, fine-tuning and alignment, and the professional practice of building production prompt systems — with a growing case-study layer contributed by students across cohorts.

**Audience.** Northeastern graduate students in INFO 7375 and related courses; practitioners building production prompt and fine-tuning pipelines; researchers who want a rigorous, mechanism-first treatment of what LLMs do and why. Assumes basic probability, linear algebra, and Python; does *not* assume prior exposure to transformer internals — Part I builds that foundation.

**Scope.** **In:** LLM output-generation mechanics (sampling, logits, temperature); hallucination and alignment failure modes; prompt frameworks (Persona, PAST, PLFR, ReAct, Chain-of-Thought, Flipped Interaction); production prompt-stack architecture; fine-tuning (SFT, RAG, LoRA, QLoRA); RLHF and DPO alignment; Chinchilla scaling and catastrophic forgetting; ethical and production-lifecycle concerns.

---

## Table of Contents

<!-- TOC sourced from `outline.md` -->

*Read by `/chapter` to know what's been written, what's planned, and what each chapter assumes. Core claims preserved from Nik's 2026-02-18 Substack TOC.*

---

## Preface

**Why Prompt Engineering Is an Engineering Discipline.** Nik-authored. Motivates the book's mechanism-first, falsifiable-claim standard.

---

## PART I — FOUNDATIONS: HOW LANGUAGE MODELS THINK (AND DON'T)

### Chapter 1 — The Stochastic Machine

*Understanding LLM Output Generation*

**Core claim.** LLMs do not retrieve answers — they sample from learned probability distributions, making every output a probabilistic event, not a deterministic lookup. Deductive reasoning from first principles of softmax and logit distributions explains temperature, Top-K, and Top-P sampling mechanics.

### Chapter 2 — Hallucination

*When Plausibility Beats Truth*

**Core claim.** Hallucination is not a bug to be patched but an emergent property of next-token prediction trained on human text, where fluency and factual grounding are orthogonal objectives. The Fact Check List Pattern is the architectural response.

### Chapter 3 — The Chinese Room and the Limits of Syntax

*Why the Best Pattern Matcher in the World Still Does Not Understand Your Prompt*

**Status:** Drafted 2026-04-21 as compression pass from near-complete Nik source. Awaiting review. Author: **Nik Bear Brown**. Slug: `chinese-room`.

**Core claim.** LLMs are powerful symbol manipulators, but Searle's Chinese Room argument reminds us that syntactic competence does not entail semantic understanding — a distinction with consequential implications for prompt design. The three strongest apparent counter-examples (chain-of-thought on novel problems, in-context learning, benchmark saturation) each turn out, on examination, to be architectural improvements to the syntactic engine rather than evidence of a category shift. Agentic architectures with tool-grounding and human decision nodes partially compensate for the semantic absence without eliminating the underlying limit.

### Chapter 4 — Sycophancy and Computational Skepticism

**Status:** Drafted 2026-04-21. Awaiting review. Author: `[Student — TA to fill in]`. Slug: `sycophancy-and-computational-skepticism`. Student submitted with incorrect book label ("Design of Agentic Systems with Case Studies"); placed in Prompt Engineering based on INFO 7375 course code and verbatim Core Claim match.

**Core claim.** LLMs are trained to maximize approval, not accuracy — making sycophancy a systematic bias that users must actively counteract through computational skepticism. The architectural response is a dissenting sub-agent with *context isolation* (not merely a second model call) plus a Human Decision Node that halts the system on irreconcilable disagreement; the common failure mode is calibration drift, in which the dissenter's context is inadvertently exposed to the pressure signal and the architecture's adversarial function silently dies while the diagram still looks correct.

---

## PART II — PROMPT ENGINEERING FRAMEWORKS

### Chapter 5 — The Architect Mindset

*Designing Prompts as Systems*

**Core claim.** Effective prompt engineering requires the Architect Mindset — designing the full prompt system (root prompts, constraints, persona, format) rather than crafting individual queries ad hoc.

### Chapter 6 — Persona Patterns

*Shaping Who the Model Is and Who It Speaks To*

**Status:** Drafted 2026-04-21. Awaiting review. Author: **Niraj Patel**. Slug: `persona-patterns`. Student submitted labeled as Ch. 12; placed at Ch. 6 per outline's verbatim core-claim match. Length breach: student draft ~8-10K words compressed to ~4K per workshop ceiling; extensive agentic-framework comparison cut (overlaps with Ch. 11 and agentic-systems Ch. 11).

**Core claim.** Two distinct and frequently confused patterns — the Persona Pattern (who the AI is) and the Audience Persona Pattern (who the AI speaks to) — each activate different latent behaviors in the model and must be applied with precision. The combined-pattern prompt works architecturally better than either single-pattern variant because the audience persona acts as a *protective constraint* that bounds the expert persona's tendency toward jargon-heavy output and assumed reader sophistication.

### Chapter 7 — Constraint Engineering

*Negative Prompts, Root Prompts, and Semantic Focus*

**Core claim.** What you tell a model *not* to do is as architecturally important as what you tell it to do — negative constraints sharpen semantic focus and reduce output entropy in ways positive instructions alone cannot achieve.

### Chapter 8 — PAST, PLFR, and Structured Prompt Frameworks

**Core claim.** Structured prompt frameworks — PAST (Problem, Action, Steps, Task) and PLFR (Prompt, Logic, Format, Result) — impose logical scaffolding that reduces ambiguity and improves output reliability at scale.

---

## PART III — ADVANCED PATTERNS AND ARCHITECTURES

### Chapter 9 — Interaction Patterns

*Flipping the Conversation*

**Core claim.** The most powerful prompt patterns are not declarative but interactive — Flipped Interaction, Ask for Input, and Cognitive Verifier shift the model from passive responder to active collaborator.

### Chapter 10 — ReAct

*Grounding Reasoning in the Real World*

**Status:** Drafted 2026-04-21 as a critique-driven revision. Awaiting review. Author: **Nik Bear Brown**. Slug: `react`. Normal Nik-authored theory chapter (no policy flags).

**Core claim.** Chain-of-Thought compounds error via conditional token dependency (effective reliability $\approx P^N$). ReAct interrupts — not eliminates — that dependency chain by injecting Observation tokens that enter the context from outside the model's probability distribution, acting as anchors that counteract the drift from prior wrong Thoughts. The interruption has three named scope limits (context-window salience decay, tool reliability, attention dilution at length), and the engineering work is what you do with them.

### Chapter 11 — The Prompt Stack

*Scalable AI Infrastructure*

**Core claim.** Production AI systems cannot be built on single-turn prompts — the Prompt Stack architecture (pre-prompts, meta-prompts, user prompts, output filters) provides the modular infrastructure required for maintainable, scalable, auditable LLM deployments.

### Chapter 12 — Chain-of-Thought, Few-Shot, and Meta Language Creation

**Core claim.** Chain-of-thought prompting, few-shot exemplars, and Meta Language Creation are complementary techniques that exploit the model's in-context learning capacity — each with distinct failure modes that disciplined prompt engineers must anticipate.

---

## PART IV — FINE-TUNING, ALIGNMENT, AND SCALING

### Chapter 13 — SFT vs. RAG

*When to Bake Knowledge In vs. Retrieve It*

**Core claim.** Supervised Fine-Tuning and Retrieval-Augmented Generation are not competing alternatives but complementary strategies with distinct cost-benefit profiles — the choice between them is an engineering decision driven by knowledge volatility, latency requirements, and update frequency.

### Chapter 14 — LoRA and QLoRA

*Parameter-Efficient Fine-Tuning*

**Status:** Drafted 2026-04-21. Awaiting review. Author: **Shwetanshu Subhash Deshmukh**. **Policy flag:** theory-authored-by-student — an exception to the "Nik-authored theory, student-authored cases" convention. Editor decision required: keep as student-authored theory, rewrite in Nik's voice, or move to Part VI as a case study of LoRA/QLoRA tradeoffs in a specific deployment.

**Core claim.** LoRA and QLoRA make fine-tuning democratically accessible by decomposing weight updates into low-rank matrices (LoRA) and combining this with 4-bit quantization of frozen base weights (QLoRA) — but the choice between full fine-tuning, LoRA, and QLoRA is an *architectural* decision about serving topology, not merely a cost optimization.

### Chapter 15 — RLHF, DPO, and Alignment

*Training Models to Do What We Mean*

**Core claim.** RLHF is the dominant method for aligning LLM behavior with human values, but it introduces systematic risks — sycophancy, reward hacking, value misspecification — that DPO and Constitutional AI partially mitigate through architectural alternatives.

### Chapter 16 — Catastrophic Forgetting, Chinchilla, and the Science of Scaling

**Core claim.** Scaling language models is not simply a matter of adding parameters — the Chinchilla Scaling Law establishes that optimal performance requires proportional scaling of both model size and training data, while catastrophic forgetting imposes hard constraints on sequential fine-tuning.

---

## PART V — SYNTHESIS AND PROFESSIONAL PRACTICE

### Chapter 17 — Cross-Module Integration

*Connecting Prompt Design to Model Behavior*

**Core claim.** The most consequential prompt engineering decisions sit at the intersection of modules — understanding how RLHF-induced sycophancy interacts with Persona Patterns, or how ReAct brittleness connects to few-shot design, unlocks the next level of engineering judgment.

### Chapter 18 — Ethical Prompt Engineering

*Power, Bias, and Responsibility*

**Core claim.** Prompt engineers wield disproportionate power over model behavior, and with that power comes an obligation to understand how prompts can amplify bias, marginalize voices, or weaponize AI systems — making ethics not an addendum but a design constraint.

### Chapter 19 — Building Production Prompt Systems

*From Prototype to Pipeline*

**Core claim.** A prompt that works in a notebook is not a production system — moving from prototype to pipeline requires versioning, evaluation frameworks, monitoring, and modular architecture that treats prompts as first-class software artifacts.

### Chapter 20 — The Future of Prompt Engineering

*Inference-Aware Scaling, Multimodal Prompting, and Beyond*

**Core claim.** Prompt engineering is a field in rapid transition — inference-aware scaling, multimodal inputs, long-context architectures, and increasingly autonomous agents are reshaping what "a prompt" even means.

---

## PART VI — Production Case Studies (planned; student-authored)

*Empty as of initial book setup. Will hold student-authored chapter-length case studies applying Part I–V frameworks to named real-world projects. Populated across cohorts.*

---

## Appendices

- **A** — Prompt Pattern Reference Card
- **B** — Sampling Parameter Cheat Sheet (Temperature, Top-K, Top-P)
- **C** — Fine-Tuning Decision Framework (SFT vs. RAG vs. LoRA vs. QLoRA)
- **D** — Glossary of Core Concepts
- **E** — Annotated Bibliography and Further Reading
- **F** — INFO 7375 Midterm Study Guide

---

## Drafted

- **Chapter 3 — The Chinese Room and the Limits of Syntax** — drafted 2026-04-21. Awaiting review. Author: **Nik Bear Brown**. Slug: `chinese-room`. Compression pass from near-complete Nik source; §3.8 experimental-paradigms section cut as redundant with §3.4.1 diagnostic method; six exercises pulled for `/mega`.
- **Chapter 4 — Sycophancy and Computational Skepticism** — drafted 2026-04-21. Awaiting review. Author: `[Student — TA to fill in]`. Slug: `sycophancy-and-computational-skepticism`. Book-placement note: student mislabeled as "Design of Agentic Systems" but content matches PE book's Ch. 4 exactly; placed here.
- **Chapter 6 — Persona Patterns: Shaping Who the Model Is and Who It Speaks To** — drafted 2026-04-21. Awaiting review. Author: **Niraj Patel**. Slug: `persona-patterns`. Chapter-number and length notes flagged above.
- **Chapter 10 — ReAct: Grounding Reasoning in the Real World** — drafted 2026-04-21 as critique-driven revision. Awaiting review. Author: **Nik Bear Brown**. Slug: `react`.
- **Chapter 14 — LoRA and QLoRA: Parameter-Efficient Fine-Tuning** — drafted 2026-04-21. Awaiting review. Author: **Shwetanshu Subhash Deshmukh**. Slug: `lora-and-qlora`. Flag: theory-authored-by-student.

## Finalized

## Killed

---

_Generated overview-and-TOC README. Source files (`book.md`, `outline.md`, etc.) remain the working documents._
