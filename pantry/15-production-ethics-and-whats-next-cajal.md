# CAJAL Figure Intelligence — Chapter 15 — Production, Ethics, and What Comes Next

Source: chapters/15-production-ethics-and-whats-next.md
Mode: /scan silent
Date: 2026-05-29

## Density Recommendation
4 figure candidates. Mixed density. The chapter is partly synthesis (verbal) and partly mechanism: the version→evaluate→monitor production pipeline is a process, the grounded-vs-ungrounded self-correction decision rule is a branching predicate, self-consistency carries a quantitative gain set, and the closing compounding-failures argument is a structural map of one mechanism surfacing across chapters.

## Figure 1: Notebook prompt to monitored pipeline
Priority: Critical
Trigger: MC — the production lifecycle is a ≥3-stage pipeline (version → evaluate-in-CI → monitor) with a feedback gate, an interdependent process whose components each exist to catch a specific brittleness perturbation
Figure type: Process flowchart
Concept statement: Turning a notebook prompt into a production system requires pinning the prompt-model-parameters triple, gating deploys behind a held-out eval harness in CI, and monitoring live drift that feeds re-validation.
Reader prior knowledge: Brittleness under paraphrase/format/model-snapshot change (Ch. 9); decoding parameters shifting the distribution (Ch. 1).
Source anchor: Section: 15.2 From notebook to monitored pipeline

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector pipeline figure on a white background flowing left to right. At the far left, draw a small source node (the notebook prompt) as a rounded rectangle with a folded corner in neutral gray. An arrow leads right to a versioning node drawn as a rounded rectangle bundling three small stacked sub-tiles (representing the prompt-text, model-snapshot, and decoding-parameters triple) in primary blue #0072B2. An arrow leads right to an evaluation-gate node drawn as a vertical gate or filter shape in secondary orange #E69F00, positioned as a checkpoint the flow must pass. An arrow leads right to a deployed node in active green #009E73. Above the deployed node, draw a monitoring node as a small separate rounded rectangle in #56B4E9 sampling the deployed output via a thin single-headed arrow, with one return single-headed arrow looping back leftward to the evaluation gate to indicate re-validation on drift. Total components: source, versioning triple node, eval gate, deployed node, monitor node — five maximum. Okabe-Ito only: neutral gray source, #0072B2 versioning, #E69F00 eval gate, #009E73 deployed, #56B4E9 monitor, #000000 arrows. No numbers, no text, no labels anywhere. Flat vector, 1pt single-headed arrows, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Left-to-right pipeline: notebook source → versioning node (three stacked sub-tiles for the prompt/model-snapshot/parameters triple) → eval-gate checkpoint → deployed node, with a monitor node sampling the deployed output and a feedback arrow returning to the eval gate.
[O - Organization] Single horizontal flow with the gate as a mandatory checkpoint; monitor node above the deployed node; one feedback loop arrow from monitor back to the eval gate.
[P - Presentation] Flat vector, 1pt single-headed arrows; Okabe-Ito only — neutral gray source, #0072B2 versioning, #E69F00 eval gate, #009E73 deployed, #56B4E9 monitor, #000000 arrows; no gradients.
[E - Exclusions] No text, no "version/eval/monitor" words, no CI-tool logos, no numeric metrics, no second pipeline, no color beyond named hexes, no red-green pairing.

### Block 3 — Negative Prompt
stage labels, version/eval/monitor words, CI logos, numeric metrics, percentages, second pipeline, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 2: The grounded-vs-ungrounded self-correction decision tree
Priority: Critical
Trigger: MC — a branching predicate (external verifiable signal? single answer? open-ended?) routing to four distinct techniques, an interdependent decision procedure that is the section's portable lesson
Figure type: Process flowchart
Concept statement: Whether self-correction helps is decided by external grounding: a verifiable signal routes to grounded self-correction, a single-answer-no-signal task routes to self-consistency, an open-ended task to intrinsic refinement, and ungrounded self-critique on reasoning is avoided.
Reader prior knowledge: ReAct's external observation channel (Ch. 11); sycophancy as approval-maximization driving over-revision (Ch. 4).
Source anchor: Section: 15.4 The self-critique debate: when does checking help?

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector decision-tree figure on a white background flowing top to bottom. At the top draw a first diamond decision node (is there an external verifiable signal) in primary blue #0072B2. Its right branch (yes) leads down to a terminal rounded-rectangle node for grounded self-correction, rendered in active green #009E73. Its left branch (no) leads to a second diamond decision node (single verifiable answer) in #0072B2. From the second diamond, the right branch (yes — single answer) leads to a terminal node for self-consistency majority-vote, also in active green #009E73 since it helps without self-judging. The left branch (no — open-ended) leads to a terminal node for intrinsic refinement in secondary orange #E69F00 to mark it as conditional/unresolved. Separately, draw one short crossed-out or barred path from the second diamond's single-answer side toward a small terminal in blocking orange #D55E00 representing ask-the-model-to-grade-itself, marked as the avoided route by a single barrier slash. Total components: two diamonds, three positive terminals, one barred avoided terminal — six maximum, single-headed arrows, no crossings. Okabe-Ito only: #0072B2 diamonds, #009E73 grounded and self-consistency terminals, #E69F00 intrinsic-refine terminal, #D55E00 avoided terminal, #000000 arrows and barrier slash. No text, no yes/no labels, no words anywhere. Flat vector, 1pt single-headed arrows, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Two-level decision tree: first diamond (external verifiable signal?) → grounded-correction terminal on yes; second diamond (single verifiable answer?) on no → self-consistency terminal on yes and intrinsic-refine terminal on open-ended; a barred avoided terminal for ungrounded self-grading.
[O - Organization] Top-to-bottom; first diamond top, second diamond second level, terminals on a lower row; the avoided route marked by a single barrier slash rather than text.
[P - Presentation] Flat vector, 1pt single-headed arrows; Okabe-Ito only — #0072B2 diamonds, #009E73 the two helpful terminals, #E69F00 conditional terminal, #D55E00 avoided terminal, #000000 arrows and slash.
[E - Exclusions] No text, no yes/no/technique-name labels, no "Reflexion/Self-Refine/self-consistency" words, no fifth terminal, no color beyond named hexes, no red-green pairing, no crossing arrows.

### Block 3 — Negative Prompt
yes/no labels, technique names, Reflexion text, Self-Refine text, self-consistency text, branch words, fifth terminal, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, crossing arrows, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 3: Self-consistency gains over single-shot CoT
Priority: Important
Trigger: PQ — three benchmark improvement figures (GSM8K +17.9%, SVAMP +11.0%, AQuA +12.2%) are explicit quantities that compose into a clean grouped bar comparison
Figure type: Statistical/quantitative
Concept statement: Majority-vote self-consistency over diverse sampled reasoning paths raises accuracy over single-shot chain-of-thought across three reasoning benchmarks without asking the model to judge itself.
Reader prior knowledge: Chain-of-thought as a single sampled path; the mode of an answer distribution (Ch. 1, §15.4).
Source anchor: Section: 15.4 (self-consistency decision branch)

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector grouped bar chart on a white background with a single vertical y-axis drawn as a plain line rising from zero. Along the horizontal baseline place three groups, one per benchmark, evenly spaced. Each group contains two adjacent bars of equal width: a left baseline bar (single-shot chain-of-thought) in neutral gray, and a right bar (self-consistency majority vote) in primary blue #0072B2, drawn taller than its gray partner to show the gain. Make the three blue bars differ slightly in their height-above-gray so the relative magnitudes of the three improvements read correctly, with the first group's gain the largest, the other two roughly similar and smaller. All bars share the common zero baseline. Total components: one y-axis baseline plus three pairs of bars — six bars maximum. Use only Okabe-Ito colors: neutral gray baseline bars, #0072B2 self-consistency bars, #000000 axis. No numbers, no percentages, no benchmark names, no text or labels anywhere. Flat vector, 1pt strokes, no shadows, no gradients, white background, y-axis from zero.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated, y-axis from zero.
[C - Content] Three benchmark groups, each a pair of bars: gray single-shot CoT baseline and taller blue self-consistency bar; first group shows the largest gain, the other two smaller and similar.
[O - Organization] Three evenly spaced groups on a shared zero baseline; within each group two adjacent equal-width bars, baseline-then-self-consistency.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — neutral gray baseline bars, #0072B2 self-consistency bars, #000000 axis; no gradients.
[E - Exclusions] No numeric values, no "+17.9%/+11.0%/+12.2%" labels, no benchmark names (GSM8K/SVAMP/AQuA), no legend text, no axis tick numbers, no color beyond named hexes, no red-green pairing, no 3D bars.

### Block 3 — Negative Prompt
numeric values, percentage labels, benchmark names, GSM8K text, legend text, axis tick numbers, words, text labels, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 4: One mechanism, three surfaces
Priority: Important
Trigger: VG — the structural synthesis claim that a single RLHF approval-maximization mechanism surfaces as sycophancy, persona drift, and over-revision across three chapters is a relational map not depictable from prose
Figure type: Conceptual map
Concept statement: One underlying mechanism — RLHF-learned approval-maximization — generates three apparently distinct failures across the book: sycophantic capitulation, persona drift toward the default register, and self-correction over-revision.
Reader prior knowledge: RLHF and sycophancy (Ch. 4); persona salience decay (Ch. 6); over-revision under "are you sure?" (§15.4).
Source anchor: Section: 15.7 Closing the loop: how the failures compound

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector conceptual-map figure on a white background showing one central source node from which three branches radiate to three peripheral surface nodes. At the center, draw a single circular hub node (the approval-maximization mechanism) in primary blue #0072B2. From the hub draw three single-headed arrows fanning outward at roughly equal angles to three identical rounded-rectangle surface nodes, each rendered in secondary orange #E69F00, representing the three distinct failure surfaces. Keep the three surface nodes equal in size and symmetrically placed around the hub (for example upper-left, upper-right, and bottom). Optionally draw three faint thin connecting lines among the three surface nodes in neutral gray to suggest they are siblings of one cause, but keep these subordinate to the radial arrows. Total components: one hub plus three surface nodes — four maximum, with three radial single-headed arrows. Okabe-Ito only: #0072B2 hub, #E69F00 surface nodes, neutral gray optional sibling links, #000000 arrows. No numbers, no text, no labels, no words anywhere. Flat vector, 1pt single-headed arrows, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] One central hub (the approval-maximization mechanism) radiating three single-headed arrows to three equal peripheral surface nodes (the three failures), with optional faint gray sibling links among the three.
[O - Organization] Radial layout: hub centered, three surface nodes symmetric around it; arrows point outward from hub to each surface; sibling links subordinate.
[P - Presentation] Flat vector, 1pt single-headed arrows; Okabe-Ito only — #0072B2 hub, #E69F00 surface nodes, neutral gray sibling links, #000000 arrows; no gradients.
[E - Exclusions] No text, no "sycophancy/persona drift/over-revision" or "RLHF" words, no chapter numbers, no fourth surface node, no color beyond named hexes, no red-green pairing.

### Block 3 — Negative Prompt
mechanism names, sycophancy text, persona drift text, RLHF text, chapter numbers, fourth surface node, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video Candidate Pass
FIGURE 1 — notebook to monitored pipeline: VIDEO CANDIDATE — the pipeline has a temporal flow and a feedback loop (deploy, monitor samples, drift triggers re-validation) — animating the drift-to-re-validation loop shows why monitoring closes a cycle a static flow only implies.
FIGURE 2 — grounded-vs-ungrounded decision tree: STATIC SUFFICIENT — a reference predicate the reader scans to a leaf; non-linear lookup is better served by a single legible frame.
FIGURE 3 — self-consistency gains: STATIC SUFFICIENT — a static quantitative comparison; one frame carries the three magnitudes.
FIGURE 4 — one mechanism, three surfaces: STATIC SUFFICIENT — a structural relationship with no process; the simultaneity of the three surfaces is the message and reads instantly.

Recommendation: Build all four as static vectors; the chapter is synthesis-heavy and each figure is a reference or comparison that one frame serves well. Promote Figure 1 to a short animated build only for an interactive edition, where dramatizing the monitor→re-validate feedback loop reinforces that production stability is engineered, not handed over.
