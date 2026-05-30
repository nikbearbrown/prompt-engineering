# CAJAL Figure Intelligence — Chapter 10 — Long-Context Prompting: Position, Retrieval, and Injection

Source: chapters/10-long-context-prompting.md
Mode: /scan silent
Date: 2026-05-29

## Density Recommendation
5 figure candidates. Mixed density. The spine is one strong quantitative U-curve (lost-in-the-middle, PQ), flanked by a multi-needle collapse bar chart (PQ), a position-as-attack-surface bar chart (PQ), and two structural figures — the recency-from-autoregression mechanism and the recommended prompt-layout schematic.

## Figure 1: The U-shaped position–accuracy curve
Priority: Critical
Trigger: PQ — the chapter's empirical spine, a(0) ≈ a(1) > a(0.5): accuracy plotted against the relative position of the relevant fact, high at both edges and sagging tens of points in the middle (Liu et al. 2024)
Figure type: Statistical/quantitative
Concept statement: A model does not read a long context uniformly — accuracy on a fact is highest when it sits at the beginning (primacy) or end (recency) of the input and drops sharply in the middle, tracing a U-shaped curve.
Reader prior knowledge: Accuracy as a percentage; relative position of a fact in the input from 0% (start) to 100% (end); the serial-position effect as a human prior (§10.2).
Source anchor: Section: 10.2 The U-shaped curve

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector line chart on a white background with a horizontal axis running left to right representing the position of the relevant fact from start to end, and a vertical accuracy axis starting at zero. Plot one smooth continuous U-shaped curve: high at the far left, descending to a clear trough in the horizontal center, then rising again to high at the far right — the two ends at similar height, the middle markedly lower. Render the curve as a single 1.5pt line in primary blue #0072B2. Mark three reference points on the curve with small filled dots: a left-edge dot and a right-edge dot both high, rendered in active green #009E73 (the well-read positions), and a center dot at the trough rendered in blocking orange #D55E00 (the lost-in-the-middle position). Draw a thin neutral-gray horizontal guide from each green edge dot toward the center to make the edge-vs-trough gap visually readable. Keep components minimal: one curve, three dots, two guide segments, two axes. Use only Okabe-Ito colors: #0072B2 curve, #009E73 edge dots, #D55E00 trough dot, neutral gray guides, #000000 axes. No numbers, no text, no labels anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] One smooth U-shaped accuracy-vs-position curve with similar-height left and right ends and a lower central trough; three marked points (two high edges, one low center); guide segments showing the gap.
[O - Organization] Position on x (start→end), accuracy on y from zero; curve high-low-high; edge dots green, trough dot orange; gray guides linking edges to trough height.
[P - Presentation] Flat vector, 1.5pt curve, 1pt axes; Okabe-Ito only — #0072B2 curve, #009E73 edge dots, #D55E00 trough dot, neutral gray guides, #000000 axes.
[E - Exclusions] No numeric axis values, percentages, or position labels; no second curve; no gridlines; no shaded fill under the curve; no color beyond named hexes; no red-green adjacency on the same mark.

### Block 3 — Negative Prompt
numeric axis values, percentage labels, position labels, second curve, gridlines, shaded area fill, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 2: Why recency — the autoregressive anchor
Priority: Important
Trigger: VG — the load-bearing mechanism (next-token prediction conditions each token on the immediately preceding ones, so recent context is weighted heavily) is a structural claim about how the objective produces recency bias, not depictable from text
Figure type: Mechanism cross-section
Concept statement: Recency bias is the autoregressive next-token objective viewed from the prompt side — each token is predicted from the ones immediately before it, so local recent context dominates and is weighted most heavily.
Reader prior knowledge: Autoregressive generation t_i ~ P(t_i | t_0…t_{i-1}); local context as the strongest predictor of the next token (§10.2).
Source anchor: Section: 10.2 Why recency: the autoregressive artifact

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector mechanism figure on a white background showing a single horizontal row of evenly spaced token cells, eight cells left to right, representing a sequence. The rightmost position is the token being predicted, drawn as an open/empty cell with a small target ring; render it active green #009E73. From the cells immediately to its left, draw several single-headed conditioning arrows curving into the predicted cell, with the arrows from the nearest cells drawn thick and bold and the arrows from cells further left drawn progressively thinner, so the visual weight concentrates on the most recent neighbors. Render the near (heavy) conditioning arrows in primary blue #0072B2 and the far (faint) arrows in neutral gray to show attenuating influence with distance. The earlier token cells themselves are plain neutral-gray outlined boxes. Keep components to eight cells plus the graded arrow set. Use only Okabe-Ito colors: #009E73 predicted cell, #0072B2 heavy near arrows, neutral gray far arrows and cells, #000000 cell outlines. No numbers, no text, no letters anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] A row of eight token cells; the rightmost is the token being predicted; conditioning arrows from prior cells, weighted thick-near / thin-far to show recent context dominating.
[O - Organization] Single horizontal sequence; predicted cell at right with target ring; graded single-headed arrows fanning into it from the left, heaviest from nearest neighbors.
[P - Presentation] Flat vector; arrow stroke graded 2pt→0.5pt by distance; Okabe-Ito only — #009E73 predicted cell, #0072B2 heavy near arrows, neutral gray far arrows and prior cells, #000000 outlines.
[E - Exclusions] No token text, no index numbers, no probability values, no captions; no attention-matrix heatmap; no more than eight cells; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
token text, index numbers, probability values, captions, attention heatmap grid, more than eight cells, text labels, words, gibberish letters, titles, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 3: Multi-needle collapse
Priority: Important
Trigger: PQ — the gotcha number: single-needle retrieval ~95% drops to ~40% for three needles in English (multilingual NIAH 2024), the benchmark that looks solved hiding the real failure
Figure type: Statistical/quantitative
Concept statement: Single-needle retrieval is largely solved (~95%), but asking for three facts at once collapses accuracy to roughly 40% — synthesis is not retrieval, and the U-curve applies to each needle separately.
Reader prior knowledge: Needle-in-a-haystack retrieval; needle count (1 vs 3); accuracy as a percentage (§10.3).
Source anchor: Section: 10.3 Multi-needle collapse: the benchmark that hides the failure

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector bar chart on a white background with the vertical accuracy axis starting at zero and running to full height, and three bars along the horizontal axis representing increasing needle count (one, two, three target facts). The first bar (one needle) is tall, reaching roughly nineteen-twentieths of full height; render it active green #009E73 to mark the solved case. The second bar (two needles) is noticeably shorter, an intermediate height; render it secondary orange #E69F00. The third bar (three needles) is short, reaching roughly two-fifths of full height; render it blocking orange #D55E00 to mark the collapse. All three bars rise from a common zero baseline with equal width and even spacing. Draw a plain y-axis and baseline with no tick numbers. Optionally add one thin neutral-gray downward step bracket spanning from the top of bar one to the top of bar three to emphasize the drop. Total: three bars plus axis. Use only Okabe-Ito colors: #009E73 one needle, #E69F00 two needles, #D55E00 three needles, #000000 axis, neutral gray drop bracket. No numbers, no text, no labels anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Three accuracy bars by needle count (1 tall ≈ solved, 2 intermediate, 3 short ≈ collapse), y from zero; optional gray bracket marking the top-of-bar-one to top-of-bar-three drop.
[O - Organization] Three bars left to right by increasing needle count; common zero baseline; equal width and spacing; descending heights.
[P - Presentation] Flat vector, 1pt strokes, bars from zero; Okabe-Ito only — #009E73 / #E69F00 / #D55E00 by needle count, neutral gray drop bracket, #000000 axis.
[E - Exclusions] No numeric value labels, axis tick numbers, percentages, or legend; no needle-count text; no 3D bars; no color beyond named hexes; keep green and orange-family bars non-adjacent in hue reading (no red-green pairing).

### Block 3 — Negative Prompt
value labels on bars, axis tick numbers, percentage text, legend text, needle-count labels, 3D bars, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 4: Position is an attack surface
Priority: Important
Trigger: PQ — the NINJA result (attack success 23.7% baseline → 58.8% on Llama-3.1-8B when the harmful goal is moved to the front; goal-at-end mitigates) ties the U-curve directly to a security control
Figure type: Statistical/quantitative
Concept statement: The same position machinery is an attack surface — placing a harmful goal at the front of a long context raises attack success far above baseline, and placing it at the end mitigates, which is why safety rules belong last.
Reader prior knowledge: Attack-success rate as a percentage; the U-curve front/end advantage from §10.2; baseline vs perturbed condition (§10.5).
Source anchor: Section: 10.5 Position is an attack surface

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector bar chart on a white background with the vertical attack-success axis starting at zero and three bars along the horizontal axis representing three placements of the harmful goal: baseline (no position manipulation), goal-at-front, and goal-at-end. The baseline bar is a low-to-moderate height drawn in neutral gray. The goal-at-front bar is the tallest, reaching well above baseline, rendered in blocking orange #D55E00 to mark the worst (most successful attack) condition. The goal-at-end bar is the shortest, at or below baseline, rendered in active green #009E73 to mark the mitigated (safest) condition. All three bars rise from a common zero baseline with equal width and even spacing. Draw a thin neutral-gray horizontal dashed-free reference line across at the baseline-bar height so front-above and end-below read immediately. Plain y-axis, no tick numbers. Total: three bars, one reference line, axis. Use only Okabe-Ito colors: neutral gray baseline, #D55E00 goal-at-front, #009E73 goal-at-end, #000000 axis and reference line. No numbers, no text, no labels anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Three attack-success bars (baseline gray, goal-at-front tallest = worst, goal-at-end shortest = mitigated), y from zero; one horizontal reference line at baseline height.
[O - Organization] Three bars left to right (baseline, front, end); common zero baseline; reference line at baseline height to show front-above / end-below.
[P - Presentation] Flat vector, 1pt strokes, bars from zero; Okabe-Ito only — neutral gray baseline, #D55E00 front, #009E73 end, #000000 axis and reference line.
[E - Exclusions] No numeric value labels, axis tick numbers, percentages, model names, or legend; no second model's bars; no 3D bars; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
value labels on bars, axis tick numbers, percentage text, model name labels, legend text, second-model bars, 3D bars, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 5: The recommended long-context layout
Priority: Supplementary
Trigger: VG — the chapter's prescriptive layout schematic (low-priority context up top, filler in the middle trough, high-priority instruction + safety rules + most-relevant facts + user question at the recency-favored bottom) is a structural placement claim
Figure type: Structural schematic
Concept statement: Because recency makes the bottom of the assembled prompt the most-attended region, the engineered layout puts low-priority context up top, filler in the under-attended middle, and the load-bearing tokens — instruction, safety rules, key facts, the question — last.
Reader prior knowledge: The U-curve (Fig. 1); the four placement rules; instructions-last as both quality and safety control (§10.4–10.5).
Source anchor: Section: 10.4 Placement rules you can test

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector schematic on a white background showing one tall vertical rectangular container divided into three stacked horizontal zones representing the assembled prompt from top to bottom. The top zone (low-priority context / system role) is a plain neutral-gray band. The middle zone (filler / mid-relevance documents) is a larger neutral-gray band drawn lighter and marked with a small inward-pointing trough indicator — a shallow concave notch on its side — to signal the lost-in-the-middle under-attended region. The bottom zone is subdivided into a small stack of three or four thin sub-bands representing the load-bearing tokens (highest-priority instruction, safety/constraint rules, most-relevant facts, user question), all rendered in active green #009E73 to mark the high-attention recency-favored region. Place a vertical attention-weight gradient indicator alongside the right edge as a simple set of tick marks growing from short at top through shortest at the middle trough to tallest at the bottom — drawn in primary blue #0072B2 — mirroring the U-curve's recency dominance. Keep to three zones plus the bottom sub-bands and the side ticks. Use only Okabe-Ito colors: neutral gray top and middle, #009E73 bottom load-bearing sub-bands, #0072B2 side attention ticks, #000000 container outline. No numbers, no text, no labels anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] A vertical prompt container in three zones — low-priority top (gray), filler middle with a trough notch (light gray), load-bearing bottom subdivided into instruction / safety rules / key facts / question (green); a side attention-tick indicator peaking at the bottom.
[O - Organization] Top-to-bottom stack; trough marked in the middle; bottom emphasized as high-attention; side ticks rise to a maximum at the bottom.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — neutral gray top/middle, #009E73 bottom sub-bands, #0072B2 side attention ticks, #000000 container outline.
[E - Exclusions] No zone-label text, no token-type words, no numbers, no captions; no more than four bottom sub-bands; no actual document text; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
zone label text, token-type words, numbers, captions, document text, more than four bottom sub-bands, text labels, words, gibberish letters, titles, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video Candidate Pass
FIGURE 1 — U-shaped curve: STATIC SUFFICIENT — the high-low-high accuracy curve is a canonical static plot; freezing it is the point.
FIGURE 2 — Recency from autoregression: VIDEO CANDIDATE — sequential next-token prediction with weight concentrating on recent neighbors is intrinsically temporal; animating the predicted cell stepping rightward as the heavy arrows track the newest neighbors would teach why the objective produces recency, though the static graded-arrow row carries it.
FIGURE 3 — Multi-needle collapse: STATIC SUFFICIENT — a three-bar quantitative drop is naturally static.
FIGURE 4 — Position as attack surface: STATIC SUFFICIENT — a baseline-vs-front-vs-end bar comparison is a frozen quantitative result.
FIGURE 5 — Recommended layout: VIDEO CANDIDATE — re-laying-out a prompt (moving the load-bearing tokens from the middle trough to the recency-favored bottom and watching the attention ticks shift) would dramatize the placement fix, though the static annotated container suffices.
Recommendation: Render all five as static figures; Figures 2 and 5 are the strongest optional-video candidates if an animated layer is produced.
