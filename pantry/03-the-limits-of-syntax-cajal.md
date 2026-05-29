# CAJAL Figure Intelligence — Chapter 3 — The Limits of Syntax

Source: chapters/03-the-limits-of-syntax.md
Mode: /scan silent
Date: 2026-05-29

## Density Recommendation
4 figure candidates. Mechanistic density. The chapter's load-bearing ideas — the Chinese Room as a symbol-manipulation pipeline, the syntax-to-semantics gap, the adversarial-collapse magnitudes, and the agentic contract-review workflow with a human node — are all structural or quantitative claims that a reader cannot reconstruct from prose alone.

## Figure 1: The Chinese Room as Symbol Pipeline
Priority: Critical
Trigger: MC — process of ≥3 interdependent steps (symbols in → rule lookup → symbols out, with the observer's false inference as a parallel node)
Figure type: Systems diagram
Concept statement: A formal system can pass uninterpreted symbols through a rulebook and emit fluent output that an outside observer mistakes for understanding, even though no semantic connection to meaning occurs anywhere inside.
Reader prior knowledge: Familiar with the idea of input/output but not with the syntax/semantics distinction made spatial.
Source anchor: Section: 3.3 A room with no windows

### Block 1 — Illustrae Paste Block
Draw a flat vector systems diagram of a closed room. On the left, an input slot where a stack of symbol cards enters; an arrow leads inward to a large central box representing a rulebook lookup, with a smaller box beside it for the operator who matches incoming shapes to outgoing shapes. An arrow leads from the rulebook box to an output slot on the right where a second stack of symbol cards exits. Outside the room on the right, place a separate observer node connected to the output slot by a dotted arrow labeled by position only, with a thought-bubble shape representing the false inference of understanding. Use roughly six components: input slot, rulebook box, operator box, output slot, observer node, inference bubble. Render the room wall as a solid enclosing rectangle. Color the rulebook and operator (the syntactic core) in blue #0072B2, the observer and its inference bubble (the mistaken semantic attribution) in vermillion #D55E00, the symbol-card stacks in neutral light gray, and connecting arrows in black #000000. Single arrowheads only, left-to-right flow. Blank unannotated flat vector on white, single column.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook figure, 300 DPI, vector, white background, unannotated.
[C - Content] Six components: input slot, rulebook lookup box, operator box, output slot, external observer node, inference thought-bubble; enclosed by a room-wall rectangle. Preserve that the syntactic core is sealed inside and the observer's inference is external and dotted.
[O - Organization] Strict left-to-right flow: input slot → rulebook/operator → output slot, all inside the wall rectangle; observer sits outside to the right, joined to the output by a dotted connector; inference bubble above the observer.
[P - Presentation] Flat vector, Okabe-Ito only — rulebook + operator #0072B2, observer + inference bubble #D55E00, symbol stacks light gray, arrows #000000, room wall #000000 1pt stroke. No text in image.
[E - Exclusions] No Chinese characters or any glyphs on the cards, no faces on the operator or observer, no brains, no speech text, no labels of any kind.

### Block 3 — Negative Prompt
Chinese characters, alphabet glyphs, readable cards, human faces, brain icons, speech bubbles with words, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 2: The Transformer Attention Pipeline as Syntax
Priority: Important
Trigger: MC — process of ≥3 interdependent steps (tokens → embedding → attention Q/K/V → softmax → layer stack → sampled token)
Figure type: Process flowchart
Concept statement: Every stage from input token to sampled output is a mathematical operation on numerical arrays, with no step that connects a symbol to a real-world referent.
Reader prior knowledge: Has seen the attention equation but not the end-to-end pipeline laid out as discrete stages.
Source anchor: Section: 3.4 Inside the room: the transformer as symbol manipulation

### Block 1 — Illustrae Paste Block
Draw a flat vector vertical process flowchart of seven stacked stages connected by downward single-headed arrows: (1) input token sequence shown as a row of small uniform squares, (2) embedding stage shown as a row of taller vector bars, (3) an attention block drawn as three parallel inputs Q, K, V converging into one combination node, (4) a softmax normalization node drawn as a small distribution shape, (5) a weighted-value output node, (6) a stack-of-layers symbol indicating repetition, (7) a final projection node emitting one highlighted output square. Use eight components maximum. Keep all seven stages in a single vertical column with even spacing. Color the entire pipeline in blue #0072B2 to signal it is one uniform syntactic mechanism, with the three Q/K/V inputs differentiated in orange #E69F00, and the final sampled output square in green #009E73 to mark it as the emitted token. Arrows black #000000, single-headed, top-to-bottom. No equations, no variable letters, no labels. Blank unannotated flat vector on white, single column.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook figure, 300 DPI, vector, white background, unannotated.
[C - Content] Seven stages: token row, embedding bars, Q/K/V convergence, softmax node, weighted-value node, repeated-layer stack symbol, final projection emitting one output square. Preserve that all stages are uniform mathematical operations in one chain.
[O - Organization] Single vertical column, evenly spaced, downward single-headed arrows between every stage; Q/K/V shown as three parallel paths merging into one node.
[P - Presentation] Flat vector, Okabe-Ito — pipeline body #0072B2, Q/K/V inputs #E69F00, final emitted token #009E73, arrows #000000 1pt. No text, no equations, no variable symbols.
[E - Exclusions] No mathematical notation, no Q/K/V letters or any letters, no softmax formula, no numbers, no labels, no matrix grids with values.

### Block 3 — Negative Prompt
mathematical notation, equations, letters Q K V, numbers, matrix values, softmax formula, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 3: Adversarial Collapse — Competence Drops Under Variant Tests
Priority: Critical
Trigger: PQ — percentages/magnitudes (standard 90–95% vs. adversarial ~55–70%), and the magnitude of the drop is the argument
Figure type: Statistical/quantitative
Concept statement: When a familiar benchmark is rewritten to disrupt the statistical pattern while preserving logical structure, model accuracy collapses from the 90–95% range to roughly 55–70%, and the size of that drop reveals the competence was syntactic rather than structural.
Reader prior knowledge: Understands the claim that benchmarks can be solved by pattern-matching; needs the magnitude made visible.
Source anchor: Section: 3.4.1 The strongest case against the room

### Block 1 — Illustrae Paste Block
Draw a flat vector grouped bar chart with a y-axis beginning at zero and running to 100 (gridline marks only, no numerals). Show two pairs of vertical bars along the x-axis. Pair one represents standard-benchmark accuracy as a tall bar reaching about 92 of 100; pair two represents adversarial-variant accuracy as a much shorter bar reaching about 60 of 100. Optionally include a second matched pair to show the contrast holds across two conditions, but keep to no more than four bars total. Color the standard/high bars in blue #0072B2 (the apparently competent condition) and the adversarial/collapsed bars in vermillion #D55E00 (the failure condition). Add a thin horizontal reference line where a noise-level drop would sit near the top, in neutral light gray, to make clear the observed drop is far larger than noise. The y-axis must start at zero. No numerals, no bar labels, no axis text. Blank unannotated flat vector on white, single column.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook figure, 300 DPI, vector, white background, unannotated.
[C - Content] A grouped bar chart, up to four bars: tall bars for standard-benchmark accuracy (~92/100), short bars for adversarial-variant accuracy (~60/100), plus one faint horizontal reference line marking a noise-level band near the top. Preserve the large vertical gap between the two conditions.
[O - Organization] Vertical bars on a zero-based y-axis (0–100), standard condition on the left of each pair, adversarial on the right; even bar spacing; gridlines without numerals.
[P - Presentation] Flat vector, Okabe-Ito — standard bars #0072B2, collapsed bars #D55E00, reference line light gray, axes #000000 1pt. No numerals, no text.
[E - Exclusions] No axis numbers, no percentage labels, no legend text, no data values, no title.

### Block 3 — Negative Prompt
axis numbers, percentage labels, data values, legend text, gridline numerals, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 4: The Contract-Review Agent — Syntactic Steps, Semantic Anchors, Human Node
Priority: Critical
Trigger: MC — process of ≥7 interdependent labeled steps with distinct node types and a redirect loop
Figure type: Process flowchart
Concept statement: An agentic workflow alternates syntactic model steps with tool-grounded semantic anchors and routes the one judgment the model structurally cannot make through a mandatory human decision node, which then redirects a new syntactic task back to the model.
Reader prior knowledge: Knows what an agent and a tool call are; needs the role-type of each step made visible.
Source anchor: Section: 3.7.1 Worked example: a contract-review agent

### Block 1 — Illustrae Paste Block
Draw a flat vector vertical process flowchart of seven nodes connected top-to-bottom by single-headed arrows, with one feedback arrow looping from the sixth node back up to a model step. Node 1: agent generates a plan. Node 2: document parser returns ground-truth text. Node 3: model processes each clause. Node 4: industry-benchmark database returns external data. Node 5: a distinctly shaped human decision node (use a diamond) where judgment occurs. Node 6: human redirects a new task back to the model, drawn with a curved feedback arrow returning to node 3. Node 7: final structured risk report. Use seven components. Color the model/syntactic nodes (1, 3) in blue #56B4E9, the tool-grounded semantic-anchor nodes (2, 4) in green #009E73, the human decision node (5) and its redirect (6) in orange #E69F00, and the final report (7) in neutral light gray. Arrows black #000000, single-headed; the redirect loop is a single curved arrow. Blank unannotated flat vector on white, single column.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook figure, 300 DPI, vector, white background, unannotated.
[C - Content] Seven nodes: plan generation, document parser, per-clause processing, benchmark database, human decision (diamond), human redirect, final report; one feedback loop from redirect back to per-clause processing. Preserve the alternation of node roles and the mandatory human gate before the report.
[O - Organization] Single vertical column top-to-bottom with single-headed arrows; the human node is a diamond breaking the rectangular rhythm; one curved feedback arrow returns upward to the processing node.
[P - Presentation] Flat vector, Okabe-Ito — model/syntactic nodes #56B4E9, tool/semantic-anchor nodes #009E73, human decision + redirect #E69F00, final report light gray, arrows #000000 1pt. No text in image; distinguish node roles by color and shape only.
[E - Exclusions] No clause text, no contract excerpts, no human figures or faces, no labels, no dollar amounts, no document content.

### Block 3 — Negative Prompt
contract text, clause excerpts, dollar amounts, document content, human faces, human figures, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video Candidate Pass
FIGURE 1 — Chinese Room symbol pipeline: STATIC SUFFICIENT — single fixed mechanism — the false-inference relationship is grasped in one frame and gains nothing from motion.
FIGURE 2 — Transformer attention pipeline: VIDEO CANDIDATE — sequential transformation through stacked layers — animating one token's path through embedding, attention, softmax, and repeated layers could make the "operation on arrays at every step" claim vivid, but static is adequate for the textbook.
FIGURE 3 — Adversarial collapse bar chart: STATIC SUFFICIENT — the argument is the magnitude of a fixed comparison — a static zero-based bar pair makes the drop unmistakable.
FIGURE 4 — Contract-review agent workflow: VIDEO CANDIDATE — multi-step process with a feedback loop and a human gate — stepping through the alternation of syntactic, semantic-anchor, and human nodes in sequence would reinforce the role distinctions, though the static flowchart conveys the architecture.

Recommendation: Render all four as static figures for the chapter; Figures 1, 3, and 4 are Critical and load-bearing, Figure 2 is Important. No video is required, though Figures 2 and 4 are the strongest animation candidates if a companion format is later produced.
