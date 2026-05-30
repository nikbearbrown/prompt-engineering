# Research: Candidate Chapter §3 — Long-Context Prompting: Position Effects
## Prompt Engineering
**Chapter one-line:** How models use (and misuse) position in long contexts — Lost-in-the-Middle, multi-needle collapse, and injection risk.
**Research date:** 2026-05-29
---

## 1. Primary Sources

### Foundational papers and texts

- **Liu, N. F., Lin, K., Hewitt, J., Paranjape, A., Bevilacqua, M., Petroni, F., & Liang, P. (2024). "Lost in the Middle: How Language Models Use Long Contexts."** *Transactions of the Association for Computational Linguistics (TACL)*, Vol. 12, pp. 157–173. **VERIFIED.** arXiv:2307.03172 (preprint July 2023). DOI: 10.1162/tacl_a_00638. ACL Anthology: 2024.tacl-1.9. Code/data: github.com/nelson-liu/lost-in-the-middle. The canonical spine source. Two tasks: multi-document QA and synthetic key–value retrieval. Finding: accuracy is highest when the relevant document/key sits at the beginning (primacy) or end (recency) of the input, and drops sharply when it must be accessed from the middle — a **U-shaped curve**. Holds even for explicitly long-context models. (Note: TACL is a journal with rolling publication; the 2024 volume assignment and 2023 arXiv date are both correct — do not "correct" one against the other.)

- **Hsieh, C.-P., Sun, S., Kriman, S., Acharya, S., Rekesh, D., Jia, F., Zhang, Y., & Ginsburg, B. (2024). "RULER: What's the Real Context Size of Your Long-Context Language Models?"** **VERIFIED.** arXiv:2404.06654 (NVIDIA). Argues the vanilla needle-in-a-haystack (NIAH) test measures only *superficial* retrieval. RULER extends NIAH with (a) multi-needle and multi-key variants, (b) **variable tracking** (multi-hop coreference proxy), and (c) **common/frequent-word extraction** (aggregation/summarization proxy). Central result: nominal context windows overstate *effective* context — most models' real usable length is far below their advertised token limit. Synthetic tasks, so no LLM-as-judge needed.

- **Hsieh, C.-Y. et al. (2024). "Found in the Middle: Calibrating Positional Attention Bias Improves Long Context Utilization."** **VERIFIED.** arXiv:2406.16008; ACL 2024 Findings (2024.findings-acl.890). Mechanism-level companion to Liu et al.: shows the U-shaped *accuracy* curve maps onto a U-shaped *attention* bias — tokens at the start and end receive higher attention **regardless of relevance**. Proposes a training-free, inference-time calibration ("found-in-the-middle") that subtracts the positional-bias component from attention weights, recovering up to **15 percentage points** of RAG accuracy. Critical for the book's mechanism-first framing: position bias is partly an *attention* artifact, not only a training-data artifact.

- **Anil, C., Durmus, E., Panickssery, N., Sharma, M., Benton, J., ... Perez, E., Grosse, R., Duvenaud, D. (2024). "Many-shot Jailbreaking."** **VERIFIED.** Anthropic; NeurIPS 2024 (proceedings hash ea456e232efb72d261715e33ce25f208); public report at anthropic.com/research/many-shot-jailbreaking (2024-04-02). Long-context attack: hundreds of faux dialogue turns demonstrating the unwanted behavior, placed *in context*, override alignment. Attack strength scales with shot count (near-zero at 5 shots, reliable at 256) following a power-law in log(shots). Demonstrated on GPT-3.5/4, Claude 2.0, Llama 2 70B, Mistral 7B. Relevance: shows long context is not just a recall problem but an *attack surface*; in-context demonstrations exploit the same positional/recency machinery.

- **NINJA — "Jailbreaking in the Haystack" (2025).** **VERIFIED as the source of the 58.8% figure.** arXiv:2511.04707; OpenReview hYZ03uKVO7. NINJA = Needle-IN-haystack JAilbreak. Appends benign, model-generated, thematically relevant filler to a harmful goal and varies the goal's *position*. On HarmBench, ASR improves **from 23.7% → 58.8% for Llama-3.1-8B-Instruct**, 23.7% → 42.5% for Qwen2.5-7B-Instruct, and 23% → 29% for Gemini Flash. Explicitly attributes the effect to the same **U-shaped primacy/recency** bias: harmful goal at the *beginning* maximizes ASR; placing it at the *end* mitigates. **Correction to the spine:** 58.8% is the *post-attack ASR for one specific model (Llama-3.1-8B)*, up from a 23.7% baseline — not a universal ceiling. State it as "up to 58.8% on Llama-3.1-8B, from a 23.7% baseline," not "up to 58.8% attack success" in the abstract.

### Key empirical cases

- **Greg Kamradt — "Needle In A Haystack" pressure tests (Nov 2023).** Repo: github.com/gkamradt/LLMTest_NeedleInAHaystack. Origin of the popular NIAH visualization. Method: insert the out-of-place sentence "The best thing to do in San Francisco is eat a sandwich and sit in Dolores Park on a sunny day" at varying depths (0–100%) across context lengths (1K → model max) drawn from Paul Graham essays. GPT-4-128K: recall degrades above ~73K tokens, weakest at 7–50% depth. Claude 2.1-200K: near-100% at very top and very bottom, degradation at depth starting ~90K. (Threads: x.com/gregkamradt/status/1722386725635580292 and /1727018183608193393.)

- **LangChain — "Multi Needle in a Haystack" (blog.langchain.com/multi-needle-in-a-haystack).** Extended Kamradt's repo to N needles + LangSmith eval. GPT-4-128K asked to retrieve 1, 3, or 10 needles. Retrieval drops as needle count rises and as context lengthens; needles placed earlier in a long context are retrieved less reliably — consistent with recency dominance.

- **Multi-needle synthesis collapse (multiple sources).** Single-fact retrieval ≈95–96% on modern models (Gemini-1.5, GPT-4o); **three target sentences in English drops to ~40%** per multilingual NIAH work (arXiv:2409.18006). This is the empirical basis for the spine's "multi-needle synthesis drops to ~60%" claim — **CORRECTION: the literature figure is closer to ~40% for 3 needles in English**; "~60%" is optimistic. Cite the specific n-needle number rather than a round "60%."

---

## 2. The Core Concept — State of the Field

### What is settled
- The **U-shaped position–accuracy curve** is robust and replicated (Liu et al. 2024; Found-in-the-Middle 2024; NINJA 2025; production RAG reports). Best recall at the extremes, worst in the middle.
- **Single-needle retrieval is largely solved** on frontier models (~95%+); it is a weak proxy for real long-context competence (RULER).
- **Effective context << advertised context.** Most models hold consistent accuracy only well below their nominal token limit (RULER; Databricks "Long Context RAG Performance," arXiv:2411.03538).
- **Adding more documents can hurt.** Beyond a point, larger top-k *lowers* recall of the correct fact — the lost-in-the-middle penalty swamps the recall gain.
- Position bias has an **attention-level signature**: start/end tokens get more attention irrespective of relevance (Found-in-the-Middle).

### What is disputed
- **How much is fixable.** Found-in-the-Middle recovers ~15 pts via inference-time calibration, implying part of the bias is a correctable attention artifact — tension with the "recency is an unfixable autoregressive artifact" framing. Honest position: recency has a *training-induced* component (autoregressive next-token objective) **and** an *architectural attention* component; the latter is partially correctable, the former less so.
- **Whether long context obsoletes RAG.** Ongoing; long-context RAG papers show retrieval still helps but introduces its own positional failures.
- **The exact multi-needle degradation curve** varies by model, language, needle similarity, and distractor design — no single number generalizes.

### What has changed recently (last 5 years)
- 2023: NIAH popularized (Kamradt); Lost-in-the-Middle preprint.
- 2024: TACL publication; RULER reframes evaluation; Found-in-the-Middle gives mechanism + fix; Many-shot Jailbreaking weaponizes long context.
- 2025: NINJA shows safety itself is position-dependent (the 58.8% result); theory papers (e.g., "Lost in the Middle at Birth," arXiv:2603.10123) attempt exact accounts of transformer position bias.

---

## 3. Application Domain Examples

- **RAG document ordering (documented).** Standard production practice: rerank retrieved chunks so the highest-relevance passages sit at the *start and end* of the assembled context, deliberately exploiting the U-curve. Reranking + hybrid search + intelligent positioning is the de facto fix (DigitalOcean, Snorkel, Atlan RAG-failure writeups). Documented failure: teams that raise top_k to "improve recall" instead *lose* the correct fact to middle-burial.
- **Agent context assembly (documented pattern, mixed evidence).** Long agent loops accumulate tool outputs and history; the oldest-but-still-relevant instruction drifts into the middle and gets ignored. "Context bloat" / "retrieval thrash" failure modes (Towards Data Science agentic-RAG writeup). Mitigation: re-inject the goal/constraints at the *end* of each turn.
- **System-prompt placement (settled practice, mechanism-backed).** Because recency persists even near the window limit, the highest-priority instructions and safety rules belong at the **end** of the assembled prompt — this both maximizes compliance (recency) and reduces adversarial override (NINJA: goal-at-end mitigates ASR).
- **Hypothetical (LABELED).** *A legal-discovery assistant fed 300 pages where the one exonerating clause sits at page 150 and is silently skipped.* Plausible given the U-curve but not a cited incident — present as illustration only.

---

## 4. The Book's Thesis Connection

Mechanism-first: the U-shaped curve is not a "quirk" to memorize but a predictable consequence of how these systems are built.

- **Recency ← autoregressive pretraining.** Next-token prediction conditions most heavily on the immediately preceding tokens; the objective itself rewards weighting recent context. This is structural, not a bug — hence recency is *stable* across context length and only partially "fixable."
- **Primacy ← attention sinks + early-token over-attention.** The start of the sequence receives outsized attention (the attention-sink phenomenon; Found-in-the-Middle's start-token bias). Primacy is *weaker* and *decays* as the window fills, because early tokens compete with ever more material — matching Kamradt's observation that top-of-document recall holds better than mid-document at extreme lengths but degrades as total length grows.
- **Falsifiable placement rules** (the book's deliverable):
  1. *Put the highest-priority instruction last.* Falsifiable: move it to the middle and measure compliance drop.
  2. *Put critical retrieved facts at the extremes, filler in the middle.* Falsifiable: A/B the rerank order, measure answer accuracy.
  3. *Put safety constraints at the end, never let user content be the last thing.* Falsifiable: NINJA-style position sweep should show lower ASR with rules-last.
  4. *Don't trust single-needle benchmarks as evidence of synthesis ability.* Falsifiable: run a 3-needle synthesis task and watch accuracy fall toward ~40%.
- **Named failure modes** to give the reader: *Lost-in-the-Middle*, *Multi-needle collapse*, *Silent contradiction resolution* (model picks one of two conflicting facts — usually the more recent — without flagging the conflict), *Position-induced jailbreak* (harmful goal at the front).

---

## 5. The AI Wayback Machine — Candidate Figures

*Serial-position effects in human memory are the deep prior for the U-curve. Diverse, lesser-known-preferred.*

1. **Hermann Ebbinghaus** (Wikipedia: "Hermann Ebbinghaus"). German psychologist, founder of experimental memory research; ran nonsense-syllable recall studies on himself in the 1880s and is credited with first describing position-dependent recall. *Anchor prompt:* "Explain Ebbinghaus's serial-position findings and map primacy/recency onto the U-shaped accuracy curve in long-context LLMs — where is the analogy tight, and where does it break?" *Skew flag:* attribution of "serial-position effect" coinage to Ebbinghaus is widely repeated but loosely sourced; present as origin of the *research program*, not a single coined term.

2. **Bennet B. Murdock Jr.** (Wikipedia: "Bennet Murdock" / cited via "Serial-position effect"). His 1962 paper *The serial position effect of free recall* (J. Exp. Psychol., 64, 482–488) gave the canonical empirical curve: steep primacy over the first 3–4 items, S-shaped recency over the last ~8, flat middle asymptote — visually the same shape as Liu et al.'s plot. *Anchor prompt:* "Compare Murdock's 1962 free-recall curve to a needle-in-a-haystack depth plot. What would it mean if an LLM's curve had a *flatter* middle than a human's?" *Skew flag:* lesser-known to a CS audience; good for de-anthropomorphizing the analogy (the *mechanisms* differ — short-term store vs. attention weighting — even when the *shapes* match).

3. **Claude Shannon** (Wikipedia: "Claude Shannon") — information-theory framing. Channel capacity and the data-processing inequality give language for *why cramming more into context can reduce usable information*: a fixed-capacity channel (effective attention budget) means added low-value tokens crowd out signal. *Anchor prompt:* "Frame lost-in-the-middle as an information-bottleneck problem: if attention is a finite-capacity channel, why does increasing top-k retrieval sometimes lower answer accuracy?" *Skew flag:* this is an *analogy*, not a derivation — Shannon capacity doesn't literally govern attention; flag as conceptual scaffolding.

---

## 6. Pedagogical Delivery Research

- **Lead with the human prior, then break it.** Open with the serial-position effect students already feel (you remember the start and end of a grocery list, not the middle), then show the LLM curve looks the same — then insist the *mechanisms differ* (no short-term store; it's attention + autoregression). The pedagogical payoff is precisely puncturing the too-easy analogy.
- **Show the picture first.** The Kamradt heatmap (depth × context-length, color = recall) is one of the most recognizable images in applied LLM work; students grasp it instantly. Use it as the hook, then move to the cleaner U-curve line plot for the mechanism discussion.
- **Single-needle vs. multi-needle as a "gotcha."** Have students predict accuracy for 1 vs. 3 needles, then reveal the ~95% → ~40% drop. Teaches the broader lesson: a benchmark that looks solved (single-needle) can hide the real failure (synthesis).
- **Hands-on position sweep.** A copy-paste exercise: same question, same fact, fact placed at start / middle / end of a 50-page filler; students measure compliance/accuracy themselves. Directly operationalizes the falsifiable rules in §4.
- **Tie security to placement.** Use NINJA's goal-at-front result to show that "put instructions last" is not just a quality tip but a *safety* control — connects §3 to the book's safety thread.

---

## 7. Representation and Display Research

**Two displays warranted.**

1. **U-shaped accuracy-vs-position curve.** X-axis = position of relevant info in context (0% = start → 100% = end). Y-axis = task accuracy. One curve high at both ends, sagging in the middle. Overlay (dashed) a human free-recall curve (Murdock shape) to make the analogy and its limits visible. Annotate the two humps: "primacy (weaker, decays with length)" and "recency (stable, autoregressive)."

2. **Placement-strategy diagram.** A schematic prompt block showing recommended layout: [system role / low-priority context]top → [filler / mid-relevance retrieved docs]middle → [highest-priority instruction + safety rules + most-relevant facts]end. Annotate with the falsifiable rules and a small inset showing the NINJA finding (harmful goal at front = high ASR; constraints at end = lower ASR). Mechanism labels: "recency persists near window limit," "primacy decays as context fills."

(Optional third: the Kamradt-style depth × length heatmap, if a reproduced/licensed version is available — otherwise describe it in prose and cite the repo.)

---

## 8. Open Questions and Research Gaps

- **How much of recency bias is truly unfixable?** Found-in-the-Middle's 15-pt calibration recovery argues part is a correctable attention artifact. The book should hold the *autoregressive* component and the *attention-sink* component apart rather than calling all of it unfixable.
- **No generalizable multi-needle degradation law.** The ~40% (3-needle, English) figure is model-, language-, and distractor-dependent. An open need: a RULER-style standardized synthesis benchmark with reported confidence intervals.
- **Contradiction handling.** The claim that models "fail to signal uncertainty and pick the most recent" of two conflicting facts is intuitive and partially supported by recency bias, but I did **not** find a single clean primary citation isolating *position-driven contradiction resolution with calibration failure*. **Flag as under-sourced**; present as a reasoned prediction from recency bias, not an established result, unless a dedicated study is located.
- **Does scaling effective context close the gap?** Long-context RAG papers (arXiv:2411.03538) suggest effective context is improving but still lags nominal limits — unresolved whether the U-curve flattens or just shifts.
- **Defense durability of "instructions-last."** NINJA shows goal-at-end mitigates, but a determined attacker controls *their* content's position; how robust the recency defense is against adaptive attacks is open.

---

## 9. Sourcing Notes

- **Verified citations:** Liu et al. 2024 (TACL Vol. 12 pp. 157–173; arXiv:2307.03172; DOI 10.1162/tacl_a_00638) ✓. RULER, Hsieh et al. (arXiv:2404.06654) ✓. Found-in-the-Middle (arXiv:2406.16008; ACL 2024 Findings) ✓. Many-shot Jailbreaking, Anil et al. (NeurIPS 2024; Anthropic 2024-04-02) ✓. Kamradt NIAH repo + threads ✓. LangChain multi-needle blog ✓.
- **The 58.8% figure — RESOLVED & CORRECTED.** Source is **NINJA, "Jailbreaking in the Haystack," arXiv:2511.04707** (2025). Exact claim: ASR rises **from 23.7% baseline to 58.8% for Llama-3.1-8B-Instruct** on HarmBench (also 42.5% Qwen2.5-7B, 29% Gemini Flash). Spine phrasing "up to 58.8% attack success" is *literally accurate* but should be stated with the 23.7% baseline and model name to avoid implying a universal ceiling.
- **Multi-needle "~60%" — CORRECTED.** Literature reports ~40% for 3 English needles (arXiv:2409.18006); cite the specific n-needle number, not a round 60%.
- **Contradiction-resolution claim — UNVERIFIED.** No clean primary source isolating position-driven silent contradiction resolution; flagged as a reasoned prediction.
- **Added primary sources beyond spine (4+):** Found-in-the-Middle (attention mechanism + fix); RULER (evaluation reframing); multilingual NIAH arXiv:2409.18006 (multi-needle numbers); Databricks long-context RAG arXiv:2411.03538 (effective vs. nominal context). Plus NINJA located as the 58.8% source.
- **Fetch status:** arXiv full-text fetches blocked by Cowork web_fetch rate limit (HTTP 429) on this run; all figures above were confirmed via WebSearch result snippets quoting the source abstracts/papers directly. Recommend a verification pass fetching arXiv:2511.04707 and arXiv:2409.18006 PDFs to confirm exact table numbers before print.
- **Wayback skew:** Ebbinghaus coinage attribution is loosely sourced (flagged); Shannon framing is analogy not derivation (flagged); Murdock is the most defensible empirical anchor.
