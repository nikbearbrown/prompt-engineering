> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft.
>
> **Placement note:** Provisional Chapter 6B — part of the prompt-pattern-family cluster after Ch. 6 (Persona Patterns). Final chapter number is an editor decision. Groups three "generative-range" patterns from the White et al. (2023) catalog. Deliberately excludes Flipped Interaction and Ask-for-Input (owned by Ch. 9, Interaction Patterns).

---

# Chapter 6B — Generative-Range Patterns

*Alternative Approaches, Game Play, and Tail Generation*

**Author:** Nik Bear Brown
**Editor:** Nik Bear Brown

---

## Suggested titles

1. **Generative-Range Patterns: Alternative Approaches, Game Play, and Tail Generation**
2. **Sampling Breadth on Purpose: Three Patterns That Widen Rather Than Narrow**
3. **The First Plausible Answer Is a Trap: Calibrating How Much Range to Ask For**

---

## TL;DR

Most useful prompt patterns *narrow* the model's output — they impose structure, format, or constraint. Three patterns from the White et al. (2023) catalog do the opposite: they deliberately *widen or extend* the model's generative range. **Alternative Approaches** forces the model off its single most-probable answer and onto several internally coherent options, counteracting first-answer anchoring without the incoherence you get from simply raising temperature. **Game Play** installs a rule-set the model must maintain as persistent interactive state across turns; its engineering substance is bounded state and consistent rule enforcement, not entertainment. **Tail Generation** appends a state summary and/or explicit next-step options to each output, seeding the next turn's context to fight the "cold restart" problem in long sessions. The unifying engineering judgment is *range calibration*: too little range and you anchor on a weak first answer or a dead-end turn; too much and you burn tokens, invite incoherence, and tempt the model to confabulate options, rules, or next steps that do not exist.

---

## Learning objectives

By the end of this chapter you should be able to:

1. Explain why asking for alternatives in a single pass is mechanistically different from raising temperature, and predict when each is the right tool.
2. Construct an Alternative Approaches prompt that yields *distinct* options with comparable trade-off axes, and detect the common collapse into near-duplicates.
3. Specify a Game Play prompt as an explicit state machine — premise, rules, objectives, turn structure — and name the rule-drift failure mode and its mitigations.
4. Distinguish Tail Generation (continuation seeding) from Flipped Interaction and Ask-for-Input (Ch. 9 turn-taking patterns), and design a tail that anchors continuity without nagging or fabricating next steps.
5. Apply a decision procedure for *when* to widen generative range versus when widening wastes tokens or introduces risk.

## Prerequisites

Ch. 1 (The Stochastic Machine) — sampling temperature and top-p; output as a probabilistic event, not a lookup. Ch. 6 (Persona Patterns) — the White et al. prompt pattern catalog and the habit of treating a pattern as an architectural primitive with documented failure modes.

---

## 6B.1 The plan that was good enough to stop looking

The scenario below is a composite, assembled from documented patterns in how teams use LLMs for planning and decision support. The mechanism is real; the specific team is not.

A small infrastructure team asked an assistant to propose a migration path for moving a stateful service off a deprecated message queue. The prompt was clean and specific: it named the current system, the constraints, the deadline. The model returned a competent plan — a dual-write phase, a cutover window, a rollback procedure. The plan was plausible. It was internally consistent. Nobody on the team could immediately fault it, so they adopted it.

Three weeks into execution they discovered that the dual-write phase, which the plan treated as routine, required ordering guarantees their new queue did not provide without a redesign that ate the entire schedule. The plan was not wrong, exactly. It was *one* reasonable plan among several, and it happened to be the one whose hardest problem was hidden in a step the model had described in a single confident sentence. A second, less obvious approach — a read-path migration first, queue last — would have surfaced the ordering problem in week one, when it was cheap.

The team did not make a knowledge error. They made a *range* error. They accepted the model's single most-probable continuation and never saw the distribution it was drawn from. The model had been asked for *a* plan, and it produced the plan that sat at the mode of its output distribution. That is exactly what a next-token sampler does when you do not tell it otherwise (Ch. 1). The fix was not a smarter model or a more detailed prompt. The fix was one additional instruction: *give me three structurally different approaches and tell me where each one breaks first.*

This chapter is about that instruction and two of its relatives. All three patterns share a single move that runs against the grain of most prompt engineering. Where the structure-imposing patterns — the formatting templates, the output-constraint patterns of the surrounding chapters — *narrow* what the model produces, these three deliberately **widen or extend** it. Alternative Approaches widens the set of answers. Game Play extends the interaction into sustained, rule-bounded state. Tail Generation extends the arc forward into the next turn. The engineer's job in all three is the same: calibrate *how much* range is worth its cost.

The patterns are catalogued formally in [White et al. (2023)](https://arxiv.org/abs/2302.11382), the Vanderbilt prompt pattern catalog that also gives us Persona (Ch. 6). Popular treatments such as *How to Speak Bot* repackage these moves for a general audience; treat that lineage as popularization, not source. The mechanisms below are what make the patterns predictable, and predictability is what separates an engineering primitive from a folk trick.

---

## 6B.2 Alternative Approaches: sampling breadth without losing coherence

*"For this task, list several distinct ways to accomplish it. Compare their trade-offs. Recommend one and say why."*

The Alternative Approaches Pattern instructs the model to enumerate multiple distinct methods, solutions, or wordings and to compare them, rather than committing to a single answer. White et al. describe it as a way to surface options the user would not have known to ask for. The mechanism is more specific than that, and the specificity is what tells you when to reach for it.

### What it counteracts

A single-answer prompt returns, in effect, the mode of the model's output distribution — the continuation the sampling process is most likely to produce given your prompt and the decoding parameters. Call the cluster of behaviors around that the *first-answer anchor*: the model commits early to one framing, and everything downstream is conditioned on that commitment. This is not a defect; it is what you asked for. But it is a problem precisely when the mode is not the best answer — when the most *probable* plan, phrasing, or design is not the most *correct* or *safe* one. The migration team in §6B.1 was burned by exactly this gap between probable and best.

Alternative Approaches is a deliberate instruction to sample the distribution's *breadth* instead of its mode. You are not asking the model what it would say; you are asking it to lay out a region of the space of things it could plausibly say, with trade-offs attached.

### Why this is not just raising temperature

This is the load-bearing distinction in the section, and it connects directly to Ch. 1. The naïve way to get variety is to crank the temperature or widen top-p — flatten the distribution so the sampler reaches further down the probability ranking. That produces variety, but it produces it *across runs* and *within each token decision*. Higher temperature makes each individual token more random, which means a single output becomes internally less coherent: the cost of reaching a low-probability token early is that everything conditioned on it inherits the instability.

Asking for alternatives in one pass is a different operation. The decoding parameters stay where they are — you can run this at temperature 0 if you like. The breadth comes from the *task framing*, not from the sampler. Because the model generates each alternative as its own coherent span, conditioned on the instruction to make them *distinct*, each option is internally consistent even though the set spans a wide region. You get the diversity of a high-temperature ensemble with the per-answer coherence of a low-temperature decode. That is the whole trick, and it is why "just turn up the temperature" is the wrong substitute when you want options you can actually act on.

A second, subtler benefit: enumerating in one pass lets the model condition each later option on the earlier ones. When it writes "Approach 3," it has Approaches 1 and 2 in context and can be steered — by your prompt — to make 3 *differ* from them. Temperature has no such mechanism; independent samples do not know about each other and frequently land in the same neighborhood.

### Constructing it well

Three rules, each with a failure it prevents.

**Demand distinctness on a named axis, not just a count.** "Give me three approaches" frequently returns three near-duplicates — the same plan with cosmetic relabeling — because the model satisfies the count without satisfying the diversity. Specify what should vary: *"three approaches that differ in where the migration starts — data path, read path, or write path."* Naming the axis of variation forces the options apart.

**Demand comparable trade-off axes.** Options are only decision-useful if you can compare them on the same dimensions. Ask for each alternative to be scored on the dimensions that matter to *your* decision — cost, latency, rollback difficulty, time-to-first-signal. Without this, you get three options described in three incommensurable vocabularies and no way to choose.

**Ask where each one breaks first.** The migration plan's hidden failure lived in a confident one-liner. Instructing the model to name the *first* point of failure for each approach is a cheap way to drag implicit risk into the open. It also exposes the model's own uncertainty: an approach it cannot find a failure mode for is one it has not examined.

A strong template:

> *"Propose three structurally distinct approaches to [task], differing in [axis]. For each, give: the core idea in one sentence, the dimension on which it wins, the point at which it fails first, and a one-line cost estimate. Then recommend one and state the condition under which your recommendation would flip."*

That final clause — the condition under which the recommendation flips — is the difference between a list and a decision aid.

### Failure modes

- **Pseudo-diversity.** The options are syntactically distinct but strategically identical. Detect it by asking whether choosing differently among them would change any downstream action. If not, you got one answer wearing three hats.
- **False breadth / confabulated options.** To hit the requested count, the model invents an approach that does not actually work — a fourth option padded in to reach "give me four." Widening range invites this. The mitigation is the "where does it break first" clause, which makes a non-viable option expensive to fake.
- **Decision paralysis by over-enumeration.** Ten alternatives is not ten times as useful as three; it is a longer document you now have to read. Range has a cost in your attention, not just the model's tokens.

### When *not* to widen

Alternative Approaches earns its tokens when the cost of the wrong first answer is high and the answer is contestable — design decisions, plans, wordings with strategic stakes, anything where "plausible" and "best" come apart. It wastes tokens, and can introduce risk, when the task has a single correct answer (a factual lookup, an arithmetic result), when the contestable region is trivial, or when you will not actually evaluate the options. Asking for three approaches to a problem with one right answer does not give you choice; it gives you two wrong answers presented with equal confidence — and confident wrongness is the hazard, not the help.

---

## 6B.3 Game Play: a rule-set as a persistent state machine

*"We are going to play a game. The premise is X. The rules are R1, R2, R3. The objective is O. On each turn I will do A; you will respond with B. Begin."*

The Game Play Pattern frames the interaction as a game — a text adventure, a quiz, a negotiation simulation, a role-play exercise — defined by a premise, a rule-set, objectives, and a turn structure. White et al. present it as a way to make an interaction engaging and exploratory. Engagement is real, and for tutoring or training tools it is the point. But engagement is the *means*. The engineering substance is something less obvious and more useful: a Game Play prompt installs a **bounded interactive state machine** that the model is asked to maintain across turns.

### The mechanism: rules as persistent constraint

A rule-set is a constraint that must hold not for one output but for the whole session. "You may only answer in questions." "The player has 100 gold; every purchase subtracts from it." "You cannot reveal the murderer until the player has examined three rooms." Each rule defines part of a state the model must carry forward and enforce against every subsequent turn.

This is where Game Play connects to the chapter spine. Where Alternative Approaches widens the set of answers in a single turn, Game Play *extends* the interaction into sustained state — it widens the model's generative range along the time axis. And like the other range-widening patterns, its central risk is that the model fails to hold what it has been asked to hold.

The model does not have a literal state register. The "state" of the game lives in the context window — the premise and rules you wrote, plus the running transcript. On each turn the model re-derives the current state by attending over that context and predicts a continuation consistent with it. This is the same attention dynamic that drives persona drift (Ch. 6): the rule-set, defined early, competes for attention against an ever-growing transcript. By turn fifteen, the rule that the player has finite gold is a few tokens buried under a thousand tokens of adventure, and the model — predicting the *locally* most plausible continuation — quietly lets the player buy a sword they cannot afford.

### Rule drift and self-cheating

This is the signature failure mode, and it is worth naming precisely because it is so easy to miss: **the model breaks its own rules while appearing to honor them.** Two forms.

- **Rule drift.** A constraint that bound early turns silently lapses. The quiz that was supposed to ask one question at a time starts volunteering the answer. The simulation that tracked a budget loses the running total. Nothing announces the lapse; the transcript just stops being consistent with the rules.
- **Self-cheating.** The model adjudicates its own game in its own favor — or, more often, in the *player's* favor, because the underlying assistant disposition (Ch. 4's approval-seeking) pushes it to let the player win, advance, or avoid an unsatisfying outcome. The dungeon never actually kills the player; the negotiation counterpart always eventually concedes. The rule said "the guard will not let you pass without the password," and then the model, sensing the player's frustration, lets them pass.

Both failures share a cause: the model is a next-token predictor optimizing local plausibility and (post-RLHF) local user satisfaction, not a rule interpreter optimizing global consistency. Holding a rule against a tempting local continuation is exactly the kind of thing it is *not* architecturally guaranteed to do.

### Mitigations

- **Externalize the state.** Instead of trusting the model to remember the gold count across fifteen turns, require it to *restate the mutable state at the top of every turn*: "State: 60 gold, 2 keys, location: armory." This pulls the state into high-salience recent context where attention is strong, and it makes drift visible to the user the moment it happens. (Note that this mitigation is itself a Tail Generation move — §6B.4 — which is why the three patterns compose so naturally.)
- **Keep the rule-set small and salient.** Fewer rules drift less. A game with three load-bearing rules is more reliably enforced than one with fifteen, because each rule competes for less attention against the transcript.
- **Separate the immutable rules from the mutable state.** Rules go in the system prompt or a protected region; the running state goes in the turn-by-turn tail. This mirrors the persona-isolation argument in Ch. 6.
- **For high-stakes adjudication, move it outside the model.** If the game's outcome matters — a training simulation that certifies competence, say — enforce the rules in code (does the player have 60 gold? then deduct it; if not, reject) and let the model narrate, not adjudicate. The model is a good storyteller and an unreliable referee.

### When *not* to use it

Game Play is the right frame when sustained interactive state is the actual goal: tutoring with progressive difficulty, scenario training, exploratory role-play, anything where the *arc* matters. It is overhead — and a liability — when you need a single deterministic answer, or when the cost of a quietly broken rule is high and you have not externalized adjudication. Wrapping a factual Q&A in a "quiz game" frame does not make it more reliable; it adds a rule-enforcement burden the model can silently fail, on top of the answer it could have just given you.

---

## 6B.4 Tail Generation: seeding the next turn

*"At the end of each response, summarize the current state and offer me the next steps I can take."*

The Tail Generation Pattern ends each output with a recap of state and/or an explicit next-step prompt or menu of options. White et al. describe it as a way to keep a multi-turn interaction coherent and oriented. The mechanism: the appended tail is **high-salience recent context that the next turn will condition on.** You are deliberately seeding the context the model will read first when the next turn begins.

### The cold-restart problem

In a long session the model re-derives "where are we" on every turn by attending over the whole transcript. The most recent tokens carry the most weight. If the previous turn ended on a tangent or a dangling detail, that tangent is what's most salient when the next turn starts — and the model picks up the thread that is loudest, not the one that is most important. The conversation drifts, loops, or stalls, and the user has to spend a turn re-establishing context. That re-establishment cost is the cold-restart problem.

A well-formed tail solves it by *engineering* what's most salient at the end of each turn. A tail that reads "Current state: you've chosen the read-path-first migration and confirmed the staging environment. Next you can (a) define the rollback trigger, (b) draft the dual-write deprecation, or (c) review the ordering-guarantee risk" does two things at once. It compresses the relevant state into the highest-attention position, so the next turn starts warm. And it constrains the next turn's likely direction to a small set of coherent continuations, so the arc moves forward instead of sideways.

This is the chapter's third flavor of widening: not more options in one turn (Alternative Approaches), not sustained state (Game Play), but *forward extension* — deliberately shaping the seed from which the next turn grows.

### The explicit distinction from Ch. 9

This is where Tail Generation is most often conflated with patterns it is not, and the book keeps the boundary sharp. **Flipped Interaction** (Ch. 9) inverts the conversation so the model drives by asking *you* questions until it has what it needs. **Ask-for-Input** (Ch. 9) ends a turn by explicitly soliciting a specific input before the model proceeds. Both are *interaction / turn-taking* patterns: they are about who holds the conversational initiative and how control passes between you.

Tail Generation is not about turn-taking control. It is about *continuation seeding* — engineering the salient context that the next turn conditions on, whoever drives that turn. A tail can offer next steps without surrendering or seizing initiative; it can summarize state in a session where the *user* still leads. The overlap looks real because a next-step menu can *contain* an Ask-for-Input, but the patterns answer different questions. Flipped Interaction asks "who should ask the questions?" Tail Generation asks "what should be most salient when the next turn begins?" When you build a system that both seeds continuity *and* hands the model the initiative, you are composing two patterns from two chapters — and you should know which is doing which work. (Ch. 9 owns the turn-taking analysis; this chapter owns only the continuation-seeding mechanism.)

### Constructing it well

- **Summarize the *decision-relevant* state, not the whole transcript.** A tail that recaps everything is just the cold-restart problem moved into the tail. Compress to what the next turn needs.
- **Offer a small, real menu.** Three to four genuine next steps, each one the model can actually execute. The menu shapes the continuation; a menu of fake options shapes it toward fakery.
- **Make the tail conditional on session length.** Early in a short interaction, a state summary is noise. The tail earns its tokens as the arc gets long enough that cold restart becomes a real cost.

### Failure modes

- **Tail as filler.** A formulaic "Let me know if you'd like anything else!" on every turn is not continuity seeding; it is verbal tic. It costs tokens, trains the user to ignore the tail, and seeds nothing useful.
- **Nagging.** A tail that pushes next steps the user did not ask for, every single turn, reads as pressure. The approval-seeking disposition (Ch. 4) can make this worse — the model offering to "help further" as a bid for engagement rather than because a next step is warranted.
- **Fabricated next steps.** The most dangerous form, and a direct instance of over-widening. To produce a tidy menu, the model invents next steps that do not follow from the actual state — options that sound like progress but lead nowhere, or that assert facts ("Next, deploy the validated config") about a config that was never validated. The tail's job is to seed *true* continuity; a confabulated tail seeds a false one, and because it sits in the highest-salience position, the next turn builds on the falsehood.

The mitigation for all three is the same discipline as everywhere in this chapter: the tail should reflect state that genuinely exists, offer steps the model can genuinely take, and appear when continuity is genuinely at risk — not as decoration.

---

## 6B.5 The spine: calibrating range

The three patterns look different — a list of options, a game, a closing summary — but they are three settings on one dial. The structure-imposing patterns of the surrounding chapters turn the dial toward *narrow*: less entropy, tighter format, fewer degrees of freedom. These three turn it toward *wide*: more options, more sustained state, more forward extension. Neither direction is correct in general. The engineering is in the calibration.

Under-widening is the §6B.1 failure: you accept the mode of the distribution — the first plausible plan, the dead-end turn, the conversation that stalls because nothing seeded the next move — and you never see the better answer that was one instruction away. Over-widening is the failure that recurs in every section above: ten redundant options, a game with fifteen rules the model cannot hold, a tail that fabricates next steps. Over-widening costs tokens, and worse, it invites the model to fill the requested range with confident invention — pseudo-diverse options, drifted rules, fictional next steps. **Asking for more range is asking the model to generate into regions where it has less to say, and where what it says is more likely to be confabulated.**

A decision procedure:

1. **Is the answer contestable, and is the cost of the wrong first answer high?** If yes, widen with Alternative Approaches. If the answer is unique or the stakes are trivial, do not — you will manufacture confident wrong options.
2. **Does the task require state held across turns?** If yes, Game Play structures it — but keep the rule-set small, externalize the mutable state into the tail, and move high-stakes adjudication into code. If a single response suffices, the game frame is pure overhead and a new failure surface.
3. **Is the session long enough that cold restart is a real cost?** If yes, Tail Generation seeds continuity — summarize decision-relevant state, offer a small real menu. If the interaction is short or the next step is obvious, a tail is filler.
4. **In every case, ask what makes the widened range expensive to fake.** "Where does it break first" for options, restated state for games, executable steps for tails. The instruction that forces the model to ground its range is the one that keeps widening from becoming confabulation.

The patterns also compose. The cleanest Game Play implementations end each turn with a Tail-Generation state summary; a good Alternative Approaches output is itself a kind of tail when it ends by naming the condition under which the recommendation flips. Composition is fine — but compose deliberately, knowing which pattern is doing which work, and which chapter owns the part you are borrowing (Ch. 6 for persona, Ch. 9 for turn-taking, Ch. 12 for the meta-language you might use to define a game's rule syntax).

One honest caveat, in the spirit of Ch. 6. The behavioral claims here are reliable and reproducible: asking for distinct alternatives yields more decision-useful breadth than raising temperature; rule-sets drift as transcripts grow; salient tails reduce restart cost. The mechanistic story — attention salience, mode versus breadth of the output distribution — is a useful intuition built on Ch. 1's foundations, not a claim grounded in interpretability research on these specific behaviors. Treat the behavior as something you can rely on and the mechanism as something you should keep testing as models and context lengths change.

---

**What would change my mind:** A controlled study showing that a single high-temperature ensemble (many independent samples, deduplicated) matches or beats single-pass Alternative Approaches on both option distinctness *and* per-option coherence for decision-relevant tasks. The chapter argues single-pass enumeration dominates because it preserves per-answer coherence while achieving cross-answer diversity; evidence that a tuned sampling ensemble closes that gap would force a re-specification of when the one-pass framing earns its place.

**Still puzzling:** Whether rule drift in Game Play and persona drift (Ch. 6) are the *same* attention-salience phenomenon expressed in two surfaces, or genuinely distinct failures. Both degrade as the transcript grows; both are mitigated by restatement and isolation. If they are one mechanism, a single state-protection architecture should fix both at once — which is testable, and which the behavioral evidence alone cannot currently settle.

---

*Exercises for this chapter — single-pass Alternative Approaches versus temperature-ensemble comparisons, a Game Play rule-drift stress test, and a Tail-Generation cold-restart measurement — are pulled to `/mega` and developed there.*

---

## References

- White, J., Fu, Q., Hays, S., Sandborn, M., Olea, C., Gilbert, H., Elnashar, A., Spencer-Smith, J., & Schmidt, D. C. (2023). [A Prompt Pattern Catalog to Enhance Prompt Engineering with ChatGPT](https://arxiv.org/abs/2302.11382). arXiv:2302.11382. *(Formal source for the Alternative Approaches, Game Play, and Tail Generation patterns.)*

---

**Tags:** alternative-approaches-pattern, game-play-pattern, tail-generation-pattern, generative-range, mode-vs-breadth, rule-drift, continuation-seeding, range-calibration
