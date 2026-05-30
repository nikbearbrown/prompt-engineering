# CAJAL Figure Intelligence — Chapter 9 — Prompt Brittleness and the Discipline of Evaluation

Source: chapters/09-prompt-brittleness-and-evaluation.md
Mode: /scan silent
Date: 2026-05-29

## Density Recommendation
4 figure candidates. Mixed density. The chapter pairs a hard quantitative spine (the 76-point format spread, the leaderboard-reordering result) with two structural claims (the conditioning-on-surface-form mechanism, the report-a-distribution procedure) — so two PQ bar/histogram figures, one mechanism schematic, and one process flowchart carry the load.

## Figure 1: Format-variant accuracy spread
Priority: Critical
Trigger: PQ — the anchor number (up to 76 accuracy points of spread on one task from formatting alone, Sclar et al. 2024) plus the §9.1 composite's two-model overlapping distributions
Figure type: Statistical/quantitative
Concept statement: A single prompt's score is the top of a wide distribution, not a capability — across semantically-equivalent format variants accuracy spans tens of points, and the spreads of two models overlap so heavily that the better-at-median model can lose at one chosen format.
Reader prior knowledge: Accuracy as a percentage; format variant as a semantically-neutral re-rendering of one prompt (§9.2); distribution vs. point estimate.
Source anchor: Section: 9.1 The eval that overstated the model

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector figure on a white background showing two horizontal distribution strips stacked vertically against a shared horizontal accuracy axis running left to right from a common origin. The top strip (Model A) is a wide cluster of short vertical tick marks spread across a long horizontal extent, with one tick at the far right end drawn taller and bolder to mark the single reported "top" score; render Model A's ticks in primary blue #56B4E9 and the lone reported-top tick in blocking orange #D55E00. The bottom strip (Model B) is a narrower cluster of ticks sitting further right on average but shorter in total extent; render Model B's ticks in secondary orange #E69F00. Draw a thin vertical median line through each strip's center of mass so the reader sees Model B's median sits right of Model A's median even though A's single top tick sits rightmost. The two strips share one horizontal axis baseline. Total components: two tick clusters, two median lines, one highlighted top tick, one axis — kept under eight. Use only Okabe-Ito colors: #56B4E9 Model A spread, #E69F00 Model B spread, #D55E00 the misleading reported top, neutral gray median lines, #000000 axis. No numbers, no text, no labels anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Two horizontal accuracy distributions (Model A wide, Model B narrower and further right at median) on a shared axis; one bold tick marks the single "top" score reported for Model A; per-strip median lines show the median ordering reverses the top-score ordering.
[O - Organization] Two stacked strips sharing one left-origin horizontal axis; median line through each; the lone reported-top tick highlighted at the right of strip A.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — #56B4E9 Model A ticks, #E69F00 Model B ticks, #D55E00 reported-top tick, neutral gray median lines, #000000 axis.
[E - Exclusions] No numeric axis values, percentages, or model names; no smooth bell curves (use tick clusters); no legend; no third model; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
numeric axis values, percentage labels, model name labels, smooth bell curves, legend text, third distribution, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 2: The model conditions on surface form
Priority: Critical
Trigger: VG — the load-bearing mechanism claim (a semantically-neutral edit is a different point in the token-conditioning space and can land on the other side of a decision boundary) is a structural relationship not depictable from prose
Figure type: Mechanism cross-section
Concept statement: Two prompts a human reads as identical are two different token sequences in the model's conditioning space, and a neutral edit can move that point across a decision boundary into a different discrete output.
Reader prior knowledge: Output as a sample conditioned on the full token sequence (Ch. 1); a decision boundary separating discrete outputs.
Source anchor: Section: 9.2 The mechanism: the model conditions on surface form

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector figure on a white background showing a two-dimensional conditioning space as a plain rectangle bisected by one slightly diagonal boundary line into two regions (the two discrete outputs). Place two point markers near the boundary on opposite sides: a left point inside region one and a right point just across into region two, connected by one short single-headed arrow indicating the neutral edit nudging the conditioning point from one side to the other. The two source points should each carry a tiny upstream stub — a short horizontal segment with a small notch difference (a colon vs a dash glyph rendered abstractly as two differing tick shapes, no letters) — feeding into each point to show the only change is surface form. Render the boundary line bold in #000000; render region one fill-free with its point in primary blue #56B4E9; render region two with its point in secondary orange #E69F00; render the crossing edit arrow in blocking orange #D55E00 to mark that a neutral edit flipped the output. Total components: one boundary, two regions, two points, two upstream stubs, one crossing arrow — kept near eight. Use only Okabe-Ito colors as specified with #000000 strokes. No numbers, no text, no letters anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] A conditioning space split by one decision boundary into two output regions; two near-boundary points on opposite sides; each fed by a tiny differing surface-form stub; a single-headed arrow showing the neutral edit moving the point across the boundary.
[O - Organization] Rectangle bisected by a diagonal boundary; two points straddling it; upstream stubs at left; crossing arrow between the two points.
[P - Presentation] Flat vector, 1pt strokes, bold boundary; Okabe-Ito only — #56B4E9 region-one point, #E69F00 region-two point, #D55E00 crossing edit arrow, #000000 boundary and stubs.
[E - Exclusions] No axis numbers, no probability values, no actual punctuation letters or text glyphs, no captions; no more than two points; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
axis numbers, probability values, punctuation letters, colon glyph, dash glyph, text glyphs, captions, additional points, text labels, words, gibberish letters, titles, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 3: Format reorders the leaderboard
Priority: Important
Trigger: PQ — the comparison-corruption result (Alzahrani et al. 2024: non-semantic perturbations shift leaderboard rankings by up to 8 positions) shown as two reordered rank columns
Figure type: Comparison panels
Concept statement: A non-semantic perturbation to the prompt format reorders which model "wins" — model rankings under one format do not survive a switch to another, so a shared fixed format does not give a fair comparison.
Reader prior knowledge: A leaderboard as an ordered ranking of models; non-semantic perturbation (reorder choices, change choice symbol) (§9.3).
Source anchor: Section: 9.3 The corruption: format reorders the leaderboard

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector comparison figure on a white background with two vertical columns of equal-size stacked rank slots side by side, separated by a gap. The left column (format one) holds five small uniform model blocks stacked top to bottom in one order; the right column (format two) holds the same five blocks in a visibly different order. Give each of the five blocks a consistent distinguishing fill so the same block can be tracked between columns: use #56B4E9, #E69F00, #009E73, #0072B2, and #CC79A7 — one hue per model, identical across both columns. Draw thin single-headed connector arrows from each block in the left column to its new position in the right column, so the crossing arrows make the reordering visible; render the connectors in neutral gray. The top slot of each column (rank one) may carry a small bracket mark to flag "the winner" position, showing a different colored block occupies it in each column. Total components: two five-slot columns, five tracked connector arrows — kept near eight visual groups. Use only Okabe-Ito colors as specified with #000000 column outlines and gray connectors. No numbers, no text, no labels anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Two ranked columns of the same five color-coded model blocks in different orders; gray connector arrows tracking each block across the reorder; a winner-slot bracket showing a different block wins under each format.
[O - Organization] Two side-by-side vertical five-slot stacks; per-block single-headed connectors from left order to right order; top slot marked.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — model blocks #56B4E9 / #E69F00 / #009E73 / #0072B2 / #CC79A7, neutral gray connectors, #000000 column outlines.
[E - Exclusions] No numeric ranks, model names, accuracy values, or captions; no more than five models; no leaderboard table gridlines with numbers; no color beyond named hexes; no red-green adjacency (keep green and orange non-adjacent).

### Block 3 — Negative Prompt
numeric ranks, model name labels, accuracy values, captions, table gridlines, more than five models, text labels, words, gibberish letters, titles, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 4: Report a distribution, not a point
Priority: Important
Trigger: MC — the five-step Create-level procedure (enumerate variants → run on one held-out set → plot the histogram → pick the metric → gate edits) is an interdependent process the chapter names as its produced artifact
Figure type: Process flowchart
Concept statement: The eval discipline is a pipeline: generate semantically-equivalent variants, run all of them on the same held-out set, plot the accuracy histogram, choose the metric to the use case, and only then optimize behind a regression gate.
Reader prior knowledge: Held-out set; variant sweep; histogram with median and interval; max-vs-average metric choice (§9.4).
Source anchor: Section: 9.4 The discipline: report a distribution, not a point

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector process flowchart on a white background reading left to right in five stages connected by single-headed arrows. Stage one: a single prompt node fanning out via three short single-headed arrows into a small column of variant nodes (the enumerated semantically-equivalent forms); render the variant fan in secondary orange #E69F00. Stage two: the variant nodes converging via arrows onto one shared held-out-set node (a single plain block); render it neutral gray. Stage three: an arrow into a small histogram glyph — four or five short vertical bars of varying height rising from a common baseline with one thin vertical median line through them; render the bars primary blue #56B4E9 and the median line #000000. Stage four: an arrow into a metric-selection node drawn as a small two-way branch (one branch up, one branch down) marking the max-vs-average choice; render in primary blue #0072B2. Stage five: an arrow into a final gate node drawn as a narrow vertical bar (a regression gate); render it active green #009E73 to mark "ship only if it passes." Keep to these six node groups, single-headed arrows, no crossings. Use only Okabe-Ito colors as specified with #000000 strokes. No numbers, no text, no labels anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Five-stage pipeline: prompt → fanned variant nodes → shared held-out-set node → accuracy histogram with a median line → max-vs-average metric branch → regression gate.
[O - Organization] Strict left-to-right flow, single-headed arrows; fan-out at the variant stage, fan-in at the held-out stage; the histogram and gate as the visual anchors.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — #E69F00 variant fan, gray held-out node, #56B4E9 histogram bars, #0072B2 metric branch, #009E73 gate, #000000 strokes and median line.
[E - Exclusions] No numeric axis values on the histogram, no metric words, no stage labels or captions; no more than five stages; no icons beyond the schematic glyphs; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
histogram axis numbers, metric words, stage label text, captions, more than five stages, percentage values, text labels, words, gibberish letters, titles, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video Candidate Pass
FIGURE 1 — Format-variant spread: STATIC SUFFICIENT — two overlapping distributions with a highlighted top tick is a frozen quantitative contrast; a bar/strip plot is the natural static form.
FIGURE 2 — Conditioning on surface form: VIDEO CANDIDATE — a neutral edit nudging a point across a decision boundary to flip the output is an intrinsically temporal cause-and-effect; animating the point crossing as the edit is applied would make "neutral to a human, decisive to the sampler" land, though the static straddle diagram carries it.
FIGURE 3 — Leaderboard reorder: VIDEO CANDIDATE — the same five blocks resorting between two formats is a transformation; an animated reshuffle with the winner slot changing hands would dramatize comparison-corruption, though the static crossing-arrows version suffices.
FIGURE 4 — Report a distribution: STATIC SUFFICIENT — a reference pipeline of stages is atemporal and best read as one flowchart.
Recommendation: Render all four as static figures; Figures 2 and 3 are the strongest optional-video candidates if an animated layer is produced.
