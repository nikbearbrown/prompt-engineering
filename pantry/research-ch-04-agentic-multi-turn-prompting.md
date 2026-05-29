# Research: Candidate Chapter §4 — Agentic and Multi-Turn Prompting
## Prompt Engineering with LLMs
**Chapter one-line:** Structuring agent loops, controlling tool exposure, enforcing structured output, and managing multi-turn context.
**Research date:** 2026-05-29
---
## 1. Primary Sources

### Foundational papers and texts

**The agent loop**
- **Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2023). "ReAct: Synergizing Reasoning and Acting in Language Models." ICLR 2023.** arXiv:2210.03629. VERIFIED — arXiv ID, venue (ICLR 2023), and full author list confirmed. Interleaves *Thought → Action → Observation* traces; reasoning helps the model induce/track/update plans and handle exceptions, while actions interface with external sources. Evaluated on HotpotQA, FEVER, ALFWorld, WebShop; outperforms reason-only (CoT) and act-only baselines and reduces fact hallucination. Code: github.com/ysymyth/ReAct. *(Cross-reference: this is Ch.10's spine — §4 cites it only as the canonical loop and does NOT re-derive it.)*
- **Schick, T., Dwivedi-Yu, J., Dessì, R., Raileanu, R., Lomeli, M., Zettlemoyer, L., Cancedda, N., & Scialom, T. (2023). "Toolformer: Language Models Can Teach Themselves to Use Tools." NeurIPS 2023.** arXiv:2302.04761 (submitted 9 Feb 2023). VERIFIED. Self-supervised; model decides *which* API to call, *when*, *what* arguments, and how to fold the result back into prediction — from a handful of demonstrations per API. Tools: calculator, QA, two search engines, translation, calendar. Establishes the "tool use as token prediction" framing that underlies modern function calling.

**Tool-use scaling and degradation (the chapter's distinctive contribution)**
- **Patil, S. G., Zhang, T., Wang, X., & Gonzalez, J. E. (2023). "Gorilla: Large Language Model Connected with Massive APIs." NeurIPS 2024.** arXiv:2305.15334 (May 2023). VERIFIED. Introduces **APIBench** (HuggingFace, TorchHub, TensorHub APIs). A finetuned LLaMA model surpasses GPT-4 at writing API calls and "substantially mitigates hallucination commonly encountered when prompting LLMs directly." Retrieval-aware variant adapts to test-time API doc changes. This is the canonical primary source for *tool hallucination* as a named failure mode.
- **Qin, Y., Liang, S., Ye, Y., et al. (2023). "ToolLLM: Facilitating Large Language Models to Master 16000+ Real-world APIs." ICLR 2024 (spotlight).** arXiv:2307.16789. VERIFIED. Builds **ToolBench** from 16,464 real RESTful APIs (49 categories, RapidAPI Hub). Demonstrates that *breadth* of the tool space is itself the hard problem; introduces DFSDT (depth-first search decision tree) over tool calls. Code: OpenBMB/ToolBench.
- **Patil, S. G., et al. (2025). "The Berkeley Function Calling Leaderboard (BFCL): From Tool Use to Agentic Evaluation of Large Language Models." ICML 2025.** (proceedings.mlr.press/v267/patil25a.html; OpenReview 2GmDdhBdDk). VERIFIED. Living benchmark. AST-based evaluation scales to thousands of functions by checking call *structure* rather than executing. Version history is itself an argument: v1 = syntactic correctness; v2 = enterprise/OSS functions; v3 = **multi-turn**; v4 = holistic agentic. Headline finding: "Top AIs ace one-shot questions but still stumble when they must remember context, manage long conversations, or decide when *not* to act."

**Structured output**
- **Willard, B. T., & Louf, R. (2023). "Efficient Guided Generation for Large Language Models."** arXiv:2307.09702 (19 Jul 2023). VERIFIED. The mechanism behind constrained/grammar-guided decoding: reframe generation as transitions over a finite-state machine compiled from a regex/CFG, building an index over the vocabulary so invalid tokens are masked with near-zero overhead. Implemented in the **Outlines** library — the primary academic citation for "enforce the schema at decode time, don't ask politely."
- **Tam, Z. R., et al. (2024). "Let Me Speak Freely? A Study on the Impact of Format Restrictions on Performance of Large Language Models." EMNLP 2024 (Industry Track).** VERIFIED via secondary sources (find arXiv ID; widely cited as Tam et al. 2024). Critical *counter-mechanism*: forcing JSON/format restrictions degrades reasoning by ~10–15% on math/symbolic tasks vs. free-form generation. Two distinct causes: (a) the *format-requesting instruction itself* costs accuracy before any decoder constraint; (b) if the answer field precedes the reasoning field, the model commits before it reasons. Decision procedure: reason free-form first, reformat in a second pass — or order schema fields reasoning-before-answer.
- **Provider docs — OpenAI, "Introducing Structured Outputs in the API" (Aug 2024).** openai.com/index/introducing-structured-outputs-in-the-api. VERIFIED. Native Structured Outputs use constrained decoding to guarantee schema conformance ("100% reliability" claim by OpenAI for gpt-4o-2024-08-06+). Key caveat directly usable as a sidebar: *"Structured outputs guarantee shape, not truth"* — right fields, possibly wrong values.

**Multi-turn context / memory**
- **Packer, C., Fang, V., Patil, S. G., Lin, K., Wooders, S., & Gonzalez, J. E. (2023). "MemGPT: Towards LLMs as Operating Systems."** arXiv:2310.08560 (12 Oct 2023). VERIFIED. **Virtual context management**: borrows OS virtual-memory hierarchy — page relevant history into the context window from external storage, evict the rest; the LLM issues function calls to manage its own memory tiers. Evaluated on document analysis beyond context length and multi-session chat. The canonical primary source for "no memory beyond the window; manage it explicitly."

### Key empirical cases
- **Laban, P., et al. (2025). "LLMs Get Lost In Multi-Turn Conversation."** arXiv:2505.06120 (May 2025). VERIFIED. Across all top open/closed models and six generation tasks, **average 39% performance drop** single-turn → multi-turn. Decomposes into a *minor* aptitude loss and a *large* rise in unreliability. Named effects: "answer bloat" (later attempts 20–300% longer), "loss-in-middle-turns," and — the sharpest finding for a decision procedure — *"when LLMs take a wrong turn, they get lost and do not recover."* Implication: don't patch a derailed thread; resummarize and restart clean.
- **Yao, S., Shinn, N., Razavi, P., & Narasimhan, K. (2024). "τ-bench: A Benchmark for Tool-Agent-User Interaction in Real-World Domains." ICLR 2025.** arXiv:2406.12045. VERIFIED. Retail + airline customer-service domains with API tools and policy guidelines. Even gpt-4o succeeds on <50% of tasks and is inconsistent (pass^8 < 25% in retail). Introduces **pass^k** (reliability across k trials). Best single empirical case for "agents that must follow rules over many turns fail at the *consistency* layer, not the capability layer."
- **"LongFuncEval: Measuring the effectiveness of long context models for function calling."** arXiv:2505.10570. VERIFIED (secondary). Quantifies tool-count degradation: performance drops **7.6%–85.6%** as the tool catalog grows (8K→120K tokens) and as the correct tool's position varies — driven by formatting failures and hallucination. Directly supports the spine claim and supplies the data for a tool-count-vs-error-rate figure.

---
## 2. The Core Concept — State of the Field

### What is settled
- **The loop works and is transparent.** Interleaving explicit reasoning with actions (ReAct) beats reason-only or act-only, and the visible trace is auditable. Embedded in LangChain, AutoGPT, and effectively every agent framework.
- **More tools = more errors.** Tool-count degradation is reproduced across APIBench, ToolBench, BFCL, and LongFuncEval. The mechanism is twofold: (a) larger tool catalogs consume context tokens that would otherwise hold reasoning; (b) selection ambiguity rises combinatorially. Mitigation consensus: scope tools narrowly; use a router/orchestrator to expose a small relevant subset per task; retrieve tools by vector similarity rather than registering everything upfront.
- **Native structured-output beats prompted JSON.** Constrained/grammar-guided decoding (Outlines, native API modes) makes schema conformance a *guarantee* rather than a request. Few-shot format exemplars beat prose descriptions of the format.
- **There is no memory beyond the context window.** State must be resupplied each turn; the only questions are *what* to resupply and *how compressed*.

### What is disputed
- **Does constraint help or hurt?** "Let Me Speak Freely?" (Tam et al. 2024) shows format restriction *degrades* reasoning, while Outlines argues constraint is near-free. The reconciliation — and the chapter's nuance — is that the cost is in the *prompt instruction and field ordering*, not the decode-time masking per se. Constrain the format; free the reasoning.
- **Agent autonomy vs. workflow.** Anthropic's "Building Effective Agents" (Dec 2024) draws a sharp line: *workflows* (LLMs orchestrated by predefined code paths) vs. *agents* (LLMs directing their own process). It argues most production value comes from simple composable workflows, not maximal autonomy — a deflationary stance against "agentic" hype.
- **Summarize vs. retrieve vs. page.** Summarization buffers (LangChain `ConversationSummaryBufferMemory`), retrieval over a vector store, and OS-style paging (MemGPT) are competing memory strategies; no consensus on a default.

### What has changed recently (last 5 years)
- **2022–2023:** The loop (ReAct) and self-taught tool use (Toolformer) are formalized; Gorilla/ToolLLM name tool hallucination and the scaling problem.
- **2023–2024:** Constrained decoding goes mainstream (Outlines, then native OpenAI Structured Outputs Aug 2024); function calling becomes a first-class API primitive.
- **2024–2026:** Evaluation shifts from single-call syntactic correctness to **multi-turn reliability** (BFCL v3/v4, τ-bench, "LLMs Get Lost" May 2025). The field's frontier is now *consistency over a conversation*, not *capability on one call*.

---
## 3. Application Domain Examples
- **Customer service (τ-bench):** airline/retail agents must call APIs *and* follow refund/rebooking policy across turns. Failure mode is inconsistency: the same task succeeds and fails across trials (pass^k collapse).
- **Enterprise API orchestration:** internal platforms expose hundreds of functions; naive registration triggers tool-count degradation. Production fix = routing agent that narrows to ~5–10 tools per sub-task.
- **Data extraction / ETL:** Pydantic-enforced structured output is the standard production pattern — define a schema, let constrained decoding fill it, validate on parse. (Pydantic + instructor/Outlines is the canonical stack.)
- **Long-running research/coding agents:** context exhaustion is the binding constraint; MemGPT-style paging or periodic summarization keeps the agent oriented over hundreds of steps.
- **Coding assistants:** multi-turn derailment ("lost in conversation") is acute — a wrong early assumption propagates; the practical countermeasure is restart-with-summary rather than continued repair.

---
## 4. The Book's Thesis Connection

Mechanism-first, this chapter answers *why* each technique works, not just *that* it does:
- **Tool-count degradation** has a measurable mechanism (context consumption + selection ambiguity) and a falsifiable decision rule (expose ≤N scoped tools; route). Cite LongFuncEval's 7.6–85.6% range as the empirical spine.
- **Structured output** is presented as a control problem: prompted JSON *requests* conformance; constrained decoding *guarantees* it by masking the vocabulary against a compiled grammar (Willard & Louf). The named trade-off — format restriction can cost reasoning (Tam et al.) — gives the chapter its falsifiable nuance: constrain shape, free reasoning, order fields reasoning-first.
- **Multi-turn memory** is framed as state management under a hard constraint (fixed window): resupply, summarize-before-drop, or page (MemGPT). The named failure mode is non-recoverable derailment (Laban et al. 2025).

**Cross-references (avoid duplication):**
- **Ch.9 Interaction Patterns** owns the *taxonomy* of multi-turn dialogue patterns. §4 cites it and instead supplies the *quantitative* multi-turn degradation data and memory-management mechanisms.
- **Ch.10 ReAct** owns the loop derivation. §4 treats ReAct as a *given* primitive and builds *outward* — onto tool scaling, structured output enforcement, and context/memory — which neither Ch.9 nor Ch.10 covers. This is the chapter's non-overlapping core.

---
## 5. The AI Wayback Machine — Candidate Figures

*(Diverse, lesser-known-preferred, substantively connected to agent loops / control / planning / production systems. Norbert Wiener deliberately avoided — flagged for other chapters.)*

1. **Charles Forgy** (Wikipedia: "Charles Forgy") — computer scientist; invented the **Rete algorithm** (1974/1979) and the **OPS5** production-system language at Carnegie Mellon. Production systems are the direct intellectual ancestor of the *condition → action* agent loop: working memory matched against rules firing actions that update memory — exactly ReAct's Observation → Thought → Action cycle, minus the LLM. OPS5 powered R1/XCON, the first commercially successful expert system. *Anchor prompt:* "Charles Forgy (circa 1982, American computer scientist) — man at a terminal with production-rule diagrams and the Rete network nearby, historically plausible editorial portrait, face-centered composition, period-appropriate clothing and workspace, accurate to known public portraits when available, no text, no watermark." *Skew:* relatively few public photos; portrait may be loosely grounded — flag for verification.

2. **Roger Schank** (Wikipedia: "Roger Schank") — cognitive scientist; with Robert Abelson, *Scripts, Plans, Goals and Understanding* (1977), directing the Yale AI Lab. "Scripts" (stereotyped action sequences) and "plans/goals" are the conceptual precursor to *tool-use planning* and structured multi-step task decomposition — an agent following a script to a goal is the symbolic ancestor of an LLM planning a tool chain. *Anchor prompt:* "Roger Schank (circa 1977, American cognitive scientist) — middle-aged man with beard at a desk, script-and-plan knowledge-structure diagrams nearby, historically plausible editorial portrait, face-centered composition, period-appropriate clothing and workspace, accurate to known public portraits when available, no text, no watermark." *Skew:* well-documented; portrait grounding good.

3. **Herbert A. Simon** (Wikipedia: "Herbert A. Simon") — with Allen Newell, *Human Problem Solving* (1972) formalized production systems and the General Problem Solver; coined *bounded rationality*. The fixed-context-window constraint on LLM agents is a literal instance of bounded rationality — reasoning under finite memory and computation — making Simon the conceptual bridge from cognitive limits to context-management engineering. *Anchor prompt:* "Herbert A. Simon (circa 1972, American cognitive scientist and economist) — older man with glasses and pipe at a desk, problem-space search diagrams nearby, historically plausible editorial portrait, face-centered composition, period-appropriate clothing and workspace, accurate to known public portraits when available, no text, no watermark." *Skew:* extensively photographed (Nobel laureate); strong grounding. *Note:* Newell is already used in Ch.10 (ReAct) per the wayback file — choose **Simon** (or Forgy) here to avoid duplicating Newell.

*Recommendation:* lead with **Charles Forgy** (production systems = the loop) as the freshest, least-reused figure; **Schank** as backup (planning/scripts); **Simon** if a bounded-rationality framing for the memory section is wanted.

---
## 6. Pedagogical Delivery Research
- **Lead with the failure, then the mechanism.** Each of the three pillars has a clean named failure to open on: *tool hallucination* (Gorilla), *reasoning collapse under format constraint* (Tam et al.), *non-recoverable derailment* (Laban et al.). Mechanism-first pedagogy: show the break, derive the cause, give the decision rule.
- **Decision-procedure boxes.** (1) "How many tools?" → scope to task; route if >~10. (2) "Prompt for JSON or constrain decode?" → constrain shape, free reasoning, order fields reasoning-first. (3) "Multi-turn going wrong?" → summarize-and-restart, don't repair.
- **Contrast pairs as exercises.** Same task with 5 vs. 50 tools (measure error rate); free-form-then-reformat vs. JSON-mode (measure reasoning accuracy); raw-history vs. summary-buffer (measure tokens + task success).
- **The version-history-as-argument device.** BFCL v1→v4 traces the field's maturation from syntax → multi-turn → agentic; a compact teaching narrative for "what got hard and why."

---
## 7. Representation and Display Research
Two figures warranted:
1. **Thought → Action → Observation loop diagram.** A cycle: LLM emits *Thought*, selects *Action* (tool call), receives *Observation*, loops; annotate where hallucination enters (Action selection) and where the trace provides auditability. Keep it visually distinct from Ch.10's ReAct figure — frame this one around *tool selection from a catalog* (the §4 angle), not the reasoning derivation.
2. **Tool-count vs. error-rate plot.** X-axis: number/size of available tools (8K→120K tokens, per LongFuncEval); Y-axis: error/hallucination rate. Show the monotone rise and annotate the 7.6–85.6% degradation band. This is the chapter's signature quantitative figure and directly visualizes the spine claim.

*(Optional third: a memory-tier schematic — context window vs. external store with paging arrows, MemGPT-style — if the multi-turn section needs a visual anchor.)*

---
## 8. Open Questions and Research Gaps
- **No agreed default memory strategy.** Summarize vs. retrieve vs. page (MemGPT) — when each wins is under-characterized; lossy summarization's failure modes (what functional context gets dropped) are poorly mapped.
- **Reliability vs. capability gap.** τ-bench / "LLMs Get Lost" show consistency, not raw ability, is the bottleneck. Why models *don't recover* after a wrong turn is mechanistically unexplained (attention-to-recent-turns is a hypothesis, not settled). *[Mechanism partly hypothetical — label as such.]*
- **Constrained-decoding reasoning cost.** Whether the Tam et al. degradation survives in 2025–2026 reasoning models with extended thinking is unresolved; early evidence suggests thinking-tokens recover most lost accuracy, but this needs replication. *[Emerging, not settled.]*
- **Tool routing at scale.** Vector-retrieval over tool descriptions is the proposed fix for large catalogs, but retrieval errors that surface the wrong tool subset are themselves an unstudied failure mode.

---
## 9. Sourcing Notes
- **Verified (arXiv ID + venue + authors):** ReAct (2210.03629, ICLR 2023); Toolformer (2302.04761, NeurIPS 2023); Gorilla (2305.15334, NeurIPS 2024); ToolLLM (2307.16789, ICLR 2024); Outlines/Willard & Louf (2307.09702); MemGPT (2310.08560); τ-bench (2406.12045, ICLR 2025); "LLMs Get Lost" (2505.06120, 2025); BFCL (ICML 2025, OpenReview 2GmDdhBdDk).
- **Verified via secondary sources only (find/confirm primary):** "Let Me Speak Freely?" (Tam et al., EMNLP 2024 Industry Track) — strongly attested across multiple secondary sources but arXiv ID not directly fetched; **confirm arXiv ID before print.** LongFuncEval (arXiv:2505.10570) — ID seen in search listing, abstract via secondary summary; confirm. OpenAI Structured Outputs blog (Aug 2024) — official URL confirmed in results, page not directly fetched.
- **Added beyond the assigned spine (7 extra sources):** Toolformer, τ-bench, "LLMs Get Lost in Multi-Turn Conversation," LongFuncEval, "Let Me Speak Freely?" (Tam et al.), OpenAI Structured Outputs docs, Anthropic "Building Effective Agents."
- **Unverifiable / flagged claims:** OpenAI's "100% reliability" for Structured Outputs is a *vendor* claim (shape-conformance, not correctness) — present as such, not as independent finding. The "attention disproportionately to first/last turns" mechanism for multi-turn derailment is reported by Laban et al. but the causal account is partly hypothetical — label.
- **Wayback skew:** Forgy has limited public imagery (grounding risk, flagged); Schank and Simon are well-documented. Newell intentionally avoided (used in Ch.10); Wiener avoided per instruction (note for other chapters).
- **No blocked fetches encountered** (all sourcing via WebSearch; no curl/python used).
