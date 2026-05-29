# CAJAL Figure Intelligence — Chapter 7 — Structuring and Governing Output

Source: chapters/07-structuring-and-governing-output.md
Mode: /scan silent
Date: 2026-05-29

## Density Recommendation
5 figure candidates. Mechanistic density. The chapter is built on one autoregressive-conditioning mechanism applied at four scopes plus one governing pattern, so figures should make the shared mechanism, the four-pattern mapping, the shared failure-and-escape, and the in-prompt-vs-isolated filter distinction visible.

## Figure 1: Structure as conditioning — entropy collapse after a committed token
Priority: Critical
Trigger: VG — the core falsifiable mechanism (committing a structural token narrows the conditional distribution over later tokens) is a claim about distribution shape, invisible in prose
Concept statement: Emitting a structure-bearing token early collapses the conditional distribution over the next token from broad and high-entropy to narrow and concentrated on label-appropriate continuations.
Figure type: Comparison panels
Reader prior knowledge: Softmax distribution, temperature, conditional entropy (Ch. 1).
Source anchor: Section: 7.2 The mechanism: structure is conditioning

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector comparison figure on a white background with two stacked panels of equal width. Each panel is a discrete bar distribution (a row of vertical bars of varying height) representing the probability over next tokens, with the y-axis baseline at zero and all bars rising from a shared horizontal floor line. The top panel (before any structural commitment) shows many bars of similar moderate height spread broadly across the axis, representing high entropy, all in neutral gray. The bottom panel (after a committed structural label) shows the same axis but with probability mass concentrated into one or two tall bars on the left and the remaining bars very short, representing low entropy; the dominant tall bars are filled active green #009E73 while the suppressed short bars stay neutral gray. Align the two panels on a common baseline and common bar positions so the redistribution is directly comparable. Keep to roughly eight bars per panel. Use only Okabe-Ito colors: gray for the broad/suppressed bars, #009E73 for the concentrated dominant bars, #000000 axis and strokes. No numbers, no axis ticks-with-values, no text, no labels anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Two next-token probability distributions over the same token positions: broad high-entropy (pre-commitment) and concentrated low-entropy (post-commitment), shown as bar charts sharing a zero baseline.
[O - Organization] Two equal panels stacked vertically, aligned on identical x-positions and a common zero baseline; concentrated mass on the left in the lower panel.
[P - Presentation] Flat vector, 1pt strokes; bars from zero baseline; Okabe-Ito only — neutral gray broad/suppressed bars, #009E73 dominant bars, #000000 axis; no fill gradients.
[E - Exclusions] No numeric axis values, tick labels, percentages, or text; no curve overlay; no more than ~8 bars; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
numeric axis values, percentage labels, tick-mark numbers, smooth curve overlays, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 2: One mechanism, four scopes
Priority: Critical
Trigger: VG — the structural claim that four surface-different patterns are one mechanism aimed at four targets (format, procedure, organization, action space) is a mapping not depictable from text
Concept statement: The Template, Recipe, Outline Expansion, and Menu Actions patterns are the same early-structural-commitment mechanism applied at four different scopes of the output.
Figure type: Conceptual map
Reader prior knowledge: The conditioning mechanism (Fig. 1 / §7.2); the four patterns by name.
Source anchor: Section: 7.2 The four structuring patterns, and the one thing they have in common

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector conceptual-map figure on a white background. Place a single central node representing the shared conditioning mechanism, filled primary blue #0072B2. Draw four single-headed connectors radiating outward to four peripheral nodes arranged evenly around the center. Each peripheral node depicts a distinct committed structure schematically: one as a stack of horizontal slot bars (flat format scaffold), one as a vertical numbered-step chain shown as stacked rungs (ordered procedure), one as a branching tree of two levels (hierarchy), and one as a closed ring of small equal segments (a bounded action set). The four peripheral nodes use secondary orange #E69F00 fill to read as the four scopes; the central mechanism node is dominant in #0072B2. Total components: one center plus four periphery plus four connectors. Connectors are 1pt single-headed radial lines that do not cross. Use only Okabe-Ito colors: #0072B2 center, #E69F00 peripheral nodes, #000000 strokes. No text, no labels, no words anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] One central mechanism node radiating to four scope nodes, each rendered as a small schematic of its committed structure: flat slot stack (format), numbered chain (procedure), two-level tree (hierarchy), closed segmented ring (action space).
[O - Organization] Hub-and-spoke; central node dominant; four periphery nodes evenly distributed; non-crossing radial single-headed connectors.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — #0072B2 hub, #E69F00 spokes, #000000 strokes; distinguish the four schematics by shape, not color.
[E - Exclusions] No text, pattern names, or captions; no more than four spokes; no icons of food/menus/people; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
pattern name text, recipe icons, restaurant menu imagery, more than four spokes, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 3: The shared failure and its escape hatch
Priority: Important
Trigger: VG — the structural relationship that each pattern's empty-slot confabulation is neutralized by a matched legal low-entropy escape value is a four-row correspondence (the chapter's own table) better shown structurally
Concept statement: Each structuring pattern shares one failure — confabulation to fill a committed slot that outruns content — and each is made safe by a matched escape value that gives the model a legal low-entropy honest completion.
Figure type: Comparison panels
Reader prior knowledge: The four patterns and their committed structures; the conditioning mechanism.
Source anchor: Section: 7.7 The shared cost, named once and precisely

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector figure on a white background structured as a four-row correspondence grid with two columns. Each of the four rows represents one structuring pattern. The left column cell shows a small schematic of a committed structure with one slot rendered empty/highlighted to mark the confabulation pressure point, filled blocking-orange #D55E00 to signal the danger. The right column cell, in the same row, shows the same structure with that slot now carrying a distinct escape marker (a small flagged element) filled active green #009E73 to signal the safe legal completion. Draw a single-headed arrow from the left cell to the right cell in each row to show the mitigation move. Keep each schematic minimal (two or three marks). Total: four rows times two cells, with four connecting arrows — eight schematic clusters maximum. Use only Okabe-Ito colors: #D55E00 for the unsafe empty slot, #009E73 for the escape value, neutral gray for the surrounding committed structure, #000000 strokes. No text, no labels, no words anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Four pattern rows, each a left "unsafe empty slot" schematic and a right "escape-value installed" schematic, joined by a single-headed mitigation arrow.
[O - Organization] Four-row, two-column grid; consistent left-to-right arrow per row; the highlighted slot in the same relative position across rows.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — #D55E00 unsafe slot, #009E73 escape value, neutral gray surrounding structure, #000000 strokes.
[E - Exclusions] No text, pattern names, escape keywords (UNKNOWN/UNSUPPORTED), or captions; no table gridlines styled as a spreadsheet; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
escape keyword text, UNKNOWN or UNSUPPORTED words, pattern name labels, spreadsheet styling, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 4: In-prompt self-filter vs. isolated classifier
Priority: Critical
Trigger: VG — the load-bearing engineering claim that context isolation makes the filter robust is a structural difference (shared vs. separate context) not legible from prose
Concept statement: An in-prompt self-filter shares the generator's context and pressure signal so it can be talked past, whereas a separately invoked classifier evaluates only the artifact in a clean isolated context.
Figure type: Systems diagram
Reader prior knowledge: Context isolation as the dissenting-sub-agent move (Ch. 4); the generator/filter relationship.
Source anchor: Section: 7.8 In-prompt filter vs. separate classifier

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector systems diagram on a white background with two side-by-side configurations separated by a thin vertical divider. Left configuration (in-prompt self-filter): one large enclosing boundary box containing both a generator node and a filter node together, with the external pressure/input arrow entering the shared box and reaching both nodes; render the shared boundary and its contents in blocking-orange #D55E00 to mark the weak shared-context arrangement, and show the filter node inside the same enclosure as the generator. Right configuration (isolated classifier): a generator node in its own boundary box, an output artifact passing along a single-headed arrow to a separate filter node in a distinct, non-overlapping boundary box; the pressure/input arrow reaches only the generator box, not the filter; render the separate filter boundary in active green #009E73 to mark the robust isolated arrangement. Use exactly: left box with two inner nodes plus input arrow; right two boxes plus artifact arrow plus input arrow — under eight components. 1pt single-headed arrows. Okabe-Ito only: #D55E00 shared-context boundary, #009E73 isolated-filter boundary, neutral gray generator nodes, #000000 strokes. No text, no labels, no words anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Two filter architectures: (left) generator and filter inside one shared context boundary with the input/pressure arrow reaching both; (right) generator in one boundary passing only its output artifact to a filter in a separate boundary, with the input/pressure arrow reaching only the generator.
[O - Organization] Two configurations side by side, thin vertical divider; nested boundary boxes; single-headed flow arrows.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — #D55E00 shared-context boundary (weak), #009E73 isolated boundary (robust), neutral gray generator nodes, #000000 strokes.
[E - Exclusions] No text, node names, or captions; the two boundaries on the right must not overlap; no icons of people or shields; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
shield icons, lock icons, person icons, overlapping right-side boundaries, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 5: Decision procedure — match the pattern to where uncertainty lives
Priority: Important
Trigger: MC — a five-question ordered decision procedure mapping uncertainty location to pattern choice, with a "none of the above" terminal
Concept statement: The right structuring/governing pattern is selected by an ordered series of questions that locate the variance that hurts (format, procedure, organization, action space, admissibility — or none), each routing to a specific pattern.
Figure type: Process flowchart
Reader prior knowledge: All five patterns; the orthogonality boundary (Ch. 2).
Source anchor: Section: 7.9 A decision procedure

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector decision-flowchart figure on a white background reading top to bottom. Begin with a start node, then a vertical chain of five decision diamonds in sequence (format consumer, procedure, long output, action space, admissibility). Each diamond has a side branch exiting right to a distinct terminal pattern-node, and a downward branch continuing to the next diamond. After the fifth diamond, the downward path ends in a final distinct terminal representing "none of the above — a correctness problem no pattern here solves." The five pattern terminals on the right use primary blue #56B4E9 fill; the final none-of-the-above terminal uses blocking-orange #D55E00 to mark it as the out-of-scope outcome. Decision diamonds use secondary orange #E69F00 fill. All connectors are 1pt single-headed lines, vertically aligned spine with clean right-exits, no crossings. Total: start, five diamonds, six terminals — kept to the eight-component spirit by aligning terminals as a compact right column. Okabe-Ito only: #E69F00 diamonds, #56B4E9 pattern terminals, #D55E00 out-of-scope terminal, #000000 strokes. No text, no labels, no words anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Ordered five-diamond decision spine, each diamond exiting right to a pattern terminal and down to the next diamond; a final out-of-scope terminal after the last diamond.
[O - Organization] Vertical decision spine with right-side terminal column; single-headed branches; the out-of-scope terminal visually distinct at the bottom.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — #E69F00 decision diamonds, #56B4E9 pattern terminals, #D55E00 out-of-scope terminal, #000000 strokes.
[E - Exclusions] No text, question text, pattern names, or yes/no labels; no swimlanes; no more than five diamonds; no icons; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
question text, pattern name labels, yes/no branch text, swimlanes, extra diamonds, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video Candidate Pass
FIGURE 1 — Entropy collapse: VIDEO CANDIDATE — a distribution transforming from broad to concentrated the instant a structural token commits is intrinsically a transition; a two-frame morph would make the conditioning mechanism vivid, though the static before/after panels carry it.
FIGURE 2 — One mechanism, four scopes: STATIC SUFFICIENT — conceptual mapping — a hub-and-spoke relationship is atemporal.
FIGURE 3 — Failure and escape hatch: STATIC SUFFICIENT — four-row correspondence — a parallel comparison, not a process.
FIGURE 4 — In-prompt vs. isolated filter: STATIC SUFFICIENT — architectural contrast — two frozen configurations the reader compares.
FIGURE 5 — Decision procedure: VIDEO CANDIDATE — ordered branching with multiple terminals — animating one scenario walking the spine to its terminal would teach the routing, though a static flowchart suffices.
Recommendation: Render all five as static figures; Figure 1 and Figure 5 are the strongest optional-video candidates if an animated layer is produced.
