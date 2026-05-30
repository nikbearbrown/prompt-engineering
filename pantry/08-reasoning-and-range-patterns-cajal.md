# CAJAL Figure Intelligence — Chapter 8 — Reasoning and Range Patterns

Source: chapters/08-reasoning-and-range-patterns.md
Mode: /scan silent
Date: 2026-05-29

## Density Recommendation
5 figure candidates. Mixed density. The chapter's organizing axis (tighten vs. widen the distribution) is conceptual, the three-route CoT contrast and self-consistency are mechanistic processes, and two quantitative claims (the zero-shot CoT jumps, the tier decision table) reward a bar chart and a structured decision figure.

## Figure 1: Tighten the path vs. widen the sample
Priority: Critical
Trigger: VG — the chapter's central organizing claim that reasoning and range patterns are opposite operations on one output distribution is a structural framing not depictable from text
Concept statement: Reasoning patterns reshape the distribution so the single most-probable path is better (tighten), while range patterns stop accepting the mode and pull more of the distribution into view (widen) — opposite moves on the same sampling machine.
Figure type: Comparison panels
Reader prior knowledge: Output as a sample from a conditional distribution; greedy vs. sampled decoding; mode (Ch. 1).
Source anchor: Section: 8.2 Two opposite moves on one machine

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector comparison figure on a white background with two equal panels separated by a thin vertical divider, each showing a probability distribution as a smooth unimodal hump rising from a shared zero baseline. The left panel (tighten the path) shows the distribution becoming narrower and taller, concentrated around its single peak, with one bold single-headed downward arrow marking the single chosen path at the peak; render the concentrated peak and its path arrow in active green #009E73. The right panel (widen the sample) shows a broader distribution with several distinct sample points marked across its spread, each by a short upward tick, and several thin single-headed arrows fanning out to indicate multiple paths drawn; render the spread sample markers in secondary orange #E69F00. Both panels share an identical horizontal baseline and axis extent so the narrowing-versus-widening contrast is direct. Keep components minimal: one curve and one path on the left, one curve and several sample ticks on the right. Use only Okabe-Ito colors: #009E73 tighten, #E69F00 widen, neutral gray baseline curve outline, #000000 axis. No numbers, no text, no labels anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Two distributions on a shared baseline: (left) narrowed, single-peak, one selected path (tighten); (right) broadened, multiple sampled points with fanned path arrows (widen).
[O - Organization] Two equal panels, thin vertical divider, identical baseline and x-extent; single bold path arrow left, several thin sample arrows right.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — #009E73 tighten elements, #E69F00 widen elements, gray curve outline, #000000 axis; no fill gradients.
[E - Exclusions] No numeric axis values, percentages, or text; no third panel; no histogram bars (use smooth curves); no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
numeric axis values, percentage labels, third panel, histogram bars, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 2: Three routes to the same step-shaped trajectory
Priority: Critical
Trigger: MC — three distinct routes (direct/greedy, zero-shot CoT prompt, CoT-decoding via top-k inspection) reaching the same correct trajectory, a multi-path process whose point is that the reasoning lives in the distribution not the prompt string
Concept statement: The same model reaches the same correct step-shaped trajectory by three different routes — direct greedy decode (misses it), a "step by step" prompt cue, or top-k first-token inspection with no prompt change — proving the reasoning was latent in the distribution.
Figure type: Process flowchart
Reader prior knowledge: Greedy vs. top-k decoding; CoT as trajectory shaping (§8.1, §8.3).
Source anchor: Section: 8.3 Chain-of-thought: emergent, conditional, and not about valid logic (worked contrast)

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector process figure on a white background showing a single shared model/query node at the left, from which three horizontal routes branch rightward to outcomes. Route (a), the direct greedy decode, is a straight single-headed arrow to a wrong-outcome node rendered in blocking-orange #D55E00. Route (b), the zero-shot CoT prompt cue, passes through a small intermediate node representing an appended prompt phrase, then a single-headed arrow to a correct-outcome node in active green #009E73. Route (c), CoT-decoding, passes through a small intermediate node representing top-k first-token inspection (drawn as a tiny fan of three branch ticks), then a single-headed arrow to the same correct-outcome node in #009E73. The two correct-outcome nodes should align vertically or visibly converge to read as the same destination. Total components: one source, two intermediate route nodes, one wrong outcome, the shared correct outcome — six maximum. 1pt single-headed arrows, no crossings. Okabe-Ito only: #D55E00 wrong outcome, #009E73 correct outcome, primary blue #56B4E9 intermediate route nodes, #000000 strokes. No text, no labels, no words anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] One source node; three routes — direct greedy (to wrong outcome), prompt-cue CoT (through a prompt-phrase node to correct outcome), CoT-decoding (through a top-k inspection fan node to the same correct outcome).
[O - Organization] Left source, three left-to-right routes, convergence of routes (b) and (c) on a shared correct-outcome node; the wrong outcome set apart.
[P - Presentation] Flat vector, 1pt single-headed arrows; Okabe-Ito only — #D55E00 wrong outcome, #009E73 correct outcome, #56B4E9 intermediate route nodes, #000000 strokes.
[E - Exclusions] No text, route labels, "step by step" words, or captions; no more than three routes; no icons; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
route label text, step-by-step words, prompt text snippets, more than three routes, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 3: Zero-shot CoT accuracy jumps
Priority: Important
Trigger: PQ — concrete benchmark numbers (MultiArith 17.7%→78.7%, GSM8K 10.4%→40.7%) on text-davinci-002 from adding the trigger phrase
Concept statement: Adding the zero-shot "let's think step by step" trigger to the same model produces large accuracy gains on multi-step arithmetic benchmarks.
Figure type: Statistical/quantitative
Reader prior knowledge: Benchmark accuracy as a percentage; zero-shot CoT (Kojima et al. 2022).
Source anchor: Section: 8.1 The reasoning trace that wasn't reasoning

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector grouped bar chart on a white background with the y-axis starting at zero and running to one hundred (representing accuracy percent). Show two benchmark groups along the x-axis. Each group contains a pair of adjacent bars: a "direct answer" bar and a "with trigger phrase" bar. The direct-answer bars are short and rendered in neutral gray; the with-trigger bars are taller and rendered in active green #009E73 to mark the improved condition. In the first group the gray bar is very short and the green bar reaches roughly four-fifths height; in the second group the gray bar is very short and the green bar reaches roughly two-fifths height. All four bars rise from a common zero baseline with consistent width and spacing. Draw a plain y-axis line and a baseline; do not add tick numbers. Total: four bars in two groups. Use only Okabe-Ito colors: neutral gray for the baseline condition, #009E73 for the improved condition, #000000 axis. No numbers, no text, no labels anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Grouped bar chart, two benchmark groups, each a pair of bars (direct vs. trigger-phrase), y from zero to one hundred; trigger bars markedly taller.
[O - Organization] Two groups along x; within-group bar pairs adjacent; common zero baseline; consistent bar width and group spacing.
[P - Presentation] Flat vector, 1pt strokes, bars from zero; Okabe-Ito only — neutral gray baseline-condition bars, #009E73 trigger-condition bars, #000000 axis.
[E - Exclusions] No numeric value labels, axis tick numbers, percentages, legends, or text; no 3D bars; no gridline clutter; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
value labels on bars, axis tick numbers, percentage text, legend text, benchmark name labels, 3D bars, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 4: Self-consistency as sample-and-vote
Priority: Important
Trigger: MC — a multi-step sampling procedure (draw N CoT trajectories at non-zero temperature, then majority-vote) that the chapter frames as the Ch. 1 sampling machine made visible
Concept statement: Self-consistency draws many independent CoT trajectories from the distribution and takes the majority-vote answer, a Monte-Carlo aggregation that is more reliable than any single decode.
Figure type: Systems diagram
Reader prior knowledge: Sampling under temperature; CoT trajectories; variance reduction by averaging (Ch. 1).
Source anchor: Section: 8.4 Self-consistency: range as a sampling procedure

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector systems diagram on a white background reading left to right. Start with a single source node (the prompt/model). From it, draw several single-headed arrows fanning out to a vertical column of parallel trajectory nodes (four or five short chain glyphs, each a small stack of two or three rungs) representing independently sampled CoT paths; render these trajectory nodes in secondary orange #E69F00 to mark the widened sampling. Each trajectory node emits a single-headed arrow into a single aggregation node on the right (the majority vote), rendered in active green #009E73 as the consensus output. One of the trajectory paths should visibly disagree (its small terminal mark set apart) to show that the vote overrides a stray wrong path; mark that dissenting terminal in neutral gray, not green. Total components: one source, four-to-five trajectory nodes, one aggregation node — kept near eight. 1pt single-headed arrows, clean fan-in. Okabe-Ito only: #E69F00 trajectories, #009E73 aggregation, gray dissenting terminal, #000000 strokes. No numbers, no text, no labels anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] One source fanning to several parallel sampled CoT trajectory nodes, all feeding one majority-vote aggregation node; one trajectory shown disagreeing to motivate the vote.
[O - Organization] Left source, middle parallel column of trajectories, right aggregation node; fan-out then fan-in with single-headed arrows.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — #E69F00 trajectory nodes, #009E73 aggregation node, neutral gray dissenting terminal, #000000 strokes.
[E - Exclusions] No text, vote counts, numbers, or captions; no more than five trajectories; no dice/coin icons; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
vote count numbers, dice icons, coin icons, probability numbers, more than five trajectories, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 5: Reasoning elicitation by model tier
Priority: Important
Trigger: VG — a four-tier mapping from model tier to recommended elicitation action (the chapter's own decision table), where the reasoning-tuned tier flips from "add CoT" to "add nothing," a structural relationship
Concept statement: Whether to elicit reasoning depends on model tier — large base models gain from CoT, mid-tier instruction-tuned models gain modestly, reasoning-tuned models should get nothing added, and any tier you control can use CoT-decoding instead.
Figure type: Hierarchy/taxonomy
Reader prior knowledge: The CoT findings by tier (Wei, Kojima, Meincke, Wang & Zhou).
Source anchor: Section: 8.3 The honest summary, as a decision rule by tier (table)

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector figure on a white background structured as four stacked horizontal tier rows arranged top to bottom by capability, like a graded ladder. Each row has a left zone (the model tier marker, a simple sized block that grows larger from top to bottom to suggest increasing capability) and a right zone (the recommended action marker). Row 1 (large base) right zone is active green #009E73 to signal "elicit CoT helps." Row 2 (mid-tier non-reasoning) right zone is a lighter active-green-to-neutral, drawn as a smaller green block, signaling "modest help." Row 3 (reasoning-tuned) right zone is blocking-orange #D55E00 to signal "add nothing — redundant and harmful." Row 4 (any tier, decoding-controlled) right zone is primary blue #56B4E9 to signal the alternative route (CoT-decoding). Keep each row to two marks; four rows total, eight marks. Separate rows with thin horizontal rules. Use only Okabe-Ito colors as specified with #000000 strokes. No numbers, no text, no labels anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Four tier rows, each with a tier-capability block (growing in size down the ladder) and a recommended-action marker color-coded by recommendation.
[O - Organization] Four stacked rows separated by thin rules; left tier marker, right action marker; capability increases downward.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — #009E73 "helps", smaller green "modest", #D55E00 "add nothing", #56B4E9 "decoding alternative", #000000 strokes and rules.
[E - Exclusions] No text, tier names, action words, or captions; no model-vendor logos; no icons; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
tier name text, action word labels, model vendor logos, icons, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video Candidate Pass
FIGURE 1 — Tighten vs. widen: STATIC SUFFICIENT — the opposing operations are best grasped as a single frozen contrast on a shared baseline.
FIGURE 2 — Three routes to the trajectory: VIDEO CANDIDATE — three parallel processes converging on one destination, with one diverging to a wrong answer — an animated traversal of each route in turn would make "the reasoning was never in the words" land, though the static convergence diagram carries it.
FIGURE 3 — CoT accuracy jumps: STATIC SUFFICIENT — quantitative comparison — a bar chart is the natural static form.
FIGURE 4 — Self-consistency: VIDEO CANDIDATE — sample-many-then-vote is intrinsically sequential (fan-out sampling, then fan-in aggregation overriding a dissenter); animating the draws accumulating into a vote would teach variance-reduction, though the static fan diagram suffices.
FIGURE 5 — Tier decision table: STATIC SUFFICIENT — a tier-to-action mapping is a reference taxonomy, atemporal.
Recommendation: Render all five as static figures; Figures 2 and 4 are the strongest optional-video candidates if an animated layer is produced.
