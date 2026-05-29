# Research: Candidate Chapter §7 — Contested and Emerging Areas
## Prompt Engineering with LLMs
**Chapter one-line:** Three live debates — whether prompting is obsolescing, when self-critique helps vs. hurts, and how multimodal prompting differs.
**Research date:** 2026-05-29

---

## 1. Primary Sources

### Foundational papers and texts

**Self-correction / reflection (the core empirical literature):**

- **Huang, Jie; Chen, Xinyun; Mishra, Swaroop; Zheng, Huaixiu Steven; Yu, Adams Wei; Song, Xinying; Zhou, Denny (2024). "Large Language Models Cannot Self-Correct Reasoning Yet."** ICLR 2024 (conference paper). arXiv:2310.01798 (submitted Oct 2023). VERIFIED — authors, venue, arXiv ID, and central claim all confirmed. Central finding: *intrinsic* self-correction (no external feedback) on reasoning tasks does **not** reliably improve and frequently **degrades** accuracy — models flip correct answers to incorrect. The apparent gains in earlier self-correction papers came largely from using oracle/ground-truth labels to decide *when* to stop correcting. This is the keystone citation for the chapter's "self-critique without grounding hurts" claim.
  - arXiv: https://arxiv.org/abs/2310.01798
  - ICLR proceedings PDF: https://proceedings.iclr.cc/paper_files/paper/2024/file/8b4add8b0aa8749d80a34ca5d941c355-Paper-Conference.pdf
  - ~668 citations on Semantic Scholar (as of search) — highly influential.

- **Wang, Xuezhi; Wei, Jason; Schuurmans, Dale; Le, Quoc; Chi, Ed; Narang, Sharan; Chowdhery, Aakanksha; Zhou, Denny (2023). "Self-Consistency Improves Chain of Thought Reasoning in Language Models."** ICLR 2023. arXiv:2203.11171 (v1 Mar 2022; v4 Mar 2023). VERIFIED — authors, venue (ICLR 2023, not 2022 publication — submitted 2022), arXiv ID all confirmed. Sample *k* diverse reasoning paths at temperature > 0, then take the **majority-vote** answer (marginalize over reasoning paths). Reported gains: GSM8K +17.9%, SVAMP +11.0%, AQuA +12.2%, StrategyQA +6.4%, ARC-challenge +3.9%. **Contrast with self-critique:** self-consistency improves *without* asking the model to judge its own work — it exploits answer-distribution structure, not metacognition. This is the chapter's cleanest "what works instead" example.
  - arXiv: https://arxiv.org/abs/2203.11171

- **Shinn, Noah; Cassano, Federico; Berman, Edward; Gopinath, Ashwin; Narasimhan, Karthik; Yao, Shunyu (2023). "Reflexion: Language Agents with Verbal Reinforcement Learning."** NeurIPS 2023. arXiv:2303.11366 (Mar 2023). VERIFIED — authors, venue, arXiv ID confirmed. Agents *verbally reflect* on a **task-feedback signal** (scalar reward or free-form, external or internally simulated), store the reflection in an episodic memory buffer, and retry. KEY NUANCE for the chapter: Reflexion works because it incorporates an **external feedback signal** (e.g., unit-test pass/fail, environment reward) — it is NOT pure intrinsic self-correction. It belongs on the "grounded" side of the decision tree. NeurIPS poster: https://neurips.cc/virtual/2023/poster/70114
  - arXiv: https://arxiv.org/abs/2303.11366
  - Code: https://github.com/noahshinn/reflexion

- **Madaan, Aman; et al. (2023). "Self-Refine: Iterative Refinement with Self-Feedback."** NeurIPS 2023. arXiv:2303.17651 (v1 Mar 30 2023; v2 May 25 2023). VERIFIED. Single LLM acts as generator, feedback-provider, and refiner, iterating without training. Reports ~20% human-preference improvement across 7 tasks (dialogue, code, math) on GPT-3.5/ChatGPT/GPT-4. IMPORTANT TENSION the chapter should surface: Self-Refine reports gains on *generation-quality* tasks (where "better" is subjective and the feedback is about style/completeness), whereas Huang et al. show *reasoning* tasks (where there is one correct answer) do not benefit. The reconciliation: intrinsic self-critique can polish open-ended outputs but cannot reliably *find its own reasoning errors*. Project site: https://selfrefine.info/
  - arXiv: https://arxiv.org/abs/2303.17651

- **CorrectBench — Anonymous/authors of arXiv:2510.16062 (2025). "Can LLMs Correct Themselves? A Benchmark of Self-Correction in LLMs."** arXiv:2510.16062 (Oct 2025). VERIFIED — but **CORRECTION TO SPINE**: this is a recent (Oct 2025) preprint, NOT an established/canonical benchmark. Treat as recent secondary synthesis, not foundational. Its **taxonomy is the useful contribution** and matches the spine: self-correction splits into **(1) intrinsic** (no external tools — RCI, Self-Refine, Chain-of-Verification/CoVe, Reflexion-style internal), **(2) external** (knowledge bases, search, tools/compilers validate outputs), and **(3) fine-tuned** (a model trained to correct). Reported headline numbers (cite cautiously, single preprint): ~5.2% gains on MATH for some strategies; hybrid/mixed strategies add accuracy but ~40% slower. Confirm venue/peer-review status before the drafter relies on the specific percentages.
  - arXiv: https://arxiv.org/abs/2510.16062
  - Project: https://correctbench.github.io/ ; code: https://github.com/HCR050806/CorrectBench

**Obsolescence debate:**

- **Karpathy, Andrej (May 7, 2025). "System prompt learning" — X/Twitter post, NOT a paper.** VERIFIED — this is a tweet (x.com/karpathy/status/1921368644069765486, dated May 7 2025), framed as a thinking-out-loud proposal, NOT peer-reviewed and NOT a formal talk. FLAG AS NON-PEER-REVIEWED OPINION. Exact framing: "We're missing (at least one) major paradigm for LLM learning... possibly... system prompt learning? Pretraining is for knowledge. Finetuning (SL/RL) is for habitual behavior. Both of these involve a change in parameters but a lot of human learning feels more like a change in system prompt." The analogy: you hit a problem, figure something out, and "remember" it in explicit terms for next time — "like taking notes for yourself" — "the LLM writing a book for itself on how to solve problems." NOTE: the term and proposal are Karpathy's; the *implementations* circulating under the name (e.g., the optillm SPL plugin by "codelion" on HuggingFace) are third-party, not Karpathy's, and unvalidated — keep them separate. Karpathy's broader "Software 3.0" framing was delivered as a talk (Latent Space writeup: https://www.latent.space/p/s3); "system prompt learning" specifically is the tweet.
  - Tweet: https://x.com/karpathy/status/1921368644069765486

- **Meincke, Lennart; Mollick, Ethan R.; Mollick, Lilach; Shapiro, Dan (2025). "Prompting Science Report 1: Prompt Engineering is Complicated and Contingent."** SSRN abstract 5165270; arXiv:2503.04818 (Mar 2025); Wharton Generative AI Labs tech report. VERIFIED. **CORRECTION/REFINEMENT TO SPINE:** the spine framed Wharton as showing "systematic prompting still beats casual prompting." The actual finding is more nuanced and *more useful*: (a) there is **no single standard** for scoring a benchmark and the choice of standard swings results dramatically; (b) it is **hard to predict in advance** whether a given prompt tweak helps or hurts a *specific* question — politeness sometimes helps, sometimes hurts. The takeaway is not "tricks win" but "effects are contingent and must be measured per task." This actually *strengthens* the book's "specification quality, measured empirically > universal tricks" thesis.
  - arXiv: https://arxiv.org/abs/2503.04818 ; SSRN: https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5165270

- **Meincke et al. (2025). "Prompting Science Report 2: The Decreasing Value of Chain of Thought in Prompting."** SSRN 5285532; Wharton GAIL. VERIFIED. Finding: on reasoning-tuned models, CoT prompting yields only marginal accuracy gains at substantial time cost (~20–80% slower); on non-reasoning models it gives modest average gains but *increased variance*. Directly supports the obsolescence thesis: a once-essential "trick" (explicit CoT) is losing marginal value as models internalize the reasoning step. https://gail.wharton.upenn.edu/research-and-insights/tech-report-chain-of-thought/

- **Meincke et al. (2025). "Prompting Science Report 3: I'll pay you or I'll kill you — but will you care?"** SSRN 5375404; Wharton GAIL. VERIFIED. Threatening or tipping the model does NOT reliably improve performance on hard benchmarks — debunks viral folk-prompting. Good case material. https://gail.wharton.upenn.edu/research-and-insights/techreport-threaten-or-tip/

- **Basil, Savir; Shapiro, Ina; Shapiro, Dan; Mollick, Ethan R.; Mollick, Lilach; Meincke, Lennart (2025/2026). "Prompting Science Report 4: Playing Pretend: Expert Personas Don't Improve Factual Accuracy."** SSRN 5879722. VERIFIED (exists; confirm exact date before citing). Across six LLMs on graduate-level science/engineering/law questions, "expert personas" gave **no consistent boost** and sometimes hurt. Meincke quote: "When LLMs first came out people assumed personas would really help, but it matters less today." Strong evidence that a canonical 2023-era trick (role/persona prompting) has decayed. (See Wharton "Why You Shouldn't Ask Chatbots to Act Like an Expert.")

**Multimodal prompting:**

- **Yang, Jianwei; Zhang, Hao; Li, Feng; Zou, Xueyan; Li, Chunyuan; Gao, Jianfeng (2023). "Set-of-Mark Prompting Unleashes Extraordinary Visual Grounding in GPT-4V."** arXiv:2310.11441 (Oct 2023), Microsoft. VERIFIED. Method: use an off-the-shelf segmenter (SAM) to partition an image into regions, overlay each with a visible **mark** (alphanumeric/box/mask), feed the *marked* image to GPT-4V, and ask grounding questions referencing the marks. Zero-shot GPT-4V+SoM beat the SOTA fully-fine-tuned referring-expression model on RefCOCOg. KEY LESSON for the chapter: the most effective multimodal "prompt" can be *drawn onto the image itself* — prompting is not only textual. Code: https://github.com/microsoft/SoM
  - arXiv: https://arxiv.org/abs/2310.11441

- **Gu, Jindong; Han, Zhen; Chen, Shuo; Beirami, Ahmad; He, Bailan; Zhang, Gengyuan; Liao, Ruotong; Qin, Yao; Tresp, Volker; Torr, Philip (2023). "A Systematic Survey of Prompt Engineering on Vision-Language Foundation Models."** arXiv:2307.12980 (Jul 2023). VERIFIED — full author list confirmed. Surveys prompting across three VLM families: multimodal-to-text (e.g., Flamingo), image-text matching (e.g., CLIP), text-to-image (e.g., Stable Diffusion). Classifies hard prompts (task instruction, ICL, retrieval-based, CoT) vs. soft prompts (tunable continuous vectors). Good anchor for "text-prompt principles carry over, but visual prompts are a new lever." Repo: https://github.com/JindongGu/Awesome-Prompting-on-Vision-Language-Model
  - arXiv: https://arxiv.org/abs/2307.12980

- **Wu, Junda; et al. (2024). "Visual Prompting in Multimodal Large Language Models: A Survey."** arXiv:2409.15310 (Sep 2024). VERIFIED (title/arXiv confirmed; confirm full author list before citing). Covers bounding boxes, markers, pixel-level prompts, soft prompts; documents the empirical folk result that **a simple red circle drawn around an object redirects model attention** to that region. https://arxiv.org/abs/2409.15310

### Key empirical cases

- **The "self-correction that wasn't" case (Huang et al. 2024):** When earlier papers reported GPT-3.5/4 "self-correcting" reasoning, the gain depended on an oracle telling the model when its answer was already right (so it stopped). Remove the oracle — let the model decide for itself whether to revise — and accuracy on GSM8K/CommonsenseQA *drops*. Documented, reproducible, named failure mode: **over-revision / correct-to-incorrect flipping.**
- **Reflexion on HumanEval coding (Shinn et al. 2023):** With unit-test pass/fail as the feedback signal, Reflexion substantially raised pass@1 — a documented case where self-reflection *works because the feedback is external and verifiable.*
- **SoM on RefCOCOg (Yang et al. 2023):** documented benchmark win for a visual-prompt intervention.
- **Wharton threat/tip and persona null results (Reports 3 & 4):** documented cases of popular tricks failing under controlled testing.

---

## 2. The Core Concept — State of the Field

### What is settled

- **Intrinsic self-correction does not reliably fix reasoning errors** and can make accuracy worse (Huang et al. 2024, ICLR). This is among the more robustly replicated negative results in prompting.
- **Self-correction with a verifiable external signal works** (compilers, unit tests, search, execution, environment reward) — Reflexion; the "external" category in CorrectBench's taxonomy.
- **Self-consistency (sample + majority vote) reliably beats single-shot CoT** on tasks with a well-defined answer (Wang et al. 2023) — and it does so *without* asking the model to judge itself.
- **Some classic single-prompt tricks have measurably decayed** as models improved: explicit CoT (diminishing marginal value, Report 2), expert personas (no consistent gain, Report 4), threats/tips (no gain, Report 3).
- **Multimodal prompting reuses text-prompt principles** (specificity, structure, examples) AND adds a genuinely new lever: marks/annotations on the image itself (SoM).

### What is disputed

- **Is prompt engineering "becoming obsolete"?** Two readings: (1) the *tricks* are obsolescing (defensible — see Reports 2–4); (2) prompt engineering *as a discipline* is obsolescing (contested — Wharton Report 1 shows effects are contingent and must still be measured, which is itself engineering work). The chapter should split this cleanly: tricks decay, specification discipline does not.
- **Does intrinsic self-critique ever help?** Generation/style tasks (Self-Refine) report gains; reasoning tasks (Huang) do not. Whether Self-Refine's gains are "real correction" or "rerolling toward the prompt's stylistic target" is unresolved.
- **Karpathy's "system prompt learning" as a third paradigm** — speculative, non-peer-reviewed, no controlled evaluation from Karpathy himself. Third-party implementations exist but are unvalidated.
- **Multimodal best practices** are genuinely unsettled — far less consensus than text-only; e.g., optimal *position* of an image relative to text in a prompt is reported to matter but lacks a settled rule.

### What has changed recently (last 5 years)

- 2022: self-consistency reframes "reasoning reliability" as a sampling/aggregation problem, not a metacognition problem.
- 2023: explosion of self-correction methods (Self-Refine, Reflexion, CoVe, RCI) — many over-claimed.
- Oct 2023: Huang et al. preprint puts the brakes on intrinsic self-correction; SoM shows visual marks beat fine-tuned grounding.
- 2024: Huang et al. formalized at ICLR; visual-prompting surveys consolidate the field.
- 2025: Wharton "Prompting Science" series empirically documents the *decay* of named tricks; Karpathy floats "system prompt learning" (May 2025).
- Oct 2025: CorrectBench preprint offers the intrinsic/external/fine-tuned taxonomy.

---

## 3. Application Domain Examples

- **Code generation (external grounding works):** an agent writes code, runs the test suite, reads the failures, and revises. This is grounded self-correction (Reflexion-style) and is reliable because the compiler/tests are an oracle. Contrast with asking the model "are you sure this code is correct?" with no execution — that is intrinsic and unreliable.
- **Math/reasoning (use self-consistency, not self-critique):** for GSM8K-style problems, sample 5–40 chains and majority-vote rather than asking the model to check its own work.
- **Open-ended writing/summarization (intrinsic refine is plausibly useful):** Self-Refine-style "critique your draft for completeness and tone, then rewrite" can help because the target is stylistic, not a single correct fact.
- **Visual QA / UI agents (multimodal):** Set-of-Mark — overlay numbered marks on screenshot regions so the model can reference "button 7" unambiguously; drives reliable grounding for GUI/agent tasks.
- **Document/chart understanding:** image-position effects — placing the image before vs. after the question text measurably changes accuracy; treat position as a tunable parameter, not an afterthought.

---

## 4. The Book's Thesis Connection

The chapter is where the book's thesis becomes self-aware. **The "specification quality > tricks" reframing IS the book's thesis**, stated in the field's own contested vocabulary: as frontier models follow instructions more faithfully, the *value of elaborate tricks* falls (Reports 2–4 document specific tricks decaying), while the value of *precise, falsifiable specification* — say exactly what you want, define success, and measure — rises. Wharton Report 1's "complicated and contingent" finding is not a refutation of prompt engineering; it is a mandate for the engineering stance the book argues for: **measure per task, don't trust universal recipes.**

The self-critique material is a direct mechanistic echo of two earlier chapters:
- **Ch. 4 sycophancy:** a model asked "are you sure?" tends to capitulate or over-revise — the same agreeableness/instability that produces sycophancy produces correct-to-incorrect flipping in intrinsic self-correction. Same mechanism, different surface.
- **Ch. 10 ReAct grounding:** the dividing line between self-correction that helps and self-correction that hurts is *external grounding*. Reflexion works because the feedback signal is real (tests, environment); intrinsic critique fails because the model is grading its own homework with the same faculties that produced the error. This is the ReAct lesson — reason *and act against the world* — applied to error-correction.

Mechanism-first framing for the drafter: **self-critique cannot create information the model didn't already have.** Majority-vote (self-consistency) extracts signal from the answer *distribution*; external tools inject *new* information. Pure intrinsic reflection does neither — so on a single-answer task it can only add noise.

---

## 5. The AI Wayback Machine — Candidate Figures

(Choose 2–3. Lesser-known preferred; all substantively connected to self-reference/recursion, error-correction, metacognition, or perception/vision.)

1. **Walter Pitts** (Wikipedia: "Walter Pitts"). Self-taught logician, co-author with McCulloch of the 1943 "A Logical Calculus of the Ideas Immanent in Nervous Activity" — the first formal model of a neuron and a founding text of self-referential, feedback-based computation. CONNECTION: recursion/self-reference at the origin of neural computation; metacognition's deep ancestry. Lesser-known (overshadowed by McCulloch). Anchor prompt: *"A homeless, self-taught logician sleeps in a professor's house and, in the evenings, helps invent the mathematical neuron — the recursive feedback element underneath every model that now tries, and fails, to check its own reasoning."* SKEW FLAG: mid-20th-c. American academic context; tragic biography (alcoholism, isolation) — handle with care, not as inspiration-porn.

2. **Heinz von Foerster** (Wikipedia: "Heinz von Foerster"). Architect of **second-order cybernetics** — "the cybernetics of *observing* systems," explicitly about self-reference and the observer who is part of the system observed. CONNECTION: a model critiquing its own output is the literal computational instance of von Foerster's "observing system observing itself" — and his work warns that self-observation is not neutral. Lesser-known outside cybernetics. Anchor prompt: *"The control of control, the communication of communication — a 1970s cybernetician asks what happens when a system tries to observe itself, half a century before we asked a language model to check its own answer."* SKEW FLAG: European émigré intellectual tradition; abstract/philosophical, risk of obscurity — keep the link to the concrete failure mode tight.

3. **David Marr** (Wikipedia: "David Marr (neuroscientist)"). *Vision* (1982) and the three levels of analysis (computational / algorithmic / implementational). CONNECTION: perception/vision lineage for the multimodal section; Marr's insistence on separating *what* problem vision solves from *how* it's implemented is the cleanest historical frame for "what does a multimodal prompt actually ask the model to compute?" Anchor prompt: *"Before any machine could see, a dying neuroscientist insisted you first say precisely what 'seeing' is for — the computational level — a discipline today's multimodal prompting still mostly skips."* SKEW FLAG: posthumous canonization can flatten the controversy (Gibsonian critiques); note vision research had rival schools.

---

## 6. Pedagogical Delivery Research

- **Lead with the negative result.** The most memorable, counterintuitive hook is Huang et al.: "asking a model to double-check itself often makes it *worse*." Students arrive assuming self-correction is obviously good; the puzzle drives the chapter.
- **Teach the decision rule, not the technique list.** The durable lesson is a *predicate*: "Is there an external, verifiable feedback signal? If yes, self-correction can help; if no, prefer self-consistency or accept the first answer." Give them the predicate, then the methods slot under it.
- **Use the trick-decay table as a humility lesson.** The Wharton Reports (persona, CoT, threats all decaying) are perfect for teaching "your favorite prompt hack has a half-life; measure it on your task."
- **Make the obsolescence question a debate exercise.** Have students argue both sides ("tricks are dying" vs. "specification engineering is forever") using the cited evidence — productive because the resolution is a *distinction*, not a winner.
- **Multimodal: a hands-on contrast.** Have students try a grounding task with plain "describe the object on the left" vs. Set-of-Mark numbered regions; the difference is vivid and immediate.
- **Flag the speculative clearly.** Karpathy's "system prompt learning" is great for imagination but must be labeled non-peer-reviewed; good for teaching students to distinguish a provocative tweet from a result.

---

## 7. Representation and Display Research

Two displays warranted:

**(A) Self-correction decision tree (grounded vs. ungrounded).** Root: "Does the task have a single verifiable answer?" → branch. If a verifiable external signal exists (compiler, tests, search, execution, environment reward) → "Grounded correction — Reflexion-style — RELIABLE." If single-answer but no external signal → "Use self-consistency (sample + majority vote), NOT self-critique." If open-ended/stylistic → "Intrinsic Self-Refine may polish; will not fix facts." Terminal warning node on the bare-intrinsic-reasoning path: "Risk: correct-to-incorrect flipping (Huang 2024)."

**(B) Intrinsic / External / Fine-tuned taxonomy table** (from CorrectBench, arXiv:2510.16062):

| Category | Feedback source | Representative methods | Reliability on reasoning | Cost |
|---|---|---|---|---|
| Intrinsic | Model's own judgment, no tools | Self-Refine, CoVe, RCI | Low — can degrade (Huang 2024) | Low–med (extra passes) |
| External | Tools / search / execution / tests | Reflexion (w/ tests), tool-augmented | High when signal is verifiable | Med–high (tool calls) |
| Fine-tuned | A model trained to correct | Correction-tuned models | Mixed; data-dependent | High (training) |

These two should be the chapter's visual spine. Everything else (multimodal, obsolescence) can run as prose + the Wharton trick-decay table if a third figure is wanted.

---

## 8. Open Questions and Research Gaps

- **When (if ever) does intrinsic self-critique help reasoning?** Is there a model-capability threshold above which self-correction becomes net-positive without tools? Unresolved.
- **Reconciling Self-Refine vs. Huang:** is Self-Refine's reported gain genuine error-correction or stylistic re-rolling toward the prompt target? No clean experiment isolates this.
- **CorrectBench durability:** single Oct-2025 preprint; its percentage results need independent replication before textbook reliance.
- **Does "system prompt learning" produce measurable gains?** No controlled evaluation from Karpathy; third-party SPL plugins are unvalidated. Open.
- **Obsolescence trajectory:** which tricks decay next as models improve, and is there an asymptote where only specification quality remains? The Wharton series is one longitudinal probe; more needed.
- **Multimodal best practices are pre-paradigmatic:** no settled rule for image-vs-text ordering, number/style of marks, or when visual prompting beats textual description. Largest genuine gap in the chapter.

---

## 9. Sourcing Notes

- **Karpathy "system prompt learning" — VERIFIED as a tweet, NOT a paper or formal talk.** Dated May 7, 2025 (x.com/karpathy/status/1921368644069765486). Must be labeled non-peer-reviewed opinion/speculation. Distinguish Karpathy's *proposal* from third-party *implementations* (optillm SPL plugin by "codelion") which are unvalidated. His broader "Software 3.0" content was a talk (Latent Space writeup); the specific "system prompt learning" framing is the tweet.
- **CorrectBench — CORRECTED.** It is arXiv:2510.16062 (Oct 2025), a recent preprint, NOT an established benchmark. The intrinsic/external/fine-tuned taxonomy IS confirmed and useful; the specific percentage claims (5.2% on MATH, ~40% slower hybrids) should be cited as single-preprint and flagged pending peer review.
- **Wharton/Meincke–Mollick — REFINED.** The spine's "systematic prompting beats casual prompting" is too strong. Actual Report 1 finding: prompt effects are "complicated and contingent" — hard to predict, scoring-standard-dependent. Reports 2–4 document specific tricks (CoT, personas, threats/tips) *losing* value. This nuance strengthens, not weakens, the book's thesis. Confirm Report 4 exact publication date (SSRN 5879722) before citing year.
- **All five core citations VERIFIED** (authors/title/year/venue/arXiv): Huang 2024 ICLR (2310.01798); Wang 2023 ICLR (2203.11171, submitted 2022); Shinn 2023 NeurIPS (2303.11366); Madaan 2023 NeurIPS (2303.17651); Yang 2023 (2310.11441).
- **Added beyond spine (count: 6):** Self-Refine (Madaan); the two VLM prompting surveys (Gu et al. 2307.12980; Wu et al. 2409.15310); Wharton Reports 2, 3, and 4. Plus three Wayback figures (Pitts, von Foerster, Marr).
- **Unverifiable / needs confirmation:** Wu et al. 2409.15310 full author list (title + arXiv confirmed); Wharton Report 4 exact date and full author order; CorrectBench peer-review status and its reported percentages; all third-party "system prompt learning" implementation claims.
- **Reflexion classification note for the drafter:** Reflexion is frequently miscited as evidence that "self-reflection works." It works *because of an external feedback signal* — place it on the grounded/external side, not as a vindication of intrinsic self-critique.
- **No fetches were blocked.** All findings from WebSearch result summaries; the drafter should open the arXiv abstracts directly to pull exact quotes/numbers before final citation.
