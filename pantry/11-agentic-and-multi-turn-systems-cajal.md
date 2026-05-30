# CAJAL Figure Intelligence — Chapter 11 — Agentic and Multi-Turn Systems

Source: chapters/11-agentic-and-multi-turn-systems.md
Mode: /scan silent
Date: 2026-05-29

## Density Recommendation
5 figure candidates. Mostly mechanistic. The spine is the Thought→Action→Observation loop interrupting the P^N chain (the chapter's central mechanism); around it sit one P^N compounding curve (PQ), a tool-count degradation bar chart (PQ), a constrained-decoding mechanism schematic, and a multi-turn memory/derailment process figure.

## Figure 1: The agent loop interrupts the P^N chain
Priority: Critical
Trigger: MC — the central mechanism: a single-shot chain compounds error token-by-token, while an injected Observation (not model-generated) anchors the chain, so effective compounding moves from P^N toward P^k
Figure type: Cycle diagram
Concept statement: Single-shot reasoning compounds error along a dependency chain (P^N); the ReAct loop injects externally-sourced Observation tokens that interrupt — not erase — that chain, re-anchoring the next Thought every few steps.
Reader prior knowledge: Autoregressive token dependency; Thought / Action / Observation token kinds; Observation tokens are returned by a tool, not sampled by the model (§11.2).
Source anchor: Section: 11.2 The loop, condensed

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector cycle diagram on a white background showing a three-node loop arranged as a triangle traversed clockwise by single-headed arrows: a Thought node at top, an Action node at lower right, and an Observation node at lower left, with arrows Thought→Action→Observation→back to Thought. Render the Thought node and Action node in primary blue #56B4E9 (both model-generated). Render the Observation node distinctly in active green #009E73 to mark that it is injected from outside the model's distribution — and draw one bold single-headed arrow entering the Observation node from outside the triangle (a short external feed stub) to signal the external world supplies it. Along the return arrow from Observation back to Thought, place a small anchor glyph (a short perpendicular tick bar across the arrow) to mark the re-anchoring point that interrupts the dependency chain; render that anchor mark in #009E73 as well. Keep components to three loop nodes, the external feed stub, and the anchor tick. Use only Okabe-Ito colors: #56B4E9 Thought and Action, #009E73 Observation and anchor, #000000 arrows and outlines. No numbers, no text, no letters anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] A three-node clockwise loop (Thought → Action → Observation → Thought); Thought and Action model-generated; Observation fed by an external stub; an anchor tick on the Observation→Thought return marking chain interruption.
[O - Organization] Triangular loop, single-headed clockwise arrows; external feed stub into Observation; anchor mark on the return arrow.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — #56B4E9 Thought and Action nodes, #009E73 Observation node, external stub, and anchor tick, #000000 arrows.
[E - Exclusions] No node-label text, no tool-call code, no probability/P^N formulas, no captions; no more than three loop nodes; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
node label text, tool-call code, formula text, probability notation, captions, more than three loop nodes, text labels, words, gibberish letters, titles, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 2: Error compounds across a single-shot chain
Priority: Important
Trigger: PQ — the P^N numbers (P=0.95: ~60% at N=10, ~36% at N=20) — chain success decaying as step count grows, the quantitative motive for the loop
Figure type: Statistical/quantitative
Concept statement: At 95% per-step reliability, chain success decays multiplicatively with length — about 60% at ten steps, about 36% at twenty — because a wrong early token poisons the conditioning for everything after it.
Reader prior knowledge: The multiplication rule; per-step accuracy P; chain length N; P_chain ≈ P^N (§11.2).
Source anchor: Section: 11.2 The loop, condensed

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector line chart on a white background with a horizontal axis representing chain length (number of steps, increasing left to right) and a vertical chain-success axis starting at zero and running to full height. Plot one smooth monotonically decreasing curve that starts high near the top-left and decays with a concave-down multiplicative shape toward the lower right, never reaching zero. Render the decay curve as a single 1.5pt line in blocking orange #D55E00 to mark deteriorating reliability. Mark two reference dots on the curve: one at a short chain length sitting at roughly three-fifths height and one at a longer chain length sitting at roughly one-third height, both as small filled dots in #000000, with thin neutral-gray horizontal guide segments dropping from each to the y-axis to show the falling success. Draw plain x and y axes with no tick numbers. Keep components to one curve, two reference dots, two guides, two axes. Use only Okabe-Ito colors: #D55E00 decay curve, neutral gray guides, #000000 dots and axes. No numbers, no text, no labels anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] One monotonically decreasing P^N-shaped chain-success curve vs chain length; two marked reference points (a shorter chain higher, a longer chain lower) with guides to the y-axis.
[O - Organization] Chain length on x, success on y from zero; concave multiplicative decay; two reference dots with horizontal guides.
[P - Presentation] Flat vector, 1.5pt curve, 1pt axes; Okabe-Ito only — #D55E00 curve, neutral gray guides, #000000 dots and axes.
[E - Exclusions] No numeric axis values, percentages, or step numbers; no second curve; no gridlines; no shaded fill; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
numeric axis values, percentage labels, step number labels, second curve, gridlines, shaded area fill, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 3: More tools, more errors
Priority: Important
Trigger: PQ — the tool-count degradation result (function-calling performance drops 7.6%–85.6% as the tool catalog grows from ~8K to ~120K tokens, LongFuncEval 2025), plus the routing rule
Figure type: Statistical/quantitative
Concept statement: Performance degrades as the tool catalog grows — a larger catalog spends context on unused descriptions and widens selection ambiguity — so error and hallucination rise with catalog size, motivating a router that surfaces only the relevant few tools.
Reader prior knowledge: Tool catalog size (in tokens or tool count); error/hallucination rate; the routing rule (scope ≤~10, else route) (§11.3).
Source anchor: Section: 11.3 Controlling tool exposure: more tools, more errors

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector bar chart on a white background with the vertical error-rate axis starting at zero and a horizontal axis showing increasing tool-catalog size in three or four steps from small to large (left to right). The bars rise in height from left to right — a short bar at the smallest catalog, increasing to a tall bar at the largest catalog — showing error climbing with catalog size. Render the smallest-catalog bar in active green #009E73 (the scoped, low-error condition) and the largest-catalog bar in blocking orange #D55E00 (the bloated, high-error condition), with the intermediate bars in secondary orange #E69F00 graduating between them. All bars rise from a common zero baseline with equal width and even spacing. To the right of the bars, add one small separate schematic: a router node (a single primary-blue #0072B2 block) with two short single-headed arrows selecting just two of several small tool stubs, illustrating the fix of surfacing only the relevant subset. Keep to four bars plus the small router inset. Use only Okabe-Ito colors: #009E73 smallest catalog, #E69F00 mid catalogs, #D55E00 largest catalog, #0072B2 router, #000000 axis. No numbers, no text, no labels anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Three-to-four error-rate bars rising with tool-catalog size (small=low green, large=high orange), y from zero; a small router inset selecting two of several tool stubs as the mitigation.
[O - Organization] Bars left-to-right by increasing catalog size with ascending heights; router inset to the right with two selecting arrows.
[P - Presentation] Flat vector, 1pt strokes, bars from zero; Okabe-Ito only — #009E73 / #E69F00 / #D55E00 by catalog size, #0072B2 router, #000000 axis.
[E - Exclusions] No numeric value labels, axis tick numbers, percentages, token counts, or legend; no tool names; no 3D bars; no color beyond named hexes; keep green and orange-family bars readable without red-green pairing.

### Block 3 — Negative Prompt
value labels on bars, axis tick numbers, percentage text, token-count labels, tool name labels, legend text, 3D bars, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 4: Constrained decoding masks the illegal vocabulary
Priority: Important
Trigger: VG — the mechanism distinction (prompted JSON requests conformance; constrained decoding guarantees it by masking the vocabulary against a compiled grammar state) is a structural claim about where the guarantee comes from, not depictable from text
Figure type: Mechanism cross-section
Concept statement: Prompted JSON only requests conformance, but constrained decoding compiles the schema into a finite-state machine and at each step masks every vocabulary token illegal in the current grammar state to near-zero, so the model literally cannot emit an invalid token.
Reader prior knowledge: Next-token vocabulary distribution; a finite-state grammar; masking probabilities to near-zero; shape ≠ truth (§11.4).
Source anchor: Section: 11.4 Enforcing structured output

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector mechanism figure on a white background showing one decode step. On the left, a small finite-state-machine glyph: three nodes connected by two single-headed transition arrows representing the compiled grammar, with one node highlighted as the current state; render the FSM in primary blue #0072B2 with the active state node filled #0072B2 and the others outlined. An arrow leads right to a vertical row of about eight candidate vocabulary slots (small uniform cells representing next-token candidates). Two or three of these slots — the grammar-legal tokens — are rendered active green #009E73 and left open; the remaining slots — the illegal tokens — are rendered as struck-through cells (a single diagonal bar across each) in neutral gray, marking them masked to near-zero. One bold single-headed arrow points from a legal green slot rightward to a single emitted-token output cell, also #009E73. Keep components to the FSM (three nodes), the eight candidate slots, and the one emitted cell. Use only Okabe-Ito colors: #0072B2 FSM, #009E73 legal/emitted tokens, neutral gray masked tokens, #000000 strokes and strike bars. No numbers, no text, no letters anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] A compiled grammar FSM (three nodes, current state highlighted) feeding a column of ~eight candidate vocabulary slots; legal tokens green and open, illegal tokens gray and struck through (masked); one emitted token selected from a legal slot.
[O - Organization] FSM at left → candidate slots in the middle (some struck) → single emitted-token cell at right via a bold arrow.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — #0072B2 FSM and active state, #009E73 legal and emitted tokens, neutral gray masked tokens with diagonal strike bars, #000000 strokes.
[E - Exclusions] No token text, no JSON characters, no probability numbers, no captions; no more than eight candidate slots; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
token text, JSON characters, braces, probability numbers, captions, more than eight candidate slots, text labels, words, gibberish letters, titles, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 5: Multi-turn derailment and summarize-and-restart
Priority: Important
Trigger: MC — the multi-turn process: state must be resupplied each turn; raw history buries early context in the trough, a wrong turn contaminates all later turns and does not recover, and the fix is to summarize-and-restart rather than repair in place
Figure type: Process flowchart
Concept statement: With no memory beyond the window, an accumulating thread buries early intake in the lost-in-the-middle trough and a wrong turn poisons every later turn (non-recovery); summarize-and-restart drops the contamination instead of reasoning from it.
Reader prior knowledge: No persistent state between calls; resupply each turn; lost-in-the-middle (Ch. 10); non-recovery after a wrong turn (Laban et al. 2025) (§11.5).
Source anchor: Section: 11.5 Managing multi-turn context

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector process figure on a white background with two horizontal tracks stacked vertically, both reading left to right as a sequence of turn nodes (small uniform blocks connected by single-headed arrows). The TOP track (repair-in-place) shows about six turn nodes; the third node is marked as a wrong turn with a small downward kink/branch and rendered blocking orange #D55E00, and every node after it is also rendered #D55E00 to show the contamination propagating; the track ends at a failure terminal also in #D55E00. The BOTTOM track (summarize-and-restart) shows the same first few turns, but immediately after the wrong third turn a compression node (a small funnel/converging glyph) collapses the prior turns into a single clean summary block rendered active green #009E73, from which a fresh short sequence of clean turn nodes (#009E73) proceeds to a success terminal. The compression node should visibly drop the orange contaminated turns (a short downward discard arrow to a small gray X-free dead stub). Keep each track to about six nodes plus the compression node. Use only Okabe-Ito colors: #D55E00 contaminated turns and failure, #009E73 clean summary and recovered turns, neutral gray discarded stub, #000000 arrows and outlines. No numbers, no text, no labels anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Two turn-sequence tracks: top = repair-in-place where a wrong turn contaminates all later turns to a failure terminal (orange); bottom = summarize-and-restart where a compression node collapses prior turns into a clean green summary, discards the contaminated turns, and proceeds to a success terminal.
[O - Organization] Two stacked left-to-right tracks; wrong turn at the same position in both; contamination propagates on top, compression + clean restart on the bottom; a discard stub from the compression node.
[P - Presentation] Flat vector, 1pt single-headed arrows; Okabe-Ito only — #D55E00 contaminated turns and failure terminal, #009E73 clean summary and recovered turns and success terminal, neutral gray discarded stub, #000000 outlines.
[E - Exclusions] No turn-number text, no conversation text, no captions; no more than six nodes per track; no color beyond named hexes; no red-green adjacency (keep the orange contamination and green recovery on separate tracks).

### Block 3 — Negative Prompt
turn number labels, conversation text, captions, more than six nodes per track, text labels, words, gibberish letters, titles, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video Candidate Pass
FIGURE 1 — Agent loop interrupts P^N: VIDEO CANDIDATE — the Thought→Action→Observation cycle with an externally-fed Observation re-anchoring the chain is intrinsically iterative; animating one full traversal with the anchor breaking the dependency would teach the interrupt property, though the static cycle with the anchor tick carries it.
FIGURE 2 — P^N compounding: STATIC SUFFICIENT — a single decay curve is a canonical static plot.
FIGURE 3 — More tools, more errors: STATIC SUFFICIENT — an ascending bar chart with a router inset is naturally static.
FIGURE 4 — Constrained decoding: VIDEO CANDIDATE — masking illegal tokens at each grammar-state transition is a per-step temporal process; animating the FSM advancing and the legal set narrowing each step would teach "cannot emit invalid," though the single-step static schematic suffices.
FIGURE 5 — Derailment and restart: VIDEO CANDIDATE — contamination propagating turn-by-turn versus a compression-and-restart is sequential by nature; animating the two tracks advancing in parallel would make non-recovery vivid, though the static two-track flowchart carries it.
Recommendation: Render all five as static figures; Figures 1, 4, and 5 are the strongest optional-video candidates if an animated layer is produced.
