# CAJAL Figure Intelligence — Chapter 13 — Beyond Prompting: The Fine-Tuning Stack

Source: chapters/13-beyond-prompting-the-fine-tuning-stack.md
Mode: /scan silent
Date: 2026-05-29

## Density Recommendation
5 figure candidates. Mixed density. The chapter is a decision chapter built on three structural spines — a three-gate escalation ladder, the LoRA low-rank decomposition, and the GRPO group-baseline mechanism — plus two quantitative passages (the LoRA parameter reduction and the corrected anchor numbers) that reward bar/forest treatment.

## Figure 1: The escalation ladder with three gates
Priority: Critical
Trigger: MC — a three-gate sequential decision process with branch outcomes at each rung is a ≥3-step interdependent procedure
Figure type: Process flowchart
Concept statement: Prompting, SFT/RAG, and RL form a cost-ordered ladder climbed only when the cheaper rung is provably insufficient, with a checkable gate (metric ceiling, knowledge volatility, verifiable reward) governing each escalation.
Reader prior knowledge: Holds the prompt-vs-fine-tune binary; needs to see the layers as ordered rungs with explicit pass/fail conditions rather than rivals.
Source anchor: Section: 13.3 The escalation ladder, with gates

### Block 1 — Illustrae Paste Block
Draw a vertical top-to-bottom flowchart on white representing escalating cost. At top a small entry rectangle for Step 0 (define eval set and target metric) in neutral gray. A single-headed arrow leads down to Gate 1, a decision block in primary blue #56B4E9; from Gate 1 a side branch arrow exits right to a SHIP terminal drawn as a rounded rectangle in active green #009E73, and a downward arrow continues to Gate 2. Gate 2 is a decision block in primary blue with two side outcome boxes in secondary orange #E69F00 (SFT and RAG); a downward arrow continues to Gate 3. Gate 3 is a decision block in primary blue with one side outcome box in blocking orange-red #D55E00 for the RL rung, the most expensive and irreversible. Position the three gate blocks at increasing depth and increasing horizontal indent to convey a rising cost axis. Keep to about seven components. Use 1pt strokes, flat vector, white, single-headed arrows only, no text in image, Okabe-Ito palette exclusively.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Confirmed components: Step-0 entry; Gate 1 with a SHIP side terminal; Gate 2 with SFT and RAG side terminals; Gate 3 with an RL side terminal. Relationship: sequential descent, each gate's failure passing control to the next deeper rung; cost rises with depth.
[O - Organization] Vertical spine of three gates with side-branch outcomes peeling off right; increasing indent down the page encodes rising cost.
[P - Presentation] Flat vector, Okabe-Ito only: Step-0 gray, three gate blocks #56B4E9, SHIP #009E73, SFT/RAG #E69F00, RL #D55E00. 1pt strokes, no text in image.
[E - Exclusions] No yes/no words, no question marks, no dollar signs, no ladder-rung pictogram, no human figure, no GPU or chip icons.

### Block 3 — Negative Prompt
yes/no words, question marks, dollar signs, literal ladder pictograms, GPU icons, chip icons, human figures, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 2: LoRA low-rank decomposition W = W0 + BA
Priority: Critical
Trigger: VG — the claim that a full-shape update factors into two thin matrices around a frozen base is a structural/dimensional relationship the equation states but a reader cannot picture
Figure type: Structural schematic
Concept statement: LoRA freezes the base weight matrix W0 and learns the update as a product BA of two thin matrices of rank r much smaller than the dimensions, so the trainable footprint shrinks from d×k to r(d+k).
Reader prior knowledge: Knows matrix shapes and rank; needs the relative-size relationship between the frozen square and the two thin factors made visually proportional.
Source anchor: Section: 13.4 The SFT rung, condensed: LoRA and QLoRA

### Block 1 — Illustrae Paste Block
Draw a matrix-shape schematic on white showing the additive update. On the left, a large square block representing the frozen base weight W0 (d by k), filled flat in neutral gray with a small lock-corner notch and no inner detail, sized large. To its right a plus sign drawn as two crossed 1pt strokes. To the right of the plus, two adjacent thin rectangles forming the product: a tall narrow rectangle B (d rows, r columns) drawn in active green #009E73, immediately abutting a short wide rectangle A (r rows, k columns) drawn in primary blue #0072B2, the two sharing the thin r dimension so their meeting edge is visibly the smallest dimension. Make B clearly tall-and-narrow and A clearly short-and-wide, both visibly far thinner than the large gray W0 square, so the eye reads r much smaller than d and k. Optionally show an equals sign and the resulting same-size square outline faintly to anchor the sum, but keep total components to six or fewer. Use 1pt strokes, flat vector, white, no text in image, Okabe-Ito palette exclusively.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Confirmed components: large frozen base square W0 (gray, lock notch); plus glyph; tall-narrow factor B; short-wide factor A sharing the small r edge; optional equals glyph. Relationship: W0 frozen, update = B times A, with r the shared small dimension dwarfed by d and k.
[O - Organization] Left-to-right: W0 + (B·A), with B and A abutting along their common r dimension; proportions encode r ≪ min(d,k).
[P - Presentation] Flat vector, Okabe-Ito only: W0 gray, B #009E73, A #0072B2, plus/equals glyphs black 1pt. No text in image.
[E - Exclusions] No matrix entry numbers, no dimension labels, no Greek letters, no alpha/r scaling annotation, no human figure, no grid of cells inside the matrices.

### Block 3 — Negative Prompt
matrix entry numbers, dimension labels, Greek letters, scaling annotations, inner cell grids, human figures, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 3: LoRA trainable-parameter reduction
Priority: Important
Trigger: PQ — the 16,777,216 → 65,536 drop (about 256×) for r=8, d=k=4096 is a quantitative claim best shown as proportional bars with y from zero
Figure type: Statistical/quantitative
Concept statement: For r=8 and d=k=4096, LoRA cuts trainable parameters from roughly 16.78 million (full-shape ΔW) to about 65.5 thousand (B plus A), a roughly 256-fold reduction.
Reader prior knowledge: Can read a bar chart; needs the magnitude of the reduction made viscerally proportional rather than left as two large numbers in prose.
Source anchor: Section: 13.4 — LoRA's mechanism (the math, visible)

### Block 1 — Illustrae Paste Block
Draw a simple two-bar vertical bar chart on white with the y-axis starting at zero and a linear scale. The left bar represents the full-shape update parameter count (about 16.78 million) drawn tall in secondary orange #E69F00. The right bar represents the LoRA parameter count (about 65.5 thousand) drawn in active green #009E73 — on a true linear zero-based axis this bar is a barely visible sliver beside the tall orange bar, which is the point: render it honestly as a near-flat line so the 256× gap is unmistakable. Draw a single thin gray y-axis line and a baseline; no gridlines, no tick numbers, no value labels inside or above the bars. Keep the two bars equal width with a clear gap between them. Total components: two bars plus axis. Use 1pt strokes, flat vector, white background, no text in image, Okabe-Ito palette exclusively.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Confirmed components: two vertical bars (full-shape ≈16.78M, LoRA ≈65.5K) on a zero-based linear y-axis. Relationship: proportional heights encode the ~256× reduction, LoRA bar a near-flat sliver.
[O - Organization] Two equal-width bars side by side with a gap; single gray y-axis at left; common baseline.
[P - Presentation] Flat vector, Okabe-Ito only: full-shape bar #E69F00, LoRA bar #009E73, axis gray. 1pt strokes, y from zero, no text, no tick numbers, no value labels.
[E - Exclusions] No value labels, no tick numbers, no gridlines, no log axis, no percentage signs, no human figure, no 3D bars, no broken/clipped axis.

### Block 3 — Negative Prompt
value labels, tick numbers, gridlines, log-scale axis, percentage signs, broken axis marks, 3D bars, human figures, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 4: GRPO group-relative baseline (critic removed)
Priority: Important
Trigger: VG — GRPO replacing PPO's learned critic with a group-standardized reward baseline is a structural mechanism contrast not depictable from the equation alone
Figure type: Comparison panels
Concept statement: GRPO drops PPO's separate critic network by sampling a group of outputs for one prompt and standardizing their rewards as the advantage baseline, so outputs above the group mean are reinforced and those below are suppressed.
Reader prior knowledge: Knows RL uses an advantage/baseline; needs to see that the baseline shifts from a learned critic network to a within-group statistic.
Source anchor: Section: 13.5 The RL rung, condensed: GRPO and verifiable reward

### Block 1 — Illustrae Paste Block
Draw two side-by-side panels on white separated by a thin gray vertical divider. Left panel (PPO): a single prompt node in gray at top, a single output node below it, and a separate critic-network block drawn in blocking orange-red #D55E00 connected by a single-headed arrow to the output, marking the extra cost component. Right panel (GRPO): one prompt node in gray at top fanning out via single-headed arrows to a group of, say, four output nodes drawn in primary blue #56B4E9; below them a single horizontal baseline rule in active green #009E73 representing the group mean, with two of the four outputs sitting above the line (reinforced) and two below (suppressed), shown purely by vertical position relative to the green line. No critic block appears in the right panel — its absence is the message. Keep total components within eight. Use 1pt strokes, flat vector, white, single-headed arrows only, no text in image, Okabe-Ito palette exclusively.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Confirmed components: left PPO panel (prompt, output, separate critic block); right GRPO panel (prompt, group of four outputs, group-mean baseline rule). Relationship: PPO needs a critic; GRPO substitutes a within-group standardized baseline, outputs above/below shown by position.
[O - Organization] Two panels split by a vertical divider; PPO left with critic highlighted, GRPO right with fan-out and a horizontal mean line.
[P - Presentation] Flat vector, Okabe-Ito only: prompts gray, PPO critic #D55E00, GRPO outputs #56B4E9, group-mean baseline #009E73. 1pt strokes, no text in image.
[E - Exclusions] No reward numbers, no Greek letters, no equation, no neural-net layer drawings, no human figure, no panel title text.

### Block 3 — Negative Prompt
reward numbers, Greek letters, equations, neural-network layer diagrams, panel titles, human figures, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 5: GEPA vs GRPO — per-benchmark accuracy deltas
Priority: Supplementary
Trigger: PQ — the four named per-benchmark gains (HotpotQA +19.0, HoVer +13.7, PUPA +5.2, IFBench +2.7) are numeric and best shown as a zero-based dot/bar array rather than a flat "6–19"
Figure type: Statistical/quantitative
Concept statement: GEPA's advantage over GRPO is not flat but varies sharply by benchmark — largest on HotpotQA, smallest on IFBench — averaging about 6 points and peaking near 19.
Reader prior knowledge: Can read a horizontal dot or bar chart; needs the spread across benchmarks made explicit to correct the misquoted "6–19" range.
Source anchor: Section: 13.6 Reading the anchor numbers precisely

### Block 1 — Illustrae Paste Block
Draw a horizontal dot plot (or thin horizontal bars) on white with four rows, one per benchmark, ordered top to bottom by descending delta: HotpotQA (+19.0), HoVer (+13.7), PUPA (+5.2), IFBench (+2.7). Use a single shared horizontal x-axis starting at zero on the left, linear scale, drawn as a thin gray line with a baseline at zero. Plot each delta as a filled dot at the end of a thin gray connector stem from the zero line, all four dots in active green #009E73 since each is a positive gain for GEPA. Add one thin vertical reference line in secondary orange #E69F00 at the average (~6 points) spanning the rows, to anchor the mean against the spread. Keep rows evenly spaced, dots equal size. No tick numbers, no value labels, no benchmark text. Total components: axis, four stems-with-dots, one mean reference line. Use 1pt strokes, flat vector, white, Okabe-Ito palette exclusively.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Confirmed components: four-row horizontal dot plot of per-benchmark deltas (19.0, 13.7, 5.2, 2.7) ordered descending; a vertical mean reference line near 6. Relationship: positions on a shared zero-based x-axis encode the spread; mean line contrasts with the peak.
[O - Organization] Four evenly spaced rows, descending by value; shared gray x-axis from zero; orange vertical mean line crossing all rows.
[P - Presentation] Flat vector, Okabe-Ito only: dots and stems #009E73, mean line #E69F00, axis gray. 1pt strokes, x from zero, no tick numbers, no value or benchmark labels.
[E - Exclusions] No value labels, no benchmark names, no tick numbers, no gridlines, no log axis, no human figure, no legend, no 3D effect.

### Block 3 — Negative Prompt
value labels, benchmark names, tick numbers, gridlines, log axis, legend keys, human figures, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video Candidate Pass
FIGURE 1 — the escalation ladder: STATIC SUFFICIENT — fixed decision structure — the gate logic and cost ordering resolve in one static flowchart; no temporal change.
FIGURE 2 — LoRA decomposition: STATIC SUFFICIENT — structural relationship — the W0 + BA shape relationship is fully legible in one frame.
FIGURE 3 — LoRA parameter reduction: STATIC SUFFICIENT — two-value comparison — a single zero-based bar pair carries the magnitude.
FIGURE 4 — GRPO group baseline: VIDEO CANDIDATE — sampling-and-scoring dynamics — the per-group sampling, scoring, and above/below-mean reinforcement is a sequence that a short animation (sample group → score → standardize → reinforce/suppress) would clarify, though a static comparison panel suffices for the core contrast.
FIGURE 5 — GEPA vs GRPO deltas: STATIC SUFFICIENT — fixed quantities — four benchmark deltas have no temporal dimension.

Recommendation: ship all five as static figures; Figure 4 is the only plausible motion candidate and only if the digital edition supports it — the static comparison panel already carries the load-bearing critic-removed contrast, so promotion is optional.
