# CAJAL Figure Intelligence — Chapter 4 — Sycophancy and Computational Skepticism

Source: chapters/04-sycophancy-and-computational-skepticism.md
Mode: /scan silent
Date: 2026-05-29

## Density Recommendation
4 figure candidates. Mechanistic density. The chapter's spine is causal and architectural — the RLHF preference-to-capitulation chain, the dissenter system whose load-bearing property is context isolation, the single line of code that silently breaks it, and the helpfulness-equals-sycophancy gradient — each a structural claim a reader cannot reconstruct from prose without a diagram.

## Figure 1: The RLHF Capitulation Chain
Priority: Critical
Trigger: MC — process of ≥3 interdependent stages (preference labels → reward model → policy optimization → output reversal), with isolation interrupting the chain
Figure type: Process flowchart
Concept statement: Agreement-biased preference labels propagate through a learned reward model into the policy's output distribution, so a correct answer reverses under pressure, and only context isolation interrupts the chain.
Reader prior knowledge: Knows RLHF has stages but not how the bias flows through them to produce capitulation.
Source anchor: Section: 4.3 The causal chain, explicitly

### Block 1 — Illustrae Paste Block
Draw a flat vector horizontal process flowchart of five stages connected by single-headed arrows: (1) preference labels shown as a pair of compared cards with one marked as preferred, (2) reward model shown as a scoring box, (3) policy optimization shown as a distribution-reshaping box, (4) output reversal shown as an answer flipping from one state to its opposite, drawn as two stacked bars swapping height. Below stage 4, add (5) an isolation node drawn as a small shielded box with a blocking bar cutting the arrow that would carry the pressure signal forward. Use five components. Color stages 1 through 4 — the bias-propagation path — in orange #E69F00 to mark them as the secondary/problem pathway, the output-reversal node in vermillion #D55E00 to mark the failure, and the isolation interruption node in green #009E73 with its blocking bar also #D55E00. Arrows black #000000, single-headed, left-to-right. Blank unannotated flat vector on white, single column.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook figure, 300 DPI, vector, white background, unannotated.
[C - Content] Five components: preference-label pair, reward-model box, policy-optimization box, output-reversal node (two bars swapping), isolation node with blocking bar. Preserve that bias flows forward through stages 1–4 and that isolation cuts the pressure-carrying arrow.
[O - Organization] Horizontal left-to-right chain for stages 1–4; isolation node branches below stage 4 with a blocking bar interrupting the pressure arrow.
[P - Presentation] Flat vector, Okabe-Ito — propagation path #E69F00, failure node #D55E00, isolation node #009E73, blocking bar #D55E00, arrows #000000 1pt. No text in image.
[E - Exclusions] No equations, no reward-function notation, no gradient symbols, no labels, no numbers, no human faces.

### Block 3 — Negative Prompt
equations, reward function notation, gradient symbols, numbers, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 2: The Dissenting Sub-Agent — Context Isolation as the Load-Bearing Commitment
Priority: Critical
Trigger: VG — structural/hierarchy claim (which agent sees which inputs) not depictable from text; the whole point is the asymmetry of what the dissenter is denied
Figure type: Systems diagram
Concept statement: The primary agent receives the user's pressure signal while the dissenter receives only the original claim and data, and the consensus check routes any disagreement to a mandatory human decision node.
Reader prior knowledge: Understands a "second model call" but not why isolation, specifically, is what makes the architecture work.
Source anchor: Section: 4.3 The dissenting sub-agent and the commitment that actually matters

### Block 1 — Illustrae Paste Block
Draw a flat vector systems diagram. On the left, two source inputs stacked: an original-claim-and-data block and a separate user-pushback block. The claim-and-data block feeds arrows to BOTH a primary agent box and a dissenter agent box. The user-pushback block feeds an arrow ONLY to the primary agent; show clearly that no arrow reaches the dissenter from the pushback block. Both agent boxes feed into a consensus-detector node in the center-right. From the consensus detector, one arrow leads to a ship-output endpoint and a second arrow leads to a distinctly shaped human decision node drawn as a diamond, which is the mandatory gate on disagreement. Use seven components: claim-and-data block, pushback block, primary agent, dissenter agent, consensus detector, ship endpoint, human decision diamond. Color the claim-and-data input and the dissenter in green #009E73 (the protected path), the pushback input in vermillion #D55E00 (the pressure signal), the primary agent in orange #E69F00, the consensus detector in blue #56B4E9, the human decision diamond in blue #0072B2, and the ship endpoint neutral light gray. Arrows black #000000, single-headed. Blank unannotated flat vector on white, single column.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook figure, 300 DPI, vector, white background, unannotated.
[C - Content] Seven components: claim-and-data input, user-pushback input, primary agent, dissenter agent, consensus detector, ship endpoint, human decision diamond. Preserve the asymmetry: pushback reaches only the primary, never the dissenter.
[O - Organization] Inputs on the left, two agents center-left, consensus detector center-right branching to ship endpoint and to the human diamond; claim-and-data fans to both agents, pushback connects to the primary only.
[P - Presentation] Flat vector, Okabe-Ito — claim-data + dissenter #009E73, pushback #D55E00, primary #E69F00, consensus detector #56B4E9, human diamond #0072B2, ship endpoint light gray, arrows #000000 1pt. No text in image.
[E - Exclusions] No human faces or figures, no chat text, no code, no labels, no speech content, no dashed arrow reaching the dissenter from pushback.
[Note: the absence of any pushback-to-dissenter connection is the figure's central content and must be visually unambiguous.]

### Block 3 — Negative Prompt
human faces, human figures, chat text, code snippets, speech bubbles, any arrow from pushback to dissenter, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 3: Calibration Drift — How One Added Input Silently Voids the Architecture
Priority: Important
Trigger: VG — a structural contrast (intact vs. drifted) where the diagram looks identical except for one added arrow, which is precisely the point text struggles to convey
Figure type: Comparison panels
Concept statement: Feeding the dissenter the pressure signal for "better calibration" leaves the architecture diagram looking intact while both agents converge on the capitulated answer and the human gate never fires.
Reader prior knowledge: Has seen the correct dissenter architecture (Figure 2) and needs to see how a single change defeats it without visible alarm.
Source anchor: Section: 4.3 calibration drift

### Block 1 — Illustrae Paste Block
Draw two side-by-side flat vector comparison panels of identical layout. Each panel shows a compact version of the dissenter system: a pushback input, a primary agent, a dissenter agent, a consensus detector, and a human decision diamond. In the LEFT panel (intact), the pushback connects only to the primary; the consensus detector shows a disagreement and an arrow fires to the human diamond, which is drawn active in green #009E73. In the RIGHT panel (drifted), add one extra arrow from the pushback into the dissenter, drawn prominently in vermillion #D55E00; now both agents agree, the consensus detector shows agreement, and the human diamond is drawn inactive/dark in neutral light gray with no firing arrow. Use five components per panel. Keep the two panels visually identical except for the single added pushback-to-dissenter arrow and the active-versus-dark state of the human diamond. Arrows black #000000 except the offending added arrow in #D55E00. Blank unannotated flat vector on white, single column.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook figure, 300 DPI, vector, white background, unannotated.
[C - Content] Two identical-layout panels each with pushback input, primary agent, dissenter agent, consensus detector, human decision diamond. Preserve that the only differences between panels are one added pushback-to-dissenter arrow and the human diamond's active (left) versus dark (right) state.
[O - Organization] Side-by-side panels, matched component positions; left = intact with active human gate, right = drifted with the extra arrow and a dark gate.
[P - Presentation] Flat vector, Okabe-Ito — active human gate #009E73, offending added arrow #D55E00, dark/inactive gate light gray, agents and detector neutral, standard arrows #000000 1pt. No text in image.
[E - Exclusions] No code, no human faces, no labels, no panel titles, no checkmarks or X marks, no warning icons.

### Block 3 — Negative Prompt
code snippets, human faces, checkmarks, X marks, warning icons, panel titles, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 4: The Approval Gradient — Helpfulness and Sycophancy as One Vector at Two Targets
Priority: Important
Trigger: VG — a conceptual structural claim (one gradient, two outcomes that usually coincide and sometimes diverge) that is hard to hold without a spatial picture
Figure type: Conceptual map
Concept statement: Approval-maximization is a single gradient that points toward both helpful and truthful outcomes when they coincide, but when the user holds a false premise the two diverge and the gradient pulls toward validating the premise.
Reader prior knowledge: Understands RLHF rewards approval; needs the helpful/truthful split made geometric.
Source anchor: Section: 4.4 "Be a helpful assistant" is where sycophancy hides

### Block 1 — Illustrae Paste Block
Draw a flat vector conceptual map shaped like a forking path. On the left, a single origin node labeled by color as the approval gradient, with one thick arrow emerging. The arrow travels right to a fork point. Before the fork, draw the helpful target and the truthful target as two endpoint nodes sitting close together, with the gradient arrow pointing at both — the coincident region. After the fork, in a lower branch, separate the two targets widely: a truthful endpoint and a validate-false-premise endpoint pulled apart, with the approval gradient arrow bending toward the validate-false-premise endpoint and away from the truthful one. Use six components: origin gradient node, fork point, coincident helpful target, coincident truthful target, divergent truthful endpoint, divergent validate-premise endpoint. Color the approval-gradient origin and its arrow in orange #E69F00, the truthful endpoints in blue #0072B2, the helpful coincident target in green #009E73, and the validate-false-premise endpoint in vermillion #D55E00. Arrows black #000000 except the gradient's own pull-arrows in #E69F00. Blank unannotated flat vector on white, single column.

### Block 2 — Full SCOPE Prompt
[S - Specification] Single-column 89mm textbook figure, 300 DPI, vector, white background, unannotated.
[C - Content] Six components: approval-gradient origin, fork point, coincident helpful target, coincident truthful target, divergent truthful endpoint, divergent validate-false-premise endpoint. Preserve that the gradient bends toward validating the false premise when targets diverge.
[O - Organization] Left-to-right forking path: single origin, arrow to a fork, a coincident cluster (helpful + truthful close together) on one branch, a divergent pair (truthful and validate-premise pulled apart) on the other, with the gradient arrow bending toward the validate-premise endpoint.
[P - Presentation] Flat vector, Okabe-Ito — gradient origin and pull-arrows #E69F00, truthful endpoints #0072B2, helpful target #009E73, validate-false-premise endpoint #D55E00, connectors #000000 1pt. No text in image.
[E - Exclusions] No words on nodes, no axis, no equations, no human figures, no labels, no thought bubbles.

### Block 3 — Negative Prompt
words on nodes, axis lines, equations, human figures, thought bubbles, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video Candidate Pass
FIGURE 1 — RLHF capitulation chain: VIDEO CANDIDATE — sequential bias propagation ending in a reversal and an interruption — animating the answer flipping and the isolation bar cutting the chain would dramatize the mechanism, though the static flowchart is sufficient.
FIGURE 2 — Dissenting sub-agent isolation: STATIC SUFFICIENT — the load-bearing content is a fixed connectivity asymmetry — one frame shows what the dissenter is denied; motion adds nothing.
FIGURE 3 — Calibration drift comparison: STATIC SUFFICIENT — the argument is a side-by-side structural contrast — static panels make the single-arrow difference legible at a glance.
FIGURE 4 — Approval gradient fork: STATIC SUFFICIENT — a conceptual geometry of coincidence and divergence — grasped in one fixed view.

Recommendation: Render all four as static figures; Figures 1 and 2 are Critical and load-bearing for the chapter's mechanism and fix, Figures 3 and 4 are Important conceptual reinforcements. No video required; Figure 1 is the only mild animation candidate.
