# CAJAL Figure Intelligence — Chapter 1 — The Stochastic Machine: Why Output Is Sampled, Not Retrieved

Source: chapters/01-the-stochastic-machine.md
Mode: /scan silent
Date: 2026-05-29

## Density Recommendation
4 figure candidates. Mixed density. The chapter is largely argumentative (sampling vs. retrieval, "random" vs. "learned") but pivots on two visualizable contrasts and one genuinely novel mechanism (reasoning latent in the distribution), which earn figures; the prose-only sections do not.

## Figure 1: Retrieval versus sampling — two mental models
Priority: Critical
Trigger: VG — the entire chapter is built on rejecting one structural model (lookup table) for another (draw from a distribution); the contrast is conceptual and not depictable from the prose
Figure type: Comparison panels
Concept statement: A database returns the stored row identically every time, whereas a language model draws a fresh sample from a distribution, so a temperature dial that changes how often a different answer appears is only explicable under the sampling model.
Reader prior knowledge: Reader has the five-coffee-shop-names reproduction in hand and the claim "this is not retrieval" but has not seen the two models set side by side.
Source anchor: Section: 1.2 Why retrieval is the wrong mental model

### Block 1 — Illustrae Paste Block
Create a blank, unannotated flat vector figure for single-column textbook width (89 mm) on a white background, with no generated text. Build two stacked panels of equal size. Top panel (retrieval model): an input arrow entering a stacked-rows table glyph, with a single arrow exiting to one identical output marker repeated three times below in a vertical column — three identical markers. Bottom panel (sampling model): an input arrow entering a bar-cluster distribution glyph, with a single arrow exiting to three *different* output markers in a vertical column, each a distinct height/shape. Use Sky Blue #56B4E9 for the database table glyph, Blue #0072B2 for the distribution glyph as the primary mechanism, light gray for the three identical retrieval outputs (uniform, inert), Bluish Green #009E73 for the three varied sampling outputs (live, divergent), Black #000000 for arrows and outlines at 1 pt. Keep the two panels clearly parallel in layout so the only difference the eye catches is "one repeated output" versus "three different outputs."

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89 mm textbook figure, 300 DPI, flat vector, white background, unannotated.
[C - Content] Two parallel panels: retrieval (table glyph to three identical outputs) and sampling (distribution glyph to three different outputs). Relationship to preserve: same input, identical outputs under retrieval vs. divergent outputs under sampling.
[O - Organization] Two stacked equal panels, parallel internal layout, single-headed input/output arrows.
[P - Presentation] Flat vector, 1 pt strokes, Okabe-Ito: Sky Blue #56B4E9 (table), Blue #0072B2 (distribution), light gray (identical outputs), Bluish Green #009E73 (varied outputs), Black #000000 (arrows). No text in image.
[E - Exclusions]
- the words "database" / "sampling" or any labels
- coffee-shop names or token strings
- temperature numbers
- a dial or slider (kept for a later figure)
- mismatched panel sizes

### Block 3 — Negative Prompt
panel labels, database text, sampling text, token strings, coffee-shop names, temperature numbers, dial widget, slider, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 2: Distribution shape sets reliability — peaked versus flat
Priority: Important
Trigger: VG — the chapter's central explanatory move is that a "reliable" answer and a "scattered" answer are the same machine sampling from differently-shaped distributions; this is a structural claim about shape, not a quantity
Figure type: Comparison panels
Concept statement: A well-attested query yields a sharply peaked distribution so repeated draws land on the same token, while an ambiguous query yields a flat distribution so repeated draws scatter — same machine, different shape.
Reader prior knowledge: Reader understands softmax shape from Ch. 0 and the §1.2 claim that reliability is a property of shape, not stored truth.
Source anchor: Section: 1.2 — "Reliability is a property of distribution shape, not of stored truth"

### Block 1 — Illustrae Paste Block
Create a blank, unannotated flat vector figure for single-column textbook width (89 mm) on a white background, with no generated text. Draw two equal bar-chart panels side by side, each with the same number of vertical bars (six) on a shared y-axis baseline at zero. Left panel: one dominant tall bar with the rest near zero (peaked). To its right, a small vertical stack of three near-identical output markers, showing draws collapsing to one answer. Right panel: six bars of nearly equal height (flat). To its right, a small vertical stack of three clearly different output markers, showing draws scattering. Use Blue #0072B2 for all distribution bars as the primary series, Bluish Green #009E73 for the stable/converged output markers beside the peaked panel, Orange #E69F00 for the scattered output markers beside the flat panel, light gray for panel frames and the zero baseline, Black #000000 for axes at 1 pt. Both panels identical frame size; bars start at zero.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89 mm textbook figure, 300 DPI, flat vector, white background, unannotated.
[C - Content] Two equal bar panels (peaked left, flat right), each with an adjacent vertical trio of output markers: convergent beside peaked, divergent beside flat. Relationship to preserve: peaked distribution to repeated identical draws; flat distribution to scattered draws.
[O - Organization] Two comparison panels, shared zero baseline, output-marker trios placed to the right of each panel.
[P - Presentation] Flat vector, 1 pt strokes, Okabe-Ito: Blue #0072B2 (bars), Bluish Green #009E73 (convergent outputs), Orange #E69F00 (scattered outputs), light gray (frames/baseline), Black #000000 (axes). No text in image.
[E - Exclusions]
- probability values or axis numbers
- token names / example queries
- panel headings
- bars not starting at zero
- red-green pairing for the two output trios

### Block 3 — Negative Prompt
probability values, axis numbers, token names, example queries, panel headings, floating bars, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 3: Two levers, one distribution — prompt change versus decoding change
Priority: Critical
Trigger: MC — §1.5's key finding is a process claim: a latent reasoning branch can be reached either by reshaping the distribution (prompt lever) or by reaching deeper into the unchanged distribution (decoding lever), both arriving at the same region
Figure type: Systems diagram
Concept statement: A latent reasoning trajectory sits below the peak of the output distribution and can be surfaced two substitutable ways — prompting lifts it to the top, or alternative-token decoding reaches down to it directly.
Reader prior knowledge: Reader has read the Wang & Zhou "CoT without prompting" result and the Kojima "think step by step" prompt result and the claim they are two levers on one object.
Source anchor: Section: 1.5 The reasoning is in the distribution, not the prompt

### Block 1 — Illustrae Paste Block
Create a blank, unannotated flat vector figure for single-column textbook width (89 mm) on a white background, with no generated text. At center, a single distribution glyph drawn as a vertical bar cluster: one tall top bar and, lower in the cluster, a distinct shorter bar marked as the latent target (a small highlighted region partway down the tail). Show two input paths converging on this single target. Path A enters from the left labeled by a reshape glyph (an arrow that bends the bar cluster so the latent bar rises toward the top) — the prompt lever. Path B enters from the right as a downward-reaching arrow that dips past the peak into the tail to touch the same latent bar directly — the decoding lever. Both paths terminate at the one highlighted latent bar. Use Blue #0072B2 for the distribution cluster as the shared object, Bluish Green #009E73 for the latent target bar as the goal both paths reach, Sky Blue #56B4E9 for the prompt-lever reshape path, Orange #E69F00 for the decoding-lever reach path, Black #000000 for outlines and arrows at 1 pt. Make it visually unmistakable that two different paths hit one shared target.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89 mm textbook figure, 300 DPI, flat vector, white background, unannotated.
[C - Content] One central distribution glyph with a highlighted latent bar below the peak; a left reshape path and a right reach-down path both terminating at that latent bar. Relationship to preserve: prompt lever and decoding lever are two routes to the same latent region of one distribution.
[O - Organization] Central shared object with two converging single-headed paths, one from each side.
[P - Presentation] Flat vector, 1 pt strokes, Okabe-Ito: Blue #0072B2 (distribution), Bluish Green #009E73 (latent target), Sky Blue #56B4E9 (prompt path), Orange #E69F00 (decoding path), Black #000000 (outlines/arrows). No text in image.
[E - Exclusions]
- lever or path labels
- prompt text or "think step by step"
- token strings, k-values, benchmark numbers
- dual-headed arrows
- a third path

### Block 3 — Negative Prompt
lever labels, path labels, prompt text, think step by step, token strings, k-values, benchmark numbers, third path, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 4: Validating a prompt by sampling the distribution
Priority: Supplementary
Trigger: MC — §1.6's engineering rule is a repeated-trial process: fix prompt and parameters, run N times, characterize the spread, and read the spread as the engineering object rather than any single run
Figure type: Process flowchart
Concept statement: A single output is one draw and proves nothing about typical behavior; characterizing a prompt requires running it many times and summarizing the distribution of outcomes (correct / varied / malformed).
Reader prior knowledge: Reader accepts output is sampled and has reached §1.6's "you cannot validate a prompt from one run."
Source anchor: Section: 1.6 What sampling forces on the engineer

### Block 1 — Illustrae Paste Block
Create a blank, unannotated flat vector figure for single-column textbook width (89 mm) on a white background, with no generated text. On the left, a single fixed-prompt block with one outgoing arrow that fans out into a vertical column of many small identical run-markers (showing N repeated runs of the same prompt). Each run-marker emits a small output token of varying type. On the right, these many outputs collapse into a single summary bar chart with three bars representing the categorized outcomes (e.g., correct, varied, malformed) on a zero baseline. Use Sky Blue #56B4E9 for the fixed-prompt block, light gray for the many repeated run-markers as neutral trials, Blue #0072B2 for the summary outcome bars as the engineering object, Bluish Green #009E73 for the single bar representing the desired/correct outcome, Black #000000 for arrows and outlines at 1 pt. Make the fan-out (one prompt, many runs) and the collapse (many runs, one summary) both legible.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89 mm textbook figure, 300 DPI, flat vector, white background, unannotated.
[C - Content] Fixed prompt fans out to N run-markers; run-markers collapse into a three-bar outcome summary on a zero baseline. Relationship to preserve: many samples are required to characterize a prompt; the summary distribution, not any single run, is the object.
[O - Organization] Left-to-right: prompt to fan-out to repeated runs to collapsed summary chart, single-headed arrows.
[P - Presentation] Flat vector, 1 pt strokes, Okabe-Ito: Sky Blue #56B4E9 (prompt), light gray (run-markers), Blue #0072B2 (summary bars), Bluish Green #009E73 (correct-outcome bar), Black #000000 (arrows/outlines). No text in image.
[E - Exclusions]
- count numbers or percentages
- category names under the summary bars
- prompt text
- bars not starting at zero
- loop-back arrows

### Block 3 — Negative Prompt
count numbers, percentages, category names, prompt text, floating bars, loop-back arrows, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video Candidate Pass
FIGURE 1 — retrieval vs sampling: STATIC SUFFICIENT — binary contrast — two parallel panels make the point in one glance; nothing evolves over time.
FIGURE 2 — shape sets reliability: VIDEO CANDIDATE — repeated-draw demonstration — animating repeated draws landing on one bar (peaked) vs. scattering (flat) dramatizes "reliability is shape," though the static side-by-side is a strong default.
FIGURE 3 — two levers one distribution: STATIC SUFFICIENT — structural convergence — the converging-paths idea is spatial, not temporal; a static diagram conveys it fully.
FIGURE 4 — validate by sampling: VIDEO CANDIDATE — accumulation process — watching outcomes accumulate into the summary chart over N runs literally enacts "one run is an anecdote, the distribution is the object"; static fan-out is an acceptable fallback.

Recommendation: ship all four as static figures; Figures 2 and 4 are the natural animation upgrades because both turn a static contrast into a watch-it-happen demonstration of sampling.
