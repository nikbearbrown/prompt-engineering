# Hero image brief — Ch. 6, Persona Patterns

**Book:** prompt-engineering
**Chapter slug:** persona-patterns
**Date:** 2026-04-21

## Concept the image should carry

The chapter's load-bearing visual claim is **the swap test** — showing that two superficially similar prompts produce categorically different outputs from the same model. A reader looking at the image for thirty seconds should see: (1) two prompts that differ only in who-is-characterized, (2) two outputs that differ categorically in who they serve, (3) the combined pattern as the architectural win that bounds both single-pattern failure modes.

## Primary recommendation — the swap-test three-column comparison

A single-panel figure with three columns, each showing a prompt→output pair on the same topic (elastic vs. plastic deformation, say, or fracture analysis).

**Column 1 — Persona Pattern only.** Header: *"You are a first-year undergraduate..."* Output below: visibly uncertain, simplified, possibly incorrect — rendered with visual markers of weak confidence (incomplete sentences, hedge language).

**Column 2 — Audience Persona Pattern only.** Header: *"Explain to a first-year undergraduate..."* Output below: accurate, accessible, scoped to the reader's decision context.

**Column 3 — Combined Pattern.** Header: *"Act as a senior metallurgist. Explain to a maintenance supervisor who must decide whether to ground an aircraft fleet."* Output below: accurate, decision-relevant, appropriately scoped.

Under each column, a small annotation naming the failure mode that column avoids (Col 1: simulates limited knowledge → may be incorrect; Col 2: retains expertise but loses expert authority cues; Col 3: retains both with audience constraint acting as protective bound).

**Critical visual move:** all three columns run on the *same base model* — labeled explicitly in a header above the figure: *"Same model. Same temperature. Only the prompt architecture differs."*

This is the book's master argument in one figure.

## Secondary recommendation — the four failure modes causal chains

A 2×2 matrix, one cell per failure mode. Each cell shows a minimal causal chain from design decision to observed symptom:

- **Drift:** single system prompt → attention dilution over conversation length → persona directive loses salience → output converges to default assistant register
- **Mismatch:** persona specified, audience not → model infers audience from persona → expert persona assumes expert audience → output technically correct, operationally useless
- **Hallucination:** expert persona assigned in narrow domain → confident generation patterns activate without knowledge activation → confident assertions that are factually wrong
- **Bleeding:** multi-agent with free-form communication → inter-agent context contaminates persona scope → one agent's positions leak into another's outputs

All four cells share visual language: same causal-arrow style, same color coding (muted teal for design decision, muted ochre for mechanism, muted slate for symptom). The parallel structure makes the chapter's classification claim visible — these *are* four distinct mechanisms, not four flavors of the same failure.

## Tertiary recommendation — the diagnostic protocol as a flowchart

A decision tree rendering of the five-step diagnostic protocol. Starting node: *"Persona-based system producing degraded output."* Five decision points branching to candidate failure modes. Each branch labeled with the test that differentiates ("run as single-turn", "check prompt for audience spec", "run agent in isolation"). Terminal nodes identify the most-likely failure mode plus the chapter section with mitigation guidance.

This turns the protocol from a prose procedure into a visual decision aid that students can consult during live diagnosis.

## Style direction

Per `book.md` voice notes: engineering-diagram aesthetic. Muted academic palette. No anthropomorphic imagery — the Persona Pattern is not a "mask the AI wears" and the Audience Persona Pattern is not a "lens the AI looks through." Both are architectural configurations of the prompt-input layer; render them as structural diagrams, not as costumed figures or characters.

Three colors used consistently across all three figures:
- **Muted teal** — Persona Pattern elements (speaker-side configuration)
- **Muted ochre** — Audience Persona Pattern elements (reader-side configuration)
- **Muted slate** — neutral content (model, output, structural arrows)

The visual parallel across figures lets readers recognize "the same thing" in different contexts — which matters because the chapter's classification claim depends on these patterns being genuinely distinct.

## Aspect ratio

- Primary (three-column swap test): very wide (21:9) — three panels side-by-side need horizontal room
- Secondary (2×2 failure modes): square (1:1)
- Tertiary (diagnostic flowchart): tall (3:4 or 2:3) — decision trees flow vertically

## Do NOT

- Generate any of these in this run.
- Render the Persona Pattern or Audience Persona Pattern as human silhouettes (a "metallurgist" figure, a "maintenance supervisor" figure, etc.). Both are structural prompt configurations; rendering them as people suggests they're identities the model "becomes" or "sees," which is the mechanistic misunderstanding the chapter is built to prevent.
- Use masks, mirrors, or reflection metaphors for the two patterns. These metaphors all imply "the AI puts on a persona" or "the AI sees a reader" — both anthropomorphic and both mechanistically wrong.
- Label the three swap-test outputs as "bad/better/best." The Persona-only and Audience-only outputs aren't *bad*, they're differently scoped. Use neutral descriptive labels (scoped-to-persona / scoped-to-audience / scoped-to-both).
- Add a "drift curve" line graph showing persona consistency over conversation length unless the notebook data backs it with real numbers. A figure based on heuristic scoring that the student's self-assessment already flagged as limited would underrepresent the finding's reliability.
- Omit the "same model" annotation on the swap-test figure. That annotation *is* the chapter's argument made visible — without it, a reader might infer that the three columns used different models.
