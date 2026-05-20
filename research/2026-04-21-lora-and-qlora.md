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
