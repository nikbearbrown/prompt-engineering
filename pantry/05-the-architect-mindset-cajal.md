# CAJAL Figure Intelligence — Chapter 5 — The Architect Mindset

Source: chapters/05-the-architect-mindset.md
Mode: /scan silent
Date: 2026-05-29

## Density Recommendation
4 figure candidates. Mixed density. The chapter is built on three reusable structures — the four-layer anatomy of a prompt, the PAST/PLFR scaffolds, and the entropy mechanism behind negative constraints — each a hierarchy, pipeline, or quantitative claim that benefits from a depictable form the prose only gestures at.

## Figure 1: The Four Layers of a Prompt
Priority: Critical
Trigger: VG — a structural/hierarchy claim (four separable layers each conditioning the output distribution differently) not depictable from text alone
Figure type: Hierarchy/taxonomy
Concept statement: A production prompt decomposes into four separable layers — root, constraints, persona, format — each acting on the output distribution in a distinct way, so each can be debugged independently.
Reader prior knowledge: Has written prompts as single paragraphs; needs the separable-layer structure made explicit.
Source anchor: Section: 5.2 Four layers: what a prompt is made of

### Block 1 — Illustrae Paste Block
Draw a flat vector stacked-layer diagram of four horizontal bands stacked vertically, each band representing one prompt layer, with a short caption-free icon-shape inside each band indicating its function: the root band shows a broad target region, the constraints band shows a region with a notch carved out of it, the persona band shows a reweighted sub-region, the format band shows a rigid grid. To the right of the stack, draw a single vertical bracket joining all four bands to one output node, signaling that the layers compose onto one output distribution. Use five components: four layer bands plus the composed-output node. Color the root band in blue #56B4E9 (the broad selecting layer), the constraints band in green #009E73 (the active carving layer), the persona band in orange #E69F00 (the secondary reweighting layer), the format band in blue #0072B2 (the structural collapsing layer), and the output node in neutral light gray. Bands separated by thin black #000000 1pt rules; the joining bracket and its arrow in black #000000, single-headed. Blank unannotated flat vector on white, single column.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook figure, 300 DPI, vector, white background, unannotated.
[C - Content] Five components: root band (broad target), constraints band (region with a carved notch), persona band (reweighted sub-region), format band (rigid grid), composed-output node joined by a bracket. Preserve that the four layers stack and compose onto one output.
[O - Organization] Four bands stacked vertically in order root → constraints → persona → format; a vertical bracket on the right joins all four to a single output node via one arrow.
[P - Presentation] Flat vector, Okabe-Ito — root #56B4E9, constraints #009E73, persona #E69F00, format #0072B2, output node light gray, rules and bracket #000000 1pt. No text in image; layer roles shown by icon-shape and color only.
[E - Exclusions] No layer names as text, no prompt text, no equations, no labels, no human figures.

### Block 3 — Negative Prompt
layer names, prompt text, equations, labels, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 2: PAST Builds the Prompt Slot of PLFR
Priority: Critical
Trigger: MC — two interlocking pipelines (PAST's four input slots nest inside the Prompt stage of PLFR's four-stage pipeline) with a validation step the model cannot self-perform
Figure type: Systems diagram
Concept statement: The PAST scaffold structures the input into Problem, Action, Steps, Task, and that authored input becomes the Prompt slot of the larger PLFR pipeline, whose Result stage adds an external validation step distinct from generation.
Reader prior knowledge: New to both acronyms; needs the nesting relationship and the generation-vs-validation seam made visible.
Source anchor: Section: 5.4 PLFR: a scaffold for the pipeline

### Block 1 — Illustrae Paste Block
Draw a flat vector systems diagram with a nested structure. On the left, a tall container box represents the PLFR Prompt stage; inside it, stack four small sub-boxes representing PAST's Problem, Action, Steps, and Task slots in order. From this container, a single-headed arrow leads right to a Logic node, then to a Format node, then to a Result node. From the Result node, draw a separate external validator box (clearly outside the main model pipeline) connected by a single-headed arrow, with a return arrow from the validator back to a ship/accept endpoint. Use eight components: the PAST-filled Prompt container counts as one container with four inner slots, plus Logic, Format, Result, external validator, and accept endpoint. Color the PAST container and its four inner slots in blue #56B4E9 (authored input), the Logic node in orange #E69F00, the Format node in blue #0072B2, the Result node in green #009E73, the external validator in green #009E73 with a distinct outline to mark it as outside the generator, and the accept endpoint neutral light gray. Arrows black #000000, single-headed. Blank unannotated flat vector on white, single column.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook figure, 300 DPI, vector, white background, unannotated.
[C - Content] PLFR pipeline: Prompt container holding four PAST sub-slots, then Logic, Format, Result nodes; an external validator box connected off the Result node returning to an accept endpoint. Preserve that PAST nests inside Prompt and that the validator is external to the generator.
[O - Organization] Left-to-right pipeline: nested PAST-Prompt container → Logic → Format → Result; validator branches out from Result and returns to the accept endpoint.
[P - Presentation] Flat vector, Okabe-Ito — PAST container + inner slots #56B4E9, Logic #E69F00, Format #0072B2, Result #009E73, external validator #009E73 with distinct outline, accept endpoint light gray, arrows #000000 1pt. No text in image.
[E - Exclusions] No acronym letters, no slot names, no prompt text, no JSON, no labels, no human figures.

### Block 3 — Negative Prompt
acronym letters, slot names, prompt text, JSON code, labels, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 3: Negative Constraints Remove Probability Mass
Priority: Critical
Trigger: PQ — a quantitative/distributional claim (a negative constraint zeroes a region and lowers entropy; positive reweighting only nudges) — the magnitude and shape of the distribution change is the argument
Figure type: Comparison panels
Concept statement: A positive constraint piles probability onto a good region while leaving the rest diffusely populated, whereas a negative constraint deletes nameable bad regions entirely, lowering output entropy and narrowing the admissible set.
Reader prior knowledge: Comfortable with a probability distribution over outputs and the idea of entropy.
Source anchor: Section: 5.5 Negative constraints are first-class — the entropy argument

### Block 1 — Illustrae Paste Block
Draw three flat vector comparison panels in a row, each showing a probability distribution as a curve or set of bars over the same horizontal output-space axis (axis baseline at zero, no numerals). Panel 1 (baseline): a broad, high-entropy spread covering the whole axis, in neutral light gray. Panel 2 (positive constraint): the same spread with one region built up taller, but mass still present everywhere else, shown with the raised good region in blue #0072B2 and the still-populated remainder in light gray. Panel 3 (negative constraint): two specific regions zeroed out to the baseline and crossed by a blocking bar, with the surviving mass renormalized taller onto the remaining region; draw the deleted regions with a blocking bar in vermillion #D55E00 and the surviving concentrated mass in green #009E73. Use no more than three components per panel. Keep the horizontal axis identical across all three panels so the reshaping is directly comparable. Axis lines black #000000 1pt; all y-axes start at zero. Blank unannotated flat vector on white, single column.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook figure, 300 DPI, vector, white background, unannotated.
[C - Content] Three panels over an identical output-space axis: (1) broad high-entropy baseline, (2) positive constraint raising one region while mass remains everywhere, (3) negative constraint zeroing two named regions with surviving mass renormalized taller. Preserve that deletion concentrates mass more decisively than reweighting.
[O - Organization] Three side-by-side panels sharing one horizontal axis and a common zero baseline; left to right shows baseline → positive → negative.
[P - Presentation] Flat vector, Okabe-Ito — baseline mass light gray, positive raised region #0072B2, deleted regions' blocking bar #D55E00, surviving concentrated mass #009E73, axes #000000 1pt. Y-axis starts at zero. No numerals, no text.
[E - Exclusions] No axis numbers, no entropy values, no equation, no region labels, no panel titles.

### Block 3 — Negative Prompt
axis numbers, entropy values, equations, region labels, panel titles, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 4: Two Failures, Two Layers — Tracing trial and shoot Through the System
Priority: Important
Trigger: MC — the assembled Wordsville system as a multi-stage pipeline where two distinct failures are fixed at two distinct, pointable layers (Step 1 + constraint vs. Result-layer validator)
Figure type: Annotated example
Concept statement: In the assembled prompt system the wrong-word-sense failure is fixed early at the sense-selection step plus a negative constraint, while the unsafe-completion failure is reduced by a constraint and then caught at the external Result-layer validator — two failures pinned to two different layers.
Reader prior knowledge: Has followed the layer and scaffold concepts; needs to see the two failure paths land on different layers.
Source anchor: Section: 5.6 Assembling the Wordsville prompt system

### Block 1 — Illustrae Paste Block
Draw a flat vector pipeline flowchart of the assembled system as a vertical sequence: persona/root node, a sense-selection step node, a constraints node, a format node, a generation node, and a final external Result-layer validator node before a ship endpoint. Then overlay two distinct failure-trace paths as colored side-arrows pointing to where each failure is handled. Trace one: a wrong-word-sense failure arrow points to the sense-selection step AND to the constraints node, indicating it is fixed early. Trace two: an unsafe-completion failure arrow points to the constraints node (reduced) and then forward to the Result-layer validator node (caught), indicating it is stopped late. Use seven components: the six pipeline nodes plus the two overlaid failure-trace indicators counted together. Color the pipeline nodes neutral light gray and blue #0072B2, the wrong-sense failure trace in orange #E69F00 landing on its early fix, the unsafe-completion failure trace in vermillion #D55E00 landing on the Result validator, and the validator node itself in green #009E73 to mark the external catch. Arrows black #000000 for the main flow; the two failure traces in their own colors, single-headed. Blank unannotated flat vector on white, single column.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook figure, 300 DPI, vector, white background, unannotated.
[C - Content] Vertical pipeline: persona/root, sense-selection step, constraints, format, generation, external Result-layer validator, ship endpoint; plus two overlaid failure traces — wrong-sense landing on sense-selection + constraints, unsafe-completion landing on constraints then the validator. Preserve that the two failures resolve at two different layers.
[O - Organization] Single vertical main flow top-to-bottom with single-headed black arrows; two colored side-arrows branch in to mark each failure's handling layer.
[P - Presentation] Flat vector, Okabe-Ito — pipeline nodes light gray and #0072B2, external validator #009E73, wrong-sense trace #E69F00, unsafe-completion trace #D55E00, main arrows #000000 1pt. No text in image.
[E - Exclusions] No words trial or shoot, no JSON, no prompt text, no node names, no labels, no human figures.

### Block 3 — Negative Prompt
the words trial or shoot, JSON code, prompt text, node names, labels, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video Candidate Pass
FIGURE 1 — Four layers of a prompt: STATIC SUFFICIENT — a fixed compositional hierarchy — the stacked-band structure reads in one frame.
FIGURE 2 — PAST nested in PLFR: STATIC SUFFICIENT — a fixed nesting and pipeline relationship — best held as one diagram showing both scaffolds at once.
FIGURE 3 — Negative constraints reshape the distribution: VIDEO CANDIDATE — a before/after transformation of a probability distribution — animating mass being deleted and renormalized would make the entropy-reduction claim vivid, though static side-by-side panels are adequate for the textbook.
FIGURE 4 — Two failures, two layers: VIDEO CANDIDATE — two failure paths traversing a multi-stage pipeline to different stop points — stepping each trace through the system in sequence would reinforce the "pointable layer" payoff, though the static annotated flowchart conveys it.

Recommendation: Render all four as static figures; Figures 1, 2, and 3 are Critical to the chapter's core structures, Figure 4 is an Important synthesis. No video required; Figure 3 is the strongest animation candidate if a companion format is later produced.
