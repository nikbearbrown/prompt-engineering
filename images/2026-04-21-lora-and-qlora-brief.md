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
