> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft. Drafted to match the anatomy and voice of the model chapter (06-persona-patterns.md).
>
> **Absorption note:** This chapter develops the Fact-Check List Pattern named here and treated in depth in the provisional 6C draft (output-governing patterns). It also absorbs the "format over truth" finding (Wang et al. 2023) from research §1. Cross-references to later chapters use the TIKTOC numbering; `[verify]` flags mark claims pending source confirmation.

---

# Chapter 2 — Hallucination and the Plausibility–Truth Gap

*Why a Model Optimized to Sound Right Is Not Optimized to Be Right*

**Author:** Nik Bear Brown
**Editor:** Nik Bear Brown

---

## Suggested titles

1. **Hallucination and the Plausibility–Truth Gap**
2. **The Citation That Did Not Exist: Why Fluency and Truth Are Orthogonal Objectives**
3. **Two Axes, Not One: Separating What a Model Sounds Like From What a Model Knows**

---

## TL;DR

A language model is trained to maximize the probability of the next token given prior context. That objective optimizes **plausibility** — how likely a continuation is given the patterns in training data — not **truth** — whether the continuation corresponds to the world. These are not the same axis, and they are not even correlated in the way human communication trains you to assume. A model can be maximally fluent and maximally wrong at once, and the surface of the output gives you no handle on which you got. This chapter shows the mechanism (next-token likelihood is computed without any term for correspondence-to-fact), shows why one widely trusted fix — chain-of-thought reasoning traces — does not close the gap (the trace optimizes for the *shape* of reasoning, not its validity), and deploys the architectural response: the **Fact-Check List Pattern**, which separates a fluent answer's load-bearing verifiable claims from its connective prose so an external check can attack them one at a time. The honest limit: the model writes the checklist too, so it surfaces commitments rather than verifying them. Real reliability comes from a check the model cannot talk its way past.

---

## Learning objectives

By the end of this chapter you should be able to:

1. **(Understand)** State why next-token prediction optimizes plausibility (likelihood under the training distribution) and contains no term for truth (correspondence to the world), using the maximum-likelihood loss.
2. **(Analyze)** Diagnose why fluency and factual grounding are orthogonal objectives — not merely uncorrelated, but produced by the same machinery — and predict the conditions under which they diverge.
3. **(Analyze)** Explain the empirical "format over truth" finding (invalid chain-of-thought rationales nearly match valid ones) and why it shows a reasoning trace conditions trajectory *shape*, not logical validity.
4. **(Apply)** Deploy the Fact-Check List Pattern to convert an unfalsifiable paragraph into an enumerated, checkable artifact, and state its honest limit.
5. **(Evaluate)** Decide when a fact-check list needs an external verifier (tool, retrieval, human node) and when self-surfacing is enough.

## Prerequisites

Ch. 1 (Stochastic Machine) — token sampling; output is a sample from a distribution, not a lookup. Basic probability — conditional probability, the chain rule of probability, and the idea of a likelihood. No transformer internals required beyond Ch. 1; the loss function is introduced here, not derived.

---

## 2.1 The citation that shipped

The scenario below is a composite, drawn from documented failure patterns in research- and analyst-assistant deployments. The mechanism is real; the specific desk is not.

In late 2025, an analyst on the **Mycroft** investment-intelligence team — a desk that uses an LLM to draft first-pass company briefs — asked the assistant a routine question: *summarize the regulatory exposure in the company's most recent 10-K, and cite the relevant risk-factor language.* The system prompt was the kind that ships everywhere: *"You are a meticulous, knowledgeable financial research assistant. Always give the user a complete, well-sourced answer."*

The assistant returned three clean paragraphs. It named a specific risk factor, quoted two sentences of disclosure language in quotation marks, and gave a page reference: *"(10-K, Item 1A, p. 27)."* The prose was fluent, the structure was exactly what an analyst expects, and the quoted language sounded precisely like SEC risk-factor boilerplate — hedged, defensive, lawyerly. The analyst, on deadline, pasted the quote and the page citation into a client-facing brief.

The quote did not exist. There was a risk factor on the general topic, but the two "quoted" sentences were not in the filing; they were a fluent reconstruction of what such a disclosure *typically* says. The page number was plausible — 10-Ks do have an Item 1A around there — and wrong. The tell, in hindsight, was that the quote was *too* clean: it said exactly what the analyst's question implied it would say.

Nothing in the output's surface separated its **load-bearing factual commitments** — *this language appears in this filing, on this page* — from its connective prose. To catch the error, the analyst would have had to reverse-engineer which sentences were falsifiable and then check each against the actual document. The format actively discouraged that. The paragraph was, as written, nearly unfalsifiable at a glance.

This chapter is about why that happens — not as a bug in one model, but as a structural property of what the machine is optimized to do — and about the architectural layer that should have been there. The short version of the diagnosis: the model was not trying to be right. It was trying to be **probable**. And probable, it turns out, is a different thing from true.

---

## 2.2 Two axes that human communication taught you to conflate

Start with the misconception, because it is the one almost every new prompt engineer carries in unexamined.

**The misconception:** *a fluent, confident, well-structured answer is more likely to be correct than a halting, hedged one.* In conversation with humans, this heuristic is mostly sound. A person who explains a topic clearly, in the right register, with the right vocabulary, usually understands it — because in humans, fluency on a topic is *produced by* understanding it. The clear explanation is causal evidence of the competence behind it. You have spent your whole life calibrating on that correlation, and it is a good correlation. For humans.

For a language model it is not merely a weaker correlation. It is, on the relevant axis, **no correlation at all** — and worse, the two properties are generated by the very same machinery, so the surface cannot tell them apart. Call the two axes:

- **Plausibility** — how probable a continuation is given the patterns in the training data. This is what the model computes and optimizes.
- **Truth** — whether the continuation corresponds to the world. This is what you want and what the model does not compute.

These are **orthogonal**: knowing where an output sits on one axis tells you nothing about where it sits on the other. A true claim can be highly plausible (the model has seen it stated many times) or implausible (the truth is awkward, rare, or counterintuitive). A false claim can be highly plausible (it fits the pattern of what such answers usually say — the Mycroft quote) or implausible (gibberish). Fluency is a measure of plausibility. It is silent about truth.

> **Core claim.** A language model trained by next-token prediction optimizes the *plausibility* of its output under the training distribution. It contains no objective term for *truth*. Fluency and factual grounding are therefore orthogonal — produced by the same machinery, varying independently — and the surface form of an output carries no information about which you received. **Hallucination is not a malfunction of this process; it is the process working exactly as specified, on an input where plausibility and truth happen to point in different directions.**

Hold the word "hallucination" at arm's length for a moment. It is a misleading name — it suggests a perceptual glitch, a rare misfire, something a healthy model wouldn't do. Mechanism before name: what actually happens is that the model samples the most probable continuation, and *sometimes the most probable continuation is false*. There is no separate "hallucination mode." The same forward pass that produces a true citation produces a fabricated one. We keep the word because the field uses it, but the mechanism is just sampling from a distribution that was never shaped by truth.

---

## 2.3 Inside the objective: where truth would have to live, and doesn't

You do not need transformer internals to see this. You need the loss function — the single equation that defines what "good" means during training.

A language model is trained on a corpus of token sequences. For a sequence $x_1, x_2, \dots, x_T$, the model factorizes the probability of the whole sequence using the chain rule of probability:

$$P_\theta(x_1, \dots, x_T) = \prod_{t=1}^{T} P_\theta\!\left(x_t \mid x_1, \dots, x_{t-1}\right)$$

Each factor $P_\theta(x_t \mid x_{<t})$ is the model's predicted probability for the next token given everything before it, with $\theta$ the model's parameters. Training adjusts $\theta$ to make the observed training sequences as probable as possible — **maximum-likelihood estimation**. Equivalently, it minimizes the average negative log-likelihood, the cross-entropy loss:

$$\mathcal{L}(\theta) = -\frac{1}{T}\sum_{t=1}^{T} \log P_\theta\!\left(x_t \mid x_{<t}\right)$$

Read this equation the way Searle reads the attention equation in Ch. 3 — as a rule, and ask what it references. Every quantity in it is about **the training text**: the tokens that actually occurred, and the probability the model assigns them. There is a term for "did the model predict the token that came next in the corpus." There is **no term anywhere** for "is the statement the model is generating true of the world." Truth does not appear in the loss because truth is not in the data in a form the loss can see. The corpus contains *strings*. It does not contain a labeled column marking which strings correspond to facts. The model is optimized to reproduce the statistical regularities of the strings — including the regularity that risk factors are phrased a certain way, that citations have a certain shape, that confident answers follow confident questions.

This is the whole mechanism, and it is worth stating starkly: **a true sentence and a false-but-stylistically-identical sentence are, to the loss function, the same kind of object.** If false-but-plausible continuations were common in the training data in a given pattern, the model learned to produce them. Even where the training data is overwhelmingly true, the model interpolates and extrapolates — it generates continuations it never saw, and nothing constrains those continuations to be true, only to be *probable-looking*. The Mycroft quote is exactly this: a continuation no filing contained, assembled from the statistical shape of filings that the model had seen.

A second-order effect compounds it. Post-training alignment — the reinforcement-from-human-feedback stage developed in Ch. 4 — optimizes for *human approval* of responses, and humans approve of fluent, confident, complete answers. So the post-training objective, if anything, *rewards* plausibility further and can penalize the honest "I don't have that." We develop that pressure (sycophancy) in Ch. 4; here, note only that nothing in either training stage installs a truth term. Pretraining optimizes likelihood; alignment optimizes approval. Neither optimizes correspondence-to-fact.

**The misconception, dissolved.** Why does fluent-implies-correct work for humans and fail for models? Because in humans, fluency is *caused by* competence — you cannot fluently explain thermodynamics without knowing thermodynamics. In a language model, fluency is caused by *exposure to fluent text*, which is entirely decoupled from whether any particular generated statement is true. The model can produce the rhythm of expertise (Ch. 6's persona-hallucination failure mode is exactly this) without the substance. You inherited a heuristic calibrated on a machine — the human brain — where the two axes are bolted together. You are now operating a machine where they are not.

---

## 2.4 The fix that isn't: why a reasoning trace doesn't add a truth term

Here is where a careful reader pushes back, and should. *Fine — a bare answer optimizes plausibility. But what if I make the model show its work? Chain-of-thought prompting — "let's think step by step" — makes the model lay out intermediate reasoning before answering. If I can see the reasoning, surely I can trust the conclusion, and surely the model that reasons is reasoning toward truth?*

This is the most important misconception in the chapter, because the fix is real for *some* tasks and seductive for the wrong reasons. Chain-of-thought (CoT) genuinely raises accuracy on multi-step problems for large models — [Wei et al. (2022)](https://arxiv.org/abs/2201.11903) showed eight CoT exemplars taking a 540B-parameter model to then-state-of-the-art on grade-school math, with the benefit *emergent with scale* (small models gained little or got worse). [Kojima et al. (2022)](https://arxiv.org/abs/2205.11916) showed the bare phrase "Let's think step by step" lifting one model on a multi-step arithmetic benchmark from 17.7% to 78.7%. So CoT works. The question is *why*, and whether the why involves the model reasoning toward truth.

The decisive evidence is an ablation. [Wang et al. (2023)](https://arxiv.org/abs/2212.10001), "Towards Understanding Chain-of-Thought Prompting," fed models reasoning exemplars whose steps were **invalid** — logically wrong, but still relevant to the problem and correctly ordered. If CoT worked by getting the model to follow valid logic, invalid exemplars should wreck performance. They did not. Prompting with invalid reasoning steps **recovered 80–90% of valid-CoT performance.** What mattered was not the *correctness* of the rationale but its **relevance to the query** and the **correct ordering of steps**.

Read that result for what it says about our two axes. A reasoning trace is itself a token sequence, generated by the same maximum-likelihood machinery as everything else. CoT does not install a truth term; it conditions the decoding trajectory into a **plausible step-shaped manifold** — the region of the output space where text *looks like* reasoning. Landing in that region happens to correlate with correct answers on problems whose correct solution has a step-shaped structure the model has seen many variants of (arithmetic, symbolic manipulation). It is still optimizing the shape of the output, not its validity. The trace is plausibility wearing the costume of logic. [verify: the 80–90% figure is from Wang et al. 2023, ACL, arXiv:2212.10001; confirmed in research notes.]

Two consequences for the prompt engineer, both falsifiable:

- **A reasoning trace is not a verification.** A fluent, well-ordered, confident chain of steps can lead to a wrong answer, and the steps will look just as reasoning-shaped as a correct chain. Do not read the visible trace as evidence the conclusion is true; it is evidence the conclusion is *step-shaped*. This is the §2.1 failure generalized: the trace, like the citation, optimizes appearance.
- **CoT is conditional, not universal.** On reasoning-tuned models, [Meincke, Mollick et al. (2025)](https://arxiv.org/abs/2506.07142) report that explicit "think step by step" adds little and sometimes *adds answer-to-answer variance*, occasionally flipping otherwise-correct answers. CoT earns its place by mechanism (conditioning toward a useful trajectory shape) under stated conditions — not as a truth charm. [verify: Meincke/Mollick "Prompting Science Report 2," arXiv:2506.07142; recent preprint, flag as 2025 and possibly not peer-reviewed.] We return to this conditionality in Ch. 8.

So showing the work does not close the plausibility–truth gap. It often *improves the answer* on structured problems — worth using — while leaving the gap exactly where it was on the surface: a wrong chain looks like a right one. We need something that does not live inside the model's own distribution.

---

## 2.5 The Fact-Check List Pattern: making commitments enumerable

The architectural response named in this book for the plausibility–truth gap is the **Fact-Check List Pattern**, from the [White et al. (2023)](https://arxiv.org/abs/2302.11382) Vanderbilt catalog of prompt patterns (the same catalog that gives us the persona patterns of Ch. 6). Mechanism before name: the pattern instructs the model to emit, alongside its answer, an explicit enumeration of the **load-bearing factual claims** — the propositions on which the answer's correctness depends — so they can be verified.

Under this pattern, the Mycroft assistant would produce its prose **and then**:

> *Claims this answer depends on:*
> *1. The 10-K contains a risk factor on the topic of [regulatory exposure X] — exists in the filing.*
> *2. The quoted sentences appear verbatim in Item 1A of that filing.*
> *3. The quoted language is located at page 27.*

Now look at what changed. The fluent paragraph is unchanged; it is still optimized for plausibility. But its **factual commitments have been separated from the connective prose and rendered as discrete, checkable items.** This is the operational form of the orthogonality claim. An unfalsifiable paragraph becomes a falsifiable list: item 1 is a topic lookup, item 2 a verbatim-string search, item 3 a page check. The pattern converts diffuse plausibility into enumerated commitments a verifier — human or tool — can attack one at a time. The analyst's job shifts from "reverse-engineer which sentences are even claims and then verify each" to "run down these three items."

There is a second, weaker effect worth naming honestly: forcing the model to *name* a claim sometimes surfaces its own uncertainty — a claim asserted confidently inside flowing prose looks shakier isolated as line item 2, and models will somewhat more often hedge an isolated claim than a buried one. Treat this as a mild bonus, not a mechanism to rely on; whether it is a real calibration effect or a formatting artifact is genuinely open. [verify: weak uncertainty-surfacing effect — suggestive but underpowered; flag as unconfirmed.]

### The honest limit (state it before you trust the pattern)

Here is the limit, and it is structural, not a tuning problem: **the model generates the checklist too.** The same distribution that fabricated the Mycroft quote will, asked to list its load-bearing facts, happily certify "the quoted sentences appear verbatim" as item 2 with full confidence. The Fact-Check List does not detect its own fabrications. A model confident enough to invent a citation is confident enough to certify it. Asking the model "is your answer correct?" routes the question back through the very distribution that produced the error — same blind spots, same confident register.

So the honest description is: **the Fact-Check List is a surfacing aid, not a verification.** Its value is that it produces an *artifact* something else can check cheaply, lowering the cost of external verification. That is genuine engineering value. It is not, by itself, reliability. This is the same lesson Ch. 3 reaches from the other direction — *you* are the semantic layer; the model executes syntactic operations and cannot be the thing that grounds them.

Reliability arrives only when an **external check** consumes the list — a check the model cannot talk its way past:

- A **tool or retrieval step** grounds each claim against a source outside the model's distribution. A document-search tool returns the actual filing; a verbatim search of Item 1A returns "string not found" — a result the model cannot wish into existence. This is exactly where the agentic Thought→Action→Observation loop of Ch. 11 enters: the checklist enumerates the claims, and a tool call grounds each against the world. An Observation token entering from outside the distribution can return a "not found" that no amount of fluency overrides.
- A **human decision node** — the irreducible external check for irreducibly high stakes (Ch. 3's contract-review example develops this; Ch. 4 develops why a separate, context-isolated check beats self-review).

A fact-check list with no external verifier is a confession nobody reads. The pattern is the *handle*; the external check is the governance. Do not mistake the handle for the door.

### When to use it

Use the Fact-Check List when the cost of an undetected false claim is high and the claims are *checkable* — citations, figures, dates, named entities, quantitative results, quotations. It is wasted on outputs whose value is not factual (brainstorming, drafting, style work). It is most powerful in narrow or high-stakes domains, which is exactly where Ch. 6's *persona hallucination* bites: an expert persona activates confident, citation-heavy prose without activating knowledge, and the Fact-Check List is the output-side response — it makes the persona's confident commitments enumerable so a tool or human can falsify them. The full treatment of this and the two sibling output-governing patterns (Semantic Filter, Helpful Assistant) is in the output-governing-patterns material (provisional Ch. 7 / 6C); this chapter establishes the orthogonality the Fact-Check List operationalizes.

---

## 2.6 A worked separation: the same answer, governed

Take a concrete **"80 Days to Stay"** request — the SEC-data retrieval running case. A user asks the assistant: *"Which of the company's risk factors mention foreign-currency exposure, and how many basis points of margin did management attribute to it last year?"*

**Ungoverned output (plausibility only):**

> *The company discloses foreign-currency exposure as a principal risk factor, noting that "fluctuations in exchange rates may materially affect our results of operations." Management attributed approximately 120 basis points of margin compression to currency effects in the prior fiscal year.*

Fluent. Confident. The quote sounds like a real disclosure; "120 basis points" sounds like a real figure. Both could be fabricated, and you cannot tell from the surface — that is the whole problem.

**Governed output (Fact-Check List appended):**

> *Claims this answer depends on:*
> *1. The filing lists foreign-currency exposure as a risk factor. [check: keyword search of Item 1A]*
> *2. The quoted sentence appears verbatim in the filing. [check: verbatim string search]*
> *3. Management attributed ~120 bps of margin compression to currency in the MD&A. [check: search MD&A; this is the highest-risk claim — a specific number]*

Now the verifier — a retrieval tool or the analyst — runs three cheap checks. Item 3 is flagged as the highest-risk claim because specific quantities are where fabrication is both most likely (the model interpolates a plausible number) and most consequential. If the retrieval tool returns "120 bps not found; MD&A states 80 bps," the model's plausibility-optimized guess is caught by an Observation it cannot override. The *answer* did not get more truthful. The *system* got verifiable. That distinction is the chapter.

---

## 2.7 Back to the citation that shipped

The Mycroft brief went out with a fabricated quote not because the model malfunctioned but because it functioned exactly as specified: it sampled the most probable continuation of a prompt that asked, in effect, for a complete, well-sourced answer — and "well-sourced" was satisfied, at the level of plausibility, by output that *had the form* of being well-sourced. The system prompt's instruction to "always give a complete answer" made it worse, treating "I can't find that language" as an unhelpful answer to avoid (the sycophancy pressure of Ch. 4, wearing a research-assistant costume).

**The fix is not a better model and not a friendlier instruction.** It is a governance layer in three parts, and each part's role is precisely defined by where it sits relative to the model's distribution:

1. A **Fact-Check List** that forces the assistant to enumerate its load-bearing claims — *this language appears in this filing, on this page.* Self-applied. A handle, not a guarantee.
2. An **external verifier** that consumes the list — a document-retrieval tool (Ch. 11) that grounds each quote against the actual filing and returns "not found" for the fabrication. External. The actual governance.
3. A **bounded instruction** that breaks the sycophantic collapse — *if the language is not in the filing, say so plainly* — backed, for client-facing briefs, by a human review node.

The book's master argument shows up here in the same shape it takes throughout: **architecture is the leverage point, not the model.** The identical model, wrapped in a layer that surfaces commitments and grounds them externally, ships a verifiable brief instead of a confident fabrication. The plausibility–truth gap is not closed inside the model — it cannot be, because the loss function has no truth term. It is *spanned from outside*, by a check the model cannot argue with.

### Bridge to Chapter 3

We have established something unsettling and made it precise: the model can be maximally fluent and flatly wrong, and the two are produced by the same machinery. A natural question follows, and it is the one Ch. 3 takes up. If a system can produce text indistinguishable from a competent expert's — fluent, well-structured, confident — and yet be wrong in ways the surface cannot reveal, then in what sense, if any, does it *understand* what it is saying? Is fluency-without-truth a sign of a syntactic engine that manipulates symbols without grasping their meaning? Ch. 3 makes that case through Searle's Chinese Room: the model is the most sophisticated pattern-matcher ever built, and pattern-matching is not understanding. The plausibility–truth gap of this chapter and the syntax–semantics gap of the next are the same crack viewed from two angles — here as a property of the training objective, there as a property of the architecture.

### Connections back and forward

Ch. 1's stochastic-machine framing supplies the substrate: output is a *sample* from a distribution, and this chapter shows the distribution was shaped by likelihood, not truth. Ch. 3 (Chinese Room) reframes the same gap as syntax vs. semantics and supplies the "you are the semantic layer" principle the Fact-Check List operationalizes. Ch. 4 (Sycophancy) explains why the *helpfulness* layer of post-training pushes the model toward the approval-maximizing answer, sharpening hallucination into "tell the user what they want." Ch. 6 (Persona) names *persona hallucination* — confident expert prose without expert knowledge — for which the Fact-Check List is the output-side response. Ch. 7 / the output-governing-patterns material develops the Fact-Check List in full alongside the Semantic Filter and Helpful Assistant patterns. Ch. 11 (Agentic Systems) supplies the external verifier — tool-grounded Observation tokens — that completes the pattern.

---

**What would change my mind:** A controlled study showing that a model's *self-applied* fact-check list, with no external verifier, reliably catches its own fabricated factual commitments at a rate competitive with an external retrieval check — across narrow, high-stakes domains and under realistic deadline-style prompting. The chapter argues self-surfacing is structurally weaker than external verification because the fabricator certifies its own claims from the same distribution; evidence that a well-designed self-check closes most of that gap would force a specification of when the external verifier is not worth its cost. Separately, a demonstration that the maximum-likelihood objective, plus standard alignment, installs a measurable truth term — that fluency and factual accuracy become reliably *correlated* on held-out factual claims without external grounding — would undercut the orthogonality claim at its root.

---

**Still puzzling:**

1. Whether the Fact-Check List's weak uncertainty-surfacing effect — isolating a claim as a line item makes the model somewhat likelier to hedge it than when it is buried in prose — is a genuine calibration effect or a formatting artifact. If real, it would be a rare case of self-applied governance doing more than surfacing: mildly *improving* calibration, not just lowering verification cost. The evidence is suggestive and underpowered.
2. Why chain-of-thought, which optimizes trajectory *shape* rather than validity, nonetheless lands on correct answers as often as it does on structured problems. The "step-shaped manifold correlates with correct solutions because correct solutions are step-shaped" story is a description, not a mechanism; what determines the size of that correlation across problem classes is not settled.
3. Whether the orthogonality is strict or merely very weak coupling. Pretraining on overwhelmingly-true corpora plausibly induces *some* statistical pull toward true continuations in-distribution. The chapter treats truth as absent from the objective, which is exactly right about the loss; whether the *data distribution* smuggles a faint truth signal back in, and how far it generalizes, is an open empirical question.

---

## References

- Wei, J., Wang, X., Schuurmans, D., Bosma, M., Ichter, B., Xia, F., Chi, E., Le, Q., & Zhou, D. (2022). [Chain-of-Thought Prompting Elicits Reasoning in Large Language Models](https://arxiv.org/abs/2201.11903). *Advances in Neural Information Processing Systems 35 (NeurIPS 2022)*. arXiv:2201.11903.
- Kojima, T., Gu, S. S., Reid, M., Matsuo, Y., & Iwasawa, Y. (2022). [Large Language Models are Zero-Shot Reasoners](https://arxiv.org/abs/2205.11916). *NeurIPS 2022*. arXiv:2205.11916.
- Wang, B., Min, S., Deng, X., Shen, J., Wu, Y., Zettlemoyer, L., & Sun, H. (2023). [Towards Understanding Chain-of-Thought Prompting: An Empirical Study of What Matters](https://arxiv.org/abs/2212.10001). *ACL 2023* (Long Papers). arXiv:2212.10001.
- Meincke, L., Mollick, E. R., Mollick, L., & Shapiro, D. (2025). [Prompting Science Report 2: The Decreasing Value of Chain of Thought in Prompting](https://arxiv.org/abs/2506.07142). arXiv:2506.07142. *(Recent preprint; flag as 2025, possibly not peer-reviewed.)*
- White, J., Fu, Q., Hays, S., Sandborn, M., Olea, C., Gilbert, H., Elnashar, A., Spencer-Smith, J., & Schmidt, D. C. (2023). [A Prompt Pattern Catalog to Enhance Prompt Engineering with ChatGPT](https://arxiv.org/abs/2302.11382). arXiv:2302.11382. *(Source of the Fact-Check List Pattern.)*

---

**Tags:** hallucination, plausibility-truth-orthogonality, maximum-likelihood-no-truth-term, fact-check-list-pattern, format-over-truth, self-applied-vs-external-check, fluency-is-not-truth

---

## Exercises

**Exercise 2.1 — (Understand) Locate the missing term.**
Write out the cross-entropy loss $\mathcal{L}(\theta) = -\frac{1}{T}\sum_t \log P_\theta(x_t \mid x_{<t})$ and annotate each symbol with the quantity it references in the training data. In two sentences, state precisely why no rearrangement of this loss can express "the generated statement is true of the world," and what *would* have to be added to the training setup (not the loss alone) to introduce a truth signal. (Hint: think about what the corpus would need to contain.)

**Exercise 2.2 — (Analyze) Predict the divergence.**
For each of the following requests, predict whether plausibility and truth are likely to *coincide* or *diverge*, and say why in one sentence each: (a) "What is the capital of France?"; (b) "Quote the third sentence of the abstract of [a specific 2019 paper]."; (c) "Summarize the plot of a famous novel."; (d) "Give the exact revenue figure from a mid-cap company's Q3 filing." Then state the general rule your four predictions imply about *which* request features push plausibility and truth apart.

**Exercise 2.3 — (Apply, produce-something) Build and stress the list.**
Take any factual question in a domain you can verify (a citation, a statistic, a quotation). (1) Get an ungoverned answer from a model. (2) Re-prompt with the Fact-Check List Pattern and capture the enumerated claims. (3) Verify each claim against a real source. (4) Now do the adversarial step that exposes the honest limit: in a *fresh* context, paste the model's own answer back and ask it "is each of these claims correct?" Record whether the model certifies any claim that your external check found false. Write a short paragraph on what this tells you about self-applied vs. external verification. *Deliverable: the two prompts, the enumerated list, your external-check results, and the self-certification result.*

**Exercise 2.4 — (Evaluate) Decide on the verifier.**
You are designing the Mycroft brief assistant. For three claim types — (a) a named risk-factor topic, (b) a verbatim quotation, (c) a specific basis-point figure — decide for each whether a self-applied fact-check list alone is sufficient, whether you need an automated retrieval/tool check, or whether you need a human node, and justify each choice by the *cost asymmetry* of an undetected error versus the cost of the check. Produce a one-page governance spec.

---

## What would change my mind

(See the boxed statement above §References — repeated here per anatomy: a controlled study showing self-applied fact-checking reliably catches a model's own fabrications without an external verifier, or a demonstration that standard training installs a measurable, generalizing truth term that correlates fluency with factual accuracy, would force a substantial revision of the orthogonality claim.)
