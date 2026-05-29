> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft.

---

# Chapter 6 — Persona and Audience Patterns

*Shaping Who the Model Is and Who It Speaks To*

**Author:** Nik Bear Brown
**Editor:** Nik Bear Brown

---

## Suggested titles

1. **Persona and Audience Patterns: Shaping Who the Model Is and Who It Speaks To**
2. **The Metallurgist Who Explained It Perfectly to Nobody**
3. **Two Patterns, One Commonly Conflated Distinction: Why "Who the Model Is" and "Who the Model Addresses" Are Different Instructions**

---

## TL;DR

Two prompt patterns that sound similar activate categorically different model behaviors: the **Persona Pattern** ("You are a metallurgist") steers the model's identity, vocabulary, and reasoning approach; the **Audience Persona Pattern** ("Assume I am a maintenance supervisor") steers the model's output complexity and content selection for a specified reader. Conflating the two — or using only one when the task requires both — produces predictable failures whose forensic trace runs directly back to the prompt architecture, not to the model's capability. The chapter's master move: pair an expert persona with a non-expert audience persona so the audience specification acts as a *protective constraint* that bounds the expert persona's jargon.

---

## Learning objectives

By the end of this chapter you should be able to:

1. **(Apply)** Distinguish the Persona Pattern from the Audience Persona Pattern using the "swap test," and predict how each changes a model's output on the same topic.
2. **(Apply)** Construct a combined-pattern prompt that pairs an expert persona with an explicit audience specification, including the audience's decision context.
3. **(Analyze)** Name the four documented failure modes (drift, mismatch, hallucination, bleeding) and identify which failure mode an observed system is exhibiting.
4. **(Apply)** Apply a five-step diagnostic protocol to classify a degraded persona-based system's failure and select the appropriate architectural fix.
5. **(Understand)** Recognize the Audience Persona Pattern as a *protective constraint* on expert personas — the architectural reason combined prompts work better than either pattern alone.

## Prerequisites

Ch. 1 (Stochastic Machine) — token sampling. Ch. 2 (Hallucination) — the orthogonality of plausibility and truth. Ch. 4 (Sycophancy) — the RLHF training pipeline and its consequences for model behavior. Ch. 5 (The Architect Mindset) — the working stance that a prompt is an engineered artifact assembled from named components, not a single wished-for sentence.

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

**Why (hypothesis, not confirmed mechanism).** The dominant working explanation is statistical co-occurrence during pretraining: documents written by or about metallurgists share vocabulary patterns and reasoning chains, and persona assignment makes those patterns more probable in next-token predictions. Stated mechanically: conditioning the context on persona-associated tokens shifts the probability mass of every subsequent token toward the region of the distribution those documents occupy. This is plausible. It fits the observed effects. It is not mechanistically confirmed by interpretability research. Treat the behavioral evidence as reliable; treat the mechanistic story as useful intuition, not ground truth.

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

### Misconception beat

The common misconception is that *"You are an expert X"* and *"explain this to an expert X"* are interchangeable ways of getting expert-grade output. They are not. The first changes the *speaker*; the second changes the *listener*. The first borrows an undergraduate's limitations when you address it at a novice; the second keeps the model's full competence and merely re-aims its delivery. The whole chapter turns on refusing to treat these as synonyms.

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

Mechanically, the audience clause adds a second conditioning signal that competes with the jargon-dense region the persona alone steers toward. The expert persona raises the probability of beach-marks-and-striation-spacing vocabulary; the audience clause lowers the probability of any token the specified non-expert reader could not parse. The output is sampled from the intersection — expert *content*, non-expert *register*. This is why the combined pattern is not merely two instructions stapled together; the second instruction is a bound on the first.

The fix for the fracture analysis tool is not *"You are a metallurgist"*; it is *"You are a metallurgist explaining findings to a maintenance supervisor who must decide whether to ground an aircraft fleet."* Same model. One additional phrase. Different output. That one phrase is the chapter's master-argument-in-miniature.

This is the same architect's-eye move Ch. 5 made for root prompts: a prompt is a set of named, composable constraints, and the leverage comes from adding the right constraint, not from rewording the wish.

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

**Mechanism.** The persona activates "expert-like" generation patterns (confident register, citation-heavy prose, domain vocabulary) without activating the underlying knowledge. The model produces text that sounds like expert output without factual grounding. Particularly dangerous in narrow or rapidly evolving domains where training data is sparse — the combination of confident communication style and absent knowledge is worse than either alone. Ch. 2's Fact-Check List Pattern is the architectural response on the knowledge side; the persona-level fix is to avoid highly specific expert personas in narrow domains without retrieval augmentation.

**Symptom.** Confident assertions that are factually incorrect. Fabricated citations with plausible-sounding journal names. Domain-appropriate vocabulary deployed inaccurately. The model never expresses uncertainty because the persona pattern activated confident communication style.

**Mitigation.** Avoid specific expert personas in domains without retrieval grounding. Combine persona assignment with explicit uncertainty instructions. Apply the Fact-Check List Pattern (Ch. 2) on confident outputs in narrow domains.

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

Chapter 2's orthogonality of plausibility and truth explains *why* persona hallucination happens: persona activates fluency patterns without activating knowledge patterns. Chapter 4's sycophancy argument applies to drift — the same RLHF pressures that make models capitulate to user disagreement also drive them toward default assistant register when persona tokens lose salience. Chapter 7 (Structuring and Governing Output) is the natural next move: once you have steered *who* speaks and *to whom*, you constrain the *shape* of what they say. Chapter 11 (Agentic and Multi-Turn Systems) develops the architectural question of where in a production system persona should live (system prompt? reinforced every N turns? separate memory layer?) and where persona bleeding is contained. Chapter 15 (Production) develops the operational monitoring question — how do you know your deployed system is still holding persona?

Persona is architectural. Architecture is the leverage point. The fractured turbine blade doesn't care whether the AI sounded like an expert. It cares whether the maintenance supervisor understood the warning.

---

## Exercises

1. **(Apply) The swap test, run.** Take any topic you know well. Write Prompt A (Persona Pattern: *"You are a [novice]. Explain X."*) and Prompt B (Audience Persona Pattern: *"Explain X. Assume I am a [novice]."*). Run both. In one paragraph, characterize the difference in accuracy and register, and state which instruction changed the *speaker* and which changed the *listener*.

2. **(Apply) Combine and bound.** Take the Wordsville prompt-architecture case (a content system writing explanatory copy for a mixed audience of editors and end-readers). Write a single combined-pattern prompt that (a) assigns a strong expert persona with a methodological orientation, (b) specifies an audience with a knowledge level *and* a decision context, and (c) leaves a deliberate channel for the model to flag where it had to suppress detail for the audience. Explain which clause is acting as the protective constraint.

3. **(Analyze) Diagnose three transcripts.** You are given three degraded persona-system transcripts (construct them, or use ones you have). For each, run the five-step diagnostic protocol and classify the failure as drift, mismatch, hallucination, or bleeding — naming the specific evidence (single-turn vs. multi-turn behavior, presence/absence of an audience clause, fabricated citations, cross-agent vocabulary echo) that rules competing modes in or out.

4. **(Create / Apply+) Build a protective-constraint pair.** For the "80 Days to Stay" SEC-data case, write *two* prompts: an unconstrained expert persona, and the same persona bounded by a non-expert audience persona with a decision context. Run both on the same financial-filing question. Quantify the difference with one audience-relevance metric you define in advance (e.g., fraction of jargon terms a target reader could parse, or whether the decision the audience faces is actually answerable from the output). Report whether the protective constraint earned its extra tokens.

---

## What would change my mind

A controlled empirical study showing that the swap test (Prompt A = Persona only, Prompt B = Audience Persona only, Prompt C = Combined) produces *equivalent* output quality across audience-relevance metrics on a representative task set. The chapter argues the combined pattern dominates both single-pattern variants; evidence that the single-pattern variants close the gap with careful prompt design would force a specification of when the combined pattern's extra instruction earns its cost.

---

## Still puzzling

1. How the Audience Persona Pattern's information-filtering effect is mechanistically different from the Persona Pattern's content-selection effect. Both filter information; one claims to filter *for the audience's needs* while the other claims to filter *through the speaker's expertise*. Whether these are genuinely distinct mechanisms at the token-probability level, or the same filtering mechanism triggered by different cues, is not something the behavioral evidence can distinguish. Interpretability research on where in the model these filters live would settle it.

2. Whether persona drift and persona-audience mismatch are truly separable when both are present. A mismatched-and-drifting system is suboptimal from turn 1 and worse by turn 12; it is not obvious that the diagnostic protocol's single-turn isolation test cleanly separates the two when the persona was never well-bounded to begin with.

3. Why strong, specific personas help structured reasoning but hurt factual recall. The co-occurrence hypothesis predicts both a reasoning *and* a knowledge boost; the observed dissociation (reasoning up, facts flat or down) is not what the simplest version of the story predicts.

---

## References

- White, J., Fu, Q., Hays, S., Sandborn, M., Olea, C., Gilbert, H., Elnashar, A., Spencer-Smith, J., & Schmidt, D. C. (2023). [A Prompt Pattern Catalog to Enhance Prompt Engineering with ChatGPT](https://arxiv.org/abs/2302.11382). arXiv:2302.11382.
- Kong, A., Zhao, S., Chen, H., Li, Q., Qin, Y., Sun, R., & Zhou, X. (2023). [Better Zero-Shot Reasoning with Role-Play Prompting](https://arxiv.org/abs/2308.07702). arXiv:2308.07702.
- Zheng, M., Pei, J., & Jurgens, D. (2023). [When "A Helpful Assistant" Is Not Really Helpful: Personas in System Prompts Do Not Improve Performances of Large Language Models](https://arxiv.org/abs/2311.10054). arXiv:2311.10054.
- ExpertPrompting (Xu et al., 2023). `[verify exact arXiv ID: https://arxiv.org/abs/2305.14688]`

---

**Tags:** persona-pattern, audience-persona-pattern, swap-test, persona-drift-mismatch-hallucination-bleeding, protective-constraint, architectural-primitive-not-stylistic-flourish
