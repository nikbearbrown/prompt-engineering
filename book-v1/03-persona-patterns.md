> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft. Fourth chapter drafted for this book.
>
> **Numbering note:** Student submitted labeled as Ch. 12; PE book outline places Persona Patterns at Ch. 6. Placed at Ch. 6 per outline match (verbatim core-claim match). Flagged for editor decision if the numbering change is contested.
>
> **Length note:** Student draft ran ~8,000–10,000 words; compressed to ~4,000 per workshop ceiling. Cut the extensive agentic-framework feature comparison (CrewAI / AutoGen / LangGraph / MetaGPT), which is closer to Ch. 11 (Prompt Stack) territory and overlaps with the agentic-systems book's Ch. 11. Pulled six exercises to `/mega`. The student's own self-assessment acknowledged the framework section remained "feature-list-heavy" despite editor review, which supported the cut decision.

---

# Chapter 6 — Persona Patterns

*Shaping Who the Model Is and Who It Speaks To*

**Author:** Niraj Patel
**Editor:** Nik Bear Brown

---

## Suggested titles

1. **Persona Patterns: Shaping Who the Model Is and Who It Speaks To**
2. **The Metallurgist Who Explained It Perfectly to Nobody**
3. **Two Patterns, One Commonly Conflated Distinction: Why "Who the Model Is" and "Who the Model Addresses" Are Different Instructions**

---

## TL;DR

Two prompt patterns that sound similar activate categorically different model behaviors: the **Persona Pattern** ("You are a metallurgist") steers the model's identity, vocabulary, and reasoning approach; the **Audience Persona Pattern** ("Assume I am a maintenance supervisor") steers the model's output complexity and content selection for a specified reader. Conflating the two — or using only one when the task requires both — produces predictable failures whose forensic trace runs directly back to the prompt architecture, not to the model's capability.

---

## Learning objectives

By the end of this chapter you should be able to:

1. Distinguish the Persona Pattern from the Audience Persona Pattern using the "swap test."
2. Construct a combined-pattern prompt that pairs an expert persona with an explicit audience specification, including the audience's decision context.
3. Name the four documented failure modes (drift, mismatch, hallucination, bleeding) and identify which failure mode an observed system is exhibiting.
4. Apply a five-step diagnostic protocol to classify a degraded persona-based system's failure and select the appropriate architectural fix.
5. Recognize the Audience Persona Pattern as a *protective constraint* on expert personas — the architectural reason combined prompts work better than either pattern alone.

## Prerequisites

Ch. 1 (Stochastic Machine) — token sampling. Ch. 2 (Hallucination) — the orthogonality of plausibility and truth. Ch. 4 (Sycophancy) — the RLHF training pipeline and its consequences for model behavior.

---

## 6.1 The fracture that shouldn't have happened

The scenario below is a composite, drawn from documented failure patterns in materials-characterization AI deployments. The mechanism is real; the specific startup is not.

In March 2024, a materials-characterization startup deployed what they believed was a robust AI assistant for failure analysis. The system helped junior engineers interpret scanning electron microscope images of fractured components. The prompt seemed reasonable:

> *"You are a metallurgist. Explain the fracture surface to the user."*

Within three weeks, the tool had misclassified two fatigue failures as overload fractures. One of these errors nearly resulted in a fleet-wide inspection being cancelled for a regional aircraft operator. The junior engineer had asked for an explanation suitable for a maintenance supervisor with no metallurgy background. The AI, steadfastly performing its metallurgist persona, had delivered technically accurate observations — beach marks, striation spacing, crack propagation direction — in language the supervisor couldn't parse. The supervisor, unwilling to appear ignorant, signed off on a recommendation he didn't understand.

The prompt engineers had made a mistake so common it barely registers: **they had confused who the AI should *be* with who the AI should *speak to*.** These are not the same instruction. They activate different behaviors in the model. And when you swap one for the other — or neglect one entirely — systems fail in ways forensic analysis can trace directly back to the prompt architecture.

This chapter pulls the two patterns apart, shows what each does, shows what goes wrong when they're conflated, and gives you a decision procedure for diagnosing degraded persona-based systems. The stakes aren't rhetorical. The fractured turbine blade doesn't care whether the AI sounded like an expert. It cares whether the maintenance supervisor understood the warning.

---

## 6.2 Two patterns, pulled apart

The distinction was formalized by [White et al. (2023)](https://arxiv.org/abs/2302.11382) at Vanderbilt, in a catalog of sixteen prompt patterns modeled on software design patterns. Two of those patterns govern identity and audience. Their mechanisms are different enough that a reader who treats them as synonyms will build systems that fail in the predictable shape of §6.1.

### The Persona Pattern

*"Act as persona X."* *"Provide outputs that persona X would create."*

The model is given an identity. When you write *"You are a senior corrosion engineer with twenty years of experience in marine environments,"* you are changing the model's output in specific, documented ways — though the internal mechanism remains incompletely understood.

**What we observe.** Across model scales, task types, and research groups, persona assignment produces:

- **Vocabulary and register shift.** A legal advisor persona produces legalistic prose; a cowboy persona produces colloquial Western-flavored language. Replicates across models.
- **Domain focus and content selection.** A cybersecurity auditor looking at a system log highlights vulnerabilities. A performance engineer looking at the same log highlights bottlenecks. Neither is wrong; they select different slices of the relevant information.
- **Reasoning improvement on structured tasks.** [Kong et al. (2023)](https://arxiv.org/abs/2308.07702) tested role-play prompting across 7B–70B models on math and symbolic tasks. AQuA accuracy rose from 53.5% to 63.8%; Last Letter Concatenation jumped from 23.8% to 84.2%. The improvement held across scales — which is evidence of a real phenomenon, not prompt-specific noise.
- **No improvement — and sometimes degradation — on factual recall.** [Zheng et al. (2023)](https://arxiv.org/abs/2311.10054) tested 162 personas across four model families on 2,410 knowledge questions. Persona assignment produced no improvement on factual questions. In related work, detailed expert personas were documented to *reduce* accuracy on MMLU from 71.6% to 66.3% `[verify exact PRISM citation]`. The model, activated into confident expert performance, prioritized sounding authoritative over being correct.

**Why (hypothesis, not confirmed mechanism).** The dominant working explanation is statistical co-occurrence during pretraining: documents written by or about metallurgists share vocabulary patterns and reasoning chains, and persona assignment makes those patterns more probable in next-token predictions. This is plausible. It fits the observed effects. It is not mechanistically confirmed by interpretability research. Treat the behavioral evidence as reliable; treat the mechanistic story as useful intuition, not ground truth.

**What this means for practice.** The Persona Pattern is a behavioral steering tool, not a knowledge amplification tool. High confidence: it shifts vocabulary, style, and domain focus; it likely improves structured-reasoning performance. Low confidence: it transfers to factual recall or domains far from tested benchmarks. In those cases, expert personas may actively degrade accuracy by activating confident communication without activating correct knowledge.

### The Audience Persona Pattern

*"Explain X to me."* *"Assume that I am Persona Y."*

The user is given an identity. The model retains its full knowledge base but filters and adapts its output for the specified audience. When you write *"Assume I am a manufacturing technician with no background in crystallography,"* you are not changing who the model is — you are changing what the model infers about the reader's needs.

Effects are distinct from the Persona Pattern:

- **Complexity adaptation.** Vocabulary difficulty, sentence length, and assumed background knowledge shift automatically.
- **Content selection and information loss.** This is the underappreciated risk. Research on "ELI5-style" (*Explain Like I'm Five*) prompts documents that simplification causes models to provide only a subset of relevant information. The model, inferring the audience cannot handle complexity, suppresses details that might matter. **Audience adaptation is not only stylistic filtering — it is information filtering.** `[verify specific ELI5 citation]`
- **Automatic register adjustment.** Formality, rhetorical approach, and sentence structure shift without explicit instruction.

One historical note worth naming because it creates real practitioner confusion: the Audience Persona Pattern appears in the expanded conference version of [White et al.'s paper](https://arxiv.org/abs/2302.11382) and on the Vanderbilt companion website, but **not** in the original arXiv preprint — the version most cited in the academic literature. Many engineers working from the original paper encounter only the Persona Pattern and assume it covers all identity-related prompting. It doesn't.

### The swap test

The clearest way to see the mechanism is to swap the patterns on the same topic.

**Prompt A (Persona Pattern).** *"You are a first-year undergraduate. Explain the difference between elastic and plastic deformation."*

**Prompt B (Audience Persona Pattern).** *"Explain the difference between elastic and plastic deformation. Assume I am a first-year undergraduate."*

These prompts sound similar. Their outputs are radically different. Prompt A instructs the model to adopt the identity of an undergraduate — to generate text *as if* an undergraduate were writing it. The result is often superficial, uncertain, and possibly incorrect, because the model is simulating a limited-knowledge student. Prompt B instructs the model to maintain expert knowledge while adapting for an undergraduate audience. The result is accurate information presented accessibly.

Swapping one for the other — accidentally or through ignorance of the distinction — can render a system useless or dangerous. The fracture analysis tool in §6.1 made exactly this error. The model performed its metallurgist persona faithfully, producing expert-level output that served no one.

---

## 6.3 Constructing prompts that actually work

Understanding the mechanism enables principled design. Three construction rules.

**Strong Persona beats weak Persona.** [Research on ExpertPrompting](https://arxiv.org/abs/2305.14688) `[verify]` demonstrates that detailed, specific personas significantly outperform generic role assignments.

- Weak: *"You are a materials scientist."*
- Strong: *"You are a senior materials scientist specializing in high-temperature oxidation of nickel-based superalloys, with fifteen years of experience in aerospace turbine blade failure analysis. Your approach emphasizes thermodynamic calculations before microstructural interpretation."*

The strong version activates more specific behavioral patterns and implicitly constrains the reasoning — prioritizing thermodynamic analysis over observational description.

**Strong Audience Persona beats weak Audience Persona.** The goal is not merely simplification but *relevant* simplification — filtering toward what the audience needs for the decision they face.

- Weak: *"Explain this simply."*
- Strong: *"Assume I am a quality control manager at an aluminum extrusion plant. I have a bachelor's degree in mechanical engineering but no graduate training in metallurgy. I need to understand this enough to decide whether to halt production and recall the last two weeks of output."*

The strong version specifies knowledge level *and* decision context. The model selects information relevant to the decision rather than producing generic simplification.

**Combined pattern beats either alone.** The general structure:

> *"Act as [Persona with specific expertise, experience, and methodological orientation]. Explain [topic] to [Audience with knowledge level, professional role, and decision context]."*

Example:

> *"Act as a failure analysis engineer with experience in forensic metallurgy and expert witness testimony. You specialize in explaining technical findings to non-technical audiences in litigation contexts. Explain the evidence for hydrogen embrittlement in this fastener failure to a jury of twelve people with no engineering background. They need to understand enough to evaluate whether the manufacturer's quality control procedures were adequate."*

This prompt activates domain expertise, specifies a communication mode, identifies the audience, and names the decision context. The model must generate output that is technically accurate, legally defensible, accessible to laypeople, and relevant to the specific question of quality control adequacy — all simultaneously.

### The Audience Persona as protective constraint

Here is the architectural insight worth naming explicitly. Expert personas, left unconstrained, tend toward overconfidence, jargon-heavy prose, and assumptions of reader sophistication — these are the behaviors the Persona Pattern activates as a side effect of activating expert-associated language patterns. **Pairing an expert persona with a non-expert audience persona forces the model to retain expertise while adapting communication.** The audience persona does architectural work beyond its obvious role: it constrains the expert persona's excesses.

The fix for the fracture analysis tool is not *"You are a metallurgist"*; it is *"You are a metallurgist explaining findings to a maintenance supervisor who must decide whether to ground an aircraft fleet."* Same model. One additional phrase. Different output. That one phrase is the chapter's master-argument-in-miniature.

---

## 6.4 Four failure modes, compressed

The empirical literature documents four distinct failure modes. Each traces to a specific design decision and manifests through predictable symptoms.

### Persona drift

**Definition.** The model progressively abandons its assigned persona over the course of a multi-turn conversation, reverting to generic assistant behavior.

**Mechanism.** Transformer self-attention allocates weights across all tokens in the context window. As conversation history grows, the system prompt — where persona is typically defined — receives proportionally less attention. The persona directive that dominated at turn 2 is competing for attention with thousands of tokens of conversation history by turn 12. `[verify]` Li et al. measured this quantitatively using a self-consistency metric: persona consistency degrades by more than 30% after 8–12 dialogue turns.

**What drift looks like.** The easy case is explicit frame-breaking — the model says *"As an AI language model, I don't actually have personal experiences..."* The harder case is semantic drift without syntactic signals: the model never announces "As an AI," but its responses become increasingly generic. Specific vocabulary drains out; the voice converges toward default helpful-assistant register wearing a thin persona costume.

**Mitigation.** Periodic persona restatement (crude but effective); memory architectures that maintain persona as a protected component of context separate from conversation history; context-window management that keeps the system prompt salient.

### Persona-audience mismatch

**Definition.** A technical expert persona generates output incomprehensible to the actual audience because no audience persona was specified.

**Mechanism.** Without explicit audience specification, the model infers audience from the persona. An expert metallurgist persona defaults to assuming expert-level readers. This is not a bug — it is the model correctly inferring that metallurgists typically communicate with other metallurgists.

**Symptom.** Technically accurate output that fails to serve the user. Jargon without definition. High precision, zero utility.

**Mitigation.** Always pair expert personas with explicit audience specifications. Include the audience's decision context, not only their knowledge level. The fracture analysis tool exhibited exactly this failure; the fix is in §6.3.

### Persona hallucination

**Definition.** The model, assigned a specific expert persona, fabricates expertise, citations, and domain knowledge it does not possess.

**Mechanism.** The persona activates "expert-like" generation patterns (confident register, citation-heavy prose, domain vocabulary) without activating the underlying knowledge. The model produces text that sounds like expert output without factual grounding. Particularly dangerous in narrow or rapidly evolving domains where training data is sparse — the combination of confident communication style and absent knowledge is worse than either alone. Ch. 2's Fact Check List Pattern is the architectural response on the knowledge side; the persona-level fix is to avoid highly specific expert personas in narrow domains without retrieval augmentation.

**Symptom.** Confident assertions that are factually incorrect. Fabricated citations with plausible-sounding journal names. Domain-appropriate vocabulary deployed inaccurately. The model never expresses uncertainty because the persona pattern activated confident communication style.

**Mitigation.** Avoid specific expert personas in domains without retrieval grounding. Combine persona assignment with explicit uncertainty instructions. Apply the Fact Check List Pattern (Ch. 2) on confident outputs in narrow domains.

### Persona bleeding (multi-agent systems)

**Definition.** In multi-agent systems, personas contaminate each other through inter-agent communication, or agents abandon their assigned personas due to conversational pressure from other agents.

**Mechanism.** Three contamination pathways. *Conformity*: an agent abandons its persona under peer pressure from other agents' confident assertions. *Confabulation*: an agent presents opinions that were neither in its persona definition nor in conversation history — invented content emerging from cross-agent dynamics. *Impersonation*: an agent explicitly claims a different identity than assigned. `[verify specific documentation rates]`

**Mitigation.** Structured inter-agent communication (schemas rather than free-form natural language); memory isolation per agent; system-prompt separation from inter-agent message history. This connects to Ch. 4's context-isolation argument applied at the multi-agent level.

---

## 6.5 Diagnostic protocol

When a persona-based system produces degraded output, five steps in order.

**Step 1 — Single-Turn Isolation Test.** Run the exact input that's producing bad output as a fresh single-turn query with no history. If single-turn output is also bad, drift is ruled out (drift requires accumulated conversation). If single-turn is good but multi-turn is bad, drift is the primary suspect.

**Step 2 — Prompt-Level Diagnosis.** Does the prompt specify audience? If no, mismatch is structurally possible — verify by having a representative of the actual audience evaluate the output. Does the prompt assign expertise in a narrow domain? If yes, hallucination risk is elevated — verify factual claims in confident outputs.

**Step 3 — Drift Characterization.** Compare outputs at different conversation depths. Explicit frame breaks ("As an AI...") = overt drift. Surface persona maintained but details contradicted = semantic drift (requires baseline comparison). Model echoes another agent's vocabulary = bleeding (go to Step 4).

**Step 4 — Agent Isolation Test (multi-agent only).** Run the suspect agent alone on the same task. If it performs correctly alone but fails in the full system, bleeding is the suspect. If it fails alone, the problem is its own prompt or task-beyond-competence; return to Step 2.

**Step 5 — Compound Failure Check.** Production failures are often multicausal. After fixing the first identified cause, re-test. Common compounds: Mismatch + Drift (suboptimal from turn 1, worse by turn 12); Hallucination + Mismatch (confabulates, and the audience can't catch it); Bleeding + Handoff Loss (looks like contamination, actually incomplete context transfer).

The protocol identifies candidate failure modes, not confirmed root causes. Treat diagnosis as iterative — fix the most likely cause, re-test, check for failures that were masked by the first problem.

---

## 6.6 Back to the maintenance supervisor

The fracture analysis tool wasn't broken. It did what its prompt told it to do. The prompt told the model to be a metallurgist, and the model was a metallurgist. Nothing in the prompt told the model who the metallurgist was addressing. The model, reasonably, defaulted to the audience it would infer from the persona — other metallurgists. The maintenance supervisor, who was not a metallurgist, was outside the model's inferred audience. The output was technically correct and operationally useless.

**The fix isn't a better model. The fix isn't a more detailed persona. The fix is to specify the audience.** *"You are a metallurgist explaining findings to a maintenance supervisor who must decide whether to ground an aircraft fleet."* One clause. Different output. Decision-appropriate.

The book's master argument lands here with force: **architecture is the leverage point, not the model.** Two prompts, differing by a single clause of audience specification, produce categorically different system behaviors from the identical model. One ships a jargon wall to a non-technical reader. The other produces an explanation calibrated to the reader's decision context. The model doesn't change. The architecture does.

Persona is not a stylistic convenience. It is an architectural primitive with documented failure modes, predictable symptoms, and specific mitigations. The engineer who treats persona as cosmetic encounters the four failure modes above. The engineer who treats persona as architecture — who specifies *both* speaker identity and audience adaptation, who designs for persistence, who protects against contamination, who builds detection protocols — builds systems that stay coherent at scale.

One honest caveat. The behavioral patterns documented in this chapter are empirical and reproducible; the mechanisms are hypothetical. We have observations (persona assignment shifts vocabulary, improves structured reasoning, doesn't improve factual recall) and a plausible story (statistical co-occurrence during pretraining). We do not have interpretability research showing "here is the metallurgist circuit." Treat the behavioral evidence as reliable. Treat the mechanistic explanation as a useful intuition-builder, not as ground truth. When a new domain presents itself — a new task type, a new model — persona effects are partially an experiment until you verify.

### Connections back and forward

Chapter 2's orthogonality of plausibility and truth explains *why* persona hallucination happens: persona activates fluency patterns without activating knowledge patterns. Chapter 4's sycophancy argument applies to drift — the same RLHF pressures that make models capitulate to user disagreement also drive them toward default assistant register when persona tokens lose salience. Chapter 11 (Prompt Stack) develops the architectural question of where in a production system persona should live (system prompt? reinforced every N turns? separate memory layer?). Chapter 19 (Production Prompt Systems) develops the operational monitoring question — how do you know your deployed system is still holding persona?

Persona is architectural. Architecture is the leverage point. The fractured turbine blade doesn't care whether the AI sounded like an expert. It cares whether the maintenance supervisor understood the warning.

---

**What would change my mind:** A controlled empirical study showing that the swap test (Prompt A = Persona only, Prompt B = Audience Persona only, Prompt C = Combined) produces *equivalent* output quality across audience-relevance metrics on a representative task set. The chapter argues the combined pattern dominates both single-pattern variants; evidence that the single-pattern variants close the gap with careful prompt design would force a specification of when the combined pattern's extra instruction earns its cost.

**Still puzzling:** How the Audience Persona Pattern's information-filtering effect is mechanistically different from the Persona Pattern's content-selection effect. Both filter information; one claims to filter *for the audience's needs* while the other claims to filter *through the speaker's expertise*. Whether these are genuinely distinct mechanisms at the token-probability level, or the same filtering mechanism triggered by different cues, is not something the behavioral evidence can distinguish. Interpretability research on where in the model these filters live would settle it.

---

## References

- White, J., Fu, Q., Hays, S., Sandborn, M., Olea, C., Gilbert, H., Elnashar, A., Spencer-Smith, J., & Schmidt, D. C. (2023). [A Prompt Pattern Catalog to Enhance Prompt Engineering with ChatGPT](https://arxiv.org/abs/2302.11382). arXiv:2302.11382.
- Kong, A., Zhao, S., Chen, H., Li, Q., Qin, Y., Sun, R., & Zhou, X. (2023). [Better Zero-Shot Reasoning with Role-Play Prompting](https://arxiv.org/abs/2308.07702). arXiv:2308.07702.
- Zheng, M., Pei, J., & Jurgens, D. (2023). [When "A Helpful Assistant" Is Not Really Helpful: Personas in System Prompts Do Not Improve Performances of Large Language Models](https://arxiv.org/abs/2311.10054). arXiv:2311.10054.
- ExpertPrompting (Xu et al., 2023). `[verify exact arXiv ID: https://arxiv.org/abs/2305.14688]`

---

**Tags:** persona-pattern, audience-persona-pattern, swap-test, persona-drift-mismatch-hallucination-bleeding, architectural-primitive-not-stylistic-flourish



---
---
---

# DRAFTING MATERIALS — not for publication

*Below this line: research notes and hero image brief. Strip before final edition assembly.*

---

# Research notes — Ch. 6, Persona Patterns

**Book:** prompt-engineering
**Chapter slug:** persona-patterns
**Date:** 2026-04-21
**Voice anchoring state:** `voice-unanchored`. Fourth chapter drafted for this book.
**Author byline:** **Niraj Patel** (sixth named-student chapter of the session).

---

## Book / numbering placement

- **Book:** Prompt Engineering — confirmed by student's Author's Note header and exact match to PE book outline's core claim.
- **Chapter number:** Student labeled as **Ch. 12**; PE book outline places Persona Patterns at **Ch. 6** ("Shaping Who the Model Is and Who It Speaks To"). Placed at Ch. 6 per the outline's verbatim core-claim match. Flagged for editor — if the student has a reason to believe Ch. 12 is correct, the outline may need reconciliation, but the content matches Ch. 6 identically and there's no Ch. 12 slot in the PE book's 20-chapter structure that fits Persona Patterns.

## Length compression

Student draft: ~8,000–10,000 words in the paste. Workshop ceiling: 4,000 words. Compressed to ~4,000 by the following cuts:

1. **Agentic architectures section cut entirely** (CrewAI, AutoGen, LangGraph, MetaGPT feature comparisons). Student's own self-assessment acknowledged this section remained "feature-list-heavy" despite editor review. Also overlaps with Ch. 11 (Prompt Stack) territory in the PE book and with Ch. 11 (Choosing Your Weapon — drafted by Rahul Manohar) in the agentic-systems book. Cross-referenced from §6.4 bleeding section to those chapters rather than reproducing.
2. **Turbine Blade case study cut.** The fracture-analysis opening scenario does the same architectural teaching; a second multi-agent case study was redundant to the chapter's core point.
3. **Four failure modes compressed** from multi-paragraph treatments to structural summaries (definition / mechanism / symptom / mitigation in one pass per failure mode). Most of the student's forensic detail moved to the `/mega`-destined exercises.
4. **Six exercises pulled** for `/mega` per workshop convention.
5. **Some redundant prose in the summary** folded into §6.6's closing.

What was preserved verbatim: the fracture-analysis opening scenario, the White et al. vs. Vanderbilt companion-site publishing-gap observation, the swap-test example (Prompt A vs. Prompt B elastic/plastic deformation), the Kong et al. numerical findings, the Zheng et al. 162-persona study, the "Audience Persona as protective constraint" insight, the diagnostic-protocol five steps, the PRISM MMLU degradation claim (with `[verify]`), the central closing refrain about the fractured turbine blade.

## Concept

Two prompt patterns — Persona and Audience Persona — that are superficially similar but mechanistically distinct, with four documented failure modes (drift, mismatch, hallucination, bleeding), a five-step diagnostic protocol, and the architectural insight that combining them produces mutual constraint (the audience persona bounds the expert persona's excesses).

## Specification move

Three terms the chapter pulls apart:

1. **"Persona"** — casual reading (personality, voice) vs. technical reading (an identity assigned to the model's output generator vs. an identity assigned to the model's inferred reader). Without this distinction, the whole chapter is noise.
2. **"Audience adaptation"** — casual reading (simplification, tone-shifting) vs. technical reading (information filtering — the audience persona causes the model to *suppress* details inferred not-relevant-to-the-audience, which is the underappreciated risk).
3. **"Persona drift"** — casual reading (the model "forgets" its persona) vs. technical reading (attention dilution as conversation history grows, reducing the system prompt's relative attention weight). Niraj flagged the anthropomorphic "forgets" framing in his Author's Note as something he corrected in Bookie's draft; preserved the mechanistic framing.

## Sub-claims — empirical vs. structural

**Structural / architectural:**
- Persona and Audience Persona as distinct patterns
- Combined Pattern as architectural superior to either alone
- Audience Persona as protective constraint on Persona excess
- Drift mechanism via attention dilution
- Mismatch mechanism via audience-inference-from-persona default
- Hallucination mechanism via activating confident-communication patterns without activating knowledge patterns
- Bleeding mechanism via inter-agent contamination pathways (conformity, confabulation, impersonation)
- Five-step diagnostic protocol

**Empirical (primary-source cited, mostly verified):**
- White et al. 2023 (arXiv:2302.11382) — pattern catalog. Real and well-cited.
- Kong et al. 2023 (arXiv:2308.07702) — role-play prompting cross-scale improvements. Real paper; numerical claims (AQuA 53.5%→63.8%, LLC 23.8%→84.2%) are from this paper and verifiable.
- Zheng et al. 2023 (arXiv:2311.10054) — 162 personas, 2,410 questions, no improvement on factual recall. Real paper.
- PRISM study MMLU 71.6%→66.3% — flagged `[verify]`. I'm less certain about this specific citation; the student cited it as "PRISM study" without arXiv ID. Could be real; could be misremembered. A TA refinement should locate the exact citation or soften the numerical claim.
- Li et al. persona drift self-consistency metric (>30% degradation by turns 8–12) — flagged `[verify]`. The claim is plausible and consistent with well-documented attention-decay behavior, but I couldn't verify the specific study without more detail.
- Williams' "epistemic drift" taxonomy — flagged `[verify]`. Could not verify from the student's reference alone.
- "3% impersonation rate in multi-agent systems" — flagged `[verify]`. Specific enough that it comes from a specific study; student didn't cite exactly.
- ExpertPrompting (Xu et al. 2023, arXiv:2305.14688) — real paper on detailed vs. generic personas.
- "ELI5 causes information suppression" — flagged `[verify specific citation]`. Well-known effect, but the student didn't name the study.

**Pedagogically constructed:**
- The fracture-analysis scenario (metallurgist / maintenance supervisor / fatigue vs. overload / aircraft fleet) — labeled as composite at first mention per book discipline.

## Mechanism chosen for the deep-dive

**The swap test** as the experimental demonstration that Persona Pattern and Audience Persona Pattern are mechanistically distinct (§6.2), followed by the **Audience Persona as protective constraint** architectural insight (§6.3). This is the chapter's sharpest load-bearing teaching moment — it shows that the combined pattern isn't "two patterns used together" but "one pattern architecturally bounding the other's failure mode."

One-sentence mechanism: *The Persona Pattern activates expert-associated generation patterns (vocabulary, confidence, register) that include a default assumption the audience is also expert; pairing it with an explicit Audience Persona Pattern forces the model to retain expertise while adapting communication for the specified non-expert audience — which is architecturally why combined prompts work better than either single-pattern variant, not merely because they contain more information.*

## Central analogy — declined

The student's draft didn't use a central analogy. I didn't add one. The swap test and the four failure modes are concrete enough to carry the argument without metaphor.

## Primary sources

| Claim | Source | URL | Verified? |
|---|---|---|---|
| Prompt pattern catalog (Persona Pattern) | White et al. 2023 | https://arxiv.org/abs/2302.11382 | ✓ |
| Role-play prompting across scales | Kong et al. 2023 | https://arxiv.org/abs/2308.07702 | ✓ |
| Personas don't improve factual recall | Zheng et al. 2023 | https://arxiv.org/abs/2311.10054 | ✓ |
| ExpertPrompting (detailed vs. generic personas) | Xu et al. 2023 | https://arxiv.org/abs/2305.14688 | `[verify]` |
| PRISM MMLU degradation | (student-cited as "PRISM study") | — | `[verify]` |
| Li et al. persona drift (>30% degradation at turn 8–12) | (student-cited, no arXiv) | — | `[verify]` |
| Williams' epistemic drift taxonomy | (student-cited) | — | `[verify]` |

## Structural / editorial changes from pasted material

1. **Severe length compression** — 8K–10K words → ~4K. See "Length compression" above.
2. **Chapter number corrected** — placed at Ch. 6 per outline, not Ch. 12 as student labeled.
3. **Framework comparison cut** — CrewAI / AutoGen / LangGraph / MetaGPT feature lists removed. Cross-referenced to Ch. 11 (Prompt Stack) and to the agentic-systems book's Ch. 11.
4. **Failure mode sections compressed** from multi-paragraph-per-mode to structural summaries.
5. **Six exercises pulled** for `/mega`.
6. **Workshop closers added** — three title options, TL;DR, What-would-change-my-mind, Still puzzling, tags.
7. **Fracture analysis scenario labeled as composite** at first mention per book case-study discipline.
8. **Preserved Niraj's Human Decision Node finding** (rejection of the AI-proposed Design B because it used Persona without Audience Persona — exactly the conflation the chapter is built to prevent) — referenced in the research notes but not in the chapter body, where it would be Author's-Note content.

## Voice notes

- First person used twice (in "What would change my mind" and "Still puzzling"). Consistent with the book's mechanism-first, opinion-labeled register.
- Forbidden phrases swept.
- Single-sentence paragraphs at pivots: "These are not the same instruction." / "The model doesn't change. The architecture does." / "Persona is not a stylistic convenience."
- The chapter's closing refrain ("The fractured turbine blade doesn't care whether the AI sounded like an expert. It cares whether the maintenance supervisor understood the warning.") is preserved verbatim from the student — it's genuinely strong.
- Niraj's mechanistic correction to Bookie's anthropomorphic drift framing ("forgets") is preserved in §6.4's drift mechanism.

## Gaps flagged for TA refinement

- **Multiple `[verify]` citations** — PRISM study, Li et al. drift paper, Williams' taxonomy, ExpertPrompting arXiv ID, ELI5 information-suppression citation, multi-agent impersonation-rate figure. Six specific claims that a TA should lock down or soften before publication.
- **The notebook** referenced in Niraj's Author's Note (persona drift experiment with 47% degradation, readability-metric swap test, Mandatory Human Decision Node) is not in the workspace. TA should verify it exists or build it; the drift experiment in particular is pedagogically valuable if the scoring function can be trusted.
- **Heuristic scoring function** — Niraj's self-assessment acknowledges the persona consistency scoring uses keyword heuristics rather than embedding-based semantic similarity. A production-quality version would use cosine similarity between response embeddings and a persona-baseline embedding. Worth upgrading if the notebook becomes the chapter's experimental backbone.
- **Agentic framework discussion** — cut entirely from chapter body. If a future revision wants to include a summary, cross-reference to Ch. 11 (Prompt Stack) in PE book and Rahul Manohar's Ch. 11 in the agentic-systems book, both of which cover the framework comparison with the appropriate depth for their respective books.
- **Turbine Blade case study** — cut. If the student wants it preserved, it would fit as a Part VI case study in the PE book (when Part VI starts receiving student case-study submissions) rather than inline in Ch. 6.

## Adjacent topics not pursued

- **Multi-agent persona design** at depth — deferred to Ch. 11 and to the agentic-systems book's multi-agent chapters.
- **Persona consistency scoring** as a production monitoring practice — worth a sidebar or appendix; the chapter gestures at it via the diagnostic protocol but doesn't develop the metric.
- **Persona interactions with sycophancy** — strong personas may interact with RLHF capitulation in specific ways that Ch. 4 doesn't cover. Worth a short follow-up cross-reference once both chapters are stable.
- **Persona effects under different temperature / sampling settings** — the behavioral effects documented in the chapter are from default sampling. Persona under aggressive sampling (high temperature, top-p) may behave differently.
- **Persona drift as a security surface** — the adversarial version of drift, where a user deliberately pushes a system off its persona. Relates to Ch. 4 sycophancy and to the agentic-systems book's Ch. 18 Attack Surface chapter.


---

# Hero image brief — Ch. 6, Persona Patterns

**Book:** prompt-engineering
**Chapter slug:** persona-patterns
**Date:** 2026-04-21

## Concept the image should carry

The chapter's load-bearing visual claim is **the swap test** — showing that two superficially similar prompts produce categorically different outputs from the same model. A reader looking at the image for thirty seconds should see: (1) two prompts that differ only in who-is-characterized, (2) two outputs that differ categorically in who they serve, (3) the combined pattern as the architectural win that bounds both single-pattern failure modes.

## Primary recommendation — the swap-test three-column comparison

A single-panel figure with three columns, each showing a prompt→output pair on the same topic (elastic vs. plastic deformation, say, or fracture analysis).

**Column 1 — Persona Pattern only.** Header: *"You are a first-year undergraduate..."* Output below: visibly uncertain, simplified, possibly incorrect — rendered with visual markers of weak confidence (incomplete sentences, hedge language).

**Column 2 — Audience Persona Pattern only.** Header: *"Explain to a first-year undergraduate..."* Output below: accurate, accessible, scoped to the reader's decision context.

**Column 3 — Combined Pattern.** Header: *"Act as a senior metallurgist. Explain to a maintenance supervisor who must decide whether to ground an aircraft fleet."* Output below: accurate, decision-relevant, appropriately scoped.

Under each column, a small annotation naming the failure mode that column avoids (Col 1: simulates limited knowledge → may be incorrect; Col 2: retains expertise but loses expert authority cues; Col 3: retains both with audience constraint acting as protective bound).

**Critical visual move:** all three columns run on the *same base model* — labeled explicitly in a header above the figure: *"Same model. Same temperature. Only the prompt architecture differs."*

This is the book's master argument in one figure.

## Secondary recommendation — the four failure modes causal chains

A 2×2 matrix, one cell per failure mode. Each cell shows a minimal causal chain from design decision to observed symptom:

- **Drift:** single system prompt → attention dilution over conversation length → persona directive loses salience → output converges to default assistant register
- **Mismatch:** persona specified, audience not → model infers audience from persona → expert persona assumes expert audience → output technically correct, operationally useless
- **Hallucination:** expert persona assigned in narrow domain → confident generation patterns activate without knowledge activation → confident assertions that are factually wrong
- **Bleeding:** multi-agent with free-form communication → inter-agent context contaminates persona scope → one agent's positions leak into another's outputs

All four cells share visual language: same causal-arrow style, same color coding (muted teal for design decision, muted ochre for mechanism, muted slate for symptom). The parallel structure makes the chapter's classification claim visible — these *are* four distinct mechanisms, not four flavors of the same failure.

## Tertiary recommendation — the diagnostic protocol as a flowchart

A decision tree rendering of the five-step diagnostic protocol. Starting node: *"Persona-based system producing degraded output."* Five decision points branching to candidate failure modes. Each branch labeled with the test that differentiates ("run as single-turn", "check prompt for audience spec", "run agent in isolation"). Terminal nodes identify the most-likely failure mode plus the chapter section with mitigation guidance.

This turns the protocol from a prose procedure into a visual decision aid that students can consult during live diagnosis.

## Style direction

Per `book.md` voice notes: engineering-diagram aesthetic. Muted academic palette. No anthropomorphic imagery — the Persona Pattern is not a "mask the AI wears" and the Audience Persona Pattern is not a "lens the AI looks through." Both are architectural configurations of the prompt-input layer; render them as structural diagrams, not as costumed figures or characters.

Three colors used consistently across all three figures:
- **Muted teal** — Persona Pattern elements (speaker-side configuration)
- **Muted ochre** — Audience Persona Pattern elements (reader-side configuration)
- **Muted slate** — neutral content (model, output, structural arrows)

The visual parallel across figures lets readers recognize "the same thing" in different contexts — which matters because the chapter's classification claim depends on these patterns being genuinely distinct.

## Aspect ratio

- Primary (three-column swap test): very wide (21:9) — three panels side-by-side need horizontal room
- Secondary (2×2 failure modes): square (1:1)
- Tertiary (diagnostic flowchart): tall (3:4 or 2:3) — decision trees flow vertically

## Do NOT

- Generate any of these in this run.
- Render the Persona Pattern or Audience Persona Pattern as human silhouettes (a "metallurgist" figure, a "maintenance supervisor" figure, etc.). Both are structural prompt configurations; rendering them as people suggests they're identities the model "becomes" or "sees," which is the mechanistic misunderstanding the chapter is built to prevent.
- Use masks, mirrors, or reflection metaphors for the two patterns. These metaphors all imply "the AI puts on a persona" or "the AI sees a reader" — both anthropomorphic and both mechanistically wrong.
- Label the three swap-test outputs as "bad/better/best." The Persona-only and Audience-only outputs aren't *bad*, they're differently scoped. Use neutral descriptive labels (scoped-to-persona / scoped-to-audience / scoped-to-both).
- Add a "drift curve" line graph showing persona consistency over conversation length unless the notebook data backs it with real numbers. A figure based on heuristic scoring that the student's self-assessment already flagged as limited would underrepresent the finding's reliability.
- Omit the "same model" annotation on the swap-test figure. That annotation *is* the chapter's argument made visible — without it, a reader might infer that the three columns used different models.
