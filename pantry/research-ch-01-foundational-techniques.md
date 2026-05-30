# Research: Candidate Chapter §1 — Foundational Techniques: What the Research Actually Shows
## Prompt Engineering
**Chapter one-line:** What the research actually shows about CoT, few-shot, persona, formatting, and base vs instruction-tuned models.
**Research date:** 2026-05-29

---

## 1. Primary Sources

### Foundational papers and texts

1. **Wei, J., Wang, X., Schuurmans, D., Bosma, M., Ichter, B., Xia, F., Chi, E., Le, Q., & Zhou, D. (2022). "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models."** *Advances in Neural Information Processing Systems 35 (NeurIPS 2022)*, Main Conference Track. arXiv:2201.11903 (submitted 28 Jan 2022).
   - The origin of few-shot CoT prompting: supplying a handful of exemplars whose answers include intermediate reasoning steps. The headline empirical claim is that the benefit is **emergent with scale** — prompting a 540B-parameter PaLM with eight CoT exemplars reached state-of-the-art on GSM8K, while small models gained little or got worse. This is the chapter's anchor for "the technique works, but only under stated conditions" — exactly the falsifiable, mechanism-bounded framing the book wants.

2. **Kojima, T., Gu, S. S., Reid, M., Matsuo, Y., & Iwasawa, Y. (2022). "Large Language Models are Zero-Shot Reasoners."** *NeurIPS 2022* (Adv. NeurIPS 35:22199–22213). arXiv:2205.11916.
   - **Added beyond the spine.** Shows that simply appending "Let's think step by step" (zero-shot, no exemplars) lifts text-davinci-002 on MultiArith from 17.7% → 78.7% and GSM8K from 10.4% → 40.7%. This is the cleanest separation of *the reasoning trace* from *the exemplars*: it isolates the mechanism (eliciting a reasoning trajectory) from the few-shot scaffolding of Wei et al. Essential for a chapter that distinguishes zero-shot from few-shot.

3. **Wang, B., Min, S., Deng, X., Shen, J., Wu, Y., Zettlemoyer, L., & Sun, H. (2023). "Towards Understanding Chain-of-Thought Prompting: An Empirical Study of What Matters."** *ACL 2023* (Long Papers). arXiv:2212.10001.
   - The mechanism paper. Demonstrates that prompting with **invalid** reasoning steps still recovers 80–90% of valid-CoT performance, and that **relevance to the query** and **correct ordering of steps** matter far more than the factual correctness of the rationale. This is the chapter's strongest "evidence over intuition" beat: CoT is not (mostly) about the model following true logic — it is about conditioning the decoding trajectory into a plausible step-shaped manifold.

4. **Wang, X., & Zhou, D. (2024). "Chain-of-Thought Reasoning Without Prompting."** *NeurIPS 2024* (Google DeepMind). arXiv:2402.10200.
   - Shows CoT-style reasoning paths can be **elicited by decoding alone** — inspecting top-k alternative first tokens rather than greedy decoding surfaces latent reasoning paths already present in the pretrained model. CoT-decoding yields +10–30 point absolute GSM8K gains across the PaLM-2 family. Directly serves the book's mechanism-first thesis: the "reasoning" is a property of the *output distribution*, not the prompt string, and a sampling/decoding choice can substitute for a prompt.

5. **Meincke, L., Mollick, E. R., Mollick, L., & Shapiro, D. (2025). "Prompting Science Report 2: The Decreasing Value of Chain of Thought in Prompting."** Wharton Generative AI Labs / SSRN abstract 5285532. arXiv:2506.07142 (8 Jun 2025).
   - The "when it stops helping" beat. For non-reasoning models CoT gives small average gains; for reasoning-tuned models the gains are marginal and CoT **adds answer-to-answer variance**, sometimes flipping otherwise-correct answers. Crucial for a decision procedure: the chapter can state *when to stop adding "think step by step"* rather than treating it as universally good.

### Key empirical cases

- **GSM8K math word problems (documented, primary).** The recurring benchmark across Wei, Kojima, and Wang & Zhou. Concrete worked-example anchor: a problem the base model gets wrong under greedy/direct answering but right once a reasoning trajectory is elicited (by exemplars, by "let's think step by step," or by top-k decoding). All three mechanisms can be shown side-by-side on one GSM8K item. *Documented, not hypothetical.*
- **"A helpful assistant" default system prompt (documented).** Zheng et al. (2024, below) note that commercial systems ship persona system prompts (ChatGPT's "You are a helpful assistant") despite no measured factual benefit — a real, shipping practice the chapter can interrogate. *Documented.*
- **Gemini low-temperature looping (documented).** Google's own Gemini 3 API guidance recommends keeping temperature at the default 1.0 because lowering it can cause looping/degradation on reasoning tasks; multiple Gemini 2.5 production incidents (Jan 2026) show infinite repetition loops. A live, model-specific counterexample to the folk rule "always use temperature 0." *Documented.*

---

## 2. The Core Concept — State of the Field

### What is settled
- **CoT raises accuracy on multi-step reasoning for large models** (arithmetic, commonsense, symbolic). Replicated across Wei, Kojima, and many follow-ups.
- **Few-shot exemplars primarily teach format and framing.** Brown et al. (2020, "Language Models are Few-Shot Learners," GPT-3, 175B, arXiv:2005.14165) established in-context learning; subsequent ablations (incl. Min et al. work on demonstration labels) show exemplars mostly fix output shape, label space, and style rather than impart new reasoning.
- **Prompt format is a real, measurable performance variable.** Sclar et al. (ICLR 2024, arXiv:2310.11324) show up to ~76 accuracy-point swings on LLaMA-2-13B from *formatting changes alone* in few-shot settings — not noise.

### What is disputed
- **Whether CoT reflects "reasoning" at all.** Wang et al. (2023) show invalid rationales nearly match valid ones, implying CoT conditions a *trajectory shape* more than it executes valid inference. Open interpretive question.
- **Whether personas help.** Zheng et al. (2024, EMNLP Findings) and Meincke/Mollick Report 4 (2025) find expert personas do **not** reliably improve factual accuracy and can hurt; yet ensembling role + neutral prompts (Jekyll & Hyde) reports gains. The reconciliation: personas affect *alignment/style/robustness via ensembling*, not *factual retrieval*.
- **Whether instruction tuning helps or suppresses latent reasoning.** See "changed recently."

### What has changed recently (last 5 years)
- 2022: CoT discovered (Wei; Kojima).
- 2023: mechanism scrutiny (Wang et al.) — relevance/ordering > correctness.
- 2024: CoT becomes a *decoding* phenomenon, not a prompting one (Wang & Zhou); formatting sensitivity formalized (Sclar).
- 2024–2025: persona skepticism hardens (Zheng; Meincke/Mollick); reasoning-tuned models (o-series, etc.) make explicit "think step by step" **redundant or harmful** (Meincke/Mollick Report 2).
- 2025–2026: base-vs-instruct reasoning gap documented — base models with CoT decoding can beat instruction-tuned zero-shot on GSM8K (arXiv:2601.13244, below).

---

## 3. Application Domain Examples

1. **Math / arithmetic agents (GSM8K-class).** Choose elicitation by model tier: few-shot CoT for older base models, zero-shot "step by step" for mid models, *nothing extra* for reasoning-tuned models (CoT adds variance — Meincke/Mollick 2).
2. **Structured extraction / parsing pipelines.** XML/delimiter tags (`<instruction>`, `<input>`, `<output>`) reduce field confusion; format choice is model-specific (reported preferences: GPT-4 ↔ Markdown, GPT-3.5 ↔ JSON, Claude/LLaMA ↔ XML). Treat format as a tunable hyperparameter, not a style choice (Sclar).
3. **Factual QA / knowledge systems.** Do **not** rely on "act as an expert" for accuracy (Zheng 2024; Meincke/Mollick 4). Invest the prompt budget in task specificity and evaluation instead.
4. **Multi-model deployments where temperature is shared config.** temperature 0.0 is reliable on OpenAI/Anthropic; on Gemini 3, Google advises *against* lowering temperature (looping risk). A portable config that hard-codes temp=0 is a latent bug.
5. **Cost/latency-sensitive reasoning.** CoT-decoding (top-k inspection, Wang & Zhou) is an alternative to prompt-side CoT — relevant when you control the decoding loop and want reasoning without longer prompts.

---

## 4. The Book's Thesis Connection

This chapter is the book's proof-of-concept that prompt engineering is an **engineering discipline, not folklore**. Every popular technique here has a folk-rule version ("always think step by step," "act as an expert," "set temperature to 0," "give examples") and a mechanism-bounded version that the research actually supports:

- CoT works **because** the prompt (or decoding choice) conditions the output distribution toward step-shaped trajectories that happen to land on correct answers more often — *not* because the model executes valid logic (Wang 2023). That reframing is falsifiable and was falsified for the naive reading (invalid rationales still work).
- The mechanism is **first-principles sampling**: Wang & Zhou (2024) prove the reasoning lives in the logit/top-k distribution, recoverable by decoding alone. This lets the chapter teach CoT through entropy/sampling rather than mysticism.
- Each folk rule gets a **named failure mode and decision procedure**: persona → degrades factual retrieval; low temperature → Gemini looping; CoT on reasoning models → added variance. This is precisely the chapter template (core claim → mechanism → failure mode → decision procedure).

---

## 5. The AI Wayback Machine — Candidate Figures

*(Checked against existing `prompt-engineering-with-llms-wayback.md` — Searle, Sagan, Goffman, Newell, Touvron already used; all candidates below are new.)*

1. **George Pólya** (Hungarian-American mathematician, 1887–1985). Author of *How to Solve It* (1945) — the canonical decomposition of problem-solving into intermediate steps ("understand, plan, carry out, look back"). Chain-of-thought is, mechanically, Pólya's heuristic imposed on a token stream. *Anchor prompt:* "George Pólya, Hungarian-American mathematician, circa 1945, seated with handwritten problem-solving heuristics, historically plausible editorial portrait, period clothing, no text, no watermark."

2. **Adele Goldberg** (American computer scientist, b. 1945; Smalltalk / Xerox PARC). Pioneer of message-passing and the idea that *interface and framing* shape what a system will do — a direct ancestor of "the format of the prompt is part of the program." Brings gender diversity and a software-design (not math/logic) lens. *Anchor prompt:* "Adele Goldberg, American computer scientist, circa 1980, at a workstation with object-oriented design notes, historically plausible editorial portrait, period clothing, no text, no watermark."

3. **Mary Everest Boole** (English mathematician/educator, 1832–1916). Pioneer of how *sequence and framing of presented examples* drive a learner's induction — essentially few-shot pedagogy a century early. Lesser-known, female, education-focused. *Anchor prompt:* "Mary Everest Boole, English mathematician and educator, circa 1890, with teaching notebooks on guided discovery, historically plausible editorial portrait, period Victorian clothing, no text, no watermark."

**Diversity flag:** Pólya (male), Goldberg (female, modern CS), Boole (female, 19th c. education) — balanced on gender and era; skews Euro/American. A non-Western candidate (e.g., a figure from the Indian or Arabic logic/grammar tradition) would improve geographic spread if the drafter wants a fourth.

---

## 6. Pedagogical Delivery Research

- **Prior knowledge required:** probability of a token under a distribution, greedy vs sampled decoding, temperature, in-context learning. NOT transformer internals (per book's stated reader model). The chapter should teach CoT through *the output distribution*, which the reader already has the math for.
- **Common misconceptions in the target reader:**
  1. "CoT makes the model reason" → it conditions trajectory shape; invalid rationales still work (Wang 2023).
  2. "More examples / a persona always helps" → examples teach format; personas don't help factual accuracy and can hurt (Zheng; Meincke/Mollick).
  3. "Temperature 0 is universally safest" → false on Gemini (looping).
  4. "Instruction-tuned > base, always" → false under CoT decoding on GSM8K (2601.13244).
- **Instructional sequence that works:** show one GSM8K item three ways (direct answer wrong → zero-shot CoT right → CoT-decoding right *with no prompt change*). The third step forces the mechanism insight: the reasoning was latent.
- **Teaching failure mode:** presenting techniques as a checklist ("do CoT, add a persona, set temp 0") reproduces the folklore the book is arguing against. Each technique must arrive with its scope condition.
- **Understand vs memorize:** memorize = "the four techniques." Understand = "every technique is a way of conditioning or decoding the output distribution; its value is empirical and model-dependent." Test the latter by asking the reader to *predict* when CoT will hurt.

---

## 7. Representation and Display Research

A **technique × evidence comparison table** would serve this chapter well. Columns: *Technique* | *Folk rule* | *What research shows* | *Mechanism* | *Named failure mode* | *Decision rule*. Rows: zero-shot CoT; few-shot CoT; persona; formatting/delimiters; temperature; base vs instruction-tuned.

A second small **figure** is warranted: a single GSM8K item rendered three ways (direct / zero-shot CoT / CoT-decoding via top-k) with the output distribution sketched — makes the "reasoning is in the distribution" point visual. Otherwise no special display required.

---

## 8. Open Questions and Research Gaps

- **Does CoT "reasoning" generalize or pattern-match?** arXiv:2601.13244 explicitly frames instruction tuning as possibly inducing "surface-level pattern matching" — unresolved.
- **Why do reasoning-tuned models stop benefiting from explicit CoT?** Meincke/Mollick 2 documents the effect; the mechanism (internal CoT already saturating) is asserted, not proven.
- **Likely-stale within 3 years:** all model-specific claims (Gemini temperature behavior, model-format preferences, specific GSM8K deltas) — these track model versions and will need re-verification each edition. Flag explicitly in the chapter.
- **Contested-as-settled:** "few-shot examples don't teach reasoning, only format" is widely repeated but rests on a specific set of ablations; treat as well-supported, not closed.
- **Persona reconciliation** (helps style/robustness, hurts factual accuracy) is a synthesis across papers with different tasks/metrics — clean but not from a single controlled study.

---

## 9. Sourcing Notes

- **Spine citations VERIFIED (exact):** Wei et al. 2022 (arXiv:2201.11903, NeurIPS 2022); Wang/Min et al. 2023 "Towards Understanding CoT" (arXiv:2212.10001, ACL 2023; 80–90% invalid-rationale figure confirmed); Wang & Zhou 2024 "CoT Reasoning Without Prompting" (arXiv:2402.10200, NeurIPS 2024); Meincke/Mollick et al. 2025 Report 2 (arXiv:2506.07142, SSRN 5285532); Brown et al. 2020 GPT-3 (arXiv:2005.14165); Jekyll & Hyde 9.98%/12-dataset figure (arXiv:2408.08631, "Persona is a Double-edged Sword," Aug 2024 — confirmed exactly).
- **Spine citation CORRECTED:** The "base models w/ CoT decoding beat instruction-tuned zero-shot on GSM8K by up to 32.7%" claim is **NOT** from Wang & Zhou (2024). It is from **"Do Instruction-Tuned Models Always Perform Better Than Base Models? Evidence from Math and Domain-Shifted Benchmarks," arXiv:2601.13244 (2026)**, which reports a 32.67% drop for Llama3-70B in zero-shot CoT. The drafter must attribute it there, not to Wang & Zhou. (Wang & Zhou's own figure is +10–30 pts from CoT-decoding across PaLM-2.)
- **Spine claim REFINED:** "persona degrades factual retrieval (PRISM-style MMLU evals)." The core empirical source is **Zheng, Pei, Logeswaran, Lee, Jurgens (2024), "When 'A Helpful Assistant' Is Not Really Helpful," EMNLP 2024 Findings, arXiv:2311.10054.** The PRISM framing matches **"Expert Personas Improve LLM Alignment but Damage Accuracy" (arXiv:2603.18507, 2026)** — a 2026 paper; treat as recent/less-settled. Also **Meincke/Mollick et al., "Prompting Science Report 4: Playing Pretend," arXiv:2512.05858 (Dec 2025)** independently confirms expert personas don't improve factual accuracy.
- **ADDITIONAL primary sources added (4):** Kojima et al. 2022 (zero-shot CoT, arXiv:2205.11916); Sclar et al. ICLR 2024 (formatting sensitivity, arXiv:2310.11324); Zheng et al. EMNLP 2024 (persona null result, arXiv:2311.10054); arXiv:2601.13244 (base-vs-instruct CoT). Bonus: Meincke/Mollick Report 4 (arXiv:2512.05858).
- **Could NOT fully verify / caution:** The spine's "positive > negative framing" formatting claim — found strong support for *delimiters/XML* and *format-sensitivity* (Sclar) but no single peer-reviewed controlled study isolating positive-vs-negative *framing*; most support is vendor docs and practitioner blogs. Drafter should present positive-framing as practitioner heuristic, not as a settled empirical finding. arXiv IDs in the 2512/2601/2603 range are 2025–2026 preprints (verified to exist on arXiv) but are recent and may not be peer-reviewed yet — flag accordingly.
