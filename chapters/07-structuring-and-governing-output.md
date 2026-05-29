> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft.

---

# Chapter 7 — Structuring and Governing Output

*Template, Recipe, Outline Expansion, Menu Actions — and the Semantic Filter That Polices the Exit*

**Author:** Nik Bear Brown
**Editor:** Nik Bear Brown

---

## Suggested titles

1. **Structuring and Governing Output: Four Patterns That Shape the Answer and One That Screens It**
2. **Committing to a Skeleton: How Structure Buys Reliability by Spending Tokens on Shape**
3. **Structure as Conditioning, Filtering as Governance: Why the Shape You Emit First Governs Everything After**

---

## TL;DR

Five prompt patterns from the [White et al. (2023)](https://arxiv.org/abs/2302.11382) catalog do two related jobs. Four *structure* the model's output to lower its entropy and make it reliable and machine-parseable: the **Template Pattern** supplies a fixed scaffold with placeholders; the **Recipe Pattern** demands a complete ordered step sequence; the **Outline Expansion Pattern** grows a skeleton into nested detail iteratively; the **Menu Actions Pattern** binds inputs to a fixed action set. The unifying mechanism is autoregressive conditioning — emitting a structure-bearing token early (a heading, a numbered step, a slot label) narrows the distribution every later token is sampled from, collapsing format variance. The unifying cost is one failure mode: over-structuring forces the model to *confabulate to fill an empty slot* when the requested structure outruns the available content; the universal mitigation is a legal low-entropy escape value. The fifth pattern, the **Semantic Filter**, *governs* the structured output — it narrows the admissible output set by screening produced text against criteria — and it is only as strong as where it runs: an in-prompt self-filter shares the generator's context and is weak under pressure; a separately invoked classifier with isolated context is the real check.

---

## Learning objectives

By the end of this chapter you should be able to:

1. **(Understand)** State the single unifying mechanism — early structural commitment narrows the conditional distribution over later tokens — and explain it in terms of autoregressive generation from Ch. 1.
2. **(Apply)** Distinguish the four structuring patterns by *where* in a task they reduce entropy (format, procedure, global organization, action space) rather than by surface appearance, and select among them with a four-question decision procedure.
3. **(Analyze)** Identify the shared failure mode — slot-driven confabulation — and predict which pattern is most exposed under what conditions; install the escape-hatch mitigation correctly in each.
4. **(Apply)** Impose a Semantic Filter to govern structured output, and distinguish in-prompt self-filtering from a separate-context classifier, characterizing the two-sided error budget (over-filtering vs. leakage).
5. **(Apply)** Compose structuring with governing (e.g., Outline Expansion → Template → Semantic Filter) without double-counting the structural budget, and recognize when *no* structuring pattern is the right move.

## Prerequisites

Ch. 1 (The Stochastic Machine) — token sampling, the softmax distribution, temperature and entropy. The entire mechanism here is a claim about how committed tokens reshape the conditional distribution over the *next* token, so the sampling model is load-bearing. Ch. 2 (Hallucination) — the orthogonality of plausibility and truth, which is the boundary of this chapter: structure makes output *reliable to consume*, not *reliable to believe*. Ch. 4 (Sycophancy) — context isolation, which is the spine of the Semantic Filter. Ch. 6 (Persona and Audience Patterns) — the pattern-catalog framing, and the working stance that a "pattern" is an architectural primitive with documented effects and failure modes, not a stylistic flourish.

---

## 7.1 The pipeline that ate a malformed list

The scenario below is a composite, assembled from documented failure patterns in LLM-backed data pipelines. The mechanism is real; the specific company is not.

In late 2024 a mid-sized logistics firm wired an LLM into the middle of an automated intake pipeline. Inbound emails from carriers — "we can take the Tuesday load, Chicago to Memphis, $2,400, dry van" — were passed to the model, which was asked to "extract the key details so we can book the load." The model's output flowed straight into a parser that populated a database row and triggered a booking. No human in the loop. The prompt had been tested on a few dozen examples and worked.

For the first two weeks it held. Then the failures began arriving in a shape nobody had designed for. One email got back a response that opened *"Sure! Here are the details from this carrier's offer:"* followed by a bulleted list. Another came back as a tidy paragraph. A third returned the fields, correctly, but reordered — origin and destination swapped from the order the parser expected — because the carrier had written the email destination-first. The parser, a brittle thing built around the assumption that line two was always the price, silently booked one load at the wrong rate and dropped three others into an error queue that no one was watching.

The root cause was not a model that "got worse." Run any one of those inputs in isolation and the model's extraction was substantively correct every time. The failure lived in the *gap between the model's output distribution and the parser's input expectations.* The model had been asked for "the key details" — a request with enormous output entropy: a hundred phrasings, several plausible orderings, optional preambles, variable punctuation, all reasonable completions, none of them what the rigid downstream consumer required. The engineers had treated formatting as something that would happen for free. It does not happen for free. Free-form natural language is, by construction, high-entropy output, and a deterministic parser is a low-entropy consumer. Something has to absorb the difference.

This chapter is about the patterns that absorb it on the *generation* side — by constraining what the model emits rather than repairing it afterward — and then about the one pattern that *governs* what is allowed out once it has been emitted. The fix for the logistics pipeline was not a smarter parser or a bigger model. It was a Template: a fixed scaffold, emitted first, that committed the model to one structure before it generated a single field value. The reordered-fields failure, the chatty-preamble failure, the paragraph-instead-of-list failure — all three are the same failure, and one structural commitment closes all three. We will get to *why* one commitment does that, because the mechanism generalizes to the other three patterns and to the cost they all share.

---

## 7.2 The four structuring patterns, and the one thing they have in common

The four structuring patterns were formalized by [White et al. (2023)](https://arxiv.org/abs/2302.11382) at Vanderbilt, in the same sixteen-pattern catalog — modeled on software design patterns — that gives us the Persona and Audience Persona patterns of Ch. 6. (The patterns are sometimes encountered first through popularizations such as the *How to Speak Bot* framing; treat those as on-ramps, not as the authority. The catalog paper is the source that states the patterns precisely enough to test.) Four of the catalog's patterns are not about *who* the model is or *what* it must avoid. They are about the **shape of the output**:

- **Template Pattern** — you supply a fixed output structure with placeholders, and the model fills the placeholders without altering the structure.
- **Recipe Pattern** — you state a goal and some known steps, and the model returns a complete, ordered sequence of steps, supplying what's missing and pruning what's redundant.
- **Outline Expansion Pattern** — you start from a high-level outline and the model iteratively expands each node into sub-nodes and detail.
- **Menu Actions Pattern** — you define a fixed menu of commands, and the model maps each input to one of them.

These look like four different tools. Mechanically they are one tool aimed at four different targets. **All four impose structure on the output to reduce entropy.** The reason that helps is a direct consequence of how the model generates text at all, so we have to be precise about the mechanism before we can reason about when each pattern earns its cost.

### The mechanism: structure is conditioning

From Ch. 1: an autoregressive language model generates one token at a time, and each token is sampled from a probability distribution that is conditioned on *every token already in the context* — including the tokens the model itself just emitted. The model does not plan a whole response and then write it. It writes token *t*, and that token becomes part of the context that shapes the distribution over token *t+1*. Formally, the model factors the joint probability of a sequence as

$$P(x_1, x_2, \dots, x_n) = \prod_{t=1}^{n} P(x_t \mid x_1, \dots, x_{t-1}),$$

and at each step it samples $x_t \sim P(\cdot \mid x_{<t})$. The conditioning set $x_{<t}$ includes the structural tokens you and it have already committed.

This is the entire mechanism of output-structuring patterns. Stated as a falsifiable claim:

> **Committing to structural tokens early narrows the conditional distribution over all later tokens.**

When the model has just emitted a heading like `## Price:` or a list marker like `3.`, the set of high-probability continuations is dramatically smaller than it was before that token existed. After `## Price:` the next tokens are overwhelmingly likely to be a currency figure, not a chatty preamble, not a paragraph about the carrier's reliability, not a reordering of fields. The structure-bearing token has done work: it has spent a small amount of the output budget to *collapse the variance* of everything downstream of it. In entropy terms, the conditional entropy $H(x_t \mid x_{<t})$ drops once $x_{<t}$ contains a committed label, because the mass concentrates on the label-appropriate continuations. Format variance — the hundred phrasings that sank the logistics pipeline — is exactly the variance that early structural commitment collapses.

This is why supplying the scaffold beats asking for the content and hoping the formatting comes out right. If you ask for "the key details," the model first has to *decide* on a structure (high entropy: many structures are plausible) and then fill it. If you supply the structure, the deciding is already done and committed in the context; the model only fills. You have moved the high-entropy decision out of the model's sampling loop and into your prompt, where it is fixed and deterministic.

Notice that the four patterns differ only in *what structure* they commit early and *how much* of the task that structure governs:

- The **Template** commits a flat slot-and-label scaffold and governs *format*.
- The **Recipe** commits an ordered enumeration and governs *procedure* — the sequence and completeness of steps.
- The **Outline Expansion** commits a *hierarchy* and governs *global organization* across a long output.
- The **Menu Actions** pattern commits a *closed set of legal outputs* and governs the *action space*.

Same mechanism, four scopes. Hold that spine; the rest of the chapter hangs four patterns, one shared failure mode, and one governing pattern on it.

---

## 7.3 Template Pattern: committing the format first

The Template Pattern supplies a fixed output structure with placeholders, and instructs the model to produce output that conforms to it exactly. The logistics fix was a template:

> *"Extract the load details from the email. Output using exactly this template and nothing else. Do not add commentary. Use `UNKNOWN` for any field not present in the email:*
> `ORIGIN: <city, state>`
> `DESTINATION: <city, state>`
> `RATE_USD: <number only, no symbols>`
> `EQUIPMENT: <dry van | reefer | flatbed | other>`
> `PICKUP_DATE: <YYYY-MM-DD>`*"*

Three things in that prompt are doing mechanistic work. First, the **labeled scaffold** itself: each `LABEL:` token, once the model emits it, conditions the following tokens toward exactly the field that label names, in the order the template fixes. The destination-first carrier email no longer reorders the output, because the *output* order is governed by the scaffold, not by the input's order. Second, the **value-type hints** inside the angle brackets (`number only`, `YYYY-MM-DD`, the enumerated equipment set) narrow each slot's distribution further — the `RATE_USD` slot is now conditioned toward a bare number, collapsing the `$2,400` / `2400 dollars` / `2.4k` variance. Third, the **closed enumeration** for `EQUIPMENT` is a miniature Menu Actions pattern embedded in a slot: it reduces that field to a four-way choice.

**What we observe.** Templates produce the most reliably machine-parseable output of any structuring pattern in this chapter, because they map most directly onto the consumer's expectations — you write the template to *be* the parser's grammar. This is why the strongest production use of the Template Pattern is to make the template a literal specification of a downstream schema (a JSON shape, a CSV header row, a fixed Markdown layout). The model's job collapses from "communicate the details" to "fill these slots," and filling slots is a low-entropy task.

**The failure mode lives here in its sharpest form.** A template is a set of slots that *must* be filled. If the input does not contain the information a slot demands, the model faces a conflict between two pressures: the instruction to conform to the template, and the absence of a legitimate value. Under that conflict the model will frequently **confabulate a value to satisfy the slot** — invent a pickup date, guess an equipment type, manufacture an origin city — because emitting *some* plausible token is higher-probability than violating the committed structure. This is the chapter's central cost, and the Template is its most exposed pattern, because every slot is a standing invitation to fabricate. The mitigation is visible in the example: an explicit escape value (`UNKNOWN`) gives the model a *legal* low-entropy completion for an empty slot, so it no longer has to choose between confabulation and structure violation. **A template without an escape hatch is a confabulation generator.** (Constraint and negative-instruction design more broadly is Ch. 5's territory; here the point is narrow — the escape value is what makes the slot safe.)

---

## 7.4 Recipe Pattern: committing the procedure

The Recipe Pattern asks the model for a *complete, ordered sequence of steps* to reach a stated goal, given some steps the user already knows. White et al.'s canonical phrasing is roughly: *"I am trying to achieve X. I know I need to do steps A and B. Provide a complete sequence of steps. Fill in any missing steps and identify any unnecessary steps."*

> *"I want to deploy a Python web service to a fresh Ubuntu VM behind HTTPS. I know I need to install the app dependencies and point a domain at the server. Give me the complete ordered sequence of steps from a bare VM to a live HTTPS endpoint. Fill in missing steps; flag any step that is unnecessary for this goal."*

Where the Template governs *format*, the Recipe governs *procedure*: the unit of structure is the ordered step, and the entropy it collapses is the entropy of *which steps, in what order*. The mechanism is the same conditioning argument applied to a sequence. Once the model has emitted `1. Provision the VM and create a non-root user`, the distribution over step 2 is conditioned on step 1 having happened — the ordered list is a chain the model must keep internally consistent, and each committed step narrows the plausible successors. This is why a Recipe surfaces *missing* steps that a free-form "how do I deploy this?" answer routinely skips: the explicit enumeration forces the model to make the decomposition visible, and a gap in a numbered chain is more conspicuous (to the model's own next-token prediction, and to you) than a gap in prose. The instruction to *prune* redundant steps does the converse — it gives the model license to emit a "this step is unnecessary because…" token rather than padding the chain.

**What we observe.** The Recipe is strongest exactly where the failure of unstructured procedural output is "silent step-skipping" — the model gives you four of the seven things you needed and the four it gave you were correct, so nothing looks wrong until step five fails in the real world. Forcing the complete ordered sequence converts a silent omission into a visible one.

**The failure mode, in its procedural form.** The Recipe's version of slot-confabulation is the **fabricated step**: asked for a *complete* sequence, the model may invent steps that don't belong, or assert ordering constraints that aren't real, because "complete and ordered" is the structure it committed to and an under-determined procedure still has to be filled out to satisfy it. The Recipe is somewhat *less* exposed to confabulation than the Template, because a step list does not have a fixed number of slots that all demand filling — the model can legitimately produce a short recipe. But the pressure is still there whenever the goal is vague or the domain is one where the model's procedural knowledge is thin. Mitigation: state the goal precisely enough that "complete" is well-defined, and explicitly license the model to mark steps as *conditional* ("only if you are using a custom domain") rather than forcing every step to read as mandatory.

---

## 7.5 Outline Expansion Pattern: committing the hierarchy

The Outline Expansion Pattern starts from a high-level outline and iteratively expands each node into sub-nodes and detail, rearranging for flow. It is the pattern for long outputs — documents, plans, curricula, reports — where the thing most likely to go wrong is not the format of any one part but the *coherence of the whole*.

> *"Produce a top-level outline (5–7 sections) for a technical onboarding guide for new backend engineers. Use only section titles, no detail. Then wait."* — and, in the next turn — *"Expand section 3 into 3–5 sub-points, titles only."* — and later — *"Now write the detail under section 3.2."*

The mechanism here is the conditioning argument plus an explicit answer to the **long-range-coherence problem** introduced by autoregressive generation. A model generating a 4,000-word document in one pass must keep the global structure coherent while every token is sampled from a distribution dominated by *local* recent context. Over a long generation, the early organizational commitments lose salience in the attention budget (the same salience-decay effect Ch. 6 names for persona drift), and the document wanders — sections overlap, the promised structure quietly dissolves, the conclusion answers a question the introduction didn't ask.

Outline Expansion attacks this by **separating the level that carries global structure from the level that carries local detail.** The skeleton — the outline — is short. It fits comfortably in context and stays salient. It carries the global coherence. Each expansion step then operates in a *small* local context (expand *this* node), where the model's strength at local fluency is exactly what you want and where long-range drift has no room to accumulate. You are not asking the model to hold a whole document coherent in one pass; you are asking it to hold a short skeleton coherent and then fill leaves one at a time, with the skeleton always in view. Hierarchical generation manages the long-range problem by *demoting* it: global coherence becomes a property of a short, persistent artifact rather than an emergent hope across thousands of tokens.

**What we observe.** Outline Expansion produces long documents with markedly better structural integrity than single-pass generation, and it has an operational bonus: because expansion is iterative, you can correct the skeleton *before* paying for the detail, which is the cheapest possible point to catch a structural mistake. (This iterative, turn-by-turn rhythm is adjacent to the interaction patterns of Ch. 11, but the move here is specifically *hierarchical decomposition of one output*, not handing conversational control to the model.)

**The failure mode, hierarchically.** Outline Expansion's confabulation risk is the **over-expanded branch**: a node that genuinely warrants two sentences gets expanded into five sub-points because the pattern's rhythm is "expand each node," and the model dutifully manufactures filler to populate a branch the content doesn't support. It is the slot-filling failure again, one level up — the empty slot is now an outline node with nothing real under it. The mitigation is to make expansion *content-driven, not uniform*: instruct the model that nodes may legitimately stay shallow, and review the skeleton for nodes that exist only because the outline looked lopsided without them.

---

## 7.6 Menu Actions Pattern: committing the action space

The Menu Actions Pattern defines a fixed menu of commands the user can invoke, and instructs the model to map each input to exactly one of them. It is the pattern for *bounded interactive systems* — a support bot, a command interface, a triage front-end — where the danger is not malformed output but *out-of-scope* output: the model helpfully doing something it was never supposed to do.

> *"You operate a document system with exactly these actions:*
> `CREATE <title>` — start a new document
> `APPEND <id> <text>` — add text to a document
> `SUMMARIZE <id>` — return a summary
> `LIST` — list all document IDs
> *For each user message, respond with exactly one action in the above syntax, or with `UNSUPPORTED: <reason>` if the request maps to no action. Take no other action and add no commentary."*

The three structuring patterns so far constrain how the model *expresses* an answer. Menu Actions constrains *what answers are even legal*. The mechanism is still conditioning, but the committed structure is a **closed set of permissible outputs**, and the entropy it collapses is the entropy of the action space itself. By emitting the menu into the context and demanding that every response be a member of it, the prompt reduces the model's degrees of freedom from "any natural-language response to a user" to "one of N actions plus a defined escape." Out-of-scope behavior — the model freelancing a fifth action because the user asked nicely — drops sharply, because a response outside the menu is now a low-probability completion relative to the committed in-menu options.

**What we observe.** Menu Actions is the pattern that makes an LLM safe to put behind an interface that *acts*. When the model's output triggers real operations, an unbounded action space is an unbounded liability; a closed menu makes the set of things the system can do auditable and finite. (Defining a fully novel command grammar with its own semantics is the **Meta Language Creation** pattern of Ch. 8; Menu Actions is the narrower case where the actions are a fixed, enumerated set rather than a new language.)

**The failure mode, at the boundary.** Menu Actions has the same confabulation risk, now expressed as **forced misclassification**: an input that maps to *no* menu item still has to become *some* output, and without an escape the model will jam it into the nearest action — routing a billing question to `SUMMARIZE` because the menu offered nothing better. This is slot-confabulation wearing a routing hat: the "slot" is the required single action, and an input with no true home gets a fabricated one. The mitigation is, again, the explicit escape (`UNSUPPORTED: <reason>`), which is to the Menu pattern what `UNKNOWN` is to the Template — a legal, low-entropy output for the genuinely-out-of-scope input, so the model never has to choose between misclassifying and breaking structure.

---

## 7.7 The shared cost, named once and precisely

Four patterns, four expressions of one failure mode. State it generally:

> **Over-structuring forces the model to confabulate to fill a committed structure whose slots outrun the available content.**

The structure is a promise the model made in its own context, and the autoregressive mechanism that makes structure *work* — committed tokens narrow later distributions — is the same mechanism that makes the failure *bite*: once `PICKUP_DATE:` is committed, emitting *a date* is higher-probability than emitting nothing or breaking the format, even when no date exists. The pattern that buys reliability by spending tokens on structure pays for it by manufacturing content to honor structure it can't fill.

The four expressions:

| Pattern | Structure committed | Empty-slot confabulation | Escape hatch |
|---|---|---|---|
| Template | labeled fields | invented field values | `UNKNOWN` for missing field |
| Recipe | ordered steps | fabricated / falsely-mandatory steps | "conditional / unnecessary" labels |
| Outline Expansion | hierarchy | over-expanded filler branches | permission for shallow nodes |
| Menu Actions | closed action set | forced misclassification | `UNSUPPORTED: <reason>` |

And the mitigation generalizes too. Every one of these patterns is made safe by the same move: **give the model a legal low-entropy output for the case the structure doesn't fit.** The escape hatch is not a politeness — it is the architectural component that converts the structure from a confabulation trap into a reliable scaffold, because it gives the model a high-probability *honest* completion to reach for instead of a fabricated one.

There is a second, quieter cost worth naming: structure can **suppress useful content.** A rigid template emits only its slots, so a genuinely important detail that has no slot — "the carrier mentioned the bridge on I-40 is closed" — is silently dropped, because the committed structure has no place to put it and the model's variance has been collapsed precisely to prevent off-template emission. Over-structuring trades the entropy you wanted to remove against expressiveness you may have wanted to keep. The engineering judgment is to structure exactly the part of the output whose variance hurts you, and leave a deliberate free-text channel (`NOTES: <anything else relevant>`) for the part where it doesn't.

### Misconception beat

The common misconception is that more structure is always safer. It is not. Structure is conditioning, and conditioning toward a shape the content cannot honestly fill is conditioning *toward fabrication*. The right amount of structure is the amount that covers the variance that actually hurts your consumer, plus an escape for everything else — never one slot more.

---

## 7.8 Governing the exit: the Semantic Filter

Structuring shapes the answer. It does not decide whether the shaped answer is *allowed out*. That is the job of a governing pattern, and the one this chapter needs is the **Semantic Filter Pattern** from the same White et al. catalog.

*"Filter this output to remove / flag content that meets criterion X."*

### What it does, mechanically

Where the four structuring patterns lower entropy *during* generation, the Semantic Filter *narrows the admissible output set* at or after generation. You define criteria — relevance, sensitivity, privacy, safety, appropriateness, tone — and the system evaluates produced text against them and modifies or blocks what fails (the catalog frames it as content analysis against filter criteria, applied dynamically, often with a feedback loop that re-screens revised output). Mechanically it is a constraint applied to text the generator was already willing to emit: it asks, of an output, not "what shape should this take" but "is this *allowed* to leave." A privacy filter strips identifying information; a relevance filter drops off-topic digressions; a safety filter blocks or rewrites content meeting a harm criterion.

So the relationship to §7.2–7.7 is clean. The structuring patterns reduce the entropy of the output's *form*. The Semantic Filter reduces the *set of outputs permitted to exit* on content grounds. One makes the answer parseable; the other makes it admissible.

### In-prompt filter vs. separate classifier — the distinction is the whole point

There are two ways to implement a Semantic Filter, and the difference is the load-bearing engineering decision.

**In-prompt filtering.** You instruct the *same* model, in the *same* call, to screen its own output: *"After answering, review your response, remove any content revealing personal data, and output only the cleaned version."* Cheap and often helpful — and weak in a predictable way: the screening reasoning shares a context window with the content being screened and with whatever user pressure produced it. The judge and the defendant are the same process, with the same incentives, in the same room. A user who can talk the generator into emitting disallowed content can usually, in the same breath, talk the self-filter into passing it.

**Separate-model / classifier filtering.** You route the output through a *distinct* call — a separate classifier, or the same base model invoked with a clean context containing only the output and the criteria, not the original prompt or the conversation that produced the content. This is more robust for the same reason Ch. 4 gives for the dissenting sub-agent: **context isolation.** The filter does not see the pressure signal; it cannot be jailbroken by the conversation that jailbroke the generator, because it was never in that conversation. It evaluates the artifact, not the argument that produced it.

This maps directly onto Ch. 4's central move. Ch. 4 argued a dissenting sub-agent works only if its context is *isolated* from the approval pressure, and that the common failure is calibration drift — the dissenter's context inadvertently exposed to the pressure signal, its adversarial function silently dying while the diagram still looks correct. The Semantic Filter has the identical failure mode. An in-prompt filter is a dissenter sharing the defendant's context: it looks like governance and provides little. A separately-invoked filter with a clean context is the real thing — and it degrades the same way if you "helpfully" pass it the original prompt for context.

### The two-sided error budget

A filter is a classifier, and every classifier has two error types you trade against each other:

- **Over-filtering (false positives).** The filter blocks or mangles benign output. A privacy filter that redacts every number destroys a financial report; a safety filter tuned hot refuses legitimate medical questions. Over-filtering is the failure that *looks* safe and quietly destroys utility — and it is invisible in safety metrics, because nothing harmful got out; you only see it in the complaints about a useless product.
- **Leakage (false negatives).** The filter passes content that violates the criterion. The PII slips through in an unusual format; the harmful content is phrased so the filter does not recognize it. Leakage is the failure the filter exists to prevent, and it is the one adversarial users target directly.

You cannot minimize both at once; tightening the threshold trades leakage for over-filtering. If $\tau$ is the filter's decision threshold, the false-negative rate falls and the false-positive rate rises as $\tau$ tightens — a monotone tradeoff, the filter's own ROC curve. The engineering question is never "is the filter accurate" but "where is the threshold, given the asymmetric cost of the two errors *in this deployment*." A filter on a children's product accepts heavy over-filtering to drive leakage near zero. A filter on an internal research tool for experts accepts more leakage to preserve utility. State the asymmetry explicitly; a filter without a stated error-cost asymmetry is untuned by definition.

### When to use it

Use a Semantic Filter when there is a *definable* criterion for inadmissible output and the cost of inadmissible output justifies a second pass. Prefer a separate-context classifier over in-prompt self-filtering whenever the content is adversarially pressured (safety, jailbreak-resistance) or the filter must be auditable. Reserve in-prompt filtering for low-adversarial, convenience cases (drop off-topic content, match a format), where the shared-context weakness costs little. And note the honest limit that ties the Semantic Filter to the rest of the book: a filter governs *admissibility*, not *truth*. It can keep PII or off-topic prose from leaving; it cannot tell you the load-bearing claim inside an admissible answer is false. That is Ch. 2's orthogonality again, and the Fact-Check List's job, not the filter's.

---

## 7.9 A decision procedure

The patterns are not interchangeable, and the choice is not aesthetic. Match the pattern to *where your uncertainty lives.* Four questions for structure, then one for governance.

**Q1 — Does a downstream consumer require a specific format?** If a parser, a schema, an API, or a rigid human workflow consumes the output, the variance that hurts you is *format* variance. Use the **Template Pattern**, and make the template the consumer's grammar. Always include an escape value for missing fields and, where relevant, a free-text notes slot. This was the logistics pipeline.

**Q2 — Is the deliverable a procedure, where the danger is missing or out-of-order steps?** If the output is *how to do something* and the failure you fear is silent step-skipping, the variance that hurts you is *procedural*. Use the **Recipe Pattern**. State the goal precisely so "complete" is well-defined, and license conditional steps so the model isn't forced to present every step as mandatory.

**Q3 — Is the output long, where the danger is global incoherence?** If you are producing a document, plan, or report long enough that single-pass generation would drift, the variance that hurts you is *long-range structural* variance. Use the **Outline Expansion Pattern**. Lock the skeleton first, review it before paying for detail, and allow shallow nodes so the pattern doesn't manufacture filler.

**Q4 — Is the model driving a bounded interactive system that acts?** If the model's output triggers operations and the danger is out-of-scope behavior, the variance that hurts you is in the *action space*. Use the **Menu Actions Pattern**. Enumerate the actions, demand exactly one per input, and provide an `UNSUPPORTED` escape so off-menu inputs aren't forced into a wrong action.

**Q5 — Must some content be kept from leaving on grounds other than shape?** If, after structuring, there is content that is well-formed but *inadmissible* — PII, off-topic, unsafe, off-policy — add a **Semantic Filter**. Decide first whether the input is adversarial: if it is, run the filter as a separate call with isolated context, not as an in-prompt self-review. State the error-cost asymmetry so the threshold is tuned, not guessed.

These compose. A common production stack is **Outline Expansion → Template → Semantic Filter**: expand a skeleton to get a coherent long document, render each leaf through a fixed template so the output is machine-parseable, then screen the rendered output through a separate-context filter before it leaves. When you compose, do not double-spend the structural budget — let each pattern govern its own scope (one carries global organization, one carries local format, one governs admissibility) rather than having them fight over the same tokens.

And there is a sixth answer the procedure must allow: **none of the above.** If your uncertainty lives in *content correctness* rather than in format, procedure, organization, action space, or admissibility — if the risk is that the model is *wrong*, not that it is *shaped wrong* or *leaking* — then no pattern in this chapter helps, and a beautifully formatted, filtered template will simply deliver a confident, parseable, admissible, wrong answer. Structure reduces output entropy; the filter narrows admissibility; neither adds knowledge. (The orthogonality of plausibility and truth is Ch. 2's argument, and it is the boundary of this chapter: these patterns make output *reliable to consume*, not *reliable to believe*.) Over-structuring a task whose real problem is correctness is worse than not structuring it, because the polish raises the reader's trust without raising the truth.

---

## 7.10 Back to the pipeline

The logistics firm's failure was never a model failure. The model extracted the right details nearly every time. The failure was an *architecture* failure: a high-entropy output ("the key details") fed to a low-entropy consumer (a rigid parser), with nothing in between to absorb the mismatch. The Template Pattern absorbed it — not by making the model smarter, but by committing the output's shape before the model generated a single value, so that the destination-first email, the chatty preamble, and the paragraph-instead-of-list all became impossible completions rather than rare ones. And had any extracted field carried something the firm could not let leave — a driver's personal phone number pasted into the email body — a Semantic Filter on the rendered row, run as a separate call, would have caught it without the generator ever getting a vote.

The deeper lesson is the one the patterns share. Output structure is not decoration applied after the fact; it is *conditioning applied up front.* Because the model samples each token from a distribution shaped by the tokens already committed, the structure you put into the context early is the structure that governs everything sampled later. That is the whole reason these patterns work, and — through the empty slot the structure can't fill — the whole reason they fail. Governance is the complement: structuring shapes what the model emits; the Semantic Filter decides what is allowed out, and it is only real when the check runs somewhere the generator cannot talk its way past. The engineer who understands the mechanism spends structure exactly where output variance is the enemy, installs an honest escape for the cases the structure doesn't fit, filters on admissibility from an isolated context, and stops adding scaffold at the point where slots begin to invite fabrication. The engineer who treats structure as free formatting ships a pipeline that books a load at the wrong rate and never sees the three it dropped.

### Connections back and forward

Chapter 6's pattern-catalog framing gives this chapter its source and its stance. Chapter 5's constraint-engineering material is where the escape value and negative instructions live in full; here they appear only as the move that makes a slot safe. Chapter 2's orthogonality of plausibility and truth is the boundary of the whole chapter — neither structuring nor filtering adds knowledge — and the Fact-Check List it names is the governing pattern this chapter deliberately does *not* cover, because it governs truth, not shape or admissibility. Chapter 4's context isolation is the spine of the Semantic Filter's separate-call form. Chapter 8 (Reasoning and Range) covers the Meta Language Creation pattern, of which Menu Actions is the narrow, enumerated case. Chapter 11 (Agentic and Multi-Turn Systems) develops where structuring and filtering layers live in a production prompt stack; Chapter 15 (Production) develops how you detect a filter that has drifted into over-filtering, or a self-review step that has silently died.

---

## Exercises

1. **(Apply) Match the pattern to the uncertainty.** For each of four short scenarios — (a) extracting invoice fields for a database, (b) writing a 12-section runbook, (c) a triage bot that opens tickets, (d) a how-to for setting up TLS — name which structuring pattern fits and *which kind of variance* it collapses. For each, write the one escape-hatch clause that makes it safe.

2. **(Apply) Install the escape hatch in all four.** Take a Template, a Recipe, a Menu Actions menu, and an Outline-Expansion instruction you have written or can write. Add the correct escape to each (`UNKNOWN`, conditional-step license, `UNSUPPORTED`, shallow-node permission). Run each twice — once on input the structure fits, once on input it doesn't — and report whether the escape suppressed confabulation.

3. **(Analyze) Confabulation vs. suppression on one input.** Construct a single input where a rigid template both confabulates one slot (no real value, model invents one) and suppresses one detail (a relevant fact with no slot). Show both failures in the output, then redesign the template (escape value + `NOTES` channel) so neither occurs. Argue whether the two costs are one underlying variance–expressiveness tradeoff or two independent failures.

4. **(Apply / Create+) Compose structure with governance, with a measurement.** For the "80 Days to Stay" SEC-data case, build an **Outline Expansion → Template → Semantic Filter** stack that produces a parseable, PII-screened summary of a filing. Implement the filter twice — once in-prompt (self-review) and once as a separate isolated call — and feed both an adversarial input that pressures the system to leak a personal identifier. Report the leakage difference and state, with a defined error-cost asymmetry, where you would set the threshold for this deployment.

---

## What would change my mind

A controlled study showing that supplying a Template scaffold produces *no* lower format-variance and *no* better parse rate than a well-written free-form extraction prompt at matched token cost — i.e., that the conditioning effect is dominated by instruction-following capability rather than by early structural commitment. The chapter claims the *position* of the structural commitment (emitted into context before the content) is doing causal work; evidence that the same reliability is achievable by a purely instructional prompt with no emitted scaffold would force me to relocate the mechanism from "conditioning on committed tokens" to "instruction-following," a different and weaker claim. Symmetrically, on the governance side: evidence that a well-prompted in-prompt self-filter matches a separate-context classifier on adversarial leakage under realistic jailbreak pressure would force me to soften the context-isolation claim and specify when a separate call is not worth its cost.

---

## Still puzzling

1. Whether slot-confabulation and content-suppression are two faces of one quantity or two independent costs. Both worsen as you add structure, which suggests a single underlying variance–expressiveness tradeoff. But confabulation is the model emitting *more* than the content supports, and suppression is the model emitting *less* than the content offers, and it is not obvious these move together — a template might confabulate in one slot while suppressing in another on the same input. Token-level analysis of where the distribution is being narrowed *toward fabrication* versus *away from off-template truth* would distinguish them.

2. Whether composing three patterns (Outline → Template → Filter) compounds or merely stacks their costs. Each has its own confabulation/over-filtering risk; it is unclear whether running them in series multiplies the failure surface or whether each pattern's escape hatch contains its own failure independently.

3. Where exactly the in-prompt filter's weakness lives. Is it that the filter shares the *pressure signal* in context, or that it shares the *generator's distribution* regardless of context? If a separately invoked call of the *same base model* with clean context is robust, the weakness is the context, not the weights — but that has not been cleanly isolated in the open literature.

---

## References

- White, J., Fu, Q., Hays, S., Sandborn, M., Olea, C., Gilbert, H., Elnashar, A., Spencer-Smith, J., & Schmidt, D. C. (2023). [A Prompt Pattern Catalog to Enhance Prompt Engineering with ChatGPT](https://arxiv.org/abs/2302.11382). arXiv:2302.11382. *(The Vanderbilt pattern catalog; source for the Template, Recipe, Outline Expansion, Menu Actions, and Semantic Filter patterns. Popular treatments such as* How to Speak Bot *are downstream popularizations of this catalog.)*

---

**Tags:** template-pattern, recipe-pattern, outline-expansion-pattern, menu-actions-pattern, semantic-filter-pattern, output-structuring, output-governance, autoregressive-conditioning, slot-confabulation, context-isolation, structure-as-entropy-reduction
