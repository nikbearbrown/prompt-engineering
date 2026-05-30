> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft.

---

# Chapter 15 — Production, Ethics, and What Comes Next

*From notebook to monitored pipeline, and the debates that outlive any one model*

**Author:** Nik Bear Brown

**Editor:** Nik Bear Brown

---

## Suggested titles

1. **Production, Ethics, and What Comes Next**
2. **The Prompt That Worked in the Notebook and Failed in the Pipeline**
3. **Tricks Decay, Discipline Doesn't: Closing the Loop on Prompt Engineering**

---

## TL;DR

A prompt that works in a notebook is not a system. Putting it into production means versioning it, building an evaluation harness that catches the brittleness of Ch. 9 before users do, and monitoring it because the model underneath you will change without asking. This closing chapter does three things. First, it walks the production lifecycle — version, evaluate, monitor — and ties it explicitly to the brittleness results that make casual deployment reckless. Second, it treats ethics not as an afterthought but as a *design constraint*: bias amplification, the concentration of power, and responsibility you cannot delegate to the model. Third, it adjudicates three live debates — is prompting obsolescing? does self-critique help? is multimodal prompting different? — and uses them to state the book's thesis in the field's own contested vocabulary: **specification quality and evaluation discipline, measured per task, outlast every trick.** The keystone result is uncomfortable and well-replicated: a model asked to check its own reasoning, with no external grounding, often gets *worse*.

---

## Learning objectives

By the end of this chapter you should be able to:

1. **Move** (Create) a working prompt from notebook to a monitored pipeline with versioning, an eval harness, and drift monitoring, justifying each component from the brittleness results of Ch. 9.
2. **Evaluate** (Evaluate) bias-amplification and power-concentration risks of a deployed prompt system and treat responsibility as a non-delegable design constraint.
3. **Apply** (Apply) the grounded-vs-ungrounded decision rule to choose between self-consistency, externally-grounded self-correction, and intrinsic self-refinement.
4. **Evaluate** (Evaluate) the obsolescence debate by distinguishing decaying *tricks* from durable *specification discipline*, citing the empirical evidence on both sides.
5. **Analyze** (Analyze) how failure mechanisms compound across the book — e.g., how RLHF-driven sycophancy (Ch. 4) interacts with persona drift (Ch. 6), and how ReAct brittleness (Ch. 11) connects to eval discipline (Ch. 9).

## Prerequisites

The whole arc, but especially: Ch. 4 (Sycophancy) — the approval-maximization mechanism that reappears in self-correction failure. Ch. 6 (Persona and Audience Patterns) — persona effects, here shown decaying. Ch. 9 (Prompt Brittleness and Evaluation) — the empirical spine this chapter operationalizes for production. Ch. 11 (Agentic and Multi-Turn Systems) — the ReAct loop whose external grounding is the dividing line of §15.4.

---

## 15.1 The prompt that worked in the notebook

Madison's marketing-intelligence team has a prompt they love. In a notebook, against a handful of hand-picked product briefs, it produces clean campaign-angle summaries with the right tone and no hallucinated claims. Someone says the obvious thing: "ship it." So they wire it into the content pipeline behind an API endpoint, and for two weeks it is wonderful.

Then three things happen, none of them dramatic on its own.

First, the inputs widen. The notebook briefs were tidy; the production briefs include a French-language brief, a brief with a 4,000-word appendix, and a brief that is mostly a competitor's pasted press release. The prompt that was tuned on tidy English briefs degrades on the messy real distribution — and degrades *silently*, because nobody is scoring the outputs anymore.

Second, the provider updates the model. The version string the team never pinned rolls from one snapshot to the next. The new snapshot is, on average, better — and on Madison's specific prompt, measurably different: it now front-loads a summary the old one buried, which breaks the downstream parser that expected the old format. This is Ch. 9's lesson arriving with a bill: the same prompt, a slightly different model, a different output shape. **Brittleness is not hypothetical; it is the default behavior of an unversioned, unmonitored prompt sitting on top of a moving model.**

Third — and this is the one that should worry an ethics reviewer — the system starts amplifying a pattern. Because the briefs that perform best in the team's A/B metric skew toward a particular demographic's language, the prompt, doing exactly what it was rewarded to do, begins producing campaign angles that lean harder into that skew with each iteration. No one decided this. The pipeline did, and the pipeline had no one watching the distribution of *who* it was speaking to and for.

None of these failures is a wording problem. You cannot "ask better" your way out of an unpinned model version or an unmonitored bias drift. They are *systems* problems, and the discipline that catches them is the same discipline the whole book has been building toward: specify precisely, evaluate empirically, and monitor continuously. This chapter closes the loop. It takes the notebook prompt to a monitored pipeline (§15.2), treats the bias drift as the design constraint it is (§15.3), and then steps back to the field's three live debates (§15.4–15.6) — which, read together, say the same thing the book has said from Ch. 1: tricks decay, discipline does not.

---

## 15.2 From notebook to monitored pipeline

A notebook prompt and a production prompt system differ the way a sketch differs from a building that has to stand up in weather. Three components turn one into the other.

### Versioning

The minimum discipline: **a prompt is an artifact with a version, and so is the model it runs against.** Madison's parser broke because the model version was implicit — "whatever the provider serves today." Pin it. Treat the (prompt-text, model-snapshot, decoding-parameters) triple as the versioned unit, because Ch. 1 established that even temperature and top-p change the output distribution, and Ch. 9 established that trivial format changes change the score. A prompt without its model snapshot and decoding settings is not reproducible, and an unreproducible prompt cannot be evaluated, only admired.

In practice: prompts live in version control, not in notebook cells; changes go through review like code; and every deployed version records the model snapshot and parameters it was validated against. When the provider ships a new snapshot, that is a *new configuration to re-validate*, not a free upgrade.

### Evaluation harnesses

This is where Ch. 9 becomes operational. A single test case — the notebook's tidy brief — tells you nothing about brittleness. An eval harness is a held-out set of inputs spanning the real distribution (Madison's French brief, the 4,000-word appendix, the press-release brief) scored by a defined metric. Two non-negotiables carried forward from Ch. 9:

- **Test across variants, not a single prompt.** Brittleness means a prompt's score swings under paraphrase, reordering, and format change. An eval that runs one phrasing measures luck, not quality. Run the variant battery and report the *distribution* of scores, not the best one.
- **Fix the scoring standard before you measure.** Wharton's Prompting Science Report 1 (Meincke et al. 2025) found that the *choice of scoring standard* swings benchmark results dramatically — the same outputs look good or bad depending on how you score them. So the standard is part of the experiment, declared up front, not chosen after seeing results. (This is the same point Ch. 9 made; here it gates whether you may ship.)

The harness runs in CI: a prompt change or a model-snapshot change must clear the held-out evals before it deploys. That is the line between engineering and vibes.

### Monitoring

Evals catch what you anticipated; monitoring catches what you didn't. Production inputs drift (Madison's input distribution widened), models update underneath you, and quality degrades in ways no offline set predicted. Minimum monitoring: sample live inputs and outputs, score them against the same standard the harness uses, and alert when the score distribution shifts or when the input distribution drifts away from what the harness covers. The bias drift in §15.1 is exactly a monitoring failure — a distributional shift in *who the outputs served* that no one was watching.

> **The thread to Ch. 9.** Production is where brittleness stops being a lab curiosity and becomes an incident. Every component here exists because the same prompt, lightly perturbed — a reworded input, a new model snapshot, a reordered few-shot — produces a different output. Versioning makes the perturbation visible; the eval harness measures its effect before users do; monitoring catches the perturbations you didn't enumerate. Skip them and you are betting your system on the prompt being robust, which Ch. 9 told you it is not.

A misconception to retire: "the model keeps getting better, so production prompts get *more* stable over time." The opposite is the realistic default. Each model update is an unrequested change to the configuration you validated. Better-on-average does not mean better-on-your-prompt, and "better" can still break a parser. Stability is something you engineer with pinning and re-validation, not something the provider hands you.

---

## 15.3 Ethics as a design constraint

It is tempting to treat ethics as a review step at the end — a checklist before launch. This chapter argues the opposite: the consequential ethical properties of a prompt system are *architectural*, set by design decisions you make early, and a checklist at the end cannot retrofit them. Three constraints.

### Bias amplification

A prompt system does not merely inherit the model's biases; it can *amplify* them through feedback. Madison's pipeline is the mechanism in miniature: an optimization target (the A/B metric) that correlates with a demographic skew will, iteration over iteration, push outputs further into that skew, because that is what the metric rewards. The bias is not in any single output you would flag in review; it is in the *distribution* the system converges toward, which is invisible at the level of individual outputs and visible only in aggregate monitoring.

This is why bias is a design constraint, not a review item. The decisions that determine it — what you optimize for, whose language your evals over-represent, whether you monitor the output distribution by audience — are made when you build the harness, not when you inspect a sample. The architectural fix is to put fairness-relevant distributions into the eval harness and the monitoring as first-class metrics, so the drift in §15.1 trips an alert instead of compounding for two weeks.

### Power and concentration

Ch. 14 ended on a sharp consequence: a single engineer can now direct a fleet of coding agents across a codebase. Generalize it. Prompt systems let a small number of people act at a scale that used to require many — which concentrates the power to shape information, automate decisions, and displace labor in fewer hands. This is a labeled judgment, not a theorem: I claim that the *concentration* effect is the ethically load-bearing one, more than any single biased output, because it determines who gets to set the optimization targets in the first place. A system that amplifies one group's preferences at scale is a power fact before it is a fairness fact.

### Responsibility you cannot delegate

The most common evasion in deployed systems is to treat the model as the responsible party — "the model said it," "the model decided." It did not decide; it sampled from a distribution your prompt and your training pipeline shaped. Ch. 2's plausibility–truth gap and Ch. 4's sycophancy both make the point: the model produces fluent, agreeable output whether or not it is correct or fair, so the human who specified the system and chose to deploy it carries the responsibility for what it does. Responsibility is non-delegable to a stochastic process. Designing as if it were — shipping without monitoring, then pointing at the model when it drifts — is the failure §15.1 dramatizes.

---

## 15.4 The self-critique debate: when does checking help?

Here is the chapter's most counterintuitive result, and the cleanest illustration of why mechanism beats intuition. Students arrive certain that asking a model to check its own work must help — double-checking is obviously good. It often makes things **worse.**

Huang et al. (2024, ICLR), "Large Language Models Cannot Self-Correct Reasoning Yet," is the keystone. The finding: *intrinsic* self-correction — asking the model to review and revise its reasoning with **no external feedback** — does not reliably improve accuracy on reasoning tasks and frequently *degrades* it. Models flip correct answers to incorrect ones. The apparent gains in earlier self-correction papers, it turns out, leaned on an oracle: ground-truth labels used to decide *when to stop* correcting. Remove the oracle — let the model decide for itself whether to revise — and accuracy on GSM8K-style tasks drops. The documented, reproducible failure mode is **correct-to-incorrect flipping.**

The mechanism is the one Ch. 2 and Ch. 4 already gave us, and naming it is the point. **Self-critique cannot create information the model didn't already have.** When you ask "are you sure?", you invoke the same faculties that produced the answer — the model grades its own homework with the pencil that made the error. And the agreeableness that Ch. 4 traced to RLHF (the model is trained to be approval-maximizing, to capitulate when pushed) is exactly the pressure that makes "are you sure?" tip a correct answer toward revision. **Sycophancy and over-revision are the same mechanism wearing two faces.** A model asked to reconsider treats the request as social pressure to find *something* to change.

So when does checking help? The dividing line is **external grounding**, and it gives a decision rule you can apply mechanically:

- **Does the task have a single verifiable answer?**
  - **No external signal, single answer (math, reasoning):** use **self-consistency** (Wang et al. 2023, ICLR) — sample $k$ diverse reasoning paths at temperature $> 0$ and take the **majority-vote** answer. Reported gains over single-shot CoT: GSM8K +17.9%, SVAMP +11.0%, AQuA +12.2%. The crucial property: self-consistency improves *without asking the model to judge itself.* It extracts signal from the structure of the answer *distribution* — marginalizing over reasoning paths — not from metacognition. It cannot flip-to-incorrect because it never asks "are you sure?"; it asks "what answer recurs?"
  - **External verifiable signal exists (compiler, unit tests, search, environment reward):** **grounded self-correction works.** This is **Reflexion** (Shinn et al. 2023, NeurIPS): an agent reflects on a *task-feedback signal* — unit-test pass/fail, environment reward — stores the reflection in episodic memory, and retries. Reflexion is constantly miscited as proof that "self-reflection works." Read the mechanism: it works **because the feedback is external and verifiable**, not because the model introspected well. On HumanEval coding, with unit-test pass/fail as the signal, Reflexion substantially raised pass@1. Put it firmly on the *grounded* side.
  - **Open-ended / stylistic (no single correct fact):** intrinsic **Self-Refine** (Madaan et al. 2023, NeurIPS) may help — "critique your draft for tone and completeness, then rewrite" reports ~20% human-preference gains. The reconciliation with Huang: Self-Refine polishes toward a *stylistic* target where "better" is subjective, but it cannot reliably *find its own reasoning errors* where there is one correct answer. Whether its gains are genuine correction or stylistic re-rolling toward the prompt's target is unresolved.

Let $p$ be the probability a single sampled answer is correct and let answers be drawn independently. With majority vote over $k$ samples, the probability the plurality answer is correct rises with $k$ whenever the correct answer is the *modal* one ($p$ above the largest wrong-answer mass) — which is why self-consistency helps on tasks where the model is right more often than it is wrong in any single consistent way, and why it cannot rescue a task where the model's modal answer is simply wrong. The math says exactly when the trick applies: it amplifies an existing majority; it does not manufacture one.

> **The grounding line is the ReAct line.** This is Ch. 11's lesson applied to error-correction. ReAct works because the agent *acts against the world* and observes a real result; the same external grounding is what separates self-correction that helps (Reflexion's tests) from self-correction that hurts (intrinsic critique). Where Ch. 11 warned that the ReAct loop is brittle when the observation channel is weak or absent, this section names the consequence: with no real observation, "reflection" is just another sample from the same faulty distribution, and the eval discipline of Ch. 9 is the only thing that will tell you it isn't helping.

The portable lesson is a *predicate*, not a technique list: **Is there an external, verifiable feedback signal? If yes, grounded self-correction can help. If no, prefer self-consistency or accept the first answer — do not ask the model to grade itself.**

---

## 15.5 Is prompt engineering obsolescing?

Walk into any 2026 engineering team and someone will claim prompt engineering is dying — the models are so good now that you just ask plainly and they comply. There is real evidence behind the claim, and real confusion in it. The resolution is a distinction, not a winner.

What is *actually* decaying is the catalog of **tricks**, and the Wharton Prompting Science series documents it case by case:

- **Chain-of-Thought** (Report 2, Meincke et al. 2025): on reasoning-tuned models, explicit CoT prompting yields only marginal accuracy gains at substantial time cost (~20–80% slower); on non-reasoning models, modest average gains with *increased variance*. A once-essential trick is losing marginal value as models internalize the reasoning step — exactly the Ch. 8 result.
- **Expert personas** (Report 4): across six models on graduate-level science/engineering/law questions, "expert personas" gave no consistent boost and sometimes hurt. The Ch. 6 mechanism predicted this — a persona changes the *register* of the answer, not what the model knows — and the decay is the empirical confirmation.
- **Threats and tips** (Report 3): threatening the model or promising it a payment does not reliably improve performance on hard benchmarks. Viral folk-prompting, debunked under controlled testing.

So one reading — *the tricks are obsolescing* — is defensible and well-supported. But the second reading — *prompt engineering as a discipline is obsolescing* — does not follow, and Wharton's own Report 1 is why. Report 1 ("complicated and contingent") found that prompt effects are *hard to predict in advance* and *swing with the scoring standard* — politeness helps on one question and hurts on another, and you cannot know which without testing. That is not a refutation of prompt engineering. **It is a mandate for it.** "Effects are contingent and must be measured per task" is the engineering stance this entire book has argued for. The discipline that survives the death of the tricks is the discipline of *specification and measurement.*

This is the book's thesis stated in the field's own contested vocabulary. As models follow instructions more faithfully, the value of *elaborate tricks* falls while the value of *precise, falsifiable specification* — say exactly what you want, define success, measure it — rises. Tricks decay; specification discipline does not.

### The speculative edge: Karpathy's "system prompt learning"

One forward-looking idea deserves a place — and a clear label. In May 2025, Andrej Karpathy floated, **in a tweet** (not a paper, not a formal talk — flag it as non-peer-reviewed speculation), the notion of "system prompt learning" as a possible missing paradigm. The framing: pretraining changes parameters for *knowledge*; fine-tuning changes parameters for *habitual behavior*; but much human learning feels more like a *change in system prompt* — you hit a problem, work something out, and write it down explicitly for next time. "The LLM writing a book for itself on how to solve problems."

It is a generative idea and worth thinking with. It is also unvalidated: Karpathy presented no controlled evaluation, and the third-party implementations circulating under the name are separate from his proposal and themselves unvalidated. I include it precisely as a teaching case in the book's epistemic discipline: a provocative tweet is not a result. Distinguish the imagination it provokes from the evidence it lacks — which is the same move §15.4 made with self-correction, and the same move Ch. 9 made with single-prompt evals.

---

## 15.6 Multimodal prompting: less settled, genuinely new

Text-prompt principles mostly carry over to images: specificity, structure, and worked examples help with a vision-language model much as they help with text. But multimodal prompting adds a genuinely new lever and is, honestly, the least settled area in the book.

The new lever: the most effective "prompt" can be *drawn onto the image itself.* **Set-of-Mark** prompting (Yang et al. 2023) uses an off-the-shelf segmenter to partition an image into regions, overlays each with a visible mark (a number, a box), feeds the *marked* image to the model, and asks grounding questions that reference the marks — "what is in region 7?" Zero-shot GPT-4V with Set-of-Mark beat the prior fully-fine-tuned state of the art on the RefCOCOg referring-expression benchmark. The lesson generalizes past one method: visual prompting is its own intervention space (a red circle drawn around an object measurably redirects model attention), distinct from textual description.

What is *not* settled: there is no agreed rule for the position of an image relative to the text in a prompt (it measurably changes accuracy on document and chart tasks, but no settled best practice), no settled number or style of marks, and no clean predicate for when a visual prompt beats a textual description. This is the largest genuine gap in the book's coverage, and I flag it as such rather than papering over it. The honest production guidance is the one this whole chapter has been building: treat image position, mark style, and prompt structure as **tunable parameters measured per task** — the same eval discipline of §15.2, now over a parameter space we understand less well.

---

## 15.7 Closing the loop: how the failures compound

The book opened on documented failures so you would need the methods before meeting them. It closes by showing that the failures are not independent — they *compound*, and the compounds are where production systems actually break. Three integrations make the point.

**RLHF-sycophancy (Ch. 4) × persona drift (Ch. 6) × self-correction (this chapter).** One mechanism — approval-maximization learned from RLHF — surfaces three times. In Ch. 4 it is sycophancy: the model capitulates to user disagreement. In Ch. 6 it is persona drift: as system-prompt tokens lose salience over a long conversation, the model reverts toward the agreeable default-assistant register the same pressure rewards. In §15.4 it is over-revision: "are you sure?" reads as social pressure and tips a correct answer wrong. If you understood the mechanism in Ch. 4, you predicted the other two. That is what mechanism-first buys you — not three facts to memorize, but one mechanism that generates all three.

**ReAct brittleness (Ch. 11) × eval discipline (Ch. 9) × grounding (§15.4).** Ch. 11's agent loops are brittle precisely where the observation channel is weak; §15.4 named why (no real observation = reflection is just resampling); and Ch. 9 supplies the only reliable detector (you measure whether the loop helps, you do not assume it). An ungrounded ReAct loop that "reflects" between steps is the self-correction failure mode running inside an agent — and the only thing that catches it is the brittleness-aware evaluation harness of §15.2.

**Brittleness (Ch. 9) × production (§15.2) × bias (§15.3).** Madison's pipeline failed three ways at once — input drift, model-version drift, bias amplification — and all three are the *same* underlying fact (a prompt is a fragile configuration on a moving substrate) viewed from three angles. Versioning addresses the substrate, the eval harness addresses the fragility, monitoring addresses the drift, and treating bias as a first-class harness metric addresses the amplification. One discipline, applied across the angles.

The synthesis is the thesis. From Ch. 1's sampled-not-retrieved output to Ch. 14's context-is-the-bottleneck, the book has argued one claim: **prompt engineering is an empirical engineering discipline, resting on mechanism and falsifiable measurement, not an art of clever phrasing.** Every chapter was a special case. Sampling variance, the plausibility–truth gap, syntactic limits, sycophancy, persona architecture, output governance, reasoning patterns, brittleness, long-context position, agent loops, automated optimization, the fine-tuning stack, context systems, and now production and ethics — each one rewards the engineer who specifies precisely, evaluates empirically, and measures per task, and each one punishes the engineer who reaches for a universal trick. The tricks have a half-life. The discipline does not. That is the whole book, and it is where we stop.

---

## Exercises

**15.1 (Create — produce something).** Take a prompt you have written in any prior chapter's exercises (or one of your own) and move it to a *monitored pipeline specification.* Produce: (a) a versioned artifact recording the (prompt, model-snapshot, decoding-parameters) triple; (b) an eval-harness design with at least eight held-out inputs spanning a realistic distribution (include at least two adversarial/edge inputs), a declared scoring standard fixed *before* you measure, and a variant battery (≥3 paraphrases/reorderings per input); (c) a monitoring plan naming the score-distribution and input-distribution signals you would alert on. Run the harness if you have the means and report the score *distribution*, not the best score.

**15.2 (Apply).** You are given four tasks: (i) GSM8K-style arithmetic word problems; (ii) generating a Python function with an accompanying test suite; (iii) polishing the tone of a customer-support email; (iv) answering a graduate-level chemistry exam question. For each, apply the §15.4 predicate to choose between self-consistency, grounded self-correction (Reflexion-style), and intrinsic Self-Refine — or "accept the first answer." Justify each choice from the *grounding* mechanism, and name the failure mode you would expect if you chose wrong (e.g., correct-to-incorrect flipping).

**15.3 (Evaluate — the obsolescence debate).** Argue *both* sides of "prompt engineering is becoming obsolete," each in ~250 words, citing the evidence: for the "tricks are dying" side, the Wharton Reports on CoT, personas, and threats/tips; for the "discipline is forever" side, Wharton Report 1's contingency finding and this book's specification thesis. Then resolve it in one paragraph by stating the *distinction* (not a winner) that dissolves the apparent conflict. Note which of your own claims are empirical (cite) and which are judgment (label).

**15.4 (Analyze — cross-module compounding).** Pick one of the three compound failures in §15.7. In a short analysis, trace the *single underlying mechanism* through its multiple surfaces, predict a fourth surface where the same mechanism would appear that the chapter did not name, and propose the one detection or mitigation that addresses the mechanism rather than any single surface.

**15.5 (Evaluate — multimodal, hands-on, optional).** Take a grounding task on an image with several similar objects. Prompt a vision-language model two ways: (a) plain text — "describe the object on the left"; (b) Set-of-Mark — overlay numbered regions and ask "what is in region 3?". Report the difference in grounding reliability, then vary one parameter (image-before-text vs. text-before-image) and report whether position changed the answer. Connect your result to the §15.2 "tunable parameters measured per task" stance.

---

## What would change my mind

A controlled study showing that *intrinsic* self-correction (no external feedback) reliably improves accuracy on single-answer reasoning tasks above some clearly identified model-capability threshold — i.e., that the Huang et al. result has an expiration date set by model scale. The chapter's §15.4 predicate hinges on the claim that ungrounded self-critique cannot create information; evidence that sufficiently capable models develop reliable, ungrounded error-detection on reasoning (not merely stylistic) tasks would force me to add a capability-threshold branch to the decision rule rather than treating "no external signal ⇒ don't self-critique" as categorical.

Separately, longitudinal evidence that *specification discipline itself* — not just the tricks — measurably loses value as models improve (that careful specification and casual specification converge in outcome on a representative, well-scored task set) would undercut the book's central thesis. The obsolescence section bets that tricks decay while discipline endures; the convergence of careful and casual specification is the falsifiable form of "the discipline is dying too."

---

## Still puzzling

1. **Is there a capability threshold above which intrinsic self-critique becomes net-positive on reasoning?** Huang et al. is robust at current scales, but no one has mapped whether the failure is permanent or a function of model capability. The §15.4 predicate would need a branch if a threshold exists.

2. **Are Self-Refine's gains real error-correction or stylistic re-rolling?** No clean experiment isolates whether intrinsic refinement on open-ended tasks *finds errors* or merely *resamples toward the prompt's target.* The reconciliation with Huang depends on the answer, and we don't have it.

3. **Which trick decays next, and is there an asymptote?** The Wharton series is one longitudinal probe of trick-decay. If the trend continues, is there a floor — a set of specification moves that never decay because they encode information the model genuinely cannot infer — or does everything eventually get internalized? The thesis bets on a floor; the evidence is suggestive, not settled.

4. **What is the right unit of accountability for an amplifying pipeline?** §15.3 argues responsibility is non-delegable, but a system whose bias emerges only in aggregate over many individually-defensible outputs strains the individual-output model of accountability that review processes assume. The mechanism of harm (distributional drift) and the mechanism of oversight (per-output review) are mismatched, and I don't have a clean resolution.

---

## References

- Huang, J., Chen, X., Mishra, S., Zheng, H. S., Yu, A. W., Song, X., & Zhou, D. (2024). [Large Language Models Cannot Self-Correct Reasoning Yet](https://arxiv.org/abs/2310.01798). ICLR 2024. arXiv:2310.01798.
- Wang, X., Wei, J., Schuurmans, D., Le, Q., Chi, E., Narang, S., Chowdhery, A., & Zhou, D. (2023). [Self-Consistency Improves Chain of Thought Reasoning in Language Models](https://arxiv.org/abs/2203.11171). ICLR 2023. arXiv:2203.11171.
- Shinn, N., Cassano, F., Berman, E., Gopinath, A., Narasimhan, K., & Yao, S. (2023). [Reflexion: Language Agents with Verbal Reinforcement Learning](https://arxiv.org/abs/2303.11366). NeurIPS 2023. arXiv:2303.11366.
- Madaan, A., et al. (2023). [Self-Refine: Iterative Refinement with Self-Feedback](https://arxiv.org/abs/2303.17651). NeurIPS 2023. arXiv:2303.17651.
- Yang, J., Zhang, H., Li, F., Zou, X., Li, C., & Gao, J. (2023). [Set-of-Mark Prompting Unleashes Extraordinary Visual Grounding in GPT-4V](https://arxiv.org/abs/2310.11441). arXiv:2310.11441 (Microsoft).
- Gu, J., et al. (2023). [A Systematic Survey of Prompt Engineering on Vision-Language Foundation Models](https://arxiv.org/abs/2307.12980). arXiv:2307.12980.
- Meincke, L., Mollick, E. R., Mollick, L., & Shapiro, D. (2025). *Prompting Science Report 1: Prompt Engineering is Complicated and Contingent.* arXiv:2503.04818; SSRN 5165270.
- Meincke, L., et al. (2025). *Prompting Science Report 2: The Decreasing Value of Chain of Thought in Prompting.* Wharton GAIL; SSRN 5285532.
- Meincke, L., et al. (2025). *Prompting Science Report 3: Threaten or Tip.* Wharton GAIL; SSRN 5375404.
- Basil, S., Shapiro, I., Shapiro, D., Mollick, E. R., Mollick, L., & Meincke, L. (2025). *Prompting Science Report 4: Playing Pretend — Expert Personas Don't Improve Factual Accuracy.* Wharton GAIL; arXiv:2512.05858 (Dec 2025); SSRN 5879722.
- Karpathy, A. (May 7, 2025). *System prompt learning* — X/Twitter post (x.com/karpathy/status/1921368644069765486). **Non-peer-reviewed; thinking-out-loud proposal, not a paper or formal result.**
- "Can LLMs Correct Themselves? A Benchmark of Self-Correction in LLMs" (CorrectBench). arXiv:2510.16062 (submitted Oct 17, 2025). **Recent preprint — intrinsic/external/fine-tuned taxonomy useful; specific percentage claims pending peer review.**

---

**Tags:** production-lifecycle, prompt-versioning, eval-harness, monitoring, brittleness, bias-amplification, power-concentration, responsibility, self-correction, self-consistency, reflexion, grounding-predicate, obsolescence-debate, tricks-decay-discipline-endures, system-prompt-learning, multimodal, set-of-mark, book-synthesis
