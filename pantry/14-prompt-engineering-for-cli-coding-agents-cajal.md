# CAJAL Figure Intelligence — Chapter 14 — Prompt Engineering for CLI Coding Agents

Source: chapters/14-prompt-engineering-for-cli-coding-agents.md
Mode: /scan silent
Date: 2026-05-29

## Density Recommendation
5 figure candidates. Mechanistic density. The chapter's spine is process and architecture — the stateful read→reason→act→observe loop, the monotonic token-budget fill, the plan-then-execute quarantine split, the lethal-trifecta security combination, and the three-failure diagnostic router — each a structural or multi-step claim not depictable from prose alone.

## Figure 1: The stateful loop and the monotonic token budget
Priority: Critical
Trigger: MC — the read→reason→act→observe cycle is a ≥4-step interdependent process whose defining property (context accumulates and never shrinks unless forced) drives the whole chapter
Figure type: Cycle diagram
Concept statement: A CLI coding agent runs a four-stage loop — read, reason, act, observe — that appends to an ever-growing context, so consumed tokens climb monotonically toward the degradation threshold with each pass.
Reader prior knowledge: The ReAct Thought→Action→Observation loop (Ch. 11); context as a finite window (Ch. 10).
Source anchor: Section: 14.2 Statefulness and the token budget

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector figure on a white background combining a cycle and a fill gauge. On the left, draw a four-node closed cycle arranged as a ring: four equal rounded-rectangle nodes (read, reason, act, observe) connected by four single-headed arrows flowing clockwise back to the start, rendered with primary blue #0072B2 node outlines and #000000 arrows. From the cycle, draw one single-headed connector arrow rightward to a tall vertical bar gauge on the right representing the context window. The gauge is a tall narrow open rectangle filling from the bottom; show the fill as a solid block rising part way up in secondary orange #E69F00, with a single horizontal threshold line near the top (about four-fifths height) drawn in blocking orange #D55E00. Place three short upward step ticks along the rising fill to suggest each loop pass adds more. Keep total components to six: four cycle nodes, one connector, one gauge. Use only Okabe-Ito colors: #0072B2 cycle nodes, #E69F00 fill, #D55E00 threshold line, #000000 arrows and gauge outline. No numbers, no percentages, no text or labels anywhere. Flat vector, 1pt strokes, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] A four-node clockwise cycle (read, reason, act, observe) feeding a vertical context-window gauge whose orange fill rises in steps toward a high blocking-orange threshold line.
[O - Organization] Cycle on the left as a ring of four nodes with clockwise single-headed arrows; one connector arrow to a tall vertical fill-gauge on the right with the threshold line near the top.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — #0072B2 cycle node outlines, #E69F00 gauge fill, #D55E00 threshold line, #000000 arrows and gauge outline; no gradients.
[E - Exclusions] No numeric percentages or "80%" text, no axis values, no fifth cycle stage, no clock icons, no downward/declining fill, no color beyond named hexes, no red-green pairing.

### Block 3 — Negative Prompt
numeric percentages, 80% label, axis values, fifth cycle node, clock icons, declining fill, downward arrows, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 2: The instruction-capacity budget
Priority: Important
Trigger: PQ — the chapter gives concrete counts (≈150–200 instruction ceiling, ≈50 consumed by the agent's own system prompt, leaving ≈100–150) that compose into a fixed budget readable as a stacked bar
Figure type: Statistical/quantitative
Concept statement: A frontier model's distinct-instruction ceiling is partly pre-spent by the agent's own system prompt, leaving only a narrow band for the engineer's instruction file before adherence degrades uniformly.
Reader prior knowledge: Long-context dilution and salience flattening (Ch. 10); the persistent instruction file (§14.3).
Source anchor: Section: 14.3 The instruction-capacity ceiling

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector bar chart on a white background showing a single tall vertical stacked bar rising from a baseline of zero. The bar is divided into two stacked segments from the bottom up: a lower segment (the agent's own system prompt) rendered in neutral gray, and an upper segment (the space available for the engineer's instruction file) rendered in primary blue #0072B2. Above the top of the blue segment, draw a single horizontal cap line spanning the bar width in blocking orange #D55E00 marking the degradation ceiling, with a short bracket on the right side indicating the gap between the top of the available band and the ceiling. The blue available segment should be visibly the larger of the two but still clearly bounded below the ceiling cap. Keep the y-axis as a plain vertical line from zero with no tick numbers. Total components: one baseline axis, two stacked segments, one ceiling cap line, one bracket — five maximum. Use only Okabe-Ito colors: neutral gray system-prompt segment, #0072B2 available segment, #D55E00 ceiling line, #000000 axis. No numbers, no text, no labels anywhere. Flat vector, 1pt strokes, no shadows, no gradients, white background, y-axis from zero.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated, y-axis from zero.
[C - Content] One stacked vertical bar: lower gray segment (system-prompt consumption), upper blue segment (engineer's available instruction space), capped by a blocking-orange ceiling line with a bracket showing the remaining margin to the ceiling.
[O - Organization] Single bar on a zero baseline; two stacked segments bottom-to-top; horizontal ceiling cap above the blue segment; right-side bracket between top of available band and the cap.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — neutral gray base segment, #0072B2 available segment, #D55E00 ceiling line, #000000 axis; no gradients.
[E - Exclusions] No numeric tick values, no "150", "200", or "50" labels, no second bar, no legend text, no percentage marks, no color beyond named hexes, no red-green pairing, no 3D bar.

### Block 3 — Negative Prompt
numeric tick values, instruction-count numbers, percentage marks, second bar, legend text, axis labels, words, text labels, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 3: The plan-then-execute split
Priority: Critical
Trigger: MC — a multi-step quarantine workflow (explore → save plan → clear → execute clean) whose point is that polluted exploratory context is discarded before execution, a process not legible from text
Figure type: Process flowchart
Concept statement: Planning happens in a session that accumulates dirty exploratory context; the durable plan is saved, the polluted window is discarded by /clear, and execution runs from only the plan in a fresh clean window.
Reader prior knowledge: Monotonic token fill and context rot (§14.1–14.2); the durable-artifact handoff (§14.6).
Source anchor: Section: 14.5 Plan in one session, execute in another

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector process figure on a white background showing two distinct session containers separated by a discard gate. On the left, draw a rounded-rectangle container (Session A, the plan session) that is visibly cluttered: inside it place three or four small overlapping irregular blobs representing dead-end exploratory material, rendered in secondary orange #E69F00. From this container draw one single-headed arrow downward to a small document node (the saved plan), drawn as a clean rectangle with a folded corner in primary blue #0072B2. Between the two containers draw a vertical dashed barrier line with a small open-gate or scissors-style break in neutral gray, labeled by shape alone as the discard point; an arrow from Session A crossing toward Session B should terminate at the barrier (blocked), while only the plan document's arrow passes through. On the right, draw a second rounded-rectangle container (Session B, execution) that is clean and empty except for the plan document arriving via a single-headed arrow, with one outgoing arrow to a final checkmark-style node in active green #009E73. Total components: two session containers, the clutter blobs as one group, the plan document, the discard barrier, the clean outcome — six maximum. Okabe-Ito only: #E69F00 clutter, #0072B2 plan document, neutral gray barrier, #009E73 clean outcome, #000000 arrows. No text, no labels, no words anywhere. Flat vector, 1pt single-headed arrows, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Session A container holding orange exploratory clutter; a blue saved-plan document; a dashed gray discard barrier that blocks the polluted context but passes the plan; Session B clean container receiving only the plan and producing a green clean outcome.
[O - Organization] Left cluttered session → saved plan document; dashed discard barrier between sessions blocking the clutter arrow but passing the plan; right clean session → green outcome; single-headed arrows throughout.
[P - Presentation] Flat vector, 1pt single-headed arrows; Okabe-Ito only — #E69F00 clutter blobs, #0072B2 plan document, neutral gray barrier, #009E73 outcome, #000000 arrows; no gradients.
[E - Exclusions] No text, no "/clear" or "Session A/B" words, no terminal/console screenshot imagery, no more than two sessions, no color beyond named hexes, no red-green pairing for the block/pass contrast (use orange-blocked vs green-pass only).

### Block 3 — Negative Prompt
session labels, slash-clear text, terminal screenshots, console windows, code text, more than two session containers, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 4: The lethal trifecta
Priority: Critical
Trigger: VG — the structural claim that exploitability arises only from the simultaneous overlap of three capabilities (private data, untrusted content, external communication) is an architectural relationship best shown as an intersection, not derivable from prose
Figure type: Systems diagram
Concept statement: A CLI agent becomes exploitable only where three capabilities overlap at once — access to private data, exposure to untrusted content, and the ability to communicate externally — so the danger is the structural combination, not any single leg.
Reader prior knowledge: Files as instruction-delivery vectors and computational skepticism toward content (Ch. 4, §14.6).
Source anchor: Section: 14.6 Security: the least-solved problem in the chapter

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector Venn-style systems diagram on a white background showing three equal circles arranged in the classic three-way overlap so that all three intersect in a central region. Draw each circle as an open outline with a thin 1pt stroke: the first circle (private data) outlined in primary blue #0072B2, the second (untrusted content) outlined in secondary orange #E69F00, the third (external communication) outlined in #CC79A7. Leave the three single-pair overlap zones plain. Fill only the central three-way intersection region — where all three circles overlap — as a solid block in blocking orange #D55E00 to mark the exploitable zone. Keep the circles equal in size and symmetrically placed. Total components: three labeled-by-color circles plus one highlighted central intersection — four maximum. Use only Okabe-Ito colors: #0072B2, #E69F00, and #CC79A7 for the three circle outlines, #D55E00 for the central exploitable fill, #000000 nowhere except optional hairline. No numbers, no text, no labels, no words anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Three equal overlapping circles (private data, untrusted content, external communication) with only the central three-way intersection filled to mark the exploitable combination.
[O - Organization] Standard symmetric three-circle Venn with a single shared central region; only that central region is filled.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — #0072B2, #E69F00, #CC79A7 circle outlines, #D55E00 central exploitable fill; no gradients, no transparency blending that creates new hues.
[E - Exclusions] No text labels for the legs, no "private data / untrusted content / external" words, no numeric counts, no fourth circle, no filled pairwise overlaps, no color beyond named hexes, no red-green pairing, no 3D spheres.

### Block 3 — Negative Prompt
leg labels, words, private data text, fourth circle, filled pairwise overlaps, numeric counts, gibberish letters, titles, captions, text labels, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion, glossy spheres

---

## Figure 5: The three-failure diagnostic router
Priority: Important
Trigger: MC — a decision process routing three confusable symptoms (context rot, instruction overflow, prompt injection) via sequential tests to distinct fixes, an interdependent branching procedure
Figure type: Process flowchart
Concept statement: One diagnostic question — does it work in a fresh session — plus two follow-up checks routes a confidently-wrong agent to one of three causes and its matching fix.
Reader prior knowledge: The three failure mechanisms (§14.2 context rot, §14.3 instruction overflow, §14.6 injection); single-turn isolation testing (Ch. 6, Ch. 9).
Source anchor: Section: 14.7 Three failures, one question

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector decision-tree figure on a white background flowing top to bottom. At the top, draw one diamond decision node (the fresh-session test) in primary blue #0072B2. From it, two single-headed branches split: a right branch (works cleanly in a fresh session) leads down to a second diamond decision node (was untrusted content just read) in #0072B2; a left branch (still fails fresh) leads to a terminal rounded-rectangle outcome node for the instruction-overflow fix in secondary orange #E69F00. From the second diamond, two single-headed branches split to two terminal rounded-rectangle outcome nodes: one for the context-rot fix and one for the prompt-injection fix, both rendered in active green #009E73 as resolved states. Align the three terminal outcome nodes along a common bottom row. Total components: two diamond decision nodes and three terminal outcome nodes — five maximum, joined by single-headed arrows with no crossings. Okabe-Ito only: #0072B2 decision diamonds, #E69F00 the instruction-overflow terminal, #009E73 the two grounded-resolution terminals, #000000 arrows. No text, no yes/no labels, no words anywhere. Flat vector, 1pt single-headed arrows, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] A two-level decision tree: top diamond (fresh-session test) branching to a second diamond (untrusted-content read?) and to an instruction-overflow terminal; the second diamond branching to context-rot and prompt-injection terminals.
[O - Organization] Top-to-bottom flow; first diamond at top, second diamond mid-right, three terminal outcome nodes aligned on a common bottom row; single-headed arrows, no crossings.
[P - Presentation] Flat vector, 1pt single-headed arrows; Okabe-Ito only — #0072B2 decision diamonds, #E69F00 instruction-overflow terminal, #009E73 the two state-dependent terminals, #000000 arrows.
[E - Exclusions] No text, no yes/no/true/false branch labels, no terminal screenshots, no fourth terminal, no color beyond named hexes, no red-green pairing, no crossing arrows.

### Block 3 — Negative Prompt
yes/no labels, true/false labels, branch text, fourth terminal node, terminal screenshots, code text, words, text labels, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, crossing arrows, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video Candidate Pass
FIGURE 1 — stateful loop and monotonic token budget: VIDEO CANDIDATE — process unfolds over iterations (cycle repeats, gauge fills toward threshold) — animating the loop incrementing the fill makes the monotonic-climb-to-threshold mechanism legible in a way a static gauge only hints at.
FIGURE 2 — instruction-capacity budget: STATIC SUFFICIENT — a single stacked-bar comparison with no temporal dimension; one frame carries the full claim.
FIGURE 3 — plan-then-execute split: VIDEO CANDIDATE — the quarantine is a temporal sequence (clutter accumulates, plan saved, context discarded at the gate, clean execution) — showing the polluted window being dropped at /clear dramatizes the reset that is the whole point.
FIGURE 4 — lethal trifecta: STATIC SUFFICIENT — a structural overlap with no process; the simultaneity is the message and reads instantly from one frame.
FIGURE 5 — three-failure diagnostic router: STATIC SUFFICIENT — a reference decision tree the reader scans non-linearly; animation would obscure rather than aid its lookup use.

Recommendation: Build all five as static vectors first (they carry the chapter unaided); promote Figures 1 and 3 to short animated builds if the companion volume or interactive edition warrants, since both encode genuine temporal mechanisms (monotonic fill; context quarantine).
