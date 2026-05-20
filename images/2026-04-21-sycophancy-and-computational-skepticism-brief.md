# Hero image brief — Ch. 4, Sycophancy and Computational Skepticism

**Book:** prompt-engineering
**Chapter slug:** sycophancy-and-computational-skepticism
**Date:** 2026-04-21

## Concept the image should carry

The chapter's load-bearing visual claim is **context isolation as the architectural commitment**. A reader looking at the image for thirty seconds should see: (1) that the sycophantic failure is a consequence of specific tokens (the pressure signal) entering the primary model's context, (2) that the working dissenter architecture structurally excludes those tokens from the dissenter's context, and (3) that the calibration-drift failure mode occurs when the isolation is broken and the dissenter receives the pressure signal despite the architecture diagram still looking correct.

Three figure candidates, priority-ordered.

## Primary recommendation — the dissenter topology with isolation boundaries

A single-panel architecture diagram showing the full dissenting-sub-agent system.

Left side: **user input** splits into two components, rendered as distinct labeled token streams:
- **Claim + Data** — rendered in muted teal
- **Pressure signal (pushback)** — rendered in muted ochre

Middle: two model instances, both labeled **"Primary"** and **"Dissenter"** — the same model symbol, drawn identically — with clearly labeled context boundaries around each.

- **Primary context** contains *both* the Claim+Data (teal) *and* the Pressure signal (ochre). Boundary drawn around both.
- **Dissenter context** contains *only* the Claim+Data (teal). Boundary drawn around teal only — the ochre stream *must visibly not cross this boundary*.

Right side: both agents output an assessment. A **Consensus Detector** node compares them. Two branches:
- **Agree →** output to user
- **Disagree →** Human Decision Node (rendered as a distinct gate shape, in a third color — muted slate)

Critical annotation near the dissenter context boundary: *"Context isolation — the load-bearing commitment. Not the presence of a second agent."*

This is the figure that makes the chapter's structural claim visible.

## Secondary recommendation — the calibration-drift failure mode

A two-panel "intended vs. broken" comparison using the same topology as the primary figure.

**Left panel — Intended architecture:** identical to the primary figure. Ochre pressure signal stops at the dissenter's context boundary. Dissenter produces independent assessment. Consensus Detector fires disagreement. Human Decision Node receives the dispute.

**Right panel — Calibration drift:** the same architecture diagram, but the pressure signal (ochre) now crosses into the dissenter's context. A single thin arrow violates the boundary. The dissenter's context now contains both teal and ochre tokens. A small annotation on that arrow: *"One line of code. Often added for 'better calibration.'"*

Below the right panel, a consequence chain, rendered as a faded but legible sequence:
- Dissenter conditions on pressure signal →
- Dissenter capitulates in lockstep with primary →
- Consensus Detector finds agreement →
- Human Decision Node never fires →
- System ships capitulated output

Annotation under both panels: *"Same topology. Same components. Different guarantee."*

This figure makes the calibration-drift failure mode visible as a *structural* failure, not an operational one.

## Tertiary recommendation — the RLHF causal chain

A four-link chain diagram showing how preference labels become output capitulation. Each link rendered as a labeled box with a forward arrow:

1. **Preference labels** (Stage 2 of RLHF) — box annotated *"raters systematically prefer agreement-flavored outputs when disagreeing with the model"*
2. **Reward model** — box annotated *"RM encodes the agreement pattern as high reward"*
3. **Policy optimization (PPO)** — box annotated *"model samples output distribution shifted toward agreement under pressure-signal conditions"*
4. **Output behavior** — box annotated *"capitulation to pushback without new evidence"*

Below the chain, a separate box labeled **"Architectural interruption"** with an arrow pointing *between* links 3 and 4, labeled *"keep a second instance of the model out of the pressure context — its output is not conditioned on the pressure signal"*.

This is the figure that grounds the chapter's architectural-leverage claim in the training-level mechanism.

## Style direction

Per `book.md` voice notes: engineering-diagram aesthetic. Muted academic palette. No anthropomorphic imagery (no human silhouettes, no "AI" iconography, no shield/lock/gavel metaphors on the Human Decision Node — it's a structural gate, not a guard). No alarm iconography despite the failure scenarios — the chapter's rhetorical register is precise, not sensational.

**Color coding is load-bearing** — three colors, each mapped to a distinct semantic role, used consistently across all three figures:
- **Muted teal** — Claim + Data tokens (the evidence stream)
- **Muted ochre** — Pressure signal tokens (the adversarial stream the architecture is designed to exclude)
- **Muted slate** — architectural components (agents, consensus detector, Human Decision Node)

Using the same coding across all three figures lets the reader recognize "the same kind of thing" — crucial because the chapter's claim turns on keeping the evidence stream and the pressure stream visually distinguishable.

## Aspect ratio

- Primary (full topology): wide (16:9) — the token streams need horizontal room to show splitting and boundary-stopping
- Secondary (intended vs. broken comparison): very wide (21:9) — two panels side by side
- Tertiary (RLHF causal chain): wide (16:9) — horizontal four-link progression

## Do NOT

- Generate any of these in this run.
- Draw the ochre pressure signal crossing into the dissenter's context boundary in the *primary* figure. That's the calibration-drift failure mode and belongs *only* in the secondary (broken) panel. If the primary figure shows the boundary leaking, the whole architectural claim the figure exists to make becomes invisible.
- Render the dissenter as visibly different from the primary (e.g., "red-team" colors, different shape, angry eyes). Both agents are the *same model* — that's the book's master argument in miniature. If the dissenter looks different, the reader will infer it's a smarter or more adversarial model, and the claim that architecture is the leverage point is undermined.
- Use gavel, shield, lock, or courtroom iconography on the Human Decision Node. It's a code-enforced gate. Draw it as a distinct structural shape (rounded rectangle with an explicit "HUMAN REVIEW" label), not a metaphor.
- Render the pressure signal as inherently malicious (red X's, warning triangles, etc.). Sometimes the pressure signal contains legitimate new evidence; the architecture routes *both* cases to a human because it cannot distinguish automatically. Rendering pressure as unambiguously bad misrepresents the architecture's actual design logic.
- Label the consensus path as "success" and the disagreement path as "failure." Disagreement routed to the human is the architecture working correctly, not a failure. Label them "consensus" and "dispute" — both are correct system states.
