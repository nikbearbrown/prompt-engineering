# Hero image brief — Ch. 10, ReAct: Grounding Reasoning in the Real World

**Book:** prompt-engineering
**Chapter slug:** react
**Date:** 2026-04-21

## Concept the image should carry

The chapter's load-bearing visual claim is **the probabilistic dependency structure of CoT, and what Observation injection does to it**. A reader looking at the image for thirty seconds should understand that model-generated tokens are drawn from a distribution that depends on prior tokens (CoT's compounding structure), that Observations enter from outside that distribution (breaking the chain of dependence through the Thought steps), and that the "interruption" is partial — the next Thought is still conditioned on prior Thoughts, just *also* on the new anchor.

This is the critique's Priority Fix #1 made visual.

## Primary recommendation — the dependency chain with and without Observations

A two-panel diagram.

**Top panel — Chain-of-Thought:**
A horizontal sequence of token boxes labeled $T_1, T_2, T_3, \ldots, T_N$. Each $T_i$ has an arrow drawn *backward* to all previous tokens $T_1, \ldots, T_{i-1}$, labeling the conditional dependence: $T_i \sim P(T_i \mid T_1, \ldots, T_{i-1})$. Every token is the same color (muted teal) — they all come from the same probabilistic system.

Below the chain, a formula and annotation: $P_{\text{chain}} \approx P^N$ with values — at $P=0.95, N=10$: $\approx 0.60$; at $N=20$: $\approx 0.36$. Label: *"A wrong token in the chain shifts the distribution of every later token."*

**Bottom panel — ReAct:**
Same horizontal sequence, but the tokens alternate in color. Thoughts are muted teal (same as CoT, because they still are model-sampled). Observations are a different color entirely — muted ochre — with a distinct visual boundary around them. An arrow from *outside the diagram* points into each Observation, labeled *"from tool call — deterministic, not sampled"*.

Conditional dependency arrows: each Thought $T_i$ still has backward arrows to prior Thoughts, *and* an additional arrow to any prior Observations. But the Observation tokens themselves have no backward arrows at all — they don't depend on prior tokens because they weren't sampled.

Label beneath the bottom panel: *"Thoughts still compound error among themselves. Observations don't. The next Thought is anchored to both — which interrupts compounding (does not erase it)."*

This is the figure that closes the critique's "mechanism not shown" gap.

## Secondary recommendation — the prompt-fix-vs-architectural-fix contrast

A two-column side-by-side diagram. Both columns show a tool-format-change failure scenario.

**Left column — Prompt-level fix:**
Tool → JSON output → Loop (no validator) → Observation buffer → Model (with "be careful" instruction in system prompt) → Thought. A dashed red line circles the entire stack, labeled: *"Fix lives inside the probabilistic system that is producing the error."*

**Right column — Architectural fix:**
Tool → JSON output → **Validator** (rendered as a distinct gate shape, in a third color — muted slate) → either typed error or passthrough → Observation buffer → Model → Thought. The validator sits outside the red dashed region, labeled: *"Fix lives outside the probabilistic system. Deterministic Python."*

Below both columns: *"A prompt is more tokens. A validator is a different kind of thing."*

This is the chapter's sharpest claim made visual.

## Tertiary recommendation — the three scope limits

A simple table (visual table, not a prose one). Three rows:

| Condition | Anchor effect | Consequence for $P^N$ |
|---|---|---|
| Short trace, reliable tools | Strong | Interrupted; effective exponent → $P^1$ per anchor segment |
| Long trace (context window filling) | Weakening | Anchors fade with distance; effective exponent drifts toward $P^N$ between anchors |
| Tool failure (broken format / wrong schema) | Broken | Observation itself becomes noise source; worse than pure CoT |

Annotation: *"ReAct interrupts compounding under conditions 1. Engineers design for conditions 2 and 3."*

## Style direction

Per `book.md` voice notes: engineering-diagram aesthetic. Muted academic palette. No alarm iconography, no anthropomorphic agents, no glowing-brain imagery. Formulas should appear in LaTeX or a clean sans-serif technical font, not decorative type.

Three colors, each mapped to a distinct token provenance:
- **Muted teal** — model-generated tokens (CoT, Thoughts)
- **Muted ochre** — externally-sourced tokens (Observations)
- **Muted slate** — architectural components (validators, tool registry)

Using the same color coding across all three images lets the reader recognize "the same kind of thing" across figures — which is load-bearing, since the chapter's argument turns on keeping these three categories distinct.

## Aspect ratio

- Primary (CoT vs. ReAct dependency chains): very wide (21:9) — the horizontal token sequence needs room for 10+ tokens in both panels
- Secondary (prompt-fix vs. architectural-fix): wide (16:9) for side-by-side columns
- Tertiary (scope limits table): square or modestly wide (4:3)

## Do NOT

- Generate any of these in this run.
- Draw the Observation tokens in the same color as Thought tokens. Color-coding provenance is the teaching move — if Thoughts and Observations look identical, the reader has been told the thing the figure exists to show is invisible.
- Use alarm/error iconography for the failure case. The distribution-shift failure is mechanistic and boring-looking; rendering it as a crash or explosion moralizes what should be architectural.
- Draw the validator as a shield, a lock, or any defensive iconography. It is a Python function. A rectangular box with a function signature above it is correct. Anthropomorphizing the validator as a guard or firewall suggests it's doing something fundamentally different from ordinary code — it isn't.
- Omit the dependency-arrow structure from the primary image. Without the backward arrows showing conditional dependence, the image degrades to "sequence of boxes" and the claim the image exists to make goes invisible.
- Render "reset" anywhere in annotations. The chapter's precise claim is *interrupt*, not *reset*. A figure label that says "error resets at each Observation" plants the misconception the chapter is built to prevent.
