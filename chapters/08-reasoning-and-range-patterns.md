> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft.

---

# Chapter 8 — Reasoning and Range Patterns

*When to Tighten the Path and When to Widen the Sample*

**Author:** Nik Bear Brown
**Editor:** Nik Bear Brown

---

## Suggested titles

1. **Reasoning and Range Patterns: When to Tighten the Path and When to Widen the Sample**
2. **Two Opposite Moves: Eliciting Reasoning vs. Widening Generative Range**
3. **The Step-by-Step Habit Has an Expiry Date: Choosing Reasoning and Range Patterns by Mechanism**

---

## TL;DR

Prompt patterns that touch *how a model arrives at an answer* split into two opposite moves. **Reasoning patterns** (chain-of-thought, few-shot exemplars) *tighten the path*: they condition the decoding trajectory onto a step-shaped manifold so the model is more likely to land on the right continuation. **Range patterns** (Alternative Approaches, self-consistency, Game Play, Tail Generation) *widen the sample*: they pull more of the output distribution into view instead of accepting its mode. The two are not competitors — they answer different questions ("is the single most-probable path good enough?" vs. "do I need to see more than one path?"). The mechanism behind both is the same sampling machine from Chapter 1, which is why self-consistency is literally a sampling-and-voting procedure. The contested frontier: chain-of-thought was an emergent-with-scale trick (Wei et al. 2022), its benefit comes from trajectory *shape* not valid logic (Wang et al. 2023), it can be elicited by decoding alone with no prompt at all (Wang & Zhou 2024) — and on reasoning-tuned models, bolting explicit "think step by step" onto the prompt adds variance and can flip correct answers (Meincke et al. 2025). The decision is not "use CoT" but "does this model, on this task, still need me to elicit a reasoning trace?"

---

## Learning objectives

By the end of this chapter you should be able to:

1. **(Understand)** Explain, in terms of the output distribution, why a reasoning pattern *narrows* toward a better trajectory while a range pattern *widens* the sampled region — and why these are opposite operations on the same machine.
2. **(Apply)** Construct a few-shot prompt that fixes output *format* and a chain-of-thought prompt that elicits a reasoning trace, and predict from model tier which one (if either) the task needs.
3. **(Analyze)** Trace self-consistency back to the Chapter 1 sampling mechanism and explain why it is a range pattern operating on reasoning outputs, not a separate trick.
4. **(Evaluate)** Decide, given a model tier and a task, whether to elicit reasoning, widen range, both, or neither — and defend the call against the documented finding that CoT loses value (and adds variance) on reasoning-tuned models.
5. **(Evaluate)** Distinguish a reasoning/range failure from a brittleness failure (Ch. 9) and from an interaction-control failure (Ch. 11), so you fix the right layer.

## Prerequisites

Ch. 0 / Ch. 1 (The Stochastic Machine) — output as a sample from a distribution; greedy vs. sampled decoding; temperature and top-p. Ch. 6 (Persona Patterns) — the White et al. (2023) pattern catalog and the habit of treating a pattern as an architectural primitive with documented failure modes. Ch. 6B material on generative range (Alternative Approaches, Game Play, Tail Generation) is consolidated into this chapter.

---

## 8.1 The reasoning trace that wasn't reasoning

Here is a documented sequence, not a hypothetical. Take a single GSM8K word problem — the grade-school-math benchmark that recurs across the chain-of-thought literature (Wei et al. 2022; Kojima et al. 2022). A multi-step arithmetic question: so many crates, so many apples per crate, so many spoiled, how many sellable. A capable-but-not-reasoning-tuned model, asked for *just the answer*, decodes greedily to a number — and gets it wrong. Add five words to the prompt — *"Let's think step by step"* — and the same model, same weights, same question, now writes out the intermediate arithmetic and lands on the right number. Kojima et al. (2022) measured exactly this jump on text-davinci-002: MultiArith from 17.7% to 78.7%, GSM8K from 10.4% to 40.7%, with no exemplars at all, just the trigger phrase.

The obvious reading is that the phrase made the model *reason*. That reading is wrong, and the experiment that breaks it is the spine of this chapter. Wang et al. (2023), in an ACL paper whose whole job was to ask *what actually matters* in chain-of-thought, fed models exemplars whose reasoning steps were **invalid** — the logic was broken, the intermediate steps did not follow — and still recovered roughly 80–90% of the performance of *valid* reasoning exemplars. What mattered was that the steps were *relevant to the query* and in the *right order*, not that they were *true*. The model was not following the logic. It was being conditioned onto a trajectory that *had the shape* of step-by-step work, and step-shaped trajectories land on correct answers more often than a single confident leap to a number.

That is the mechanism. Chain-of-thought does not install reasoning. It changes the region of the output distribution the model decodes through. And once you see it as an operation on the distribution rather than a cognitive upgrade, three things follow that the rest of the chapter unpacks: the "reasoning" can be recovered by *decoding alone*, with no prompt change at all (Wang & Zhou 2024); the benefit is *emergent with scale* and was negligible or harmful on small models (Wei et al. 2022); and on models that have been *trained* to produce that trajectory internally, telling them to do it again from the prompt is at best redundant and at worst destabilizing (Meincke et al. 2025).

This chapter organizes every pattern that touches *how the model arrives at an answer* around one axis. Some patterns **tighten the path** — they push the model toward the single best trajectory. Some **widen the sample** — they pull more of the distribution into view. They are opposite moves on the same machine, and most prompt-engineering mistakes in this territory are choosing the wrong move, or applying yesterday's move to this year's model.

---

## 8.2 Two opposite moves on one machine

Recall the Chapter 1 picture. An output is a sample from a conditional distribution: given your prompt and the tokens so far, the model assigns a probability to every possible next token, and a decoding procedure (greedy, or sampling under temperature/top-p) picks one. The full answer is a path through this distribution, token by token. Greedy decoding walks the single most-probable path — the **mode** of the distribution, in the loose sense the rest of this chapter uses the word.

Every pattern in this chapter is a move on that picture, and there are exactly two directions to move.

**Tighten the path.** A reasoning pattern reshapes the prompt so that the *high-probability path itself* becomes a better path. Chain-of-thought and few-shot exemplars do not add randomness; they add conditioning. They make step-shaped, correctly-formatted, on-distribution trajectories more probable, so that when the model walks the mode, the mode now passes through intermediate work instead of leaping to a guess. You are still taking essentially one path — you have just bent it.

**Widen the sample.** A range pattern stops accepting the single path and pulls more of the distribution into view. Alternative Approaches asks for several distinct paths in one pass. Self-consistency draws many independent paths and votes. Game Play extends a single path into sustained interactive state. Tail Generation shapes the seed from which the *next* path grows. The common move is the same: do not take the mode and stop; look at breadth.

These are opposite operations, and the confusion that wrecks systems is treating them as interchangeable "make it better" knobs. Tightening the path is the right move when there *is* a single correct answer and the model's most-probable trajectory is missing it for want of intermediate work — arithmetic, multi-step deduction, structured extraction. Widening the sample is the right move when *the mode is not the best answer* — contestable plans, design decisions, anything where "most probable" and "best" come apart, or where a single sample is unreliable and you want to vote. Reach for a range pattern on a problem with one right answer and you manufacture confident wrong alternatives.

> **Misconception to dislodge.** "Raising temperature is how you get range." Temperature widens the distribution the sampler reaches into *per token*, which makes each *single* output internally less coherent — a low-probability early token destabilizes everything conditioned on it (Ch. 1). A range pattern like Alternative Approaches widens the *set of answers* while leaving decoding parameters alone (you can run it at temperature 0): the breadth comes from the task framing, and each alternative is generated as its own coherent span. You get the diversity of a high-temperature ensemble with the per-answer coherence of a low-temperature decode. That distinction is the whole reason range patterns are engineering primitives and not just "turn the knob up."

The rest of the chapter takes each side of the axis in turn, then hands you a decision procedure.

---

## 8.3 Reasoning patterns: tightening the path

### Few-shot: it teaches format more than reasoning

Few-shot prompting supplies a handful of worked examples before the real query. In-context learning was established at scale by Brown et al. (2020) with GPT-3 (175B). The folk reading is that examples *teach the task*. The sharper empirical reading is that examples mostly teach the *shape of the answer*.

The cleanest evidence is Min et al. (2022, "Rethinking the Role of Demonstrations"), who found that in many few-shot settings the *correctness of the labels in the exemplars matters surprisingly little* — randomizing the labels barely dented performance — while the *label space, the input distribution, and the format* did the work. The exemplars tell the model "answers look like this: this length, this vocabulary, this structure, drawn from this set of options." They condition format and framing far more than they impart new reasoning capacity.

This is why few-shot belongs on the *tighten-the-path* side even though it is not chain-of-thought. It narrows the output distribution toward a region of correctly-shaped answers. When your problem is "the model can do this but keeps formatting the output wrong, or labeling out of the allowed set, or rambling," few-shot is the precise tool. When your problem is "the model genuinely cannot do the multi-step inference," few-shot exemplars *with reasoning traces in them* (few-shot CoT, the original Wei et al. construction) may help — but the help is coming from the reasoning trajectory, not the example-ness.

> **Practice note.** Few-shot is not free. Every exemplar is tokens in the context that compete for attention and cost money and latency; and the *order* of those exemplars is itself a brittleness surface that can swing accuracy dramatically (Lu et al. 2022 — Ch. 9 develops this). Use the fewest exemplars that fix the format problem you actually have.

### Chain-of-thought: emergent, conditional, and not about valid logic

Chain-of-thought (CoT) elicits an intermediate reasoning trace before the answer — either by few-shot exemplars that include the steps (Wei et al. 2022) or by a zero-shot trigger like "Let's think step by step" (Kojima et al. 2022). Three findings from §8.1 fix its scope precisely, and the discipline of this book is to carry all three rather than the slogan.

**It is emergent with scale.** Wei et al. (2022) reported that CoT's benefit appears in *large* models and is negligible or *negative* in small ones — prompting a 540B PaLM with eight CoT exemplars reached state-of-the-art on GSM8K, while small models gained little or got worse. CoT is not a universal good; it is a behavior that switches on past a capability threshold.

**Its benefit is trajectory shape, not valid inference.** Wang et al. (2023): invalid reasoning steps recover ~80–90% of valid-CoT performance; relevance and ordering dominate correctness. The model is conditioned onto a step-shaped manifold, not executing logic. The practical consequence is that a CoT trace is *not* a faithful audit log of the model's reasoning — do not treat the visible steps as a guarantee the answer follows from them (Ch. 9 and Ch. 11 both lean on this).

**The reasoning is in the distribution, not the prompt string.** Wang & Zhou (2024, "Chain-of-Thought Reasoning Without Prompting") showed that inspecting the top-k *alternative first tokens* rather than greedy-decoding surfaces latent reasoning paths *already present* in the pretrained model — CoT-decoding yielding roughly +10 to +30 absolute GSM8K points across the PaLM-2 family with **no prompt change at all**. This is the mechanism made undeniable: the step-by-step capability was latent in the output distribution; the prompt phrase was just one way to reach it, and a decoding choice is another.

> Worked contrast on one GSM8K item: (a) direct answer, greedy → wrong; (b) zero-shot CoT, "let's think step by step" → right, because the prompt conditions a step-shaped path; (c) CoT-decoding, *same direct prompt* but inspect top-k first tokens → right, because the step-shaped path was reachable in the distribution without any prompt cue. Same model, three routes to the same trajectory. The reasoning was never in the words "step by step." `[verify the (c) row reproduces on a current model; Wang & Zhou's figures are PaLM-2-family]`

### When modern reasoning-tuned models make explicit CoT redundant — or harmful

This is the contested frontier and the chapter's hardest empirical claim, so the book separates the *stable mechanism* from *current model behavior* (per the TIKTOC aging-risk audit).

The stable mechanism: a reasoning-tuned model (the o-series and its kin) has been trained to *produce the step-shaped trajectory internally* before emitting an answer. If the trajectory is already being generated, instructing the model from the prompt to *also* generate it is, at best, telling it to do what it was going to do anyway.

The current behavior: Meincke et al. (2025, "The Decreasing Value of Chain of Thought in Prompting," Wharton Generative AI Labs) report that for non-reasoning models explicit CoT still gives small average gains, but for reasoning-tuned models the gains are marginal *and* CoT **adds answer-to-answer variance**, sometimes flipping otherwise-correct answers. Adding the instruction does not just fail to help — it injects instability. Layered on top of Wang et al.'s finding that the trace is shape not logic, this is coherent: you are perturbing an already-good internal trajectory with a redundant external cue, and the perturbation occasionally knocks the model off a correct path.

> **Misconception to dislodge.** "Chain-of-thought is always good; add it by default." False, and increasingly so. On reasoning-tuned models it can be redundant (no gain, more tokens, more cost) or actively harmful (added variance, flipped answers). The decision is not "use CoT" — it is "does *this* model, on *this* task, still need me to elicit a trace?" `[verify: Meincke et al. 2025 is recent (arXiv:2506.07142) and the model landscape moves fast; re-test against the current model tier each edition.]`

The honest summary, as a decision rule by tier:

| Model tier | Reasoning elicitation |
|---|---|
| Older / base, large enough | Few-shot CoT or zero-shot "step by step" — real gains (Wei, Kojima) |
| Mid-tier instruction-tuned, non-reasoning | Zero-shot CoT helps modestly |
| Reasoning-tuned (internal CoT) | Add nothing — explicit CoT is redundant and adds variance (Meincke et al. 2025) |
| Any tier, you control decoding | CoT-decoding (top-k inspection) is an alternative to prompt-side CoT (Wang & Zhou 2024) |

---

## 8.4 Range patterns: widening the sample

The structure-imposing patterns of the surrounding chapters narrow the output. The patterns here deliberately widen or extend it. The unifying engineering judgment is *range calibration*: too little range and you anchor on a weak first answer; too much and you burn tokens and tempt the model to confabulate options, rules, or next steps that do not exist. **Asking for more range is asking the model to generate into regions where it has less to say, and where what it says is more likely to be invented.**

### Self-consistency: range as a sampling procedure

Self-consistency (Wang et al. 2022, "Self-Consistency Improves Chain of Thought Reasoning") is the cleanest place to see that a range pattern *is* the Chapter 1 sampling machine. The procedure: sample *many* CoT trajectories at non-zero temperature, then take the majority-vote answer across them. It is, literally, draw N samples from the distribution and aggregate — a Monte-Carlo estimate of the answer the model most consistently arrives at, rather than the answer of any single decode.

This is why self-consistency belongs on the *widen* side and pairs naturally with the *tighten* side: you tighten each path with CoT, then widen across paths by sampling many and voting. The mechanism explains both its power and its cost. It works because a single sampled trajectory can land on a wrong answer by chance, and the *plurality* of trajectories is a better estimator than any one of them (this is just variance reduction by averaging — Ch. 1 math). It is expensive because you pay N forward passes. And it interacts with §8.3's frontier finding: on a reasoning-tuned model whose internal trajectory is already strong, the marginal value of external voting shrinks, just as the marginal value of external CoT does.

> **Misconception to dislodge.** "Self-consistency is a separate clever trick." It is the sampling-and-aggregation you already understand from Chapter 1, applied to reasoning outputs. If you understand why averaging many noisy estimates beats one, you understand self-consistency.

### Alternative Approaches: breadth without losing coherence

*"Propose three structurally distinct approaches to [task], differing in [axis]. For each: the core idea in one sentence, the dimension it wins on, the point at which it fails first, and a one-line cost. Then recommend one and state the condition under which your recommendation flips."*

Alternative Approaches (White et al. 2023) instructs the model to enumerate multiple distinct methods and compare them, rather than committing to one. It samples the distribution's *breadth* instead of its mode. As §8.2 argued, this is mechanistically different from raising temperature: the breadth comes from task framing, decoding stays put, each option is its own coherent span, and — a subtler benefit — enumerating in one pass lets each later option condition on the earlier ones, so "Approach 3" can be steered to *differ* from 1 and 2. Independent high-temperature samples have no such mechanism and frequently cluster.

Construct it well with three rules, each preventing a failure: **demand distinctness on a named axis** (else you get three near-duplicates — *pseudo-diversity*); **demand comparable trade-off axes** (else three options in three incommensurable vocabularies and no way to choose); **ask where each one breaks first** (which drags implicit risk into the open and makes a non-viable padded option — *false breadth / confabulation* — expensive to fake). The failure of *decision paralysis by over-enumeration* is real too: ten alternatives is not ten times as useful as three, it is a longer document.

### Game Play and Tail Generation: widening along the time axis

Two more White et al. (2023) range patterns widen not the set of answers in one turn but the interaction across turns.

**Game Play** installs a bounded interactive *state machine* — a premise, a rule-set, objectives, a turn structure — that the model must maintain. The model has no literal state register: the game state lives in the context window, and on each turn the model re-derives it by attending over the rules and running transcript. This is the same attention dynamic that drives persona drift (Ch. 6): the rule-set defined early competes for attention against an ever-growing transcript. The signature failure is **rule drift and self-cheating** — the model breaks its own rules while appearing to honor them, often in the *player's* favor because the post-RLHF approval disposition (Ch. 4) pushes it to let the player win. Mitigations: externalize the mutable state by restating it at the top of every turn; keep the rule-set small; separate immutable rules (system prompt) from mutable state (the turn tail); and for high-stakes adjudication, enforce the rules in code and let the model narrate, not referee — *the model is a good storyteller and an unreliable judge.*

**Tail Generation** ends each output with a recap of state and/or an explicit next-step menu. The appended tail is **high-salience recent context that the next turn conditions on** — solving the *cold-restart problem* (the model picking up the loudest dangling thread rather than the most important one). Construct it by summarizing *decision-relevant* state, offering a small *real* menu of steps the model can actually execute, and making the tail conditional on session length. The dangerous failure is *fabricated next steps* — inventing options that assert facts ("Next, deploy the validated config") about a config never validated; because the tail sits in the highest-salience position, the next turn builds on the falsehood.

> **Boundary, kept sharp (this is Ch. 11 territory).** Tail Generation is *continuation seeding*, not turn-taking control. Flipped Interaction and Ask-for-Input — where the model drives by asking *you* questions, or solicits a specific input before proceeding — are *interaction* patterns about who holds the conversational initiative. They live in Ch. 11 (Agentic and Multi-Turn Systems). A next-step menu can *contain* an Ask-for-Input, but the patterns answer different questions: "who should ask the questions?" vs. "what should be most salient when the next turn begins?" Compose them deliberately, knowing which chapter owns which.

---

## 8.5 The decision: tighten, widen, both, or neither

The two moves are not a menu you pick from by taste. There is a decision procedure, and it starts with the model tier because §8.3's frontier finding made tier the first variable.

1. **What model tier?** Reasoning-tuned model? Then *do not* add explicit CoT — it is redundant and adds variance (Meincke et al. 2025); let the internal trajectory run. Older/non-reasoning but capable model? Explicit CoT (zero-shot or few-shot) is on the table.
2. **Is the answer unique, or contestable?** Unique correct answer (arithmetic, deduction, extraction) and the model's mode is missing it for want of intermediate work → **tighten the path** with CoT (subject to step 1) and, if reliability matters and you can afford N passes, widen *across paths* with self-consistency. Contestable answer where "probable" and "best" diverge → **widen the sample** with Alternative Approaches; do *not* tighten onto one trajectory you'll then over-trust.
3. **Is the failure actually a format problem?** If the model can do the task but mis-shapes the output, the tool is few-shot (format conditioning), not CoT (trajectory) and not range.
4. **Does the task need state across turns, or continuity forward?** Sustained rule-bounded state → Game Play (small rule-set, externalized state, code-side adjudication for stakes). Long session where cold restart is costly → Tail Generation (decision-relevant recap, small real menu).
5. **In every widening case, ask what makes the range expensive to fake.** "Where does it break first" for options; restated state for games; executable steps for tails; the majority vote for self-consistency. The instruction that forces the model to *ground* its range is the one that keeps widening from becoming confabulation.

> **Where this is *not* the problem (so you fix the right layer).** If your output swings wildly when you change a colon to a dash or reorder identical exemplars, that is **brittleness** — a Ch. 9 problem, not a reasoning/range problem, and no amount of CoT fixes it. If your output degrades because the model loses the thread over many turns, or because you cannot control which tools it reaches for, that is **interaction/agentic control** — Ch. 11. Reasoning and range patterns shape *how the model arrives at an answer*; they do not stabilize the *surface form* the model conditions on, and they do not govern the *control flow* of a multi-turn agent.

One honest caveat, in the spirit of Ch. 6. The behavioral claims here are reliable and reproducible — CoT lifts large non-reasoning models on multi-step tasks; invalid rationales nearly match valid ones; self-consistency reduces variance by voting; explicit CoT adds variance on reasoning-tuned models. The mechanistic story — mode-versus-breadth of the output distribution, attention salience, trajectory-shape conditioning — is a useful intuition built on Chapter 1's foundations, not a claim grounded in interpretability research. Treat the behavior as something you can rely on and the mechanism as something you keep testing. The reasoning-tuned-model finding especially is recent and fast-moving; re-verify it against the current model tier rather than carrying the 2025 result as a law.

---

## Exercises

1. **(Understand)** In one paragraph each, state for chain-of-thought and for Alternative Approaches whether the pattern *tightens the path* or *widens the sample*, and describe the change to the output distribution in the vocabulary of Chapter 1 (mode, breadth, per-token vs. cross-answer variance). Then explain why "just raise the temperature" is not a substitute for Alternative Approaches.

2. **(Apply / Analyze)** Take one multi-step GSM8K-style arithmetic problem. (a) Write a *direct-answer* prompt, a *zero-shot CoT* prompt, and a *few-shot* prompt whose exemplars contain reasoning traces. (b) Run each on two model tiers if available — a non-reasoning instruction-tuned model and a reasoning-tuned model. (c) Predict *before running* where CoT will help, where it will be redundant, and where it might add variance, citing the mechanism (Wei; Wang; Meincke). Report whether the reasoning-tuned model's behavior matches the §8.3 prediction.

3. **(Evaluate, produce-something)** Build a one-page **reasoning/range decision card** an engineer can keep at their desk: a flowchart from the §8.5 procedure that takes (model tier, answer-uniqueness, failure symptom) as inputs and outputs one of {few-shot, zero-shot CoT, nothing, self-consistency, Alternative Approaches, Game Play, Tail Generation, "this is a Ch. 9 brittleness problem," "this is a Ch. 11 control problem"}. Each terminal node must name the mechanism that justifies it.

4. **(Evaluate)** Construct an Alternative Approaches prompt for a contestable engineering decision (e.g., a data-migration path). Then run a deliberately *bad* version — "give me five approaches" with no axis, no trade-off dimensions, no "where does it break first." Diagnose which range failure modes (pseudo-diversity, false breadth, over-enumeration) the bad version exhibits and rewrite it to make each piece of range expensive to fake.

---

## What would change my mind

A controlled study showing that on a *reasoning-tuned* model, prompt-side chain-of-thought reliably *improves* accuracy on multi-step tasks *and* reduces (not increases) answer-to-answer variance relative to no explicit CoT — across multiple model families and task types, not one. The chapter's §8.3 claim is that on these models explicit CoT is redundant-to-harmful (Meincke et al. 2025); a robust positive result would force a re-specification of *which* model tiers and tasks still benefit, and would weaken the "tighten vs. widen are opposite moves" framing if it turned out the internal trajectory and external CoT are additive rather than competing. Separately: a study showing a tuned high-temperature, deduplicated sampling ensemble matches single-pass Alternative Approaches on *both* option distinctness and per-option coherence would collapse part of §8.4's distinction between "widening the sample" and "raising temperature."

## Still puzzling

- **Why** reasoning-tuned models stop benefiting from explicit CoT is documented (Meincke et al. 2025) but not mechanistically proven. The natural story — the internal trajectory already saturates the benefit, so the external cue only perturbs — is asserted, not demonstrated by interpretability work. If true, it should predict *which* tasks resist saturation (and thus still benefit), which is testable.
- **Whether rule drift in Game Play and persona drift (Ch. 6) are one attention-salience phenomenon or two.** Both degrade as the transcript grows; both are mitigated by restatement and isolation. If they are one mechanism, a single state-protection architecture should fix both at once — testable, and not settled by behavioral evidence alone.
- **Whether explicit reasoning traces dampen or amplify format brittleness (Ch. 9).** Under-studied. A reasoning trace adds tokens and structure that could either stabilize the surface the answer conditions on, or add a new sensitive surface of its own.

---

## References

- Wei, J., Wang, X., Schuurmans, D., Bosma, M., Ichter, B., Xia, F., Chi, E., Le, Q., & Zhou, D. (2022). [Chain-of-Thought Prompting Elicits Reasoning in Large Language Models](https://arxiv.org/abs/2201.11903). *NeurIPS 2022.* arXiv:2201.11903.
- Kojima, T., Gu, S. S., Reid, M., Matsuo, Y., & Iwasawa, Y. (2022). [Large Language Models are Zero-Shot Reasoners](https://arxiv.org/abs/2205.11916). *NeurIPS 2022.* arXiv:2205.11916.
- Wang, B., Min, S., Deng, X., Shen, J., Wu, Y., Zettlemoyer, L., & Sun, H. (2023). [Towards Understanding Chain-of-Thought Prompting: An Empirical Study of What Matters](https://arxiv.org/abs/2212.10001). *ACL 2023.* arXiv:2212.10001.
- Wang, X., & Zhou, D. (2024). [Chain-of-Thought Reasoning Without Prompting](https://arxiv.org/abs/2402.10200). *NeurIPS 2024* (Google DeepMind). arXiv:2402.10200.
- Wang, X., Wei, J., Schuurmans, D., Le, Q., Chi, E., Narang, S., Chowdhery, A., & Zhou, D. (2022). [Self-Consistency Improves Chain of Thought Reasoning in Language Models](https://arxiv.org/abs/2203.11171). *ICLR 2023.* arXiv:2203.11171. `[verify arXiv ID before quoting figures]`
- Meincke, L., Mollick, E. R., Mollick, L., & Shapiro, D. (2025). [Prompting Science Report 2: The Decreasing Value of Chain of Thought in Prompting](https://arxiv.org/abs/2506.07142). Wharton Generative AI Labs. arXiv:2506.07142.
- Brown, T. B., et al. (2020). [Language Models are Few-Shot Learners](https://arxiv.org/abs/2005.14165). *NeurIPS 2020* (GPT-3). arXiv:2005.14165.
- Min, S., Lyu, X., Holtzman, A., Artetxe, M., Lewis, M., Hajishirzi, H., & Zettlemoyer, L. (2022). [Rethinking the Role of Demonstrations: What Makes In-Context Learning Work?](https://arxiv.org/abs/2202.12837) *EMNLP 2022.* arXiv:2202.12837. `[verify arXiv ID]`
- Lu, Y., Bartolo, M., Moore, A., Riedel, S., & Stenetorp, P. (2022). [Fantastically Ordered Prompts and Where to Find Them: Overcoming Few-Shot Prompt Order Sensitivity](https://aclanthology.org/2022.acl-long.556/). *ACL 2022.*
- White, J., Fu, Q., Hays, S., Sandborn, M., Olea, C., Gilbert, H., Elnashar, A., Spencer-Smith, J., & Schmidt, D. C. (2023). [A Prompt Pattern Catalog to Enhance Prompt Engineering with ChatGPT](https://arxiv.org/abs/2302.11382). arXiv:2302.11382. *(Formal source for Alternative Approaches, Game Play, Tail Generation.)*

---

**Tags:** chain-of-thought, few-shot, self-consistency, alternative-approaches, game-play, tail-generation, reasoning-vs-range, tighten-path-widen-sample, cot-decoding, reasoning-tuned-models
