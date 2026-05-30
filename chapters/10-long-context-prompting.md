> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft.
>
> **Sourcing note:** Figures verified against source abstracts on a dedicated fact-check pass — NINJA (arXiv:2511.04707), multilingual NIAH / mLongRR (arXiv:2409.18006), Found-in-the-Middle (arXiv:2406.16008), and Lost-in-the-Middle (arXiv:2307.03172) all confirmed.

---

# Chapter 10 — Long-Context Prompting: Position, Retrieval, and Injection

*Where in the window you put a thing decides whether the model uses it*

**Author:** Nik Bear Brown
**Editor:** Nik Bear Brown

---

## Suggested titles

1. **Long-Context Prompting: Position, Retrieval, and Injection**
2. **The Middle Is Where Instructions Go to Die**
3. **Why the Same Fact Is Read at the Edges and Ignored in the Center**

---

## TL;DR

A language model does not read a long context uniformly. Accuracy on a fact is highest when that fact sits at the **beginning** or **end** of the input and sags in the **middle** — a U-shaped curve replicated across models and tasks ([Liu et al., 2024](https://arxiv.org/abs/2307.03172)). The recency half of that curve is an artifact of the autoregressive next-token objective: a model trained to predict each token from the ones immediately before it learns to weight recent context heavily. Three consequences follow for prompt design. First, place your highest-priority instruction **last**, where recency makes it most likely to be obeyed. Second, do not trust single-needle retrieval benchmarks — asking for three facts at once can drop accuracy from ~96% to ~40% ([multilingual NIAH, 2024](https://arxiv.org/abs/2409.18006)). Third, the same position machinery is an attack surface: placing a harmful goal at the *front* of a long context raised attack success on one model from a 23.7% baseline to 58.8% ([NINJA, 2025](https://arxiv.org/abs/2511.04707)), which means safety rules belong at the end and user content must never be the last thing the model reads.

---

## Learning objectives

By the end of this chapter you should be able to:

1. **(Understand)** State the U-shaped position–accuracy curve and explain mechanistically why the recency component follows from autoregressive pretraining.
2. **(Apply)** Place instructions, retrieved facts, and safety rules in a long prompt according to three falsifiable placement rules, and design the A/B test that would falsify each.
3. **(Analyze)** Predict multi-needle synthesis collapse — distinguish a benchmark that *looks* solved (single-needle) from the failure it hides (multi-fact synthesis).
4. **(Analyze)** Diagnose a long-context injection attempt and explain why "instructions-last" is a safety control, not only a quality tip.
5. **(Evaluate)** Separate the autoregressive (hard-to-fix) component of position bias from the attention-sink (partially correctable) component, and judge how much of the curve a given mitigation can move.

## Prerequisites

Ch. 1 (Stochastic Machine) — token sampling and conditional distributions; the model generates each token conditioned on the ones before it. Ch. 4 (Sycophancy) — context isolation as a defense. Ch. 9 (Brittleness) — the discipline of testing across variants rather than trusting a single prompt. Basic probability: conditional probability and the multiplication rule.

---

## 10.1 The exoneration on page 150

Start with a scenario, labeled as a hypothetical because it is one: it illustrates a real mechanism, not a documented incident.

A legal-discovery assistant for the **"80 Days to Stay"** matter is handed a 300-page exhibit bundle assembled from an SEC production. Somewhere in that bundle — page 150, dead center — is a single clause that exonerates the defendant. The assembled prompt is straightforward: 300 pages of documents, then the question, *"Does any document here contradict the SEC's allegation that the filing was knowingly false?"* The model reads it, reasons fluently, and answers: *"No document in the production contradicts the allegation."*

The clause was right there. The model had it in context. It read past it.

This is not a hallucination in the Ch. 2 sense — the model did not fabricate. It is not a capability gap — a model that can find the clause when you paste page 150 alone misses it when the clause is buried mid-bundle. The failure is **positional**. Where the clause sat in the window decided whether the model used it. Had the retrieval system placed that page at the *start* or *end* of the assembled context, the model would very likely have caught it.

The lesson this chapter develops: in long-context prompting, *where you put a thing* is an engineering decision with measurable consequences, and the consequences are predictable from how the model was built. The middle of a long context is where instructions and facts go to be ignored. We will make that claim precise, give you placement rules you can test, and then show that the same machinery is an attack surface a careless prompt leaves wide open.

---

## 10.2 The U-shaped curve

You already have a prior for this, even if you have never seen an LLM. Recite a grocery list someone read you ten seconds ago and you will reliably get the *first* item and the *last* item; the middle is mush. Psychologists named this the **serial-position effect** — strong recall at the start (primacy) and end (recency), weak recall in the middle ([Murdock's 1962 free-recall curve](https://en.wikipedia.org/wiki/Serial-position_effect) — *Journal of Verbal Learning and Verbal Behavior*, 64, 482–488 — is the canonical human plot).

Language models show a curve of the same *shape*. The mechanisms are not the same — there is no human short-term store inside a transformer — but the picture rhymes, and the rhyme is a useful hook so long as we puncture it before it misleads.

**The empirical claim.** [Liu, Lin, Hewitt, Paranjape, Bevilacqua, Petroni, and Liang (2024)](https://arxiv.org/abs/2307.03172), published in *TACL* (Vol. 12, pp. 157–173; arXiv:2307.03172), ran two tasks: multi-document question answering and a synthetic key–value retrieval task. In each, they placed the relevant document or key at different positions in the input and measured accuracy. The result is the spine of this chapter:

> Accuracy is highest when the relevant information sits at the **beginning** (primacy) or the **end** (recency) of the input, and drops sharply when the model must retrieve it from the **middle** — a U-shaped curve. The effect holds even for models explicitly built for long contexts.

Plot accuracy against the position of the relevant fact, with position running 0% (start) to 100% (end), and you get a curve high at both edges and sagging in the center.

Let $a(p)$ be accuracy when the target fact sits at relative position $p \in [0,1]$. The empirical finding is

$$a(0) \approx a(1) > a(0.5),$$

with the gap between the edges and the middle reaching tens of percentage points on hard configurations. This is not a quirk to memorize. It is a consequence of how the model was trained and how it allocates attention — which we take in two halves, because the two halves of the curve have *different* mechanisms and *different* fixability.

### Why recency: the autoregressive artifact

Here is the load-bearing mechanism for the whole chapter. A model is trained by predicting each token from the tokens before it. Formally, for token $t_i$,

$$t_i \sim P(t_i \mid t_0, t_1, \dots, t_{i-1}).$$

During pretraining the objective rewards getting the *next* token right given the immediately preceding ones. In ordinary text, the strongest predictor of the next word is usually the words right before it — local context dominates. A model that learns to weight recent tokens heavily is a model that minimizes its training loss. So the autoregressive objective *itself* builds in a bias toward the most recent context.

That is why **recency is stable**: it persists even near the window limit and even in long-context models, because it is baked into what the model was optimized to do. It is not a bug that a bigger window fixes. It is the training objective showing through. This is the chapter's mechanism-before-name: the thing practitioners call "recency bias" is the autoregressive next-token objective viewed from the prompt-design side.

### Why primacy: attention sinks, and why it is weaker

The start of the sequence also gets outsized attention, through a different route. Transformers exhibit an **attention-sink** phenomenon — early tokens, often the very first, receive large attention weight somewhat regardless of their relevance, acting as a place for attention to "park." [Hsieh et al.'s "Found in the Middle" (2024)](https://arxiv.org/abs/2406.16008) (ACL 2024 Findings) showed that the U-shaped *accuracy* curve maps onto a U-shaped *attention* curve: start and end tokens get more attention irrespective of whether they are relevant.

But primacy is **weaker than recency and decays as the window fills**. Early tokens compete with ever more material as the context grows; the start-of-document advantage that holds at 10K tokens erodes at 100K. Greg Kamradt's widely circulated needle-in-a-haystack pressure tests show exactly this texture: top-of-document recall holds better than mid-document recall, but degrades as total length grows ([Kamradt NIAH repo, 2023](https://github.com/gkamradt/LLMTest_NeedleInAHaystack)).

### The honest split: how much is fixable

Here is where the easy story breaks, and you should let it. "Found in the Middle" proposed a training-free, inference-time **calibration**: estimate the position-only component of the attention bias and subtract it, recovering up to **15 percentage points** of RAG accuracy. That recovery is evidence that *part* of the bias is a correctable attention artifact — not the immutable consequence of the training objective.

So the honest position is two-part, and you should resist collapsing it:

- The **autoregressive component** of recency bias comes from the training objective. It is structural and hard to fix at inference time.
- The **attention-sink component** is an architectural artifact and is *partially* correctable — the 15-point calibration recovery is the evidence.

Anyone who tells you the whole curve is an unfixable law of nature is overclaiming; anyone who tells you it is a tuning knob you can dial away is also overclaiming. The curve has a hard floor and a soft ceiling.

**Misconception to dislodge.** *"A bigger context window means the model reads everything in it."* No. Advertised context length is the *nominal* window. [Hsieh et al.'s RULER (2024)](https://arxiv.org/abs/2404.06654) (NVIDIA, arXiv:2404.06654) made the point sharply: the vanilla needle-in-a-haystack test measures only superficial retrieval, and once you extend it with multi-key, variable-tracking (a multi-hop proxy), and aggregation tasks, most models hold consistent accuracy only well *below* their advertised token limit. The **effective context** is much smaller than the nominal context. A 200K window does not mean 200K usable tokens; it means 200K tokens you are *allowed* to send, of which a model-and-task-dependent fraction is actually attended to with full reliability.

---

## 10.3 Multi-needle collapse: the benchmark that hides the failure

Single-needle retrieval — "find the one out-of-place sentence in this haystack" — is largely **solved** on frontier models. Numbers near 95–96% are routine on modern models for one fact in one long document. If your evaluation stops there, you will conclude your long-context system works.

It does not, and here is the gotcha. Ask for *more than one* fact at once and the floor drops out. Work on multilingual needle-in-a-haystack ([Multilingual Needle in a Haystack / mLongRR, arXiv:2409.18006](https://arxiv.org/abs/2409.18006)) reports that the best models (Gemini-1.5, GPT-4o) hit **~96% in English** with a **single** target sentence, but **three target sentences in English drops to roughly 40%** (and 0% in low-resource Somali) — confirmed against the paper's abstract. That is the empirical basis for "multi-needle collapse," and note the correction the research file insists on: the figure is **~40% for 3 needles**, not the rounder, more optimistic "~60%" that circulates. Cite the specific n-needle number, not a comfortable round one.

LangChain's extension of Kamradt's test to N needles confirms the direction: retrieval drops as needle count rises and as context lengthens, and needles placed earlier in a long context are retrieved less reliably — consistent with recency dominance ([LangChain multi-needle blog](https://blog.langchain.com/multi-needle-in-a-haystack/)).

Why does adding a second and third needle break things so much harder than the first? Two mechanisms compound. First, **synthesis is not retrieval**: pulling one fact to the front of generation is easy; holding three facts simultaneously salient while composing an answer competes for the same finite attention budget. Second, **the U-curve applies to each needle separately** — with three needles scattered through a long context, at least one of them is probably sitting in the middle, where the curve says it will be missed.

There is a related, under-sourced prediction worth flagging honestly. When two documents in a long context *contradict* each other, the recency bias predicts the model will silently resolve toward the more recent fact without flagging the conflict — call it **silent contradiction resolution**. This is intuitive and consistent with recency, but no clean primary citation isolating *position-driven* contradiction resolution with calibration failure could be located (UNVERIFIED — not an established result in the literature). Treat it as a reasoned prediction from the recency mechanism, not a documented finding.

The broader lesson generalizes past long context, and it is the Ch. 9 lesson wearing new clothes: **a benchmark that looks solved can hide the real failure.** Single-needle at 95% is a press release. Three-needle synthesis at 40% is your production system.

> **Running example.** For "80 Days to Stay," the SEC-retrieval task is rarely "find the one clause." It is usually "reconcile the revenue-recognition note (page 40), the restatement disclosure (page 150), and the auditor's letter (page 280)" — a three-needle synthesis across a long bundle. The single-needle benchmark that made the pipeline look ready is exactly the wrong evidence for the job it has to do.

---

## 10.4 Placement rules you can test

The mechanism converts directly into engineering. Here are the rules, each stated as a falsifiable claim with the experiment that would break it. This is the chapter's deliverable: not "be aware of position effects" but "put things here, and here is how you'd prove me wrong."

**Rule 1 — Put the highest-priority instruction last.** Because recency persists even near the window limit, the instruction you most need obeyed belongs at the *end* of the assembled prompt, after the documents, not in a system preamble buried under 200 pages.
*Falsifiable test:* take a working prompt, move the key instruction to the middle, hold everything else fixed, and measure the compliance drop. If compliance does not fall, the rule is wrong for your model and task.

**Rule 2 — Put critical retrieved facts at the extremes; filler in the middle.** This is standard production RAG practice: rerank retrieved chunks so the highest-relevance passages land at the *start and end* of the assembled context, deliberately exploiting the U-curve (documented across RAG-failure writeups from DigitalOcean, Snorkel, Atlan).
*Falsifiable test:* A/B the rerank order — best-first-and-last vs. best-in-the-middle — and measure answer accuracy. If middle-placement does not hurt, the U-curve is not biting your pipeline.

**Rule 3 — Put safety constraints at the end, and never let user content be the last thing.** Recency that helps compliance also helps an attacker whose content is recent. Safety rules go last; untrusted user or document content must not occupy the final, highest-attention position.
*Falsifiable test:* run a NINJA-style position sweep (§10.5) and confirm attack success is lower with rules-last than with user-content-last.

**Rule 4 — Do not trust single-needle benchmarks as evidence of synthesis ability.** A pipeline that scores 95% on one-needle retrieval can score 40% on three-needle synthesis.
*Falsifiable test:* run a 3-needle synthesis task and watch accuracy fall toward ~40%. If it holds near 95%, your synthesis is unusually robust — measure it, do not assume it.

**The counterintuitive corollary — more documents can hurt.** Teams routinely raise `top_k` to "improve recall," reasoning that more retrieved chunks means more chances to include the right one. Beyond a point this *backfires*: the correct fact gets buried in the middle of a now-longer context, and the lost-in-the-middle penalty swamps the recall gain. The fix is not more documents; it is *better-placed* documents — rerank and position, do not just retrieve more.

A schematic of the recommended layout:

```
[ top ]      system role / low-priority context
[ middle ]   filler / mid-relevance retrieved docs
[ end ]      highest-priority instruction
             + safety / constraint rules
             + the most-relevant retrieved facts
             + the user's actual question
```

Recency makes the bottom of that block the most-attended region. That is where the load-bearing tokens go.

---

## 10.5 Position is an attack surface

Everything above is about *quality*. The same machinery is a *security* problem, and this is the part a careless prompt designer never sees coming.

If the model attends most to the front and end of a long context, then an attacker who controls *where* their content sits controls how much the model attends to it. Two literatures make this concrete.

**Many-shot jailbreaking.** [Anil et al. (2024)](https://www.anthropic.com/research/many-shot-jailbreaking) (Anthropic; NeurIPS 2024) showed that stuffing hundreds of faux dialogue turns demonstrating an unwanted behavior *into the context* overrides alignment. Attack strength scales with shot count, near-zero at 5 shots and reliable around 256, following a power law in the log of the number of shots, and it works across GPT-3.5/4, Claude 2.0, Llama 2 70B, and Mistral 7B. The point for us: long context is not just a recall problem, it is an *attack surface*, and in-context demonstrations exploit the same positional/recency machinery that helps legitimate instructions.

**NINJA — position-dependent safety.** The sharper result for this chapter is [NINJA, "Jailbreaking in the Haystack" (2025)](https://arxiv.org/abs/2511.04707) (arXiv:2511.04707). NINJA appends benign, model-generated, thematically relevant filler to a harmful goal and varies the *position* of that goal in the context. On HarmBench, attack success rose **from a 23.7% baseline to 58.8% for Llama-3.1-8B-Instruct** (also 23.7% → 42.5% for Qwen2.5-7B-Instruct, and roughly 23% → 29% for Gemini Flash) — figures confirmed against the NINJA paper. NINJA explicitly attributes the effect to the same U-shaped primacy/recency bias: putting the harmful goal at the *beginning* maximizes attack success, and putting it at the *end* mitigates.

State that result precisely, because it is easy to mangle. **58.8% is the post-attack attack-success rate for one specific model (Llama-3.1-8B-Instruct), up from a 23.7% baseline — it is not a universal ceiling.** "Up to 58.8% on Llama-3.1-8B, from a 23.7% baseline" is the honest phrasing; "up to 58.8% attack success" stated bare implies a law that the data does not support.

**The defense falls straight out of the mechanism.** Because harmful-goal-at-front maximizes attack success and harmful-content-at-end mitigates, two structural controls follow:

1. **Safety rules go last.** Recency makes the final instruction the most-attended; put the constraints there, where they win the attention competition against earlier content.
2. **Never let untrusted content be the last thing.** If a user (or a retrieved document) can place their content at the end of the assembled prompt, recency works *for them*. Wrap user content, and re-append your constraints *after* it.

This is the same instinct as Ch. 4's context isolation, now expressed as a layout rule: **"put instructions last" is not only a quality tip — it is a safety control.** The mechanism that makes your good instruction obeyed is the mechanism an attacker borrows; you keep it on your side by owning the final position.

**Misconception to dislodge.** *"Instructions-last makes injection impossible."* It does not. It *mitigates*. A determined attacker controls the position of *their* content too, and against an adaptive attacker who can append after your rules, recency stops being purely your friend. The durability of the recency defense against adaptive attacks is an open question (§ Still puzzling). Instructions-last raises the cost of injection; it does not close the door.

---

## 10.6 Back to page 150

Return to the exonerating clause. Nothing was wrong with the model and nothing was wrong with the clause. The retrieval system assembled 300 pages and let the one page that mattered fall in the dead center of the window — the trough of the U-curve, the region the autoregressive objective and the attention machinery jointly under-weight. The model read fluently past it because the architecture around the model placed it where the model reads least.

The fix is not a better model and not a cleverer question. The fix is **placement**: rerank so the high-relevance pages land at the start and end, keep filler in the middle, append the question and any constraints last. Same model, same documents, different layout — and the clause moves from the trough to the edge, where the curve says it gets used.

That is the book's master argument in this chapter's terms: **architecture is the leverage point, not the model.** In long-context prompting, "architecture" is partly just *where in the window each token sits.* You do not get to change how the model attends. You do get to decide what occupies the high-attention positions. The engineer who treats the context window as an undifferentiated bag of tokens ships systems that miss page 150. The engineer who treats position as a designed variable — instructions last, facts at the edges, user content never final, synthesis tested not assumed — ships systems that hold up under length and under attack.

One honest caveat to carry forward. The U-shaped curve is robust and replicated, but the *exact* multi-needle degradation curve varies by model, language, needle similarity, and distractor design — no single number generalizes. The ~40%-at-three-needles figure is a calibration point, not a law. When a new model or a new domain arrives, the *shape* is a strong prior and the *magnitudes* are an experiment you still have to run.

---

## Exercises

1. **(Understand)** In one paragraph, explain why recency bias follows from the autoregressive next-token training objective, and why this makes recency *more* stable than primacy as the context window fills. Do not use the phrase "the model pays more attention to recent tokens" without saying *why* the training objective produces that.

2. **(Apply)** You are given a 50-page filler document, one target fact, and a question the fact answers. Design — in prose, with exact prompt layouts — a position sweep that places the fact at the start, the middle, and the end. State the metric you will record and the result that would *falsify* Rule 1 (highest-priority instruction last).

3. **(Analyze)** A teammate reports that their RAG pipeline scores 96% on a needle-in-a-haystack benchmark and concludes it is production-ready for the "80 Days to Stay" three-document reconciliation task. Write the two-sentence objection that names the specific failure the benchmark hides, and the one experiment you would run before agreeing.

4. **(Analyze / Evaluate)** Given the NINJA result (23.7% → 58.8% on Llama-3.1-8B from baseline), a colleague writes in a design doc: "Long-context models have a 58.8% jailbreak rate." Identify exactly what is wrong with that sentence, rewrite it correctly, and state the one architectural control the result motivates.

5. **(Apply — produce)** Take a real long-context prompt you use (or write a plausible one for the "80 Days to Stay" SEC task) and *re-lay-it-out* under the four placement rules. Submit the before and after, annotate where the high-priority instruction, the most-relevant facts, the filler, and the safety rules each sit, and mark which single change you expect to move accuracy most and why.

---

## What would change my mind

A controlled study showing that, on a representative multi-needle synthesis task across current frontier models, accuracy at three needles does **not** fall meaningfully below single-needle accuracy *and* that the position of each needle does not predict whether it is retrieved. The chapter argues multi-needle collapse and position-dependence are predictable from the U-curve; evidence that frontier models have flattened the curve enough that placement no longer moves accuracy would force me to restrict the placement rules to a class of older or smaller models rather than stating them generally. A weaker version that would also move me: a demonstration that inference-time calibration ("Found in the Middle"-style) reliably recovers the *full* gap, not ~15 points — which would shift recency from "structural, hard to fix" toward "correctable artifact," and change Rule 1 from architecture to a tuning step.

## Still puzzling

- **How much of recency is truly unfixable.** The 15-point calibration recovery says part of the bias is a correctable attention artifact, but the autoregressive component should be far stickier. We do not have a clean decomposition that says "X points are training-objective, Y points are attention-sink" for a given model.
- **Whether silent contradiction resolution is real and position-driven.** It is a reasoned prediction from recency, not a cited result. A dedicated study varying the position of two conflicting facts and measuring whether the model flags the conflict or silently takes the recent one would settle it.
- **Defense durability of "instructions-last" against an adaptive attacker.** NINJA shows goal-at-end mitigates, but an attacker who controls the final position can turn recency against you. How robust the recency defense is when the adversary optimizes position is open.
- **Does scaling effective context close the U-curve or just shift it?** Long-context RAG work ([Databricks, arXiv:2411.03538](https://arxiv.org/abs/2411.03538)) suggests effective context is improving but still lags nominal limits. Whether the curve flattens or merely moves is unresolved.

---

## References

- Liu, N. F., Lin, K., Hewitt, J., Paranjape, A., Bevilacqua, M., Petroni, F., & Liang, P. (2024). [Lost in the Middle: How Language Models Use Long Contexts](https://arxiv.org/abs/2307.03172). *Transactions of the Association for Computational Linguistics*, 12, 157–173. arXiv:2307.03172. DOI: 10.1162/tacl_a_00638.
- Hsieh, C.-P., Sun, S., Kriman, S., Acharya, S., Rekesh, D., Jia, F., Zhang, Y., & Ginsburg, B. (2024). [RULER: What's the Real Context Size of Your Long-Context Language Models?](https://arxiv.org/abs/2404.06654) arXiv:2404.06654.
- Hsieh, C.-Y., et al. (2024). [Found in the Middle: Calibrating Positional Attention Bias Improves Long Context Utilization](https://arxiv.org/abs/2406.16008). ACL 2024 Findings (2024.findings-acl.890). arXiv:2406.16008.
- Anil, C., Durmus, E., Panickssery, N., Sharma, M., Benton, J., … Perez, E., Grosse, R., Duvenaud, D. (2024). [Many-shot Jailbreaking](https://www.anthropic.com/research/many-shot-jailbreaking). Anthropic; NeurIPS 2024.
- NINJA — [Jailbreaking in the Haystack](https://arxiv.org/abs/2511.04707) (2025). arXiv:2511.04707. (23.7% → 58.8% ASR on Llama-3.1-8B-Instruct confirmed against the paper.)
- Multilingual Needle in a Haystack / mLongRR (2024). [arXiv:2409.18006](https://arxiv.org/abs/2409.18006). (~96% single-needle → ~40% three-needle in English confirmed against the abstract.)
- Kamradt, G. (2023). [Needle In A Haystack — Pressure Testing LLMs](https://github.com/gkamradt/LLMTest_NeedleInAHaystack). GitHub repository.
- LangChain (2024). [Multi Needle in a Haystack](https://blog.langchain.com/multi-needle-in-a-haystack/). Blog.
- Databricks (2024). [Long Context RAG Performance of Large Language Models](https://arxiv.org/abs/2411.03538). arXiv:2411.03538.

---

**Tags:** lost-in-the-middle, u-shaped-position-curve, recency-as-autoregressive-artifact, multi-needle-collapse, long-context-injection, instructions-last

---

## A note about AI

Long-context prompting is where "it has a big context window" gets mistaken for "it reads everything you give it." The model will accept 200K tokens. It will attend to a much smaller, position-skewed slice of them.

Where the model genuinely helps: running your own position sweep. Ask the model to take a fixed fact and a fixed question, and generate three prompts with the fact at the start, middle, and end of identical filler — then you run all three and read the curve off your own outputs. The model is good at producing the controlled stimuli; you do the measuring.

Where the model does damage: confidently answering "no" to "does anything here contradict X?" when the contradicting passage was sitting in the middle of the context the whole time. The fluent negative is the dangerous one, because it reads exactly like a thorough search that found nothing.

The rule: where you put a fact in the window changes whether the model uses it. Test placement; do not trust coverage.

---

##  AI Wayback Machine
**Hermann Ebbinghaus** was the German psychologist who founded experimental memory research, running nonsense-syllable recall studies on himself in the 1880s and first describing position-dependent recall.

**Run this:**

```
Who is Hermann Ebbinghaus, and how does their work connect to the lost-in-the-middle position effect we covered in this chapter? Keep it to three paragraphs. End with the single most surprising thing about their career or ideas.
```

→ Search **"Hermann Ebbinghaus"** on Wikipedia.

**Now make the prompt better.** Try one of these:

- Ask it to map primacy and recency from Ebbinghaus's serial-position findings onto the U-shaped LLM accuracy curve — and to say where the analogy is tight and where it breaks.
- Add a constraint: "Answer including where the human-memory mechanism (short-term store) differs from the LLM mechanism (attention + autoregression)."

What changes? What gets better? What gets worse?
