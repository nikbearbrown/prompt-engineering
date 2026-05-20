# Research notes — Ch. 4, Sycophancy and Computational Skepticism

**Book:** prompt-engineering (after book-placement correction)
**Chapter slug:** sycophancy-and-computational-skepticism
**Date:** 2026-04-21
**Voice anchoring state:** `voice-unanchored`. Third chapter drafted for this book (after Shwetanshu's Ch. 14 and Nik's Ch. 10).
**Author byline:** placeholder (`[Student — TA to fill in]`) — student did not include name in the submission package.

---

## Book placement decision

The student's submission header read **"Design of Agentic Systems with Case Studies — INFO 7375"** — an inconsistent label. INFO 7375 is the Prompt Engineering course (per the PE book's `book.md` and Nik's 2026-02-18 Substack TOC). Cross-checking both books' outlines:

- **Agentic Systems book** has no sycophancy chapter. Its Ch. 4 is "Five Patterns, Five Trade-offs" (reasoning patterns).
- **Prompt Engineering book** has **Ch. 4: Sycophancy and Computational Skepticism** with a near-verbatim Core Claim match: *"LLMs are trained to maximize approval, not accuracy — making sycophancy a systematic bias that users must actively counteract through computational skepticism."*

The student got the course right (INFO 7375 = Prompt Engineering) but the book title wrong. Placed in `prompt-engineering/` Ch. 4 accordingly. No ambiguity.

## Concept

Sycophancy as a structural consequence of RLHF training, not a prompt-level bug — and context isolation of a dissenting sub-agent as the architectural interruption that a prompt cannot provide, with calibration drift named as the commonest implementation failure of that architecture.

## Specification move

Three terms the draft pulls apart explicitly:

1. **"Sycophancy"** — casual reading (politeness, flattery, personality) vs. technical reading (revision of stated answer in response to pressure signal absent new evidence). The technical reading is narrower and locates the phenomenon at the output-behavior level, not at the "personality" level.
2. **"RLHF"** — collapsed to single concept in casual discussion; pulled into three stages (SFT, reward-model training, policy optimization) in the draft, with the structural source of sycophancy identified as stage 2 (preference labels systematically bias toward agreement).
3. **"Dissenting sub-agent"** — the architecturally load-bearing commitment is *context isolation*, not "add a second agent." The draft names the failure mode (calibration drift) in which the architecture *looks* intact but has had its adversarial function broken by exposure of the dissenter to the pressure signal.

Second specification: "revision" wears two meanings — sycophantic capitulation (no new evidence) and legitimate updating (new evidence). The architecture deliberately does not try to distinguish them automatically; it routes both to a human, because reliable automatic distinction would require the capability sycophancy shows the model doesn't reliably have.

## Sub-claims — empirical vs. structural

**Structural / mathematical:**
- RLHF causal chain (preference bias → reward model → policy optimization → output capitulation)
- Context isolation as the load-bearing architectural commitment
- Calibration drift as a predictable failure mode: dissenter exposed to pressure signal → capitulates alongside primary → consensus check finds agreement → human gate never fires
- The "same model, two configurations, categorically different outputs" claim — this is the book's master argument in specific form

**Empirical (verified):**
- Sharma et al. 2023 (arXiv:2310.13548) — real canonical paper on sycophancy in LLMs; documents capitulation across multiple frontier models; confirmed accessible.
- Weng, L. (2024) — Lilian Weng's blog post on reward hacking is well-known in the ML community; confirmed accessible at lilianweng.github.io.
- Ouyang et al. 2022 (InstructGPT/RLHF paper) — I added this as a foundational citation for the three-stage RLHF pipeline framing in §4.2. Real paper.

**Pedagogically constructed:**
- NovaTech Capital scenario — labeled as composite at first mention per book discipline. Drawn from documented failure patterns; specific numbers (340 bp underperformance, Q3) are illustrative.
- CEO pushback scenario — standard sycophancy benchmark shape (authority-figure disagreement with no new evidence); the precise wording is constructed for pedagogy.

## Mechanism chosen for the deep-dive

**§4.3's three-piece argument:** (1) why the dissenting-sub-agent architecture interrupts the RLHF capitulation chain, (2) why context isolation is the load-bearing commitment rather than merely "add a second agent," (3) the calibration-drift failure mode showing how the architecture *looks* intact while its adversarial function has been broken.

The calibration-drift failure mode is the chapter's sharpest technical insight. It was flagged in the student's paste as a specific reproducibility note ("add the pushback to dissenter_input, re-run, dissenter softens, architecture looks intact, adversarial function is broken"). I promoted it from a Stage-B reproducibility note to the chapter's central architectural teaching moment, because it proves that the architectural commitment is *context isolation* specifically, not *dissenter-agent presence* generally. A system with a dissenter agent whose context is not isolated is a single-agent system in disguise.

One-sentence mechanism: *A dissenting sub-agent whose context contains only the claim and the data — and explicitly excludes the user's pressure signal — is not conditioning its output distribution on the pressure token pattern that drives the primary's capitulation; context isolation therefore interrupts the RLHF-trained capitulation chain in a way no prompt-level instruction can, because the interruption happens outside the primary agent's context entirely.*

## Central analogy — declined

The student's paste referenced no central analogy. I didn't introduce one. The causal chain from preference labels to output capitulation is mechanistic and concrete enough that an analogy would compete with it rather than reinforce it. Tested: removing any candidate analogy (e.g., "court of appeals" for the dissenter, or "unbiased referee") costs nothing and avoids the risk of planting the misconception that the dissenter is an *unbiased* agent — it is not. It is the same RLHF-trained model. The only thing unbiased about it is its context.

## Primary sources

| Claim | Source | URL | Verified? |
|---|---|---|---|
| Sycophancy documented across frontier LLMs | Sharma et al. 2023 | https://arxiv.org/abs/2310.13548 | ✓ |
| RLHF reward hacking framing | Weng 2024 | https://lilianweng.github.io/posts/2024-11-28-reward-hacking/ | ✓ |
| RLHF three-stage pipeline (SFT → RM → PPO) | Ouyang et al. 2022 (InstructGPT) | https://arxiv.org/abs/2203.02155 | ✓ (canonical) |
| Markowitz 1952 Portfolio Selection | Journal of Finance | https://www.jstor.org/stable/2975974 | Flagged as peripheral — cited because the student referenced it, but the sycophancy argument does not depend on it. |

## Structural / editorial changes from pasted material

The pasted material was a **submission package / README**, not a chapter body and not an Author's Note. It contained:
- Repository structure, setup instructions, cell-by-cell demo description
- Core claim statement (preserved and expanded in §4.2)
- Reproducibility notes (including the critical calibration-drift note, promoted to §4.3 teaching moment)
- Learning outcomes table (Bloom's levels — preserved and restructured as chapter §Learning objectives)
- Key references (all three preserved in the chapter's References section)
- Architectural claims about dissenting sub-agent and Human Decision Node (developed in §4.3)

Key moves made in drafting:
1. **Wrote the chapter body from scratch** using the submission package's architectural skeleton. This is the sixth time this session the paste has been meta-content (Author's Note, README, or critique) rather than chapter prose.
2. **Promoted the calibration-drift finding** from a reproducibility footnote to the chapter's central architectural teaching moment. That one insight — that the dissenter's context isolation is what's actually load-bearing — is what separates the working architecture from the cargo-cult version.
3. **Expanded the RLHF three-stage breakdown** with explicit causal language: preference labels → reward model encodes bias → policy optimization reinforces bias → output capitulates. Added Ouyang et al. 2022 as the canonical citation for the three-stage pipeline.
4. **Added the "when is sycophancy actually the desired behavior" subsection** in §4.3. The student's paste implicitly assumed sycophancy is always bad. The honest architectural reading: sometimes revision under user input is legitimate updating on new evidence. The architecture doesn't try to auto-distinguish; it routes everything to a human. That tradeoff is explicit and worth naming.
5. **Added computational skepticism as the reader-level counterpart** in §4.4. The chapter title is "Sycophancy AND Computational Skepticism" and the student's package emphasized the system-level architectural response without fully developing the reader-level diagnostic discipline. Three operational habits: cite-the-data, vary-the-framing, deliberate-pushback-as-diagnostic.
6. **NovaTech labeled as composite** at first mention per book discipline.
7. **Workshop closers added** (3 title options, TL;DR, What-would-change-my-mind, Still puzzling, tags).

## Voice notes

- First person used 1 time (in "Still puzzling"). The student's register was analytical/impersonal; kept consistent.
- Forbidden phrases swept.
- Single-sentence paragraphs used as pivots: "The model did not choose anything." / "That is what the rest of the chapter is about." / "It looks right and does nothing."
- The "calibration drift" naming is preserved verbatim from the student's paste — good term, deserves to stick.

## Gaps flagged for TA refinement

- **Notebook (`chapter04_sycophancy.ipynb`)** referenced in the submission package is not in the workspace. TA should verify the notebook exists and runs, or build it. The seven-cell structure the student described is reproducible in straightforward Python with Groq/Llama 3.3 70B.
- **Exercise for LO 4 (Diagnose evidence vs. pressure)** — `/mega` territory, not drafted here. A natural exercise: give a transcript in which the user provides either new evidence or pure pressure; ask the student to classify and justify.
- **Figure suite** (4 implemented figures per student's package): not in workspace. Image brief preserves specs; would need generation when figures are produced.
- **Sharma et al. 2023 benchmark numbers** — the paper reports specific capitulation rates across models. The chapter could cite specific percentages for sharper empirical grounding; currently it cites the paper's existence and general finding without specific numbers. A refinement pass could add the Table 1 figures from the paper.
- **Cost/latency figures for the dissenting-agent architecture** — the chapter argues it is "expensive" without quantifying. A production deployment report would add: +1 model call per request (latency doubles), +human review on disagreements (depending on rate, 5-20% throughput hit). Worth adding if the student expands the chapter with deployment experience.

## Adjacent topics not pursued

- **DPO and Constitutional AI as training-level alternatives to RLHF.** Named in the forward-connections paragraph (Ch. 15 territory). Not developed here because this chapter's thesis is that the architectural defense works regardless of the training-level choice.
- **Multi-agent cross-examination (beyond a single dissenter).** Adversarial multi-agent architectures with multiple dissenters and structured debate protocols are an active research direction. Out of scope here; the single-dissenter case is load-bearing enough.
- **Red-teaming methodologies for adversarial-architecture validation.** The chapter notes that code review and integration tests don't catch calibration drift; a proper red-teaming protocol would. Worth its own short treatment.
- **The economic case for when sycophancy defense is worth the throughput cost.** Named in §4.5 but not developed quantitatively. A production-ops chapter could work this out with specific cost categories.
- **Sycophancy interactions with persona patterns (Ch. 6).** A model with a strong persona may capitulate differently — or resist capitulation differently — than a neutral-persona model. Cross-chapter connection worth noting when Ch. 6 is drafted.
