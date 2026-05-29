# CAJAL Figure Intelligence — Chapter 0 — Foundations: Sampling, Logits, and the Shape of a Distribution

Source: chapters/00-foundations-sampling-and-logits.md
Mode: /scan silent
Date: 2026-05-29

## Density Recommendation
4 figure candidates. Foundational density. The chapter is one chained mechanism — logits to softmax to temperature to truncation to chain-rule conditioning — so figures should make the *transformations of a distribution* visible rather than decorate the prose.

## Figure 1: The decoding pipeline — logits to sampled token
Priority: Critical
Trigger: MC — five interdependent stages (logits, scale by T, softmax, truncate, renormalize, sample) must occur in order, and the chapter explicitly fixes that order in §0.4
Figure type: Process flowchart
Concept statement: A token is emitted by a fixed-order pipeline that rescales raw logits, normalizes them to probabilities, truncates the tail, then draws a sample.
Reader prior knowledge: Reader knows softmax, temperature, and truncation as separate ideas from §0.2–0.4 but has not seen them composed as one ordered sequence.
Source anchor: Section: 0.4 Truncation: top-k and top-p — "The order of operations"

### Block 1 — Illustrae Paste Block
Create a blank, unannotated flat vector figure for single-column textbook width (89 mm) on a white background, with no generated text. Lay out a left-to-right horizontal process chain of six stages connected by single-headed arrows: (1) a vertical bar cluster representing raw logits of uneven height, (2) a divide-block representing temperature scaling, (3) a curved-bell block representing softmax normalization, (4) a bar cluster with the right-hand bars cut away representing truncation, (5) a compact bar cluster representing renormalization, (6) a single isolated highlighted bar representing the drawn sample. Use Sky Blue #56B4E9 for the input logits stage, Blue #0072B2 for the softmax normalization stage as the structural anchor, Orange #E69F00 for the temperature-scaling stage, Vermillion #D55E00 for the truncation stage where the tail is removed, Bluish Green #009E73 for the final sampled-token stage as the positive output, light gray for the renormalization connector, and Black #000000 for all arrows and bar outlines at 1 pt. Keep all six stages on one horizontal baseline, evenly spaced, arrows strictly single-headed and left-to-right.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89 mm textbook figure, 300 DPI, flat vector, white background, unannotated image layer for later typography.
[C - Content] Show only six ordered stages: raw logits, temperature scaling, softmax, truncation, renormalization, sampled token. Relationship to preserve: strict left-to-right ordering — temperature acts before softmax, truncation acts after softmax, sampling is last.
[O - Organization] Single horizontal process chain, one baseline, even spacing, single-headed arrows between adjacent stages only.
[P - Presentation] Flat vector, 1 pt black strokes, Okabe-Ito only: Sky Blue #56B4E9 (logits input), Orange #E69F00 (temperature scaling), Blue #0072B2 (softmax anchor), Vermillion #D55E00 (truncation), light gray (renormalization), Bluish Green #009E73 (sampled output), Black #000000 (arrows/outlines). No text in image.
[E - Exclusions]
- baked-in stage labels or equations
- vocabulary-size numbers or token strings
- branching paths or loops
- any stage beyond the six named
- background grid or axes ticks with numbers

### Block 3 — Negative Prompt
baked-in stage labels, equations, vocabulary numbers, token strings, branching paths, loops, extra stages, numbered axes, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 2: Temperature reshapes the distribution
Priority: Critical
Trigger: VG — the chapter draws an ASCII version of exactly this (§0.3, the temperature-scale sketch); the claim "low T sharpens, high T flattens" is structural and not conveyable from prose alone
Figure type: Comparison panels
Concept statement: Dividing every logit by temperature before softmax sharpens the distribution onto one token as T falls toward zero and flattens it toward uniform as T rises.
Reader prior knowledge: Reader has worked the three-token arithmetic at T = 0.5, 1, and 2 and has seen the author's rough ASCII rendering; this is the clean version.
Source anchor: Section: 0.3 Temperature — "The temperature scale, drawn on the page"

### Block 1 — Illustrae Paste Block
Create a blank, unannotated flat vector figure for single-column textbook width (89 mm) on a white background, with no generated text. Draw three side-by-side bar-chart panels of identical frame size sharing one common baseline, each panel containing the same number of vertical bars (five) but with different height profiles. Left panel: one tall dominant bar with the rest near zero, representing low temperature (sharp). Middle panel: a graded descending staircase of bars, representing neutral temperature. Right panel: five bars of nearly equal height, representing high temperature (flat, near-uniform). Every bar's y-axis baseline must start at zero. Use Blue #0072B2 for the bars in all three panels as the primary data series, light gray for each panel's frame and shared baseline, and Black #000000 for axis lines at 1 pt. Keep panels evenly spaced and equally sized; no color variation between panels, only height differs.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89 mm textbook figure, 300 DPI, flat vector, white background, unannotated.
[C - Content] Three equal panels, five bars each, y-axis from zero: panel 1 one tall bar (sharp), panel 2 descending staircase (neutral), panel 3 near-equal bars (flat). Relationship to preserve: same distribution under three temperatures, ranging from concentrated to uniform.
[O - Organization] Three comparison panels in a row, identical frames, shared baseline at zero, even spacing.
[P - Presentation] Flat vector, 1 pt strokes, Okabe-Ito: Blue #0072B2 for all bars, light gray for frames/baseline, Black #000000 for axes. No text in image.
[E - Exclusions]
- numeric axis labels or probability values
- token names under bars
- T-value annotations
- differing bar colors between panels
- any panel with bars not starting at zero

### Block 3 — Negative Prompt
numeric axis labels, probability values, token names, temperature annotations, differing panel colors, floating bars, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 3: Top-k versus top-p on three distribution shapes
Priority: Important
Trigger: PQ + VG — the chapter gives explicit probability vectors and shows the two rules selecting *different-size* candidate sets depending on distribution shape (peaked, medium, flat); the divergence is the load-bearing quantitative point
Figure type: Comparison panels (matrix)
Concept statement: A fixed-count cut (top-k) and an adaptive mass cut (top-p) keep the same set on a medium distribution but diverge on flat and peaked ones, because top-p's nucleus grows and shrinks with the model's uncertainty.
Reader prior knowledge: Reader has done the renormalization arithmetic and read the three worked vectors (medium p, flat q, peaked r) but has not seen the two cuts contrasted visually across shapes.
Source anchor: Section: 0.4 Truncation — "Top-p (nucleus) sampling" worked examples

### Block 1 — Illustrae Paste Block
Create a blank, unannotated flat vector figure for single-column textbook width (89 mm) on a white background, with no generated text. Build a small two-row by three-column grid of bar-chart cells, all cells the same frame size and sharing y-axis baselines at zero. The three columns represent three distribution shapes: a peaked profile (one tall bar, rest tiny), a medium profile (clear descending steps), and a flat profile (near-equal bars). The top row shows a fixed-width selection: in every top cell exactly three left-most bars are marked as kept and the remainder as discarded, regardless of shape. The bottom row shows an adaptive selection: the kept set is one bar in the peaked cell, three bars in the medium cell, and four bars in the flat cell. Use Bluish Green #009E73 to fill bars that are kept, light gray to fill bars that are discarded, Black #000000 for cell frames and baselines at 1 pt. Keep the grid aligned, equal cell sizes, no connecting arrows.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89 mm textbook figure, 300 DPI, flat vector, white background, unannotated.
[C - Content] 2x3 grid of bar charts. Columns = peaked, medium, flat distribution. Top row = fixed three-bar cut. Bottom row = adaptive cut keeping 1 / 3 / 4 bars. Relationship to preserve: top-k keeps a constant count across shapes; top-p keeps a variable count that tracks uncertainty.
[O - Organization] Aligned 2-row by 3-column matrix, equal cells, shared zero baselines, no arrows.
[P - Presentation] Flat vector, 1 pt strokes, Okabe-Ito: Bluish Green #009E73 (kept bars), light gray (discarded bars), Black #000000 (frames/baselines). No text in image.
[E - Exclusions]
- k or p threshold numbers
- probability values or token labels
- row or column headers
- arrows between cells
- bars not starting at zero

### Block 3 — Negative Prompt
threshold numbers, probability values, token labels, row headers, column headers, arrows between cells, floating bars, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 4: The chain-rule feedback loop
Priority: Important
Trigger: MC — autoregressive generation is a multi-step loop where each sampled token re-enters as conditioning for the next distribution; §0.5 hangs the whole "why prompting is engineering" argument on this feedback
Figure type: Cycle diagram
Concept statement: Each emitted token is appended to the running context, which reshapes the next conditional distribution, so a single early sample propagates forward through every subsequent step.
Reader prior knowledge: Reader has the chain-rule equation and the "feedback" prose but has not seen the loop where output becomes the next step's input.
Source anchor: Section: 0.5 What the distribution is conditioned on

### Block 1 — Illustrae Paste Block
Create a blank, unannotated flat vector figure for single-column textbook width (89 mm) on a white background, with no generated text. Draw a horizontal sequence of three context-block rectangles growing in length left to right (each longer than the last to show the context accumulating). Below each context block sits a small distribution glyph (a tiny bar cluster), and from each distribution glyph a single-headed arrow points to a single sampled-token marker. A second single-headed arrow then curves from each sampled-token marker up into the *next*, longer context block, showing the token being appended. Use Sky Blue #56B4E9 for the context blocks as the conditioning structure, Blue #0072B2 for the distribution glyphs as the primary computed object, Bluish Green #009E73 for the sampled-token markers as the positive output, Black #000000 for all arrows and outlines at 1 pt. Keep the growth of the context blocks visible and the append-arrows clearly feeding forward, never backward.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89 mm textbook figure, 300 DPI, flat vector, white background, unannotated.
[C - Content] Three growing context blocks; under each a distribution glyph; each glyph arrows to a sampled-token marker; each marker arrows forward into the next, longer context block. Relationship to preserve: output token feeds back as conditioning for the next distribution; context strictly grows.
[O - Organization] Left-to-right forward-feeding loop, growing context rectangles, single-headed arrows only, no backward arrows.
[P - Presentation] Flat vector, 1 pt strokes, Okabe-Ito: Sky Blue #56B4E9 (context blocks), Blue #0072B2 (distribution glyphs), Bluish Green #009E73 (sampled tokens), Black #000000 (arrows/outlines). No text in image.
[E - Exclusions]
- token strings or words inside context blocks
- probability numbers on the glyphs
- subscript indices
- backward or dual-headed arrows
- a closed circular loop (the flow is forward, not cyclic-return)

### Block 3 — Negative Prompt
token strings, words in blocks, probability numbers, subscript indices, backward arrows, closed circular loops, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video Candidate Pass
FIGURE 1 — decoding pipeline: STATIC SUFFICIENT — ordered stages, no continuous parameter — the six-stage flow reads in one pass and has no animatable variable.
FIGURE 2 — temperature reshaping: VIDEO CANDIDATE — continuous-parameter sweep — sliding T from 0 to infinity and watching the bars morph from a single spike to uniform is the single most animation-native idea in the chapter.
FIGURE 3 — top-k vs top-p: VIDEO CANDIDATE — adaptive-cut demonstration — animating the nucleus boundary sliding inward/outward as the distribution shape changes makes "the cut tracks uncertainty" self-evident; static matrix is a strong fallback.
FIGURE 4 — chain-rule feedback: STATIC SUFFICIENT — discrete step sequence — the forward-feed reads fine as a static three-step strip; animation adds little beyond the arrows.

Recommendation: ship all four as static figures; prioritize Figure 2 (and secondarily Figure 3) for an optional interactive/animated companion, since both turn on a continuous parameter the static page can only sample.
