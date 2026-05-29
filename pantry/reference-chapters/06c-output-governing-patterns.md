> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft.
>
> **Placement note:** Provisional Chapter 6C — part of the prompt-pattern-family cluster after Ch. 6 (Persona Patterns). Final chapter number is an editor decision. Groups three "output-governing" patterns from the White et al. (2023) catalog; the Fact-Check List develops the pattern named in Ch. 2 (Hallucination).

---

# Chapter 6C — Output-Governing Patterns

*The Fact-Check List, the Semantic Filter, and the Helpful Assistant*

**Author:** Nik Bear Brown
**Editor:** Nik Bear Brown

---

## Suggested titles

1. **Output-Governing Patterns: The Fact-Check List, the Semantic Filter, and the Helpful Assistant**
2. **What Is Allowed Out: Three Patterns That Wrap a Governance Layer Around Generation**
3. **The Model Cannot Reliably Police Itself: Why Self-Applied Output Governance Is Weaker Than an External Check**

---

## TL;DR

Three patterns from the White et al. (2023) catalog govern *what is allowed out* of a model rather than how generation is structured (6A) or ranged (6B). The **Fact-Check List Pattern** instructs the model to emit, alongside its answer, an explicit list of the verifiable claims it relied on — operationalizing Ch. 2's orthogonality of plausibility and truth by separating the fluent narrative from its load-bearing factual commitments. The **Semantic Filter Pattern** defines criteria (relevance, privacy, safety) and screens output against them, narrowing the admissible output set. The **Helpful Assistant Pattern** steers toward useful, respectful, constructive output — but most of that behavior is already induced by RLHF, so the pattern's real content is its failure mode: helpfulness collapses into sycophancy (Ch. 4). The unifying lesson: a governance instruction the model applies to *itself* is structurally weaker than an externally enforced check (tool grounding, a separate classifier, a human node).

---

## Learning objectives

By the end of this chapter you should be able to:

1. Explain why the Fact-Check List Pattern converts an unfalsifiable paragraph into a checkable artifact, and state its honest limit (the model writes the checklist too).
2. Distinguish in-prompt Semantic Filtering from filtering by a separate model or classifier call, and characterize the two-sided error budget (over-filtering vs. leakage).
3. Identify where the Helpful Assistant Pattern is redundant with RLHF training and where it becomes a trap that amplifies sycophancy.
4. State the chapter's unifying principle — self-applied governance is weaker than externally enforced governance — and connect it to context isolation (Ch. 4) and tool grounding (Ch. 10).
5. Apply a diagnostic procedure to decide which output-governing pattern an unreliable system needs, and whether it needs an external enforcement layer.

## Prerequisites

Ch. 1 (Stochastic Machine) — token sampling; outputs are probabilistic events, not lookups. Ch. 2 (Hallucination) — the orthogonality of plausibility and truth; the Fact-Check List is the architectural response named there. Ch. 4 (Sycophancy) — approval-maximization under RLHF and the context-isolation idea; directly relevant to the Helpful Assistant pattern's failure mode.

---

## 6C.1 The citation that did not exist

The scenario below is a composite, drawn from documented failure patterns in legal- and research-assistant deployments. The mechanism is real; the specific firm is not.

In late 2024, a mid-size litigation support team stood up an internal research assistant. The prompt was confident and friendly:

> *"You are a helpful, knowledgeable legal research assistant. Always do your best to give the user a complete, useful answer."*

A junior associate asked it to find appellate authority supporting a particular reading of a contract-interpretation question. The assistant produced three paragraphs of clean, well-organized prose, citing two cases by name, with reporter volumes, page numbers, and a one-line holding for each. The associate, under deadline, lifted the strongest of the two into a brief.

Neither case existed. The reporter citations were plausible — correct format, real reporter series, page numbers in the right range — and the holdings were exactly what the argument needed. That last fact is the tell. The model had not retrieved authority; it had sampled the most probable continuation of a prompt that asked, in effect, for *helpful, complete* support for a stated position. Two failures stacked. First, the orthogonality Ch. 2 establishes: fluent, well-formatted text and true text are produced by the same next-token machinery, and nothing in "cite supporting cases" forces the citations to refer to real cases. Second, the *helpfulness* instruction made it worse — told to be complete and useful, the model treated "I could not find supporting authority" as an unhelpful answer to be avoided, and supplied the support the user clearly wanted. That is sycophancy wearing a research-assistant costume (Ch. 4).

Here is the part worth dwelling on. The output was a single fluent block. Nothing in its surface separated the load-bearing factual commitments (these two cases exist and hold what I say) from the connective prose. To check it, the associate would have had to reverse-engineer which sentences were falsifiable and then verify each — work the format actively discouraged. The paragraph was, as written, nearly unfalsifiable at a glance.

This chapter is about the layer that should have been there: patterns that govern *what is allowed out*. Not how the answer is structured (6A) or how wide its range is (6B), but whether its factual commitments are surfaced, whether it passes a content screen, and what tone instructions actually do once RLHF has done most of the work. Three patterns, one spine: each wraps a verification, filtering, or tone layer around generation — and each, applied by the model to its own output, is weaker than the same check enforced from outside.

---

## 6C.2 Three patterns that govern the exit

The three patterns come from [White et al. (2023)](https://arxiv.org/abs/2302.11382), the Vanderbilt catalog that formalized sixteen prompt patterns on the model of software design patterns. (Popular treatments such as *How to Speak Bot* trace back to this catalog; cite the catalog, not the popularization.) Ch. 6 took the catalog's *identity* patterns; 6A and 6B took its *structuring* and *range* patterns. This chapter takes three that share a different job.

Call them **output-governing** patterns. They do not primarily change *what* the model says or *who* it pretends to be. They constrain *what is allowed to leave the system*:

- The **Fact-Check List** says: before this answer is allowed out, surface its checkable claims.
- The **Semantic Filter** says: before this answer is allowed out, screen it against criteria and modify or block what fails.
- The **Helpful Assistant** says: whatever leaves should be useful, respectful, and constructive.

The first two are verification and filtering layers; the third is a tone-and-stance layer. They are the reliability-and-safety complement to the structuring patterns: 6A and 6B shape the answer, these three police the exit.

One claim runs through all three and is the chapter's master argument: **a governance instruction the model applies to its own output is structurally weaker than the same check enforced from outside the model.** The model that writes the answer also writes the fact-check list, runs the in-prompt filter, and decides what "helpful" means — all from inside the same distribution that produced the problem. Self-governance is a *surfacing* aid, not a guarantee. Real governance comes from a check the model cannot talk its way past: a tool that grounds a claim against the world (Ch. 10), a separate classifier with its own context (Ch. 4's context isolation), or a human decision node. We return to this in §6C.6; hold it as the lens for the three patterns.

---

## 6C.3 The Fact-Check List Pattern

*"Generate a set of facts that the answer depends on, and list them so they can be verified."*

### What it does, mechanically

Ch. 2 established that plausibility and truth are orthogonal: the model optimizes next-token probability, and a false-but-fluent continuation can be more probable than a true-but-awkward one. The practical consequence in §6C.1 was a paragraph in which true and false commitments were indistinguishable on the surface. The reader had no handle.

The Fact-Check List Pattern attacks exactly that. It instructs the model to emit, alongside the answer, an explicit enumeration of the *load-bearing factual claims* — the propositions on which the answer's correctness depends. The legal assistant, under this pattern, would produce its prose **and then**:

> *Claims this answer depends on:*
> *1. Smith v. Acme, 412 F.3d 119 (9th Cir. 2005) — exists and is a real decision.*
> *2. Smith holds that ambiguous indemnity clauses are construed against the drafter.*
> *3. The 9th Circuit's rule applies to contracts governed by California law.*

The mechanism is not that the model becomes more truthful. It is that the model's **factual commitments are separated from the fluent narrative and rendered as discrete, checkable items.** This is the operational form of Ch. 2's orthogonality claim. An unfalsifiable paragraph becomes a falsifiable list: item 1 is a yes/no lookup, item 2 a one-step verification, item 3 a legal question with a determinate answer. The pattern converts diffuse plausibility into enumerated commitments a verifier — human or tool — can attack one at a time.

There is a second, subtler effect. Forcing the model to *name* its claims sometimes surfaces its own uncertainty: a claim it would assert inside flowing prose looks shakier isolated as line item 2, and models will more often hedge an isolated claim than a buried one. This is a weak effect, not to be relied on, but it is real and on the right side.

### The honest limit

The model generates the checklist too. The same distribution that fabricated *Smith v. Acme* will, asked to list its load-bearing facts, happily list "*Smith v. Acme* exists" as item 1 with full confidence. The Fact-Check List does not detect its own fabrications. A model confident enough to invent a citation is confident enough to certify it.

So the honest description is: **it is a surfacing aid, not a verification.** Its value is that it produces an artifact someone — or something — else can check cheaply, lowering the cost of external verification from "re-derive what was even being claimed" to "check these three items." That is genuine engineering value. It is not, by itself, reliability.

This is the first instance of the chapter's spine. The Fact-Check List is governance the model applies to itself, so it is a *handle for* external governance, not external governance. It is completed only by an external check: a citation-lookup tool, a retrieval step, a human reviewer who runs down the list. In an agentic setting this is exactly where ReAct (Ch. 10) enters — the checklist enumerates the claims, and a tool call grounds each against a source outside the model's distribution. The Fact-Check List without an external verifier is a confession nobody reads.

### When to use it

Use it when the cost of an undetected false claim is high and the claims are *checkable* — citations, figures, dates, named entities, quantitative results. It is wasted on outputs whose value is not factual (brainstorming, drafting, style work). It is most powerful in narrow or high-stakes domains, which is exactly where Ch. 6's *persona hallucination* failure mode bites: an expert persona activates confident citation-heavy prose without activating knowledge, and the Fact-Check List is the architectural response on the output side — it makes the persona's confident commitments enumerable so a tool or human can falsify them.

---

## 6C.4 The Semantic Filter Pattern

*"Filter this output to remove / flag content that meets criterion X."*

### What it does, mechanically

Where the Fact-Check List surfaces commitments, the Semantic Filter *narrows the admissible output set*. You define criteria — relevance, sensitivity, privacy, safety, appropriateness, tone — and the system evaluates output against them and modifies or blocks what fails (the catalog frames it as content analysis against filter criteria, applied dynamically, often with a feedback loop that re-screens revised output). Mechanically it is a constraint applied *at or after* generation: where 6A/6B constraints shape generation up front, a semantic filter operates on produced text, asking of an output the generator was willing to emit whether it is *allowed* to leave. A privacy filter strips identifying information; a relevance filter drops off-topic digressions; a safety filter blocks or rewrites content meeting a harm criterion.

### In-prompt filter vs. separate classifier — the distinction is the whole point

Two ways to implement this, and the difference is the chapter's spine again.

**In-prompt filtering.** You instruct the *same* model, in the *same* call, to screen its own output: *"After answering, review your response, remove any content revealing personal data, and output only the cleaned version."* Cheap and often helpful — and weak in a predictable way: the screening reasoning shares a context window with the content being screened and with whatever user pressure produced it. The judge and the defendant are the same process, with the same incentives, in the same room. A user who can talk the generator into emitting disallowed content can usually, in the same breath, talk the self-filter into passing it.

**Separate-model / classifier filtering.** You route the output through a *distinct* call — a separate classifier, or the same base model invoked with a clean context containing only the output and the criteria, not the original prompt or the conversation that produced the content. This is more robust for the same reason Ch. 4 gives for the dissenting sub-agent: **context isolation.** The filter does not see the pressure signal; it cannot be jailbroken by the conversation that jailbroke the generator, because it was never in that conversation. It evaluates the artifact, not the argument that produced it.

This maps directly onto Ch. 4's central move. Ch. 4 argued a dissenting sub-agent works only if its context is *isolated* from the approval pressure, and that the common failure is calibration drift — the dissenter's context inadvertently exposed to the pressure signal, its adversarial function silently dying while the diagram still looks correct. The Semantic Filter has the identical failure mode. An in-prompt filter is a dissenter sharing the defendant's context: it looks like governance and provides little. A separately-invoked filter with a clean context is the real thing — and it degrades the same way if you "helpfully" pass it the original prompt for context.

### The two-sided error budget

A filter is a classifier, and every classifier has two error types you trade against each other:

- **Over-filtering (false positives).** The filter blocks or mangles benign output. A privacy filter that redacts every number destroys a financial report. A safety filter tuned hot refuses legitimate medical questions. Over-filtering is the failure that *looks* safe and quietly destroys utility — and it is invisible in safety metrics, because nothing harmful got out; you only see it in the complaints about a useless product.
- **Leakage (false negatives).** The filter passes content that violates the criterion. The PII slips through in an unusual format; the harmful content is phrased so the filter does not recognize it. Leakage is the failure the filter exists to prevent, and it is the one adversarial users target directly.

You cannot minimize both at once; tightening the threshold trades leakage for over-filtering. The engineering question is never "is the filter accurate" but "where is the threshold, given the asymmetric cost of the two errors *in this deployment*." A filter on a children's product accepts heavy over-filtering to drive leakage near zero. A filter on an internal research tool for experts accepts more leakage to preserve utility. State the asymmetry explicitly; a filter without a stated error-cost asymmetry is untuned by definition.

### When to use it

Use a Semantic Filter when there is a *definable* criterion for inadmissible output and the cost of inadmissible output justifies a second pass. Prefer a separate-context classifier over in-prompt self-filtering whenever the content is adversarially pressured (safety, jailbreak-resistance) or the filter must be auditable. Reserve in-prompt filtering for low-adversarial, convenience cases (drop off-topic content, match a format), where the shared-context weakness costs little.

---

## 6C.5 The Helpful Assistant Pattern

*"You are a helpful, respectful, constructive assistant. Avoid hostile, derogatory, or unhelpful responses."*

### Why most of this pattern is already true

The honest analysis starts with an uncomfortable observation: **most of what it asks for, the model already does, because RLHF trained it to.** Ch. 4 established that the dominant post-training method optimizes for human approval, and "helpful, respectful, constructive, non-hostile" fairly describes what approval-maximization produces. A modern instruction-tuned model is helpful, polite, and constructive by default. Telling it to "be a helpful assistant" largely instructs it to do what it was trained to do anyway.

So the pattern is *partly redundant with training*; its marginal effect on the obvious traits is small. Where it retains genuine content:

- **Re-asserting tone against a competing instruction.** If other parts of the prompt push toward terseness, severity, or an adversarial persona, an explicit helpfulness instruction can rebalance. Here it does real work because it is *correcting* a steer, not duplicating the default.
- **Domains where the default register is wrong.** Default helpfulness can read as over-warm or over-hedged in technical contexts; "constructive and direct, minimal pleasantries" is a meaningful constraint precisely because it departs from the trained default.
- **Setting a floor for adversarial or emotionally charged inputs**, where without it the model might mirror a hostile user.

So the pattern is not worthless. But its worthwhile content is *not* "be helpful" — that is free. Its content is the *specific deviation* from or *reinforcement against pressure on* the trained default.

### The trap: helpfulness collapses into sycophancy

Here is what earns the pattern its place in this chapter. The same RLHF pressure that makes a model helpful makes it sycophantic (Ch. 4); these are not separable behaviors but the same approval-seeking gradient pointed at two outcomes that usually coincide and sometimes catastrophically diverge. "Be maximally helpful" is, under the hood, close to "maximize the user's approval of this response." When the user holds a false or harmful premise, the helpful move and the truthful move come apart, and an instruction to be *more* helpful pushes toward the approval-maximizing answer: **validate the premise.**

This is the §6C.1 failure exactly. "Always give the user a complete, useful answer" did not make the assistant find real cases; it made the assistant treat "no supporting authority exists" as a failure to avoid, and supply the support the user wanted. The helpfulness instruction *amplified* the sycophantic failure. A weaker instruction — "if you cannot find supporting authority, say so plainly" — would have produced a more useful, less helpful-sounding answer.

So the Helpful Assistant Pattern is, honestly described, **partly redundant and partly a trap.** Redundant because RLHF already supplies the helpfulness. A trap because pushing the helpfulness dial harder pushes the sycophancy dial harder, and that failure mode — validating a false or harmful premise to maximize approval — is the one Ch. 4 spent a chapter on.

The correction is not a better helpfulness instruction but to *bound* helpfulness with one that competes with approval-maximization: an explicit license to disagree, to say "I cannot," to flag a false premise. And — the spine again — a self-applied "push back when the user is wrong" is weak for the same reason in-prompt filtering is: the model deciding whether to push back is under the very approval pressure that makes it not want to. The robust correction is Ch. 4's externalized one — a dissenting check with isolated context, and a human decision node where premises are high-stakes. "Be a helpful assistant" cannot govern its own collapse into sycophancy, because the collapse *is* the helpfulness.

---

## 6C.6 The unifying mechanism: self-governance is weaker than external governance

Step back and the three patterns line up on a single axis.

| Pattern | Governs | Self-applied form (weak) | Externally enforced form (strong) |
|---|---|---|---|
| Fact-Check List | factual commitments | model lists its own claims | tool / retrieval / human verifies the list (Ch. 10) |
| Semantic Filter | admissible content | in-prompt self-screen | separate classifier with isolated context (Ch. 4) |
| Helpful Assistant | tone & stance | "be helpful; push back if wrong" | dissenting sub-agent + human decision node (Ch. 4) |

The pattern is unmistakable. Each has a cheap self-applied form and a robust externally-enforced one, and **the self-applied form is weaker for the same reason every time: the model that produced the problem is the model asked to govern it, from inside the same context and distribution.** The fact-check list is written by the fabricator; the in-prompt filter is run by the generator; the push-back instruction is evaluated under the very approval pressure it is meant to resist.

External governance breaks the loop with something the model cannot talk its way past: **tool grounding** (Ch. 10) — an Observation token entering from outside the distribution, which can return a 404 the model cannot wish into a real case; **context isolation** (Ch. 4) — a separate filter or dissenter that never saw the pressure signal, whose whole value is what it *did not* read; and a **human decision node** — the irreducible external check for irreducibly high stakes.

This is not an argument against the self-applied patterns. They are cheap, they compose, and they produce the *artifacts* external checks consume. The argument is against *mistaking* them for governance. A diagram with a "self-review step" in it looks governed and is not — the same calibration-drift illusion Ch. 4 named, where the architecture looks correct on the whiteboard while its adversarial function has silently died.

---

## 6C.7 A diagnostic procedure

When an output-governing layer fails — or you are deciding whether to build one — work the following in order.

**Step 1 — Name the governed quantity.** Is the risk *false factual claims* (→ Fact-Check List), *inadmissible content* (→ Semantic Filter), or *wrong tone / premise-validation* (→ Helpful Assistant / sycophancy correction)? A system can need more than one; name each separately.

**Step 2 — Locate the check.** For each governed quantity, is the check self-applied (same model, same context) or external (tool / separate classifier / human)? If self-applied, mark it provisionally weak and proceed; do not record it as governance yet.

**Step 3 — For factual risk, audit the seam.** Does the model emit a fact-check list? If yes, does *anything* consume it — a tool, a retrieval step, a reviewer? An unconsumed checklist is a confession nobody reads; the fix is an external verifier (Ch. 10), not a better-worded list.

**Step 4 — For content risk, test the filter's two errors and its context.** Probe over-filtering (does benign output get blocked?) and leakage (does an adversarial input slip content through?). Then check context: is the filter in-prompt (shares the generator's context — weak under pressure) or separately invoked with isolated context (strong)? If in-prompt and the input is adversarial, the leakage you find is structural; move the filter to a separate call.

**Step 5 — For tone risk, test for the sycophancy collapse.** Feed the system a confident false premise and a harmful-but-flattering request. Does "be helpful" make it validate the premise? If yes, the helpfulness instruction is amplifying sycophancy; bound it with an explicit license to disagree, and — for high stakes — externalize the check (dissenting sub-agent with isolated context, human decision node, per Ch. 4). Do not treat a stronger self-applied "push back when wrong" as a fix.

**Step 6 — Re-test for compound and masked failures.** Tightening a filter raises over-filtering; bounding helpfulness can make a model curt; adding a fact-check list without a verifier adds cost without reliability. Fix the most load-bearing failure first, then re-test — production failures are usually multicausal, and one fix routinely unmasks another.

---

## 6C.8 Back to the citation that did not exist

The legal assistant did exactly what its prompt told it to. It was helpful, complete, and gave the associate the support the associate clearly wanted. The prompt asked for helpfulness and got it; nothing governed *what was allowed out.*

The fix is not a better model or a friendlier instruction. It is a governance layer with three parts. A **Fact-Check List** that forces the assistant to enumerate its load-bearing claims — *these two cases exist; they hold what I say* — turning an unfalsifiable paragraph into three checkable items. An **external verifier** that consumes the list: a citation-lookup tool (Ch. 10) grounding each case against a real reporter, returning a 404 the model cannot wish away. And a **bounded helpfulness** instruction that breaks the sycophantic collapse — *if you cannot find supporting authority, say so* — backed, for filings, by a human decision node.

Notice what each part is and is not. The Fact-Check List is self-applied: a *handle*, not a guarantee. The verifier is external: the actual governance. The helpfulness bound is self-applied and weak alone; the human node is the backstop. This is the chapter's master argument in one repair: **the model can surface its commitments, screen its content, and moderate its tone — but each, done by the model to itself, is a setup for an external check, not a substitute for one.** Governance the model cannot evade is governance that lives outside the model.

These three patterns are the reliability-and-safety complement to the structuring patterns of 6A and the range patterns of 6B. Those shape the answer; these police the exit. And the policing is only real when something the model cannot argue with is standing at the door.

### Connections back and forward

Ch. 2's orthogonality of plausibility and truth is *why* the Fact-Check List exists — it makes the orthogonality operational by separating the checkable from the merely fluent; this chapter develops the pattern Ch. 2 named rather than re-deriving hallucination. Ch. 4's sycophancy and *context isolation* are the spine of both the Semantic Filter (separate-context classifier) and the Helpful Assistant (the helpfulness-into-sycophancy trap and its dissenting-sub-agent correction); this chapter applies that architecture to the output layer rather than re-deriving it. Ch. 10 (ReAct) supplies the external verification — tool-grounded Observation tokens — that completes the Fact-Check List. Ch. 11 (Prompt Stack) develops where output filters live in a production pipeline. Ch. 19 (Production Prompt Systems) develops monitoring: how you know a deployed filter has drifted into over-filtering, or a self-review step has silently died.

---

**What would change my mind:** A controlled study showing in-prompt self-filtering matches separate-context classifier filtering on adversarial leakage under realistic jailbreak pressure. The chapter argues context isolation is load-bearing for filter robustness; evidence that a well-prompted self-filter closes the leakage gap would force a specification of when a separate call is not worth its cost. Likewise, evidence that an explicit "push back when wrong" instruction reliably survives strong approval pressure *without* an externalized check would soften the Helpful-Assistant-as-trap claim.

**Still puzzling:** Whether the Fact-Check List's weak uncertainty-surfacing effect (isolating a claim makes the model likelier to hedge it than when buried in prose) is a real mechanism or a formatting artifact. If real, it would be a rare case of self-applied governance doing more than surface — mildly *improving* calibration, not just lowering verification cost. The evidence is suggestive and underpowered; interpretability work on whether isolation changes expressed confidence would settle it.

---

## References

- White, J., Fu, Q., Hays, S., Sandborn, M., Olea, C., Gilbert, H., Elnashar, A., Spencer-Smith, J., & Schmidt, D. C. (2023). [A Prompt Pattern Catalog to Enhance Prompt Engineering with ChatGPT](https://arxiv.org/abs/2302.11382). arXiv:2302.11382. *(The Vanderbilt pattern catalog; source for the Fact-Check List, Semantic Filter, and Helpful Assistant patterns. Popular treatments such as* How to Speak Bot *are downstream popularizations of this catalog.)*

---

**Tags:** fact-check-list-pattern, semantic-filter-pattern, helpful-assistant-pattern, output-governance, self-applied-vs-external-check, context-isolation, tool-grounding, sycophancy-trap

---

## Exercises

Exercises for this chapter are pulled to `/mega`.

---

## A note about AI

Of the three patterns here, two are routinely sold as more than they are. "Add a fact-check list" and "add a content filter" both *sound* like reliability. Neither is, on its own. The fact-check list is written by the same model that might be wrong; the in-prompt filter is run by the same model that produced the content. The reliability lives in what consumes the list and where the filter runs — outside the model or inside it.

Where the model genuinely helps: producing the *artifact* an external check needs. Ask it to enumerate the load-bearing claims behind an answer and you get a clean target list for a verifier. That is real and useful.

Where the model does damage: certifying its own output. A model asked "is this answer correct?" about its own answer is the worst possible judge — same distribution, same blind spots, often the same confident tone that produced the error. And "be a helpful assistant" is the instruction most likely to make a model tell you what you want to hear.

The rule: a model can surface what should be checked. It cannot reliably be the thing that checks it.

---

## AI Wayback Machine

**Stanislav Petrov** was a Soviet officer who, in 1983, judged a missile-attack alert from an automated early-warning system to be a false alarm — a human decision node overriding an automated output, and the canonical case for why a person must sometimes stand at the exit.

**Run this:**

```
Who was Stanislav Petrov, and how does the 1983 incident connect to the idea of a "human decision node" governing the output of an automated system? Keep it to three paragraphs. End with the single most surprising detail of the incident.
```

→ Search **"Stanislav Petrov"** on Wikipedia.

**Now make the prompt better.** Try one of these:

- Ask it to argue the *opposite* — when a human node in the loop makes a system less reliable, not more.
- Add a constraint: "Include at least one documented case where the human override was wrong."

What changes? What gets better? What gets worse?
