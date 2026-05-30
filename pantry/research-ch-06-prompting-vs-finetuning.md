# Research: Candidate Chapter §6 — Prompt Engineering vs. Fine-Tuning: The Evolving Answer
## Prompt Engineering
**Chapter one-line:** Why the prompting/fine-tuning binary is false — the layered stack (prompt-optimize → SFT → RL) and how to decide.
**Research date:** 2026-05-29

---

## 1. Primary Sources

### Foundational papers and texts

- **Shao, Z., et al. (2024). "DeepSeekMath: Pushing the Limits of Mathematical Reasoning in Open Language Models."** arXiv:2402.03300 (v1 Feb 2024; v3 Apr 2024). DeepSeek AI. *This is the paper that introduced **Group Relative Policy Optimization (GRPO)**.* GRPO is a PPO variant that removes the learned value/critic network: instead of training a separate critic to estimate the advantage, it samples a *group* of outputs for the same prompt, scores them, and uses the group's standardized (whitened — mean/variance normalized) reward as the baseline. This cuts the memory and compute of RL post-training roughly in half. GRPO was later used to train DeepSeek-R1, which popularized it; it now ships in HuggingFace TRL and VERL. **VERIFIED — arXiv ID, authorship (Zhihong Shao et al., DeepSeek), and the "introduced GRPO" attribution all confirmed.** Cross-ref Ch.15 (RLHF/DPO) for the mechanism; this decision chapter treats GRPO only as a *tier-3 escalation option*.

- **Agrawal, L. A., et al. (2025). "GEPA: Reflective Prompt Evolution Can Outperform Reinforcement Learning."** arXiv:2507.19457 (July 2025; accepted ICLR 2026, Oral). 17 authors led by Lakshya A Agrawal; the DSPy/Stanford-adjacent line of work. **GEPA = Genetic-Pareto.** It optimizes the *text of prompts* in a compound LLM system: it samples execution trajectories (reasoning, tool calls, outputs), reflects on them in natural language to diagnose failures, proposes prompt edits, tests them, and keeps a Pareto frontier of complementary candidates. The headline contrast with GRPO is below. **VERIFIED — title, arXiv ID, lead author, and "outperform RL" framing all confirmed.** This is the central empirical anchor for the chapter's "start with prompt optimization" thesis.

- **Soylu, D., Potts, C., Khattab, O., et al. (2024). "Fine-Tuning and Prompt Optimization: Two Great Steps that Work Better Together."** arXiv:2407.10930. Introduces the **BetterTogether** algorithm (released in DSPy): alternate between optimizing prompts and fine-tuning weights in a pipeline. This is the *direct primary source* for the "layered approach beats either alone" claim — see §2. Cross-ref Ch.13 (SFT/RAG) and Ch.14 (LoRA/QLoRA) for the weight-tuning mechanism.

- **Soylu, D., et al. (2025). "Multi-module GRPO: Composing Policy Gradients and Prompt Optimization for Language Model Programs."** arXiv:2508.04660. Introduces **MMGRPO** (`dspy.GRPO` optimizer). Most relevant primary source showing prompt-optimization and RL *composed* rather than chosen between — the explicit "stack" the chapter argues for.

### Key empirical cases

- **Pornprasit, C., & Tantithamthavorn, C. (2024). "Fine-Tuning and Prompt Engineering for Large Language Models-based Code Review Automation."** arXiv:2402.00905; published in *Information and Software Technology* (Elsevier), DOI 10.1016/j.infsof.2024.107523. **Both authors are at Monash University, Australia.** **CORRECTION:** the spine's attribution to "University of Australia" is **wrong** — there is no such institution; the correct affiliation is **Monash University**. (PromptHub's blog summary is a *secondary* relay of this paper.) This is the source of the "63–1,100%" figure — see §3 for the precise numbers and caveats.

- **GEPA benchmark suite (Agrawal et al. 2025):** HotpotQA, HoVer, IFBench, PUPA, evaluated on Qwen3-8B (open) and GPT-4.1-mini (proprietary). Primary source for the "6–19 points / 35×" claim — exact numbers in §2.

---

## 2. The Core Concept — State of the Field

### What is settled

- **The binary is dead as an engineering frame.** Prompting and fine-tuning are not mutually exclusive choices; they are *layers* of a post-training stack that can be combined. The DSPy line of work (BetterTogether, MMGRPO) treats prompt text and model weights as two sets of parameters of the *same* system, optimizable jointly. This is no longer controversial among practitioners building compound systems.

- **Prompt optimization should usually come first.** It is cheap, fast, requires no GPUs or labeled training corpus, and is reversible. Fine-tuning incurs ongoing model-maintenance cost (retraining when the base model updates, hosting a custom checkpoint, eval drift). The consensus heuristic: *escalate only when the prompt-optimized ceiling is provably insufficient.*

- **GRPO mechanism is settled.** Critic-free, group-relative advantage estimation; ~2× cheaper than PPO; the de-facto RL method for reasoning post-training (DeepSeek-R1, and open implementations in TRL/VERL).

### What is disputed

- **The headline "prompt optimization beats RL" claim — VERIFIED but narrow.** The spine's "beats GRPO by 6–19 points using 35× fewer compute" resolves precisely to GEPA (Agrawal et al. 2025):
  - **"GEPA outperforms GRPO by 6% on average and by up to 20%, while using up to 35× fewer rollouts"** (paper's own abstract framing).
  - The "6–19 point" range comes from the *per-benchmark deltas over GRPO*: **HotpotQA +19.0 pts (62.3 vs 43.3), HoVer +13.7 pts (52.3 vs 38.6), PUPA +5.2 pts (91.8 vs 86.7), IFBench +2.7 pts (38.6 vs 35.8)**. So "6–19 points" is defensible as *"roughly +3 to +19 points depending on benchmark, ~+6 on average."* **The book should state it as "up to ~19 points / ~6 on average, with up to 35× fewer rollouts"** — not a flat "6–19."
  - **CAVEAT / SCRUTINY:** "35× fewer rollouts" is a *sample-efficiency* claim (number of program executions), not wall-clock or dollar compute, and "rollouts" ≠ "compute resources" one-to-one — the spine's phrasing "35× fewer compute resources" is a slight overclaim of what the paper measures. GRPO here was a specific `dspy.GRPO`/multi-module setup, not a maximally-tuned RL run. **This is one paper on four benchmarks; treat "prompt optimization beats RL" as a demonstrated existence-proof on agentic/compound tasks, not a universal law.** GRPO's home turf (single-model math/code reasoning à la DeepSeek-R1) is *not* what GEPA tested.

- **The "up to 60% on multi-hop reasoning" layered-approach claim — VERIFIED, but it is the BetterTogether number and needs precise attribution.** Soylu et al. 2024 (arXiv:2407.10930) report: *"BetterTogether strategies optimizing the weights and prompts of a pipeline together outperform optimizing weights alone and prompts alone by **up to 60%** and **6%**, respectively, on average across LMs and tasks"* (mistral-7b, llama-2-7b, llama-3-8b on multi-hop QA, math reasoning, classification). **CORRECTION/PRECISION:** the 60% is the gain of joint optimization **over fine-tuning weights *alone***, and only ~6% over prompt-optimization alone — *not* a flat "60% over either alone." The book must not write "by up to 60% on multi-hop reasoning" without that asymmetry, or it misrepresents the paper. The separately-reported MMGRPO (2508.04660) figure — *"+11% over the post-trained LM, +5% over prompt optimization alone"* — is the cleaner "stack beats parts" number for the GRPO tier.

### What has changed recently (last 5 years)

- **2024:** GRPO (DeepSeekMath, Feb) → DeepSeek-R1 (Jan 2025) makes verifiable-reward RL cheap and mainstream. Same year, BetterTogether (Jul) reframes prompt-vs-tune as joint optimization.
- **2025:** GEPA (Jul) lands the provocative "reflective prompt evolution can beat RL" result; MMGRPO (Aug) composes the two. DSPy matures into the de-facto prompt-optimization compiler.
- **2026 (current):** Practitioner syntheses (e.g., llm-stats.com, *"Is Fine-Tuning Better Than Prompt Engineering in 2026?"*) consolidate the "prompt-optimize first, escalate deliberately" stance. **Treat llm-stats.com and PromptHub as SECONDARY/practitioner sources** — they relay the primary papers above.

---

## 3. Application Domain Examples

**Code-review automation (Pornprasit & Tantithamthavorn 2024, Monash — DOCUMENTED, with caveats).** Task: generate the revised code given an original + reviewer comment; metric = **Exact Match (EM)** against the human-written revision. Findings, stated precisely:
- *Fine-tuning GPT-3.5 with **few-shot** learning achieves **63.91% – 1,100% higher EM** than non-fine-tuned models.* (This is the spine's "63–1,100%" figure — **VERIFIED**, but note it is the *few-shot* fine-tuned variant, and it is a *relative* percentage gain over baselines, so the 1,100% upper bound reflects a very low denominator baseline, not 11× absolute accuracy.)
- *Fine-tuning GPT-3.5 with **zero-shot** learning achieves **73.17% – 74.23% higher EM** than the prior (non-LLM) approaches* — this is closest to the spine's "fine-tuning zero-shot beat all prompt methods."
- *Prompt engineering: GPT-3.5 with few-shot beats GPT-3.5 zero-shot by 46.38% – 659.09% EM.*
- *Adding a **persona** to the prompt **hurt**: −1.02% to −54.17% EM* — a clean, citable counter-result against reflexive persona-prompting.
- **CAVEAT:** EM is a brittle metric (penalizes any non-identical-but-correct revision); GPT-3.5 is now dated; the gains are over weak baselines. The honest takeaway is *"on this narrow high-EM-ceiling code task, fine-tuning beat prompting"* — a domain-specific, high-accuracy use case, exactly the regime where the chapter says fine-tuning earns its cost.

**Compound agentic systems (GEPA / DSPy — DOCUMENTED).** Multi-hop QA (HotpotQA), fact verification (HoVer), privacy-preserving delegation (PUPA): here *prompt evolution beat GRPO* (§2 numbers). Regime: dynamic, multi-module, no clean single reward — prompting wins.

**When pure prompting suffices (consensus, lightly documented):** rapid deployment, dynamic/changing requirements, general business tasks, knowledge that changes faster than you can retrain. The recurring practitioner warning: *organizations overestimate the need for custom models* — fine-tuning is often "expensive theater" that adds knowledge better served by RAG (cross-ref Ch.13). **Label: practitioner consensus, not a controlled study.**

**When fine-tuning is necessary (consensus):** (1) persistent style/persona/format that must hold *regardless of user instruction*; (2) high-accuracy narrow domain with a stable labeled set and a plateaued prompt; (3) **smaller-model deployment** — freezing behavior into a small model you can host cheaply at high volume. The cost crossover is volume-driven (millions of requests/month). One widely-cited but **unverified** practitioner figure: "fine-tuned models ~28.3% higher accuracy on domain tasks" — **FLAG as illustrative; no clean primary source located.**

---

## 4. The Book's Thesis Connection

This is a **decision/strategy chapter**, and its job is *not* to re-teach mechanism. Ch.13 owns SFT-vs-RAG; Ch.14 owns LoRA/QLoRA; Ch.15 owns RLHF/DPO/GRPO internals. What §6 *adds*, in the book's mechanism-first / falsifiable / named-failure-mode idiom:

- **A falsifiable decision procedure, not a vibe.** "Prompt-optimize first" becomes a *testable gate*: build an eval set, run automated prompt optimization (DSPy/GEPA), measure the ceiling; only escalate to SFT if the ceiling is below requirement *and* you have a stable labeled set; only escalate to RL/GRPO if (a) you can define a *verifiable reward* and (b) the prompt-optimized ceiling is still insufficient. Each arrow has a precondition you can check.

- **Named failure modes for the decision itself:** *Premature fine-tuning* (paying retraining cost for what a better prompt fixes); *reward-hacking escalation* (reaching for GRPO without a verifiable reward); *persona-reflex* (the Monash −54% EM result — adding a persona because it "feels" right); *RAG-vs-tune confusion* (fine-tuning to inject knowledge that belongs in retrieval — cross-ref Ch.13).

- **Mechanism-first reframe:** prompts and weights are both *parameters of one system*. That single sentence dissolves the binary and licenses the BetterTogether/MMGRPO "compose them" result. The chapter's spine — prompt-optimize → SFT → RL — is the *order of escalating cost and irreversibility*, justified by the empirical anchors (GEPA: prompting can beat RL on agentic tasks at 35× lower sample cost; Monash: fine-tuning wins on narrow high-accuracy tasks).

---

## 5. The AI Wayback Machine — Candidate Figures

Three figures, each substantively tied to a layer of the stack (optimization, RL, decision theory). Lesser-known-where-possible; Wikipedia-anchored.

1. **Herbert Robbins & Sutton Monro — "A Stochastic Approximation Method" (1951).** Wikipedia: *Stochastic approximation*. The ancestor of every gradient-descent-with-noise method — the mathematical root of *automated optimization* itself (and of RL's stochastic-gradient core). Connects directly to the chapter's tier-1 (prompt optimization as search) and tier-3 (GRPO as stochastic policy gradient). *Lesser-known relative to "backprop"; rewards the reader.* **Anchor prompt:** "Explain Robbins–Monro stochastic approximation (1951) as the conceptual ancestor of modern automated optimization — why optimizing under noisy feedback (a few sampled rollouts) is the same problem whether you're tuning prompts or policy weights." **Skew flag:** mid-20th-c. American statistics; pre-ML framing.

2. **Arthur Samuel — self-learning checkers program (1959), "Some Studies in Machine Learning Using the Game of Checkers."** Wikipedia: *Arthur Samuel (computer scientist)*. Coined "machine learning"; built one of the first systems to *improve from self-play* via what we'd now call temporal-difference learning — the deep ancestor of GRPO's "sample outcomes, adjust behavior." **Anchor prompt:** "Trace the line from Samuel's 1959 self-learning checkers (learning from game outcomes) to GRPO's group-relative reward — what's genuinely the same, and what's new about LLM-scale RL?" **Skew flag:** game-playing, single-agent, IBM-era hardware; risks overstating continuity.

3. **Abraham Wald — sequential analysis / SPRT (1945; declassified from WWII work).** Wikipedia: *Sequential analysis*. Decision theory's founding move: *decide to stop, continue, or escalate* using the data so far, rather than fixing the experiment size in advance — a direct historical analogue of the chapter's escalation gate (prompt → SFT → RL only as evidence warrants). **Anchor prompt:** "Present Wald's sequential probability ratio test (1945) as a decision-theoretic template for the prompt→fine-tune→RL escalation ladder: each tier is a 'continue or stop' decision made on accumulated evidence." **Skew flag:** wartime statistics, hypothesis-testing frame; the analogy is structural, not literal.

---

## 6. Pedagogical Delivery Research

- **Lead with the falsified binary.** Students arrive believing they must "choose." Open by showing the GEPA result (prompting beat RL) *and* the Monash result (fine-tuning beat prompting) side by side — the contradiction forces the realization that the answer is *"it depends, and here's the decision procedure."*
- **Teach the ladder as escalating cost/irreversibility**, not as a quality ranking. The most common student error is treating fine-tuning as "more advanced/better." Counter with the cost-crossover and the "organizations overestimate custom models" caveat.
- **Use the persona −54% EM result as a memorable myth-buster** — concrete, counterintuitive, citable.
- **Distinguish "rollouts" from "compute" explicitly** when presenting the 35× figure, modeling the book's discipline of reading numbers precisely.
- **Worked decision walk-throughs:** one task that should stop at prompting (dynamic business task), one that justifies SFT (narrow high-accuracy code task), one that justifies GRPO (verifiable-reward math/code reasoning).

---

## 7. Representation and Display Research

**Two displays are warranted (specify both):**

1. **Layered-stack decision flowchart** (the spine made visual). Entry: "Define eval set + requirement." Gate 1: "Run automated prompt optimization (DSPy/GEPA) → ceiling ≥ requirement?" → if yes, ship. Gate 2: "Stable labeled set + need frozen behavior / small deployable model?" → SFT (Ch.14). Gate 3: "Verifiable reward exists AND prompt ceiling still insufficient?" → RL/GRPO (Ch.15). Each gate annotated with its *failure mode* if skipped. Mirror Wald's "continue/stop" logic.

2. **Cost-vs-capability comparison table.** Rows: Prompt engineering / Automated prompt optimization (DSPy-GEPA) / SFT (LoRA) / RL (GRPO). Columns: needs labeled data?, GPU/compute cost, reversibility, ongoing maintenance, when it wins, key empirical anchor. Populate "when it wins" / anchors from §2–3 (GEPA agentic tasks; Monash narrow-EM code; GRPO verifiable-reward reasoning).

---

## 8. Open Questions and Research Gaps

- **Does "prompt optimization beats RL" generalize beyond compound/agentic tasks?** GEPA's win is on multi-module pipelines; GRPO's strength is single-model reasoning. No head-to-head on the *same* reasoning task at matched compute is firmly established. Open.
- **What's the real compute/dollar (not rollout) crossover** between GEPA-style optimization and GRPO? "35× fewer rollouts" doesn't cleanly translate to cost; the conversion is unstudied here.
- **When does joint optimization (BetterTogether/MMGRPO) beat sequential escalation?** The chapter teaches a ladder; the DSPy work suggests *composing* tiers can beat climbing them. The boundary is unsettled.
- **The "28.3% accuracy gain from fine-tuning" and similar round practitioner figures lack primary sourcing** — a genuine gap the book should flag rather than cite.
- **Model-version churn vs. fine-tuning ROI:** as base models update every few months, the maintenance cost of a custom checkpoint may dominate — under-quantified.

---

## 9. Sourcing Notes

**Verified primary sources (web-confirmed):**
- GRPO origin — Shao et al. 2024, arXiv:2402.03300 (DeepSeekMath). Authorship, ID, "introduced GRPO" all confirmed.
- GEPA — Agrawal et al. 2025, arXiv:2507.19457; ICLR 2026 Oral. Title, ID, lead author confirmed.
- Code-review case — Pornprasit & Tantithamthavorn 2024, arXiv:2402.00905; *Inf. & Softw. Tech.* DOI 10.1016/j.infsof.2024.107523; **Monash University**.
- Layered approach — Soylu et al. 2024 BetterTogether (arXiv:2407.10930); Soylu et al. 2025 MMGRPO (arXiv:2508.04660).

**Claim adjudication:**
- **"6–19 points / 35× fewer compute"** — VERIFIED as GEPA: up to ~19 pts (HotpotQA), ~6 pts avg, up to 35× fewer *rollouts*. **Correct the book to "up to ~19 pts / ~6 avg" and say "rollouts," not "compute resources."**
- **"layered beats either alone by up to 60% on multi-hop reasoning"** — VERIFIED as BetterTogether, but the 60% is gain *over fine-tuning-weights-alone*; only ~6% over prompt-opt-alone. **Must state the asymmetry; do not write a flat "60% over either."** Cleaner "stack beats parts" stat: MMGRPO +11% over post-trained LM / +5% over prompt-opt.
- **"63–1,100% higher Exact Match"** — VERIFIED (few-shot fine-tuned GPT-3.5, Monash 2024). Relative % over weak baselines; pair with the zero-shot 73–74% figure.
- **"University of Australia" attribution** — **WRONG. Correct to Monash University.** (PromptHub is a secondary relay.)
- **"28.3% accuracy gain from fine-tuning"** — UNVERIFIED / illustrative practitioner figure; flag.

**Secondary/practitioner (label as such):** llm-stats.com (2026 synthesis), PromptHub blog, deeplearning.ai The Batch (GEPA writeup), morphllm.com.

**Sources consulted:**
- https://arxiv.org/abs/2402.03300 (DeepSeekMath / GRPO)
- https://arxiv.org/abs/2507.19457 (GEPA)
- https://arxiv.org/abs/2402.00905 + https://research.monash.edu/.../fine-tuning-and-prompt-engineering... (code-review case; Monash affiliation)
- https://arxiv.org/abs/2407.10930 (BetterTogether)
- https://arxiv.org/pdf/2508.04660 (MMGRPO / dspy.GRPO)
- https://llm-stats.com/blog/research/fine-tuning-vs-prompt-engineering-2026 (secondary)
- https://en.wikipedia.org/wiki/Stochastic_approximation (Robbins–Monro)
- https://en.wikipedia.org/wiki/Arthur_Samuel_(computer_scientist)
- https://en.wikipedia.org/wiki/Sequential_analysis (Wald)

**Fetch notes:** Direct arXiv PDF/HTML fetches returned empty/PDF-only or HTTP 429 (rate limit); all figures above are corroborated via WebSearch result text and multiple independent secondary relays (deeplearning.ai, emergentmind, alphaxiv for GEPA; Monash research portal + ScienceDirect/ACM for the code paper). No curl/python used.
