> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft.

---

# Chapter 1 — The Stochastic Machine: Why Output Is Sampled, Not Retrieved

*The same prompt, twice, gives two answers — and the reason is the entire foundation of the discipline*

**Author:** Nik Bear Brown
**Editor:** Nik Bear Brown

---

## Suggested titles

1. **The Stochastic Machine: Why Output Is Sampled, Not Retrieved**
2. **Same Prompt, Different Answer: Sampling as the Root Cause**
3. **Not a Database: Reading Every Output as a Probabilistic Event**

---

## TL;DR

Ask a model the identical question twice and you can get two different answers — not because the model "changed its mind," but because each answer is a fresh sample drawn from a learned conditional distribution over tokens, and sampling is by definition non-deterministic above temperature zero. This chapter takes the distribution mechanics of Ch. 0 and turns them into behavioral law: every output is a *probabilistic event*, not a database lookup, which means (a) identical prompts legitimately diverge, (b) the divergence is controllable — you can predict, from the sampling parameters, whether outputs will be tight or scattered, and (c) the model's own "reasoning" is itself a property of the output distribution, not of the prompt string, demonstrated by the fact that chain-of-thought reasoning paths can be elicited by changing the *decoding* alone, with no change to the prompt (Wang & Zhou, 2024). Treating the model as a retrieval system is the single most expensive misconception in prompt engineering; treating it as a stochastic machine is the foundation everything else is built on. The chapter ends by handing Ch. 2 its question: if every output is sampled, when is the model *confidently, invisibly wrong*?

---

## Learning objectives

By the end of this chapter you should be able to:

1. **(Understand)** Explain why identical prompts can produce different outputs, in terms of sampling from a conditional distribution rather than retrieval from a store.
2. **(Understand)** Distinguish "the model is random" from "the model samples from a *learned, structured* distribution," and say why the distinction matters for engineering.
3. **(Apply)** Predict the *direction* in which a change to temperature, top-p, or top-k will move the variability and character of a model's outputs on a given task.
4. **(Apply)** Design a minimal experiment to measure output variability for a fixed prompt, and interpret the result (tight vs. scattered) in terms of distribution shape.
5. **(Analyze)** Use the "reasoning lives in the distribution, not the prompt" finding to argue why a decoding change can substitute for a prompt change, and identify when each lever is appropriate.

## Prerequisites

Ch. 0 (Foundations: Sampling, Logits, and the Shape of a Distribution) — softmax, temperature as logit rescaling, top-k/top-p as truncation, and the chain-rule view of autoregressive generation. If you skipped Ch. 0 because your course assumes that math, the one fact you must carry in is this: at each step the model emits a probability distribution over its whole vocabulary and *draws a sample* from it. This chapter is the consequences of that fact. (Ch. 0 = mechanics of the distribution; Ch. 1 = what those mechanics do to behavior.)

---

## 1.1 The reproduction: same prompt, different answer

Run this. Set a chat model's temperature to roughly 0.9 and send the same prompt five times, in five fresh sessions so no history carries over:

> *"Give me a name for a coffee shop that specializes in single-origin Ethiopian beans. Just the name, nothing else."*

You will get something like: *Yirgacheffe & Co.* — *The Origin Room* — *Abyssinia Roasters* — *Single Hill Coffee* — *Harrar House*. Five sends, five names. No setting changed between sends. No typo. The model did not "misremember." Nothing went wrong.

Now do the uncomfortable version. Lower the temperature toward 0 and send the *same* prompt five times. Now you will very likely get the *same* name five times — say, *Yirgacheffe & Co.* every time. Same machine, same prompt, but now the outputs collapse to one.

Two observations sit on the table, and they are the whole chapter:

1. **The variability is real and prompt-independent.** You did not phrase the question five different ways. The divergence at high temperature came from the machine, not from you.
2. **The variability is controllable.** A single parameter — the same temperature knob from Ch. 0 — turned a scatter of five distinct answers into one repeated answer. Whatever is producing the divergence responds predictably to a dial.

If the model were a database — if "the answer" were stored somewhere and looked up — neither observation would make sense. A database returns the same row every time; it does not have a dial that controls how often it returns a *different* row. The behavior in front of you is not retrieval. It is sampling. And the dial is temperature, doing exactly what Ch. 0 said it does: at high $T$ the distribution over candidate names is flat enough that several names share meaningful probability mass, so different draws land on different names; at low $T$ the distribution sharpens until one name holds nearly all the mass, so every draw lands there.

The rest of this chapter earns the claim that *this is the normal case, not a glitch*, and then extracts the engineering consequences.

---

## 1.2 Why retrieval is the wrong mental model

The intuition that an LLM "looks things up" is seductive because so much of its behavior *mimics* retrieval. Ask for the capital of France and it reliably returns "Paris." Ask for the boiling point of water at sea level and it returns "100°C." It feels like a lookup table with very good coverage.

Here is the mechanism that the retrieval picture gets wrong. From Ch. 0: at each step the model computes a distribution $P(x_t \mid x_{<t})$ over its entire vocabulary and samples a token from it, then conditions on that token to compute the next distribution, and so on. There is no row labeled "capital of France → Paris" anywhere in the system. There is a distribution that, *given the context "The capital of France is,"* places almost all its mass on the token ` Paris`. The reliability you observe is the reliability of a sharply peaked distribution, not of a stored fact.

This is testable, and the test is the §1.1 reproduction. A retrieval system has no notion of temperature; you cannot make a database return a different row "more often" by turning a knob. A sampling system does exactly that. The fact that temperature *works at all* is direct evidence that the underlying operation is a draw from a distribution, not a fetch from a store. (Mechanism before name: the thing we just described — a system that defines a probability distribution over the next item conditioned on all prior items, and generates by repeatedly sampling and feeding the result back in — is what is meant by an **autoregressive generative model**. The name is a label for the mechanism, not an explanation of it.)

Two consequences fall out immediately:

**Reliability is a property of distribution *shape*, not of stored truth.** "Capital of France" is reliable because the training distribution made that conditional extremely peaked. A genuinely ambiguous or sparsely-attested query produces a *flat* distribution — many tokens sharing mass — and so produces high run-to-run variability even at modest temperature. The same machine is "reliable" on one query and "scattered" on another, with no change to the machine. That is impossible to explain with retrieval and immediate to explain with sampling.

**There is no "the answer" to be returned — there is only the next sample.** When you ask a question, the model is not retrieving an answer and deciding how to word it. The wording *is* the answer; it is generated token by token by sampling. This is why two correct answers can be phrased completely differently, and why a single unlucky early sample can derail an entire response (recall Ch. 0's feedback loop: each sampled token re-conditions every distribution after it).

**Common misconception.** *"Okay, but at temperature 0 it's deterministic, so then it really is a lookup."* At $T = 0$ the model takes the argmax token at each step, which is deterministic *given identical logits*. But it is still not retrieval — it is greedy sampling from the same distribution, just with the randomness removed by always taking the peak. And in practice even $T = 0$ is not bit-identical across runs: floating-point non-associativity, request batching on the server, and silent model updates perturb the logits enough to occasionally flip a token `[verify: cite reproducibility-of-LLM-inference discussion]`. "Deterministic at temperature 0" is an idealization of the math, not a property you can lean on in production. Determinism is a *limit* of the sampling process, not an escape from it.

---

## 1.3 "Random" is the wrong word, too

Having argued the model samples, we now have to defend it from the opposite error. When people learn that output is sampled, the next thought is often *"so it's just random — it makes things up at random."* That is as wrong as the retrieval picture, in the other direction.

The distribution the model samples from is not uniform and not arbitrary. It is **learned** — shaped by training on a vast corpus so that the conditional $P(x_t \mid x_{<t})$ assigns high probability to continuations that resemble the training data and low probability to continuations that do not. "The capital of France is ___" yields a distribution with a spike on ` Paris` precisely because, across training, that continuation was overwhelmingly the one that occurred. The sampling is random; *what it is sampling from* is a highly structured, data-shaped object.

So the precise statement is: **the model draws a random sample from a non-random, learned distribution.** Both halves matter for engineering.

- The *learned, structured* half is why prompt engineering is possible at all. If outputs were uniform noise, no prompt could steer them. Because the distribution is conditioned on your context (Ch. 0, §0.5), changing the context changes the distribution's shape, and that is the lever you pull.
- The *random sample* half is why prompt engineering is *empirical*. A single run tells you what the model did *that draw*, not what the distribution looks like. To characterize a prompt's behavior you must sample it repeatedly — which is the seed of the evaluation discipline that Ch. 9 builds out in full.

Hold both. "It's a lookup" and "it's random" are the two cliffs on either side of the road. The road is: *a random sample from a learned conditional distribution.*

**Worked framing — Wordsville.** Throughout the book, *Wordsville* is our running prompt-architecture case: a content system that generates short town-newsletter blurbs from structured event data. Suppose Wordsville's prompt is *"Write a one-sentence announcement for: {event}"* and the event is a bake sale. Run it many times at $T = 1$ and the outputs scatter across phrasings — *"The annual bake sale returns Saturday,"* *"Don't miss Saturday's bake sale,"* *"Sweet treats await at this weekend's bake sale."* This scatter is not the system malfunctioning. It is the system *working as a sampler*: the distribution over "acceptable one-sentence bake-sale announcements" is broad because many phrasings are good, so draws land in different places. When the Wordsville team wants consistency (a fixed house voice), they are really asking to *reshape the distribution* — lower the temperature, or constrain the prompt so the distribution of acceptable outputs is narrower. They are not asking the model to "stop being random"; they are asking to engineer the distribution's shape. That reframing — from "make it consistent" to "narrow the distribution" — is the move that separates prompt engineering from prompt wishing.

---

## 1.4 Predicting the divergence: the parameters as behavioral controls

If output is a sample from a distribution, and temperature/top-k/top-p reshape that distribution (Ch. 0), then those parameters are *behavioral controls* and you should be able to predict their effects without running the model. Here is the prediction table the chapter wants you to be able to reconstruct from mechanism:

| Change | Effect on distribution (Ch. 0) | Effect on observed behavior |
|---|---|---|
| Raise temperature | Flattens — mass spreads toward unlikely tokens | More variety run-to-run; more "creative"; eventually incoherent |
| Lower temperature | Sharpens — mass concentrates on leaders | More repetitive, more deterministic; can loop on some models |
| $T \to 0$ (greedy) | Argmax at each step | Same output each run (idealized); locally-optimal, sometimes globally worse continuations |
| Lower top-p / smaller top-k | Truncates more of the tail | Fewer "surprising" tokens survive; tighter, safer, less diverse |
| Higher top-p / larger top-k | Truncates less | More tail tokens in play; more variety, more risk of an odd draw |

Two predictions worth stating as falsifiable claims, because you can check them in ten minutes:

1. **On a task with many good answers (naming, brainstorming, phrasing), raising temperature increases run-to-run variety.** This follows directly: such tasks have broad distributions, and flattening a broad distribution spreads draws further. *Falsifiable:* if you found a task where raising temperature did not increase output diversity despite a measurably non-peaked distribution, the framing would be in trouble.
2. **On a task with one strongly-favored answer (factual recall on well-attested facts), temperature has little effect until it is high enough to overcome a large logit gap.** A peaked distribution stays peaked under mild flattening — Ch. 0's arithmetic showed an 86% leader at $T=0.5$ still leading at 50% at $T=2$. So "capital of France" survives temperature changes that scatter "name a coffee shop." Same knob, different effect, *because the distributions differ in shape* — which is the unifying prediction.

This is what it means to say the parameters are controls and not magic: their effects are *deducible* from distribution shape plus the task's answer-space breadth. An engineer who internalizes this stops asking "what temperature should I use?" as if there were a universal answer and starts asking "how broad is the space of acceptable outputs for *this* task, and do I want to sample widely or narrowly across it?"

**Common misconception.** *"Higher temperature = more creative is always good for creative tasks."* Temperature does not add creativity; it widens the sample. Past a point, widening the sample on a coherence-demanding task just samples incoherent tokens — the tail of the distribution is full of tokens that are *possible* but *bad*. "Creativity" that survives is creativity that was already in the plausible region of the distribution; temperature only governs how far into the tail you reach. There is a task-specific sweet spot, found empirically, not a monotonic "more is better."

---

## 1.5 The reasoning is in the distribution, not the prompt

Here is the finding that most sharply proves output is a property of the distribution rather than of the prompt string — and it is the bridge from "sampling explains variability" to "sampling explains *capability*."

The standard story about getting a model to reason is *prompting*: add "Let's think step by step" (Kojima et al., 2022) or supply worked examples with reasoning traces (Wei et al., 2022), and accuracy on multi-step problems jumps. Kojima et al. lifted text-davinci-002 on the MultiArith benchmark from 17.7% to 78.7% with a single appended phrase `[verify exact figures, arXiv:2205.11916]`. The intuitive reading is that the *words* "think step by step" unlock reasoning.

Wang & Zhou (2024), "Chain-of-Thought Reasoning Without Prompting," falsifies the strong version of that reading. They show that chain-of-thought reasoning paths can be elicited **by changing the decoding alone, with no change to the prompt at all** `[verify arXiv:2402.10200, NeurIPS 2024]`. The mechanism: instead of greedily taking the top token at the first step, inspect the top-$k$ *alternative* first tokens and continue decoding from each. Some of those alternative branches are reasoning trajectories — step-by-step paths — that were already present in the model's output distribution, just not at the very peak. The reasoning was *latent in the distribution*; greedy decoding simply was not surfacing it. Selecting it is a sampling/decoding choice, and it yields large gains (reported as +10 to +30 absolute points on GSM8K across the PaLM-2 family).

Sit with what this means for the retrieval-vs-sampling argument. If you can extract a reasoning chain by changing *which part of the distribution you sample from*, with the prompt held fixed, then the reasoning capability is not a property of the prompt string — it is a property of the *shape of the output distribution*, accessible through decoding. The prompt "Let's think step by step" and the decoding trick are two different ways of reaching the same latent region of the distribution: the prompt reshapes the distribution so reasoning paths rise to the top; the decoding trick leaves the distribution alone and reaches deeper into it. Same destination, two levers.

This generalizes into a working principle for the rest of the book: **a prompt change and a decoding change are often substitutable, because both are operations on the same underlying distribution.** When you cannot edit the decoding (most chat APIs expose only temperature/top-p, not top-k branch inspection), you reach the latent region by prompting. When you control the decoding loop (you run the model yourself), you have a second lever. Knowing they are levers on the *same* object is what lets you reason about which to use rather than cargo-culting one.

A second, sobering result from the same literature keeps us honest about *what* the reasoning is. Wang et al. (2023), "Towards Understanding Chain-of-Thought Prompting," showed that prompting with **invalid** reasoning steps still recovers 80–90% of valid-CoT performance, and that the *relevance* of steps to the query and their *ordering* matter far more than their factual correctness `[verify arXiv:2212.10001, ACL 2023]`. So the chain-of-thought is not (mostly) the model executing valid logic and reading off the result. It is the model being conditioned into a step-shaped trajectory through the distribution — a trajectory that *lands on correct answers more often* without necessarily *being* correct reasoning. This is the cleanest possible illustration of the chapter's thesis: the output is a sampled trajectory through a learned distribution, and "reasoning" is the *shape* of that trajectory, not a guarantee about its content. Ch. 8 develops the decision procedure for when to elicit reasoning and when (on reasoning-tuned models) it adds variance and stops helping.

**Common misconception.** *"Chain-of-thought makes the model reason, so it makes the model correct."* The two papers above pull these apart. CoT reliably changes the *trajectory shape* (step-by-step), which correlates with landing on correct answers on many tasks. It does not install valid logic — invalid rationales work nearly as well — and on reasoning-tuned models the explicit "think step by step" can add answer-to-answer variance and occasionally flip a correct answer to a wrong one (Meincke, Mollick et al., 2025, "Prompting Science Report 2") `[verify arXiv:2506.07142]`. Reasoning prompting is a distribution-reshaping tool with scope conditions, not a correctness switch.

---

## 1.6 What sampling forces on the engineer

Pull the consequences together, because they reshape the job.

**You cannot validate a prompt from one run.** A single output is one sample. It tells you the prompt *can* produce that output, not that it *typically* does. To make a falsifiable claim about a prompt's behavior — "this extraction prompt returns valid JSON 98% of the time" — you must sample it repeatedly and count. This is not pedantry; it is the direct consequence of output being a probabilistic event. The minimal experiment: fix the prompt, fix the parameters, run $N$ times, and characterize the *distribution* of outputs (how often correct, how varied, how often malformed). One run is an anecdote; the distribution is the engineering object. (Ch. 9 turns this into a full evaluation discipline; the seed is here.)

**"It worked for me" is a statement about one draw.** When a colleague says a prompt works and you cannot reproduce it, neither of you is necessarily wrong — you may have drawn different samples from a broad distribution. The fix is to narrow the distribution (lower temperature, tighter prompt, constrained output format) until the behavior you want is the *typical* draw, not a lucky one. Reliability engineering for LLMs is, mechanically, distribution-narrowing.

**The parameters are part of the prompt.** Temperature and top-p are not "settings" separate from your prompt design; they co-determine the output distribution along with the prompt text. A prompt that is excellent at $T = 0.2$ may be unusable at $T = 1.2$. Reporting a prompt's behavior without reporting its decoding parameters is like reporting a measurement without units. Wordsville's "house voice consistency" problem from §1.3 is half a prompt problem and half a temperature problem, and treating it as purely a wording problem will fail.

**Mycroft note.** *Mycroft*, our investment-intelligence running case, surfaces the cost of getting this wrong. A research analyst asks Mycroft to summarize a filing and gets a clean, confident summary; satisfied, they ship it. The summary was one draw from a distribution that, on this particular filing, was not sharply peaked — several plausible-but-conflicting summaries shared mass. A second draw would have read differently, and the difference would have flagged that the model was *uncertain* here. By treating the single confident output as "the answer," the analyst discarded exactly the signal — output variability — that sampling makes available for free. The stochastic machine hands you an uncertainty estimator (run it a few times and watch the spread); treating it as a retrieval system throws that estimator away.

---

## 1.7 The bridge: confident, and invisibly wrong

Everything above is, in a sense, good news: output is sampled, sampling is controllable, and the controls are deducible from distribution shape. But the same mechanism carries a threat that the rest of Act One exists to confront.

The distribution the model samples from maximizes the probability of *plausible* continuations — sequences that resemble the training data. Nothing in $\prod_t P(x_t \mid x_{<t})$ references truth (Ch. 0, §0.5). So the machine is exactly as fluent when it is right as when it is wrong. A sharply peaked distribution produces a confident-sounding answer whether the peak sits on a true token or a false-but-plausible one. The sampling machinery cannot tell the difference from the inside; neither, from the surface, can you.

This is the failure that sampling makes possible and *invisible*: the model can be confidently, fluently wrong, with the same texture it has when it is confidently right. Run-to-run variability gives you a partial tell (a wobbling answer signals a flat distribution, hence uncertainty), but a *peaked distribution on a wrong token* gives you a stable, confident error with no surface signal at all.

If every output is sampled, when is it confidently wrong — and how would you ever know? That is Chapter 2.

---

## Exercises

1. **(Understand)** A colleague insists the model "remembers" the answer to a factual question because it gives the same response every time at the default settings. Using the mechanism from §1.2, explain in one paragraph why consistent output does *not* imply retrieval, and describe the single experiment that would distinguish "peaked distribution" from "stored fact." (Hint: there isn't one from the outside — explain why, and what that implies.)

2. **(Apply)** Pick two tasks: one with a broad answer space (e.g., "suggest a tagline") and one with a narrow one (e.g., "what is 7 times 8"). Predict, *before running*, how output variability will respond to raising temperature from 0.2 to 1.0 on each. State your predictions as falsifiable claims tied to distribution shape.

3. **(Apply / Produce)** Run the experiment from Exercise 2 if you have model access (or describe the protocol precisely if you do not). For each task, send the fixed prompt at least 10 times at each temperature, record the outputs, and report: how many *distinct* outputs you got, and whether the result matched your prediction. Produce a short table (task × temperature × distinct-output count) and one paragraph interpreting any mismatch in terms of the actual distribution shape you must have been sampling.

4. **(Analyze)** Wang & Zhou (2024) elicit reasoning by decoding changes with the prompt fixed; Kojima et al. (2022) elicit it by changing the prompt with decoding fixed. Argue, using the "both are operations on the same distribution" framing from §1.5, when you would prefer each lever in a real system. Name one constraint (e.g., API surface, latency, cost) that would force the choice.

5. **(Evaluate)** A teammate proposes: "To make our summarizer reliable, set temperature to 0 — then it's deterministic and we're done." Critique this in terms of the chapter. Identify (a) the sense in which it is true, (b) two senses in which it is false or risky (reference §1.2's determinism caveat and §1.4's greedy-decoding caveat), and (c) what you would measure instead to claim the summarizer is "reliable."

---

## What would change my mind

The central claim is that every LLM output is best understood as a sample from a learned conditional distribution, and that this — not retrieval, not pure randomness — explains both run-to-run divergence and its controllability. What would force a revision: a documented, reproducible regime in which a production model's run-to-run output variability is *not* governed by its sampling parameters — for example, a model whose outputs diverge substantially across runs at a genuine temperature of 0 with identical logits, *beyond* what floating-point/batching nondeterminism can account for, or a model whose output diversity is *invariant* to temperature/top-p across tasks of clearly different answer-space breadth. Either finding would mean some other mechanism (a stochastic component not described by the softmax-sampling picture) is driving behavior, and the "read every output as a sample from this distribution" foundation — which the entire book inherits — would need to be replaced rather than refined.

## Still puzzling

1. **How much run-to-run variability is "free uncertainty signal" versus noise?** §1.6 (Mycroft) suggests resampling reveals model uncertainty, but the mapping from "spread of outputs" to "calibrated confidence" is not established. When does output spread track real uncertainty, and when is it just stylistic wobble on a confident answer?
2. **Are prompt-levers and decoding-levers ever *non*-substitutable?** §1.5 claims they reach the same distribution. Is there a capability reachable only by decoding (e.g., the latent reasoning branches) that *no* prompt can surface, or vice versa? `[TODO: check whether Wang & Zhou or follow-ups test prompt-equivalence of CoT-decoding]`
3. **What exactly is a "step-shaped trajectory"?** Wang et al. (2023) show invalid rationales work nearly as well as valid ones, implying CoT conditions trajectory *shape*. But "shape" is doing heavy lifting and is not formally characterized at the token-probability level. Interpretability work that located what changes in the distribution under CoT would settle a question Ch. 8 also leaves open.

---

## References

- Wang, X., & Zhou, D. (2024). Chain-of-Thought Reasoning Without Prompting. *NeurIPS 2024* (Google DeepMind). `[verify arXiv:2402.10200]` — reasoning paths elicited by decoding alone, prompt fixed; the chapter's central evidence that reasoning lives in the distribution.
- Kojima, T., Gu, S. S., Reid, M., Matsuo, Y., & Iwasawa, Y. (2022). Large Language Models are Zero-Shot Reasoners. *NeurIPS 2022*. `[verify arXiv:2205.11916]` — "Let's think step by step"; the prompt-side lever to the same latent reasoning.
- Wei, J., Wang, X., Schuurmans, D., Bosma, M., Ichter, B., Xia, F., Chi, E., Le, Q., & Zhou, D. (2022). Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. *NeurIPS 2022*. `[verify arXiv:2201.11903]` — few-shot CoT; emergence with scale.
- Wang, B., Min, S., Deng, X., Shen, J., Wu, Y., Zettlemoyer, L., & Sun, H. (2023). Towards Understanding Chain-of-Thought Prompting: An Empirical Study of What Matters. *ACL 2023*. `[verify arXiv:2212.10001]` — invalid rationales recover 80–90% of valid-CoT performance; relevance and ordering matter more than correctness.
- Meincke, L., Mollick, E. R., Mollick, L., & Shapiro, D. (2025). Prompting Science Report 2: The Decreasing Value of Chain of Thought in Prompting. Wharton Generative AI Labs. `[verify arXiv:2506.07142 / SSRN 5285532]` — CoT adds variance and can hurt on reasoning-tuned models; the scope condition referenced in §1.5.
- Brown, T., et al. (2020). Language Models are Few-Shot Learners (GPT-3). *NeurIPS 2020*. `[verify arXiv:2005.14165]` — in-context learning; background for the sampling-conditioned-on-context view.

---

**Tags:** sampling-not-retrieval, autoregressive, temperature-as-control, output-variability, reasoning-in-the-distribution, cot-decoding, probabilistic-event, distribution-shape
