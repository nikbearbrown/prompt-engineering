# CAJAL Figure Intelligence — Chapter 6 — Persona and Audience Patterns

Source: chapters/06-persona-and-audience-patterns.md
Mode: /scan silent
Date: 2026-05-29

## Density Recommendation
4 figure candidates. Mixed density. The chapter pairs a clean conceptual distinction (two patterns, the swap test, the protective-constraint mechanism) with a procedural diagnostic protocol and a taxonomy of four failure modes, so most leverage is in conceptual-map and process figures rather than quantitative ones.

## Figure 1: Persona vs. Audience Persona — what each instruction changes
Priority: Critical
Trigger: VG — structural claim that two similar-sounding instructions act on different targets (speaker vs. listener), not depictable from prose alone
Figure type: Comparison panels
Concept statement: The Persona Pattern changes who the model *is* (speaker identity, vocabulary, reasoning), while the Audience Persona Pattern changes who the model *speaks to* (output complexity and content selection) while preserving full model knowledge.
Reader prior knowledge: Knows a prompt is a set of named constraints (Ch. 5); knows token sampling (Ch. 1).
Source anchor: Section: 6.2 Two patterns, pulled apart

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector comparison figure with two side-by-side panels of equal size on a white background. Left panel represents the Persona Pattern: a single labeled box at top (the model/speaker) connected by a downward arrow to an output box, with the speaker box emphasized as the changed element using primary blue #56B4E9 fill. Right panel represents the Audience Persona Pattern: the same model box at top in neutral gray, an arrow down to a distinct reader/listener box emphasized as the changed element in secondary orange #E69F00, then an arrow to an output box. Place a thin vertical divider line between the two panels. In each panel use exactly three stacked components (model, the changed element, output) joined by single-headed downward arrows with 1pt strokes. Keep the emphasized element visually dominant by fill weight only. Use only Okabe-Ito colors: #56B4E9 for the speaker-as-changed, #E69F00 for the listener-as-changed, gray for unchanged elements, #000000 for strokes. No text, no labels, no words anywhere in the image. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, fully unannotated (no text).
[C - Content] Two prompt patterns shown as parallel three-node chains: Persona Pattern (speaker box is the changed node) and Audience Persona Pattern (listener box is the changed node); both retain a model-source node and an output node.
[O - Organization] Two equal panels side by side separated by a thin vertical rule; within each panel three boxes stacked vertically, joined top-to-bottom by single-headed arrows.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — primary blue #56B4E9 (Persona changed node), secondary orange #E69F00 (Audience changed node), gray neutral for unchanged nodes, #000000 strokes; emphasis by fill only.
[E - Exclusions] No text, letters, slot labels, titles, or captions; no third panel; no diagonal or curved connectors; no icons of people; no color beyond the named hexes; no red-green pairing.

### Block 3 — Negative Prompt
human figures, faces, speech bubbles, third panel, diagonal connectors, color-coded legends, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 2: The combined pattern as a protective constraint
Priority: Critical
Trigger: VG — the load-bearing architectural claim (audience clause bounds the expert persona's jargon) is a structural intersection not depictable from text
Figure type: Conceptual map
Concept statement: Pairing an expert persona with a non-expert audience persona samples output from the intersection of expert content and non-expert register, because the audience clause is a second conditioning signal that bounds the first.
Reader prior knowledge: Token-probability conditioning (Ch. 1); the two patterns from §6.2.
Source anchor: Section: 6.3 The Audience Persona as protective constraint

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector conceptual-map figure on a white background showing two large overlapping regions arranged as a two-set intersection. The left region represents the expert-persona influence and is filled secondary orange #E69F00 at low opacity; the right region represents the audience-clause bound and is filled primary blue #0072B2 at low opacity. Their overlapping intersection in the center is the admissible output zone and is emphasized in active green #009E73. Add one short arrow entering from the left labeled-position pointing into the orange region and one short arrow entering from the right pointing into the blue region, both single-headed with 1pt strokes, to show two conditioning signals pushing inward toward the intersection. Keep total components to five: left region, right region, intersection, and two inward arrows. Use only Okabe-Ito colors: #E69F00, #0072B2, #009E73, with #000000 strokes. The intersection must be the visually dominant element. No text, no labels, no words, no set-notation symbols anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Two overlapping influence regions (expert-persona signal, audience-clause signal) with a highlighted intersection representing admissible output; two inward single-headed arrows representing the competing conditioning signals.
[O - Organization] Standard two-set overlap centered horizontally; one arrow entering each outer region pointing toward the center; intersection centered and emphasized.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — #E69F00 expert region, #0072B2 audience region, #009E73 intersection (active/admissible), #000000 strokes; regions at reduced fill so overlap reads clearly.
[E - Exclusions] No text, set-notation symbols, percentages, or labels; no third set; no shading gradients to fake depth; no icons; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
set notation symbols, mathematical operators, percentages, third circle, venn legend, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 3: Four persona failure modes
Priority: Important
Trigger: VG — a taxonomy of four distinct failure modes, each with its own locus and cause, is a hierarchy/classification not legible from running prose
Figure type: Hierarchy/taxonomy
Concept statement: Persona-based systems fail in four distinct, separable modes — drift (over turns), mismatch (no audience), hallucination (knowledge absent), bleeding (multi-agent) — each tracing to a specific design decision.
Reader prior knowledge: The two patterns and the diagnostic intent; multi-agent systems as a special case.
Source anchor: Section: 6.4 Four failure modes, compressed

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector taxonomy figure on a white background. Place one parent node at top center representing persona failure. Draw single-headed connectors descending to four child nodes arranged in a single horizontal row beneath it. The first three child nodes (drift, mismatch, hallucination) are single-turn-or-general failures and use neutral gray fill. The fourth child node (bleeding) is the multi-agent special case and is set apart on the right with a blocking-orange #D55E00 fill and a slightly heavier outline to mark it as the distinct multi-agent branch. Below the fourth node only, add a small bracket grouping two tiny sub-nodes representing its two contamination sub-pathways, kept minimal. Total components: one parent, four children, two small sub-nodes — eight maximum. Connectors are 1pt single-headed lines that branch cleanly without crossing. Use only Okabe-Ito colors: gray for the three general modes, #D55E00 for the multi-agent mode, #000000 strokes. No text, no labels, no words anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] One root failure node branching to four failure-mode nodes; the fourth (multi-agent) node distinguished and carrying two small contamination sub-nodes.
[O - Organization] Root at top center; four children in one horizontal row; non-crossing single-headed branch connectors; the multi-agent node positioned rightmost with its sub-nodes bracketed beneath it.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — neutral gray for the three general modes, blocking #D55E00 for the multi-agent mode, #000000 strokes; emphasis by fill and outline weight only.
[E - Exclusions] No text, mode names, or captions; no more than four children; no icons; no decorative tree ornamentation; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
extra branches, more than four children, crossing connectors, organizational-chart photos, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 4: Five-step diagnostic protocol
Priority: Important
Trigger: MC — an ordered five-step decision procedure with branch points (single-turn isolation, prompt diagnosis, drift characterization, agent isolation, compound check)
Figure type: Process flowchart
Concept statement: A degraded persona system is diagnosed by an ordered protocol whose branch outcomes route to specific failure-mode hypotheses and back-loops for compound failures.
Reader prior knowledge: The four failure modes from §6.4; multi-agent as a branch.
Source anchor: Section: 6.5 Diagnostic protocol

### Block 1 — Illustrae Paste Block
Create a flat blank unannotated vector process-flowchart figure on a white background reading top to bottom. Begin with a start node, then a first decision diamond (single-turn isolation test) with two outgoing single-headed branches. Continue to a second decision diamond (prompt-level diagnosis), then a third (drift characterization), then a fourth decision diamond gated for the multi-agent case (agent isolation), and finally a fifth process box (compound failure check) that has one feedback arrow looping back upward to an earlier step. Use exactly: one start node, four decision diamonds, one terminal process box, and one feedback loop arrow — six core components plus the loop. Decision diamonds use primary blue #56B4E9 fill; the terminal compound-check box uses active green #009E73; the single feedback loop arrow is drawn distinctly in #D55E00 to mark the re-test back-edge. All connectors are 1pt single-headed lines, vertically aligned, no crossings except the clearly routed feedback edge. Use only Okabe-Ito colors with #000000 strokes. No text, no labels, no words anywhere. Flat vector, no shadows, no gradients, white background.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook width, 300 DPI, vector, white background, unannotated.
[C - Content] Five ordered diagnostic stages: start, four decision diamonds (single-turn isolation, prompt diagnosis, drift characterization, multi-agent isolation), terminal compound-check box, plus one feedback edge back to an earlier stage.
[O - Organization] Vertical top-to-bottom flow; decision diamonds with two branches each; one routed feedback arrow looping from the terminal box up to a prior node.
[P - Presentation] Flat vector, 1pt strokes; Okabe-Ito only — #56B4E9 decision diamonds, #009E73 terminal box, #D55E00 feedback edge, #000000 strokes.
[E - Exclusions] No text, step numbers, yes/no labels, or captions; no swimlanes; no more than four diamonds; no icons; no color beyond named hexes; no red-green pairing.

### Block 3 — Negative Prompt
yes/no text on branches, step number labels, swimlanes, extra diamonds, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video Candidate Pass
FIGURE 1 — Persona vs. Audience Persona: STATIC SUFFICIENT — single structural contrast — the whole point is one frozen side-by-side comparison the reader scans, no temporal evolution.
FIGURE 2 — Protective constraint intersection: STATIC SUFFICIENT — the intersection is a single equilibrium state — the two inward signals are conceptual, not a sequence that unfolds in time.
FIGURE 3 — Four failure modes: STATIC SUFFICIENT — taxonomy — a classification is inherently atemporal.
FIGURE 4 — Diagnostic protocol: VIDEO CANDIDATE — multi-step branching process with a feedback loop — animating the traversal of one example transcript through the branches and the re-test back-edge would clarify the iterative "fix, re-test, check masked failures" logic that a static flowchart only implies.
Recommendation: Render all four as static textbook figures; reserve Figure 4 for an optional animated walkthrough if a companion video layer is produced.
