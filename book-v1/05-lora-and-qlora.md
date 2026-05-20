> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft. First chapter drafted for this book.
>
> **Policy flag — theory-authored-by-student.** Per the book's authorship convention, Parts I–V are Nik-authored theory and Part VI holds student case studies. This chapter is an exception: a student (Shwetanshu Subhash Deshmukh) wrote the theory for a Part IV slot. Editor decision required on how to handle: (a) keep as student-authored theory; (b) rewrite in Nik's voice with Shwetanshu's name as contributor; (c) move to Part VI as a case study on "Choosing LoRA vs. QLoRA in a constrained-hardware deployment." Flagged in the outline.

---

# Chapter 14 — LoRA and QLoRA

*Parameter-Efficient Fine-Tuning*

**Author:** Shwetanshu Subhash Deshmukh
**Editor:** Nik Bear Brown

---

## Suggested titles

1. **LoRA and QLoRA: Parameter-Efficient Fine-Tuning**
2. **Three Fine-Tuning Strategies, Three Failure Modes: The Architectural Decision Disguised as a Cost Decision**
3. **Shared-Base, Adapter-Routed: Why Cheap Fine-Tuning Introduces Failures That Expensive Fine-Tuning Doesn't Have**

---

## TL;DR

The choice between full fine-tuning, LoRA, and QLoRA is usually framed as a cost optimization — you want the same result for less GPU time — but it's really an architectural decision about *serving topology*, and each topology introduces failure modes the others don't have. LoRA's low-rank decomposition and QLoRA's hybrid 4-bit/FP16 precision architecture are the mechanisms; adapter misrouting and rank starvation are the failures the cheap options add to your system.

---

## Learning objectives

By the end of this chapter you should be able to:

1. Derive the LoRA parameterization $W = W_0 + BA$ from first principles, and state the memory and compute savings relative to full fine-tuning.
2. Explain QLoRA's hybrid-precision architecture: which weights are 4-bit NF4, which are FP16, and where computation happens.
3. Apply a five-criterion decision matrix (memory, task difficulty, deployment topology, monitoring, update frequency) to choose among full fine-tuning, LoRA, and QLoRA.
4. Diagnose two failure modes that are specific to shared-base adapter architectures: **adapter misrouting** (silent wrong-adapter selection) and **rank starvation** (capacity-floor violation on hard tasks).
5. Specify at least one architectural defense (verification layer, rank ablation, router instrumentation) for each failure mode.

## Prerequisites

Chapter 13 (SFT vs. RAG) — assumes the reader has already made the decision to fine-tune rather than retrieve, and is now choosing *how* to fine-tune. Linear algebra through matrix decomposition (SVD). Familiarity with gradient descent at the level of "the optimizer updates weights using the gradient of the loss."

---

## 14.1 The $200 fine-tune that silently misrouted customers

A team fine-tunes five adapters — one per customer segment — on top of a single base model. They use LoRA because the total GPU cost is about $200, versus roughly $2,000 for five full fine-tunes. The adapters train cleanly. The eval harness passes. The system ships.

Three weeks into production, a customer-success team notices that approximately 8% of replies to enterprise-segment inquiries are subtly wrong in a specific way: they use SMB-segment pricing terminology. Not all of the replies, and not obviously — the language is fluent, the format is correct, the responses read like legitimate answers. A careful audit eventually traces the failure to the adapter router: a classification step that decides which of the five adapters handles each incoming query. Under load, the router's confidence scores cluster close to the decision boundary for a class of queries the router wasn't trained on, and roughly 8% of those queries end up being handled by the wrong adapter. Each adapter produces fluent, well-formatted output conditioned on its own fine-tuning distribution. The output looks right. The output is wrong.

Nothing about this failure exists in a full-fine-tuning architecture. Five independent fine-tuned models don't share a router; each model is its own serving endpoint. A customer goes to the enterprise endpoint or doesn't. There is no possibility of a silent routing failure, because there is no router.

The team had framed the $200-vs-$2,000 choice as a cost optimization. It wasn't. It was a choice about **serving topology** — five independent models versus one shared base with five adapters — and the cheaper topology added a failure mode (adapter misrouting) that the more expensive topology didn't have. The model weights in the LoRA case were identical to what you'd get from an equivalent full fine-tune on each segment. The failure lived entirely in the architecture around the model, not in the model's capabilities.

That's the chapter. LoRA and QLoRA aren't cheaper versions of full fine-tuning. They are *different architectures* whose cheapness is a consequence of specific structural decisions, and those decisions introduce specific failures you have to design for.

---

## 14.2 Three strategies, three architectures

Three fine-tuning strategies show up in practice. Each is a different commitment about where updates happen, how they're stored, and how the resulting system gets served.

**Full fine-tuning.** Every weight of the base model is updated during training. After training, the model is an entirely new object — its weights diverge from the base model's weights everywhere. Serving topology: independent models, one per task. If you fine-tune for five customer segments, you deploy five models, each with its own full-size weight file. GPU memory during training: dominated by parameter gradients and optimizer states, typically 4× the model's FP16 size for Adam.

**LoRA (Low-Rank Adaptation).** Base model weights are frozen. Trainable parameters are introduced as small low-rank matrices added to specific weight matrices in the base (usually the attention query and value projections). After training, the adapter is a small file (typically 0.1–1% of the base model's size). Serving topology: one shared base model in memory, multiple adapters loaded alongside, a router that selects which adapter to apply per query. ([Hu et al., 2021](https://arxiv.org/abs/2106.09685)).

**QLoRA.** Same adapter architecture as LoRA. Difference: the frozen base model's weights are stored in a compressed 4-bit format (NF4 — NormalFloat 4-bit) to reduce memory. The adapter weights themselves, and all computation, remain in FP16/BF16. QLoRA adds Paged Optimizers and Double Quantization for further memory reduction. Serving topology: same as LoRA (shared base, routed adapters) but the shared base takes roughly 4× less memory. ([Dettmers et al., 2023](https://arxiv.org/abs/2305.14314)).

### "Fine-tuning" hides three different decisions

Engineering discussions often collapse three separate questions into the single phrase *"let's fine-tune."* They are not the same question.

- **How is training parameterized?** Full-model gradient updates vs. low-rank adapter updates. This decision determines training cost.
- **How are weights stored?** Full-precision FP16 across the whole model, vs. FP16 for trainable weights and 4-bit NF4 for frozen base weights. This decision determines memory at rest.
- **How is the trained system served?** One model per task, or one shared base with routed adapters. This decision determines failure modes.

Full fine-tuning picks *all three* in the "expensive" direction. LoRA picks "cheap" on training and "shared base" on serving, but keeps "full precision" on storage. QLoRA picks "cheap" on all three. The three strategies are not points on a single cost axis; they are different combinations of three distinct choices. Which is why the decision matrix has more than one row.

---

## 14.3 LoRA's mechanism — and what the rank is doing

LoRA parameterizes weight updates as a low-rank matrix. For a base weight matrix $W_0 \in \mathbb{R}^{d \times k}$, a full fine-tune replaces $W_0$ with $W_0 + \Delta W$ where $\Delta W \in \mathbb{R}^{d \times k}$ has the same dimensions as $W_0$. That's a lot of parameters: if $d = k = 4096$, then $\Delta W$ has about 17 million parameters per matrix.

LoRA's insight is that $\Delta W$ doesn't need to have that many degrees of freedom — task-specific adaptations tend to live in a low-dimensional subspace. The paper empirically demonstrates this by measuring the *intrinsic dimension* of the adaptation: the smallest rank at which fine-tuning still works. For many downstream tasks, the answer is surprisingly low — sometimes as small as 4 or 8. This connects to earlier results on the intrinsic dimensionality of fine-tuning ([Aghajanyan et al., 2020](https://arxiv.org/abs/2012.13255)).

Exploiting that, LoRA parameterizes the update as the product of two small matrices:

$$\Delta W = BA$$

where $B \in \mathbb{R}^{d \times r}$, $A \in \mathbb{R}^{r \times k}$, and $r \ll \min(d, k)$. The forward pass becomes:

$$h = W_0 x + BA x$$

Only $B$ and $A$ are trained. $W_0$ is frozen. The total number of trainable parameters is $r(d + k)$ — for $r=8$ and $d=k=4096$, that's 65,536 parameters per matrix instead of 16,777,216. A reduction of roughly **256×**.

One additional detail worth knowing: LoRA scales the adapter's contribution by a factor $\alpha/r$, where $\alpha$ is a hyperparameter. So the effective forward pass is:

$$h = W_0 x + \frac{\alpha}{r} BA x$$

This scaling decouples the learning rate from the rank. A rank-4 adapter with $\alpha = 8$ and a rank-32 adapter with $\alpha = 64$ both multiply their contribution by 2, so you can change $r$ without re-tuning the optimizer.

### Why rank is a capacity floor

Rank matters because it is a hard architectural upper bound on how much the adapter can change the model's behavior. A rank-$r$ update can represent any function of the form "add a linear combination of $r$ vectors to the base weight matrix, decomposed into $r$ directions." If the task genuinely requires more directions than $r$ allows, the adapter cannot represent the change, regardless of how long you train or how clean the data is. This is the mechanism behind rank starvation, which we'll see in §14.5.

A practical guideline: start with $r = 8$ for most tasks, raise to $r = 16$ or $r = 32$ if the downstream eval plateaus below what a full fine-tune achieves. Numbers are rough; the right rank depends on the task and should be selected by ablation, not by intuition.

---

## 14.4 QLoRA's precision architecture — the correction that matters

The single most common misunderstanding about QLoRA is the belief that "QLoRA runs the model in 4-bit precision." It does not. QLoRA is a **hybrid-precision** system with three distinct components, and the distinction matters for memory reasoning, training behavior, and performance expectations.

**The frozen base weights are stored in 4-bit NF4.** NF4 (NormalFloat 4-bit) is a quantization scheme designed for weight distributions that are roughly normally distributed — which empirically, LLM weights are, after normalization. Each weight in the base model is represented using 4 bits instead of 16. That's the source of QLoRA's memory savings. These weights are *frozen*; they do not receive gradient updates.

**The adapter weights are stored in FP16/BF16.** The LoRA adapter matrices $B$ and $A$ are the *trainable* part of the system. They are not quantized. They live in 16-bit floating point throughout training, because gradient updates through quantized values lose information and destabilize training.

**Computation happens in FP16/BF16.** On each forward pass, the 4-bit base weights are **dequantized back to FP16** before any matrix multiplication. The forward pass of $h = W_0 x + BAx$ is an FP16 computation. Backward pass, gradients, and optimizer state all live in 16-bit. QLoRA does not get 4-bit speedup; it gets 4-bit *storage compression* on the portion of the model that doesn't change.

The two additional tricks QLoRA introduces:

- **Double Quantization** — the quantization constants used to decompress NF4 are themselves quantized. Saves about 0.4 bits per parameter on average.
- **Paged Optimizers** — optimizer state for the FP16 adapters is paged to CPU memory when GPU memory pressure is high, avoiding out-of-memory errors on gradient spikes.

Why this distinction matters for the decision matrix: QLoRA's memory savings come entirely from **storage compression of frozen weights**. They do not come from faster computation. If your bottleneck is training throughput rather than memory, QLoRA does not help. If your bottleneck is memory — you want to fine-tune a 70B model on a single GPU — QLoRA is the architecture that makes it possible, because the 70B base weights now fit in the VRAM you have, while the adapter training happens in the precision where gradients actually mean something.

This is the architectural correction at the heart of the chapter, and it was arrived at by rejecting a tempting but wrong analogy: that QLoRA "compresses the model into 4-bit." That framing is memorable and wrong. The model *stores in 4-bit* and *computes in 16-bit*. Getting this distinction right is the difference between a decision framework that works and one that tells you the wrong thing when your bottleneck isn't memory.

---

## 14.5 The decision matrix

Five criteria. One row per strategy.

| Criterion | Full fine-tuning | LoRA | QLoRA |
|---|---|---|---|
| **Training memory (for a 7B model, Adam)** | ~120 GB | ~20 GB | ~6 GB |
| **Representational capacity** | Full (entire weight space) | Rank-bounded (task-specific, often sufficient for $r \geq 8$) | Same as LoRA |
| **Serving topology** | Independent models per task | Shared base + routed adapters | Shared base (4-bit) + routed adapters |
| **Dominant failure mode** | Catastrophic forgetting under sequential fine-tunes (Ch. 16) | **Adapter misrouting** (silent); **rank starvation** on hard tasks | Same as LoRA, plus quantization-edge-case artifacts |
| **Update frequency that justifies the choice** | Rare (stable domains, single high-value task) | Frequent (multiple variants, routine retraining) | Frequent *and* memory-constrained |

The matrix is read per-row by the engineer deciding which strategy fits a specific deployment. A common failure mode of the decision itself is treating it as a one-axis optimization ("which is cheapest"). Cost is one criterion of five, and the other four matter at least as much when production failures start arriving.

Two failure modes are specific to the adapter architectures (LoRA and QLoRA) and require explicit architectural defenses. The following subsections walk through each.

### 14.5.1 Adapter misrouting — the silent failure

In a shared-base adapter architecture, a **router** decides which adapter handles each incoming query. Routers are themselves small classifiers — sometimes an embedding-similarity lookup, sometimes a learned classification head, sometimes a simple rule set. They are not the base LLM. They have their own training data, their own failure modes, and their own uncertainty.

When the router makes a wrong decision, the query is handled by an adapter trained on a different distribution. The adapter produces output conditioned on *its* fine-tuning signal — fluent, well-formatted, and confidently wrong for the actual query. Because all adapters share the base model's language fluency and output space, there is no syntactic signal that anything is off. The output looks normal.

**Defense.** A verification layer downstream of the adapter that compares the generated output against the query using a cheap semantic similarity check. For the customer-segment case, this might be: embed the query and the output; if cosine similarity between the output and exemplars from the adapter's training distribution is below a threshold, flag for review. Threshold selection matters — too high and legitimate novel queries trigger reviews; too low and misroutings slip through. In Shwetanshu's original research notes the threshold was set heuristically at 0.85 and flagged as "heuristic, not calibrated on validation data" — an honest limitation that a production deployment would close by running the verification layer against a labeled validation set and picking the threshold that maximizes the router's F1.

### 14.5.2 Rank starvation — the capacity-floor failure

A rank-$r$ adapter can represent at most a rank-$r$ update to the base weights. For tasks whose true adaptation lives in a higher-dimensional subspace, the adapter runs out of capacity. The model still produces output, because the base model is fluent on its own. The adapter just fails to push the output toward the task's true distribution on the hard cases — the cases where the adaptation needed to be strongest.

The diagnostic signature is a **split performance profile**: the adapter performs well on easy task instances (where small adjustments suffice) and degrades on hard ones (where larger adjustments are required). A team that evaluates on an easy-weighted holdout set sees a high average score and ships. Production then surfaces the failures one hard instance at a time.

**Defense.** Run a **rank ablation** during development: train adapters at $r = 4, 8, 16, 32, 64$ and plot the eval-score-vs-rank curve. If performance plateaus below the full-fine-tune ceiling at the highest rank you can afford, the adapter architecture may not be sufficient for the task. Consider full fine-tuning, or decompose the task so that separate adapters handle sub-tasks with lower intrinsic dimensionality each.

---

## 14.6 Back to the $200 fine-tune

The team in §14.1 wasn't wrong to reach for LoRA. For their workload — five customer segments, modest adaptation requirements, tight GPU budget — LoRA was a reasonable choice. What they missed was that **reaching for LoRA was a choice about serving topology**, and the topology they chose (shared base, routed adapters) had a failure mode (misrouting) that the topology they compared against (independent models) did not.

The architectural fix wasn't to abandon LoRA. It was to build a verification layer downstream of the router, calibrate its threshold on a labeled validation set, and treat the fraction of flagged queries as a first-class monitoring metric. Under that architecture, misrouting still happens — the router is still imperfect — but misrouted queries are caught before they reach the customer. The cost: an additional semantic-similarity computation per query, perhaps 10–50 milliseconds of latency. The savings: the $1,800 GPU differential was real; the misrouting failure was also real; the verification layer made the real savings retrievable without eating the real failure.

**Full fine-tuning** is the right answer when: the domain is stable, updates are rare, memory isn't a constraint, and independent model endpoints per task match your deployment's fault-isolation requirements.

**LoRA** is the right answer when: multiple task variants share enough base model capability that a single shared base makes sense, per-task adaptation is modest enough that rank-$r$ updates suffice, and you can afford the architectural overhead of a router and a verification layer.

**QLoRA** is the right answer when: all of the above *plus* training memory is the binding constraint. If you can fit a full-precision base in VRAM, QLoRA's quantization tricks buy you nothing and add complexity. If you can't, they make the whole enterprise possible.

The chapter's master argument: each of these three strategies produces systems that **fail in different ways**. The model weights in each case may be nearly equivalent on a held-out benchmark. The architectures around the model are different, and the failures are different. This is what it means to say that fine-tuning strategy is an architectural decision rather than a cost one. The cost is a consequence of the architecture; the architecture is the thing you're actually choosing.

### Connections forward

Chapter 15 covers RLHF, DPO, and Constitutional AI — alignment techniques that sit atop any of the three fine-tuning strategies and add their own failure modes (reward hacking, sycophancy amplification). Chapter 16 develops catastrophic forgetting formally, which is the failure mode full fine-tuning exhibits under sequential retraining and which LoRA partially mitigates by keeping the base frozen. Chapter 19 revisits the adapter-routing architecture as a production-system concern, and the verification-layer defense described here becomes part of the larger Prompt Stack governance discussed there.

---

**What would change my mind:** A well-documented production deployment of an adapter-routed system at moderate scale (≥ 3 adapters, ≥ 6 months of uptime, measurable query volume) that maintained sub-1% misrouting rates *without* a verification layer downstream of the router, relying only on the router's own confidence calibration. The chapter argues the verification layer is a required architectural component; a clean counter-example would force a specification of the conditions under which router confidence alone is sufficient.

**Still puzzling:** Whether rank starvation can be diagnosed *before* training from task-intrinsic properties — the data's effective dimensionality, the distance from the base model's pretraining distribution, the task's position in the output space — rather than empirically from a rank ablation. [Aghajanyan et al. (2020)](https://arxiv.org/abs/2012.13255)'s intrinsic-dimensionality measurements are suggestive, but they are computed *after* fine-tuning rather than predicted before it. A principled pre-training estimate of required rank would save the ablation phase; I don't yet have one.

---

**Tags:** lora-qlora-architecture, parameter-efficient-fine-tuning, serving-topology, adapter-misrouting, rank-starvation



---
---
---

# DRAFTING MATERIALS — not for publication

*Below this line: research notes and hero image brief. Strip before final edition assembly.*

---

# Research notes — Ch. 14, LoRA and QLoRA

**Book:** prompt-engineering
**Chapter slug:** lora-and-qlora
**Date:** 2026-04-21
**Voice anchoring state:** `voice-unanchored`. First chapter drafted for this book.
**Author byline:** **Shwetanshu Subhash Deshmukh** (fifth named-student chapter of the session).
**Policy flag:** `theory-authored-by-student` — exception to the book's "Nik-authored theory, student-authored cases" convention. Editor decision required.

---

## Theory-vs-case status

Per the Prompt Engineering book's `book.md`, Parts I–V are Nik-authored theory and Part VI is the student case-study layer. Shwetanshu wrote Ch. 14 — a Part IV theory chapter — making this an early exception to the split. Editor options:

1. **Keep as student-authored theory.** Preserve Shwetanshu's byline on a theory chapter. Cheapest; publishes his work fastest. Asymmetry worth naming: if other Part IV chapters stay Nik-authored, Ch. 14 reads differently. Manageable at five chapters across the book; less manageable if it becomes a pattern.
2. **Rewrite in Nik's voice, attribute Shwetanshu as contributor.** Standard textbook convention for editor-and-contributor authorship. Shwetanshu's technical corrections (the HDN on QLoRA precision) survive; the voice stays consistent with the rest of Part I–V.
3. **Move to Part VI as a case study.** Would need to be recast: "The LoRA Misrouting Case" or "The QLoRA Precision Correction Case." The chapter is theory-shaped, not case-shaped; this path would require substantive rewriting.

My read: **Option 2** if Nik wants a uniformly Nik-voiced theory, **Option 1** if first-edition publication speed matters more than voice uniformity. Flagged for decision.

## Concept

Three fine-tuning strategies — full fine-tuning, LoRA, and QLoRA — are not three points on a cost axis; they are three distinct architectures with distinct serving topologies and distinct failure modes. The central teaching move is to pull "fine-tuning" apart into three separable decisions (training parameterization, weight storage, serving topology) and show that each strategy picks them in a different combination.

## Specification move

"Fine-tuning" hides at least three decisions that are usually collapsed:

1. **Training parameterization.** Full gradient updates (all weights) vs. low-rank updates (adapter only).
2. **Weight storage.** Full precision everywhere vs. 4-bit frozen + 16-bit trainable.
3. **Serving topology.** One model per task vs. one shared base with routed adapters.

Conflating these produces the "LoRA is cheaper fine-tuning" framing, which is both true (it is cheaper) and architecturally misleading (because the cheapness comes with serving-topology commitments the expensive option doesn't have). The chapter's pedagogical trick is to make the three decisions separable, then show how each strategy combines them.

Second specification: "cost" wears at least three meanings in this context — training cost (GPU hours), memory cost (VRAM required during training), and operational cost (monitoring, router maintenance, verification layer overhead). QLoRA saves training memory specifically, not training compute; LoRA saves training compute specifically, not serving overhead. Which cost is binding depends on the deployment.

## Sub-claims — empirical vs. structural

**Structural / mathematical:**
- LoRA parameterization $W = W_0 + BA$, parameter count reduction of ~256× at $r=8$
- Rank as an upper bound on the representational capacity of the adaptation
- QLoRA's hybrid-precision architecture — three distinct precision regimes

**Empirical (verified):**
- Hu et al. 2021 (LoRA): [arXiv:2106.09685](https://arxiv.org/abs/2106.09685) — original paper, parameter reductions of 10,000× for GPT-3 class models
- Dettmers et al. 2023 (QLoRA): [arXiv:2305.14314](https://arxiv.org/abs/2305.14314) — NF4, Double Quantization, Paged Optimizers
- Aghajanyan et al. 2020 (intrinsic dimensionality): [arXiv:2012.13255](https://arxiv.org/abs/2012.13255) — predicts why low-rank adaptation works

**Pedagogically constructed:**
- The $200-vs-$2,000 five-adapter customer-segment scenario in §14.1 — labeled as a representative case, not a documented real incident
- The 8% misrouting rate — illustrative, plausible, not measured from a specific deployment
- The training-memory figures (~120 GB / ~20 GB / ~6 GB) — order-of-magnitude estimates for a 7B model with Adam; actual values depend on sequence length and batch size

## Mechanism chosen for the deep-dive

**QLoRA's hybrid-precision architecture** — the three distinct precision regimes (4-bit NF4 frozen base, FP16 trainable adapters, FP16 computation throughout). This was Shwetanshu's Human Decision Node correction to Bookie's original draft, and it is the chapter's most consequential technical teaching moment. A reader who finishes §14.4 with the correct mental model can make downstream decisions (when QLoRA helps and when it doesn't) from first principles.

One-sentence mechanism: *QLoRA's memory savings come entirely from storage compression of frozen base weights, not from reduced-precision computation — which means QLoRA is the right architecture when training memory is the binding constraint, and is architecturally irrelevant when training throughput is the constraint.*

## Central analogy — dropped

The original student draft used a materials-science analogy ("compresses the base crystal, reducing each atom's positional precision from 16 bits to 4 bits"). Shwetanshu himself rejected and corrected this in his Human Decision Node — the analogy implied the entire model operates in 4-bit, which is architecturally false. He notes: *"the analogy was elegant but mechanistically wrong."*

The merged chapter drops the analogy entirely. The math ($W = W_0 + BA$) plus the three-component precision breakdown carries the argument cleanly. A chapter whose author had to correct his own central analogy mid-draft is a chapter that probably doesn't need the analogy.

## Primary sources

| Claim | Source | URL | Verified? |
|---|---|---|---|
| LoRA parameterization and results | Hu et al. 2021 | https://arxiv.org/abs/2106.09685 | ✓ |
| QLoRA (NF4, DQ, Paged Optimizers) | Dettmers et al. 2023 | https://arxiv.org/abs/2305.14314 | ✓ |
| Intrinsic dimensionality of fine-tuning | Aghajanyan et al. 2020 | https://arxiv.org/abs/2012.13255 | ✓ |

## Structural / editorial changes vs. pasted material

The user supplied only an Author's Note — three pages of design rationale, tool-usage accounting, and self-assessment — with **no actual chapter prose** (this is the fourth time this session: similar to Rahul's Ch. 11, the Ch. 12 paste, and Shwetanshu's Ch. 14). I wrote the chapter body from Shwetanshu's architectural skeleton.

Key preserved from the Author's Note:

- The architectural-not-cost-optimization framing
- The three-strategy comparison (full FT / LoRA / QLoRA)
- The Human Decision Node on QLoRA precision — preserved as §14.4's central teaching moment
- Adapter misrouting as failure mode #1
- Rank starvation as failure mode #2
- The five-criterion decision matrix
- The "verification layer with heuristic 0.85 threshold" honest-limitation flag
- The architectural-argument master claim: different strategies = different failure modes

Key invented for the chapter body:

- The $200/$2,000 five-adapter customer-segment scenario in §14.1 — the concrete puzzle the chapter opens with
- The math walkthrough of LoRA parameterization in §14.3
- The decision-matrix table with specific memory figures for a 7B model
- The forward-connections paragraph to Ch. 15/16/19

Byline preserved: **Shwetanshu Subhash Deshmukh**, per the book's authorship convention.

## Book scaffolding created in this run

`books/prompt-engineering/` was new to the workspace. Created:
- `books/prompt-engineering/book.md` — per-book metadata with theory-case authorship convention, voice notes, scope
- `books/prompt-engineering/outline.md` — 20-chapter TOC from the 2026-02-18 Substack post
- `books/prompt-engineering/chapters/.gitkeep` + Ch. 14 draft
- `books/prompt-engineering/exercises/.gitkeep`
- `books/prompt-engineering/style/.gitkeep`

## Voice notes

- First person used twice in the draft (the "my read" in 14.3, the "I don't yet have one" in "Still puzzling") — consistent with the book's mechanism-first, opinion-labeled register.
- Forbidden phrases swept: no "obviously," "clearly," "in many ways," "robust."
- Single-sentence paragraphs used at pivots: "The output looks right. The output is wrong." / "It does not." (re: QLoRA running in 4-bit) / "The chapter is theory, not procurement."
- The materials-science analogy is deliberately absent per Shwetanshu's own HDN; the chapter argues the math is the analogy.

## Gaps flagged for TA refinement

- **`theory-authored-by-student` flag** at the top of the draft and in the outline — explicit editor decision required before publication. Listed as Options 1–3 in the outline entry above.
- **Verification-layer threshold (0.85)** — honestly flagged as heuristic. A production-refined version would run the threshold against a labeled validation set; mentioned in §14.5.1 as an operational next step.
- **Memory figures** (~120/~20/~6 GB) are order-of-magnitude for a 7B model with Adam. Vary by sequence length, batch size, gradient accumulation, and optimizer. Worth a `[verify]` flag in the table before publication if precise numbers are desired.
- **Notebook** referenced in Shwetanshu's Author's Note (demo of both failure modes, QLoRA live training, memory profiling) is not verified present in the workspace. TA should confirm or add.
- **Intrinsic-dimensionality reproduction** — flagged in Shwetanshu's self-assessment as "could be developed more rigorously — the chapter states the finding but does not reproduce or visualize the measurement." A student extending this chapter could add an appendix that runs the Aghajanyan measurement on a specific model and plots the result.

## Adjacent topics not pursued

- **Other PEFT methods** (prefix tuning, adapter layers, prompt tuning) — excluded per Shwetanshu's scoping decision to keep the decision framework to three options.
- **LoRA composition / adapter merging** — mentioned as an open research direction; not taught as reliable technique.
- **GPTQ / AWQ** (inference-time quantization methods) — different decision surface from QLoRA (training-time quantization); intentionally kept out of this chapter.
- **Hyperparameter tuning recipes for LoRA/QLoRA** — the chapter teaches decision criteria, not cookbooks. Recipe-level guidance belongs in an appendix or supplementary notebook.


---

# Hero image brief — Ch. 14, LoRA and QLoRA

**Book:** prompt-engineering
**Chapter slug:** lora-and-qlora
**Date:** 2026-04-21

## Concept the image should carry

The chapter's load-bearing visual claim is **QLoRA's hybrid-precision architecture** — that the 4-bit storage is confined to the *frozen* base weights, while the adapter weights and all computation happen in FP16. A reader looking at the image for thirty seconds should see: (1) three distinct precision regimes, (2) where each lives in the model, (3) that computation happens only after dequantization.

Secondary load: the **three serving topologies** (independent full-fine-tuned models vs. shared-base + LoRA adapters vs. shared-4-bit-base + LoRA adapters) side-by-side, making the architectural differences visible.

## Primary recommendation — QLoRA precision architecture

A single-panel diagram showing the forward pass of one transformer block under QLoRA. Three visually distinct regions:

- **Base weights $W_0$** (frozen): rendered in one muted color (dark slate), annotated **"4-bit NF4 storage"** — visibly smaller, tiled compactly.
- **LoRA adapters $B, A$** (trainable): rendered in a second color (warm teal), annotated **"FP16 — trainable"** — full-size boxes, clearly distinct from the 4-bit base.
- **Computation pathway** (arrows through the diagram): rendered in a third visual element (dashed arrows, or a lighter shade), annotated **"FP16 compute after dequantization"** — showing that $W_0$ must be dequantized before participating in the matrix multiply $W_0 x$.

A small inset callout: *"The 4-bit is storage only. Gradients flow through FP16. QLoRA does not accelerate compute — it compresses idle memory."*

This figure directly implements Shwetanshu's Human Decision Node correction. Without it, readers will slip back into the "QLoRA runs in 4-bit" misconception. The figure is the correction made visual.

## Secondary recommendation — three-topology comparison

A wide three-panel figure showing the three serving topologies side by side.

**Left panel — Full fine-tuning:** Five independent transformer blocks, each a different color, labeled "Model A," "Model B," "Model C," "Model D," "Model E." No connection between them. Each has its own inference endpoint.

**Middle panel — LoRA:** One large transformer block (the shared base, in slate). Five small colored adapters attached to it, labeled $\Delta_A, \Delta_B, \Delta_C, \Delta_D, \Delta_E$. A **router** node at the top that routes each incoming query to one of the five adapters. The router is visually distinct from both the base and the adapters — it's its own architectural element.

**Right panel — QLoRA:** Same as LoRA, but the shared base is visibly compressed (darker, smaller) and labeled "4-bit NF4." Adapters unchanged.

Below all three panels, a row of annotations:
- Left: *"Independent endpoints; no router; no misrouting failure mode."*
- Middle: *"Shared base; router decides; misrouting is possible."*
- Right: *"Same as LoRA; memory-constrained case."*

This makes the architectural consequence of each choice visible — particularly that the router is a new architectural element introduced by LoRA/QLoRA that full fine-tuning doesn't have, and that *this* is where the misrouting failure mode lives.

## Tertiary recommendation — rank-capacity ablation curve

A simple line graph. X-axis: adapter rank $r$ (log scale, 4 / 8 / 16 / 32 / 64). Y-axis: eval score (normalized 0–1). One line per task difficulty level: "easy," "medium," "hard."

The diagnostic signature the figure should make visible: the easy line plateaus at high rank-4; the medium line plateaus at rank-16; the hard line is still climbing at rank-64 (rank starvation). A horizontal dashed line labeled "full fine-tune ceiling" sits above the highest curve, showing what the adapter architecture cannot reach.

This is the empirical picture of rank starvation — the failure mode as a specific, recognizable shape on a chart.

## Style direction

Per `book.md` voice notes: technical-diagram aesthetic, muted academic palette, no stock photography. Engineering-drawing feel — like a schematic from a hardware design document rather than an infographic. Color encoding should do real work (3 distinct precision regimes = 3 distinct colors), not decorate.

No anthropomorphic imagery, no glowing brains, no "AI" iconography. The chapter's argument is that fine-tuning is a systems architecture choice, and the images should match — this is engineering, not magic.

## Aspect ratio

- Primary (QLoRA precision): square or modestly wide (1:1 or 4:3)
- Secondary (three-topology comparison): very wide (21:9) — three panels side by side need the width
- Tertiary (rank-capacity curve): wide (16:9) for the X-axis range

## Do NOT

- Generate any of these in this run.
- Render QLoRA's 4-bit region as *encompassing the whole model*. That is the exact misconception the figure exists to correct.
- Use the materials-science "crystal" or "compressed atoms" analogy anywhere in the image. Shwetanshu rejected it in his Human Decision Node; the chapter is built without it.
- Render the router in the LoRA/QLoRA panels as a neutral gateway. It should be visibly its *own* component — the architectural element that did not exist under full fine-tuning. The router is where the misrouting failure lives; the image should make it visible as a distinct, nameable thing.
- Use more than three colors. Three colors per chapter, mapped to three precision regimes, keeps the mental model clean. Adding a fourth color introduces ambiguity.
