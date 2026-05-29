> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft.

---

# Chapter 0 — Foundations: Sampling, Logits, and the Shape of a Distribution

*The optional front-load: what an LLM is actually emitting when it emits a token*

**Author:** Nik Bear Brown
**Editor:** Nik Bear Brown

---

## Suggested titles

1. **Foundations: Sampling, Logits, and the Shape of a Distribution**
2. **Before the First Token: Softmax, Temperature, and the Truncated Tail**
3. **The Number Behind the Word: Reading an LLM as a Probability Engine**

---

## TL;DR

Every token a language model emits is a draw from a probability distribution the model computes fresh at each step. The model produces a vector of raw scores called *logits* — one per vocabulary item — and a function called *softmax* converts that vector into a proper probability distribution that sums to one. Three knobs reshape that distribution before a token is drawn: **temperature** rescales the logits (flattening or sharpening the distribution by dividing every score by a constant $T$ before softmax), and **top-k** and **top-p (nucleus)** sampling *truncate* it (discarding the long tail of low-probability tokens before drawing). Understanding these three operations — one rescaling, two truncations — is the entire mechanical foundation for everything that follows: it is why identical prompts diverge (Ch. 1), why fluent text can be confidently wrong (Ch. 2), and why "set temperature to 0" is sometimes a bug rather than a safety measure. This chapter is the optional math front-load; if your course assumes softmax and decoding, skip to Ch. 1.

---

## Learning objectives

By the end of this chapter you should be able to:

1. **(Understand)** Describe an LLM's output at each step as a sample from a conditional probability distribution over the vocabulary, and state what the distribution is conditioned on.
2. **(Understand)** Compute, by hand, the softmax of a small logit vector and verify it forms a valid probability distribution.
3. **(Apply)** Predict the directional effect of changing temperature on a given logit vector — which tokens gain probability mass and which lose it — and explain why $T \to 0$ approaches greedy (argmax) decoding.
4. **(Apply)** Distinguish top-k from top-p truncation mechanically, and identify a distribution shape where they select different candidate sets.
5. **(Analyze)** Name one decoding configuration that produces a documented failure (e.g., low-temperature looping) and explain it in terms of distribution shape.

## Prerequisites

This is the foundational chapter. It assumes only the book's stated baseline: basic probability (a distribution sums to one; conditional probability), exponentials and logarithms, and comfort reading a vector. No transformer internals are required — we treat the network up to the final layer as a black box that emits a vector of scores. Chapters 1 onward build directly on this material; Ch. 1 (The Stochastic Machine) turns the mechanics here into behavioral consequences.

---

## 0.1 The number behind the word

Open any chat model. Type *"The capital of France is"* and watch it answer *"Paris."* It feels like a lookup — like the model reached into a table, found the row for France, and read off the cell. It is not a lookup. Something more peculiar happened, and the peculiarity is the whole subject of this book.

Here is what actually happened. The model read your tokens, ran them through its layers, and at the final step produced a list of numbers — one number for *every* token in its vocabulary. Modern vocabularies run roughly 50,000 to 130,000 entries `[verify current vocab sizes for GPT-4o / Claude / Llama 3]`, so this list is a vector with tens of thousands of components. The entry for ` Paris` was high. The entry for ` Lyon` was lower but not zero. The entry for ` Tokyo` was lower still. The entry for ` banana` was very low — but, and this is the load-bearing fact, *not zero*. Every token in the vocabulary received a score. The model then converted those scores into probabilities and *drew a sample*. It happened to draw ` Paris` because ` Paris` had most of the probability mass. On a different draw, with the dial set differently, it might have drawn ` Lyon`.

The model did not retrieve "Paris." It sampled it. The answer felt deterministic because the distribution was sharply peaked — almost all the mass sat on one token — but the machinery underneath was probabilistic the whole time. Change the shape of that distribution and the same prompt yields different text. That is the mechanism this chapter makes precise, before Ch. 1 turns it into a behavioral law.

The name for the raw score vector is **logits**. The name for the function that turns logits into probabilities is **softmax**. We will earn both names by mechanism first.

---

## 0.2 From scores to probabilities: the softmax

We have a vector of raw scores, one per vocabulary token. Call them $z_1, z_2, \ldots, z_V$ where $V$ is the vocabulary size. These are the **logits**. They are arbitrary real numbers: they can be negative, they can be large, they do not sum to anything in particular. They are not yet probabilities.

To draw a token we need a genuine probability distribution: every entry non-negative, the whole thing summing to one. The function that does this is the **softmax**:

$$
p_i = \frac{e^{z_i}}{\sum_{j=1}^{V} e^{z_j}}
$$

Read it mechanically. Exponentiate each logit ($e^{z_i}$) — this forces every term positive, since $e^x > 0$ for all real $x$, and it stretches gaps: a logit that is larger by a fixed amount becomes *multiplicatively* larger after exponentiation. Then divide each exponentiated score by the sum of all of them. Dividing by the total guarantees the results sum to one. So $p_i$ is non-negative and $\sum_i p_i = 1$: a valid distribution.

Do it by hand on three tokens so the arithmetic is not abstract. Suppose three candidate tokens have logits $z = (2.0,\ 1.0,\ 0.1)$.

- Exponentiate: $e^{2.0} \approx 7.389$, $e^{1.0} \approx 2.718$, $e^{0.1} \approx 1.105$.
- Sum: $7.389 + 2.718 + 1.105 = 11.212$.
- Divide: $p \approx (0.659,\ 0.242,\ 0.099)$.

Check: $0.659 + 0.242 + 0.099 = 1.000$. The token with logit $2.0$ holds about 66% of the mass; the token with logit $0.1$ holds about 10%. A *small* logit gap (here, $2.0$ vs $1.0$, a gap of one) became a sizable probability gap (66% vs 24%) because of the exponential. This is why softmax is "soft": it does not hand all the mass to the winner the way a hard `argmax` would, but it does concentrate mass on the leaders. Hold onto that exponential — temperature acts on it directly.

**Common misconception.** *"Logits are probabilities, just unnormalized."* Not quite, and the difference matters. Logits live on an additive scale; probabilities live on a multiplicative one after exponentiation. Adding a constant $c$ to *every* logit changes nothing about the resulting distribution — the constant cancels top and bottom ($e^{z_i + c} = e^c e^{z_i}$, and $e^c$ factors out of both numerator and denominator). But *multiplying* every logit by a constant — which is exactly what temperature does — changes everything. The mistake of treating logits as "probabilities you just have to normalize" hides the one operation (scaling) that temperature exploits.

---

## 0.3 Temperature: one constant that reshapes the whole curve

Now the first knob. **Temperature** is a single positive number $T$ that we divide every logit by *before* applying softmax:

$$
p_i = \frac{e^{z_i / T}}{\sum_{j=1}^{V} e^{z_j / T}}
$$

That is the entire definition. One division, applied to every logit, inside the exponential. The name "temperature" is borrowed from statistical physics, where the Boltzmann distribution has exactly this form and $T$ is the physical temperature of a system — high temperature spreads a system across many states, low temperature pins it to the lowest-energy one. The borrowed intuition is exact here too, so the name is earned, not decorative. But you do not need the physics; you need the algebra of "divide before exponentiating."

Watch what the division does to our three-token example, $z = (2.0,\ 1.0,\ 0.1)$.

**At $T = 1$** (the neutral setting — dividing by one changes nothing) we recover the distribution from §0.2: $p \approx (0.659,\ 0.242,\ 0.099)$.

**At $T = 0.5$** (low temperature) we divide the logits by $0.5$, i.e. *multiply them by two*: $z/T = (4.0,\ 2.0,\ 0.2)$.
- Exponentiate: $e^{4.0} \approx 54.60$, $e^{2.0} \approx 7.389$, $e^{0.2} \approx 1.221$.
- Sum $\approx 63.21$; divide: $p \approx (0.864,\ 0.117,\ 0.019)$.
- The leader's share jumped from 66% to 86%. The distribution got **sharper** — mass concentrated on the top token.

**At $T = 2$** (high temperature) we divide by two: $z/T = (1.0,\ 0.5,\ 0.05)$.
- Exponentiate: $e^{1.0} \approx 2.718$, $e^{0.5} \approx 1.649$, $e^{0.05} \approx 1.051$.
- Sum $\approx 5.418$; divide: $p \approx (0.502,\ 0.304,\ 0.194)$.
- The leader's share fell from 66% to 50%; the long-shot token climbed from 10% to 19%. The distribution got **flatter** — mass spread toward the tail.

So the mechanism is clean. **Low $T$ sharpens** (concentrates mass on the leaders, output becomes more repetitive and "confident"). **High $T$ flattens** (spreads mass toward unlikely tokens, output becomes more varied and, eventually, more incoherent). The two limits make this precise:

- As $T \to 0$, the division blows up the gaps without bound; in the limit, the top token's probability goes to one and everything else to zero. This is **greedy decoding** (also called argmax decoding): always take the single highest-logit token. So "temperature zero" is not a separate mechanism — it is the limiting case of temperature, and it is *deterministic* in the sense that the same logits always yield the same token. (Same logits — but floating-point nondeterminism, batching, and model updates mean "temperature 0" is not a guarantee of bit-identical output across runs in production. Ch. 1 returns to this.)
- As $T \to \infty$, every $z_i/T \to 0$, so every $e^{z_i/T} \to 1$, and the distribution flattens to *uniform*: every token equally likely, the prompt's influence washed out entirely. Pure noise.

**The temperature scale, drawn on the page:**

```
 T → 0            T = 1            T → ∞
 ┌──────────┐     ┌──────────┐     ┌──────────┐
 │ █        │     │ █        │     │ ▃ ▃ ▃ ▃ ▃│
 │ █        │     │ █ ▃      │     │ ▃ ▃ ▃ ▃ ▃│
 │ █        │     │ █ ▃ ▂    │     │ ▃ ▃ ▃ ▃ ▃│
 └──────────┘     └──────────┘     └──────────┘
  greedy /          neutral          uniform /
  argmax            (default)        pure noise
  deterministic     calibrated       prompt washed out
```

**Common misconception.** *"Temperature 0 is the safe default — it removes randomness, so it removes errors."* It removes *sampling* randomness, not error. Greedy decoding always picks the locally highest-probability token, which can walk the model into a globally worse continuation, and on some models it triggers pathological **looping** — the model gets pinned on a high-probability token that re-licenses itself, and repeats. Google's own Gemini 3 API guidance recommends keeping temperature at the default 1.0 because lowering it can cause looping and degradation on reasoning tasks, and multiple Gemini 2.5 production incidents in early 2026 showed infinite repetition loops `[verify Gemini guidance URL and incident dates]`. So "always use temperature 0" is a folk rule with a documented, model-specific counterexample. Temperature is a tunable parameter, not a safety setting.

A note for builders: APIs differ on whether they accept $T = 0$ literally (some clamp it to a tiny epsilon to avoid dividing by zero), and the *useful* range of $T$ is model-specific. There is no universal "correct" temperature; there is a temperature that, for *your* model and *your* task, produces the diversity-versus-determinism trade-off you want — a claim you settle empirically, which is the book's whole posture.

---

## 0.4 Truncation: top-k and top-p

Temperature *rescales* the distribution but leaves every token in play — even at low $T$, that ` banana` token from §0.1 retains a microscopic but nonzero probability, and across thousands of tokens those microscopic tails can sum to a meaningful chance of drawing something absurd. The other two knobs address this differently: instead of reshaping the curve, they **cut off its tail** before sampling. These are *truncation* methods.

### Top-k sampling

**Top-k** is the blunter of the two. Mechanism: sort the tokens by probability, keep only the $k$ most probable, zero out everything else, and *renormalize* the survivors so they sum to one again. Then sample from those $k$.

Take a five-token example with post-softmax probabilities:

$$
p = (\underbrace{0.40}_{A},\ \underbrace{0.25}_{B},\ \underbrace{0.20}_{C},\ \underbrace{0.10}_{D},\ \underbrace{0.05}_{E})
$$

With **top-k, $k = 3$**: keep $A, B, C$ (the three largest), discard $D, E$. The survivors sum to $0.40 + 0.25 + 0.20 = 0.85$, so renormalize by dividing each by $0.85$:

$$
p' = (0.471,\ 0.294,\ 0.235,\ 0,\ 0)
$$

Now $D$ and $E$ can never be drawn. The model samples among $A, B, C$ with the rescaled probabilities. The point of top-k is to keep the long, weird tail out of reach while preserving randomness among the plausible leaders.

The weakness of top-k is that $k$ is *fixed* regardless of the distribution's shape. When the model is genuinely uncertain — mass spread across, say, fifteen reasonable tokens — a $k$ of 3 amputates twelve good candidates. When the model is nearly certain — one token at 0.97 — a $k$ of 3 drags two near-zero tokens into contention. The cut is the same size whether the distribution is a needle or a plateau. That mismatch is exactly what the next method fixes.

### Top-p (nucleus) sampling

**Top-p**, also called **nucleus sampling** and introduced by Holtzman et al. (2020) `[verify: "The Curious Case of Neural Text Degeneration," arXiv:1904.09751]`, makes the cut *adaptive*. Mechanism: sort tokens by probability, then walk down the sorted list accumulating probability mass until the running total first reaches the threshold $p$; keep exactly that set (the "nucleus"), discard the rest, renormalize, and sample.

Same five-token example, $p = (0.40, 0.25, 0.20, 0.10, 0.05)$, with **top-p, $p = 0.80$**:

- Accumulate: $A$ alone is $0.40$ (below $0.80$). $A + B = 0.65$ (below). $A + B + C = 0.85$ (first time we reach or exceed $0.80$). Stop.
- Nucleus = $\{A, B, C\}$. Discard $D, E$. Renormalize over $0.85$: $p' = (0.471, 0.294, 0.235, 0, 0)$.

Here top-p with $p = 0.80$ happened to select the *same* three tokens as top-k with $k = 3$. They diverge the moment the distribution changes shape. Consider a flatter distribution, $q = (0.22, 0.21, 0.20, 0.19, 0.18)$:

- **Top-k, $k = 3$** still keeps exactly three tokens ($0.22, 0.21, 0.20$), discarding two perfectly reasonable candidates at $0.19$ and $0.18$.
- **Top-p, $p = 0.80$** accumulates $0.22 + 0.21 + 0.20 + 0.19 = 0.82 \ge 0.80$, keeping *four* tokens. The nucleus grew because the model was less certain.

And on a peaked distribution, $r = (0.95, 0.02, 0.01, 0.01, 0.01)$:

- **Top-k, $k = 3$** keeps three tokens — including two at 0.01 that contribute almost nothing but two units of noise.
- **Top-p, $p = 0.80$** keeps *one* token ($0.95 \ge 0.80$), correctly collapsing to near-greedy behavior when the model is confident.

That is the whole reason top-p is usually preferred: **the size of the candidate set tracks the model's uncertainty.** Wide when the model is unsure, narrow when it is confident — which is the behavior you actually want from a truncation rule.

**Common misconception.** *"Top-p of 0.9 means I keep 90% of the tokens."* No — it means you keep the smallest *set of tokens* whose *probability mass* sums to at least 0.9. On a peaked distribution that can be a single token; on a flat one it can be hundreds. The threshold is on cumulative *probability*, not on token count. (Token count is what top-*k* controls; conflating the two is the most common decoding bug in practitioner code.)

### The order of operations

Temperature and truncation compose, and the order is conventionally: apply temperature to the logits, softmax to get probabilities, *then* truncate (top-k and/or top-p) on those probabilities, renormalize, and sample. So in a typical API call with `temperature=0.7, top_p=0.9` the model first sharpens the curve a little (T < 1), then keeps the nucleus, then draws. Setting `temperature=0` short-circuits the rest: there is nothing to truncate when one token holds all the mass. Knowing this order lets you reason about *why* two configurations that look similar behave differently — a skill Ch. 1 leans on hard.

---

## 0.5 What the distribution is conditioned on (and why this is the whole book)

One more precision, and it is the bridge to everything ahead. At every step the model does not produce *a* distribution — it produces a distribution *conditioned on the entire sequence so far*. Formally, if $x_1, \ldots, x_{t-1}$ are the tokens emitted up to now (your prompt plus whatever the model has already generated), the model defines

$$
P(x_t \mid x_1, \ldots, x_{t-1})
$$

and samples $x_t$ from it; then it appends $x_t$ and computes $P(x_{t+1} \mid x_1, \ldots, x_t)$, and so on. The probability of a whole output is the product of these conditional steps, the **chain rule** of probability:

$$
P(x_1, \ldots, x_n) = \prod_{t=1}^{n} P(x_t \mid x_{<t})
$$

This single equation is why prompt engineering is engineering. The prompt is the conditioning context $x_{<t}$ at the first generated step. Changing the prompt changes every conditional distribution downstream of it. You are not "asking" the model a question; you are *setting the conditions* under which a sequence of samples is drawn. And because the output feeds back in as conditioning for the next token (each $x_t$ becomes part of the context for $x_{t+1}$), a single early sampling accident — one low-probability token drawn at step 3 — reshapes every distribution after it. That feedback is why two runs of the identical prompt can diverge into entirely different answers, the phenomenon Ch. 1 opens on.

It is also why **a fluent sentence carries no guarantee of truth.** The chain rule maximizes the probability of *plausible-looking sequences* — sequences that resemble the training distribution — not true ones. Plausibility and truth are computed by the same machinery and are not the same quantity. That orthogonality is the subject of Ch. 2. The math is already on the page: nothing in $\prod_t P(x_t \mid x_{<t})$ references a fact, only a learned conditional distribution over tokens.

**Common misconception.** *"The model knows the answer and is choosing how to phrase it."* There is no separate "answer" stored apart from the distribution. The answer *is* the sequence of samples. When the distribution is sharply peaked on the correct token (capital of France), the sampling reliably lands right and it looks like knowledge. When the distribution is diffuse or peaked on a plausible-but-wrong token, the same sampling machinery produces a confident error. Nothing in the mechanism distinguishes the two cases from the inside — which is the uncomfortable foundation the rest of the book is built to engineer around.

---

## Exercises

1. **(Understand)** Given logits $z = (3.0,\ 1.5,\ 0.5,\ -1.0)$, compute the softmax distribution at $T = 1$ by hand (you may approximate $e^x$). Verify it sums to approximately one. Then state, *without recomputing*, which direction each probability will move when you raise the temperature to $T = 2$, and justify your prediction from the mechanism.

2. **(Apply)** Recompute the distribution from Exercise 1 at $T = 0.5$. By how many percentage points does the top token's probability change relative to $T = 1$? Write one sentence connecting the magnitude of that change to the size of the logit gaps.

3. **(Apply)** You are given the post-softmax distribution $p = (0.50,\ 0.18,\ 0.12,\ 0.10,\ 0.06,\ 0.04)$. (a) Which tokens survive **top-k with $k = 4$**? (b) Which survive **top-p with $p = 0.85$**? (c) Construct a *different* six-token distribution on which top-k ($k=4$) and top-p ($p=0.85$) select different candidate sets, and explain in one sentence what feature of your distribution causes the divergence.

4. **(Apply / Produce)** Write a 150–250 word "decoding configuration note" you could paste into a project README. It must (a) state a default temperature and top-p for a *named* task (e.g., extracting structured fields from invoices vs. brainstorming product names), (b) justify each value mechanically in terms of distribution shape, and (c) name one failure mode the configuration is chosen to avoid. Use the temperature and truncation mechanics from this chapter, not folk rules.

5. **(Analyze)** Explain, in terms of distribution shape and the conditioning feedback loop of §0.5, why lowering temperature can *increase* the chance of repetition/looping on some models, even though low temperature is usually described as "more reliable." Identify what you would measure to confirm looping is the failure (rather than, say, the prompt itself).

---

## What would change my mind

The central claim of this chapter is mechanical and largely settled: an autoregressive LLM emits a sample from a softmax-normalized, temperature-scaled, optionally truncated distribution over its vocabulary, conditioned on the running sequence. What would force a substantive revision is a documented, reproducible class of production models whose token selection is *not* describable as sampling from such a distribution — for instance, a decoding architecture that selects tokens by a non-probabilistic search over full sequences (beyond beam search, which is still scoring sequences by these same conditional probabilities) and that is empirically shown to make the per-step softmax framing predictively wrong for its outputs. If a widely deployed model's observed output statistics could not be reproduced by *any* setting of temperature/top-k/top-p over its logits, the "read the output as a sample from this distribution" framing — and the rest of Part I that rests on it — would need rebuilding rather than refinement.

## Still puzzling

1. **Why these particular defaults?** Vendors converge on temperatures near 0.7–1.0 and top-p near 0.9–1.0, but the choice is largely empirical folklore tuned to perceived output quality. Is there a principled, task-independent argument for a default, or is it irreducibly model- and task-specific? `[TODO: survey current vendor defaults with citations]`
2. **What is the right truncation when the distribution is genuinely bimodal** — two sharply separated good answers with a dead zone between? Neither top-k nor top-p has a notion of "modes"; both just walk the sorted tail. Do mode-aware decoders matter in practice, or does the chain-rule feedback wash the question out?
3. **How much of "temperature 0 is deterministic" survives real infrastructure?** Floating-point non-associativity, request batching, and silent model updates all perturb logits. Is there a clean way to characterize the residual nondeterminism a user sees at $T = 0$? (Ch. 1 raises this; it is not resolved here.)

---

## References

- Holtzman, A., Buys, J., Du, L., Forbes, M., & Choi, Y. (2020). The Curious Case of Neural Text Degeneration. *ICLR 2020*. `[verify arXiv:1904.09751]` — origin of nucleus (top-p) sampling and the degeneration analysis motivating truncation.
- Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., Kaiser, Ł., & Polosukhin, I. (2017). Attention Is All You Need. *NeurIPS 2017*. `[verify arXiv:1706.03762]` — the transformer; the softmax output layer over the vocabulary is standard here.
- Goodfellow, I., Bengio, Y., & Courville, A. (2016). *Deep Learning*. MIT Press. — standard reference for the softmax function and its properties (Ch. 6). `[verify chapter/section for softmax + temperature]`
- Ackley, D. H., Hinton, G. E., & Sejnowski, T. J. (1985). A Learning Algorithm for Boltzmann Machines. *Cognitive Science*, 9(1). `[verify]` — the statistical-physics origin of the temperature parameter in the Boltzmann/Gibbs distribution form softmax-with-temperature mirrors.
- Fan, A., Lewis, M., & Dauphin, Y. (2018). Hierarchical Neural Story Generation. *ACL 2018*. `[verify arXiv:1805.04833]` — early use of top-k sampling for generation.
- Google. Gemini API generation-configuration guidance (temperature and looping). `[verify exact URL and version; documents the low-temperature looping caution referenced in §0.3]`

---

**Tags:** softmax, logits, temperature, top-k, top-p, nucleus-sampling, autoregressive-decoding, chain-rule, distribution-shape
