> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft.
>
> **Provenance note:** Drafted from the TIKTOC Ch. 5 entry (absorbing the PAST/PLFR and Constraint-Engineering material) plus standard prompt-engineering knowledge. Pantry source was thin; framework-specific empirical claims are flagged `[verify]`. Running example: Wordsville.

---

# Chapter 5 — The Architect Mindset: Structured Prompt Frameworks

*From Ad-Hoc Queries to Designed Prompt Systems — and Why Telling the Model What NOT to Do Is First-Class Engineering*

**Author:** Nik Bear Brown
**Editor:** Nik Bear Brown

---

## Suggested titles

1. **The Architect Mindset: Structured Prompt Frameworks**
2. **PAST and PLFR: Two Skeletons for a Prompt That Behaves Like a Spec**
3. **The Constraint That Sharpened the Output: Why "Do Not" Is Not Padding**

---

## TL;DR

A prompt is not a sentence you tune until it works; it is a *system* with separable parts — a **root** (the task and its frame), **constraints** (what is and is not allowed), a **persona** (who is speaking), and a **format** (the shape of the output). Two scaffolds make the parts explicit instead of tangled: **PAST** (Problem, Action, Steps, Task) structures the *input* you hand the model, and **PLFR** (Prompt, Logic, Format, Result) structures the *pipeline* from prompt to validated output. The chapter's sharpest claim is mechanistic: **negative constraints are first-class.** Telling the model what *not* to do removes probability mass from regions of the output distribution, narrows the admissible set, and lowers output entropy — which is *why* a well-constrained prompt is not just safer but more reliable. We build the whole system on the **Wordsville** prompt-architecture case, then hand persona forward to Ch. 6 as one architectural layer among several.

---

## Learning objectives

By the end of this chapter you should be able to:

1. **(Apply)** Decompose an ad-hoc query into the four architectural layers — root, constraints, persona, format — and explain what each layer controls.
2. **(Apply)** Express a task using the PAST scaffold (Problem, Action, Steps, Task) and explain how each slot reduces a specific class of failure.
3. **(Analyze)** Use the PLFR pipeline (Prompt, Logic, Format, Result) to separate prompt authoring from output validation, and identify where a system needs an external check.
4. **(Evaluate)** Justify a negative constraint mechanically — as probability-mass removal that lowers output entropy — rather than treating "do not" lines as cosmetic.
5. **(Create)** Design a full prompt system for a new task, with all four layers specified, at least three negative constraints, and a stated validation step.

## Prerequisites

Ch. 1 (Stochastic Machine) — output is sampled from a conditional distribution; the prompt *is* the conditioning. Ch. 2 (Hallucination) — fluency and truth are orthogonal. Ch. 4 (Sycophancy) — self-applied governance is weaker than external; "be helpful" hides a failure mode. Comfort with the idea of a probability distribution over tokens and the entropy of a distribution.

---

## 5.1 The prompt that worked on Tuesday and broke on Wednesday

**Wordsville** is an educational-content platform that generates illustrated vocabulary lessons for primary-school children — a target word, a child-safe definition, an example sentence, and a one-line illustration brief an artist or image model can render. The team's first prompt was the kind everyone writes first:

> *"Write a vocabulary lesson for the word 'gallop' for kids."*

On Tuesday it produced something lovely: a clean definition, a horse in a sentence, a sweet illustration brief. The team shipped it. On Wednesday, the same prompt on the word *"trial"* produced a definition that drifted into courtroom procedure, an example sentence referencing a criminal defendant, and an illustration brief featuring a judge's gavel — technically a correct sense of the word, entirely wrong for seven-year-olds. The next word, *"shoot,"* produced something the team did not even screenshot.

Nothing was wrong with the *model*. The prompt under-specified the task so badly that the model was free to sample from an enormous space of valid-but-unwanted completions. "For kids" is not a constraint; it is a vibe. The prompt named a task and then left every architectural decision — reading level, which word sense, safety boundaries, output shape — to the sampler.

This is the failure the chapter is about, and the misconception underneath it: that a prompt is a *phrasing* you polish until it works. It is not. **A prompt is a specification, and a specification has parts.** When the parts are implicit, the model fills them by sampling — and a sampler conditioned on an under-specified prompt is exactly the stochastic machine of Ch. 1, doing precisely what it should: drawing from the whole distribution you failed to narrow. The architect's job is to narrow it on purpose, layer by layer, and to know which layer is doing the narrowing.

By the end of the chapter the Wordsville prompt will be a system with named parts, and we will be able to point at the specific layer that fixes the *"trial"* failure and the specific layer that fixes the *"shoot"* failure. They are not the same layer.

---

## 5.2 Four layers: what a prompt is made of

Before the scaffolds, the anatomy. Strip any production prompt down and you find four separable concerns. Keeping them separable is the entire architect mindset — because when they are tangled into one paragraph, you cannot change one without disturbing the others, and you cannot tell which one failed.

1. **Root.** The task itself and the frame around it: *what is being produced, for what purpose, in what situation.* The root answers "what is this prompt for?" In Wordsville: *produce a vocabulary lesson for a primary-school child.* The root is necessary and almost never sufficient — the Tuesday prompt was *all* root.

2. **Constraints.** The boundaries on the output — positive (*must include an example sentence*) and, crucially, negative (*must not use any word sense involving violence, law, or adult themes*). Constraints are where most reliability lives, and §5.5 argues the negative ones are doing more work than they get credit for.

3. **Persona.** *Who is speaking* — the identity, register, and domain stance the model adopts. Wordsville might use *"You are a warm primary-school teacher."* Persona is a real architectural layer with documented effects and documented failure modes, and it is large enough to earn its own chapter. We name it here and hand it to Ch. 6.

4. **Format.** *The shape of the output* — fields, order, length, machine-readability. Wordsville needs a strict object: `{word, definition, example_sentence, illustration_brief}`. Format is what makes a prompt's output *consumable by a system* rather than just readable by a person.

A note on why the separation pays. Each layer maps to a different *kind* of conditioning on the output distribution $p(y \mid \text{prompt})$. The root selects the broad region (lessons, not recipes). Constraints carve mass out of that region (no violent senses). Persona reweights toward a stylistic sub-region (warm, simple register). Format collapses the surviving mass onto a rigid structure. They compose, and because they compose you can debug them independently: change the format without touching the safety constraints, swap the persona without re-deriving the task. A single tangled paragraph offers none of this; every edit is a global edit with unpredictable reach.

**Misconception, named.** "Persona, constraints, format — that's just a longer prompt; the model reads it all as one blob anyway." It does read it as one token stream, true. But *you* do not have to author it as one blob, and the discipline of separating the layers is what lets you find the failing one. The model's flat input does not require flat authoring — that confusion is the source of un-debuggable prompts.

---

## 5.3 PAST: a scaffold for the input

PAST is a scaffold for *the thing you hand the model.* It forces the root and part of the constraints into four named slots: **P**roblem, **A**ction, **S**teps, **T**ask. Read it as: here is the situation, here is what I want done about it, here is how to go about it, here is the precise deliverable.

- **Problem** — the situation and its stakes. *Why does this task exist?* For Wordsville: *"Children aged 6–8 are learning new vocabulary and need definitions they can actually understand; existing dictionary definitions are written for adults and confuse them."* Stating the problem does real work: it gives the model the *purpose* against which it can resolve ambiguity. The *"trial"* failure happened partly because the model had no stated purpose telling it that a courtroom sense was wrong for this reader.

- **Action** — the high-level verb. *What is the one thing to do?* *"Write one complete vocabulary lesson for a single target word."* This bounds scope: not a lesson plan, not five words, not a quiz. One lesson.

- **Steps** — the decomposition. *In what order, by what method?* *"(1) Choose the word sense most familiar to a 6–8-year-old. (2) Write a definition under 15 words using only common words. (3) Write one example sentence set in everyday child experience. (4) Write a one-line illustration brief."* Steps are where you encode *method* — and they double as a lightweight chain-of-thought scaffold (Ch. 8 develops when explicit reasoning helps). Critically, Step 1 is where the *"trial"* failure gets fixed: an explicit instruction to select the child-familiar sense.

- **Task** — the precise deliverable and its acceptance condition. *What exactly must come back, and how will you know it's right?* *"Return the four fields. The lesson is acceptable only if a 6-year-old could read the definition aloud and a parent would find the illustration brief unobjectionable."* Task is the slot most people skip and the one that most reduces the gap between "the model did something" and "the model did the thing."

Worth noticing: PAST is not magic words. It is a checklist that converts an under-specified request into a specified one by *refusing to let you leave a slot empty.* The Tuesday prompt had an Action and a thin Task and nothing else. Filling Problem and Steps is what closes the ambiguity the sampler was exploiting. `[verify: PAST as a named acronym appears in practitioner prompt-engineering material; treat the slot semantics here as the operative content rather than a specific citation]`

---

## 5.4 PLFR: a scaffold for the pipeline

PAST structures the *input*. **PLFR** structures the *pipeline* — the path from a prompt to a result you can trust: **P**rompt, **L**ogic, **F**ormat, **R**esult.

- **Prompt** — the authored input (often a PAST-structured one, plus persona and constraints). This is the layer everything else is built on.

- **Logic** — the reasoning or processing the model performs, and the place you decide *how much* reasoning to elicit and whether to expose it. For Wordsville the logic is light (sense-selection + simplification). For Mycroft's fund analysis (Ch. 4) it is heavy and worth making explicit. Logic is also where you decide whether a single call suffices or whether the task needs decomposition into multiple calls — the seam where prompt engineering becomes prompt-*system* engineering.

- **Format** — the contract on the output's shape. PLFR promotes format from "ask nicely" to "validated contract." Wordsville's format is a JSON object with four required string fields; the format layer says not just *"return JSON"* but *"these keys, these types, these length bounds."*

- **Result** — the *validated* output, and the explicit recognition that *generation and validation are different steps.* This is the PLFR move that PAST does not make: PLFR insists that something checks the Result against the Format contract and the Task's acceptance condition *before* it ships. For Wordsville: a schema validator confirms the four fields exist and the definition is under 15 words; a safety classifier (a *separate* call — Ch. 4's context-isolation logic, Ch. 7's Semantic Filter) screens the illustration brief. The `"shoot"` failure is fixed *here*, at the Result layer, by an external check the generating model cannot talk its way past — not by a better-worded prompt.

The relationship between the scaffolds: **PAST builds the Prompt slot of PLFR.** PAST is the zoom-in on input authoring; PLFR is the zoom-out to the whole input→output→validation pipeline. A small task may need only PAST. Any task whose wrong outputs are costly needs the Result discipline that PLFR makes explicit. `[verify: PLFR acronym provenance; the pipeline decomposition is the load-bearing content]`

**Misconception, named.** "If the prompt is good enough, I don't need a validation step." This is the Ch. 4 error in a new costume. The model that wrote the output is the worst judge of the output — same distribution, same blind spots. PLFR's Result layer exists precisely because no prompt makes the generator a reliable self-validator. Validation is a *different* layer, run by something else.

---

## 5.5 Negative constraints are first-class — the entropy argument

Here is the chapter's sharpest and most mechanistic claim. Practitioners treat *"don't do X"* lines as defensive padding — nice-to-haves you add after the "real" prompt. **That is backwards.** Negative constraints are among the most powerful tools you have, and there is a clean reason why, grounded in Ch. 1's picture of output as a sample from a distribution.

Recall that the model produces output by sampling tokens from a conditional distribution $p(y \mid \text{prompt})$. The *uncertainty* in that distribution — how spread out it is across possible outputs — is measured by its entropy:

$$
H(Y \mid \text{prompt}) = -\sum_{y} p(y \mid \text{prompt}) \, \log p(y \mid \text{prompt}).
$$

High entropy means the model is choosing among many plausible continuations; that is exactly the freedom that let *"trial"* wander into a courtroom. Every constraint you add changes the conditioning, and a *well-aimed* constraint **removes probability mass from a region of output space** — and removing mass from a region, when the surviving mass renormalizes onto fewer effective outcomes, lowers the entropy. Lower entropy means a *narrower admissible set*: fewer ways for the output to be wrong, more agreement across samples (which is also why constrained prompts are less brittle — Ch. 9).

Now the asymmetry that makes negative constraints *first-class* rather than redundant with positive ones. A **positive** constraint (*"use simple words"*) reweights toward a region but leaves the complement diffusely populated — "simple" is itself a wide target. A **negative** constraint (*"do not use any word sense involving violence, law, courts, or adult themes; do not use any word longer than three syllables"*) does something sharper: it **zeroes out** specific, nameable regions of the distribution. You are not nudging the model toward good outputs; you are *deleting* the bad ones you can anticipate. Deleting a region is a stronger operation than reweighting toward another, because it removes the failure *with certainty* rather than making it merely less likely — to the extent the model honors the constraint, which is why the Result layer (§5.4) still checks.

A useful intuition. Imagine the output space as a field, and the model's probability as soil heaped over it. A positive constraint piles more soil on the good patch; rain still falls everywhere else. A negative constraint *fences off and removes* the soil from the bad patches entirely; the rain that would have fallen there now falls on what remains. The second operation shapes the distribution more decisively because it acts on what you *don't* want, which is often far easier to specify precisely than what you *do*. "Don't mention violence" is crisp; "be appropriate" is not.

This is why the architect treats *what NOT to do* as a design surface, not an afterthought. For Wordsville, the negative constraints carry the safety guarantee:

> *Do not: use any word sense involving violence, weapons, law, courts, death, or adult themes. Do not use vocabulary above a 2nd-grade reading level. Do not exceed 15 words in the definition. Do not write an illustration brief depicting any person in distress.*

Each line removes a nameable failure region. Together they collapse the admissible output set to something a 6-year-old's parent would approve — *and* they make the output more consistent across the thousands of words Wordsville will process, because a lower-entropy distribution produces less sample-to-sample variation. Reliability and safety, from the same mechanism.

**One honest limit.** Constraints are conditioning, not hard guarantees; the model can violate a stated negative constraint, exactly as it can ignore any other instruction (Ch. 14 discusses why instruction-following is influential, not absolute). The entropy argument says negative constraints *strongly* reshape the distribution. It does not say they bound it to zero. That residual is why §5.4's Result layer exists — the negative constraints make violations *rare*, the external validator catches the rest. The two layers are complementary: constraints lower the rate; validation catches the remainder. [verify: a controlled measurement of output-entropy reduction under negative vs. positive constraints would make this claim empirical rather than mechanism-plus-judgment; I am not aware of a clean published number]

---

## 5.6 Assembling the Wordsville prompt system

Now put the layers and scaffolds together. The Wordsville prompt as an architected system, with each part labeled by the layer it implements:

```
[PERSONA — handed to Ch. 6]
You are a warm, patient primary-school teacher who explains words to young children.

[ROOT / PAST-Problem]
Children aged 6–8 are learning new vocabulary. Adult dictionary definitions
confuse them and sometimes expose them to inappropriate word senses.

[PAST-Action]
Write one complete vocabulary lesson for a single target word: {WORD}.

[PAST-Steps / LOGIC]
1. Choose the word sense most familiar to a 6–8-year-old.
2. Write a definition under 15 words using only common, 2nd-grade words.
3. Write one example sentence set in everyday child experience.
4. Write a one-line illustration brief suitable for a children's picture book.

[CONSTRAINTS — negative, first-class]
Do NOT use any word sense involving violence, weapons, law, courts, death,
  or adult themes.
Do NOT use vocabulary above a 2nd-grade reading level.
Do NOT exceed 15 words in the definition.
Do NOT depict any person in distress in the illustration brief.

[FORMAT]
Return ONLY a JSON object:
{ "word": str, "definition": str (<15 words),
  "example_sentence": str, "illustration_brief": str }

[PAST-Task / acceptance condition]
The lesson is acceptable only if a 6-year-old could read the definition aloud
and a parent would find the illustration brief unobjectionable.
```

And the **PLFR pipeline** around it:

- **Prompt** — the block above.
- **Logic** — single call; the four Steps are the model's reasoning scaffold.
- **Format** — schema-validated JSON.
- **Result** — a schema validator (fields present, definition length) *and* a separate-context safety classifier on the illustration brief before anything ships.

Trace the two original failures through the finished system. The *"trial"* failure — wrong word sense — is fixed at **PAST-Step 1 + the negative constraint** on law/courts: the model is told to pick the child-familiar sense and forbidden the courtroom region of output space. The *"shoot"* failure — a genuinely unsafe completion — is *reduced* by the negative constraint on violence/weapons and then *caught* at the **PLFR Result layer** by the external classifier if the constraint is ever violated. Two failures, two different layers, each pointable. That pointing-ability is the whole return on the architect mindset.

---

## 5.7 Why this is the architect mindset, and the bridge to persona

Step back. The shift this chapter asks for is from *prompt-as-phrasing* to *prompt-as-system.* The ad-hoc author tweaks words and hopes the distribution narrows; the architect names the layers, fills the scaffold slots, deletes the failure regions on purpose, and puts a validator at the exit. Same model, same task — categorically different reliability, for the same reason the book argues throughout: **architecture is the leverage point, not the model.** The Wordsville system is not smarter than the Tuesday prompt. It is *structured*, and structure is what converts a stochastic machine's freedom into engineered behavior.

Notice what each scaffold contributes. PAST stops you from under-specifying the input — its slots are a refusal to leave the task ambiguous. PLFR stops you from conflating generation with validation — its Result layer is the external check Ch. 4 argued no self-governing prompt can replace. And the negative-constraint argument reframes "do not" lines from padding to your most decisive control over the output distribution, because deleting a nameable failure region is a stronger operation than nudging toward a vague good.

One layer we named and deferred: **persona.** We slotted *"You are a warm primary-school teacher"* into the Wordsville system as one architectural layer among four, and that is exactly the right way to hold it — not as the prompt's personality, but as a *component* with a job (here, steering register toward warm and simple) and, as Ch. 6 will show, its own documented failure modes (drift, mismatch, hallucination). Persona is large enough and treacherous enough to earn a chapter of its own. We hand it forward not as decoration but as the next architectural layer to engineer with the same discipline we just applied to root, constraints, and format.

### Connections back and forward

Ch. 1's distribution view of output is the foundation of §5.5's entropy argument — constraints are conditioning, and conditioning reshapes $p(y \mid \text{prompt})$. Ch. 4's external-validation principle is the spine of PLFR's Result layer. Ch. 6 (Persona) develops the persona layer we deferred. Ch. 7 (Structuring and Governing Output) develops the Format and Result layers — Templates, Recipes, and the Semantic Filter that the Wordsville safety classifier instantiates. Ch. 8 (Reasoning) develops when the PAST-Steps / PLFR-Logic layer should elicit explicit reasoning. Ch. 9 (Brittleness) is the empirical follow-through on §5.5's reliability claim: a structured, lower-entropy prompt should test as *less brittle* across format variants — and Ch. 9 shows you how to measure it rather than assert it.

---

## Exercises

1. **(Apply)** Take this ad-hoc prompt — *"Summarize this customer review for our dashboard."* — and rewrite it as a PAST-structured prompt. Fill every slot (Problem, Action, Steps, Task) explicitly, and state for each slot which class of failure an empty slot would have allowed.

2. **(Analyze)** You are handed a working single-call prompt and asked to make it production-safe. Walk it through PLFR and identify specifically what the **Result** layer must check that the **Prompt** layer cannot guarantee. Name at least one check that must run as a *separate* call and explain why (tie to Ch. 4).

3. **(Evaluate)** A teammate says: *"Negative constraints just make the prompt longer and the model ignores half of them anyway — drop them and write a clear positive prompt instead."* Using the entropy argument of §5.5, write a rebuttal that (a) concedes the teammate's true point and (b) explains why negative constraints are still first-class. Be precise about what "removing probability mass" buys you that "reweighting toward good" does not.

4. **(Create)** Design a complete prompt system for a *new* task of your choosing (not Wordsville). Deliver: the four labeled layers (root, constraints, persona, format), at least three negative constraints each justified by the failure region it deletes, a PAST-structured input, and a one-paragraph PLFR pipeline naming the Result-layer validation. State one acceptance condition a reviewer could test against.

---

## What would change my mind

A controlled study showing that a single, carefully phrased *unstructured* prompt matches a layered PAST/PLFR system on both output reliability (variance across samples and across format variants, per Ch. 9) and safety-constraint adherence, on a representative task set — with the structured system's extra tokens conferring no measurable advantage. The chapter claims the layered architecture dominates ad-hoc phrasing for any task whose wrong outputs are costly; evidence that skilled single-paragraph prompting closes that gap would force a specification of *which* tasks justify the scaffolding's authoring cost and which do not. Separately, a measurement showing negative constraints do *not* reduce output entropy relative to matched positive constraints would undercut §5.5's central mechanism and demote negative constraints from "first-class" to "stylistic."

---

## Still puzzling

- **How much entropy does a negative constraint actually remove?** The §5.5 argument is mechanism-plus-judgment, not a measured number. A clean experiment — same task, matched positive vs. negative constraints, measure $H(Y \mid \text{prompt})$ via output-distribution sampling — would turn the claim empirical. I expect negative constraints to win on entropy reduction *per token spent*, but I do not have the number.
- **Where is the layer boundary the model actually respects?** We author root, constraints, persona, and format as separable layers, but the model sees a flat token stream. Whether the model's processing preserves anything like our layer structure — or whether a constraint and a format instruction interact in ways our clean decomposition hides — is an interpretability question the behavioral evidence cannot settle. The decomposition is load-bearing for *authoring and debugging*; whether it is load-bearing *inside the model* is open.

---

## References

- White, J., Fu, Q., Hays, S., Sandborn, M., Olea, C., Gilbert, H., Elnashar, A., Spencer-Smith, J., & Schmidt, D. C. (2023). [*A Prompt Pattern Catalog to Enhance Prompt Engineering with ChatGPT*](https://arxiv.org/abs/2302.11382). arXiv:2302.11382. *(The pattern-catalog tradition the layer decomposition draws on; Template and Output-Customization patterns inform the Format layer.)*
- Shannon, C. E. (1948). [*A Mathematical Theory of Communication*](https://ieeexplore.ieee.org/document/6773024). *Bell System Technical Journal*, 27(3), 379–423. *(Source of the entropy definition used in §5.5.)*
- PAST / PLFR scaffolds — practitioner prompt-engineering frameworks. `[verify: locate authoritative primary sources for the PAST and PLFR acronyms; the slot semantics are treated as the operative content in this draft pending citation]`

---

**Tags:** prompt-as-system, four-layer-architecture, past-scaffold, plfr-pipeline, negative-constraints-first-class, output-entropy, wordsville

---

## A note about AI

The architect mindset is the rare prompt-engineering idea the model can genuinely help you practice — because the failure it prevents (under-specification) is one the model can be made to expose.

Where the model genuinely helps: hand it your ad-hoc prompt and ask it to *list every decision the prompt leaves unspecified* — which word sense, which reading level, which output fields, which failure modes. The list is your missing PAST slots and missing constraints. The model is good at enumerating the freedom you accidentally granted it.

Where the model does damage: writing the validation for you and calling it done. If you ask the model to both generate and check Wordsville's safety, you have rebuilt the Ch. 4 failure — the generator grading its own homework. The Result layer's check has to be something the generating call cannot see its own way around.

The rule: use the model to find the holes in your specification; do not let it be the thing that fills *and* inspects them.

---

## AI Wayback Machine

**Christopher Alexander** was an architect whose *A Pattern Language* (1977) argued that good design comes from a vocabulary of reusable, named patterns — the direct intellectual ancestor of the "prompt pattern" and the layered-system mindset of this chapter.

**Run this:**

```
Who is Christopher Alexander, and how does their idea of a "pattern language" connect to the structured prompt frameworks we covered in this chapter? Keep it to three paragraphs. End with the single most surprising thing about their career or ideas.
```

→ Search **"Christopher Alexander (architect)"** on Wikipedia.

**Now make the prompt better.** Try one of these:

- Ask it to apply Alexander's notion of a pattern to a specific prompt-design decision (e.g., the negative-constraint layer).
- Add a constraint: "Answer including criticisms or limits of applying architectural pattern languages to prompt engineering."

What changes? What gets better? What gets worse?
