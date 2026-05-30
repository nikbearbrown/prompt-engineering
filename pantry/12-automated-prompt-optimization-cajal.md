# CAJAL Figure Intelligence — Chapter 12 — Automated Prompt Optimization: The Post-Manual Era

Source: chapters/12-automated-prompt-optimization.md
Mode: /scan silent
Date: 2026-05-29

## Density Recommendation
4 figure candidates. Mechanistic density. The chapter's load is structural and procedural — a search-loop mechanism, a 2-axis optimizer taxonomy, a 5-step worked pipeline, and a yes/no decision gate — so figures carry process and relationship that prose states but cannot make visible at a glance.

## Figure 1: The optimization loop (write → score → propose)
Priority: Critical
Trigger: MC — the propose-score-feedback loop is a ≥3-step interdependent cycle that repeats until convergence
Figure type: Cycle diagram
Concept statement: Automated prompt optimization replaces the human "write-observe-tweak" loop with a mechanical cycle in which a proposer generates a candidate prompt, a scalar metric scores it against a labeled eval set, and the score feeds back to drive the next proposal.
Reader prior knowledge: Familiar with iterative prompt editing by hand; new to formalizing it as a closed optimization loop with a metric and eval set as fixed inputs.
Source anchor: Section: 12.2 The reframe: prompting as a search problem

### Block 1 — Illustrae Paste Block
Draw a closed clockwise cycle of four nodes connected by single-headed arrows on a white background. Node one is a rounded rectangle labeled-position for the proposer, drawn in primary blue #56B4E9. An arrow leads to node two, a rectangle for the candidate prompt, in neutral gray. An arrow leads to node three, a rectangle for the language model running the prompt on an eval-set example, in secondary orange #E69F00. An arrow leads to node four, a rectangle for the scalar metric scoring output against reference, in active green #009E73. A return arrow closes the loop from the metric node back to the proposer, carrying the feedback. Place two flat input shapes feeding the metric node from outside the cycle, drawn in gray as fixed user-supplied inputs: a small stack-of-pages shape for the labeled eval set and a small function shape for the metric. Keep all five-to-six components evenly spaced around a central circular flow. Use 1pt strokes, flat vector, no text inside the image, single-headed arrows only, Okabe-Ito palette exclusively.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Confirmed components: proposer node, candidate-prompt node, LM-execution node, scalar-metric node, plus two external fixed-input shapes (labeled eval set, metric function). Relationship: a closed feedback cycle where score returns to proposer; eval set and metric feed in from outside as user-supplied constants.
[O - Organization] Four nodes arranged around a central clockwise circular flow connected by single-headed arrows; closing feedback arrow from metric back to proposer; two external input shapes entering the metric node from the left margin.
[P - Presentation] Flat vector, Okabe-Ito only: proposer #56B4E9, candidate-prompt gray, LM #E69F00, metric #009E73, external inputs gray. 1pt strokes, no text in image.
[E - Exclusions] No human figure, no brain or robot iconography, no gauges or dials, no dollar signs, no clocks, no metric numbers shown.

### Block 3 — Negative Prompt
human figures, robot icons, brain icons, dials, gauges, numeric scores, dollar signs, clocks, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 2: DSPy Signature compiles to model-specific prompts
Priority: Critical
Trigger: VG — the "declare the what, compile the how" claim (one typed contract → different prompt strings per model) is structural and not depictable from the text alone
Figure type: Systems diagram
Concept statement: A DSPy Signature is a single typed input→output contract that a compiler expands, via the optimizer, into different concrete prompt strings (instruction plus demonstrations) for different model families — same what, different how.
Reader prior knowledge: Understands input/output typing loosely; may conflate the Signature with the final prompt text it never contains.
Source anchor: Section: 12.2 — The Signature: declare the what, let the compiler find the how

### Block 1 — Illustrae Paste Block
Draw a left-to-right three-stage diagram on white. At left, a single clean rectangle representing the Signature as a typed contract (an input field shape, an arrow glyph, an output field shape inside it), drawn in primary blue #0072B2 to mark it as the canonical source. A single-headed arrow leads right into a central diamond-or-gear shape representing the compiler/optimizer, drawn in active green #009E73. From the compiler, two divergent single-headed arrows fan out to the right into two separate output rectangles representing two compiled prompts for two different model families, each drawn in secondary orange #E69F00. Make the two output rectangles visibly different in internal proportion — one shorter with three small demonstration slots, one taller with six — to show same-contract, different-realization without any text. Keep to six components total. Use 1pt strokes, flat vector, white background, single-headed arrows only, no text in the image, Okabe-Ito palette exclusively.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Confirmed components: one Signature contract block (input field, arrow glyph, output field), one compiler/optimizer node, two divergent compiled-prompt output blocks differing in internal slot count. Relationship: one source contract fans out through the compiler into two distinct model-specific prompt realizations.
[O - Organization] Left-to-right flow: Signature → compiler → fan-out to two outputs; the two outputs stacked vertically at right and visibly different in proportion and slot count.
[P - Presentation] Flat vector, Okabe-Ito only: Signature #0072B2, compiler #009E73, both outputs #E69F00. 1pt strokes, no text in image.
[E - Exclusions] No code syntax, no quotation marks, no readable instruction text, no model logos or brand marks, no human figure, no equation.

### Block 3 — Negative Prompt
code syntax, quotation marks, readable instructions, model logos, brand marks, equations, human figures, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 3: The optimizer grid — search strategy × what is optimized
Priority: Important
Trigger: VG — a 2-axis taxonomy placing five optimizer families by search strategy and optimization target is a structural relationship the prose tabulates but does not show spatially
Figure type: Conceptual map
Concept statement: The optimizer families differ along two axes — how they search the prompt space (propose-and-score, trajectory-feedback, textual-gradient, evolutionary, Bayesian) and what they optimize (instructions, demonstrations, or both) — and occupy distinct cells of that grid.
Reader prior knowledge: Has met the named optimizers individually; needs the spatial layout that makes "they are not all the same" legible.
Source anchor: Section: 12.3 The optimizer zoo, in one grid

### Block 1 — Illustrae Paste Block
Draw a 2-axis grid on white: a vertical axis with five stacked row-bands for the five search strategies, and a horizontal axis with three column-bands for instructions / demonstrations / both. Render the grid lines in neutral gray at 1pt. Place five filled marker cells positioned to show occupancy: four markers in the leftmost (instructions) column at four successive rows, drawn in secondary orange #E69F00, and one marker in the rightmost (both) column at the bottom row, drawn in primary blue #0072B2 to single out the Bayesian joint-space method as distinct. Leave the demonstrations-only column empty to show the field clusters on instructions. Keep the five markers as simple flat filled rounded squares of equal size. Total components: the grid frame plus five markers. Use 1pt strokes, flat vector, white background, no text in the image, no axis numbers, Okabe-Ito palette exclusively. Do not draw arrows; this is a positional map, not a flow.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Confirmed components: a 5-row by 3-column grid frame; five occupancy markers — four in the leftmost column across four rows, one in the rightmost column bottom row. Relationship: positional placement encodes search strategy (rows) against optimization target (columns); empty middle column shows clustering.
[O - Organization] Vertical axis = five search-strategy bands; horizontal axis = three target columns; markers placed in occupied cells only.
[P - Presentation] Flat vector, Okabe-Ito only: grid lines gray, four instruction-column markers #E69F00, single both-column marker #0072B2. 1pt strokes, no text, no numbers.
[E - Exclusions] No arrows, no axis tick numbers, no method names, no legend, no checkmarks, no human figure, no 2x2 quadrant shading.

### Block 3 — Negative Prompt
arrows, axis numbers, method names, legend keys, checkmarks, quadrant shading, human figures, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 4: The decision gate — four questions, two lanes
Priority: Important
Trigger: MC — a four-condition gate routing a task into one of two procedural lanes is a multi-step conditional process
Figure type: Process flowchart
Concept statement: A task is routed to the automated lane only if all four gate conditions (metric, eval set, high volume, stability) hold; any single failure sends it to the manual prompt-and-eyeball lane.
Reader prior knowledge: Comfortable with flowchart conventions; needs the all-yes/any-no branch logic made explicit.
Source anchor: Section: 12.5 The decision gate: when to optimize, when to hand-tune

### Block 1 — Illustrae Paste Block
Draw a top-to-bottom flowchart on white. At top, a single entry rectangle for the incoming task in neutral gray. A single-headed arrow leads down into a tall decision block containing four small stacked condition rows (four thin rounded bars) representing metric, eval set, high volume, stability — draw this gate block outline in primary blue #56B4E9 with the four inner bars in gray. From the gate, two single-headed branch arrows diverge: a left-down arrow labeled by position as the all-yes path leading to the automated lane, and a right-down arrow as the any-no path leading to the manual lane. The automated-lane terminal is a rounded rectangle in active green #009E73. The manual-lane terminal is a rounded rectangle in secondary orange #E69F00. Inside the automated terminal place three tiny sequential sub-boxes suggesting signature→optimizer→compiled-prompt; inside the manual terminal place a small two-box loop suggesting write↔tweak. Keep to about seven components. Use 1pt strokes, flat vector, white, single-headed arrows only, no text in image, Okabe-Ito palette exclusively.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Confirmed components: task entry block; four-condition gate block with four inner bars; two branch arrows (all-yes, any-no); automated-lane terminal with three sequential sub-boxes; manual-lane terminal with a two-box loop. Relationship: conjunctive gate — all four pass → automated; any fail → manual.
[O - Organization] Vertical flow top to bottom; gate diverges into two lanes side by side below it; automated lane left, manual lane right.
[P - Presentation] Flat vector, Okabe-Ito only: task entry gray, gate outline #56B4E9 with gray inner bars, automated terminal #009E73, manual terminal #E69F00. 1pt strokes, no text in image.
[E - Exclusions] No yes/no words, no question-mark glyphs, no human figure, no traffic-light imagery, no gears, no dollar signs.

### Block 3 — Negative Prompt
yes/no words, question marks, traffic lights, gears, dollar signs, human figures, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video Candidate Pass
FIGURE 1 — the optimization loop: VIDEO CANDIDATE — temporal iteration — the loop's value is its repetition-to-convergence; a short animation cycling the score back into the proposer over several rounds would show convergence that a single static frame cannot.
FIGURE 2 — Signature compiles to model-specific prompts: STATIC SUFFICIENT — single fan-out relationship — the same-what/different-how claim resolves fully in one frame.
FIGURE 3 — the optimizer grid: STATIC SUFFICIENT — positional taxonomy — a map of fixed positions has no temporal dimension.
FIGURE 4 — the decision gate: STATIC SUFFICIENT — conditional branch — the all-yes/any-no logic is fully legible in one static flowchart.

Recommendation: ship all four as static figures; optionally promote Figure 1 to a short looping animation if the chapter's digital edition supports motion, since convergence-over-rounds is the one genuinely temporal idea here.
