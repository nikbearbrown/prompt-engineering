# Research notes — Ch. 6, Persona Patterns

**Book:** prompt-engineering
**Chapter slug:** persona-patterns
**Date:** 2026-04-21
**Voice anchoring state:** `voice-unanchored`. Fourth chapter drafted for this book.
**Author byline:** **Niraj Patel** (sixth named-student chapter of the session).

---

## Book / numbering placement

- **Book:** Prompt Engineering — confirmed by student's Author's Note header and exact match to PE book outline's core claim.
- **Chapter number:** Student labeled as **Ch. 12**; PE book outline places Persona Patterns at **Ch. 6** ("Shaping Who the Model Is and Who It Speaks To"). Placed at Ch. 6 per the outline's verbatim core-claim match. Flagged for editor — if the student has a reason to believe Ch. 12 is correct, the outline may need reconciliation, but the content matches Ch. 6 identically and there's no Ch. 12 slot in the PE book's 20-chapter structure that fits Persona Patterns.

## Length compression

Student draft: ~8,000–10,000 words in the paste. Workshop ceiling: 4,000 words. Compressed to ~4,000 by the following cuts:

1. **Agentic architectures section cut entirely** (CrewAI, AutoGen, LangGraph, MetaGPT feature comparisons). Student's own self-assessment acknowledged this section remained "feature-list-heavy" despite editor review. Also overlaps with Ch. 11 (Prompt Stack) territory in the PE book and with Ch. 11 (Choosing Your Weapon — drafted by Rahul Manohar) in the agentic-systems book. Cross-referenced from §6.4 bleeding section to those chapters rather than reproducing.
2. **Turbine Blade case study cut.** The fracture-analysis opening scenario does the same architectural teaching; a second multi-agent case study was redundant to the chapter's core point.
3. **Four failure modes compressed** from multi-paragraph treatments to structural summaries (definition / mechanism / symptom / mitigation in one pass per failure mode). Most of the student's forensic detail moved to the `/mega`-destined exercises.
4. **Six exercises pulled** for `/mega` per workshop convention.
5. **Some redundant prose in the summary** folded into §6.6's closing.

What was preserved verbatim: the fracture-analysis opening scenario, the White et al. vs. Vanderbilt companion-site publishing-gap observation, the swap-test example (Prompt A vs. Prompt B elastic/plastic deformation), the Kong et al. numerical findings, the Zheng et al. 162-persona study, the "Audience Persona as protective constraint" insight, the diagnostic-protocol five steps, the PRISM MMLU degradation claim (with `[verify]`), the central closing refrain about the fractured turbine blade.

## Concept

Two prompt patterns — Persona and Audience Persona — that are superficially similar but mechanistically distinct, with four documented failure modes (drift, mismatch, hallucination, bleeding), a five-step diagnostic protocol, and the architectural insight that combining them produces mutual constraint (the audience persona bounds the expert persona's excesses).

## Specification move

Three terms the chapter pulls apart:

1. **"Persona"** — casual reading (personality, voice) vs. technical reading (an identity assigned to the model's output generator vs. an identity assigned to the model's inferred reader). Without this distinction, the whole chapter is noise.
2. **"Audience adaptation"** — casual reading (simplification, tone-shifting) vs. technical reading (information filtering — the audience persona causes the model to *suppress* details inferred not-relevant-to-the-audience, which is the underappreciated risk).
3. **"Persona drift"** — casual reading (the model "forgets" its persona) vs. technical reading (attention dilution as conversation history grows, reducing the system prompt's relative attention weight). Niraj flagged the anthropomorphic "forgets" framing in his Author's Note as something he corrected in Bookie's draft; preserved the mechanistic framing.

## Sub-claims — empirical vs. structural

**Structural / architectural:**
- Persona and Audience Persona as distinct patterns
- Combined Pattern as architectural superior to either alone
- Audience Persona as protective constraint on Persona excess
- Drift mechanism via attention dilution
- Mismatch mechanism via audience-inference-from-persona default
- Hallucination mechanism via activating confident-communication patterns without activating knowledge patterns
- Bleeding mechanism via inter-agent contamination pathways (conformity, confabulation, impersonation)
- Five-step diagnostic protocol

**Empirical (primary-source cited, mostly verified):**
- White et al. 2023 (arXiv:2302.11382) — pattern catalog. Real and well-cited.
- Kong et al. 2023 (arXiv:2308.07702) — role-play prompting cross-scale improvements. Real paper; numerical claims (AQuA 53.5%→63.8%, LLC 23.8%→84.2%) are from this paper and verifiable.
- Zheng et al. 2023 (arXiv:2311.10054) — 162 personas, 2,410 questions, no improvement on factual recall. Real paper.
- PRISM study MMLU 71.6%→66.3% — flagged `[verify]`. I'm less certain about this specific citation; the student cited it as "PRISM study" without arXiv ID. Could be real; could be misremembered. A TA refinement should locate the exact citation or soften the numerical claim.
- Li et al. persona drift self-consistency metric (>30% degradation by turns 8–12) — flagged `[verify]`. The claim is plausible and consistent with well-documented attention-decay behavior, but I couldn't verify the specific study without more detail.
- Williams' "epistemic drift" taxonomy — flagged `[verify]`. Could not verify from the student's reference alone.
- "3% impersonation rate in multi-agent systems" — flagged `[verify]`. Specific enough that it comes from a specific study; student didn't cite exactly.
- ExpertPrompting (Xu et al. 2023, arXiv:2305.14688) — real paper on detailed vs. generic personas.
- "ELI5 causes information suppression" — flagged `[verify specific citation]`. Well-known effect, but the student didn't name the study.

**Pedagogically constructed:**
- The fracture-analysis scenario (metallurgist / maintenance supervisor / fatigue vs. overload / aircraft fleet) — labeled as composite at first mention per book discipline.

## Mechanism chosen for the deep-dive

**The swap test** as the experimental demonstration that Persona Pattern and Audience Persona Pattern are mechanistically distinct (§6.2), followed by the **Audience Persona as protective constraint** architectural insight (§6.3). This is the chapter's sharpest load-bearing teaching moment — it shows that the combined pattern isn't "two patterns used together" but "one pattern architecturally bounding the other's failure mode."

One-sentence mechanism: *The Persona Pattern activates expert-associated generation patterns (vocabulary, confidence, register) that include a default assumption the audience is also expert; pairing it with an explicit Audience Persona Pattern forces the model to retain expertise while adapting communication for the specified non-expert audience — which is architecturally why combined prompts work better than either single-pattern variant, not merely because they contain more information.*

## Central analogy — declined

The student's draft didn't use a central analogy. I didn't add one. The swap test and the four failure modes are concrete enough to carry the argument without metaphor.

## Primary sources

| Claim | Source | URL | Verified? |
|---|---|---|---|
| Prompt pattern catalog (Persona Pattern) | White et al. 2023 | https://arxiv.org/abs/2302.11382 | ✓ |
| Role-play prompting across scales | Kong et al. 2023 | https://arxiv.org/abs/2308.07702 | ✓ |
| Personas don't improve factual recall | Zheng et al. 2023 | https://arxiv.org/abs/2311.10054 | ✓ |
| ExpertPrompting (detailed vs. generic personas) | Xu et al. 2023 | https://arxiv.org/abs/2305.14688 | `[verify]` |
| PRISM MMLU degradation | (student-cited as "PRISM study") | — | `[verify]` |
| Li et al. persona drift (>30% degradation at turn 8–12) | (student-cited, no arXiv) | — | `[verify]` |
| Williams' epistemic drift taxonomy | (student-cited) | — | `[verify]` |

## Structural / editorial changes from pasted material

1. **Severe length compression** — 8K–10K words → ~4K. See "Length compression" above.
2. **Chapter number corrected** — placed at Ch. 6 per outline, not Ch. 12 as student labeled.
3. **Framework comparison cut** — CrewAI / AutoGen / LangGraph / MetaGPT feature lists removed. Cross-referenced to Ch. 11 (Prompt Stack) and to the agentic-systems book's Ch. 11.
4. **Failure mode sections compressed** from multi-paragraph-per-mode to structural summaries.
5. **Six exercises pulled** for `/mega`.
6. **Workshop closers added** — three title options, TL;DR, What-would-change-my-mind, Still puzzling, tags.
7. **Fracture analysis scenario labeled as composite** at first mention per book case-study discipline.
8. **Preserved Niraj's Human Decision Node finding** (rejection of the AI-proposed Design B because it used Persona without Audience Persona — exactly the conflation the chapter is built to prevent) — referenced in the research notes but not in the chapter body, where it would be Author's-Note content.

## Voice notes

- First person used twice (in "What would change my mind" and "Still puzzling"). Consistent with the book's mechanism-first, opinion-labeled register.
- Forbidden phrases swept.
- Single-sentence paragraphs at pivots: "These are not the same instruction." / "The model doesn't change. The architecture does." / "Persona is not a stylistic convenience."
- The chapter's closing refrain ("The fractured turbine blade doesn't care whether the AI sounded like an expert. It cares whether the maintenance supervisor understood the warning.") is preserved verbatim from the student — it's genuinely strong.
- Niraj's mechanistic correction to Bookie's anthropomorphic drift framing ("forgets") is preserved in §6.4's drift mechanism.

## Gaps flagged for TA refinement

- **Multiple `[verify]` citations** — PRISM study, Li et al. drift paper, Williams' taxonomy, ExpertPrompting arXiv ID, ELI5 information-suppression citation, multi-agent impersonation-rate figure. Six specific claims that a TA should lock down or soften before publication.
- **The notebook** referenced in Niraj's Author's Note (persona drift experiment with 47% degradation, readability-metric swap test, Mandatory Human Decision Node) is not in the workspace. TA should verify it exists or build it; the drift experiment in particular is pedagogically valuable if the scoring function can be trusted.
- **Heuristic scoring function** — Niraj's self-assessment acknowledges the persona consistency scoring uses keyword heuristics rather than embedding-based semantic similarity. A production-quality version would use cosine similarity between response embeddings and a persona-baseline embedding. Worth upgrading if the notebook becomes the chapter's experimental backbone.
- **Agentic framework discussion** — cut entirely from chapter body. If a future revision wants to include a summary, cross-reference to Ch. 11 (Prompt Stack) in PE book and Rahul Manohar's Ch. 11 in the agentic-systems book, both of which cover the framework comparison with the appropriate depth for their respective books.
- **Turbine Blade case study** — cut. If the student wants it preserved, it would fit as a Part VI case study in the PE book (when Part VI starts receiving student case-study submissions) rather than inline in Ch. 6.

## Adjacent topics not pursued

- **Multi-agent persona design** at depth — deferred to Ch. 11 and to the agentic-systems book's multi-agent chapters.
- **Persona consistency scoring** as a production monitoring practice — worth a sidebar or appendix; the chapter gestures at it via the diagnostic protocol but doesn't develop the metric.
- **Persona interactions with sycophancy** — strong personas may interact with RLHF capitulation in specific ways that Ch. 4 doesn't cover. Worth a short follow-up cross-reference once both chapters are stable.
- **Persona effects under different temperature / sampling settings** — the behavioral effects documented in the chapter are from default sampling. Persona under aggressive sampling (high temperature, top-p) may behave differently.
- **Persona drift as a security surface** — the adversarial version of drift, where a user deliberately pushes a system off its persona. Relates to Ch. 4 sycophancy and to the agentic-systems book's Ch. 18 Attack Surface chapter.
