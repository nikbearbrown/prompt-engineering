# CAJAL Figure Intelligence — Chapter 2 — Hallucination and the Plausibility–Truth Gap

Source: chapters/02-hallucination-and-the-plausibility-truth-gap.md
Mode: /scan silent
Date: 2026-05-29

## Density Recommendation
4 figure candidates. Mixed density. The chapter argues one orthogonality thesis (plausibility vs. truth) and then deploys one architectural pattern (Fact-Check List + external verifier); the thesis wants a two-axis figure and the pattern wants a flow figure, while the loss-function and worked-example passages stay in prose.

## Figure 1: The two axes — plausibility and truth are orthogonal
Priority: Critical
Trigger: VG — the chapter's core claim is literally geometric ("two axes," "orthogonal," "knowing one tells you nothing about the other"); §2.2 spells out all four quadrant cases
Figure type: Conceptual map (2x2 axes)
Concept statement: Plausibility (probability under training data) and truth (correspondence to the world) are independent axes, so an output can occupy any of four quadrants — including fluent-and-false, the dangerous one.
Reader prior knowledge: Reader has the §2.2 misconception (fluent implies correct) and the explicit enumeration of true/false x plausible/implausible cases.
Source anchor: Section: 2.2 Two axes that human communication taught you to conflate

### Block 1 — Illustrae Paste Block
Create a blank, unannotated flat vector figure for single-column textbook width (89 mm) on a white background, with no generated text. Draw two perpendicular axes forming four quadrants: a horizontal axis running from low to high plausibility, a vertical axis running from false to true. Place one distinct marker dot in each of the four quadrants: true-and-plausible (top right), true-and-implausible (top left), false-and-plausible (bottom right), false-and-implausible (bottom left). Emphasize the bottom-right marker (false but plausible — the hallucination quadrant) as the focal danger point by making it the largest/boldest dot. Use Black #000000 for the two axis lines and arrowheads at 1 pt, Bluish Green #009E73 for the two true-axis markers (top quadrants), Vermillion #D55E00 for the false-and-plausible danger marker (bottom right, emphasized), light gray for the false-and-implausible marker (bottom left, inert). Keep the quadrant cross centered and the four dots clearly one-per-quadrant.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89 mm textbook figure, 300 DPI, flat vector, white background, unannotated.
[C - Content] Two perpendicular axes (plausibility horizontal, truth vertical) with one marker per quadrant; the false-and-plausible marker emphasized. Relationship to preserve: the axes are independent and the bottom-right quadrant is the dangerous, fluent-but-false region.
[O - Organization] Centered 2x2 quadrant cross, single marker per quadrant, emphasis on bottom-right.
[P - Presentation] Flat vector, 1 pt strokes, Okabe-Ito: Black #000000 (axes), Bluish Green #009E73 (true markers), Vermillion #D55E00 (false-plausible danger marker), light gray (false-implausible marker). No text in image.
[E - Exclusions]
- axis labels ("plausibility" / "truth" / "true" / "false")
- quadrant captions
- example sentences or the Mycroft quote
- gridlines beyond the two axes
- red-green markers adjacent enough to read as a pair

### Block 3 — Negative Prompt
axis labels, plausibility text, truth text, quadrant captions, example sentences, Mycroft quote, dense gridlines, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 2: Where truth would have to live in the loss — and doesn't
Priority: Important
Trigger: VG — §2.3 argues a structural absence: every term in the cross-entropy loss references training text, and there is no slot for correspondence-to-fact; the figure makes the "missing term" spatial
Figure type: Annotated structural schematic
Concept statement: The maximum-likelihood objective scores only whether the model predicted the token that actually occurred in the corpus; there is no term in the pipeline where a truth-of-the-world signal could enter.
Reader prior knowledge: Reader has read the chain-rule factorization and cross-entropy loss and the claim that truth is not in the data in a form the loss can see.
Source anchor: Section: 2.3 Inside the objective: where truth would have to live, and doesn't

### Block 1 — Illustrae Paste Block
Create a blank, unannotated flat vector figure for single-column textbook width (89 mm) on a white background, with no generated text. Show a simple horizontal training-signal pipeline: a corpus block (stacked text-line glyphs, no readable text) feeds an arrow into a model block, which emits a predicted-next-token glyph; a comparison node checks the predicted token against the actual-next-token glyph drawn from the corpus, and feeds a loss-update arrow back to the model. Separately, draw a detached "world / facts" block off to the side with a dashed, broken connector that does NOT reach the comparison node — an empty docking slot showing the missing truth term. Use Sky Blue #56B4E9 for the corpus block, Blue #0072B2 for the model block as the primary subject, light gray for the predicted/actual token glyphs and comparison node, Bluish Green #009E73 for the loss-update feedback arrow (the signal that exists), Vermillion #D55E00 for the detached world/facts block and its broken connector (the signal that is absent), Black #000000 for solid arrows and outlines at 1 pt. Make the broken/unconnected world block visually distinct from the closed training loop.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89 mm textbook figure, 300 DPI, flat vector, white background, unannotated.
[C - Content] Closed loop: corpus to model to predicted token, compared against actual next token, loss fed back. Detached world/facts block with a broken connector to an empty slot. Relationship to preserve: the training signal closes over text only; truth has no path into the objective.
[O - Organization] Horizontal closed training loop with one detached, non-connecting external block.
[P - Presentation] Flat vector, 1 pt strokes, Okabe-Ito: Sky Blue #56B4E9 (corpus), Blue #0072B2 (model), light gray (token glyphs/comparison), Bluish Green #009E73 (loss feedback), Vermillion #D55E00 (detached world block + broken connector), Black #000000 (solid arrows/outlines). No text in image.
[E - Exclusions]
- the loss equation or any math symbols
- readable corpus text or token strings
- the words "truth" / "loss" / "world"
- a completed connection from the world block (it must stay broken)
- dual-headed arrows

### Block 3 — Negative Prompt
loss equation, math symbols, readable corpus text, token strings, truth label, loss label, world label, completed world connection, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 3: The Fact-Check List Pattern with external verification
Priority: Critical
Trigger: MC — §2.5 and §2.7 define a multi-step governance pipeline: fluent answer to enumerated load-bearing claims to external verifier to grounded not-found/confirmed, with the model unable to override the external observation
Figure type: Process flowchart
Concept statement: The pattern splits a fluent answer into discrete checkable claims that an external tool or human verifies one at a time, because the model that wrote the answer cannot validate its own fabrications from the same distribution.
Reader prior knowledge: Reader has seen the Mycroft three-claim enumeration and the "honest limit" that the model writes the checklist too, so the external check is what governs.
Source anchor: Section: 2.5 The Fact-Check List Pattern / 2.7 Back to the citation that shipped

### Block 1 — Illustrae Paste Block
Create a blank, unannotated flat vector figure for single-column textbook width (89 mm) on a white background, with no generated text. Left to right: (1) a fluent-answer block (a solid paragraph glyph), feeding into (2) a fan-out into three discrete enumerated-claim items stacked vertically (three small rounded rectangles), feeding into (3) an external verifier node drawn as a distinct module with its own outside-the-system marker (e.g., a tool/document glyph sitting apart from the model region), which returns (4) per-claim verdict markers — two confirmed, one rejected. Draw a boundary outline around stages 1–2 to mark "inside the model's distribution" and place the verifier in stage 3 clearly OUTSIDE that boundary. Use Sky Blue #56B4E9 for the fluent-answer block, Blue #0072B2 for the three enumerated-claim items as the structural handle, Orange #E69F00 for the external verifier module (the outside agent), Bluish Green #009E73 for the two confirmed verdicts, Vermillion #D55E00 for the one rejected/not-found verdict, light gray for the inside-the-model boundary outline, Black #000000 for arrows and outlines at 1 pt. The verifier sitting outside the model boundary must be unmistakable.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89 mm textbook figure, 300 DPI, flat vector, white background, unannotated.
[C - Content] Fluent answer to three enumerated claims (inside a model boundary) to an external verifier (outside the boundary) to three verdicts (two confirmed, one rejected). Relationship to preserve: the enumerated claims are self-generated but the governing check sits outside the model's distribution.
[O - Organization] Left-to-right flow with a boundary outline enclosing the model-internal stages and the verifier placed outside it, single-headed arrows.
[P - Presentation] Flat vector, 1 pt strokes, Okabe-Ito: Sky Blue #56B4E9 (answer), Blue #0072B2 (claim items), Orange #E69F00 (external verifier), Bluish Green #009E73 (confirmed verdicts), Vermillion #D55E00 (rejected verdict), light gray (boundary), Black #000000 (arrows/outlines). No text in image.
[E - Exclusions]
- claim text or the Mycroft quote
- page numbers / basis-point figures
- tool brand names or logos
- the words "verifier" / "fact-check"
- a verifier drawn inside the model boundary

### Block 3 — Negative Prompt
claim text, Mycroft quote, page numbers, basis-point figures, tool logos, brand names, verifier label, fact-check label, verifier inside boundary, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 4: Why a reasoning trace adds no truth term
Priority: Supplementary
Trigger: VG — §2.4 makes a structural claim: chain-of-thought conditions the output into a plausible "step-shaped manifold" without installing validity, evidenced by invalid rationales recovering most of the gain
Figure type: Conceptual map
Concept statement: A reasoning trace steers generation into the region of output space that looks like reasoning, which correlates with correct answers on step-shaped problems but is still a plausibility region, not a validity check.
Reader prior knowledge: Reader has the Wang et al. invalid-rationale result (80–90% of valid-CoT performance) and the "plausibility wearing the costume of logic" framing.
Source anchor: Section: 2.4 The fix that isn't: why a reasoning trace doesn't add a truth term

### Block 1 — Illustrae Paste Block
Create a blank, unannotated flat vector figure for single-column textbook width (89 mm) on a white background, with no generated text. Draw a large outer region representing all plausible outputs, and inside it a smaller enclosed sub-region representing the "step-shaped" reasoning-looking region. Inside that step-shaped sub-region, place two markers: one valid-reasoning marker and one invalid-reasoning marker, sitting close together to show both land in the same region. Draw a separate, partially overlapping but distinct region representing "correct answers," overlapping the step-shaped region only in part — to show correlation, not containment. An input arrow (the CoT prompt) points into the step-shaped sub-region. Use light gray for the outer all-plausible region, Sky Blue #56B4E9 for the step-shaped reasoning sub-region as the conditioned target, Bluish Green #009E73 for the partially overlapping correct-answers region, Orange #E69F00 for the CoT input arrow, Black #000000 for the valid and invalid markers and all outlines at 1 pt. The partial (not full) overlap between step-shaped and correct must be clear.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89 mm textbook figure, 300 DPI, flat vector, white background, unannotated.
[C - Content] Outer plausible-output region; inner step-shaped sub-region holding both a valid and an invalid marker; a partially overlapping correct-answers region; a CoT input arrow into the step-shaped region. Relationship to preserve: CoT targets the step-shaped region (regardless of validity), which only partially overlaps correctness.
[O - Organization] Nested/overlapping region map, two markers inside the inner region, partial overlap with a separate correct region, one input arrow.
[P - Presentation] Flat vector, 1 pt strokes, Okabe-Ito: light gray (plausible region), Sky Blue #56B4E9 (step-shaped region), Bluish Green #009E73 (correct region), Orange #E69F00 (CoT arrow), Black #000000 (markers/outlines). No text in image.
[E - Exclusions]
- region labels or percentages
- the phrase "step by step" or any prompt text
- arithmetic/example content
- full containment of correct inside step-shaped (must be partial overlap)
- dual-headed arrows

### Block 3 — Negative Prompt
region labels, percentages, step by step text, prompt text, arithmetic, example content, full containment, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video Candidate Pass
FIGURE 1 — two axes orthogonal: STATIC SUFFICIENT — fixed conceptual geometry — the quadrant map is inherently static; the four cases read at once.
FIGURE 2 — missing truth term: STATIC SUFFICIENT — structural absence — the broken connector and closed loop are spatial; nothing changes over time.
FIGURE 3 — Fact-Check List pipeline: VIDEO CANDIDATE — sequential grounding — stepping through enumerate to verify to one claim flipping to "not found" enacts the governance the model cannot override; static flow is a fine default.
FIGURE 4 — step-shaped manifold: STATIC SUFFICIENT — region relationship — the overlap geometry is the whole point and is static.

Recommendation: ship all four as static figures; only Figure 3 warrants an optional animated walkthrough, since the per-claim external check resolving in sequence is the chapter's one genuinely temporal mechanism.
