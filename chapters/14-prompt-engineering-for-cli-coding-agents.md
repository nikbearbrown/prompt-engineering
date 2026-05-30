> **Voice status:** `voice-unanchored`. Both root `style/` and `books/prompt-engineering/style/` empty as of this draft.

---

# Chapter 14 — Prompt Engineering for CLI Coding Agents: Why Context Is the Bottleneck

*Engineering an agent's context system, not just its prompt*

**Author:** Nik Bear Brown

**Editor:** Nik Bear Brown

---

## Suggested titles

1. **Prompt Engineering for CLI Coding Agents: Why Context Is the Bottleneck**
2. **The Agent That Got Dumber as the Session Got Longer**
3. **Context Is the Bottleneck, Not Intelligence: Engineering the State a Coding Agent Works From**

---

## TL;DR

A chat prompt is a one-shot instruction; a CLI coding agent is a loop — read, reason, act, observe, repeat — over an accumulating context the engineer must manage. The frontier model inside the loop is rarely the limiting factor. What limits it is *what it knows at a given step*: how much of its instruction budget is already spent, whether the context has been polluted by failed attempts and stale reads, and whether untrusted file content has slipped instructions into the stream. This chapter teaches four moves that engineer the context system rather than the wording: persistent instruction files (CLAUDE.md / AGENTS.md) kept as a short onboarding map; the plan-then-execute split that quarantines exploratory context; token-budget management; and an injection-aware permission posture grounded in Simon Willison's "lethal trifecta." This is an *overview*. The depth treatment is the companion volume *Prompt Engineering for CLI AI Coding Agents*.

---

## Learning objectives

By the end of this chapter you should be able to:

1. **Explain** (Understand) how the read→reason→act→observe loop of a stateful CLI agent differs from one-shot chat prompting, and why "context rot" has no chat equivalent.
2. **Explain** (Understand) why a persistent instruction file is delivered as an influential-but-not-absolute user-message reminder, and what the instruction-capacity ceiling implies for its length.
3. **Apply** (Apply) the plan-then-execute split and token-budget management to a scoped refactor, including explicit scope, stopping conditions, and verification commands.
4. **Apply** (Apply) an injection-aware permission posture using the lethal-trifecta test to decide where sandboxing and approvals must sit.
5. **Analyze** (Analyze) a degraded agent session to classify whether the cause is context rot, instruction overflow, or prompt injection.

## Prerequisites

Ch. 4 (Sycophancy and Computational Skepticism) — the skepticism posture, here turned toward untrusted file content. Ch. 9 (Prompt Brittleness and Evaluation) — eval discipline, here applied to verifying what an agent actually loaded and did. Ch. 10 (Long-Context Prompting) — position effects, recency, and the failure of attention to spread evenly over a long window; context rot is the agent-scale expression of those effects. Ch. 11 (Agentic and Multi-Turn Systems) — the ReAct loop and tool exposure, which this chapter applies to coding specifically.

---

## 14.1 A session that got worse the longer it ran

The session below is a composite, assembled from documented CLI-agent failure patterns rather than a single transcript. The mechanism is real; the specific run is reconstructed.

A Wordsville engineer opens a coding agent in the project repository to fix a bug in the dialogue renderer. The first ten minutes go cleanly. The agent reads the renderer module, locates an off-by-one in a loop that truncates the last line of NPC dialogue, proposes a one-line fix, runs the test suite, and reports green. Good.

Then the engineer keeps going in the same session. "While you're here, also fix the inventory serializer." The agent reads three more files, tries an approach, hits a failing test, tries another, hits a different failing test, reads two more files to understand why, finds a third approach, and lands it. "Now the save-game migration." More reads. A failed attempt. A correction. Another failed attempt. A correction to the correction.

By the time the engineer says "okay, now go back and also handle the empty-dialogue edge case in the renderer" — the very module the agent fixed cleanly an hour ago — the agent does something strange. It re-edits the renderer using the *old, buggy* loop bound, reintroducing the off-by-one it had already fixed. It cites a test command that the project doesn't use. It writes a helper function that duplicates one it read forty minutes earlier. Nothing in its output announces a problem. The prose is confident. The diffs look plausible.

The engineer's instinct is to blame the model: it "got dumber," or "got tired," or "lost the thread." None of that is what happened. The model is exactly as capable as it was in minute one. What changed is the *context it is reasoning from*. The window now holds a sediment of failed attempts, superseded approaches, stale file contents that no longer match disk, and corrections layered on corrections. The agent is not confused in the human sense. It is working faithfully from a context that **no longer represents the current state of the world.** This failure mode is called **context rot**, and it has no equivalent in one-shot chat, because chat has no accumulating state to rot.

Here is the diagnostic move that proves it: open a *fresh* session and ask the agent, with no history, to handle the empty-dialogue edge case in the renderer. It does it cleanly, the way it did in minute one. Same model, same task, different context — and the difference is the whole story.

That is this chapter's thesis, stated by the field's own practitioners: **in CLI coding agents, context is the bottleneck, not intelligence.** Frontier models are capable enough. The failures cluster around what the model knows at a given step, how many instructions it is being asked to hold at once, and whether the context has been polluted. The engineering discipline that follows is not about wording. It is about designing and defending the *context system* the agent reasons from.

A scope note before we go further. This chapter is an **overview**. It teaches the stable core — statefulness, the token budget, persistent instruction files, the plan-then-execute split, and injection security — at the depth a single chapter allows. The full treatment, with tool-by-tool behavior, the instruction-capacity math worked out, multi-session continuity patterns, and the complete security landscape, is the companion volume *Prompt Engineering for CLI AI Coding Agents* (covering Claude Code, Codex CLI, Cursor, Aider, and Cowork). Where you want depth, go there.

---

## 14.2 Statefulness and the token budget

Start with the structural difference, because everything else follows from it.

A chat prompt is a single instruction with a single response. You write, the model answers, and the interaction is — from the model's side — stateless. A CLI coding agent runs a **loop**: it reads a file, reasons about what it read, takes an action (an edit, a shell command, a tool call), observes the result, and repeats. Each pass appends to a context the engineer is responsible for managing. The agent is not answering a question; it is conducting an investigation whose notes pile up in front of it.

This is the same Thought→Action→Observation loop developed in Ch. 11, now running against a filesystem instead of a generic tool set. The new fact at the coding-agent scale is that the loop *fills the context fast*. A single bug investigation can read a dozen files, run the test suite three times, and accumulate several failed-attempt diffs — tens of thousands of tokens, none of which the model chose to forget.

### The 80% rule

Practitioner experience and Anthropic's own auto-compaction defaults converge on a working rule of thumb: output quality begins to degrade as the context approaches roughly **80% of capacity** [practitioner heuristic, not a published threshold; auto-compaction in Claude Code triggers in this range]. Treat that figure as a soft architectural constraint rather than a sharp cliff: the practical implication is that you should plan to *restart or compact* around 80% rather than watch quality erode while you fill the last fifth.

We can make the intuition explicit. Let $C$ be the context window size in tokens and $u(t)$ the tokens consumed after $t$ loop iterations. Useful work continues while

$$u(t) < 0.8\,C.$$

The trouble is that $u(t)$ is *monotonically increasing* — the loop only ever adds. Every file read, every tool result, every error message, every prior turn stays in the window unless you explicitly remove it. So the engineering question is not "how do I make the model smarter" but "how do I keep $u(t)$ below the degradation threshold while still giving the agent what it needs." Two levers: put less in (be selective about reads, prefer pointers to copies), and take stale material out (compaction, fresh sessions). Both are context engineering, not prompt wording.

This connects directly to Ch. 10. Long-context models do not attend uniformly across the window; instructions placed early lose salience as later tokens accumulate, and a window stuffed with near-duplicate or contradictory material produces the multi-needle collapse you measured there. **Context rot is the agentic, accumulating version of that effect**: the renderer fix in §14.1 was still *in* the window when the agent re-broke it, but buried under an hour of superseded material, competing for attention with everything that came after.

### A misconception worth killing early

The common belief is that a bigger context window solves this — that a million-token window means you never have to manage context. It does not. A bigger window raises $C$, which buys you more iterations before the 80% line, but it does nothing about the *quality* of attention over a polluted window. A window full of stale reads and failed attempts is a worse working context at one million tokens than a clean window at one hundred thousand. Capacity is not the same as signal. The skill is curating what occupies the window, not maximizing the window.

---

## 14.3 Persistent instruction files replace the system prompt

In chat, the system prompt carries your standing instructions. A CLI agent has a system prompt too, but you usually cannot edit it — it belongs to the tool. The lever you *do* control is a **persistent instruction file** that the agent reads at session start and re-reads during operation: `CLAUDE.md` for Claude Code, the emerging cross-tool `AGENTS.md` standard, `.cursorrules` for Cursor and Windsurf. These files survive across the loop's re-reads, compaction, and summarization in a way that a single opening message does not.

### Where the file actually lands — and why that matters

Here is the design fact that surprises most engineers, and that explains a lot of "why won't it follow my rules" frustration. In Claude Code, `CLAUDE.md` is **not injected as the system prompt.** It is delivered as a `<system-reminder>` block inside a *user* message, after the real system prompt, carrying a caveat to the effect of: *this context may or may not be relevant; you should not respond to it unless it is highly relevant.*

Read that caveat carefully, because it determines how your file behaves. Your instructions are **influential, not absolute.** They sit in user-message position, which means the model weighs them against everything else in the window rather than treating them as inviolable. And the agent is explicitly instructed to *ignore sections it judges irrelevant* — a guardrail added after narrow, hotfix-laden instruction files were observed to degrade performance by injecting task-specific noise into every unrelated request. The consequence for design is sharp: **only universally applicable instructions belong in the file.** A rule that matters for one module, dropped into the global file, is either ignored (when irrelevant, wasting space) or misapplied (when the model wrongly judges it relevant). Vague or conflicting rules get applied inconsistently for the same reason.

### The instruction-capacity ceiling

There is a second, harder limit, and it is the one that turns "write good rules" into "write *few* good rules." A model can only follow so many distinct instructions before adherence degrades. Practitioner research circulating in 2025 (via HumanLayer) puts the ceiling for frontier thinking models at roughly **150–200 distinct instructions** before adherence breaks down; smaller or non-thinking models decay faster (exponentially rather than linearly). Crucially, the agent's *own* system prompt is reported to consume on the order of **50 of those slots** before your file ever loads — leaving you perhaps 100–150. [These are practitioner figures circulated via HumanLayer, not numbers from a controlled, published study — treat them as order-of-magnitude guidance, not measured constants.]

Two consequences follow, and the second is the dangerous one.

First, budget discipline: you are not writing into an empty instruction space. You are writing into a space that is already a third full before you type a character.

Second — and this is the part that should change your behavior — past the threshold, models are reported to **ignore instructions roughly uniformly, not selectively.** It is not that your 201st instruction gets dropped while the first 200 hold. It is that *all* of them start to slip. This is why a bloated instruction file is worse than a short one even for the rules it shares with the short version: the bloat degrades adherence to everything, including the rules you cared about most. The mechanism rhymes with the long-context dilution of Ch. 10 — too many competing directives, like too many competing tokens, flatten the salience of each.

The practical ceiling that falls out of this is **roughly 80–120 lines, and under 100 is better.** HumanLayer reports running a production file under 60 lines [practitioner report, not a controlled study]. The file is an *onboarding map*, not a manual.

### What belongs, what doesn't

The map answers three questions:

- **WHAT** — the tech stack, the project structure, a directory map. Where things live.
- **WHY** — the purpose and the design intent, so the agent can make judgment calls in situations the rules don't cover.
- **HOW** — the exact verification commands: how to run tests, type-check, build, lint. Not "run the tests" but the literal command string.

What does *not* belong: code-style rules (a linter enforces those far more reliably than an instruction the model might judge irrelevant); task-specific instructions (ignored when off-task, costly when wrongly applied); commands the agent can discover for itself; and anything that could be loaded on demand from a sub-file.

### Progressive disclosure: the `agent_docs/` pattern

That last category — "anything that could be loaded on demand" — is the lever that keeps the file short without losing detail. Keep `CLAUDE.md` minimal and make it an **index** that points to deeper documents the agent reads only when relevant:

```
agent_docs/
  building.md
  running_tests.md
  code_conventions.md
  service_architecture.md
  database_schema.md
```

The agent loads `database_schema.md` when it's touching the database and ignores it otherwise. This is **progressive disclosure**: the standing context stays small (protecting the instruction budget and the token budget both), while depth is available on demand. Anthropic's Agent Skills (a `SKILL.md` plus metadata) formalize the same idea — a short always-loaded header pointing to detail loaded when triggered.

One discipline within the pattern: **prefer pointers to copies.** A path or a file-plus-line-number reference (`see src/render/dialogue.ts:142`) stays correct as the code evolves; a copied snippet goes stale the moment someone edits the original, and a stale snippet in your instruction file is a context-rot generator you built on purpose.

And one cheap trick that exploits Ch. 10's recency effect directly: **restate your most critical rules at the *end* of the file as well as the top.** Claude Code's own system prompt repeats its hardest constraints at the bottom for exactly this reason — the most recent tokens carry disproportionate salience. Top *and* end.

> **Current tools (as of 2026).** These details age fastest; the companion volume tracks them. *Claude Code:* repo-level, directory-scoped, and user-global `~/.claude/CLAUDE.md` files with scope inheritance; delivered as the `<system-reminder>` user-message block described above. *Codex CLI:* uses `AGENTS.md`, with a hard **32 KiB combined project-doc limit** — exceed it and large files silently truncate, so a too-long file can vanish without warning. *Cursor / Windsurf:* `.cursorrules`, capped at **6,000 characters per file and 12,000 total**, with Always-On / Manual-(@mention) / Model-Decision rule modes and glob frontmatter for scoping. *Aider:* convention files via `/read CONVENTIONS.md` (read-only, cached), plus its distinctive **repo map** — a concise summary of key files, symbols, and signatures sent with each request, its answer to large-codebase context. *Continue:* rules apply to Agent/Chat/Edit but **not** autocomplete/apply — verify mode coverage. `AGENTS.md` is an emerging cross-tool standard, not yet universal; check per-tool support. Treat every number here as verify-before-print.

---

## 14.4 Context engineering for large codebases

Two kinds of context fail in two different ways, and confusing them sends you fixing the wrong thing.

**Static context** is what you set before the session: the system prompt, `CLAUDE.md`, the rules files. Its characteristic failure is *consistent convention violations* — the agent always names things the wrong way, always misses a required step — because the standing instruction is missing, wrong, or being judged irrelevant.

**Dynamic context** is what arrives during the loop: file contents, tool results, conversation history. Its characteristic failure is *acting on stale or incomplete information* — the agent edits against a version of a file that has since changed, or never read the file that mattered. Context rot is a dynamic-context failure.

The fix differs by kind. A consistent convention violation is a static-context bug: fix the instruction file. An acting-on-stale-info failure is a dynamic-context bug: no amount of rewriting `CLAUDE.md` fixes it, because the rule was fine — the working context was wrong. Diagnose which kind you have before you touch anything.

### Cache-stable layout

A subtle static-context discipline: **keep the instruction file's content stable across sessions.** Prompt caching keys on prefix stability — everything after a changed segment is a cache miss. Drop a dynamic timestamp or a frequently-edited "current task" line into `CLAUDE.md` and you invalidate the cache for everything below it on every session, paying full price to re-process content that didn't change. The lesson generalizes: put volatile material in dynamic context where it belongs, and keep static context static.

### Monorepos and the whole-repo-dump temptation

For a large or multi-package repository, the instinct is to give the agent "all the context" — dump the repo into the window so it knows everything. This is the misconception §14.2 warned about, at architectural scale. It blows the token budget, dilutes attention, and seeds context rot. The disciplined moves instead:

- **Directory-scoped instruction files** — a `CLAUDE.md` per package, loaded when the agent works in that package, so each scope sees only its own rules.
- **On-demand architecture docs** — ADRs, module READMEs, the `agent_docs/` index — loaded when relevant rather than up front.
- **Sub-agents over dumps** — when you need to understand several modules, dispatch focused sub-agents to analyze each in parallel and return *summaries* to a coordinator that holds the summaries, not the full file contents. This is the operator-plus-workers pattern from Ch. 11, applied to keep the coordinator's window clean: the coordinator reasons over compressed findings while each worker burns its own (disposable) context on the raw material.

The through-line of this whole section is one rule: **the agent should read what it needs, when it needs it, and no more.** Selectivity is the skill.

---

## 14.5 Plan in one session, execute in another

This is the single highest-leverage workflow change in the chapter, and it follows directly from §14.2's monotonic-fill problem.

Exploration is dirty. To plan a non-trivial change, the agent reads widely, considers approaches, and rejects most of them. That rejected material — the tangents, the dead ends, the "actually no" reversals — is *exactly* the sediment that produces context rot. If you then execute in the same session, the agent executes from a window full of the approaches it already discarded. The §14.1 renderer regression is this failure: an hour of superseded exploration buried the clean answer.

The fix is to quarantine exploration from execution:

1. **Plan** in one session. Let the agent explore freely, read what it needs, and produce a written plan.
2. **Save the plan** to a markdown file — the durable artifact.
3. **`/clear` or open a fresh session** — discard the polluted exploratory context entirely.
4. **Execute** from *only* the plan document, in a clean window.

The execution session never sees the dead ends. It sees a clean plan and a clean window, which is the condition under which the agent performed well in §14.1's minute one. This is Anthropic-endorsed practice, and the mechanism is exactly the token-budget and context-rot mechanics of §14.2: you are resetting $u(t)$ to near zero and loading only signal.

### What a good execution prompt specifies

A plan that an agent can execute cleanly names four things:

- **Scope** — which files are in bounds and which are out. "Only touch `src/render/`; ask before editing anything else."
- **Stopping condition** — what "done" looks like, concretely, and how to check it. Not "fix the bug" but "the empty-dialogue case renders without truncation and `npm test` is green."
- **Acceptance criteria** — the exact checks to run: the test command, the type-check command, the lint command.
- **Workflow** — the loop discipline: inspect before editing, summarize the plan for review before irreversible actions, make the *smallest* change that satisfies the criteria, run the verification command, then stop and summarize the diff.

For repeated workflows, capture them as **reusable slash commands** (`.claude/commands/*.md`) — a `/commit` command, a `/run-tests-and-summarize` command — so the discipline is encoded once rather than retyped.

### The two-correction rule

When an execution attempt fails, the temptation is to correct it in place: "no, not like that, try this." After one or two corrections, *stop.* Each correction layers more superseded reasoning into the window — you are correcting your way into context rot. The practitioner rule of thumb: **after two failed corrections, `/clear` and write a fresh prompt** that folds in what you learned. Don't correct out of a polluted session; start a clean one with better instructions. This is the plan→execute split applied at small scale, mid-task.

> **Worked example — from rule-dump to onboarding map, then a clean refactor.**
>
> *Starting point.* The Wordsville repo has a 340-line `CLAUDE.md` that began as a useful file and grew into a junk drawer: every code-style preference ("use 2-space indents," "prefer `const`"), a dozen one-off hotfix notes ("when editing the combat module, remember the 2024 damage-formula change"), full pasted copies of the database schema and three service interfaces, and a buried, correct set of test commands. It is well over the instruction-capacity ceiling, and adherence has been slipping for weeks — the agent ignores rules unpredictably, which is the uniform-degradation signature from §14.3.
>
> *Step 1 — cut to the map.* Delete the code-style rules (the linter enforces them). Delete the hotfix notes (task-specific; they belong in the relevant module's `agent_docs/`). Replace the pasted schema and interfaces with **pointers** (`see agent_docs/database_schema.md`, `see src/services/README.md`). Keep WHAT (stack, directory map), WHY (this is a text-adventure engine; dialogue correctness is safety-critical for the gameplay contract), and HOW (the exact `npm test`, `npm run typecheck`, `npm run lint` strings). Restate the two hardest rules — "inspect before editing; smallest change that passes" — at the end. The file lands at **84 lines.**
>
> *Step 2 — build the `agent_docs/` index.* Move the schema, service architecture, build notes, and the combat-module hotfix into `agent_docs/{database_schema,service_architecture,building,combat_notes}.md`, and make `CLAUDE.md`'s last section a one-line-each index pointing at them. Standing context shrinks; depth is now on demand.
>
> *Step 3 — plan the refactor (session A).* Task: extract the duplicated dialogue-truncation logic (the §14.1 bug lived in one of two copies) into a single helper. The agent explores both call sites, the renderer, and the relevant test files, and writes `plans/dedupe-truncation.md`: the two call sites, the proposed helper signature, the files in scope, and the verification commands. It tried one approach (a shared mixin) and rejected it — that dead end is now in session A's polluted window.
>
> *Step 4 — execute (session B).* `/clear`. Fresh session. Prompt: *"Execute `plans/dedupe-truncation.md`. Scope: only `src/render/`. Stopping condition: both call sites use the new helper, no behavior change, `npm test` green. Inspect before editing; smallest change; run `npm test` then stop and summarize the diff."* The agent — working from a clean window and a clean plan, never seeing the rejected mixin approach — lands the extraction, runs the tests, and stops. No regression, because the discarded exploration was discarded.

---

## 14.6 Multi-session continuity and injection security

Two problems remain, and they are the ones the loop's statefulness forces on you.

### Continuity: the model is stateless across sessions

`/clear` is a feature, but it cuts both ways: an LLM retains nothing across sessions. Whatever the agent "knew" at the end of session A is gone at the start of session B unless you persisted it *explicitly.* Three patterns do this:

- **Compaction.** `/compact` summarizes the history while preserving critical state, freeing budget without a full reset. You can customize what it preserves through the instruction file ("when compacting, keep the modified-files list and the test commands"). The §14.2 discipline applies: compact or restart around 80% rather than watching quality degrade in the last fifth.
- **Session notes / work logs.** Write a status file at the end of a session (files changed, tests run, open risks, follow-ups) and read it at the start of the next — a durable handoff note the next session loads as its starting context.
- **Registry / sub-agent patterns.** A coordinator keeps a date-stamped registry of what's been done; sub-agents return summaries. The sequencing rule: if agent B needs agent A's output files, run them sequentially; otherwise run in parallel. Git worktrees give parallel agents clean, isolated working trees.

These tie back to Ch. 9: a handoff note is only useful if it accurately records what *actually* happened, which means verifying the agent's claims (did the tests really pass?) rather than trusting its summary. Eval discipline does not stop at the session boundary.

### Security: the least-solved problem in the chapter

Now the hard part. A chat model reads what you send it. A CLI coding agent reads *the filesystem* — and a file is an instruction-delivery vector. Every README, every code comment, every dependency's docstring, every test fixture, every `.env`, every `.vscode/settings.json` is text the agent ingests, and any of it can carry instructions aimed at the agent rather than at you. The attack surface is vastly larger than chat's, and it expands further the moment the agent can read issues, email, or the web.

The framing that organizes this comes from Simon Willison: the **lethal trifecta.** An agent is exploitable, regardless of how well the model is hardened, when all three of the following are true:

1. it has access to **private data** (your repo, your secrets, your environment);
2. it is exposed to **untrusted content** (file contents, dependencies, web results it didn't author);
3. it can **communicate externally** (network calls, writing files, opening PRs, running shell commands).

A default CLI coding agent has all three. That is the point of Willison's framing: the danger is not a clever individual exploit but the *structural combination.* If an attacker can get text in front of the agent (untrusted content) while the agent can read your secrets (private data) and make a network call (external communication), the attacker can in principle read+exfiltrate. Documented patterns include file-content injection that reads and exfiltrates secrets, poisoned editor config that achieves code execution, and malicious MCP server entries that reach arbitrary command execution. A single 2025 disclosure reported **30+ vulnerabilities across six tools** (Cursor, Roo Code, JetBrains Junie, Copilot, Kiro.dev, Claude Code), including a Codex CLI MCP-entry path (CVE-2025-61260, patched in Codex CLI 0.23.0). OWASP's 2025 Top-10 for LLM Applications lists prompt injection at **#1**, and notes there is no foolproof model-layer prevention.

This is where Ch. 4's computational skepticism returns, now aimed at files. The skepticism posture treats user assertions as claims to be checked rather than facts to be accepted; the agent version treats *file content* the same way — text in a repo is data to be processed, never instructions to be obeyed.

**What prompting can do.** You can reduce blast radius. Instruct the agent to treat repository text as untrusted data, never to follow instructions embedded in files, to make conservative writes, to require confirmation before destructive operations, never to print secrets, and to stay within an explicit scope. These are real mitigations — they shrink what a successful injection can accomplish.

**What prompting cannot do.** Against a determined attacker, prompting *cannot prevent injection.* An instruction in your file is influential, not absolute (§14.3) — and so is an instruction in the attacker's file. You cannot out-prompt a structural vulnerability. The trifecta is a property of the architecture, not of the wording, so the defense must be architectural too:

- **Sandboxing** — run the agent in a container or restricted filesystem so a successful injection can't reach your real secrets or your real network.
- **Disable auto-approve on untrusted repos** — a human approves shell commands and writes when the code isn't yours.
- **MCP permission scoping** — limit which tools the agent can call, cutting the "external communication" leg.
- **Human review** of irreversible actions.

The operating rule, stated plainly: **treat any repository you did not author as hostile, and never enable auto-approve on an unfamiliar codebase.** The model is not your security boundary. The architecture is.

A misconception to retire on the way out: "a better, more aligned model will solve prompt injection." It will not, any more than a better-behaved employee solves the problem of a building with no locks. As long as the three legs of the trifecta are present, the exposure is present. Hardening the model raises the cost of an attack; it does not remove the surface.

---

## 14.7 Three failures, one question

The three failure modes this chapter teaches look similar from the outside — the agent does something wrong, confidently — but they have different causes and different fixes, and the diagnostic question that separates them is short.

| Symptom | Likely cause | The test | The fix |
|---|---|---|---|
| Was clean early, degrades as the session runs long; re-breaks fixed code; cites stale commands | **Context rot** (dynamic) | Does it work cleanly in a *fresh* session? | `/clear`, plan→execute split, compaction |
| Ignores rules from turn one, *unpredictably*, even short tasks; adherence slips across the board | **Instruction overflow** (static) | Is the instruction file over ~100 lines / past the capacity ceiling? | Cut to an onboarding map; `agent_docs/` |
| Takes an action no one asked for, especially after reading an unfamiliar file; touches secrets or network | **Prompt injection** | Did it just read untrusted content while holding the trifecta? | Sandbox, revoke auto-approve, scope tools |

The single question that routes you: **does it work in a fresh session?** If yes, you have context rot or injection (state-dependent). If it fails even fresh and clean, you have an instruction problem or a task-beyond-scope — fix the file, not the session. Run that test first; it is the agentic analog of Ch. 6's single-turn isolation test and Ch. 9's insistence on controlled comparison.

---

## Exercises

**14.1 (Analyze).** You are given three CLI-agent transcripts (provided in the course repo, `exercises/ch14/`). In transcript A, the agent fixes a module cleanly, then after 40 minutes of unrelated work re-introduces the bug it fixed. In transcript B, the agent ignores the project's stated test command from the very first turn, on a trivial task, with a 280-line `CLAUDE.md`. In transcript C, the agent reads a third-party dependency's README and then attempts to `curl` an external URL with an environment variable in the query string. For each, classify the failure as context rot, instruction overflow, or prompt injection, state the one-line diagnostic test you'd run to confirm, and name the fix. (Use the §14.7 table, but justify each call from the *mechanism*, not the table row.)

**14.2 (Apply).** You are handed a 300+-line `CLAUDE.md` (provided). Rewrite it under the capacity ceiling: produce a `CLAUDE.md` of under 100 lines that is a genuine onboarding map (WHAT / WHY / HOW), plus an `agent_docs/` index of at least three load-on-demand files showing what you moved out and why. Replace at least two pasted snippets with pointers. In a short paragraph, explain which cuts protect the *instruction* budget and which protect the *token* budget — and why a code-style rule belongs in neither.

**14.3 (Create — produce something).** Pick a real repository you have access to (or the course's Wordsville fork). Produce a **CLAUDE.md + task-prompt pair** for a single scoped change. The `CLAUDE.md` must include a Security section that names the lethal trifecta and states a permission posture. The task prompt must specify scope (paths in/out), a stopping condition with a concrete verification command, acceptance criteria, and the inspect→plan→minimal-change→verify→summarize workflow. Then actually run a plan→execute split on it (plan in one session, `/clear`, execute in another) and append a one-paragraph note on whether the split changed the agent's behavior versus doing it all in one session.

**14.4 (Evaluate, optional).** Take a non-trivial task and run it two ways: (a) entirely in one long session, correcting in place as needed; (b) as a plan→execute split with a two-correction-then-clear rule. Track context usage (% of window) and count the regressions or stale-reference errors in each. Report whether the split's overhead paid for itself, and at what task size you'd expect the answer to flip.

---

## What would change my mind

A controlled study showing that, holding the model fixed, a deliberately *polluted* long session (sediment of failed attempts and stale reads) produces output of equal quality to a fresh-context execution of the same final task — across a representative set of coding tasks and a defensible scoring standard. This chapter's central claim is that context state, not model capability, drives the §14.1 degradation; the plan→execute split earns its overhead only if the fresh window genuinely outperforms the polluted one. Evidence that careful in-session correction closes the gap would force a re-specification of *when* the split's cost is worth paying — and would weaken "context is the bottleneck" toward "context is *a* bottleneck, sometimes."

Separately, a demonstrated *model-layer* defense that reliably prevents prompt injection while the lethal trifecta remains structurally present would overturn §14.6's claim that the defense must be architectural. I am not holding my breath, but it is the falsifiable form of the claim.

---

## Still puzzling

1. **Where exactly is the instruction-capacity ceiling, and is it really uniform degradation?** The ~150–200 figure is practitioner-reported, not a measured curve with error bars, and the claim that adherence fails *uniformly* past the threshold (rather than dropping the marginal instruction) deserves a controlled experiment. The fix-the-file advice survives either way, but the mechanism story would change.

2. **Is "context rot" one phenomenon or several?** We have lumped stale reads, superseded approaches, and contradictory corrections under one name because they share a fix (fresh context). It is not obvious they share a mechanism at the attention level. Ch. 10's position effects, near-duplicate dilution, and contradiction-handling might be three distinct failures wearing one label.

3. **Does the plan→execute split's value scale with model capability, or against it?** As models get better at ignoring irrelevant context, the cost of a polluted window should fall — which would erode the split's payoff over time, the same way Ch. 8's reasoning-tuned models eroded explicit CoT's value. Or the opposite: bigger windows invite bigger pollution. Unclear which trend wins.

4. **Can the lethal-trifecta exposure be measured, not just asserted?** "All three legs present ⇒ exploitable" is a structural claim. A quantified exploit-success rate as a function of which legs are cut (sandbox on/off, auto-approve on/off, network on/off) would turn a binary warning into a risk model an engineer could budget against.

---

## References

- Willison, S. (2025). *The lethal trifecta for AI agents: private data, untrusted content, and external communication.* simonwillison.net, Jun 16, 2025. https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/
- Anthropic (2025). *Effective context engineering for AI agents.* Anthropic Engineering blog (Sep 2025). https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
- Anthropic (2025). *Equipping agents for the real world with Agent Skills.* Anthropic Engineering blog (Dec 18, 2025). https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills
- Anthropic. *Best practices for Claude Code* (code.claude.com/docs) — best practices, modifying system prompts, context management.
- HumanLayer (2025). *Writing a good CLAUDE.md* (Nov 2025) — instruction-capacity and file-length practice [practitioner write-up, not a peer-reviewed study].
- Yang, J., et al. (2024). *SWE-agent: Agent-Computer Interfaces Enable Automated Software Engineering.* NeurIPS 2024.
- Zhan, Q., et al. (2024). *InjecAgent: Benchmarking Indirect Prompt Injections in Tool-Integrated Large Language Model Agents.* ACL 2024.
- OWASP (2025). *Top 10 for Large Language Model Applications* — prompt injection ranked LLM01 (#1). https://genai.owasp.org/llmrisk/llm01-prompt-injection/
- VILA-Lab (Liu, J., Zhao, X., Shang, X., & Shen, Z.). *Dive into Claude Code: The Design Space of Today's and Future AI Agent Systems* — corpus of 253 CLAUDE.md files across 242 repos. arXiv:2604.14228.
- The Hacker News / Cymulate (Dec 2025). *Researcher uncovers 30+ flaws in AI coding tools enabling data theft and RCE.* CVE-2025-61260 — OpenAI Codex CLI auto-executes MCP server entries from local config without approval; patched in Codex CLI 0.23.0.
- *Companion volume:* Brown, N. B. *Prompt Engineering for CLI AI Coding Agents* (Claude Code, Codex CLI, Cursor, Aider, Cowork) — the depth treatment behind this overview chapter.

---

**Tags:** cli-coding-agents, context-is-the-bottleneck, context-rot, claude-md, agents-md, instruction-capacity-ceiling, plan-then-execute, token-budget, lethal-trifecta, prompt-injection, progressive-disclosure
