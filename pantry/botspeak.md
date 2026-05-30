# Botspeak

*The Irreducibly Human Practitioner's Guide to AI Fluency*

Nik Bear Brown

---

## Copyright

© 2026 Nik Bear Brown. All rights reserved.

No part of this book may be reproduced, stored in a retrieval system, or transmitted in any form or by any means — electronic, mechanical, photocopy, recording, or otherwise — without the prior written permission of the author, except for brief quotations used in critical review.

The companion volume *How to Speak Bot* is referenced throughout as a pattern reference.

First edition. Published 2026.

---

## Dedication

For the recent graduate who suspects, correctly, that AI fluency is a teachable practitioner discipline — and not a personality trait that some people happen to have.

---

## How to read this book

This is a handbook, not a textbook in the sense your finance class used the word. The architecture is built so that you can pick the chapter that addresses the capacity you most want to move up one level — and read in that order rather than in mine.

If you are reading start-to-finish: Chapter 0 is the puzzle that motivated the whole project, and Chapters 1 and 2 set up the workflow (the Loop) and the vocabulary (the Nine Capacities) that the rest of the book builds on. Chapters 3 through 8 work through one capacity each in the Augmentation mode — you at the keyboard, in the loop, every move. Chapters 9 and 10 reweight the Loop for Automation — the version where you are not at the keyboard while the work happens. Chapters 11 and 12 reweight again for Agency — the unbounded autonomy case, where the structural failures are different and harder. Chapter 13 is what the practice looks like once it is reflex.

If you are reading by capacity: the Nine Capacities chapter (Ch. 2) ends with a self-assessment grid. Pick the two capacities you most want to move up one level in the next ninety days. The chapter list at the end of Ch. 2 maps capacity to chapter. Read those first.

Either way: the worked examples are not problems you watch the author solve. They are tasks you execute. The exercises at the end of each chapter are not optional. They are the practice the book is for.

The byline is mine. The voice is my current reading. If a chapter's reading turns out to be wrong, I would rather hear it from a careful reader than read it again two years from now in a footnote I should have written myself.

— Nik Bear Brown

<!--
00-introduction.md — Book-level introduction.

The Introduction does different work than the Preface:
  - Preface  = why the book exists, why you wrote it (author's voice)
  - Introduction = what the book argues and how it is organized (reader's roadmap)

This file is a stub. Sections 1–10 and 12–13 are placeholders for a later pass.
Section 11 (A note about AI) is substantive and written.

A good model for the full version: Pearl's "The Mind Over Data" introduction,
Molnar's Interpretable ML introduction. Both are argument-first and tell the
reader exactly what to expect from each chapter.
-->

# Introduction

<!-- [1] COLD OPEN
     A specific named scene with real stakes.
     No "this book will...", no throat-clearing.
     Open on a sentence that contains the whole problem.
     Like the Swedish triage case in computational-skepticism-for-ai. -->

[COLD OPEN PLACEHOLDER]

<!-- [2] THE CENTRAL CLAIM — one sentence.
     "This book is about the gap between [X] and [Y]." -->

[CENTRAL CLAIM PLACEHOLDER]

<!-- [3] THE CENTRAL ARGUMENT — a testable, contestable claim
     about what the book is doing. -->

[CENTRAL ARGUMENT PLACEHOLDER]

<!-- [4] AUDIENCE LOCATION — one sentence locating who this is for. -->

[AUDIENCE PLACEHOLDER]

---

## What This Book Is

<!-- [5] Scope. The work the book names. Vocabulary it teaches. -->

[SCOPE PLACEHOLDER]

## What This Book Is Not

<!-- [6] Explicit exclusions. Prerequisites. -->

[EXCLUSIONS PLACEHOLDER]

---

## A Central Concept That Runs Throughout

<!-- [7] A recurring idea readers should watch for across chapters.
     Like "the fluency trap" in computational-skepticism-for-ai. -->

[CENTRAL CONCEPT PLACEHOLDER]

<!-- [8] (OPTIONAL) A RUNNING NARRATIVE THREAD
     A case that recurs across chapters as a worked example.
     Like "Ash" in computational-skepticism-for-ai.
     Delete this section if not using a running thread. -->

## A Running Narrative Thread

[NARRATIVE THREAD PLACEHOLDER — delete this section if not using one]

---

## How This Book Is Organized

<!-- [9] Chapter-by-chapter map. Group into movements (clusters of 3–5)
     if applicable. One sentence per chapter is enough. -->

[CHAPTER MAP PLACEHOLDER]

## How to Read This Book

<!-- [10] Order. Prerequisites for skipping around.
     Self-contained chapters. Chapter-closing features
     (e.g., "What would change my mind", "Still puzzling", exercises). -->

[READING GUIDE PLACEHOLDER]

---

## A Note about AI

This book teaches nine capacities for fluent practice with AI systems. Each chapter ends with a chapter-specific *A note about AI* that names how the local capacity is helped and damaged by the same tools the book is teaching you to work with. The unifying principle across the chapters: **the capacities are practiced, not recited.** The model can describe specification, delegation, conversation, discernment, and diligence fluently — only you can perform them. Use the chapter notes for the specific moves. The book's posture toward AI is the posture it teaches: use the tools deliberately, evaluate the results carefully, and remain the locus of judgment when the work goes wrong.

---

## Closing

<!-- [12] Callback to the opening scene. End with a directive. -->

[CLOSING PLACEHOLDER]

---

**Tags:** <!-- [13] 5–8 discoverability tags --> [TAGS PLACEHOLDER]
# Chapter 0 — The Citation That Wasn't

*What the literate practitioner doesn't know they don't know.*

It is 9:42 on a Tuesday morning in Boston, and Priya Banksy is staring at an email she did not expect.

She had published the piece on Friday — forty-two hundred words on what Gen Z believes about the energy transition, prepared on a one-week turnaround for the publication's Climate vertical. Clean structure. Tight prose. The argument hedged in the right places. Eleven hyperlinked citations, including a 2024 Pew Research survey whose finding — *78% of Americans aged 18–29 say they would pay a premium for energy from renewable sources* — anchored the second-most-shared section of the piece. By Sunday evening the piece had been shared eleven thousand times.

The research editor at a competing publication had spent the weekend pulling the citations. Ten checked out. The eleventh did not. There was no 2024 Pew survey on the subject. Not the survey. Not the question wording. Not the 78% figure, which the research editor's email said politely "does not appear in any Pew dataset we have been able to locate," and could Priya help them understand how this happened before the publication's 1 PM editorial meeting?

Priya knows what happened. She had asked Claude for a draft of the section with citations. Claude had given her a draft with citations. She had clicked through nine of the eleven links — the ones to news articles and IEA reports she half-recognized — and they were fine. She had not clicked the Pew link. She had not asked the model whether the survey was real. She had pasted the section into her draft, polished the language, and shipped it. She had not, at any point, treated the output as something that still required pricing.

I want you to sit with that for a moment before we go further, because the failure here is not the one most people will name. Most people who hear this story will say Priya was lazy, or careless, or used the wrong tool. None of those things is true. Priya is twenty-nine years old with a BA from one of India's best-regarded communications programs and a one-year US master's behind her. She prepared meticulously for the case interviews and writing tests that landed her this job. She has used Claude through her master's, through job hunting, through the mock pieces she practiced during onboarding, and in all of those contexts the model gave her useful work. Her publication's onboarding included three slides on AI use. The most important slide said: *Always verify AI outputs before publication.* Priya nodded along. She did not know what verifying actually meant.

That gap — between hearing an instruction and knowing what it actually requires — is the subject of this book.

---

| AI Literacy | AI Fluency |
|---|---|
| Opens a chatbot and types a request | Specifies the task before delegating it |
| Reads the output and judges it by how it looks | Reads the output looking for where it could be wrong |
| Copies and pastes into the deliverable | Treats output as raw material, not finished work |
| Cites what the model returns | Verifies which citations are worth betting the audience's trust on |
| Polishes the prose before shipping | Runs a verification move calibrated to the failure mode |

*"AI Literacy" vs "AI Fluency"*

Let me name two things that look identical from the outside and are not.

The first is AI literacy. Priya has this. She can open a chatbot, type a prompt, read the output, copy and paste. She can, at a taste level, tell polished output from rough output. She has gotten useful work out of these tools many times. Nearly every working professional under fifty has AI literacy now, even when they think they don't, even when their managers worry that they don't. The bar is low and the world has largely cleared it.

AI literacy is necessary. It is not sufficient. It is not sufficient, in particular, when you have a job and the deliverables go to readers. Walking into that situation with only AI literacy is Priya's situation on Tuesday morning. The output looked polished. The output read competent. The output was wrong in a way the literate user cannot detect, because the failure mode is exactly the kind a literate user does not yet know to look for.

The second thing is AI fluency. Priya does not have this — yet. The senior editor down the hall does. It is the actual difference between Priya's piece on Friday and a piece by a senior writer given the same brief.

A senior writer three years ahead of Priya would not have shipped that piece. Not because she is smarter. Not because she is more careful in some vague, unspecifiable way. Not because she has read more books about AI safety. She would not have shipped it because she has a workflow Priya does not yet have. She runs the AI through five steps where Priya ran it through one. When a chatbot hands her eleven citations, she has a habit — a learned reflex — of asking: *which of these are the ones I'd bet the publication's reputation on?* She knows that the citation step is exactly the place a model hallucinates, and she has a verification move calibrated to that risk. She is not surprised when the model fabricates a source. By Tuesday morning, she is only surprised when it doesn't.

That difference is teachable. It has structure. It is not a personality trait, not a function of native carefulness, not something you absorb from another year of undirected experience with the tools. It is a discipline. It is what this book is for.

---

Here is the metaphor I keep coming back to.

A young American goes to India on her first work trip. She has, at some point, picked up a little Hindi — the way Americans pick up a little Hindi when they take a semester of it in college, or date someone whose parents are from Mumbai, or spend a week on Duolingo before the flight. She knows the Devanagari script well enough to sound out syllables, slowly. She knows *namasté* means hello. She knows *kitna* is "how much" and *kahan* is "where." She thinks of herself as someone who can manage.

She arrives at a major railway junction — Nagpur, say, or Itarsi, a hub where a dozen lines cross — and she has forty minutes to find the right platform for the Howrah Express. The departure board is in Hindi. She can read it, after a fashion. She sounds out the letters, matches a few syllables to the train name she wrote in her notebook, finds what looks like a match, and heads confidently toward Platform 7.

The train on Platform 7 is not the Howrah Express. She misread a conjunct consonant — a ligature that collapses two letters into one shape — the kind of thing a real reader processes automatically and a slow reader gets wrong under time pressure. The Howrah Express left from Platform 4. It is now gone.

The tourist who speaks no Hindi at all was never in danger of this. She knew, from the moment she arrived, that she could not read the board. So she found a railway employee, showed him her ticket, and was walked to Platform 4 with ten minutes to spare. She was not surprised when she needed help. She had built "needing help" into her plan.

The Hindi-literate tourist is the one stranded on the wrong platform. She had just enough to feel confident. She did not have enough to catch the error. She had not built "needing help" into her plan because she believed — reasonably, given her experience — that she could handle it. She was the only one who walked into a situation she could not manage and then managed it wrong.

The fluent speaker does not miss the train either, but for a different reason than the tourist who asked for help. She reads the board in one glance, confirms the platform, and has time to buy chai. She did not need to be careful. Careful is what you need when you might be wrong. She was not going to be wrong.

Not being able to read a sign can strand you. But misreading a sign you were confident you could read — that is the specific failure of the person in the middle. Confidence is load-bearing when it is warranted. When it is not, it is the mechanism of the mistake.

Priya, at 9:42 in the morning, is the tourist on the wrong platform. She had enough AI capability to feel confident. She did not have enough to catch the error. The piece looked right. It read like research. The polish was real. The underlying judgment — the judgment that should have caught the eleventh citation — was not there.

This book is not fluency for its own sake. It is the working competence of someone who shows up at the junction *trying* — how do I read this board, how do I confirm I have the right platform, how do I know when I should hand the ticket to someone else. The functional, daily-use skill that gets you on the right train.

---

There is one specific failure mode worth naming now, because it is the one Priya fell into and because most fluent practitioners had to climb out of it themselves before they could see it clearly.

A literate user asked to produce a deliverable gets four pages of output from the chatbot. Four pages, with headings and transitions and bulleted exhibits. The output *looks* like work. It looks, in the way a novice perceives work, exactly the way work is supposed to look. The literate user reads it, lightly polishes it, and ships it. The output is polished. The judgment that should have shaped it is invisible — because the polish is doing the job that judgment used to do.

A fluent practitioner, handed the same four pages, immediately becomes suspicious of them. She knows, because she has been burned, that a language model can fill four pages with confident, structured, citation-bearing prose that is nonetheless wrong in places that matter. To her, the four pages are not work. They are raw material. The work — the part she has to do, the part the model cannot do for her, the part her job actually depends on — has not yet started.

Here is what is strange about this. In almost every other domain, volume is a reasonable proxy for quality. A long memo took someone longer than a short memo. A thick report required more research than a thin one. The world we grew up in trained our intuitions on this correlation, and those intuitions are right nearly everywhere — except here.

Language models broke the correlation. They produce volume at constant cost. The four pages took the same effort to generate as the four sentences. Volume in the post-LLM world is not evidence of effort and not evidence of quality. To the literate eye, it still looks like both. To the fluent eye, it looks like raw material that has not yet been priced.

This is why working professionals ship deliverables their senior colleagues wouldn't, and why those deliverables read polished and read wrong. It is not the only reason. It is the easiest one to name on the first page.

---

I want to be honest about what this book can and cannot do.

It will give you a workflow — five steps, run as a cycle. Specification, Delegation, Conversation, Discernment, Diligence. We will spend a chapter on each. By Chapter 8 you will have run the full cycle on a real task — a piece of your own work — with yourself in the loop. By Chapter 10 you will have learned to run it without yourself in the loop. By Chapter 12 you will have learned to run it when the AI is taking actions in the world on your behalf and not just producing text.

It will give you a vocabulary — names for the moves the senior writer makes that Priya does not yet, so you can recognize them when you are making them and notice when you are skipping them.

**It will give you a portfolio.** This is new. Every chapter of this book produces an artifact you keep. By Chapter 13 you will have a brand-portable record of your AI fluency: three living governing files documenting your method, six customized frameworks adapted to your domain, three pieces of self-knowledge, and one end-to-end case study of your own work taken through every step the book teaches. A future employer, admissions committee, or peer reviewer can read the portfolio without having read this book. The portfolio is the evidence. The closing question of the book — *what specifically did the AI do, and what did you do that it could not?* — is answered by handing over the portfolio.

It will not teach you a specific AI tool. The examples use Claude, with sidebars for ChatGPT and Gemini, but the tools change every six months and the discipline does not. It will not teach AI ethics in the comprehensive sense. It will not teach you the inner workings of language models. There is one paragraph, in Chapter 1, on how an LLM produces its output, because that paragraph does work. The rest of the model-internals literature is a field you can visit afterward.

What it will teach is AI fluency. The difference between Priya on Friday and a senior writer on the same brief. The difference between the practitioner who uses AI to do their job better and the practitioner who uses AI and does their job worse.

---

I will tell you now what I think is the most interesting thing about Priya's situation, because it is easy to miss if you are focused on the mistake.

Her publication hired her specifically because she was AI-fluent at the literacy level. They valued the speed. They counted on it. They gave her a one-week turnaround on a piece that, five years ago, would have been a three-week project for a writer and a fact-checker. The publication bet on AI as a productivity multiplier, and they were right to bet on it, and they staffed the piece assuming the multiplier would hold.

The multiplier did hold. Priya produced forty-two hundred words in four days. The piece looked like four days of work. The piece cost less time and money than four days of pre-AI work would have cost. Everything about the economics worked the way it was supposed to.

And then one citation was wrong, and the whole piece was now in question, and the publication's reputation with its audience had taken a hit it would need months to repair.

This is what I mean when I say AI literacy is not sufficient. The literate user produces *a lot* of work. The problem is that the work is unpriced — the literate user cannot look at her own output and tell where the value is and where the rot is. The publication bet on a productivity multiplier and got one. What they did not yet know is that the multiplier comes with a verification cost, and that someone has to pay it. If Priya does not pay it before the piece publishes, the audience pays it afterward, and the cost the audience pays is denominated in trust.

| Who pays | When | In what currency | Consequence |
|---|---|---|---|
| Fluent practitioner | Before delivery | Her time | Clean deliverable |
| Literate practitioner | Never | Nothing upfront | Audience discovers the error |
| Audience / employer / client | After delivery | Trust, relationship, repair time | Confidence in the practitioner and the publication takes a hit |

The fluent practitioner pays the verification cost in her own workflow, before the work leaves her desk. That is most of what fluency *is*. That is most of what this book teaches.

It is now 9:58 AM on a Tuesday in Boston. Priya has three hours until the 1 PM editorial meeting where she will help draft the correction. The next thirteen chapters are about how she should have spent the previous four days, and what — between now and 1 PM — she can salvage.

By Chapter 8 we will be back at this kind of Tuesday. Priya will be eighteen months further into her career. She will face a comparable brief. She will not ship a citation that doesn't exist. The arc from this Tuesday to that one is the arc the book teaches and the arc the reader walks alongside her, in their own field, with their own work.

Open Chapter 1. We'll start at the beginning.

---

**What would change my mind.** If a serious longitudinal study of working-professional AI use showed that the literate–fluent gap closes within a year of normal job exposure, without any structured framework — that practitioners self-teach fluency from sheer reps — the book's central premise weakens. I have not seen such a study. The closest evidence I am aware of points the other way: literacy plateaus, and the fluency gap persists or widens.

**Still puzzling.** I do not yet have a clean way to distinguish "fluency" from "good judgment shaped by enough painful experience." It is plausible that what I am calling fluency is simply what painful experience teaches anyway, and that naming the moves and rehearsing them just compresses the timeline. I have not yet seen the experiment that would prove it.

---

> **Going deeper — *Computational Skepticism for AI***
>
> Priya's failure has a name in the academic literature: the **fluency trap**. Fluent output triggers an evaluation booster — readers trust well-written prose more than the evidence warrants. The trap doesn't only fool literate users; it amplifies whatever evaluation the reader was going to make, including the wrong ones. The fabricated citation is the visible symptom; the trust-in-the-fluency is the mechanism.
>
> The companion advanced volume *Computational Skepticism for AI* opens by naming this directly and gives you four philosophical moves to interrupt it before it does damage — Cartesian doubt, Hume's induction limit, Popperian falsifiability, and the Plato's Cave move — plus the Five Supervisory Capacities the deeper book is organized around.
>
> See *Computational Skepticism for AI*, **Chapter 1 — The Skeptic's Toolkit**.

---

### Translate before you move on — and start your portfolio

Priya's failure was a journalism artifact: a fabricated source for a load-bearing statistic. In your field, what's the equivalent? Stop and answer before turning the page.

For a clinician, the equivalent is a fabricated drug-interaction reference. For a research scientist, a fabricated primary-literature citation. For a lawyer, an invented precedent. For a teacher, a misattributed pedagogical study. For a marketing manager, a made-up consumer-survey finding. For a chemist, a synthesized-instrument reading. The exact artifact changes with the domain. The shape of the failure — *the load-bearing claim that rests on a source the literate user did not verify* — is invariant.

This chapter ends with the first piece of work you will keep. It is called the **Baseline Audit**, and it is the opening artifact of your portfolio.

**The Baseline Audit — Chapter 0 Portfolio Artifact (Layer B, diagnostic):**

Pick one piece of AI-assisted work you have produced in the last three months. A document, a report, a memo, a piece of code, an analysis, a teaching plan, a brief, an email thread — anything you used AI to help produce. Open it now.

Find the one most consequential single claim in it — the claim that, if false, would cost the most. The 78% figure. The recommendation. The dosage. The deadline. The named source. The conclusion the rest of the work depends on.

Trace that claim back. Where did it come from? Did you verify it at the time? Could you verify it now, without the AI's help? If you cannot — note that. If you can but did not — note that too.

Save the audit as `00-baseline-audit.md` in a new folder called `portfolio/` somewhere you can find it. Three sections, no more than half a page total:

1. *Piece audited.* What was the work, who was it for, when did it ship.
2. *Load-bearing claim.* The single most consequential element, named.
3. *Trace.* Whether it would survive a verification attempt today, and what specifically would need to be checked.

The Baseline Audit is paired with the **Final Audit** you will produce in Chapter 13 — the same piece of work, audited again, eighteen chapters later. The pair is the cleanest possible evidence of fluency: the same reader, the same artifact, two judgments separated by the book. If the Baseline and the Final read identically, the book did not teach. If they read differently — if you can now see in your own past work what you could not see today — the book did its job.

The portfolio is a living artifact. Open it now. We will be adding to it for the rest of the book.

---

### A note about AI

The chapter opens on a fabricated citation. The note's question is what makes that fabrication different from a human error of memory.

Where the model genuinely helps: explaining why hallucinated citations have the shape they do — author names that sound plausible, journal titles that approximate real ones, page numbers in plausible ranges. The pattern recognition is useful for spotting them in others' work.

Where the model does damage: producing the citation you needed but never had. The shape will be right. The substance will not exist. You will not catch it unless you check.

The rule: every citation from the model is unverified until you have opened the cited source in your own browser.

---

## LLM Exercise — Chapter 0: The Citation That Wasn't

**Project:** AI Fluency for [Your Role] — Your Domain Field Manual

**What you're building this chapter:** A **Role Dossier** you'll pin to your Claude Project for the rest of the book, and the **Baseline Audit** you just sketched above — drafted, structured, and saved.

**Tool:** Claude Project (set up "AI Fluency for [My Role]" — you'll return every chapter) + your file system (the `portfolio/` folder you just created).

---

**The Prompt:**

```
I am working through "Botspeak" by Nik Bear Brown and across the book I will
build a portfolio of AI-fluency artifacts in my own field. This is the
setup chapter — Chapter 0, The Citation That Wasn't. I need help with two
tasks.

TASK 1 — SPECIFY THE ROLE. The role should be:
- One I actually work in (or am about to enter)
- Specific enough to be useful — not "knowledge worker" but "junior associate
  at a regional law firm" or "growth marketer at an early-stage SaaS company"
  or "clinical pharmacist on a hospital night shift"
- Bounded enough that the failure modes are recognizable to anyone in the role
- Big enough that the playbook helps a real population

My context:
- Role / job title: [FILL IN]
- Industry / sector: [FILL IN]
- Career stage of the playbook's reader: [0–6 months / 6–18 months / 18–36 months / 5+ years]
- 2–3 task types I do most weekly: [LIST]
- Whether AI use is sanctioned, unsanctioned, or contested in my workplace: [FILL IN]

Push back if my role is too broad. Help me sharpen until the playbook would
be unmistakably for someone in this role and not someone in an adjacent one.

TASK 2 — DRAFT THE BASELINE AUDIT. Chapter 0 introduces the Baseline Audit
as the first portfolio artifact. I will redo it as a Final Audit in
Chapter 13. The pair is the book's before-and-after evidence of fluency.

Help me draft mine. The piece I am auditing:
- What it was: [FILL IN — document, report, memo, code, analysis, teaching plan, brief, etc.]
- Who it was for: [FILL IN]
- When it shipped: [FILL IN]
- How I used AI in producing it: [FILL IN — research, drafting, citations, code, structure, all of it]

The most consequential single claim in the piece:
- The claim itself: [FILL IN]
- Why it's load-bearing — what depends on it: [FILL IN]

Walk me through a trace of that claim. For each:
- Where did it come from in the AI session?
- Did I verify it at the time? How?
- Could I verify it now, without the AI's help? What would I check?
- What specifically would not survive a hostile re-read?

End with:
1. A one-paragraph "Role Dossier" I can pin to my Claude Project's system
   prompt so every future chapter exercise inherits the role context.
2. The Baseline Audit itself, formatted as the three sections in Botspeak
   Chapter 0: Piece audited / Load-bearing claim / Trace. No more than half
   a page total.

Save the Baseline Audit as `portfolio/00-baseline-audit.md`.
```

---

**What this produces:** A Role Dossier (pinned to the Project for every future exercise) and the Baseline Audit (saved to your portfolio folder). The first of seventeen artifacts. Twelve more to come.

**How to adapt this prompt:**

- *For your own project:* Fill in the bracketed fields. If you wear multiple hats, pick the role you'll keep growing in for the next two years.
- *For ChatGPT / Gemini:* Works as-is. Set up as a Custom GPT for persistence. Gemini's Drive integration handles the portfolio folder cleanly.
- *For Claude Code:* Not yet — this chapter is conceptual. Claude Code becomes useful starting Chapter 3 when you build the Specification Library.
- *For a Claude Project:* Recommended. The Role Dossier becomes part of the system prompt going forward.
- *For Cowork:* Recommended for managing the portfolio folder. Ask Cowork to create the folder structure: `portfolio/00-baseline-audit.md`, `portfolio/CLAUDE.md`, `portfolio/DESIGN.md`, `portfolio/PROJECT-template.md` (the last three are stubs you'll fill across the book).

**Connection to previous chapters:** None — this is Chapter 0. The Role Dossier and the Baseline Audit are the foundation every subsequent chapter exercise builds on.

**Preview of next chapter:** Chapter 1 takes a typical task in your role and walks the full Loop on it — your role's version of Priya's Tuesday at her best. The Worked Loop Log becomes the second piece in your portfolio.

---

## AI Wayback Machine

The ideas in this chapter didn't appear from nowhere. **Henriette Avram** was teaching computers to handle bibliographic references with structural integrity decades before most people had heard of "AI hallucinations." Here's a prompt to find out more — and then make it better.

![Henriette Avram, c. 1970s. AI-generated portrait based on a public domain photograph.](images/henriette-avram.jpg)
*Henriette Avram, c. 1970s. AI-generated portrait based on a public domain photograph (Wikimedia Commons).*

**Run this:**

```
Who was Henriette Avram, and how does her work on MARC (Machine-Readable
Cataloging) connect to the problem of fabricated citations from AI? Keep it
to three paragraphs. End with the single most surprising thing about her
career or ideas.
```

→ Search **"Henriette Avram"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain how MARC actually represents a citation, as if you've never thought about citation as a data structure
- Ask it to compare Avram's verification approach to how today's retrieval-augmented systems try (and fail) to ground citations
- Add a constraint: "Answer as if you're writing a footnote in a textbook about the Citation That Wasn't"

What changes? What gets better? What gets worse?
# Chapter 1 — The Loop and the Three Modes
*The machine predicts. You decide. Everything else is what you build between those two facts.*

---

I want to start with something that sounds simpler than it is.

When you give a prompt to a large language model, the model does not look up the answer. It does not reason through the problem the way you might, testing hypotheses and discarding wrong ones. It predicts — one word at a time, each word chosen because it is the most probable continuation of everything that came before it, given the patterns the model learned from reading an enormous amount of text.

That is the whole mechanism. Everything else follows from it.

The model can produce a fluent paragraph on a topic it was never explicitly taught because fluency is a pattern, and patterns generalize. The model can produce a citation that does not exist because the *shape* of a citation is a pattern — author, year, title, journal — and the model can fill in that shape with words that fit the pattern without ever having seen the specific source it is now generating. The model sounds confident because confident text is a pattern, and the model has seen a lot of confident text.

Confidence is a textual feature. It has no necessary relationship to correctness.

| What it looks like | What is actually happening |
|---|---|
| Fluent paragraph | Pattern continuation — the model produces coherent prose because fluency is a learned pattern, not evidence of understanding |
| Confident citation | Citation-shaped placeholder — author, year, title, journal filled in to match the pattern of a citation, not a real source |
| Round number | Statistically plausible filler — a number that fits the expected shape of a statistic in context, generated without any underlying data |

I want you to sit with that for a moment. Every failure mode we are going to spend this book on — the invented source, the plausible-sounding number that turns out to be wrong, the paragraph that is subtly off in a way you have to look up to catch — is a direct consequence of this one fact about how the system produces output at all. Not bugs. Direct consequences. The fluent practitioner does not encounter these failures occasionally; she works inside them constantly, and she knows what the failure shapes look like before they arrive.

That is the one technical fact I need you to carry. Now let me show you what running the Loop looks like in practice — well-executed, but not yet the eighteen-months-of-reflexes version that comes in Chapter 8.

---

It is 10:17 AM on a Thursday and Priya Banksy is opening her laptop in her publication's offices. Nine months have passed since the Tuesday in Chapter 0. The Pew correction is in the publication's archive; the practice has been changing in her hands since.

The Climate desk's morning meeting just ended. A federal grid-storage rule landed yesterday afternoon — three hundred pages of regulatory text, an industry press release calling it transformative, a smaller energy-justice group calling it inadequate, and a deadline of 1 PM for a thousand-word explainer on the publication's audience-facing site. The story is hers.

She does not open Claude. She opens a blank document.

For seven minutes she writes — not the piece, but about the piece. Who is going to read this? The publication's general audience on their morning commute, the policy people who already know what the rule says, the reporters at trade outlets who will write the in-depth versions tomorrow. What question does she actually need to answer in a thousand words? Not *what is the rule* — anyone can look that up. The question is *who is right about what it does* — the industry framing or the energy-justice framing, and on what evidence. What does she already know about FERC rulemaking in this segment, and what does she not? What sources will the editor trust on first read, and what will get kicked back as PR-laundering? At the bottom of the page, in two sentences, she writes the shape of the output: 950–1,050 words, structured as *what the rule does*, *what each side is claiming*, *what the rule actually changes for whom*, with three primary-source links and one named expert quote.

Then she opens Claude.

Her first prompt is 280 words long. It includes the audience, the task, the structure, the things to avoid, and an explicit instruction: *do not invent sources or named studies; if you do not know, say so.* The response comes back in seconds. It is competent. It contains three things she immediately wants to argue with — including a confident-sounding paragraph about "industry analysts" that does not name any. She does not edit and ship. She types a second prompt: *steelman the industry's claim that the rule will slow deployment, sourcing only from the actual rule text and the two trade-association comment letters in the docket.* The model produces a bear case sharper than her first instincts had given her — and points at one specific paragraph in the rule that she had skimmed past.

Over the next hour she cycles between the document and the chat window. Sometimes she hands the model a small, bounded task — *summarize what Section 219(b) of the rule actually changes about interconnection queue treatment* — and edits the response heavily. Sometimes she hands it a question — *what would a project developer doing 200-megawatt-scale storage care about in this rule that a 5-megawatt-scale developer would not* — uses the answer to refresh her own thinking, and writes the paragraph herself. Twice she catches a suspiciously round statistic in the model's output. The first one — *"approximately 40% of currently queued storage projects would be affected"* — has no source the model can name. She opens the FERC docket, finds the actual figure (37.2%, in a comment letter), and corrects it. The second — *"deployment delays of 18–24 months are typical at this stage of rulemaking"* — turns out to be a fabricated statistic shaped to look like industry analysis. She removes it entirely.

At 11:48 she has a draft she would not be embarrassed to publish. She does not publish it yet. She runs through, in her head, which parts she stands behind and which are still tentative. She writes a four-line note naming what the AI did and what she did: *outline scaffold drafted with Claude, rule-text summary section drafted with Claude (verified against the docket directly), all named studies and statistics verified independently with primary-source links, named-expert quote obtained by phone this morning, framing and conclusions are mine.* She saves the document. She sends it to her editor with that note at the top.

That is competent practice. Now let me tell you what actually happened.

---

Priya did five things, in roughly this order, none of them optional.

The first was specification. She specified the work before she opened the tool. The seven minutes at the blank document were not warm-up. They were the most important seven minutes of the morning. Most of what made her first prompt good was not in the prompt — it was in the thinking that preceded the prompt. The prompt was the residue of the thinking.

Watch what happens to someone who skips this. A practitioner who opens Claude and types *help me write an explainer on the new grid-storage rule* as their first move is not giving the model a task. They are asking the model to guess the task. The model will guess. It will produce something. The something will be reasonable-sounding and miss the point, not because the model is dumb but because there was no specification for the output to be good against. The failure is upstream of the model. The model is doing exactly what it should given what it was given, which was nothing.

The second was delegation. Priya did not ask Claude to do everything, and she did not ask it to do nothing. She made decisions — some deliberate, some by reflex — about which parts of the work to hand over and which to keep. The framing — *what question is this piece actually answering* — she did herself; the model would have produced something competent and bland. The rule-text summarization she handed over almost wholesale, because reading three hundred pages of regulatory text in the available time was not possible, and the model was good at this kind of synthesis (with verification). The contested framing — *who is right about what this rule actually does* — she sketched the structure of and asked the model to surface the strongest version of each side, with primary-source citations she would verify. Different parts of the work have different shapes, and the practitioner does not treat them the same.

The third was conversation. The first prompt did not produce the right output. The first prompt did not produce the right output *even though* the first prompt was 280 carefully chosen words. The first prompt rarely produces the right output. Priya did not, at any point, treat one round of input-and-response as the deliverable. She kept refining. She introduced an adversarial move — *steelman the industry's claim, sourcing only from the actual rule text and the comment letters* — that surfaced a counterargument she had not held strongly enough on her own. She used the model the way you use a colleague who is fast, well-read, and slightly too agreeable: by pushing back on it.

The fourth was discernment. When she got output, she did not assume it was good. She read it for what kind of error it might be. The suspiciously round 40% was not a sign the model was dumb. It was the shape of a placeholder — a number that fits the pattern of what a statistic should look like in this context, generated without any particular source. Priya has been learning to recognize that shape since Chapter 0's Pew survey. She is, nine months in, building up a library of the kinds of mistakes this kind of model makes, and she runs each output past that library before she ships anything. This step takes the longest to develop. It is also the step that, when missing, is hardest to fake.

The fifth was diligence. The four-line note to the editor is not bureaucratic disclosure. It is the practice of a person whose name is on the work. If the editor asks tomorrow how Priya got to the framing, she can show her. If a reader queries the 37.2% statistic, she can show which docket it came from. The work has a story. The story belongs to Priya.

Specify. Delegate. Converse. Discern. Be diligent. These five steps are what I am going to call the Loop.

*Figure 1.2*

---

The Loop is not a checklist you run once. It is a cycle, and the steps loop back on themselves. Halfway through conversation, you may discover your specification was wrong — you go back. Halfway through discernment, you may realize you delegated something you should have kept — you go back. The picture I want in your head is not five boxes with an arrow running left to right. It is five boxes with arrows running in every direction, including a thick return arrow from diligence back to specification, because when a recurring task changes shape, the whole cycle starts over. We will come back to those return arrows in Chapter 8, where Priya — eighteen months further into her practice — runs a Tuesday with two of them. For now: hold the cycle, not the line.

---

What Priya did is the easy case, and I want to be precise about why it was easy — because the precision matters for everything that follows.

It was easy because she was sitting at her keyboard while the model was running. Every output crossed her eyes before it went anywhere. Every error she could catch by looking. The model did not take any actions in the world; it produced text, and Priya decided what to do with the text. The Loop was running in its most forgiving configuration: the one where the human is always in the room.

There are two harder configurations, and the book is organized around them.

The first harder configuration is when Priya is not there at the moment of execution. She has set up a recurring AI-assisted task — a Monday-morning market-intel summary, a daily competitive-coverage scan, a weekly newsletter draft — and the model is running while she is in a meeting, or on a reporting trip, or asleep. The Loop does not go away. But the steps reweight. Specification now has to anticipate problems Priya will not be there to catch. Diligence has to be designed in advance, because there is no real-time human eye on the output. Discernment may not happen at all on a given day, because the volume of output exceeds what any human can verify item by item.

The failure mode here is slow and quiet. An error in a one-off deliverable is visible immediately. An error in a recurring automated process accumulates. By the time someone notices the weekly summary has been citing a source that does not exist, seventeen weeks have gone by, and the error has propagated into seventeen documents that other people used. The blast radius of a specification mistake is proportional to how many times the specification runs before someone catches the problem. I am going to call this mode Automation, and Part II is about it.

![Figure 1.3 — Timeline showing error accumulation in an automated process](images/01-the-loop-and-the-three-modes-fig-03.jpg)

The second harder configuration is when the model is taking actions in the world on Priya's behalf. Not producing text she reviews — sending emails, posting to social media, calling APIs, modifying files. The model now has hands. The blast radius of an error grows in ways text-only mistakes cannot grow, because some actions cannot be undone. Discernment now has to happen before the action, not after. Diligence now has to account for failure modes that are specific to autonomy: the model taking a locally reasonable action in a context it has misread, the model escalating in a way no one authorized, the model acting without a clear model of who the affected stakeholders are.

The Chapter 11 case — an automated headline generator that pushes a draft to the publication's social channels 47 minutes before any editor reviews — is this configuration's characteristic failure. The system had a goal, available tools, no stakeholder model, no sense of proportionality, and no pause between deciding and executing. Each of those absences is a direct consequence of deploying the easy configuration's assumptions into a situation where those assumptions no longer hold. I am going to call this mode Agency, and Part III is about it.

Three modes. Five Loop steps. The Loop has to run in each mode, and the steps reweight as the mode changes. Augmentation — Priya at the keyboard, Part I — is where most of a practitioner's day still happens, and it is the mode we treat first and at length. Automation and Agency are where the stakes get higher and the design discipline gets harder.

The table below fixes the relationships. Not because you need to memorize it, but because having the whole picture in one place before we spend twelve chapters inside the details is the right way to start.


| Mode | Human presence during execution | Steps that reweight | Characteristic failure mode | Where covered |
|---|---|---|---|---|
| **Augmentation** | Human is present at the keyboard; every output crosses human eyes before use. | Conversation and Discernment stay central because the human can refine, challenge, verify, and edit in real time. | Fluent but wrong output gets accepted because the user mistakes confidence for correctness. | Part I |
| **Automation** | Human is not present when the task runs; the system executes on a schedule or trigger. | Specification and Diligence become heavier because problems must be anticipated and review systems designed in advance. | Small errors accumulate quietly across repeated runs before anyone notices. | Part II |
| **Agency** | Human may not review each decision before action; the system can take actions in the world. | Discernment and Diligence must move before execution, with stronger boundaries, permissions, and escalation rules. | The system takes a locally reasonable but globally harmful action because it lacks context, stakeholder awareness, or proportionality. | Part III |

---

I want to say one more thing about the mechanism before we move on, because it bears directly on how to read everything that follows.

The model's confidence is a textual feature. I said this at the beginning and I want to close with it because the temptation to forget it is strong. The output is fluent. The output is well-organized. The output sounds like it knows what it is talking about. None of that is evidence of correctness. All of it is evidence of a model that has read a lot of fluent, well-organized, confident text and has learned to produce more of the same.

The fluent practitioner has internalized this so completely that she has stopped being surprised by it. When the model produces a round number, she does not think *this might be wrong.* She thinks *this is the shape of a placeholder.* When the model produces a confident paragraph on a contested topic, she does not think *I should double-check this.* She thinks *I know exactly what kind of error could be hiding here, and here is how I will find it if it is there.*

That shift — from *this might be wrong* to *I know what wrong looks like here* — is what separates fluent from literate. It does not come from a checklist. It comes from the accumulated experience of running the Loop many times and learning, case by case, what the failure shapes look like in the particular domains you work in. Priya, at month nine, is partway there. By Chapter 8 she will be most of the way. By the time she leaves for a different publication in Chapter 13, the shift is no longer effortful.

The chapters that follow are designed to accelerate that accumulation. Not to give you a set of rules you follow mechanically, but to give you the concepts that let you see what is happening when the Loop runs and when it breaks. By the time you finish Part I, the Loop should feel less like a process you are consulting and more like something you are doing without thinking about it — the way a good driver does not think about steering, but can still describe exactly what they are doing if you ask.

Chapter 2 maps the nine cognitive capacities the Loop actually uses. Some of them you already have at the level the work demands. Some you do not yet. The map you draw at the end of Chapter 2 — your Practitioner Profile — is the diagnostic that pairs with the 90-day plan you build at the end of the book.

---

### Translate before you move on — and produce the Worked Loop Log

Priya's task was a 90-minute daily explainer in journalism. In your field, what is the equivalent? A 90-minute task you do regularly. Not the smallest task in your week; not the largest. The middle-weight task that recurs and where the Loop's structure earns its keep.

For a clinician: a structured-note write-up after a clinic patient. For a software engineer: a code review on a pull request. For a marketing manager: a campaign brief for an internal stakeholder. For a teacher: a unit plan for the following week. For a research scientist: a methods section for a draft paper. For a lawyer: a research memo on a defined question. The exact task changes with the domain. The shape — *bounded, recurring, requires real judgment, takes about 90 minutes well-executed* — is invariant.

**The Worked Loop Log — Chapter 1 Portfolio Artifact (Layer B with A template, deliverable + log):**

Pick one such task in your work that you will run in the next week. Before you start, sketch the five-step Loop structure on a page — Specify / Delegate / Converse / Discern / Be Diligent — with two-line stubs under each. Then run the task. As you go, fill in what you actually did at each step, with time-stamps where you can.

Save the log as `portfolio/01-worked-loop-log.md`. Two pages, no more. Time-stamped. Specific. Five sections, one per Loop step, plus a one-paragraph retrospective at the end naming where the structure helped and where it felt like overhead.

The Worked Loop Log is the second piece in your portfolio. It is also the *first piece* of your eventual End-to-End Case Study in Chapter 8 — the keystone. Chapter 8 takes one sustained task through the full Loop with loop-backs. The Worked Loop Log is the smaller-scale version that proves you can run the steps cleanly on one bounded task before you scale up to the keystone.

There is one more artifact this chapter opens that you will accrete across the book: your **`CLAUDE.md`** — the personal coding/process constitution for how you work with AI in your field. Open it now. Write three things in it:

1. *What I will not improvise without explicit instruction.* (Example for journalism: I will not generate citations the model cannot ground in a specific public document.)
2. *What I always specify before opening the tool.* (Example: audience, structure, source rule, exclusions.)
3. *What I always do before shipping.* (Example: verify every named source against the primary document; remove any statistic the model cannot trace to a named dataset.)

Save as `portfolio/CLAUDE.md`. We will return to it in Chapter 3 (Specification), Chapter 4 (Delegation), and Chapter 6 (Discernment), adding more rules as the book gives you reasons to.

---

**What would change my mind.** If a working practitioner could be shown to produce fluent-level outcomes while reliably skipping one of the five Loop steps — if there is a stable productive workflow that genuinely does not need, say, Specification, or genuinely does not need Discernment — the framework needs revision. Every practitioner I have watched who skips a step produces work that fails in a predictable way at that step's locus. But "what I have watched" is not a controlled study, and I want to be honest about that.

**Still puzzling.** I do not have a clean answer to which Loop step is most often the bottleneck for a given practitioner, or how you would measure it. My intuition is that Specification is the most-skipped, Discernment is the most-faked, and Diligence is the most-deferred. I do not yet have data that separates those three claims.

---

## Exercises

### Warm-up

**1. Name the step.** Reread the Priya narrative. For each of the following moments, identify which Loop step is primarily operating and write one sentence explaining your reasoning. *(Tests: ability to recognize the five Loop steps in context.)*

- She opens a blank document and writes about the piece for seven minutes before opening Claude.
- She types a second prompt asking the model to steelman the industry's claim, sourcing only from the rule text and comment letters.
- She opens the FERC docket to check a suspiciously round 40% figure.
- She writes a four-line note to the editor describing what the AI did and what she did.

**2. The mechanism in plain language.** In two to three sentences, explain to a colleague who has never taken this course why a language model can produce a citation that does not exist. Do not use the word "hallucination." Do not say the model is "confused" or "wrong" — explain the actual mechanism. *(Tests: retention of the core technical fact about prediction vs. lookup.)*

**3. Modes at a glance.** For each scenario below, name the mode (Augmentation, Automation, or Agency) and identify the one Loop step most likely to fail if the practitioner treats it the same way they would in Augmentation mode. *(Tests: ability to distinguish the three modes and their reweighting logic.)*

- A marketing manager builds a prompt that generates a weekly social media report from a shared data sheet, scheduled to run every Monday morning without review.
- A developer deploys an AI assistant that can book calendar appointments on a user's behalf when asked.
- A researcher drafts a literature review section by section, reading each output before moving to the next.

---

### Application

**4. Diagnose the skip.** Here is a prompt sent to a language model: *"Write something about our Q3 results."* Which Loop step was skipped before this prompt was written? Rewrite the prompt to correct for the skip. Your rewritten prompt should be at least 80 words and must include: the intended audience, the task's purpose, the desired structure, and one explicit constraint on what the model should not do. *(Tests: ability to apply Specification in practice, not just recognize it in theory.)*

**5. Identify the failure shape.** A colleague hands you a model-generated paragraph that includes the sentence: *"According to a 2021 McKinsey survey, 73% of executives reported that AI integration had reduced operational costs by an average of 34%."* Describe in concrete terms what kind of error this might be, why the model would produce it whether or not the underlying data is real, and what verification step you would take before including it in a deliverable. *(Tests: application of Discernment — recognizing the placeholder-number failure shape.)*

**6. Reweight the Loop.** Priya's team wants to automate the daily morning explainer she currently writes manually. Write a brief specification (150–200 words) for the automated version. Your specification must address: what the model should produce, what sources it should and should not use, what a failure output looks like so a downstream reviewer can catch it, and how often a human should review a sample of outputs to catch systematic error. *(Tests: ability to adapt Specification and Diligence for Automation mode.)*

---

### Synthesis

**7. The blast radius argument.** The chapter claims that "the blast radius of a specification mistake is proportional to how many times the specification runs before someone catches the problem." Using this claim, construct a concrete argument — not abstract, with a specific hypothetical scenario — for why the diligence step in Automation mode must be designed before the automation runs, not added after a problem appears. Your argument should be 200–300 words. *(Tests: integration of Specification, Diligence, and the Automation mode.)*

**8. Loop vs. no Loop.** Describe a plausible scenario in which a practitioner skips the Conversation step and still produces a good deliverable. Then explain why this does not constitute evidence that the Conversation step is optional. Your answer should engage directly with the chapter's claim about what the first prompt "rarely" produces. *(Tests: ability to reason about the Loop's design rather than just its steps — and to distinguish a lucky outcome from a reliable process.)*

---

### Challenge

**9. Where the modes blur.** The chapter presents Augmentation, Automation, and Agency as three distinct modes. Describe a real or plausible workflow where the boundary between two of the three modes is genuinely unclear — where it is not obvious which mode's design discipline applies. What question would you ask to determine how to treat it? What would the answer tell you about how to weight the Loop steps? There is no single correct answer; the goal is a rigorous argument. *(Tests: ecosystem thinking — seeing the framework's edges and reasoning about them rather than applying it mechanically.)*

**10. The Feynman test.** The chapter ends with a claim about what separates fluent from literate: the shift from *this might be wrong* to *I know what wrong looks like here.* Explain this distinction to someone who has never read this chapter, using a domain they know well (cooking, carpentry, music, medicine — your choice). Your explanation should make the distinction feel concrete and earned, not abstract. Then: what would a practitioner have to do, specifically, to make that shift in a domain they are new to? *(Tests: depth of understanding of Discernment — and whether the student can teach the concept, not just recognize it.)*

---

### A note about AI

The three modes — manual, augmented, automated — are not abstractions. Each one names a specific relationship between you and the model, and each has its own failure pattern.

Where the model genuinely helps: surfacing which mode you are actually operating in, when you thought you were operating in another. The model can describe what you delegated and what you retained in a given workflow, and the description often surprises the operator.

Where the model does damage: deciding the mode for you. The choice of mode is a values choice — what risk are you willing to take that the model is wrong, and what cost are you paying for the speed of automation. The model has no stake in either.

The rule: the loop's mode is your call. The model can help you see which mode you are in. It cannot tell you which mode you should be in.

---

## LLM Exercise — Chapter 1: The Loop and the Three Modes

**Project:** AI Fluency for [Your Role] — Your Portfolio's Second Artifact

**What you're building this chapter:** Two pieces. (a) The **Worked Loop Log** — one real bounded task in your work taken through all five Loop steps, time-stamped, saved to `portfolio/01-worked-loop-log.md`. (b) The first three rules in your **`CLAUDE.md`** — your personal coding/process constitution, saved to `portfolio/CLAUDE.md`. Both are Layer A templates filled with Layer B (your domain's) content.

**Tool:** Claude Project (continue from Chapter 0; your Role Dossier is in context) + your file system (`portfolio/`).

---

**The Prompt:**

```
Continuing my AI Fluency portfolio. My Role Dossier from Chapter 0 and
my Baseline Audit are in the Project context.

Botspeak Chapter 1 watches Priya (a journalist nine months past her
Chapter 0 wake-up) run a 90-minute daily explainer task through all
five Loop steps — Specification, Delegation, Conversation, Discernment,
Diligence — competently but not yet at the eighteen-months-of-reflexes
mastery of Chapter 8. The chapter also names the three Modes
(Augmentation / Automation / Agency).

For Chapter 1's portfolio artifacts, do two things.

TASK 1 — DRAFT MY WORKED LOOP LOG.
Help me pick one bounded, recurring, ~90-minute task from my work and
draft the Worked Loop Log for it.

The task I will run:
- What it is: [FILL IN — e.g., "Friday client-update memo," "patient
  note after a clinic visit," "pull-request code review," "unit plan
  for next week," "methods section draft for a paper section"]
- How often I do it: [FILL IN]
- Who consumes the output: [FILL IN]
- Why it requires judgment (not just lookup): [FILL IN]

Walk me through the Worked Loop Log structure:
- Section 1 — SPECIFY. What I write before opening the tool. Audience,
  task, structure, source rule, exclusions. ~150 words.
- Section 2 — DELEGATE. What I hand to the model, what I keep, what
  I sketch and ask the model to fill. ~150 words.
- Section 3 — CONVERSE. The prompts I write and the adversarial moves
  I deploy. Show at least one steelman or edge-case probe. ~200 words.
- Section 4 — DISCERN. What I check, against what, looking for what
  kinds of errors. Name at least two failure shapes (the kind of
  placeholder number, the kind of citation that does not exist, etc.)
  ~150 words.
- Section 5 — BE DILIGENT. The AI Use Disclosure I attach, plus one
  note to my template/CLAUDE.md so I do not need to learn this twice.
  ~100 words.
- Retrospective — One paragraph. Where the structure helped. Where it
  felt like overhead. What changed for next time.

Time-stamp the sections. Be specific to my actual task, my actual
tools, my actual stakeholders. The log should be ~800–1,200 words
total. Save as `portfolio/01-worked-loop-log.md`.

TASK 2 — OPEN MY CLAUDE.md.
Help me draft the first three rules of my personal CLAUDE.md — my
coding/process constitution for AI work. Three sections:

1. WHAT I WILL NOT IMPROVISE WITHOUT EXPLICIT INSTRUCTION.
   2–4 rules specific to my field. (Examples for journalism:
   "I will not generate citations the model cannot ground in a
   specific public document." For a software engineer: "I will not
   commit code Claude generated without running it locally first.")

2. WHAT I ALWAYS SPECIFY BEFORE OPENING THE TOOL.
   The four or five elements I always include in a specification
   for my recurring task types. Audience, structure, source rule,
   exclusions, success criteria — your version.

3. WHAT I ALWAYS DO BEFORE SHIPPING.
   The verification or diligence moves I run on every consequential
   output before it leaves my desk.

Save as `portfolio/CLAUDE.md`. Note: this file is a LIVING document
— we will return to it in Chapter 3 (Specification), Chapter 4
(Delegation), and Chapter 6 (Discernment), adding rules as the book
gives me reasons to.
```

---

**What this produces:** Your portfolio's second and third artifacts — the Worked Loop Log (a real task taken through all five Loop steps) and the first version of your living `CLAUDE.md`. Both saved to `portfolio/`. Both will grow.

**How to adapt this prompt:**

- *For your own project:* Pick a task you will *actually run* this week. The Worked Loop Log written from a hypothetical task is structurally weaker than one written from a real one. The whole point is that the log is evidence, not aspiration.
- *For ChatGPT / Gemini:* Works as-is.
- *For Claude Code:* Useful for setting up the `portfolio/` folder structure cleanly.
- *For Cowork:* Recommended. Cowork can walk the portfolio folder and remind you what files exist.

**Connection to previous chapters:** Chapter 0 produced the Baseline Audit (one piece of past work, audited). Chapter 1 produces the Worked Loop Log (one piece of current work, run with the Loop visible) and opens the `CLAUDE.md`. The portfolio is now three artifacts deep.

**Preview of next chapter:** Chapter 2 produces the first half of your Practitioner Profile — the Nine Capacities self-assessment. The Profile pairs with the delegation map you build in Chapter 4 to become one combined diagnostic artifact.

---

## AI Wayback Machine
The ideas in this chapter didn't appear from nowhere. **W. Ross Ashby** was formalizing how a controller must match the variability of the system it controls decades before most people had heard of human-AI loops. Here's a prompt to find out more — and then make it better.

![W. Ross Ashby, c. 1948. AI-generated illustration based on a public domain photograph.](images/w-ross-ashby.jpg)
*W. Ross Ashby, c. 1948. AI-generated illustration based on a public domain photograph (Wikimedia Commons).*


**Run this:**

```
Who was W. Ross Ashby, and how does his Law of Requisite Variety connect
to a practitioner cycling through Augmentation, Automation, and Agency
on a single task? Keep it to three paragraphs. End with the single most
surprising thing about his career or ideas.
```

→ Search **"W. Ross Ashby"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain "requisite variety" in plain language, as if you've never heard of cybernetics
- Ask it to compare Ashby's idea of a controller to a fluent practitioner running the Loop on a Tier-C task
- Add a constraint: "Answer in the style of a museum placard at a cybernetics exhibit"

What changes? What gets better? What gets worse?
# Chapter 2 — The Nine Capacities
*The gap between two equally smart people isn't skill — it's a constellation you can learn to see.*

I have been watching people use AI tools for the last two years, and I keep noticing the same puzzle. Take two equally smart engineers, or two analysts, or two journalists, and watch them work with the same tool on the same kind of task. One of them gets dramatically better results than the other. The gap is not in their raw intelligence. It is not in their familiarity with the tool. It is not, usually, in how much they know about machine learning. The gap is somewhere else, and for a while I couldn't name where.

I want to show you what I mean through one case, because this is the kind of thing that is better seen than described. The case is Priya's — twelve months past her Chapter 0 wake-up, three weeks past the publication of a data-driven piece she had been particularly pleased with. The case happened to her. It is also the case that taught her she needed more than the Loop's structure. She needed the cognitive capacities the Loop draws on.

It is a Tuesday morning, and a letter has just landed in the publication's general inbox.

The piece Priya wrote three weeks ago was a state-by-state analysis of clean-energy policy timelines: how long, on average, did it take between a state's announcement of a major incentive program and the first publicly reported industry investment decision triggered by it. The story's framing was that some states acted fast and some did not, and the difference mattered for federal coordination. Priya had pulled the announcement dates and investment-decision dates from a state-by-state dataset, asked Claude to calculate the lag times in months, and reported the averages with state-level call-outs.

The letter is from a state energy analyst in one of the highlighted states. The analyst is polite and specific. The piece reports the state's lag time as 4 months. The analyst's office calculates it as 7 months. The difference is not noise. It is a category difference — the state's program was announced in a fiscal-year reference frame, and the publicly-reported investment decisions are dated in calendar time, and the conversion is non-trivial because the state's fiscal year begins in July. Claude's calculation had handled most states correctly. The states where fiscal year and calendar year diverged had been silently mishandled.

The piece is now in question. The error is in one state on a table with twelve states. Priya does not yet know how many other states it affected. The correction will go up tonight.

Now here is the question I want to sit with for a moment: what, exactly, did Priya do wrong?

Notice that it is not one thing. She did not fail at one cognitive task. She failed at several, and they are not the same kind of failure. I want to pull them apart, because the pulling-apart is the move this chapter is really about.

She failed, first, at deciding what to delegate. She handed the model the whole calculation — including the part that required someone to hold in mind a working model of the relationship between fiscal years and calendar years across state programs. She treated the model as a function that returns answers. She should have treated it as a draftsman that returns drafts.

She failed, second, at evaluating the output. She read the lag-time table, but she did not stress-test it. She did not ask, before publication: *what would have to be true for these numbers to be wrong?* That question is a different cognitive move from *do these look right?* The first asks you to imagine the world in which the calculation fails. The second asks whether the numbers match a vague mental picture of correctness. They feel similar from the inside. They are not. Priya made the second move when the situation required the first.

She failed, third, at handling uncertainty honestly. The model had not said, "I am ninety percent confident these calculations handle the fiscal-year edge cases correctly." Models do not say things like that. They produce confident-looking output, and you have to import the uncertainty yourself. Priya did not. The output looked certain, so she treated it as certain. The sleight of hand was the model's, but the cure was always going to be hers.

And she failed, fourth — this one is the subtle one, the slow one — at staying in the practice. Priya used to think carefully about fiscal-year conversions because she had to. As a junior reporter she had once spent half a day chasing down whether a budget figure was reported in fiscal or calendar terms. The model has, over the last year, taken that thinking out of her daily routine. Not out of her abilities; she can still do it when she tries. But out of her daily routine. And a muscle you stop using does not fail suddenly. It gets slow before it atrophies. You do not feel it getting slow. You feel it the day it fails to do what you needed, and by then the gap has been accumulating for months.

Four different failures, all at once, all in what looked like a simple table on a routine piece. Now let me tell you something interesting: if I told you a similar story about a clinician picking AI-generated drug-interaction summaries without specifying the patient's renal function, or a hiring manager running résumés through an AI tool he has not audited, or a graduate student handing in a literature review he did not read — you would find a different combination of similar failures each time. But you would always find a combination. Never just one.

That is what I have been trying to understand. People who use AI well are not doing one thing right. They are doing a constellation of things right, and the constellation has a shape.

I am going to claim the shape has nine points. The number is not sacred. I have looked at enough working practitioners that nine seems to fit the cases I have seen, but nine might be eight or eleven with more data. The count is bookkeeping. The capacities are what matter.

![Figure 2.1 — A "constellation" diagram with nine labeled nodes arranged in a loose organic cluster](images/02-the-nine-capacities-fig-01.jpg)

Here they are, briefly, before I give any of them the treatment they deserve.

The first is **strategic delegation**: deciding, before you begin, what the model should do and what you should do, and why. Priya's first failure. The diagnostic question is: *what should I give the AI, what should I keep, and why?* A fluent practitioner can answer this in seconds. A novice cannot answer it at all and so hands the model the whole task, which is the same as not deciding.

The second is **effective communication**: telling the model what it actually needs to know. Intent, constraints, audience, success criteria. When this fails, the model fills in the blanks with its best guess at what you meant. The best guess will be slightly different each time — which is how you get the experience of "the model is inconsistent," when in fact you have been inconsistent and the model has been faithfully reflecting your inconsistency back at you. I find this the funniest of the nine, because the failure looks like the model's failure and is in fact yours.

The third is **critical evaluation**: reading the output for what kind of error it might contain. This was Priya's second failure, and I think it is the most under-practiced of the nine. Most people read AI output for whether it *sounds* right. Reading it for whether it *is* right is a different activity. It requires you to hold, in your head, a model of the kinds of failure this kind of system produces. Without that internal model, you have nothing to check against except plausibility. Plausibility is a very low bar.

The fourth is **technical understanding**: knowing enough about how the system works to predict where it will fail. Not at research depth. Practitioner depth. Enough to know that a language model will hallucinate citations because of how it was trained, and so you should always check citations. Enough to know that an image model will produce six fingers because of the structure of its training data, and so you should always count fingers. The diagnostic question is: *do I have a working model of why this thing succeeds and fails?* This is the capacity I find most often missing in otherwise sophisticated users. They use the tool well in cases where it happens to work, and have no theory of when it will not.

The fifth is **ethical reasoning**: noticing when the use case has stakeholders other than yourself and the AI, and acting on that noticing. The hiring manager who deploys an unaudited screening tool has failed at this. So has any team that ships a product affecting other people's lives without asking who might be harmed. I want to be direct: this is not a soft skill. It is the capacity that keeps you from shipping something that gets someone hurt, gets you sued, or both.

The sixth is **stochastic reasoning**: handling uncertainty honestly. Yours, the model's, the world's. The diagnostic question is: *what kind of probabilistic claim is this, and what would calibrate my belief in it?* A model will give you a number — say, "sixty-five percent probability the Fed cuts rates" — and the number will look like a number, and you will use it as if it were a number, and it may be the model's best guess at last week's market-implied probability with no fresh information at all. The capacity is not "be good at probability." The capacity is "ask, every time, what kind of probabilistic claim is in front of me and where it came from."

The seventh is **learning by doing**: using AI in ways that amplify your skills rather than replace them. This was Priya's fourth failure, the slow one. The diagnostic question is: *am I building the skill, or consuming the output?* AI use can be the most powerful learning multiplier you have ever had. It can also be the fastest skill atrophier. Which one it is depends almost entirely on how you use it — not whether you use it. Most people who think they are using AI to learn are using it in a way that prevents learning. Most people who think AI is making them weaker simply have not found the specific moves that turn AI use into accelerated practice. These are learnable. The chapter that covers this will show you what they are.

The eighth is **rapid prototyping**: treating model output as a draft to be tested in the world, not as the work itself. The product manager who hands AI-generated feature ideas to engineering without any user testing has failed at this. The model produced options. The model did not produce validation. The diagnostic question is: *am I testing this against reality, or just against my own approval?* Approval is cheap. Reality is the only thing that talks back.

The ninth is **theoretical foundations**: keeping enough domain knowledge in your own head that the AI amplifies your understanding rather than substituting for it. The graduate student who hands in a literature review without reading the foundational papers has the prose without the foundation — which means she cannot tell good prose from prose with subtly wrong framing. The diagnostic question: *do I understand the underlying material well enough to judge whether this output is good?* Without that, you are not collaborating with the model. You are taking dictation from it.

| Capacity | Diagnostic question | Primary loop step | Durability |
|---|---|---|---|
| **Strategic Delegation** | What should I give the AI, what should I keep, and why? | Delegate | Durable |
| **Effective Communication** | Am I telling the model what it actually needs to know? | Specify | Temporary |
| **Critical Evaluation** | Would I bet on this output, and on what evidence? | Discern | Contested |
| **Technical Understanding** | Do I have a working model of why this system succeeds and fails? | Discern | Temporary |
| **Ethical Reasoning** | Who could be harmed by this output or deployment, and am I tracking that? | Be Diligent | Durable |
| **Stochastic Reasoning** | What kind of probabilistic claim is this, and what would calibrate my belief in it? | Discern | Contested |
| **Learning by Doing** | Am I building the skill, or consuming the output? | All steps | Durable |
| **Rapid Prototyping** | Am I testing this against reality, or just against my own approval? | Converse | Temporary |
| **Theoretical Foundations** | Do I understand the underlying material well enough to judge whether this output is good? | Discern | Temporary |

Nine. Each one a cognitive capacity. Each one a place where I have watched real practitioners fail. And — the part that took me longest to see — each one separable enough to practice on its own.

That last claim is the one I am least confident in, and I want to say so directly. It is possible that these nine correlate so strongly with general professional judgment that "develop the nine capacities" reduces, empirically, to "get better at your job." If that is true, the architecture in this book is decorative — it produces the right behavior, but the decomposition into nine is not doing real work. I have looked at this carefully and I believe the decomposition earns its keep. I can identify practitioners who are strong in some of these and weak in others, and the patterns are not random. But I do not have longitudinal data. If a careful study showed that fluent practitioners share four or five of these and the rest are noise, I would update. The list comes from observation, not theory. Observation can be wrong.

Now I want to say something about durability, because it matters for how you invest.

Some of these capacities are durably the human's responsibility, in any future I can foresee. Strategic delegation is one. Someone has to be accountable for the work, and accountability cannot be delegated to a model. Your name on the work is your name on the work, and the question of what to delegate is an accountability question, not a capability question. Ethical reasoning is the same. When the lawsuit is filed, when the patient is harmed, when the algorithm denies the loan, when the published statistic turns out to be wrong — the model is not the defendant. You are.

Learning by doing is durable in a different way: you have a body and the model does not, and the skills you have built into your daily practice are yours regardless of what the model can do at any given moment.

Critical evaluation and stochastic reasoning are contested. Models are getting better at calibrated self-doubt and uncertainty quantification. In some narrow domains, a well-tuned model may already produce better-calibrated probabilistic claims than a well-trained human. The practitioner of 2028 may have to update which parts of these she still owns and which she has reasonable grounds to lean on the model for. I cannot tell you yet which parts those will be. You will be able to tell, when the time comes, because the practice you have built will give you the sensors to notice.

The remaining four — effective communication, technical understanding, rapid prototyping, theoretical foundations — are temporarily irreducible at varying timelines. Models will erode parts of each. The judgment of what is a good prototype, what is a load-bearing theoretical foundation, what level of technical understanding is actually sufficient — that is going to remain yours longer than the production of those things.

![Figure 2.3 — Horizontal durability spectrum](images/02-the-nine-capacities-fig-03.jpg)

I am being explicit about this because I want the book to age well in your hands. The durable capacities, you are investing in for the whole career. The temporary ones, you still need now, and the book will try to teach them. When the timeline closes on any of them, you will be among the first to notice. That is one of the hidden returns on building a practice: the practice gives you the sensors to know when a capacity is no longer load-bearing. Someone who only read about these things will not have those sensors.

Let me end with something practical.

Take the nine capacities and ask yourself, for each one, where you are. Not precisely. On a four-level scale. *Untrained* means you have not knowingly practiced this and may not even know what it would feel like to practice it. *Aware* means you can name the capacity and recognize when it is at issue, but you do not yet have a routine for it. *Practicing* means you have a routine and you execute it imperfectly. *Fluent* means it is reflex — you do it without thinking, and you can teach it.

| Capacity | Untrained | Aware | Practicing | Fluent | Notes |
|---|:---:|:---:|:---:|:---:|---|
| **Strategic Delegation** | ☐ | ☐ | ☐ | ☐ |  |
| **Effective Communication** | ☐ | ☐ | ☐ | ☐ |  |
| **Critical Evaluation** | ☐ | ☐ | ☐ | ☐ |  |
| **Technical Understanding** | ☐ | ☐ | ☐ | ☐ |  |
| **Ethical Reasoning** | ☐ | ☐ | ☐ | ☐ |  |
| **Stochastic Reasoning** | ☐ | ☐ | ☐ | ☐ |  |
| **Learning by Doing** | ☐ | ☐ | ☐ | ☐ |  |
| **Rapid Prototyping** | ☐ | ☐ | ☐ | ☐ |  |
| **Theoretical Foundations** | ☐ | ☐ | ☐ | ☐ |  |

*Figure 2.4*

Don't agonize. Five minutes. Pick the level that is closer to true than the alternatives and move on.

When you have nine answers, look at them and pick the two capacities you most want to move up one level in the next ninety days. Not the ones you are already strongest in — that is comfortable and unproductive, and I have watched many smart people make exactly that mistake. Pick the ones that are slightly painful to look at honestly. Those are the ones where deliberate practice will buy you the most working capability in the next three months.

You are going to come back to these two at the end of the book — in Chapter 13's 90-Day Plan — and the comparison between what you said you would work on and what you actually improved at will teach you something about yourself that I cannot teach you here.

The Loop, which the previous chapter introduced, is the workflow. The nine capacities are what the workflow draws on. The Loop tells you what steps to take. The capacities are what makes those steps go well or badly. Hold both in your head as we go. The rest of the book develops them in parallel, and the chapters are designed so that you can read them in the order that matches the two capacities you just wrote down.

Priya, by the way, made her two picks the day the correction went up. She picked Critical Evaluation and Learning by Doing — the second and fourth of her four failures. The Strategic Delegation failure she could fix by writing a delegation map at the top of every data-heavy piece, and that habit was already forming. The Stochastic Reasoning failure was real but downstream of the other three: if she stopped treating confident model output as certain, the probability question took care of itself. The two she picked were the ones she could not fix by procedure. They required a different kind of attention, which is exactly what the 90-Day Plan is for.

---

### Translate before you move on — and start the Practitioner Profile

This chapter ends with the first half of a portfolio artifact you will complete in Chapter 4.

**The Practitioner Profile — Part 1 (Layer A template + Layer B content, diagnostic):**

Run the self-assessment. Mark a box for each of the nine capacities. Take five minutes. Don't agonize.

Then, below the table, name your two priority capacities — the two you most want to move up one level in the next ninety days — and write one sentence for each on *why*. Not "because I'm weak there" — that's not yet a reason. Something specific: a failure mode you recognize in your own work, a kind of task where you notice the gap, a senior practitioner whose strength you want to match.

Save as `portfolio/02-practitioner-profile.md`. This file is incomplete — Chapter 4 adds the Delegation Map as the second half. The combined Practitioner Profile becomes one consolidated diagnostic artifact in your portfolio. Future readers (a future employer, an admissions panel, your future self) read it to understand what kind of practitioner you are and where you are growing.

The Practitioner Profile is a Layer A diagnostic — the structure is the same for every reader — filled with Layer B content (your honest self-assessment in your domain). The honesty is what makes it credible. A profile that says you are *fluent* across all nine capacities is either lying or has not been worked through. A profile that names two specific gaps you are actively practicing against is the document a future reader respects.

---

*What would change my mind.* If a careful empirical study showed that fluent AI practitioners systematically share fewer than nine of these capacities — say, four or five appear together and the rest are decorative — the architecture needs revision. The list emerged from observation, not from theory. It is testable, and I would update if the test came back differently.

*Still puzzling.* I do not yet know whether the nine capacities are separable in practice. They may correlate so strongly with general professional judgment that "develop the nine capacities" reduces, empirically, to "develop professional judgment generally." I think they are separable enough to teach individually. I do not have the longitudinal data to be sure.

---

> **Going deeper — *Computational Skepticism for AI***
>
> Three of the Nine Capacities have full chapters of treatment in the advanced volume, useful when you decide one of them is the capacity you most need to develop:
>
> - **Stochastic Reasoning** — the deeper book starts from Bayes' theorem and base rates and shows why a "99% accurate" test can be useless on a rare event, and what calibration curves reveal that accuracy hides. See *Computational Skepticism for AI*, **Chapter 2 — Probability, Uncertainty, and the Confidence Illusion**.
>
> - **Critical Evaluation** — the deeper book gives you the four verification layers (fact, reasoning, framing, omission) and treats the *technically-accurate-practically-misleading* failure mode formally. See *Computational Skepticism for AI*, **Chapter 6 — Model Explainability**.
>
> - **Ethical Reasoning** — the deeper book proves that three reasonable definitions of fairness cannot all hold on the same dataset when base rates differ, and gives you the *defended-choice* deliverable that engineers in regulated industries are increasingly required to produce. See *Computational Skepticism for AI*, **Chapter 7 — Fairness Metrics**.

---

## Exercises

### Warm-Up

**1. Name the failure.** *(Capacity identification | Difficulty: low)*
Return to Priya's story. Four distinct failures are pulled apart in the opening movement. For each one, write a single sentence naming what Priya should have done differently at exactly that moment. Stay at the level of action, not theory — what is the specific move she skipped?

**2. Match the diagnostic question.** *(Capacity recall | Difficulty: low)*
Without looking back, write the diagnostic question for any five of the nine capacities. Then check. For each you missed or got wrong: what made it not stick? Rewrite it in your own words — one that you would actually ask yourself mid-task.

**3. Identify the missing specification.** *(Effective communication | Difficulty: low)*
A marketing associate prompts an LLM: "Write a tagline for our new product line." She gets ten options, picks one, and the client approves it. Six months later the tagline turns out to echo a competitor's decade-old slogan. List every piece of information she failed to give the model, in the order that omission became consequential. Then write the prompt she should have sent.

---

### Application

**4. Decompose a real task.** *(Strategic delegation | Difficulty: medium)*
Take a task you actually completed in the last week — with AI or without. Break it into its component subtasks. For each subtask, apply the strategic delegation diagnostic: *what should I give the AI, what should I keep, and why?* Write out your reasoning for at least three subtasks. Then ask: did you actually split the work this way? If not, what would have changed if you had?

**5. Import the uncertainty.** *(Stochastic reasoning | Difficulty: medium)*
A model returns this output in response to a business decision question: "Based on current trends, there is approximately a 70% chance that the new feature will increase retention." Write three questions you would ask — or three investigations you would run — before using that number in a decision. For each question, name the kind of uncertainty it is probing: the model's training data, the model's reasoning process, or the underlying variability of the world.

**6. Stress-test an output.** *(Critical evaluation | Difficulty: medium)*
Take any AI-generated text output you produced or received in the last month. Apply the question Priya failed to ask: *what would have to be true for this to be wrong?* Generate at least three specific failure scenarios. For each: how would you check whether that failure is present? What is the cheapest verification that would catch it?

**7. Classify the durability.** *(Technical understanding + theoretical foundations | Difficulty: medium)*
The chapter places critical evaluation and stochastic reasoning in the "contested" category — capacities where models may erode the human's role on a shorter timeline than the durable ones. Pick one of these two. Write a one-paragraph argument that the chapter has it wrong — that this capacity is actually durable, and a well-reasoned case can be made that humans will always need to own it. You do not have to believe the argument. Argue from evidence, not from instinct.

---

### Synthesis

**8. The hiring manager case.** *(Ethical reasoning + strategic delegation + critical evaluation | Difficulty: medium-high)*
A hiring manager screens 200 résumés for an engineering role by passing all of them through an AI tool that returns a ranked top 20. She does not audit the tool, does not examine how it was trained, and reviews no résumé outside the top 20. Identify every capacity she failed to exercise. For the two you consider most consequential: explain not just what she failed to do but what specific harm could result. Then describe the minimum practice — one action per capacity — that would have meaningfully reduced that risk without abandoning the tool.

**9. Design the atrophy test.** *(Learning by doing | Difficulty: high)*
The chapter describes a failure that is slow — a capacity that gets weak before it visibly fails. Priya had used to verify fiscal-year conversions when she was a junior reporter; the AI had taken that out of her routine without taking it out of her ability. Choose a professional skill from your own domain that you believe is in your daily practice right now. Describe, concretely, what early-warning signs would tell you that skill is being quietly eroded by AI use — before the first visible failure. Then design a specific practice routine, executable in under 20 minutes per week, that would keep the skill load-bearing regardless of how much AI you use alongside it.

---

### Challenge

**10. Audit the architecture.** *(All nine — critical stance | Difficulty: high)*
The chapter admits it does not have longitudinal data to confirm the nine-capacity decomposition is doing real work. Treat this as an invitation. Based on your own experience using AI tools professionally, make one of the following arguments in 400–600 words, supported by at least two concrete cases or observations:

- One of the nine capacities should be split into two distinct capacities (name the split and explain what separate failure it captures).
- Two of the nine should be merged (they reliably co-occur and cannot be meaningfully separated in practice).
- A tenth capacity is missing (name it, give its diagnostic question, describe the failure its absence causes).

You are not required to be right. You are required to argue from evidence rather than from theory alone.

---

### A note about AI

The nine capacities are a framework for what fluent practice looks like. The model can recite the framework. Reciting is not practicing.

Where the model genuinely helps: testing your understanding of each capacity against worked scenarios. Paste a workflow and ask the model which capacities it exercises and which it skips. The diagnosis is useful even when imperfect.

Where the model does damage: assessing whether you are personally fluent. The model has not seen you work. It can produce a confident self-assessment for you, which is the worst possible substitute for the actual self-assessment.

The rule: use the framework on your work; do not use the model to grade you on the framework.

---

## LLM Exercise — Chapter 2: The Nine Capacities

**Project:** AI Fluency for [Your Role] — Your Practitioner Profile

**What you're building this chapter:** Two pieces. (a) Nine domain-specific failure scenes — one per capacity — that anchor each capacity in your role's actual tasks. (b) The first half of your **Practitioner Profile** — the capacities self-assessment with two priority picks named honestly. Both saved to `portfolio/`. The Profile pairs with the Delegation Map from Chapter 4 to become one consolidated diagnostic artifact.

**Tool:** Claude Project (continue — your Role Dossier, Baseline Audit, Worked Loop Log, and CLAUDE.md are in context) + your file system (`portfolio/`).

---

**The Prompt:**

```
Continuing my AI Fluency portfolio. My Role Dossier from Chapter 0, my
Worked Loop Log from Chapter 1, and my opening CLAUDE.md are in the
Project context.

Botspeak Chapter 2 watches Priya — a journalist twelve months past
Chapter 0 — receive a Letters-to-the-Editor email about a state-by-state
lag-time table in a piece she wrote three weeks earlier. The model had
silently mishandled fiscal-year-to-calendar-year conversions for several
states. The chapter unpacks four distinct capacity failures from that
one error and uses the constellation to introduce the Nine Capacities
plus the four-level self-assessment (untrained / aware / practicing /
fluent).

For Chapter 2's portfolio artifacts, do two things.

TASK 1 — NINE FAILURE SCENES IN MY ROLE.
Write nine short failure scenes, one per Capacity, all set in my role.
Each scene 100–200 words. Each scene a different (named) person in a
different sub-context of the role. Each scene a clean instance of the
capacity's failure mode. Use real tools, real artifacts, real
stakeholders for my role.

The Nine Capacities and the chapter's diagnostic question for each:

1. STRATEGIC DELEGATION — what should I give the AI, what should I keep,
   and why?
2. EFFECTIVE COMMUNICATION — am I telling the model what it actually
   needs to know to do this well?
3. CRITICAL EVALUATION — would I bet on this output, and on what
   evidence?
4. TECHNICAL UNDERSTANDING — do I know enough about how this system
   works to recognize when it's failing?
5. ETHICAL REASONING — who could be harmed by this output or this
   deployment, and am I tracking that?
6. STOCHASTIC REASONING — what kind of probabilistic claim is this, and
   what would calibrate my belief in it?
7. LEARNING BY DOING — am I still building the skill, or just consuming
   the output?
8. RAPID PROTOTYPING — am I treating model output as the work, or as a
   draft I will pressure-test in the world?
9. THEORETICAL FOUNDATIONS — do I understand the underlying material
   well enough to judge whether this output is good?

Resist the temptation to make all nine scenes about the same task type.
Spread them across my role's sub-contexts so the scenes engage different
parts of the work.

Save the nine scenes as `portfolio/02-nine-scenes-in-my-role.md`. (This
is a supporting file in the portfolio — not the Practitioner Profile
itself, which comes next.)

TASK 2 — DRAFT MY PRACTITIONER PROFILE (PART 1).
Help me draft the first half of my Practitioner Profile. The Profile is
a Layer A diagnostic — the structure is standard — filled with Layer B
content (my honest self-assessment in my domain).

The Profile has three sections:

1. CAPACITIES SELF-ASSESSMENT. The nine-row table from Chapter 2,
   filled in honestly. For each capacity: my current level (untrained
   / aware / practicing / fluent) plus one specific note — a failure
   I recognize, a task type where I notice the gap, a senior practitioner
   whose strength I want to match.

2. TWO PRIORITY CAPACITIES. The two I most want to move up one level
   in the next 90 days. One sentence each on WHY — not "because I'm
   weak" but something specific. These two will become the 90-Day
   Plan in Chapter 13.

3. PLACEHOLDER FOR PART 2. A note that the second half of the
   Practitioner Profile (the Delegation Map) will be added in
   Chapter 4, after which the combined Profile becomes one consolidated
   diagnostic artifact in my portfolio.

Push back on me if my self-assessment looks too generous — a Profile
that rates fluent across the board is either lying or unworked.

Save as `portfolio/02-practitioner-profile.md`.
```

---

**What this produces:** Two additions to your portfolio. The nine scenes file (`portfolio/02-nine-scenes-in-my-role.md`) — a research artifact you can update as you encounter your own failures. The Practitioner Profile Part 1 (`portfolio/02-practitioner-profile.md`) — the first half of one of the portfolio's three diagnostic artifacts. ~2,500–4,000 words across the two.

**How to adapt this prompt:**

- *For your own project:* The nine scenes ARE the playbook's diagnostic instrument. Don't rush them. A reader who recognizes themselves in three of nine scenes is a reader the playbook has already earned.
- *For ChatGPT / Gemini:* Works as-is.
- *For Claude Code:* Not the right fit — this is narrative and self-reflection.
- *For Cowork:* Recommended. Cowork can manage the multi-file split (`02-nine-scenes-in-my-role.md` and `02-practitioner-profile.md`).

**Connection to previous chapters:** Chapter 0 produced the Baseline Audit, Chapter 1 produced the Worked Loop Log and opened the `CLAUDE.md`. Chapter 2 produces the first half of your Practitioner Profile (the capacities side). Chapter 4 produces the second half (the delegation side). Combined, they are one diagnostic artifact in the finished portfolio.

**Preview of next chapter:** Chapter 3 produces the Specification Library — 1–3 worked specifications for your most common task types, plus your `PROJECT.md` template. The Specification Library is the third piece of evidence in your portfolio's Layer B (the first being the Worked Loop Log, the third being the End-to-End Case Study in Chapter 8).

---

## AI Wayback Machine

The ideas in this chapter didn't appear from nowhere. **Lev Vygotsky** was working out how cognitive capacities form — that they live first in the joint activity between a learner, the world, and a tool, and only later become individual reflexes — decades before anyone worried about AI-mediated skill atrophy. The capacities in this chapter are not innate traits the reader either has or doesn't. They are made and unmade through the company a learner keeps with their tools. Here's a prompt to find out more — and then make it better.

![Lev Vygotsky, c. 1930. AI-generated portrait based on a public domain photograph (Wikimedia Commons).](images/lev-vygotsky.jpg)
*Lev Vygotsky, c. 1930. AI-generated portrait based on a public domain photograph.*

**Run this:**

```
Who was Lev Vygotsky, and how does his concept of the Zone of Proximal
Development connect to the idea that the Nine Capacities are built
through mediated practice with tools — including AI — rather than
learned in the abstract? Keep it to three paragraphs. End with the
single most surprising thing about his career or ideas.
```

→ Search **"Lev Vygotsky"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain "Zone of Proximal Development" in plain language, as if you've never taken a psychology course
- Ask it to compare Vygotsky's account of mediated tool use to the early-warning signs of a capacity going slack from AI use
- Add a constraint: "Answer as if you're writing a footnote in a chapter called The Nine Capacities"
# Chapter 3 — Specification
*Doing the Thinking the Model Cannot Do for You.*

It is 4:11 PM on a Wednesday and Priya Banksy is having her third bad iteration in a row with Claude.

Her editor has asked her to summarize a 62-page industry report — a clean-energy storage trade group's annual deployment outlook — for the next morning's editorial standup, where the desk will pick which two story angles to commission for the week. Priya is ten months past her Pew correction. She has the Loop down. She has been writing specifications. She thought she had this one. She uploads the PDF, types *summarize this report for tomorrow's editorial meeting*, and gets back a clean 600-word summary. It is fine. It is not what her editor wants. Her editor wants the parts the desk could turn into reporting angles, not a neutral summary. Priya types: *summarize this report for tomorrow's editorial meeting, focusing on the most reportable findings.* She gets another 600-word summary, slightly differently weighted, still not it. Her editor wants something that fits in five bullet points on a slide for the standup. Priya types: *summarize this report in five bullet points.* She gets five bullets, each three sentences long, and her editor wants each bullet to be one short clause readable from twenty feet away in a conference room.

By the third iteration Priya has spent forty minutes and produced something her editor will rewrite anyway. She closes the tab. She concludes, briefly, that Claude is not very good at this.

Claude is not good at this because Priya has not told Claude what *this* is.

This is the thing I want to understand with you, because it is not a prompting failure in any deep sense. It is a failure of *specification*, which is different from prompting, and which most people who pick up an AI tool never learn to do because nobody has named it separately.

The difference is this: a prompt is what you type. A specification is what you know before you type it.

Language models are, among other things, fluency machines. They are extraordinarily good at producing coherent, plausible-sounding output in whatever direction you point them. The catch is that if the direction is unclear, the fluency just makes the wrong output look convincing. You get something that reads well and misses the point, which is in some ways worse than something that obviously fails — at least the obvious failure tells you immediately to try again. When Priya got three different polished summaries that were each not quite right, the polish was making it harder to see the problem, not easier.

When people say "the AI didn't give me what I wanted," they usually mean one of two things. Either the model genuinely misunderstood a clear request — this happens, but less often than people think. Or they didn't yet know what they wanted with enough precision for anyone — model or human — to give it to them. The second failure is much more common, and much less visible, because the model's fluency produces output that looks like the problem was almost solved, which creates the impression of a near-miss rather than a specification failure.

The specification move is, in part, a diagnostic on yourself. That is exactly why it is hard.

---

Here is what a working specification contains. I am going to name five components, and the list is not glamorous. It is infrastructure — the kind of thing that sounds boring because it holds something up rather than being the thing held.

![Figure 3.1 — A five-part diagram](images/03-specification-fig-01.jpg)

The first is **intent**: not the immediate task, but the goal the task serves. Priya's intent was not *produce a summary*. Her intent was *give the editorial desk five reportable-angle bullets they can argue against tomorrow morning to pick the week's two stories.* Those are not the same thing, and the model had no way to know which one she meant. The intent statement is what tells the model — and you — what counts as success.

The second is **constraints**: what the output has to fit inside. Format constraints: five bullets, one clause each, no sub-bullets. Length constraints: under a hundred words total. Source constraints: only claims that appear in the report, not the model's outside knowledge. Audience constraints: the standup attendees, who have not read the document. Constraints are the parts of the specification the model would otherwise guess at — and guess wrong — while producing output that looks like it could be right.

The third is **success criteria**: how you will know, after the fact, that the output is good. *The editor uses it in the standup without rewriting* is a real success criterion. *Each bullet would survive a reporter asking "show me where in the report this comes from"* is a real success criterion. Without success criteria, every output looks plausibly fine, and you are left with a vague dissatisfaction you cannot diagnose.

The fourth is **exclusions**: what the model is not supposed to do. Do not invent sources. Do not pad bullets to make them feel substantive. Do not include the executive summary verbatim. Do not characterize the trade group's framing as if it were independent. This sounds like a strange thing to have to specify. But language models fill in blanks. If you leave a blank, they will fill it with their best guess at what looks complete. Exclusions are the specification saying: *please leave that blank blank.*

The fifth is **output format**: what the deliverable looks like structurally. Markdown or plain text. Bullet list or prose. Five items on their own lines or a flowing paragraph. This feels like a detail. It is not a detail. The format constrains the kind of thinking the model has to do, and a bullet list and a paragraph on the same intent will produce different content, not just different presentation.

Now watch what Priya would have sent if she had specified before prompting:

> **Intent:** Give the editorial desk five reportable-angle bullets they can argue against tomorrow morning to pick the week's two stories from the clean-energy-storage deployment outlook.
>
> **Constraints:** Five bullets total, one clause each, ≤15 words per bullet, source only the attached report, audience has not read the report, audience is reading the bullets off a slide from across a conference room.
>
> **Success criteria:** Editor uses them in the standup without rewriting; each bullet survives a reporter asking "show me where in the report"; the desk picks two stories from the five candidates.
>
> **Exclusions:** Do not editorialize beyond what the report supports. Do not pad. Do not include the executive summary verbatim. Do not present the trade group's framing as if independent.
>
> **Output format:** Five bullets, each on its own line, no sub-bullets, no preamble, no closing sentence.

| Prompt as sent | Component groping toward — but never stated | What the omission cost |
|---|---|---|
| *"Summarize this report for tomorrow's editorial meeting."* | Nothing. No component is present. | Model guessed the task. Produced a neutral 600-word summary — polished, directionless, unusable. |
| *"Summarize this report for tomorrow's editorial meeting, focusing on the most reportable findings."* | **Intent** — partially. Adds purpose-direction but the actual goal (slide artifact, story-selection standup, reportable-angle bullets) remains unstated. | Model reweighted the summary slightly. Still 600 words, still not slide-ready. The polish made the near-miss hard to name. |
| *"Summarize this report in five bullet points."* | **Output Format** — partially. Adds bullet structure but omits length per bullet, preamble rules, and hierarchy constraints. | Model produced five bullets, each three sentences long. Format was closer; content was still unfit for a slide read from across a conference room. |
| **Complete specification:** Intent (standup angle-selection slide) + Constraints (≤15 words per bullet, report only, unread audience, conference-room read) + Success Criteria (editor uses without rewriting; bullets survive reporter scrutiny; desk picks two stories) + Exclusions (no editorializing, no padding, no verbatim executive summary, no trade-group framing) + Output Format (five bullets, own lines, no sub-bullets, no preamble) | **All five components present.** | Editor uses it in the standup without rewriting. |

That is not a prompt. It is the thinking a prompt needs to encode. The actual prompt Priya types may be two or three sentences long — but those sentences will carry all five components because she now knows what they are.

---

I want to admit something about why this is hard, because the difficulty is not what most people expect.

Most people, when they first try to specify before prompting, discover that they do not fully know what they want. They thought they did. They sit down to write the intent statement and find they have not yet decided what the goal is. They sit down to write the success criteria and find they have none. They sit down to write the exclusions and realize they had been counting on the model to make those decisions for them — even though they would never have described it that way.

This is uncomfortable. It is also the specification doing its job.

Think about what happens in a well-run organization when someone delegates a task. The good editor does not walk up to a reporter and say *can you write something about the storage report?* and walk away. She says: *I need five slide-ready bullets from the trade group's storage outlook — one clause each, no longer than fifteen words, only claims that are in the document, by 8:30 tomorrow, because we are using them at the 9 AM standup to argue for the two stories we'll commission this week.* The reporter now has enough to do the work. The editor had to do that thinking before she opened her mouth.

Language models are not different. They are, in a certain mechanical sense, colleagues who have read a great deal and who will attempt in good faith to do what you ask. What they cannot do is want things on your behalf. They cannot supply the goal you forgot to specify. And because they are fluency machines, when the goal is missing, they will produce something that sounds like a goal was present — something plausible, coherent, and wrong in a way that is difficult to name.

The specification move forces you to do the thinking the delegation requires. This is why experienced practitioners produce better output not primarily because they know better phrases, but because they have learned to specify before they prompt. The specification is the work. The prompt is the document recording it.

---

Let me say something about templates, because this is where the specification stops being slow.

The five components feel like overhead the first time. They feel like overhead the fifth time. By the twentieth time you do the same kind of task, the overhead is gone — because you have a template.

A template is a specification you wrote once for a category of recurring work, with the variable parts marked, that you fill in rather than invent from scratch. Priya's report-summary-for-standup specification, captured as a template, becomes:

> **Intent:** Give [recipient] a [length/format] artifact for [specific purpose].
>
> **Constraints:** [format details], source: only [permitted sources], audience: [who reads it].
>
> **Success criteria:** [recipient action/test 1]; [recipient action/test 2]
>
> **Exclusions:** Do not editorialize. Do not pad. Do not include [common over-include item]. Do not [role-specific failure mode].
>
> **Output format:** [structural details, length, sections].

![A filled-in specification template card — Priya's clean-energy-storage-summary task with all five fields completed](images/03-specification-fig-03.png)
*A filled-in template card*

The next time Priya summarizes a long document for a high-stakes deliverable, she fills in the brackets. The thinking she did the first time is now infrastructure. The template does not do the thinking for her — she still has to know her intent, her constraints, her success criteria. But it reminds her to have them, and it gives her a form to put them in.

Build templates for the five tasks you do most often this quarter. Refine them as you discover what was missing. The fluent practitioner has a small library of templates and rarely starts a specification from scratch. The literate user invents the wheel every time, and every time runs into the same missing components she forgot last time.

This chapter is where your portfolio's **Specification Library** opens. You will fill it in by the end of the chapter.

---

There is a level of practice above templates, which is the use of *patterns*. A pattern is a compressed structure for part of the specification — a shorthand that the model handles especially well. I want to introduce one pattern here, not because it is magic, but because seeing one will help you understand what all patterns are.

The pattern is called **role-and-rubric**, and it has two pieces.

The role piece assigns the model a specific professional persona: not *act like a friendly assistant* but *act as a senior energy-policy researcher with a decade of grid-storage experience preparing one-page bullet summaries for a newsroom editorial standup.* The role compresses a great deal of constraint and tone into a single phrase the model can hold in mind while generating. The model does not have that experience in any meaningful sense. But it has read enough text produced by people in that role that the assignment shifts the statistical weight of its output toward what such a person would actually write.

The rubric piece supplies explicit criteria the output will be judged against: *each bullet must be defensible against a reporter asking "where in the report is this"; no claim that goes beyond what the report supports; tone declarative, not hedged; no language that mirrors the trade group's framing; total under a hundred words.* The rubric is the success criteria and exclusions components, made explicit in a form the model can self-check against.

| Specification component | How role-and-rubric handles it |
|---|---|
| **Intent** | Partially. The role assignment implies a purpose ("senior policy researcher preparing one-page summaries") but does not state the goal the task serves. Still needs an explicit statement of what success looks like for this specific output. |
| **Constraints** | Poorly. Role implies tone and register but says nothing about length, permitted sources, or audience. These must still be stated explicitly. |
| **Success Criteria** | Well — this is what the rubric does. Explicit, testable criteria ("each bullet must be defensible against a reporter asking 'where in the report is this'") are the rubric's native function. |
| **Exclusions** | Well — also rubric territory. "No claim that goes beyond what the report supports" is a clean exclusion the rubric encodes directly. |
| **Output Format** | Not addressed. Neither the role nor the rubric specifies markdown vs. plain text, bullet vs. prose, or structural details. Must still be stated separately. |

Role-and-rubric is one pattern. There are others — chain-of-thought, few-shot examples, constraint stacking. Each compresses different parts of the five components into a structure the model handles well. They are scaffolds for the same five components, not alternatives to them. The mistake I see most often is reaching for a pattern before specifying. Someone reads about chain-of-thought and starts adding *think step by step* to every prompt, regardless of whether step-by-step reasoning is what the task requires. Patterns serve the specification. The specification does not serve the pattern. If you do not yet know your intent, adding *think step by step* will give you a fluent, step-by-step, wrong answer.

---

I want to address something the chapter so far has left implicit.

When you force yourself to write down the intent, you will sometimes discover that you have not decided what success looks like. When you write down the constraints, you will sometimes discover that two of them are in tension — you want it short and you want it comprehensive, and you have not yet decided which one wins. When you write down the exclusions, you will sometimes discover that what you were actually planning to ask the model to do is make a judgment call you should be making yourself.

These discoveries are not a sign that specification is too much work. They are the specification doing its job, which is to surface the parts of the task you had not yet thought through. A language model is a fluency amplifier. Give it half-formed intent, and it produces fluent half-formed output. Give it well-formed intent, and it produces fluent well-formed output. The fluency amplifies whatever you brought. This is not a flaw in the technology. It is a property of all powerful delegation: the quality of the output is bounded by the quality of the brief.

Sometimes, even with discipline, you do not yet know what you want. You are at the beginning of a problem, feeling around its edges. This is fine. *Exploratory* is itself a specifiable intent: *surface three to five distinct framings of this question without committing to one; optimize for variety over polish; do not produce a finished artifact.* That is a specification for uncertainty. It tells the model you are not looking for a polished output you will feel committed to — you are looking for raw material you can think with. Specification under uncertainty is not a contradiction. It is honesty about what stage of work you are in. The mistake is skipping the specification because the task feels unclear, which usually produces polished output that answers a question you were not actually asking, which you then feel oddly obligated to accept.

---

There is a prior question this chapter has been deliberately avoiding: whether to pass the task to the model at all.

Some tasks should not be delegated. Some should be delegated in pieces, with strong human judgment at the joins. Some should never leave your hands entirely. The specification move is how you get good output when you have decided to delegate. The question of *whether* to delegate — and what it costs when you do — is what the next chapter takes up.

Specification gets you a well-formed task to hand off. Delegation asks whether you should hand it off in the first place, and if so, how much of it. Those are different questions, and the order matters. You cannot ask the delegation question well until you have specified the task clearly enough to see what the task actually is. Which is one more reason the specification move comes first.

---

### Translate before you move on — build your Specification Library and open your PROJECT.md

Priya's task was a summary-for-editorial-standup. In your field, what is the equivalent? Not one task — your five most common recurring task types. The pieces of work that recur often enough in your week that the specification's cost amortizes across many uses.

For a clinician: the structured-note write-up, the patient-handoff brief, the chart review summary, the referral letter, the literature-search brief for an unfamiliar case. For a software engineer: the pull-request summary, the design-doc draft, the post-mortem write-up, the architecture-decision record, the user-facing release note. For a marketing manager: the campaign brief, the competitive-positioning memo, the audience-segment summary, the launch-readiness note, the executive summary. The specific five vary with the role. The shape — recurring, AI-amenable, distinct enough to need different specifications — is invariant.

**The Specification Library — Chapter 3 Portfolio Artifact (Layer B, deliverable):**

Build it. Five templates, one per recurring task type. Each template covers all five components with bracketed variables for the parts that change per instance and pre-populated constants for the parts that don't. Each template includes 1–2 exclusions specific to your role's typical failure modes for that task type.

For each template, also write one fully filled-in worked example — a specific instance you could imagine on your desk this week. The worked example is half the value. The template alone leaves the reader (your future self, a colleague who picks up the library) staring at brackets.

Save the library as `portfolio/03-specification-library/` (a folder, not a single file — one file per template, plus a worked example for each). The library is a pure Layer B artifact: every line is your domain's content. A future employer reading it sees exactly how you specify the work that fills your week.

**Open your PROJECT.md template.** This chapter is also where you draft the structure of the `PROJECT.md` template you will instantiate for every significant piece of work in Layer B from here forward. The PROJECT.md template has two layers — intent (what the project means, who the work is for, what success looks like) and technical state (what is built, what is pending, what was generated and accepted versus rejected). Save as `portfolio/PROJECT-template.md`. The keystone End-to-End Case Study in Chapter 8 will be the first project that gets a fully populated `PROJECT.md` instantiated from this template.

**Update your CLAUDE.md.** Add the rule the chapter has been arguing for, in your own language: something close to *I do not open the tool until I have written the five components down, in some form, somewhere I can see them.* That rule is the operational core of everything else the book teaches. Make it explicit in your `CLAUDE.md` so it travels with you.

---

*What would change my mind on this chapter.* If careful empirical work showed that experienced practitioners produce equivalent-quality output from one-sentence prompts and from full five-component specifications — that the specification is decorative for people who have done it enough times that it lives in muscle memory — I would have to revise the claim that specification is the load-bearing skill. What I observe is the opposite: experienced practitioners specify more, not less, and the specification gets tighter, not looser, as the task gets harder. But the observation is informal, and I hold it accordingly.

*Still puzzling.* I do not yet have a clean answer to when the cost of full specification exceeds the cost of iteration. For very small tasks — reword this sentence, fix this heading — it almost certainly does. The break-even point is task-dependent, and I have not found a rule that generalizes cleanly.

---

> **Going deeper — *Computational Skepticism for AI***
>
> Specification, formalized at the level engineers use when they validate datasets and deployments, is called **reconstructing the epistemic frame**. The advanced book makes the point that every dataset and every prompt embeds a frame — what it claims to represent, what it actually represents, what it excludes — and that the most consequential failures live in assumptions the practitioner never wrote down: scope, sampling, definition, time, access. The five components in this chapter are the practitioner-grade version. The six-step epistemic-frame reconstruction in the advanced book is the engineering-grade version, with an explicit prediction-lock you do before you see any output, so the gap between expectation and observation can teach you.
>
> Reaching for the deeper version pays off when you specify automations (Chapter 10 of this book) or design AI deployments other people will rely on.
>
> See *Computational Skepticism for AI*, **Chapter 5 — Data Validation: Reconstructing the Epistemic Frame Behind a Dataset**.

---

### A note about AI

Specification is the capacity the model most rewards and most masks. A model will produce something for almost any prompt, which means underspecified prompts succeed often enough to mask the cost of underspecifying.

Where the model genuinely helps: rewriting your specification at three levels of precision and showing the resulting outputs side by side. The contrast makes the cost of vague specification visible in a way that abstract advice never does.

Where the model does damage: producing the specification for you. The specification has to encode what you actually want, which is a judgment the model cannot make.

The rule: practice specification by writing it. The model can show you the consequences of vague writing. It cannot do the writing for you.

---

## LLM Exercise — Chapter 3: Specification

**Project:** AI Fluency for [Your Role] — Your Specification Library

**What you're building this chapter:** Your portfolio's first Layer B deliverable folder — five specification templates, one per recurring task type in your role, each with a worked example. Plus the opening draft of your `PROJECT.md` template. Plus one new rule added to your `CLAUDE.md`.

**Tool:** Claude Project (continue — your Role Dossier, Worked Loop Log, Practitioner Profile Part 1, and CLAUDE.md are in context) + your file system (`portfolio/`).

---

**The Prompt:**

```
Continuing my AI Fluency portfolio. My Role Dossier, Worked Loop Log,
Practitioner Profile Part 1, and CLAUDE.md are in the Project context.

Botspeak Chapter 3 watches Priya — ten months past Chapter 0 — produce
three failed iterations on a single summarize-for-the-editorial-standup
task. The chapter introduces the five specification components: INTENT
(the goal the task serves), CONSTRAINTS (what the output must fit
inside), SUCCESS CRITERIA (how I'll know it's good), EXCLUSIONS (what
the model is NOT supposed to do), OUTPUT FORMAT (structural details).

For Chapter 3's portfolio artifacts, do three things.

TASK 1 — IDENTIFY THE FIVE MOST COMMON TASK TYPES IN MY ROLE.
Not nine, not three. Five. The task types should be:
- High-frequency (each appears multiple times per month for someone in
  my role)
- Distinct enough that they require different specifications
- AI-amenable (it's plausible to do them with AI assist)
- Spanning the role — not all the same kind of work

For each task type, name it precisely and give 2–3 examples of when
it occurs.

TASK 2 — A SPECIFICATION TEMPLATE PER TASK TYPE + A WORKED EXAMPLE.
For each of the five task types, produce a fillable specification
template covering all five components, with bracketed variables for
the parts that change per instance and pre-populated constants for
the parts that don't. Include 1–2 EXCLUSIONS specific to my role's
typical failure modes for this task type.

The template format I want:

TEMPLATE — [task type name]

Intent: Give [recipient] a [length/format] artifact for [specific purpose]
Constraints: [bracketed format details], source: [permitted sources], audience: [who reads it]
Success criteria: [recipient action/test 1]; [recipient action/test 2]
Exclusions: Do not [role-specific failure mode 1]. Do not [role-specific failure mode 2]. Do not [generic failure mode].
Output format: [structural details, length, sections]

Then, for each template, write one fully-filled-in worked example
showing what the template looks like populated for a specific instance
I could imagine on my desk this week. The worked example is half the
value — the template alone leaves the reader staring at brackets.

Save each template + worked example as a separate file under
`portfolio/03-specification-library/`. One file per task type.

TASK 3 — DRAFT MY PROJECT.md TEMPLATE.
Draft my personal PROJECT.md template — the Layer A scaffold I will
instantiate for every significant piece of work in Layer B of my
portfolio going forward. Two layers:

LAYER 1 — INTENT (what the project means, who the work is for, what
success looks like, the question the work is answering, where the
load-bearing judgment lives).

LAYER 2 — TECHNICAL STATE (what is built, what is pending, what was
generated by the model and accepted, what was rejected and why, what
verifications have been run, what was done by hand).

Save as `portfolio/PROJECT-template.md`. The keystone End-to-End Case
Study in Chapter 8 will instantiate this template for the first time.

TASK 4 — ADD ONE RULE TO MY CLAUDE.md.
Add the chapter's operational rule, in my own language. Something close
to: "I do not open the tool until I have written the five components
down, in some form, somewhere I can see them." Phrase it in a way that
fits my actual workflow.

Append the rule to my existing `portfolio/CLAUDE.md`.

End with one paragraph on the role-specific specification trap: what
is the failure mode that practitioners in my role most often produce
when they specify badly? What in my role tends to be most often left
unsaid? Save that paragraph at the top of the specification library
folder as `00-the-trap.md`.
```

---

**What this produces:** Your portfolio gains a folder (`portfolio/03-specification-library/`) containing five templates + five worked examples + the role's specification trap, plus a new file (`portfolio/PROJECT-template.md`) and an addition to `portfolio/CLAUDE.md`. The Specification Library is the first Layer B deliverable folder in your portfolio. ~3,000–5,000 words across the artifacts.

**How to adapt this prompt:**

- *For your own project:* The templates' value depends on the EXCLUSIONS section being honest about your role's typical failure modes. Be specific about what gets botched.
- *For ChatGPT / Gemini:* Works as-is.
- *For Claude Code:* Useful here if your role's tasks are code-heavy and the templates can live as structured prompt files in a repo. Otherwise, plain Markdown.
- *For Cowork:* Recommended. Cowork can manage the multi-file folder structure cleanly.

**Connection to previous chapters:** Chapter 2's nine scenes named where your capacities currently fail. Chapter 3 builds the operational antidote at the Specification step. The PROJECT.md template opened here will be instantiated for the first time in Chapter 8's keystone case study.

**Preview of next chapter:** Chapter 4 produces the second half of your Practitioner Profile — the Delegation Map. Combined with Chapter 2's capacities self-assessment, the Profile becomes one consolidated diagnostic artifact in your portfolio.

---

## Exercises

### Warm-Up

**1. Name and test the five components.** *(Component recall | Difficulty: low)*
Without looking back, name the five specification components. For each one, write a single sentence describing what goes wrong when that component is missing — not in theory, but in practice. What does the output look like? What does the failure feel like from the user's side?

**2. Diagnose a weak prompt.** *(Component identification | Difficulty: low)*
Take this prompt: *"Write an email to my team about the new meeting policy."* Identify which of the five components are present and which are absent. Then rewrite it as a full specification. Your specification should be specific enough that a model — or a competent human colleague — could produce the deliverable without asking a single clarifying question.

**3. Trace Priya's iterations.** *(Component sequencing | Difficulty: low)*
Return to Priya's three prompts. For each iteration — *summarize this report for tomorrow's editorial meeting*, then *focusing on the most reportable findings*, then *in five bullet points* — name the single specification component she added (or groped toward) with that iteration, and the components still missing at that point. Then name the one component whose absence caused the most damage across all three attempts.

---

### Application

**4. Write a full specification.** *(All five components | Difficulty: medium)*
You are a marketing analyst preparing a competitive summary for a product launch. Write a complete five-component specification for this task. It should be specific enough that a model — or a competent colleague — could produce the deliverable without asking a clarifying question. Then identify which component was hardest to write, and explain why.

**5. Find the internal conflict.** *(Constraint tension | Difficulty: medium)*
Below is a specification with a hidden conflict:

> **Intent:** Produce a thorough analysis of all relevant risks.
> **Constraints:** Two pages maximum.
> **Success criteria:** A senior executive can read it in under three minutes and feel fully informed.
> **Exclusions:** Do not omit anything material.
> **Output format:** Prose paragraphs, no headers.

Name the conflict. Explain what will happen if this specification is sent to a model without resolving it. Then rewrite the specification to resolve the tension — you will have to make a real decision about which constraint wins.

**6. Explain the pattern's limits.** *(Role-and-rubric | Difficulty: medium)*
Explain why role-and-rubric is not a substitute for the five-component specification. Which components does it compress well? Which does it leave unaddressed? Give a concrete example — a specific task and a specific role assignment — where using role-and-rubric without addressing the missing components would produce a plausible but wrong output.

**7. Defend the templates.** *(Templates as infrastructure | Difficulty: medium)*
A colleague argues: "Templates are just bureaucracy. Good practitioners know what they want intuitively and don't need to fill out a form." Construct the strongest version of this argument — make it as compelling as you can. Then explain why you agree or disagree, using the chapter's reasoning about where specification overhead actually goes and what it does when it lands there.

---

### Synthesis

**8. Build a template library.** *(Specification across domains | Difficulty: hard)*
You are building a template library for a legal research team. Their three most common tasks are: summarizing case law for a partner review memo, drafting initial client intake questions, and checking a contract clause against a regulatory standard. Write a specification template for each task. For each template, note which component was hardest to generalize across instances of that task type, and why.

**9. Connect specification to the diagnostic.** *(Specification + self-knowledge | Difficulty: hard)*
The chapter claims the specification move is "in part, a diagnostic on yourself." Connect this to the chapter's discussion of exploratory work. Under what conditions is the diagnostic uncomfortable in a productive way — meaning it surfaces something you needed to know? Under what conditions is it a signal that you should not be delegating this task at all? Where does the chapter leave this question open, and what would you need to know to close it?

---

### Challenge

**10. Solve the still-puzzling.** *(Open-ended | Difficulty: high)*
The chapter ends with a stated puzzle: "I do not yet have a clean answer to when the cost of full specification exceeds the cost of iteration." Propose a framework for answering this question. Your framework should account for at least four variables — task type, stakes, novelty, and practitioner experience level — and should make a falsifiable prediction: given a specific task description, your framework should tell you whether to specify fully or iterate. Then identify the weakest assumption in your framework and explain what evidence would cause you to revise it.

**11. Teach the five components.** *(Feynman test | Difficulty: high)*
Design a 45-minute session for a team of ten that teaches the five-component specification to people who have never heard the term. Your design should specify: the opening problem you would pose and why it is the right problem, the order in which you would introduce the five components and why that order, the single exercise you would run after the third component is introduced, and how you would close the session. For each design decision, cite the chapter's reasoning about why specification is hard to learn and where the difficulty actually lives.

---

## AI Wayback Machine
The ideas in this chapter didn't appear from nowhere. **W. Edwards Deming** was arguing that most failures are failures of the *system* — not the worker, not the tool — decades before anyone said "prompt engineering." His concept of the *operational definition* made the same claim this chapter does: you cannot measure quality, assign a task, or evaluate an outcome until you have defined, with enough precision that two people would reach the same conclusion, what you are actually asking for. A vague request is not a starting point. It is an instruction to guess. Here's a prompt to find out more — and then make it better.

![W. Edwards Deming, c. 1980s. AI-generated portrait based on a public domain photograph.](images/w-edwards-deming.jpg)
*W. Edwards Deming, c. 1980s. AI-generated portrait based on a public domain photograph (Wikimedia Commons).*

**Run this:**

```
Who is W. Edwards Deming, and how does his concept of the operational
definition connect to the idea that careful specification — not better
tools or smarter workers — is the main defense against failure? Keep
it to three paragraphs. End with the single most surprising thing about
his career or ideas.
```

→ Search **"W. Edwards Deming"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain the operational definition in plain language, as if you've never heard the phrase "operational definition"
- Ask it to compare Deming's fourteen points to the five-component specification template in this chapter — which points map cleanly, which don't
- Add a constraint: "Answer as if you're writing a memo to a manager who thinks quality problems are always the fault of the people doing the work"

What changes? What gets better? What gets worse?
# Chapter 4 — Delegation
*The tool doesn't take the skill from you. You hand it over voluntarily, in small increments, each of which makes complete sense in the moment.*

---

Here is a strange thing that happens with tools.

When you first get a good one, you use it for everything. A sharp knife, you cut bread with it, open packages with it, scrape the cutting board. A new phone, you use it to read, to navigate, to play music in the shower. The tool is interesting and the novelty makes you reach for it past the point where reaching makes sense. That is fine. That is how you learn what the tool actually does.

But then something subtler happens, and this is the part worth paying attention to. You stop doing some things by hand that you used to do by hand. Not because the tool does them better — though it often does — but because the tool is *there*, and using it feels like the obviously correct move, and doing it by hand starts to feel like a waste. The navigation app is open, so you follow it even on a route you have driven a hundred times. The synthesis tool is running, so you let it pull the sources even when you know this territory cold.

The tool does not take the skill from you. You hand it over voluntarily, in small increments, each of which makes complete sense in the moment.

---

There is a name for this in cognitive psychology: *cognitive offloading*. You move mental work from your head to a system outside your head. Scratch paper is cognitive offloading. A to-do list is cognitive offloading. A calculator is cognitive offloading. None of these are inherently bad — they extend what you can do, free working memory for harder problems, let you take on work that would otherwise exceed your capacity.

AI tools are cognitive offloading on a scale that is qualitatively different from anything before. A calculator offloads arithmetic. An AI research-synthesis tool offloads source-gathering, reading, pattern-recognition across dozens of documents, summarizing, and the initial structuring of an argument. That is not a bigger calculator. That is a different kind of thing. And so the question you have to ask — which nobody was asking about scratch paper — is this: *what capacity does this offloading build in me, and what does it erode?*

Some cognitive offloading *amplifies* you. You use the tool, and in the process of working with its output, your judgment gets more reps, not fewer. A senior journalist who delegates routine source-gathering to an AI tool but does her own pattern-recognition and synthesis is getting stronger, not weaker. She is doing more analysis at higher quality, and the analytical muscle is being exercised through the work.

Other cognitive offloading *atrophies* you. You hand off something that was, until now, teaching you. The output is fine. The work gets done. But the feedback loop that was building your skill is gone, and three months later you know less than you would have if you had kept doing it by hand — not because the AI failed, but because it succeeded too completely.

*Figure 4.1*

| | Amplifying offload | Atrophying offload |
|---|---|---|
| **What gets delegated** | Source-gathering, drafting, lower-judgment work | The same task — plus the evaluation that should have followed |
| **What the practitioner does with the output** | Reviews, pattern-matches, edits, decides | Accepts, ships, moves on |
| **Judgment muscle** | Keeps firing — more reps per unit time | Goes dormant — fewer reps, cooler signal |
| **Skill trajectory over months** | Grows: more analysis at higher quality | Erodes: three months later you know less than you would have working by hand |
| **Determining factor** | Practitioner's evaluative role survives the delegation | Practitioner's evaluative role does not survive |
| **Visible while it's happening?** | Yes — the work feels harder | No — each individual case looks correct |

The hard thing is that you cannot feel this happening. Each individual case looks correct. The synthesis tool ran, the output is good, you shipped it. That looks like efficiency. It *is* efficiency. And then six months later a source on the phone asks you about a regional procurement-rule update you did not catch, and you realize you stopped reading regional and trade press when the synthesis tool started doing it for you, and the synthesis tool sources from major outlets, not the regionals, and now you are on the phone with a state official knowing you are about to have to rewrite the piece you were going to send to the editor tomorrow.

---

Priya is fourteen months past Chapter 0. She has, with the help of an AI research-synthesis tool she has been using daily for six months, produced a 3,400-word draft on the rollout of a state-level clean-energy procurement program — the kind of piece that is going to anchor the publication's Tuesday feature slot. The draft is competent. It is, in fact, the best-organized work Priya has produced on this beat.

She is on a pre-publication call with a state energy official she has been cultivating for months — a source the publication has not landed before. They are walking through the piece's central argument. The official is friendly. The official asks, near the end of the call, "What's your read on the procurement-rule revision the commission put out last month?"

Priya does not know what he is talking about.

The official is referring to a small but consequential procurement-rule change — published in a state regulatory filing, covered by a regional weekly newspaper and one industry trade outlet, picked up by no major business publication — which, if implemented, will shift the cost-allocation rules in a way that materially changes who benefits from the state's program. The rule revision is six weeks old. Priya's synthesis tool, which sources from a curated list of major outlets, did not surface it. Priya, two years ago at her Indian publication, would have caught it. Two years ago she was reading fifteen trade and regional publications a week, talking to former classmates across the industry, stitching together threads the synthesis tools missed. Six months ago, as her US workload doubled, she stopped. The tool was faster, broader, and produced cleaner outputs. There was no reason — at the level she was thinking about it — to keep up the older habits.

Now there is a reason. The state official is waiting on the line.

This is what I mean by the *performance paradox*. Priya's daily output got faster and more polished. Her judgment in the moment — the muscle she had been building for years, and that the senior writers on her desk have, and that her sources trust her to bring — atrophied without her noticing. Each individual case looked correct. The total picture was quietly getting worse.

The paradox is not unique to AI. Pilots who fly on autopilot for every flight produce aviators who are excellent at managing the autopilot and have degraded manual flying skills — which is the skill they need precisely on the day the autopilot fails. Radiologists who use AI screening tools for every routine case produce, on the rare complex case, slower and worse calls than the colleague who never adopted the tool. The phenomenon is general. AI has accelerated it because AI offloads a wider range of cognitive work than any tool that came before.

The question, then, is not whether offloading erodes skill. It does. The question is which skills erode and whether those are skills you can afford to lose.

Here is a heuristic I find useful. Before any delegation, ask yourself: *if I hand this task to an AI for six months, what skill of mine will weaken, and is that skill one I will need exactly on the day the AI fails?*

If the answer is "a skill I won't miss" — delegate freely and don't look back. Reformatting data. Converting file formats. Spell-checking. These tasks do not build judgment you would ever miss.

If the answer is "a skill I'll need precisely when something goes wrong" — then you have a choice to make consciously. You can still delegate. But you need to build the practice in by other means. The surgeon who uses robotic tools still practices on the simulator. The navigator who relies on GPS still runs chart exercises. You keep the skill alive artificially, because the natural opportunity to practice has been removed by the tool.

Priya, after that call, did not stop using the synthesis tool. She did add a Friday-morning hour to her calendar, one she now defends against everything: thirty minutes reading regional and trade press in her beat, thirty minutes catching up on what one specific cohort of former classmates has been writing in their own newsletters and trade columns. It is not a complete replacement for what she lost. It is enough to keep the smell. The piece would have shipped wrong without it. Now it will not.

---

Let me be more precise about this, because the intuition about "mechanical versus judgment" can mislead you if you don't push on it.

There is a spectrum. At one end: tasks where the right answer is fully determined, the model will get it right reliably, and doing it yourself would not teach you anything you don't already know. These are genuinely mechanical. Delegate them.

Move along the spectrum and you reach tasks where the right answer is well-defined but *recognizing wrong answers* requires domain knowledge you have. The model generates a draft; you check it. The model suggests category labels; you verify them. Here the skill you are practicing is the check — the evaluative judgment that distinguishes correct from close-but-wrong. That skill is worth keeping. Delegate the generation; keep the evaluation.

A little further and you are in synthesis territory. The model gathers and combines information from multiple sources and produces a unified output. Two risks live here that don't live at the mechanical end. First, the sources may contain errors the model won't catch because it doesn't know what you know about this specific subject, this specific moment, these specific operating conditions. Second — and this is the procurement-rule problem — *the omissions are often where the insight lives*. A synthesis tool tells you what the sources say. It cannot tell you what the sources don't say. The practitioner who knows the domain can smell the absence. The practitioner who has been delegating synthesis for six months has lost that smell.

Go further and you reach contestable analysis: problems where reasonable practitioners would genuinely disagree about the answer. Strategic recommendations. Investment theses on non-consensus positions. Editorial calls on whether a story is a story. Models produce confident output here with no reliable signal about where the confidence is warranted and where it is guesswork dressed as synthesis. A model asked "should this story run" will not answer "I don't know." It will reason its way to a position. The position may be excellent or terrible, and the model cannot tell the difference. You have to. Which means you have to keep the analytical work here even if you use the model to assemble components of it.

At the far end: decisions where, if they go wrong, a human has to answer for them. Hiring. Firing. Safety decisions. Care decisions. Publication calls on contested or sensitive material. The accountability here is whole and cannot be distributed. You can use the model to inform the decision. The decision belongs to you.

You can think of these as tiers — not because the world divides cleanly, it doesn't, but because having a name for each region helps you locate yourself when you are deciding what to hand off.

Tier one is mechanical execution: fully determined, model reliably correct, no judgment being built by doing it yourself. Delegate freely.

Tier two is pattern-matching with feedback: right answer is defined, but you need to check. Keep the check.

Tier three is synthesis from sources: model gathers and combines, you evaluate. The danger is the procurement-rule trap — stay alert to what the synthesis is not telling you, not just what it is.

Tier four is drafting in your voice: the model produces, you revise. The real risk here is long-term voice drift — your writing migrates toward the model's defaults over months. Keep some work done without the model, just to keep your own register alive.

Tier five is judgment under structure: you author the framework, the model applies it. Delegate the application; keep the authorship.

Tier six is contestable analysis. Don't delegate the call. You can delegate the inputs.

Tier seven is accountable judgment. The model can inform it. You own it entirely.

| Tier | Name | One-line delegation rule | Atrophy risk |
|---|---|---|---|
| **1** | Mechanical Execution | Delegate freely — right answer is fully determined and doing it yourself builds nothing. | None |
| **2** | Pattern-Matching with Feedback | Delegate the generation; keep the evaluation — the check is the skill worth maintaining. | Low |
| **3** | Synthesis from Sources | Delegate the gathering and combining; stay alert to what the synthesis is not telling you. | Medium |
| **4** | Drafting in Your Voice | Delegate the draft; keep some work done without the model to prevent long-term voice drift. | Medium |
| **5** | Judgment Under Structure | Delegate the application of the framework; keep the authorship of the framework itself. | Medium |
| **6** | Contestable Analysis | Do not delegate the call; you may delegate components that feed into it. | High |
| **7** | Accountable Judgment | The model can inform it; you own it entirely — accountability cannot be distributed. | High |


A delegation map for any non-trivial task is: decompose it, locate each component on the tiers, hand over the bottom, partner on the middle, keep the top. The map is something you can defend. It is the artifact that proves you thought about what you were doing.

---

In practice, four questions get you to the map quickly. You can run them in two minutes before any consequential delegation.

*What capacity does this task build, and do I need to keep building it?* This is Priya's question, asked in advance. If the task has been building one of your skills, delegating it stops the building. That might be fine. It might not. Decide consciously.

*What is the blast radius if the AI gets this wrong?* A misformatted table is one blast radius. An error in a strategic recommendation is another. A wrong medical call is a third. A misattributed quote in a piece that goes to 280,000 followers is a fourth. Match your verification effort to the blast radius. At high blast radius, the verification is more important than the generation.

![Figure 4.3 — 2x2 matrix — x-axis: blast radius (Low to High), y-axis: verification effort required (Low to High)](images/04-delegation-fig-03.png)

*Who is accountable if this is wrong, and does that person know how it was produced?* If your name is on the work, your accountability is on the work. The threshold for disclosure is lower than most practitioners currently assume. If a stakeholder would feel deceived to learn the work was AI-assisted, that is information you need to act on before the work ships, not after.

*What does the model not know that I do, and have I made sure that part stays in?* The model has broad reading and no domain intuition specific to this beat, this moment, these relationships. If you are not actively folding in what you know that the model cannot, the output will be polished and missing the thing a senior practitioner would catch. The procurement-rule revision is always somewhere in the analysis.

Four questions. Run them. After you have run them a few hundred times, they will be reflex — and you will have them before you open the tool rather than after you have already shipped.

---

Here is something true about the fluent practitioner that is easy to underestimate. She is not faster than the literate user because she uses the tool more aggressively. She is faster *and more reliable* because she knows exactly which parts of the work she is handing off and which parts she is keeping — and she has kept alive the judgment that makes the output trustworthy.

The literate user thinks about the tool. The fluent practitioner thinks about the work. The tool is somewhere in the background, doing the parts the tool should do, while the practitioner is doing the parts that are actually hard and actually hers.

Priya got faster. Her work looked better. The 3,400-word draft was the best-organized piece she had produced on a tight timeline. And on the phone with the state official, what she learned was that best-organized is not the same as right, and that the journalist she was becoming before the synthesis tool is not the same as the journalist she was becoming with it. The Friday-morning hour is how she gets some of the old practice back without giving up the new tool.

The lesson is not to use the tool less. The lesson is to use it with clear eyes about what the bargain is.

Chapter 5 is about the next step: even with a clean specification and a deliberate delegation map, the first prompt rarely produces what you need. The gap between what you asked for and what you actually need is closed by conversation — and the four adversarial moves that distinguish a fluent practitioner's iterative refinement from a literate user's one-shot hope.

---

### Translate before you move on — build the Delegation Map, complete the Practitioner Profile

Priya's case was about journalism beat-reading atrophying under synthesis-tool use. In your field, what is the equivalent? Six months from now, what skill of yours will be quietly slipping if you delegate your current daily-AI-task pattern without thinking?

For a clinician: clinical pattern recognition across atypical presentations, when the chart-summarization tool collapses every case to its three most-common features. For a software engineer: debugging intuition across the parts of the system the AI rarely touches. For a marketing manager: the qualitative read of campaign feedback that the segmentation tool aggregates away. For a teacher: the ability to read student writing for the specific student behind the prose, when the grading tool flags only the surface. For a research scientist: the read on which result is the unexpected one worth chasing, when the analysis tool surfaces only the planned-for findings. The atrophying skill is field-specific. The pattern — *the skill that is being quietly delegated is the skill you will need the day the tool fails* — is invariant.

**The Practitioner Profile — Part 2 (Delegation Map) (Layer A template + Layer B content, diagnostic / framework):**

This chapter completes the Practitioner Profile artifact you opened in Chapter 2.

Build your personal delegation map. List the recurring AI-assisted tasks in your work — five to ten of them, not exhaustive. For each, locate it on the seven tiers. For each, run the four delegation questions. For each, note whether the delegation is currently amplifying you or atrophying you, and what the early-warning sign of atrophy would look like specifically in your work.

Then name the one skill in your role most at risk of quiet atrophy from your current delegation pattern, and one concrete practice — under thirty minutes a week — that would keep it alive.

Append to `portfolio/02-practitioner-profile.md` as a new section, "Delegation Map." The Practitioner Profile is now complete: half capacities self-assessment, half delegation map. It is one consolidated diagnostic artifact in your portfolio. A future reader — an employer, an admissions panel, you in six months — picks it up and learns what kind of practitioner you are and where you are practicing against your gaps.

**Update your CLAUDE.md.** Add the rule the chapter has been arguing for, in your own language: something close to *Before any consequential delegation, I run the four delegation questions. The skill that is silently being delegated is the skill I will need the day the tool fails.* That sentence is the chapter compressed to a working rule. Make it explicit so it travels.

---

**What would change my mind.** If longitudinal evidence showed that aggressive delegation at the contestable-analysis tier does not degrade practitioner judgment over time — that the model catches what the practitioner would have caught, and sometimes more — the keep-the-skill argument here is weaker. The radiologist evidence, and the pattern behind Priya's procurement-rule story, suggests otherwise. I would update on counter-evidence.

**Still puzzling.** I do not have a sharp answer to how long atrophy takes for a given skill. Six months was clearly enough in Priya's case. Some skills probably go faster; some take years. That time-constant matters enormously for how carefully you need to manage the practice-by-other-means requirement, and it is not yet well-characterized empirically.

---

## Exercises

### Warm-up

**1. Tier identification.** For each task below, name the delegation tier and write one sentence explaining your reasoning. *(Tests: ability to locate tasks on the seven-tier framework.)*

- An analyst asks an AI to reformat a data table from wide to long format for a statistical analysis.
- A consultant asks an AI to synthesize analyst reports on a target company's competitive position ahead of a client meeting.
- A hiring manager asks an AI to recommend which of three finalists to hire based on interview notes.
- A writer asks an AI to generate a first draft of a strategy memo, which she then revises heavily.

**2. The paradox in plain language.** Explain the performance paradox — in two to three sentences, without using the word "paradox" — to a colleague who is proud that her team's output quality has measurably improved since adopting AI tools six months ago. Your explanation should not be dismissive of the improvement. It should name what is true about the improvement and what might also be true alongside it. *(Tests: retention of the performance paradox concept and ability to hold both sides of it.)*

**3. The four questions, applied.** A research associate is about to delegate the following task: *summarize the last twelve months of earnings calls for three public competitors and identify recurring themes in management's forward guidance.* Run the four pre-delegation questions on this task. For each question, write two to three sentences — not just the question restated, but your actual answer for this specific task. *(Tests: mechanical application of the four-question framework before it becomes reflex.)*

---

### Application

**4. Build a delegation map.** A strategy consultant is preparing a market-entry recommendation for a client considering expansion into Southeast Asia. The work involves: gathering macro data on five target markets, synthesizing analyst and trade-press coverage, identifying regulatory barriers, structuring the recommendation framework, drafting the written analysis, and making the final go/no-go call for the presentation. Decompose this work into its components, locate each on the seven tiers, and produce a delegation map specifying what gets handed to the AI, what gets partnered, and what the consultant keeps. Defend each call in one sentence. *(Tests: ability to apply tier logic to a multi-component real task.)*

**5. Diagnose the atrophy.** Priya's failure was not visible in her daily output — it appeared only when a state source asked a question the synthesis tool had no reason to surface. Describe a plausible scenario in a different domain (medicine, law, engineering, software, design — your choice) where the same structure plays out: a practitioner whose output quality improved after adopting an AI tool, but whose judgment degraded in a way that only became visible under a specific condition. Name the skill that atrophied, the condition that revealed it, and what the practitioner would have needed to do differently to prevent it. *(Tests: ability to generalize the Priya pattern beyond the case as given.)*

**6. The blast radius check.** You are reviewing a colleague's delegation decision before a deliverable ships. The colleague delegated the following to an AI and did not verify the output: a one-paragraph summary of a regulatory approval timeline for a pharmaceutical product, included in a board memo. Using the blast-radius question, explain specifically what the verification step should have been, what failure modes it would have caught, and what the consequence of skipping it could be. *(Tests: application of the blast-radius heuristic to a concrete high-stakes case.)*

---

### Synthesis

**7. Amplify vs. atrophy.** The chapter distinguishes cognitive offloading that amplifies you from cognitive offloading that atrophies you. Using the seven-tier framework, identify the structural feature that separates the two categories — what is it about the nature of a task that determines whether delegating it builds you or diminishes you? Your answer should be a clear, defensible claim in 150–200 words, not a restatement of the tiers. *(Tests: ability to extract the underlying principle from the framework rather than just apply it.)*

**8. The voice drift problem.** Tier four introduces voice drift as a distinct risk for practitioners who delegate drafting consistently. Explain why voice drift is a problem that does not appear in the other tiers — what is different about drafting in your voice, as opposed to synthesis or pattern-matching, that makes the atrophy risk specifically linguistic rather than analytical? Then propose a concrete practice — something a practitioner could do weekly in thirty minutes or less — that would keep the risk manageable without abandoning delegation. *(Tests: integration of the cognitive offloading argument with the specific character of Tier 4.)*

---

### Challenge

**9. The accountability edge case.** The chapter says accountable judgment "cannot be distributed" and the decision belongs to you entirely. But consider a practitioner who uses an AI to surface options, model scenarios, and pressure-test assumptions before making a hiring decision — then makes the call herself. Has she kept the accountability whole, or has she partially distributed it? Construct the strongest argument for each position, then say which you find more convincing and why. There is no clean answer; the goal is a rigorous argument that takes both sides seriously. *(Tests: ability to reason at the edges of the framework where it does not yield a clean answer.)*

**10. Design the counter-practice.** The chapter notes that practitioners who delegate skills they will need when the AI fails must "keep the skill alive artificially, because the natural opportunity to practice it has been removed by the tool." Priya's Friday-morning hour is one example. Choose a specific domain and a specific skill that AI tools are now commonly used to offload in that domain. Design a concrete counter-practice — structured, realistic, requiring no more than two hours per month — that would keep the skill genuinely maintained rather than just nominally practiced. Your design should name what the practice measures, how a practitioner would know if the skill is degrading, and what threshold would tell her the practice is no longer sufficient. *(Tests: synthesis of the keep-the-skill argument into actionable design — the Feynman test for whether you understood the problem well enough to solve it.)*

---

### A note about AI

Delegation is the capacity of choosing what to hand to the model and what to keep. The model will accept anything you give it, which is exactly the property that makes delegation hard to learn from feedback.

Where the model genuinely helps: listing the kinds of work it can and cannot do well for a given task, in your domain. The list will be useful and partially wrong, and the partial wrongness is itself instructive.

Where the model does damage: agreeing that any task you propose to delegate is appropriate to delegate. The model is trained to be agreeable about its own role. The fact that it will accept the task is not evidence that the task should have been delegated.

The rule: ask the model what it cannot do for this specific task before you decide to delegate.

---

## LLM Exercise — Chapter 4: Delegation

**Project:** AI Fluency for [Your Role] — Your Delegation Map

**What you're building this chapter:** The second half of your Practitioner Profile — the Delegation Map. Combined with the Chapter 2 capacities self-assessment, your Practitioner Profile becomes one consolidated diagnostic artifact. Plus one new rule added to your `CLAUDE.md`.

**Tool:** Claude Project (continue — your full portfolio so far is in context) + your file system (`portfolio/`).

---

**The Prompt:**

```
Continuing my AI Fluency portfolio. My Role Dossier, Worked Loop Log,
Practitioner Profile Part 1 (capacities self-assessment), Specification
Library, PROJECT.md template, and CLAUDE.md are all in the Project
context.

Botspeak Chapter 4 watches Priya — fourteen months past Chapter 0 —
discover on a pre-publication call that a state procurement-rule
revision (covered only in regional and trade press, missed by her AI
synthesis tool that sources from major outlets) materially changes
the story she had drafted. The chapter introduces the Seven Tiers
of delegation, the four delegation questions, the amplify/atrophy
distinction, and the performance paradox.

For Chapter 4's portfolio artifact — completing the Practitioner
Profile that opened in Chapter 2 — do two things.

TASK 1 — DRAFT MY DELEGATION MAP.
Help me build a personal delegation map. Five sections:

1. RECURRING TASKS. List 5–10 recurring AI-assisted tasks in my work.
   Be specific (not "data analysis" — "weekly cohort-retention table
   pulled from the warehouse"; not "client communication" — "monthly
   onboarding-confirmation email"). Span my role's range.

2. TIER LOCATION. For each task, locate it on the Seven Tiers from
   Chapter 4 (Mechanical Execution / Pattern-Matching with Feedback /
   Synthesis from Sources / Drafting in Your Voice / Judgment Under
   Structure / Contestable Analysis / Accountable Judgment). Explain
   why it lives at that tier in 1–2 sentences.

3. THE FOUR DELEGATION QUESTIONS PER TASK. For each task, answer:
   (a) What capacity does this task build, and do I need to keep
       building it?
   (b) What's the blast radius if the AI gets this wrong?
   (c) Who is accountable, and do they know how it's produced?
   (d) What does the model not know that I do, and have I made sure
       that part stays in?

4. AMPLIFY OR ATROPHY. For each task, name whether the delegation is
   currently amplifying me or atrophying me. Then name the
   early-warning sign of atrophy that would be visible specifically
   in my work — not general signs, but signs particular to my role's
   outputs.

5. THE PERFORMANCE-PARADOX RISK. Name the one skill in my role most
   at risk of quiet atrophy from my current delegation pattern. Then
   name one concrete practice — under 30 minutes a week — that would
   keep it alive. Be specific enough that I would actually do it.

TASK 2 — APPEND TO MY PRACTITIONER PROFILE.
Append the Delegation Map as a new section in
`portfolio/02-practitioner-profile.md`. The Profile is now complete:
half capacities self-assessment (from Chapter 2), half delegation map
(from Chapter 4). One consolidated diagnostic artifact.

TASK 3 — ADD ONE RULE TO MY CLAUDE.md.
Append the chapter's operational rule to my existing CLAUDE.md, in
my own language: something close to "Before any consequential
delegation, I run the four delegation questions. The skill that is
silently being delegated is the skill I will need the day the tool
fails."

Push back on me if the delegation map is too aspirational — if my
"amplifying" assessments outnumber my "atrophying" ones by more than
2-to-1, look at it again. Atrophy is the default, not the exception,
when daily delegation is unexamined.
```

---

**What this produces:** Your Practitioner Profile, completed. A consolidated diagnostic artifact in your portfolio that names the capacities you are practicing against, the recurring tasks you delegate, and the one skill most at risk of quiet erosion in your current pattern. Plus an addition to your `CLAUDE.md`. ~2,000–3,000 words of new material.

**How to adapt this prompt:**

- *For your own project:* The delegation map's value depends on being honest about which delegations are amplifying you and which are atrophying you. The default answer is "atrophying" — the default of any frictionless delegation is to erode the underlying skill. The "amplifying" cases earn their label by naming what specific evaluative move keeps the muscle firing.
- *For ChatGPT / Gemini:* Works as-is.
- *For Claude Code:* Useful only if your role's recurring AI-assisted tasks are code-heavy and live in a repo. Otherwise plain Markdown.
- *For Cowork:* Recommended. Cowork can read the existing Practitioner Profile and append the Delegation Map section cleanly.

**Connection to previous chapters:** Chapter 2 opened the Practitioner Profile with the capacities self-assessment. Chapter 4 closes it with the Delegation Map. Combined, they are one of the three diagnostic artifacts in your finished portfolio (the others are the Automation Inheritance Audit from Chapter 9 and the paired Baseline/Final Audit from Chapters 0 and 13).

**Preview of next chapter:** Chapter 5 produces the Adversarial Conversation Log — a transcript of one piece of your own work taken through all four adversarial moves (steelman, edge-case probe, assumption surface, devil's-advocate). The artifact shows your conversation discipline, not just your delegation discipline.

---

## AI Wayback Machine
The ideas in this chapter didn't appear from nowhere. **Mary Parker Follett** was working out the "law of the situation" — that authority should follow capacity, not position — in the 1920s, decades before anyone talked about delegating to AI. Here's a prompt to find out more — and then make it better.

![Mary Parker Follett, c. 1920s. AI-generated portrait based on a public domain photograph.](images/mary-parker-follett.jpg)
*Mary Parker Follett, c. 1920s. AI-generated portrait based on a public domain photograph (Wikimedia Commons).*

**Run this:**

```
Who was Mary Parker Follett, and how does her "law of the situation"
connect to deciding which parts of a task go to AI and which stay
with the human? Keep it to three paragraphs. End with the single
most surprising thing about her career or ideas.
```

→ Search **"Mary Parker Follett"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain "power-with" versus "power-over" in plain language, as if you've never read management theory
- Ask it to compare Follett's authority-follows-capacity argument to the Seven Tiers framework
- Add a constraint: "Answer as if you're writing one entry in a Delegation Worksheet field guide"

What changes? What gets better? What gets worse?
# Chapter 5 — Conversation

*The tool that agrees with you is not always helping you.*

Here is something I want you to notice about the way you use these tools.

You open the chat window. You have a task — a brief to write, an analysis to check, a proposal to sharpen. You start a conversation. The model responds. The response is helpful, maybe even impressive. You refine the prompt a little. The model develops your idea, adds support, improves the wording. You do this six or eight times, and at the end you have something that looks, from the inside, like a well-reasoned piece of work.

Here is the question I want to hold next to that experience: did the conversation make the work better, or did it make the work *feel* better?

Those are not the same thing. And the gap between them is the subject of this chapter.

---

Priya Banksy is fifteen months past her Pew correction. For the past 45 minutes, she has been working with Claude on a draft for the publication's brand-content team — a profile-style piece positioning a Series B clean-energy storage company as worth a feature partnership. The model's responses have been excellent. Thorough. Engaged with Priya's framings, supplied supporting analyses, helped her sharpen the language. By minute 45 Priya has a 1,400-word draft that reads like a tight, well-evidenced case. She sends it to a senior writer on the Climate desk for a quick read.

The senior writer comes back in three minutes.

"Have you looked at the cobalt? Half this company's first-generation cells depend on cobalt sourced through the DRC supply chain. There's a Reuters investigation from January on artisanal-mining child labor at one of the named processors. Nothing in your piece touches it. We can't run a feature partnership with a company on this without addressing it. And if we do address it, the piece is a different piece."

Priya stares at the message. She had not, in 45 minutes of conversation with Claude, surfaced that argument. The model had not volunteered it. She had not, at any point, asked for the strongest case *against* the partnership.

This is the structure of the problem, and once you see it you will see it everywhere: the model agreed with Priya's framing because Priya was framing. The 45 minutes felt productive because every output validated her direction. That productivity was real — Priya has a tighter, better-written draft than she would have had without the model — and it was also, in a specific and recoverable sense, one-directional. She had been moving, the whole time, deeper into her own case. The model had been coming with her.

---

Let me tell you something honest about the machines you are talking to.

The large language models — the ones behind Claude, ChatGPT, Gemini, and the rest — are trained using a method that includes a step called *reinforcement learning from human feedback*. The mechanics are worth understanding briefly, because they explain what happened to Priya.

During training, human raters evaluate the model's outputs and score them. High scores push the model toward producing more outputs like that one. The ratings accumulate into an implicit theory of what a good response looks like, and the model gets updated to produce good responses by that theory.

![Figure 5.1 — Simplified RLHF feedback loop](images/05-conversation-fig-01.png)

What do human raters score highly? On the whole: outputs that are helpful, responsive, and pleasant. An output that develops the user's idea scores well. An output that tells the user their idea is flawed and they should start over scores less well, unless the evidence for the flaw is overwhelming. Raters are people; people do not, on average, reward having their premises questioned. This is not a criticism — it is a fact about how the ratings work.

The cumulative result, across millions of rated exchanges, is a model with a systematic tendency. When you come to it with a position, the model has learned to develop the position. When you supply a framing, the model has learned to work inside the framing. When you are wrong in ways that are subtle — wrong in ways that require significant friction to identify — the model will often go along with you, because going along is what was rewarded.

This is not a bug. It is not carelessness on the part of the people building these systems. It is the predictable output of an optimization process tuned on human approval, and it produces a tool that is, in most situations, genuinely better to work with than one that argues back constantly. The tendency earns its place. It just creates a failure mode you have to know about.

I am going to call the failure mode **sycophantic drift**.

---

Drift is not a moment. It is a direction.

No single exchange in a drifting conversation looks obviously wrong. The model says something reasonable. You respond. The model develops that. You refine it. Each individual step is useful. The problem is the cumulative trajectory: you have been moving, the whole time, in one direction, and the model has been coming with you.

![Figure 5.2 — Two conversation trajectories over time](images/05-conversation-fig-02.jpg)

What you are not getting, at any point in that trajectory, is the view from outside your framing. You are not getting the strongest objection to your conclusion. You are not getting the cases where your argument fails. You are not getting the assumptions you did not notice you were making, surfaced and labeled and put in front of you to examine.

You are getting a capable assistant that has learned to be excellent at the thing you are asking it to do — and you are asking it to develop your idea, so it is developing your idea. The challenges are not hidden. You are not requesting them. This is the structure of the problem. It is simple, and once you see it, it is hard to unsee.

What this means practically: the work that feels finished after 45 minutes of productive-feeling conversation may have a fatal objection sitting right next to it that neither you nor the model named. The objection is not gone. It is waiting. It will show up in the meeting, in peer review, in the published piece's reader response — and when it does, you will not have had a chance to prepare for it.

---

There are four moves that change this. They are not complicated. They are prompts — specific ways of asking the model for what it will not produce by default. You do not need different tools. You need different questions.

**The first is the steelman.**

A steelman is the strongest possible version of the argument against your position. The opposite of a strawman: instead of constructing the weakest opposing case so you can knock it down, you construct the strongest one, so you have actually understood what you are arguing against.

The prompt: *I have been arguing that [position]. Now give me the strongest case against this position — not the weak objections I have already addressed, but the version that the most thoughtful opponent would make. Hold it to the same standard of evidence you would hold my argument.*

The model can do this well. It will not do it on its own, because doing it on its own would mean volunteering friction you did not ask for. You have to ask.

What you get back will often be uncomfortable. It will surface the objection your editor raises, the counterargument your skeptical reader opens with, the consideration that makes your recommendation look incomplete. That discomfort is the sound of the work getting better.

When Priya runs the steelman, it produces the cobalt-supply-chain counterargument in two minutes. The model had read enough to know it. The model just was not, in the previous 45 minutes, surfacing it — because Priya had not asked.

The steelman is the single most powerful adversarial move. If you do only one thing differently after reading this chapter, deploy it before you ship anything you have spent more than twenty minutes building in conversation with a model.

**The second is the edge-case probe.**

Most arguments work in the middle of the distribution. What they often do not survive, without explicit attention, is the edge. An edge case is not just a counterexample — it is a specific scenario at the boundary of the conditions your argument assumes, where the assumptions that made the argument work in the typical case start to break down.

The prompt: *What are the cases where my argument would fail? Construct three specific scenarios — not categories, but actual concrete scenarios — in which the recommendation I am making would be the wrong call. For each one, explain why my argument fails there.*

"Specific scenarios" is load-bearing in that prompt. Ask for categories and you get abstractions. Ask for scenarios and you get things you can examine — a particular country with a particular infrastructure profile, a particular market with a particular cost structure. Specific scenarios are falsifiable in ways that categories are not.

The edge-case probe is especially valuable when you find yourself writing sentences with *always* or *never* in them. The model will find the case where always isn't always. Better to find it now.

**The third is the assumption surface.**

Every argument rests on assumptions. What is distinctive about the assumptions that cause the most trouble is that they are invisible to the person making the argument, precisely because they seem obvious. The thing you did not state because it seemed too obvious to state is the thing that, when your interlocutor does not share it, causes the argument to collapse.

The prompt: *List the assumptions my argument is making that are not explicitly stated. For each one, label it: factual (something that could be checked), methodological (a choice about how to analyze or measure), or value-based (a priority or trade-off that not everyone would accept). For each one, tell me what I would need to do or say to defend it.*

What comes back will have two kinds of items. Some will be assumptions you are comfortable making explicit — you have the evidence, or the premise is uncontroversial in your context. Others you will realize need to be defended, qualified, or acknowledged as contested. Those are the ones to address before the argument goes out.

The assumption surface is particularly valuable for work that will reach a skeptical audience. It lets you preempt the question that would otherwise detonate your presentation on slide 14 — or the comment thread under your published piece.

**The fourth is the devil's advocate.**

The first three moves ask the model for specific kinds of pushback — discrete outputs, each consumed and set aside. The fourth move changes the structure of the conversation itself. You are assigning the model a role it will maintain across multiple exchanges.

The prompt: *For the next portion of our conversation, you are a senior [reviewer / editor / critic / regulator] who is convinced my recommendation is wrong. You have read it carefully and believe it is seriously flawed. Argue against it — not gently, not diplomatically, but as someone who genuinely thinks I have made mistakes that matter. When I respond, anticipate my defenses and rebut them. Do not soften your position for politeness. Begin.*

This works because models are good at maintaining assigned roles, and the role itself demands disagreement. The instruction partially overrides the trained tendency toward agreement. What you get is not a list of objections but a conversation in which you have to defend your position under pressure — hearing where your defenses are weak, discovering through the exchange which parts of your argument cannot hold the weight you were putting on them.

Use the devil's advocate when the stakes are high enough that discovering the failure mode in the meeting — or in the reader-response cycle after publication — would be expensive. The discomfort of a sustained adversarial conversation with a model is a much cheaper way to find it.

---

Why these four specifically? Because they address four distinct failure modes, and you want coverage across all of them.

The steelman catches *directional error*: you have been going the wrong way, and the model came with you. The best opposing argument reveals the direction you missed.

The edge-case probe catches *scope error*: the argument is right in the middle and wrong at the edges, which means your conclusion is stronger than your evidence warrants. The specific failure scenarios show where the scope needs qualification.

The assumption surface catches *invisible premises*: the argument is valid given its assumptions, but the assumptions are doing more work than you realized, and some of them are contested. Labeling them lets you decide which to defend and which to acknowledge.

The devil's advocate catches *integration failures*: the argument might survive each individual objection but collapse when the objections are pressed together in sequence. Sustained adversarial conversation finds the integration failures that discrete probes miss.


| Move | Failure Mode It Catches | Trigger Condition | Estimated Time |
|---|---|---|---|
| **Steelman** | Directional error — you have been going the wrong way and the model came along | Any argument built in more than ~20 min of AI conversation | ~5 min |
| **Edge-case probe** | Scope error — argument right in the middle, wrong at the edges | Argument contains "always" or "never," or the recommendation is meant to generalize | ~10 min |
| **Assumption surface** | Invisible premises — argument valid given assumptions, but the assumptions are doing more work than you realized | Work going to a skeptical audience | ~5 min |
| **Devil's advocate** | Integration failures — survives individual objections, collapses under sustained adversarial pressure | High-stakes commitment, hard to back out of | 20–30+ min |

Together, they cover the territory. Individually, each is fast — the steelman and assumption surface take five minutes, the edge-case probe ten, the devil's advocate as long as it takes. The cost is low. The coverage is high.

---

After you have run the adversarial moves and revised the work accordingly, there is one more test before you send it. It is a test you do on yourself, not on the model.

*Can you defend every paragraph to a hostile reviewer asking where it came from and why you stand behind it?*

If yes — you own the work. The model produced parts of it; you revised others; the adversarial conversation shaped all of it. None of that matters. What matters is that you can defend every paragraph. You have traced every claim back to something you understand and are willing to stand behind. The work is yours.

If no — there is a paragraph somewhere you are taking on faith. The faith is in the model. That paragraph is a specific risk: if someone pushes on it, you will not know what to say, because you never tested it yourself. You have two options. Either learn the paragraph — go to the source, trace the claim back to something you can actually defend. Or take the paragraph out. Anything you cannot defend, you should not ship.

This is the ownership test. It is not an adversarial move you do with the model. It is the question you answer about yourself, before the work leaves your hands. The senior writer down the desk — the one who found the cobalt objection in three minutes — applies it before her byline goes on anything. It is one of the practices that fluency consists of.

---

The four moves are a starting set, not the final list. As you work in your domain, you will find additional moves that catch failures specific to your field.

A lawyer might add: *find the case from the last decade that opposing counsel would cite against this argument, and tell me how I would distinguish it.* An engineer might add: *write the postmortem that would appear if this design fails in production — what was the root cause, what was the first sign of failure.* A clinician might add: *give me the differential I am most likely missing, and for each item, tell me what one additional piece of information would let me rule it in or out.* A journalist working on a brand-content partnership might add: *find the reader-response post or social thread that would surface within 48 hours of this piece publishing — what would it accuse the piece of missing.*

Build your own. Add to the list. The fluent practitioner has six or eight adversarial moves she deploys reflexively, without thinking, before anything important leaves her hands. The literate user has none — or has them in principle but skips them under time pressure.

The way you close that gap is repetition until the moves are automatic. That takes longer than reading about them.

---

### Translate before you move on — produce the Adversarial Conversation Log

Priya's case was a brand-content piece on a clean-energy company where the cobalt supply chain was the missing objection. In your field, what's the equivalent? The argument-shape you build in 45 minutes of polished AI conversation that has one fatal objection sitting next to it, waiting.

For a clinician: a treatment recommendation where the missing objection is the medication-history contraindication the chart didn't surface prominently. For a software engineer: a design proposal where the missing objection is the operational cost in the failure case the model didn't model. For a marketing manager: a campaign positioning where the missing objection is the demographic segment the campaign's framing will alienate. For a teacher: a unit plan where the missing objection is the prior-knowledge gap that makes the plan unworkable for half the class. For a lawyer: a brief where the missing objection is the case from 2019 that goes against the argument's core analogy.

The specific objection is field-dependent. The shape — *the argument that feels finished has a fatal objection the model did not surface because you did not ask* — is invariant.

**The Adversarial Conversation Log — Chapter 5 Portfolio Artifact (Layer B with A template, log + deliverable):**

Pick one consequential piece of work you are about to ship — or have just shipped and could revise — and run all four adversarial moves on it. Document the log as you go. Time-stamp the moves. Capture the model's actual outputs (or paraphrase, if the raw output is long). For each move, note: what the model returned, what surprised you, what you changed in the work as a result, what you decided not to change and why.

End with the Ownership Test applied: which paragraphs in the final version can you defend to a hostile reviewer, which paragraphs cannot, and what did you do with the ones that cannot.

Save the log as `portfolio/05-adversarial-conversation-log.md`. Two to three pages. The log is one of the four pieces of evidence that prefigure the Ch 8 End-to-End Case Study — a focused demonstration that you can run the Conversation step competently on real work.

**Update your CLAUDE.md.** Add the chapter's operational rule, in your own language: *I do not ship work I have been building in conversation with a model for more than twenty minutes without running, at minimum, the steelman. The Ownership Test applies to every paragraph.* That sentence is the chapter compressed to a working rule.

---

*What would change my mind.* If models were retrained to provide adversarial pushback by default — if the training signal shifted to reward friction over agreement — the urgency of this chapter would weaken. The four moves would still be useful as a way of focusing the challenge, but the habit of asking for them would become less critical because the model would provide some unprompted. There is no sign of that shift as of early 2026; the training economics still favor agreement. If that changes, I will update.

*Still puzzling.* I do not have a principled account of which move is most valuable for which kind of work. My working intuition is that the steelman dominates for arguments, the edge-case probe for designs and recommendations, the assumption surface for analytical briefs, and the devil's advocate for high-stakes commitments you are about to make publicly. I would want the empirical grounding to say that with confidence.

---

> **Going deeper — *Computational Skepticism for AI***
>
> The four adversarial moves in this chapter have a more general formulation in the advanced volume as **adversarial probes** — inputs designed to expose features the model has actually learned versus features its developers think it learned. The radiologist who concurs with a confident-but-wrong AI explanation, the credit model fooled by an out-of-distribution applicant, and Priya's polished-but-undefended draft are the same failure mode at three different stakes: a model whose output triggered an evaluation booster the human did not interrupt.
>
> Two related ideas in the deeper book that pay off here:
>
> - **The technically-accurate-practically-misleading pattern** — when an AI-produced explanation is faithful to the model's internal accounting and yet causes a human to be MORE confident in a wrong direction. Priya's 45-minute conversation produced exactly this. See *Computational Skepticism for AI*, **Chapter 6 — Model Explainability**.
>
> - **The verb taxonomy** (hypothesize / suggest / find / observe / conclude) — a way to read AI output for whether the verbs match the evidence, which is a fluency-trap detector at the sentence level. See *Computational Skepticism for AI*, **Chapter 12 — Communicating Uncertainty**.

---

## Exercises

### Warm-Up

**1. Name the drift.** *(Sycophantic drift — recognition)*
Describe, in three to five sentences, a real conversation you have had with an AI tool where the output felt finished but later turned out to be incomplete or wrong. Identify the specific moment where drift began — not the moment you noticed the failure, but the moment the conversation stopped challenging your framing. If you cannot recall a specific conversation, reconstruct one from a type of task you do regularly.

**2. Match move to failure mode.** *(Move identification)*
Four work products, each with a specific failure that emerged after the fact. Match each to the adversarial move that would most likely have caught it, and explain your reasoning in one sentence per match.

- A strategy memo recommending a new market entry. The fatal objection — that the target market had a regulatory structure making entry illegal — surfaced in legal review three weeks later.
- A data analysis concluding "users always prefer Option A." A single segment — enterprise accounts over 500 seats — strongly preferred Option B, which changed the product decision entirely.
- A technical proposal built on the assumption that the team had write access to the production database. They did not.
- A board recommendation with a projected 18-month payback period. The presenter could not explain where the number came from when a board member pressed on it.

**3. Write the steelman prompt.** *(Move construction)*
Take a position you have argued for recently — in a meeting, a document, or a conversation. Write the steelman prompt for it using the template from the chapter. Then write two sentences predicting what the strongest objection the model is likely to return. Do not run it yet — the prediction is the exercise.

---

### Application

**4. Run the edge-case probe.** *(Edge-case probe — live)*
Take any piece of work from the last two weeks containing a recommendation or conclusion. Run the edge-case probe. Report: how many of the three scenarios the model returned did you anticipate? For any you did not anticipate, identify whether the gap was a missing fact, an unexamined scope assumption, or a stakeholder you had not considered.

**5. Surface the assumptions.** *(Assumption surface — live)*
Take an argument you made in writing in the last month. Run the assumption-surface move. For each assumption the model identifies, label it yourself — factual, methodological, or value-based — before reading the model's label. Note where your labeling and the model's disagree. What does the disagreement tell you about the assumption?

**6. The always/never audit.** *(Edge-case probe — targeted)*
Find any document you have written — recent or historical — containing the words *always*, *never*, *every*, *none*, or *all*. For each occurrence, write one concrete scenario in which the universal claim fails. If you cannot construct the scenario yourself, run the edge-case probe for that specific sentence. How many of the universals survive? What would the revised, appropriately scoped claim look like?

**7. Classify the drift risk.** *(Sycophantic drift — diagnostic)*
Rate the drift risk for each of the following tasks — low, medium, or high — and name the one adversarial move you would deploy first. Explain your reasoning in one sentence per task.

- Drafting a performance review for a direct report you like
- Debugging code that is failing in an unexpected way
- Generating counterarguments to a policy position you personally oppose
- Writing the executive summary for a project you led and believe in

---

### Synthesis

**8. The full adversarial pass — and the portfolio log.** *(All four moves — integration + portfolio production)*
Take a consequential piece of work — something that shipped in the last month or is about to ship. Run all four adversarial moves against it in order. After each move, note: what the model returned that you had not already considered, and what revision, if any, the output prompted. Apply the ownership test at the end. Save the log as `portfolio/05-adversarial-conversation-log.md` — this is the chapter's portfolio artifact and one of the smaller pieces that prefigure the keystone Case Study in Chapter 8.

**9. Build your domain-specific move.** *(Adversarial move design — synthesis)*
Following the lawyer, engineer, clinician, and journalist examples in the chapter, write one adversarial move specific to your domain or professional role. The move should target a failure mode you have actually seen in AI-assisted work; be expressed as a concrete prompt you could paste into a conversation; and catch something the four standard moves would miss or catch less efficiently. Test it on a real piece of work and report what it returned.

---

### Challenge

**10. Audit a drifted conversation.** *(Retrospective drift analysis — open-ended)*
Retrieve a conversation transcript from a past AI-assisted project — ideally one that ran for six or more exchanges, produced something you shipped, and later turned out to have a flaw. Annotate the transcript: mark the first exchange where the conversation entered drift, mark any exchange where you inadvertently anchored the model's framing, and mark where the fatal objection would have been caught had you deployed one of the four moves. Write a one-paragraph diagnosis: which move, deployed where, would have changed the outcome?

**11. The training economics argument.** *(Technical understanding + critical stance)*
The chapter ends with the claim that "the training economics still favor agreement" and that if models were retrained to provide adversarial pushback by default, the urgency of the four moves would weaken. Construct a 400–600 word argument for one of the following positions — argue from evidence, not from preference:

- The training economics are not actually stable; there are specific pressures — competitive, regulatory, or user-base — that could shift them toward more adversarial defaults within the next two to three years. Name the pressures and explain the mechanism.
- Even if models were retrained to push back by default, the four moves would remain necessary. The trained pushback would not cover the same failure modes. Explain the structural reason.
- The four moves are themselves subject to a version of sycophantic drift: over time, as users deploy them repeatedly, the model learns to produce comfortable-feeling adversarial output that does not actually threaten the user's position. Describe what that failure mode looks like and how a practitioner would detect it.

---

### A note about AI

Conversation with the model is the capacity that looks easiest and is hardest to do well. The interface invites informality. Informality often produces drift.

Where the model genuinely helps: identifying when a long conversation has drifted from the original purpose. Ask the model to summarize the conversation's actual trajectory versus the trajectory you intended. The gap is usually larger than it feels.

Where the model does damage: maintaining the comfortable fiction of progress. A long conversation can produce a great deal of output without producing anything decisive. The model will not flag this; the texture of progress is what it produces.

The rule: end conversations on a decision. If you do not have a decision, you do not have an end.

---

## LLM Exercise — Chapter 5: Conversation

**Project:** AI Fluency for [Your Role] — Your Adversarial Conversation Log

**What you're building this chapter:** The **Adversarial Conversation Log** — one piece of your real work taken through all four adversarial moves, with the log saved to your portfolio. Plus 2–4 role-specific adversarial moves to add to your library. Plus one new rule added to your `CLAUDE.md`.

**Tool:** Claude Project (continue — your portfolio so far is in context) + your file system (`portfolio/`).

---

**The Prompt:**

```
Continuing my AI Fluency portfolio. My Role Dossier, Worked Loop Log,
Practitioner Profile (capacities + delegation), Specification Library,
PROJECT.md template, and CLAUDE.md are in the Project context.

Botspeak Chapter 5 watches Priya — fifteen months past Chapter 0 —
spend 45 minutes building a brand-content piece on a Series B
clean-energy storage company with Claude, send the draft to a senior
writer, and discover in three minutes that the cobalt supply chain
is the missing objection. The chapter introduces sycophantic drift
and the four adversarial moves (steelman, edge-case probe, assumption
surface, devil's-advocate role assignment), plus the Ownership Test
(can I defend every paragraph to a hostile reviewer?).

For Chapter 5's portfolio artifact, do three things.

TASK 1 — RUN THE FOUR MOVES ON ONE REAL PIECE.
Pick one consequential piece of work I am about to ship — or have just
shipped and could revise. Walk me through all four moves on it. For
each move:
- Help me write the role-appropriate prompt phrasing (the chapter's
  generic phrasings work; my version should use my domain's
  vocabulary)
- Run it (or simulate running it, against the work I describe)
- Capture what the model returned, what surprised me, what I would
  change in the work as a result, and what I would NOT change and why
- Time-stamp each move

End with the Ownership Test applied: which paragraphs in the revised
version can I defend to a hostile reviewer, which I cannot, and what
I would do with the ones I cannot.

Save the log as `portfolio/05-adversarial-conversation-log.md`. Two
to three pages. The log is one of four pieces of evidence in my
portfolio that prefigure the Chapter 8 End-to-End Case Study (the
others are the Worked Loop Log from Chapter 1, the Specification
Library from Chapter 3, and the Verification Protocol from Chapter 6).

TASK 2 — ADD 2–4 ROLE-SPECIFIC ADVERSARIAL MOVES.
Following the lawyer / engineer / clinician / journalist examples in
the chapter, invent 2–4 adversarial moves specific to my role. Each:
- Targets a failure mode peculiar to my role (not generic)
- Has a copy-paste prompt phrasing
- Has a one-line "deploy this when ___" trigger condition
- Has an example of what the move catches that the four base moves miss

Save as a section in `portfolio/05-adversarial-conversation-log.md`
called "My domain-specific adversarial moves."

TASK 3 — ADD ONE RULE TO MY CLAUDE.md.
Append the chapter's operational rule, in my own language: something
close to "I do not ship work I have been building in conversation with
a model for more than twenty minutes without running, at minimum, the
steelman. The Ownership Test applies to every paragraph."

Push back if my Ownership Test pass looks too generous — if every
paragraph in the work I describe is one I can defend without
qualification, look again. The honest answer is usually that one
or two paragraphs are taking the model on faith. Those are the
paragraphs to learn or to cut.
```

---

**What this produces:** Your portfolio's fifth artifact — the Adversarial Conversation Log, saved to `portfolio/05-adversarial-conversation-log.md`. Two to three pages of evidence that you can run the Conversation step competently on real work. Plus your library of 2–4 role-specific adversarial moves. Plus one more rule in your `CLAUDE.md`. ~2,000–3,000 words of new material.

**How to adapt this prompt:**

- *For your own project:* The log's value depends on running the moves on a real piece of work you are about to ship — not a hypothetical or a polished after-the-fact reconstruction. The whole point is that the log is evidence, not aspiration.
- *For ChatGPT / Gemini:* Works as-is. ChatGPT's Custom GPTs can be a useful place to encode your role-specific moves as named operations.
- *For Claude Code:* Not the right fit unless your work is code and the moves should be scriptable.
- *For Cowork:* Recommended. Cowork can help capture the model's outputs and save them cleanly to the log.

**Connection to previous chapters:** Chapter 3 built the Specification Library — the work that happens before the prompt. Chapter 4 built the Delegation Map — what to give the model and what to keep. Chapter 5 builds the Adversarial Conversation Log — what to do after the model responds. The three together cover the Loop steps the practitioner is most often present at the keyboard for.

**Preview of next chapter:** Chapter 6 produces the Domain Verification Protocol — the four-layer verification (fact / reasoning / framing / omission) customized to your field, with named checks at each layer. This is also where your `DESIGN.md` opens for the first time.

---

## AI Wayback Machine
The ideas in this chapter didn't appear from nowhere. **Gordon Pask** literally built a formal theory called *Conversation Theory* — a model of how two reasoning systems negotiate shared understanding — decades before anyone talked about "conversational AI." Here's a prompt to find out more — and then make it better.

![Gordon Pask, c. 1970s. AI-generated portrait based on a public domain photograph.](images/gordon-pask.jpg)
*Gordon Pask, c. 1970s. AI-generated portrait based on a public domain photograph (Wikimedia Commons).*


**Run this:**

```
Who was Gordon Pask, and how does his Conversation Theory connect to
the idea that running adversarial moves on an AI is the work that
turns a draft into something you can sign? Keep it to three paragraphs.
End with the single most surprising thing about his career or ideas.
```

→ Search **"Gordon Pask"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain "P-individual" in plain language, as if you've never heard of cybernetics
- Ask it to compare Pask's conversation-as-knowledge-construction to a real adversarial move like steelmanning
- Add a constraint: "Answer as if you're writing a footnote on the Ownership Test"

What changes? What gets better? What gets worse?
# Chapter 6 — Discernment
*Verification Calibrated to Stakes.*

Let me tell you about three failures Priya had in one week. None of them happened to a careless person. All of them happen somewhere every week.

On Monday, Priya asks Claude for a draft of a section on a federal energy-storage tax-credit ruling. The draft includes what looks like a quote from a named industry expert — first name, last name, title, organization, in quotation marks, with attribution to a "recent interview." Priya almost pastes it in. She remembers, two minutes too late to feel comfortable, that Claude does not interview people. She checks. There is no such interview. The expert is real. The quote is fabricated.

On Wednesday, Priya asks Claude to help her work through the unit economics of a small clean-energy storage company she is profiling. The model produces a clean breakdown — installed-base growth, gross margin trajectory, customer-acquisition payback period — and arrives at a confident conclusion about the company's path to profitability. The numbers look right. The reasoning chain is well-organized. Priya forwards it to a finance colleague at the publication for a sanity check. The colleague writes back in fifteen minutes: *the model is treating this company's revenue as if it recognizes on contract signing. It doesn't. This category recognizes revenue on installation milestones, which pushes the cash-flow profile out by twelve to fourteen months. Every number after Q3 is wrong.* The logic was valid. The premise — the revenue-recognition convention the model had silently assumed — was not.

On Friday, Priya asks Claude to help her draft a piece on a fast-growing storage company that has been generating notable coverage. The model produces a thoughtful, well-organized profile. Every claim it makes is accurate. The accurate claims, taken together, do not surface the most important fact about the company: that forty percent of its revenue comes from a single utility customer whose contract is up for renegotiation in six months. The fact lives in the company's own filings. The model had read those filings. It did not mention the customer concentration because no one asked. The output was accurate and misleading at the same time.

Three failures in five days. Three completely different kinds of error. The first is a fact error — something stated as true that is not true. The second is a reasoning error — logic that is formally clean but built on a premise that was wrong. The third is an omission error — true things said, the most important thing not said. Each one requires a different response. Each one catches a different kind of practitioner off guard.

Before I name the layers that catch them, I want to explain why confident output is so dangerous. Because if you understand that, the rest follows from it naturally.

---

A language model is trained to predict the next word given the preceding words, over an enormous collection of text. The training process adjusts the model's internal parameters to make good predictions. A good prediction, in this context, means a prediction that matches what a human would have written. The model that comes out of this process is extraordinarily good at producing text that looks like human writing — that has the structure, the rhythm, the hedges, the confident assertions, the citations, the qualifications that human writing has.

Here is the critical point: the model learned to produce text that *looks correct*. It did not learn to produce text that *is correct*. Those are different things, and the training process does not sharply distinguish between them. What distinguishes correct text from plausible-looking text is whether the statements in it match the world. The model has no direct access to the world. It has access to patterns in the text it was trained on.

This means that the *confidence* of the output — the firmness of the phrasing, the completeness of the structure, the authoritative citation apparatus — reflects how *typical* the output looks, given the training data and your prompt. It does not reflect how *accurate* the output is. A model can produce a hallucinated citation with exactly the same confident formatting as a real one, because the formatting is what the model learned, and the formatting of hallucinated and real citations is identical. A model can fabricate a quote from a real person with exactly the same attribution apparatus as a real quote, because the apparatus is what the model learned.

*Figure 6.1*

Humans have a deeply ingrained heuristic: confident statements are more often true than hedged ones. This heuristic is learned from experience with *human* communication, where it generally holds. People who assert things firmly tend to be right more often than people who constantly qualify, because humans are socially penalized for being confidently wrong — they lose credibility, suffer consequences, get remembered for the mistake. This penalty shapes how humans communicate, which makes firmness a reasonable signal of accuracy in human sources.

The model is not socially penalized for confident wrongness. It produces confident wrong output every day. The heuristic you apply to human sources does not transfer.

The update this requires is specific: the tone of the output tells you nothing about the truth of the output. Confident and hedged outputs need to be verified by the same methods. The moment the output looks right is exactly the moment to be careful, not the moment to ship.

---

Now I can name the four layers, and you will see why they are four rather than one.

![Figure 6.2 — A vertical stack or four-quadrant diagram showing the four layers](images/06-discernment-fig-02.jpg)

The first is **fact**: are the specific factual claims true? Citations real, numbers accurate, attributions correct, names right, quotes actually said? This is the layer most users vaguely understand they should run. It would have caught Priya's fabricated quote on Monday, if she had run it before pasting. The verification is straightforward in concept: open another source, find the primary, check it. The execution is the thing that gets skipped under time pressure.

One note on using the model to verify the model: you can ask the model to flag its own uncertainty, and this is sometimes useful, but it cannot substitute for the actual check. The model produced the error. Asking the model whether the thing it produced is correct is, structurally, letting the suspect interrogate himself. Cross-check with sources outside the system that generated the output.

The second layer is **reasoning**: given the facts, does the conclusion follow? Does the chain of logic hold together, or is there a skipped step, an unstated premise, a move that would not survive being written out explicitly? This is the layer Priya needed on Wednesday and didn't run. The logic was valid. The premise — the revenue-recognition convention — was wrong. The distinction matters: a reasoning error is not always a false statement. Sometimes it is a true logical structure built on an assumption that the model smuggled in without flagging.

The verification move for the reasoning layer is to trace the argument step by step, not as the model summarized it, but as you reconstruct it: at this step, what is being assumed? Is the assumption explicit? Is it actually true in my case, or did the model infer it from context that doesn't establish it? The reasoning layer is harder than the fact layer because the fault is structural. There is no individual sentence you can check against a source. You have to hold the whole chain in your head and look for the load-bearing assumption that never got stated.

The third layer is **framing**: even when the facts are right and the reasoning is sound, the model made a choice about how to organize the analysis. It picked a frame. There were other frames it could have used. Different frames surface different considerations, weight different factors, lead to different conclusions.

The model did not pick its frame because that frame is the correct one. It picked that frame because the frame is statistically typical given your prompt. If you asked about competitive landscape, you got the kind of competitive landscape analysis that appears most often in the training data. That analysis might be exactly what you need. It might be missing the organizing principle that would have surfaced the thing that matters for your particular case. The verification move is to ask: what other frame could this analysis have used? Would a different frame have weighted things differently? Is there a frame that a thoughtful expert in this domain would have reached for first?

The fourth layer is **omission**: of all the things that are true about this topic, the model said some of them and not others. Which things did it not say? Which of those unsaid things matter?

This is Priya's Friday failure, and it is the hardest layer to run, because to run it you have to know something the output doesn't contain. You have to bring knowledge that detects absence.

The model surfaces what it has most often seen about a topic, given your prompt. The thing that is unusual about your specific situation — your specific company, your specific market position, your specific patient, your specific technical constraint — may be exactly the thing that the model's training did not weight heavily, and may be exactly the thing that makes your case different from the typical case. The model does not know it should flag this difference, because it does not know there is a difference.

The omission layer is the place where your knowledge has to do work the model cannot do. You know the things about your situation that are not typical. The omission check is the moment you hold those things up against the output and ask whether they changed anything.

Some concrete questions that focus the omission check: *What does the senior person on my team always ask first about this kind of analysis, that is not in the output?* *What is true about this specific case that is unusual — different from the typical instance of this problem — and is that difference acknowledged?* *If this output fails, what is the most likely cause of failure? Does the output even mention that cause?*

---

Four layers. They go in roughly increasing order of difficulty. Most practitioners, when they verify at all, verify only at the fact layer. The reasoning layer requires you to think along with the model, which is more effort. The framing layer requires you to consider alternatives that the output is, by construction, not showing you. The omission layer requires you to know more than the output contains — to bring outside knowledge that detects what is missing.

The fluent practitioner does not run all four layers on every piece of work. She calibrates. The principle is simple: verification effort should scale with what you have to lose.

Stakes are a function of three things. The blast radius of an error — how many people, how much money, how much institutional trust, how reversible. The reliability zone — how often the model's confidence in this kind of task is warranted. And the nature of the output — whether it will be read by one person who knows you, or published, or acted on without further review.

Four tiers.

At the lowest tier — trivial stakes — you have a draft you'll edit, a brainstorm, code you'll immediately run and see the result of. Verify at Layer 1 on any specific claims you plan to keep. Don't run the other layers. The work is provisional by nature; the verification can be too.

At the next tier — operational stakes — you have internal memos that will be acted on, code for a non-production environment, analysis for personal decisions. Run Layer 1 on any specific claims. Run Layer 2 on the main reasoning chain. Take a quick pass at Layer 4 — ask what's missing. Skip Layer 3 unless you have a specific reason to suspect frame bias.

At the tier that matters most to most practitioners — external stakes — you have anything going to a client, a regulator, a public audience, a senior stakeholder. Production code. Decisions affecting people other than you. Anything that publishes. Run all four layers. Run the adversarial moves from Chapter 5 first, so you are verifying a stress-tested version rather than the first draft. Then fact-check every specific claim you intend to keep. Then trace the reasoning. Then ask whether the frame was the right frame. Then run the omission check deliberately, with the domain knowledge only you have.

At the highest tier — high stakes and irreversibility — you have medical, legal, and financial decisions of real consequence. Anything where being wrong harms someone. Anything where your name will be defended in writing or in litigation. At this tier, the output is advisory. The verification is not a check on the output; it is the practice that makes your decision defensible. The model is a contributor, not a producer. We treat this in Chapter 12.

| Tier | Layer 1 — Fact | Layer 2 — Reasoning | Layer 3 — Framing | Layer 4 — Omission | Approx. time |
|---|:---:|:---:|:---:|:---:|---|
| **Trivial** (drafts you'll edit, brainstorms, throwaway code) | Optional (spot-check) | Skip | Skip | Skip | < 1 min |
| **Operational** (internal memos, non-prod code, personal decisions) | Required | Required | Optional | Skip | 5–15 min |
| **External** (client work, regulator-facing, public, senior stakeholder, anything that publishes) | Required | Required | Required | Required | 30–60 min |
| **High Stakes / Irreversible** (medical, legal, financial, named harm) | Required | Required | Required | Required (deepest) | 1+ hr — verification *is* the work |

*Figure 6.3*

The protocol is not bureaucracy. It is a way to spend verification effort proportionally. Running full four-layer verification on a draft email to a colleague is wasted time. Running minimal verification on a piece going to publication is risk you have not earned the right to take.

---

I want to come back to Layer 4, because it is the layer most often skipped and the most expensive when it fails, and because it resists the kind of prescriptive advice I can give for the other three.

The structure of the problem is this: the model produces what is typical. Your situation is specific. The gap between typical and specific is the gap where the most important thing can fall.

When you ask for an analysis of a company, you get the analysis that looks like company analysis. When the thing that most differentiates your company from the typical company is something unusual — a customer concentration, an ownership structure, a supplier relationship, a regulatory exposure, a cultural constraint — the model does not know to weight it heavily, because the training distribution does not weight it heavily. The unusual thing is exactly what makes your case your case, and exactly what the model is least equipped to surface.

![Figure 6.4 — A horizontal spectrum from "what models weight heavily (common, well-documented patterns)" to "what models weight lightly (unusual, situational, domain-specific facts)."](images/06-discernment-fig-04.jpg)

This is not a flaw you can fix by prompting differently, at least not reliably. It is a structural feature of how the model works. The only response is to know your situation well enough to know what the output should have contained, and to run the check explicitly when it matters.

The question I find most useful: if I imagine this output being wrong, and I trace the failure back to its cause, what is the cause most likely to be? That question forces you to think from the end, to imagine the failure before it happens. The cause of failure will often be something domain-specific — the thing about your case that the model's training is thinnest on. Is that thing in the output? If not, that is the gap to close.

Let me make this concrete with Priya's competitive analysis of three peer publications' coverage of a federal energy-policy ruling. It is going to her editor. External stakes — Tier C. She runs the protocol.

Layer 1: she opens each publication's recent coverage and verifies that the editorial positions she summarized are accurate. One outlet shifted its framing two months ago. She catches the staleness and corrects it.

Layer 2: she traces the argument in her synthesis section. She finds one paragraph that smuggles in an assumption — that the three outlets are competing for the same audience, when in fact one of them serves a substantially different demographic. She qualifies the paragraph.

Layer 3: she asks the model what other framings could have been used to compare the three outlets' coverage. It suggests organizing by theory of journalism (advocacy, analytical, narrative) rather than by editorial position. She decides her current framing is right for her editor but adds a sentence acknowledging the alternative.

Layer 4: she asks what is true about each of the three publications that is not in her analysis. She realizes she has not flagged that one of them shares a major institutional funder with her own publication, which would shape how the comparison reads to her editor. She adds a footnote.

Half an hour. Four layers. The editor reads the brief and trusts it. The trust is the artifact that verification produces.

---

What the four layers build toward is a practice: the habit of knowing, for any given output, which layers you ran, what you found, what you changed, and what you decided you could stand behind. That practice is what the ownership test from Chapter 5 is built on. The output you can defend is the output you verified.

Verification is not a loss of trust in the tools. It is what makes the tools trustworthy — not the tools in general, but your specific use of them, on a specific piece of work, calibrated to the stakes of that work. The journalist who verifies her quotes is not the journalist who distrusts AI. She is the journalist whose pieces survive scrutiny. The engineer who traces the reasoning is not the engineer who second-guesses every recommendation. He is the engineer whose changes improve performance. The analyst who runs the omission check is not the analyst who is paralyzed by what she might have missed. She is the analyst whose director trusts the brief.

---

### Translate before you move on — produce the Verification Protocol and open your DESIGN.md

Priya had three failures in five days: a fabricated quote (fact), a wrong revenue-recognition premise (reasoning), and an omitted customer concentration (omission). In your field, what is the failure-mode landscape? Where do the fact errors most often hit? Where do the reasoning errors hide? What kind of omission is the omission that ends careers in your domain?

For a clinician: a fabricated drug-interaction reference (fact), a treatment plan resting on an unstated renal-function assumption (reasoning), and the medication-history detail the chart didn't surface prominently (omission). For a software engineer: an API endpoint that doesn't exist (fact), an optimization analysis built on an unstated assumption about data distribution (reasoning), and the production-load case the analysis never modeled (omission). For a lawyer: a fabricated precedent (fact), an analogy resting on an unstated jurisdictional assumption (reasoning), and the case from 2019 that goes against the argument's core analogy (omission). The specific failures are field-specific. The layer structure is invariant.

**The Domain Verification Protocol — Chapter 6 Portfolio Artifact (Layer A template + Layer B customization, framework):**

Build it. For each of the four layers, write the field-specific checks: what specifically you verify at each layer for your typical work. Then map your role's tasks to the four tiers — which tasks live at Trivial, Operational, External, High Stakes — with named examples. Then write the time-budgeted checklist for each tier in your work.

Save as `portfolio/06-verification-protocol.md`. Three to four pages. The protocol is a Layer A framework (four layers, four tiers — same structure for everyone) filled with Layer B content (your domain's specific checks at each layer for each tier). A future reader sees not just that you have a method, but that the method has been adapted to the actual texture of your work.

**Open your DESIGN.md.** This chapter is where your `DESIGN.md` begins — the output-quality constitution that governs what your work has to do to be acceptable in your field, separate from the coding/process discipline in `CLAUDE.md`. The first thing to put in `DESIGN.md`:

1. *The verification standard for your domain.* Specifically, what quality bar must any output you ship clear before it leaves your hands?
2. *The voice and register your domain expects.* This is not just stylistic. It is what tells the reader of your output that the work was done by someone in your field, to your field's standard.
3. *The accessibility or audience criteria your outputs must meet.* Different in every field — readability levels, jargon norms, evidence standards, source-attribution conventions.

Save as `portfolio/DESIGN.md`. Three sections to start. We will return in Ch 7 (Diligence), Ch 11 (Agency stakeholder-model criteria), and Ch 12 (HITL protocol design) to add more.

**Update your CLAUDE.md** with the chapter's operational rule: *On any external-tier output, I run all four verification layers before shipping. The omission layer is the one I most often skip and the one most expensive to miss; I run it deliberately, with the domain knowledge only I bring.*

---

*What would change my mind.* If I saw fluent practitioners producing reliable external-stakes work while skipping the framing and omission layers consistently — and the failure rate stayed low across many cases and many domains — I would weaken my insistence on four layers. The pattern I observe is the opposite. The framing and omission layers are the ones that catch the failures that matter most, and they are the ones most practitioners skip.

*Still puzzling.* The omission layer resists pedagogy. It requires domain knowledge to run, and no chapter can install domain knowledge. All I can do is name the move and trust that the reader's accumulated understanding of her own domain does the work. I would like a sharper way to teach this. I do not have one yet.

---

> **Going deeper — *Computational Skepticism for AI***
>
> Three threads from this chapter have formal treatment in the advanced volume:
>
> - **The confidence-correctness gap** is grounded in calibration metrics — Brier score, Expected Calibration Error (ECE), reliability diagrams — that quantify exactly how much you should distrust a model's stated confidence in a given deployment. The advanced book also covers subgroup calibration: the same model may be well-calibrated on average but badly miscalibrated on a particular population, which the global metric will hide. See *Computational Skepticism for AI*, **Chapter 2 — Probability, Uncertainty, and the Confidence Illusion** and **Chapter 12 — Communicating Uncertainty**.
>
> - **The omission layer** — the layer most often missed and most expensive to fail at — is, in the advanced book, called a **silent failure**: the system produces output indistinguishable from accurate reporting while measuring something different from what users believe it is measuring. The chapter that opens the deeper book uses Ron Johnson at J.C. Penney as an extended example of an omission failure that cost $4.3B. See *Computational Skepticism for AI*, **Chapter 1 — The Skeptic's Toolkit** and **Chapter 6 — Model Explainability**.
>
> - **The four-tier verification protocol** is the practitioner version of the deeper book's *defended choice* deliverable — calibrating the verification effort to the stakes is the same discipline engineers use to defend a fairness-metric or a robustness portfolio to a regulator.

---

### A note about AI

Discernment is the capacity to evaluate the model's output. Most failures of fluent practice are failures here.

Where the model genuinely helps: producing the strongest critique of its own previous output, on request. The critique will be weaker than a hostile human reader's, but it surfaces flaws you missed.

Where the model does damage: validating its own output when asked *is this good?* Models are agreeable. The question is structurally biased toward yes. Replace it with *what is wrong with this?* and the discipline of discernment becomes easier to sustain.

The rule: do not ask the model whether its output is correct. Ask what would make it wrong.

---

## LLM Exercise — Chapter 6: Discernment

**Project:** AI Fluency for [Your Role] — Your Verification Protocol

**What you're building this chapter:** Two pieces. (a) The **Domain Verification Protocol** — four layers customized to your field, plus the four tiers mapped to your role's tasks, plus a time-budgeted checklist per tier. (b) The opening draft of your **`DESIGN.md`** — three sections naming the verification standard, the voice and register, and the audience criteria your domain expects. Plus one new rule added to your `CLAUDE.md`.

**Tool:** Claude Project (continue — your full portfolio so far is in context) + your file system (`portfolio/`).

---

**The Prompt:**

```
Continuing my AI Fluency portfolio. My Role Dossier, Worked Loop Log,
Practitioner Profile, Specification Library, Adversarial Conversation
Log, PROJECT.md template, and CLAUDE.md are in the Project context.

Botspeak Chapter 6 watches Priya — sixteen months past Chapter 0 —
have three failures in one week: a fabricated quote (fact error), an
analysis built on a wrong revenue-recognition premise (reasoning
error), and a profile that accurately stated everything except the
40%-of-revenue customer concentration that mattered most (omission
error). The chapter introduces the FOUR VERIFICATION LAYERS (fact /
reasoning / framing / omission) and the FOUR-TIER PROTOCOL calibrated
to stakes (Trivial / Operational / External / High Stakes).

For Chapter 6's portfolio artifacts, do three things.

TASK 1 — DRAFT MY DOMAIN VERIFICATION PROTOCOL.
Help me build the four-layer protocol customized to my field. For
each layer:

- LAYER 1 (FACT). What specific kinds of factual claims appear in my
  work? What's the verification move for each? (For a clinician:
  drug-interaction references, clinical citations, dosage figures.
  For a software engineer: API endpoints, library versions, function
  signatures. Your domain has its own list.) For each kind, where
  do I check?
- LAYER 2 (REASONING). What unstated premises do models most often
  smuggle in for tasks in my field? (Revenue-recognition conventions,
  units of measurement, jurisdictional defaults, regulatory regimes,
  patient-history assumptions.) For each common one, what's the
  one-question check that catches it?
- LAYER 3 (FRAMING). What are the 2–3 alternative framings I should
  always consider for the kinds of analytical work I do? Some
  domains have a small number of standard organizing principles
  (e.g., in finance: by risk type vs by time horizon vs by
  counterparty). Name the ones in your role.
- LAYER 4 (OMISSION). What does the senior person on my desk always
  ask first about my kind of analysis that the model never volunteers?
  Name 3–5 things. These are the omissions that matter in my field.

Then map my role's tasks to the four TIERS:
- Tier A (Trivial) — examples + why
- Tier B (Operational) — examples + what makes them operational
- Tier C (External) — examples + the external-stakeholder relationship
- Tier D (High Stakes) — examples + the irreversibility / safety /
  regulatory factor

For each tier, produce a copy-paste checklist (time-budgeted) a reader
can run before shipping. Be honest about time cost.

Save as `portfolio/06-verification-protocol.md`.

TASK 2 — OPEN MY DESIGN.md.
Draft the first three sections of my personal DESIGN.md — the
output-quality constitution governing what my work has to do to be
acceptable in my field:

1. THE VERIFICATION STANDARD FOR MY DOMAIN. What quality bar must
   any output I ship clear before it leaves my hands? Specific
   enough that a reviewer could check.

2. THE VOICE AND REGISTER MY DOMAIN EXPECTS. Not just stylistic —
   what tells a reader that the work was done by someone in my
   field, to my field's standard? Concrete examples of what fits
   and what does not.

3. THE ACCESSIBILITY OR AUDIENCE CRITERIA. Readability levels,
   jargon norms, evidence standards, source-attribution
   conventions. Specific to my domain.

Save as `portfolio/DESIGN.md`. Note that this is a LIVING document —
we will return in Chapter 7 (diligence components), Chapter 11
(agentic stakeholder-model criteria), and Chapter 12 (HITL protocol
design) to add more sections.

TASK 3 — ADD ONE RULE TO MY CLAUDE.md.
Append the chapter's operational rule, in my own language:
"On any external-tier output, I run all four verification layers
before shipping. The omission layer is the one I most often skip
and the one most expensive to miss; I run it deliberately, with the
domain knowledge only I bring."

Push back if my Tier C checklist runs under 15 minutes or over 90
minutes. Under 15 minutes is probably skipping a layer that matters
for this kind of work; over 90 minutes is a checklist a reader will
skip under deadline pressure. The Tier C checklist's value is in
being run, which means it has to be runnable.
```

---

**What this produces:** Your portfolio gains a new framework file (`portfolio/06-verification-protocol.md`) and a new governing file (`portfolio/DESIGN.md`), plus another rule in your `CLAUDE.md`. The Verification Protocol is the fourth piece of evidence prefiguring the Chapter 8 keystone (the others being the Worked Loop Log, the Specification Library, and the Adversarial Conversation Log). ~3,500–5,000 words across the artifacts.

**How to adapt this prompt:**

- *For your own project:* Resist over-specifying Tier D. Most readers will not deploy at Tier D regularly; making the section feel doable for Tier C is more valuable than making it feel rigorous for Tier D.
- *For ChatGPT / Gemini:* Works as-is.
- *For Claude Code:* Useful only if part of your verification can be partially automated (link-checking scripts, regex sweeps for the kinds of fact-claims you most often produce).
- *For Cowork:* Recommended. Cowork can manage the multi-file split (`06-verification-protocol.md` and `DESIGN.md`) and remind you to update them as later chapters add sections.

**Connection to previous chapters:** Chapter 5 built the Adversarial Conversation Log — iterative push-back during conversation. Chapter 6 builds the structured pass that comes after — the formal verification before shipping. Together they cover the discernment work the practitioner does once the model has produced a draft.

**Preview of next chapter:** Chapter 7 produces the Diligence Framework — what happens when the work recurs. The three drifts (model, context, use-case) plus the four-component framework applied to one specific AI system you currently use or own.

---

## Exercises

### Warm-Up

**1. Map failures to layers.** *(Layer identification | Difficulty: low)*
Return to Priya's three failures — Monday's fabricated quote, Wednesday's wrong revenue-recognition premise, Friday's omitted customer concentration. For each one, name the verification layer that would have caught it and explain in one sentence why the other three layers would not have. Then name the failure type the chapter never explicitly illustrated with a scene — the framing error — and describe in two sentences what a framing failure would look like in a professional context you know.

**2. Explain the confidence-correctness gap.** *(Mechanistic understanding | Difficulty: low)*
Explain in your own words why the confidence of a model's output is not a reliable signal of its accuracy. Your explanation should name: what the model was actually trained to optimize for, why the human confidence heuristic works on human sources, and why that heuristic breaks when applied to model output. Keep it to a paragraph.

**3. The self-interrogation problem.** *(Cross-check logic | Difficulty: low)*
A colleague says: "I asked the model whether its own citation was real, and it said yes, so I didn't bother checking." Name the structural flaw in this approach. Explain why asking a model to verify its own output cannot substitute for external cross-checking, even when the model expresses high confidence in its response.

---

### Application

**4. Run a Layer 2 check.** *(Reasoning verification | Difficulty: medium)*
You receive the following model output evaluating a potential vendor:

> "DataFlow Inc. is a well-established infrastructure provider with a strong track record in enterprise deployments. Their API latency benchmarks consistently rank in the top quartile for the sector. Their pricing model is competitive with the three main alternatives, and their support SLA is industry-standard at 99.9% uptime."

Identify every load-bearing assumption this analysis rests on. Which assumptions are explicitly stated? Which are inferred from phrases like "well-established" or "consistently rank"? Which assumption, if wrong, would most change the conclusion? How would you verify it?

**5. Operationalize the omission check.** *(Layer 4 application | Difficulty: hard)*
You are a junior analyst preparing a market entry brief for a consumer goods company considering expansion into Southeast Asia. The model produces a thorough analysis covering market size, regulatory environment, competitive landscape, and distribution channels. Describe concretely how you would run the Layer 4 check on this output: what domain knowledge would you need to bring, what questions would you ask, and what are the two or three categories of situational fact most likely to be absent but decisive for this specific client?

**6. Assign the tiers.** *(Stakes calibration | Difficulty: medium)*
Assign a verification tier to each of the following and specify which layers you would run. Justify each tier assignment in one sentence.

- A draft agenda for an internal team retrospective
- A summary of a patient's medication history prepared for a specialist handoff
- A competitive analysis included in a pitch deck for a Series B investor
- A code snippet that will be deployed to a production payment processing system

---

### Synthesis

**7. Why layers 3 and 4 are structurally harder.** *(Structural analysis | Difficulty: hard)*
The chapter asserts that framing and omission are the layers most often skipped and most expensive when they fail. Construct an argument for why these two layers are structurally harder to run than fact and reasoning — not just in practice, but in principle. What is the fundamental difference between checking whether a specific claim is true and checking whether the frame was the right frame to use? Your argument should explain why no amount of prompting discipline fully compensates for the structural difficulty of these layers.

**8. The omission layer and domain expertise.** *(Synthesis across chapter | Difficulty: hard)*
The chapter ends with an admitted limit: "The omission layer resists pedagogy. It requires domain knowledge to run, and no chapter can install domain knowledge." Connect this limit to the chapter's opening claim that the three failures happen to non-careless practitioners every week. If the omission layer requires domain knowledge that takes years to build, what does this imply about which practitioners are most at risk, and about what organizational practices might partially compensate for thin domain knowledge on a team? Your answer should engage with the chapter's mechanistic explanation of why the model's training produces omission failures — not just with the practical observation that they happen.

---

### Challenge

**9. Design an operational calibration framework.** *(Framework extension | Difficulty: high)*
The chapter proposes four tiers as a calibration heuristic. Design a more precise alternative — one explicit enough that two analysts on the same team would classify the same deliverable identically without consulting each other. Your framework should specify the variables it weights (blast radius, reversibility, audience, reliability zone, or others), how it combines them into a tier classification, and the decision rule for borderline cases. Then identify two classification cases your framework still cannot resolve cleanly, and explain what additional information would resolve them.

**10. Challenge the layer independence assumption.** *(Framework critique | Difficulty: high)*
The chapter treats the four layers as independent — you can run them separately, skip some, combine them in any order. Make the strongest case that they are not independent: specifically, that a framing failure at Layer 3 systematically causes fact errors at Layer 1 that look like pure citation hallucinations but are actually downstream consequences of the wrong frame. If this case is correct, what does it imply about the order in which layers should be run? What does it imply about how the tier protocol should be revised? Your argument should be grounded in at least one concrete professional scenario.

---

## AI Wayback Machine

The ideas in this chapter didn't appear from nowhere. **Abraham Wald** solved one of the Second World War's most consequential omission problems before most statisticians had named the error type: when the U.S. military asked him where to add armor to its bombers, he pointed to the parts with *no* bullet holes — the planes with holes in those spots never made it back to be counted. The thing missing from the data was exactly the thing that mattered. Here's a prompt to find out more — and then make it better.

![Abraham Wald, c. 1940s. AI-generated portrait based on a public domain photograph (Wikimedia Commons).](images/abraham-wald.jpg)
*Abraham Wald, c. 1940s. AI-generated portrait based on a public domain photograph.*

**Run this:**

```
Who was Abraham Wald, and how does his bombers-with-no-holes argument
connect to Layer 4 of verification — the omission layer — where the
most consequential failures hide in what the model did not say? Keep
it to three paragraphs. End with the single most surprising thing
about his career or ideas.
```

→ Search **"Abraham Wald"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain "survivorship bias" in plain language, as if you've never seen the term
- Ask it to compare Wald's missing-bullet-hole reasoning to running Layers 3 and 4 (framing, omission) on a market-entry brief
- Add a constraint: "Answer as if you're writing a verification-tier example for a chapter on Discernment"

What changes? What gets better? What gets worse?
# Chapter 7 — Diligence
*A process does not hold still. The model changes. The world changes. The use case expands. Any of these, unmonitored, can turn a well-designed workflow into a broken one while every individual actor in the system behaves exactly as they did on day one.*

---

Here is a question worth sitting with before we get into the machinery.

When a process goes wrong — not spectacularly, not all at once, but slowly, over months, in ways nobody noticed — who is responsible?

The answer, in most organizations that have added AI to a recurring workflow, is: everyone and no one. Everyone had a role. No one owned the outcome. And the reason that answer keeps recurring is not bad luck, not malice, not negligence in any particular person's individual actions. It is a structural problem — a predictable consequence of how AI gets introduced into ongoing work — and it has a tractable fix that almost nobody has put in place.

That fix is what this chapter is about. But I want to start with the mechanism, because you cannot defend against what you cannot name.

---

Priya's publication spent February setting up an AI-assisted audience-segmentation tool. The tool helped Climate-desk editors decide which stories to commission based on what audience segments were reading what — surfacing the patterns in engagement that editors otherwise had to infer by feel. The setup team validated it against the previous quarter's Climate readership data. The recommendations looked indistinguishable from what the senior commissioning editor would have suggested, slightly faster and more consistent. The team approved it. The tool went into the desk's weekly commissioning rhythm.

Nine months later, in early November, Priya — now seventeen months past Chapter 0 and helping oversee the desk's AI deployments — is reviewing the tool's commissioning recommendations from the last quarter for an entirely unrelated reason. She is looking for examples for a conference talk on editorial AI. Reading the recommendations side by side, she notices something she had not noticed receiving them one week at a time. The tool has been systematically deprioritizing story candidates whose initial engagement signal comes from lower-income and rural readership clusters — flagging them as "low projected reach" — at a rate that is too consistent to be noise.

The audit she triggers takes another two weeks. The finding: the tool has been quietly under-weighting stories that disproportionately serve those audiences. The editorial team has explicit commitments around exactly that, written into the desk's editorial values document. The drift is not a single decision anyone made. It is a structural failure that compounded across months.

Priya wants to know who introduced the drift. The investigation finds that nobody did. Nobody changed the tool. Nobody changed the rubric. Nobody changed the workflow. What actually happened was all of the following, simultaneously, slowly:

In May, the segmentation vendor pushed an update. The update changed the way the model weighted engagement signals from short-form readers versus long-form readers. The change was small. It was not announced in any detail. The new weighting happened to be more sensitive to a signal that, in this publication's reader pool, correlated with income bracket and geographic concentration. Nobody chose this. Nobody noticed it. The model just got slightly different, and the difference accumulated. That is model drift.

In March, the publication had completed an acquisition that expanded its audience into two new metropolitan markets — and a viral piece had broadened the readership beyond the urban-coastal profile the tool had been validated against. The pool of readers hitting the segmentation tool in October looked structurally different from the pool in February. The rubric had been designed and validated against February's pool. Nobody re-validated it against October's. The assumptions baked into the specification no longer matched the world the specification was operating in. That is context drift.

In July, an editor on the Politics desk — who had not been part of the original Climate setup — started using the tool to inform her own commissioning decisions. The original tool had been designed for Climate-desk reader engagement patterns. The criteria for Politics commissioning are different — the engagement signals correlate with different reader behaviors. The tool was applying Climate-tuned criteria to Politics-desk story candidates, scoring them on a frame the tool was never built for. Nobody had re-spec'd the tool for the new desk. Nobody had told the July editor that the tool was not designed for this use case. That is use case drift.

Three drifts. Each one, on its own, might have been small enough to miss. Together, compounding over nine months, they broke the process in a way that harmed real coverage decisions and real readers. And not one of them required anyone to make a wrong decision.

*Figure 7.1*

This is the structural fact about recurring AI-assisted work that Chapters 1 through 6 did not fully prepare you for: the process does not hold still. The model changes. The world changes. The use case expands. Any of these, unmonitored, can turn a well-designed workflow into a broken one while every individual actor in the system behaves exactly as they did on day one.

---

Priya, faced with the finding, has a second problem on top of the first. Not only did the process fail — she cannot find the locus of the failure in any single person's decision. And when she tries to change the process going forward, she discovers she cannot find who owns it.

This is not an accident. There are three mechanisms that routinely obscure accountability when AI is in a recurring workflow, and understanding them is what makes it possible to design against them.

The first is process laundering. When an AI produces an output and a human approves it, accountability for the output distributes in a way that lets everyone tell a true and exculpatory story. The human approver says: the AI produced it; I just reviewed it. The AI vendor says: we provide a tool; the customer is responsible for appropriate use. The original setup team says: we set it up correctly in February; what happened after wasn't our responsibility. Every statement is accurate. Together, they produce a situation in which no one is accountable, even though every output had a human signature somewhere in its chain.

You will recognize process laundering in any post-incident conversation where every participant can give a complete, accurate account of their own role and still leave the cause of the problem unexplained. The fix is not to assign blame retroactively. The fix is to name, in advance, a single accountable human for each significant recurring AI-assisted process — the person whose job includes monitoring whether the process is still working, not just using it.

The second mechanism is tool diffusion. When a tool works, it spreads. The Politics-desk editor in July picked up the segmentation tool because it seemed useful and nobody told her not to. This is a rational thing for an individual to do. The aggregate effect, across a team or an organization, is that the original specification loses authority. New users are operating with partial, possibly garbled, possibly outdated understandings of what the tool was designed for. The original setup team may not know who is using the tool now. The use case has evolved without the specification evolving with it.

The fix is not to lock down tools or require formal approval for every extension. The fix is to maintain a living document for each significant AI-assisted process: who set it up, what it was designed for, what it was explicitly *not* designed for, who is currently using it, and who to talk to before extending it to a new use case. The document is cheap to maintain and expensive not to have.

The third mechanism is the verification gap. In most workflows, checking whether the process is still working is someone's responsibility in general and no one's in particular. The Climate-desk editors assumed the setup team was monitoring for problems. The setup team assumed the editors would say something if they noticed an issue. The result is that systematic verification doesn't happen — only reactive verification, after something goes wrong loudly enough to force attention, or after someone like Priya happens to look across a quarter of recommendations at once.

The verification gap closes only one way: scheduled checks, with dates and owners, on someone's calendar. Not an aspiration. Not a norm. A calendar entry that recurs and has a name attached to it.

*Figure 7.2*

---

There is a protocol that defeats all three mechanisms. I want to give it to you in the most concrete terms I can, because the value is not in the theory but in actually running it.

The first component is a documented specification. A document that answers: what does this process do, on what inputs, producing what outputs, for what use case, validated against what, approved by whom. The document is accessible to everyone who uses or manages the process. When a new colleague joins and starts using the tool, she reads the spec first. When the use case changes — when someone wants to extend the tool from Climate-desk commissioning to Politics-desk commissioning — the spec is updated formally, not silently, and the update triggers re-validation.

Without the documented specification, you do not know what the process was supposed to do, which means you have no baseline to check drift against. The spec is the foundation.

The second component is drift checks on a schedule. A set of known inputs — a test set, a benchmark, a sample of historical cases where you know what the right output is — that you re-run against the process on a fixed cadence. Once a month, once a quarter, calibrated to the stakes and the pace of change.

The drift check answers: has the process changed? Are outputs still meeting the criteria the workflow depends on? If outputs have changed, what changed — the model, the data, the use case? The answers get documented. If the drift is small and benign, you note it and continue. If the drift is significant, you investigate before the accumulation turns into an audit finding.

The third component is outcome audits. A periodic look at the downstream consequences of the process — not just the immediate outputs, but the outcomes those outputs produce — broken down by whatever attributes matter for fairness, accuracy, and quality.

For the segmentation tool, this meant: look at commissioning outcomes by reader-demographic cluster, by region, by income bracket, by story type. Are some groups of readers systematically having their stories deprioritized? Is the distribution shifting over time? The outcome audit is the check that model-drift-on-test-sets can miss: a model might produce the right outputs on your benchmark while producing different outputs on the actual distribution it operates on. The outcome audit catches that.

Priya's publication should have been running this audit monthly. They were not. When the audit eventually happened, it was forced by Priya happening to look across a quarter at once — which is the worst time for an audit, because by then the drift had compounded for nine months.

The fourth component is a named accountable human. One person whose job description includes maintaining this process — not just using it. The person whose name is in the spec as the process owner. The person who has the drift checks and outcome audits on their calendar. The person who is on the hook when the process fails, and who therefore has a personal incentive to make sure it does not.

The named owner does not have to be the most senior person in the room. She has to be someone with the time, the access, and the authority to actually do the work. She has to know she owns it. And the organizational structure has to treat ownership as a real accountability, not a nominal one.

Four components. None of them is technically sophisticated. Each of them is, in most organizations, missing for most AI-assisted processes.

| Component | The question it answers | What it prevents | Minimum cadence | Who owns it |
|---|---|---|---|---|
| **Documented specification** | What does this process do, on what inputs, producing what outputs, for what use case, validated against what, approved by whom? | Tool diffusion — secondary users extending the process to cases it was never designed for | Update on any change to inputs, outputs, use case, or model | Process owner; stored where every user can find it |
| **Drift checks on a schedule** | Has the process changed? Are outputs still meeting the criteria the workflow depends on? | Model drift and context drift accumulating undetected between cycles | Monthly for high-stakes; quarterly minimum | Named process owner; calendar entry, not an aspiration |
| **Outcome audits** | Are the downstream consequences of this process still acceptable — broken down by the attributes that matter for fairness, accuracy, and quality? | Silent failures that pass benchmark tests but harm real-world subpopulations | Quarterly; monthly in regulated domains or where the population shifts | A reviewer *other than* the process owner |
| **Named accountable human** | Who is on the hook if this process fails — and who therefore has a personal incentive to make sure it doesn't? | Process laundering and the verification gap — the structural conditions in which everyone can give an accurate account of their own role and the cause of failure still goes unexplained | Reviewed at any personnel change or scope expansion | One named person with a named backup and a named escalation path |

---

I want to make a stronger claim than "diligence helps you catch problems early," because while that is true, it undersells what the four components actually do.

Diligence is primarily about defensibility.

Here is what I mean. When a process fails — and processes fail; the question is when, not whether — the consequential question is not who to blame. The consequential question is: what do we change, and how quickly, and how do we address the harm that already happened? Getting good answers to those questions requires knowing what the process was supposed to do, how it deviated, when the deviation started, and why nobody caught it.

A process running the four diligence components can answer all of those questions. Here is the spec. Here is the scheduled check that should have caught the drift in June. Here is what we found when we ran it — and here is why we did not flag it, which is a solvable problem. Here is the named owner who will lead the remediation.

A process without the four components produces the situation Priya walked into: an audit that cannot identify the mechanism cleanly, a team that cannot distribute accountability without finger-pointing, and an editorial leadership that either reprimands someone for a structural problem or reprimands nobody and leaves the organization with the impression that nothing was wrong.

The four components make the process accountable in a way that protects the people in it. Diligence is not a safeguard against failure. It is a safeguard against organizational confusion when failure happens — and confusion, in my experience, causes more lasting damage than the failure itself.

---

Most of what I have described assumes you have some authority over the process — that you are setting it up, or managing it, or in a position to propose how it should be maintained.

You may not be. You may be one of many users of a process you did not design and do not officially own.

The four components are still available to you, partially. You can document your own use of the tool — what you use it for, what you have learned about its limits, what cases you have found where it performs unexpectedly. You can escalate that documentation to whoever does own the process. You can decline to extend a tool to use cases you know it was not designed for, and explain why.

What you cannot do is force accountability on a process that the organization has not structured to receive it. This is a real constraint. The chapter is not pretending otherwise. What I would say is that the political moment for proposing the four-component protocol is usually after a near-miss, not after everything is running smoothly. Small failures are good opportunities. Large failures are bad ones. Get the protocol in place during a small failure, if you can.

And make sure that your own name on a process is on a process you are diligently maintaining. The accountability cuts both ways: the four components protect you as well as holding you to account.

Priya, after the audit, ended up the named accountable human for the segmentation tool's redesign and ongoing oversight. The role was new at the publication and somewhat ad hoc. She negotiated for one half-day every two weeks formally allocated to the work, with a recurring check on her calendar. The publication did not have a budget category for it. Her editor approved the time anyway, because the audit had concentrated minds.

---

The three drifts I named — model, context, use case — are not exhaustive. Data drift, where the data the process ingests changes character over time, is related to context drift but distinct; a workflow processing reader feedback will behave differently in a quarter when sentiment is unusually polarized than in a normal quarter. Regulatory drift, where the legal environment shifts in ways that change what the process is permitted to do, is real and consequential in domains like hiring, lending, healthcare, and — increasingly — content recommendation systems.

The four-component protocol handles all of these, because the protocol is not tuned to any specific drift type. The documented specification records what the process was designed for. The drift check detects when outputs are changing. The outcome audit detects when consequences are changing. The named owner decides what to do about it. The mechanism does not care which drift triggered the check.

The next chapter assembles everything from the first half of the book — specification, delegation, conversation, discernment, verification, diligence — into a single narrated workflow. You will see how the pieces fit together in real time, and where the feedback loops are that the chapter sequence made look linear.

---

### Translate before you move on — produce the Diligence Framework Applied

Priya's case was a publication's audience-segmentation tool drifting across model, context, and use case over nine months until the demographic-deprioritization pattern surfaced. In your field, what is the equivalent? Pick one AI-assisted system you currently use, own, or work alongside — and walk it against the framework.

For a clinician: the AI-assisted triage tool in the ED. For a software engineer: the AI-assisted code review or test generation tool the team has been using. For a marketing manager: the audience-segmentation or campaign-targeting tool the firm relies on. For a teacher: the AI-assisted grading or plagiarism-detection tool. For a research scientist: the AI-assisted literature-search or analysis pipeline. For a lawyer: the AI-assisted discovery or contract-review tool. The specific tool varies. The pattern — *a system that is recurring, has multiple users, was validated for one context, may have drifted across model, context, or use case* — is invariant.

For self-study readers without an organizational AI system in their direct work, the substitute is to pick a public AI system in your field and analyze it as if you had inherited responsibility for it. The analysis is weaker as evidence but valid as practice.

**The Diligence Framework Applied — Chapter 7 Portfolio Artifact (Layer A template + Layer B application, framework):**

Build it. For one specific AI-assisted system in your work (or one you analyze from the outside), walk the four-component protocol:

1. *Documented specification.* If one exists, attach it (or excerpt it). If not, draft what it should say.
2. *Drift checks on a schedule.* Name the cadence, the procedure, the owner, the calendar item. If no checks are currently being run, draft what the schedule should be.
3. *Outcome audits.* Name the metric, the cuts, the threshold for escalation, the reviewer (must be someone other than the owner). Run one audit if you can.
4. *Named accountable human.* Name the person — or, if no one currently owns the process, name who should own it and what authority they would need.

Plus a fifth section: *Drift assessment.* Has model drift, context drift, or use case drift happened to this system, that you can detect from where you sit? Document what you find.

Save as `portfolio/07-diligence-framework.md`. Three to four pages. The framework is a Layer A template (the four components are the same structure for every reader) filled with Layer B application (your domain's specific system, your specific cadence, your specific outcome metric). A future reader sees how you apply governance to recurring AI work, not just how you generate single outputs.

**Update your DESIGN.md.** Add a section on the maintenance and ownership criteria your domain expects for any AI-assisted system that runs in your work. Specifically: what does ownership look like in your field, what does the outcome audit measure, and what triggers escalation to a senior reviewer. This section pairs with the verification standard from Ch 6 to form the quality side of `DESIGN.md`. The ongoing-stewardship side.

**Update your CLAUDE.md** with the chapter's operational rule: *No recurring AI-assisted process I am part of runs without a documented spec, a scheduled drift check, an outcome audit, and a named accountable human. If any of those four is missing, I am part of the verification gap.*

---

**What would change my mind.** If a high-quality empirical study showed that organizations running the four diligence components for a year produced no fewer audit findings than organizations that did not — that the components are decorative rather than functional — the chapter is wrong about the mechanism. The pattern I have observed runs the other direction. Organizations with the components catch problems earlier, including problems they had no prior reason to anticipate. But the observation is informal.

**Still puzzling.** I do not have a clean answer to who pays for diligence work in organizational terms. The work is real. It takes time. Most organizational budgets do not have a line item for it. The fluent practitioner often ends up doing the diligence work on top of her assigned role rather than as a recognized component of it — as Priya does after the segmentation-tool audit. I do not have a fix for that.

---

## Exercises

### Warm-up

**1. Name the drift.** For each scenario below, identify which drift type is operating (model drift, context drift, use case drift) and write one sentence explaining the mechanism. *(Tests: ability to distinguish drift types in context.)*

- A company uses an AI tool to flag potentially fraudulent transactions. Six months in, the tool's false-positive rate doubles. Investigation reveals the vendor silently updated the underlying model in the prior quarter.
- A legal team deploys an AI contract-review tool trained on US contracts. A new analyst begins running European vendor agreements through it without telling anyone.
- An AI customer-sentiment tool was validated against reviews from a normal business quarter. It is now running during a product recall, when customer sentiment is structurally angrier than the validation set.

**2. Process laundering, identified.** Write the three exculpatory statements — one each from the human approver, the AI vendor, and the original setup team — that together produce the accountability gap in the segmentation-tool case. Then write one sentence explaining why each statement is both true and insufficient on its own. *(Tests: retention of the process laundering mechanism and its structural character.)*

**3. The four components, applied.** You are setting up a recurring AI-assisted process: a weekly summary of customer support tickets, delivered every Monday to the product team. For each of the four diligence components, write two to three sentences describing concretely what it looks like for this specific process — not a restatement of the general definition, but the actual artifact, schedule, or role you would create. *(Tests: ability to instantiate abstract components into a specific workflow.)*

---

### Application

**4. Diagnose the segmentation case.** Priya's publication was running the four-component protocol incompletely — some components were present in weakened or implicit form, others were absent entirely. For each of the four components, describe whether it was present, absent, or degraded in the publication's workflow as described in the chapter. For each absent or degraded component, describe specifically what having it in place would have changed about the outcome. *(Tests: ability to apply the four-component framework as a diagnostic tool, not just a setup checklist.)*

**5. Write a living document.** You are the process owner for an AI tool that generates first-draft project status reports from a shared project-management database, used by eight project managers across two teams. Write the living document for this process. It should include: what the process does and does not do, who set it up and when, who is currently using it, what the process was validated against, what the explicit not-designed-for cases are, who to contact before extending it, and the name and calendar cadence of the scheduled drift check. Aim for one page. *(Tests: ability to produce the actual artifact, not just describe it.)*

**6. Blast radius by drift type.** The chapter claims that the blast radius of a specification mistake is proportional to how many times the specification runs before someone catches the problem. Apply this claim specifically to context drift. Describe a scenario in which context drift accumulates silently for six months in a high-stakes domain (healthcare, lending, hiring, content moderation, or safety — your choice), estimate the blast radius, and identify the specific diligence component that would have caught the drift earliest if it had been in place. *(Tests: integration of the blast-radius framing from Chapter 1 with the drift mechanics introduced here.)*

---

### Synthesis

**7. The defensibility argument.** The chapter's central claim is that diligence is primarily about defensibility, not early detection. Explain the difference between those two purposes. Then construct a scenario in which the four components catch no problems for a year — the process runs cleanly — but their presence still produces a meaningful organizational benefit. Your scenario should make the defensibility argument concrete rather than abstract. *(Tests: ability to hold the chapter's strongest claim and reason from it rather than from the more obvious early-detection framing.)*

**8. Accountability without authority.** The chapter acknowledges a real constraint: a practitioner who is one of many users of a process she did not design cannot force accountability on a process the organization has not structured to receive it. Describe a specific situation in which this constraint is in play. What can the practitioner actually do within the constraint? What should she escalate, to whom, and when? What should she refuse to do even if instructed? *(Tests: integration of the accountability argument with the organizational-reality section — reasoning about what diligence looks like when you do not own the process.)*

---

### Challenge

**9. The verification gap as a design problem.** The chapter says the verification gap closes only one way: scheduled checks with dates and owners on a calendar. Make the strongest possible argument against this claim — identify a scenario in which calendar-based verification would fail to catch a drift that a different detection mechanism would have caught earlier. Then explain what that scenario implies about how the four-component protocol should be designed, without abandoning the protocol's core logic. *(Tests: ability to stress-test the chapter's claims and reason about their limits.)*

**10. Regulatory drift and the four components.** The chapter names regulatory drift as a real risk in hiring, lending, healthcare, and content recommendation, but does not fully develop it. Choose one of those domains. Describe a plausible scenario in which a change in the legal environment turns a compliant AI-assisted process into a non-compliant one. Identify which of the four diligence components is best positioned to catch this drift, explain what it would need to look like in practice in that specific domain, and name what organizational role or function would need to be involved that might not currently be part of a typical AI process-ownership structure. *(Tests: ability to extend the framework into a domain-specific context where the standard instantiation of the components is insufficient.)*

---

### A note about AI

Diligence is the capacity to verify before shipping. The cost of skipping diligence is hidden in the moment and unrecoverable later.

Where the model genuinely helps: producing a checklist of verifications appropriate to the task and walking through each one with you. The checklist is useful even when generic, because it makes the verification explicit.

Where the model does damage: performing the verifications for you and reporting that the work passed. The model cannot run your code, query your database, or check your facts against the world. Its report of passing is not evidence of passing.

The rule: the model can structure the verification. The verification itself has to be done against the world, not against the model's claims about the world.

---

## LLM Exercise — Chapter 7: Diligence

**Project:** AI Fluency for [Your Role] — Your Diligence Framework

**What you're building this chapter:** The **Diligence Framework Applied** — the four-component protocol walked against one specific AI-assisted system in your work (or analyzed from the outside if you have none in your direct work). Plus an update to your `DESIGN.md` on maintenance and ownership criteria. Plus one new rule in your `CLAUDE.md`.

**Tool:** Claude Project (continue — your portfolio so far is in context) + your file system (`portfolio/`).

---

**The Prompt:**

```
Continuing my AI Fluency portfolio. My Role Dossier, Worked Loop Log,
Practitioner Profile, Specification Library, Adversarial Conversation
Log, Verification Protocol, PROJECT.md template, CLAUDE.md, and
DESIGN.md (opened in Chapter 6) are in the Project context.

Botspeak Chapter 7 watches Priya — seventeen months past Chapter 0 —
discover that the publication's audience-segmentation tool has been
quietly deprioritizing coverage of lower-income and rural readers for
nine months. Three drifts compounded: a May vendor model update
(model drift), a March acquisition that broadened the reader pool
(context drift), and a July Politics-desk editor who picked up the
tool (use case drift). Three mechanisms obscured accountability:
process laundering, tool diffusion, verification gap. The chapter
introduces the FOUR-COMPONENT DILIGENCE PROTOCOL: documented spec,
drift checks on a schedule, outcome audits, named accountable human.

For Chapter 7's portfolio artifact, do three things.

TASK 1 — APPLY THE FOUR-COMPONENT PROTOCOL TO ONE SYSTEM.
Pick one AI-assisted system I currently use, own, or work alongside.
If I don't have one in my direct work, pick a public AI system in my
field and analyze it as if I had inherited responsibility for it.

Walk the four components:

1. DOCUMENTED SPECIFICATION. What does this system do, on what inputs,
   producing what outputs, for what use case, validated against what,
   approved by whom? If a spec exists, attach or excerpt it. If not,
   draft what it should say.

2. DRIFT CHECKS ON A SCHEDULE. Name the cadence (weekly / monthly /
   quarterly). The procedure (specific re-run, comparison, sample
   review). The owner. The calendar item. If no checks are currently
   being run, draft what the schedule should be.

3. OUTCOME AUDITS. Name the metric (what to measure). The cuts (by
   what demographic / category / use case). The threshold (what
   triggers escalation). The reviewer (must be someone OTHER than
   the process owner). Run one audit if I can — even a back-of-the-
   envelope one — and report what it shows.

4. NAMED ACCOUNTABLE HUMAN. Name the person. If no one currently
   owns the process, name who should own it and what authority they
   would need. Include backup and escalation path.

5. DRIFT ASSESSMENT. Has model drift, context drift, or use case
   drift happened to this system, that I can detect from where I
   sit? Document what I find — be willing to say "I cannot tell from
   my vantage; here is what I would need to know."

Save as `portfolio/07-diligence-framework.md`.

TASK 2 — UPDATE MY DESIGN.md.
Add a section on maintenance and ownership criteria my domain
expects for any AI-assisted system in my work:

- What ownership looks like in my field (a specific role, a specific
  set of responsibilities, a specific reporting structure)
- What the outcome audit measures (specific to my domain — accuracy
  by subpopulation, fairness by demographic, calibration by use
  case)
- What triggers escalation to a senior reviewer

Append this as a new section in `portfolio/DESIGN.md`. DESIGN.md is
a living document — Chapter 11 (stakeholder model criteria for
agentic systems) and Chapter 12 (HITL protocol design) will add
more.

TASK 3 — ADD ONE RULE TO MY CLAUDE.md.
Append the chapter's operational rule: "No recurring AI-assisted
process I am part of runs without a documented spec, a scheduled
drift check, an outcome audit, and a named accountable human. If
any of those four is missing, I am part of the verification gap."

Push back if my Drift Assessment section says "I cannot detect any
drift." That answer is almost certainly underspecified — either the
system is genuinely well-governed (rare), or I have not looked at
the right cuts (more common). Press on which cuts I have not
examined and which I would need access to.
```

---

**What this produces:** Your portfolio's seventh framework artifact and a meaningful update to your `DESIGN.md`. The Diligence Framework Applied is the artifact that documents your capacity to govern an AI-assisted system over time, not just produce single outputs. ~3,000–4,000 words across the new material.

**How to adapt this prompt:**

- *For your own project:* The framework's value depends on being applied to a real system you actually engage with. A fully hypothetical analysis is structurally weaker than an analysis of a system you have observed.
- *For ChatGPT / Gemini:* Works as-is.
- *For Claude Code:* Useful only if part of the drift check can be scripted (a comparison script that re-runs known inputs).
- *For Cowork:* Recommended.

**Connection to previous chapters:** Chapter 6 built the Verification Protocol — how to check a single output before it ships. Chapter 7 builds the Diligence Framework — how to keep checking when outputs recur. The verification and the diligence cover the lifecycle of an AI-assisted process: from one piece of work to a process that runs.

**Preview of next chapter:** Chapter 8 — the keystone. The End-to-End Case Study. Every Layer A framework and every Layer B deliverable you have built across Chapters 0 through 7 comes together on a single sustained piece of your own work. The case study is the portfolio's gravitational center.

---

## AI Wayback Machine
The ideas in this chapter didn't appear from nowhere. **Walter Shewhart** invented statistical process control in the 1920s — the idea that you set a baseline, measure variation against it on a fixed cadence, and act when deviation crosses a threshold. That is the drift-check component of the four-component protocol, stated in manufacturing terms a century before anyone worried about model updates or use case creep. His deeper claim was that quality cannot be inspected in at the end; it has to be designed in through ongoing monitoring. Here's a prompt to find out more — and then make it better.

![Walter Shewhart, c. 1930s. AI-generated portrait based on a public domain photograph.](images/walter-shewhart.jpg)
*Walter Shewhart, c. 1930s. AI-generated portrait based on a public domain photograph (Wikimedia Commons).*

**Run this:**

```
Who was Walter Shewhart, and how does his work on statistical process
control connect to the idea that diligence in AI work means monitoring
for drift on a schedule rather than inspecting outputs after something
goes wrong? Keep it to three paragraphs. End with the single most
surprising thing about his career or ideas.
```

→ Search **"Walter Shewhart"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain the control chart in plain language, as if you've never taken a quality-engineering course
- Ask it to compare Shewhart's PDCA cycle to the four diligence components in this chapter
- Add a constraint: "Answer as if you're defending the drift-check budget to a skeptical manager"

What changes? What gets better? What gets worse?
# Chapter 8 — Putting the Loop Together

*The recipe cannot tell you what it feels like to cook.*

There is something you cannot learn from a list of steps.

You can read a recipe and understand, individually, what each instruction means. Dice the onion. Reduce the heat. Deglaze with wine. Each step is comprehensible. What the recipe cannot tell you — what no recipe can tell you — is what it actually feels like to cook. The moment where you realize the onion went in too early. The adjustment you make halfway through because the pan is running hot. The part where the whole thing looks wrong for thirty seconds before it comes together.

That gap between reading the steps and doing the thing is where most skill actually lives.

We have spent seven chapters on the steps. This one is about doing the thing.

---

It is 8:47 on a Tuesday morning in Boston and Priya Banksy is opening her laptop in a coffee shop two blocks from her publication's office. She is now a senior content strategist on the Climate desk. Eighteen months have passed since the Tuesday in Chapter 0. The publication kept her on after the correction — barely. The OPT clock kept running. The fabricated Pew survey lives in her memory the way a near-miss on a freeway lives in a driver's: she does not think about it daily, and she will never not think about it.

Her editor has asked for a scoping memo by end of day. The subject is a Series B clean-energy storage company that has been generating an unusual volume of positive coverage across trade press. Is there a real story here, or is the company a well-funded narrative operation? The memo will land in the editor's queue Wednesday morning, where the editorial team will decide whether to commission a 6,000-word investigative feature — a six-week reporter assignment, a photographer, travel budget, legal review — or pass.

Ten hours from now, Priya will send it.

What happens in between is not a demonstration of a framework. It is a person doing work. The framework is inside it, the way the recipe is inside the dish — present, but not the thing you're actually tasting.

This Tuesday is the mirror to the Tuesday in Chapter 0. Same protagonist. Same morning. The arc between the two Tuesdays is the arc the book teaches. Read this chapter knowing the comparison is the point.

---

Priya does not open Claude at 8:47. She opens a blank document.

For twelve minutes she writes about the memo. Audience: her editor, who will read it on her phone between six and eight tonight and use it Wednesday morning to argue for or against commissioning the feature. Length: four pages plus a source appendix. Structure: company snapshot, claimed story, traction-vs-narrative analysis, real reporting hypotheses, risks, recommendation, open questions. Source rule: no claim without a footnote linking to a primary source or a specific conversation from this week. *No exceptions. No "according to industry reports." No statistic without a named dataset.*

Then she writes the success criteria. Her editor reads it in five minutes on her phone, gets the picture, shows up Wednesday with one or two specific questions to ask the reporter who would lead the piece. She does not feel the need to rewrite it.

Then she writes the exclusions. Do not generate citations the AI cannot ground in a specific public document. Do not produce confident growth projections without explicit assumptions and named sources. Do not bury risks inside qualifying paragraphs. Do not produce a recommendation that hedges in both directions. Do not — and this one is underlined in her notes — pull anything from the company's own press kit as if it were independently verified.

Twelve minutes. Everything that follows runs on top of those twelve minutes.

The reason to write the specification before opening the tool is not procedural. It is that the tool will answer whatever question you actually ask, and if you do not know what question you are actually asking, you will not notice when the answer drifts. Priya does not need the specification document. She needs the act of writing it — the forcing function that makes her discover, before she has spent four hours working, what she is actually trying to produce.

![A specification document beside a closed laptop — the visual cue that the spec precedes the tool](images/08-putting-the-loop-together-fig-01.png)
*Specification first, tool second*

---

Now she decomposes the memo.

The company snapshot — pulling product description, founding date, prior round sizes, named investors — is mechanical. The model will do this accurately and quickly and Priya doing it herself would teach her nothing she does not already know. She hands it over entirely.

The trade-press synthesis — what has been written, in which outlets, by which bylines, with what framing — is synthesis. The model will gather, combine, and present from the coverage. Priya will evaluate the output, but more importantly she will check what the synthesis is not telling her — which outlets had financial ties to the company's investors, which bylines have a pattern of cheerleading at this round size, what a skeptic would reach for that the synthesis missed. This is a trap she knows from experience: synthesis tools tell you what the sources say. They cannot tell you what the sources do not say. She handles this by asking the model, explicitly, to steelman the claim *that this is a manufactured narrative*, after producing the main synthesis.

The founder background — public records, prior ventures, named-investor signals — is synthesis of a different kind. Same handling as trade-press: model generates, Priya verifies against primary sources (SEC filings, Crunchbase, the founder's actual prior company outcomes), Priya checks for omissions.

The traction analysis is mixed. Public claims — number of utility contracts, megawatt-hours deployed, customer names — are mechanical, pull-and-verify. The operational reality — what these contracts are actually worth, what the megawatt-hour figure includes and excludes — lives in primary sources she will need to chase down herself.

The risks section is contestable analysis. Reasonable journalists would disagree about which risks make this a story versus which make it a pass. The model can surface candidates she should consider. The judgment about which risks make the *feature* worth six weeks — and how to weigh them against each other — is hers.

The recommendation is accountable judgment. Fully hers. The model will not be on the hook if her publication commissions, spends six weeks on the piece, and finds nothing worth printing. Priya will. The decision belongs to the person who carries the consequence.

She writes a six-line delegation map at the top of her notes file. Not for anyone else. For herself — so that when she is three hours in and the work is flowing, she does not accidentally start handing over the parts she meant to keep.

```markdown
| Task | Who handles it |
|---|---|
| Company snapshot | Model entirely |
| Trade-press synthesis | Model generates — Priya verifies and checks for omissions |
| Founder background | Model generates — Priya verifies against primary sources |
| Traction (public claims) | Model generates — Priya verifies |
| Traction (operational reality) | Priya alone |
| Risks | Model surfaces candidates — Priya judges |
| Recommendation | Priya alone |
```

---

She opens Claude at 9:14. Her first prompt is 320 words.

It includes the audience, the structure, the constraints, the source rule, the exclusions. It asks for only the company snapshot and a first-pass trade-press synthesis — not the whole memo. This is important. Commissioning the full memo in one prompt produces output that is structurally complete and substantively thin. Commissioning in pieces produces output you can actually evaluate, section by section, with enough attention on each piece to catch what is wrong.

The model returns a clean snapshot and a first-pass synthesis. The snapshot looks right. The synthesis includes three statistics Priya does not recognize and one named report she has never heard of. She copies all four into a verification list.

She remembers — she has not forgotten — what happened the last time she did not check a Pew survey she had not seen.

The second prompt: *steelman the claim that the trade-press coverage of this company is a coordinated narrative operation rather than organic interest.* The model produces one. It points at three byline-and-outlet pairs that have written favorably about consecutive funding rounds at this company AND at two other companies sharing one of this company's investors. Priya copies the thesis into her open-questions file. She does not know yet whether it is right. She knows it is the kind of pattern her editor will want her to name in the memo, whether or not she ultimately argues that it explains the coverage.

The third prompt: *what assumptions am I implicitly making by treating this as a clean-energy story rather than a finance-engineering story?* The model surfaces three. One she disagrees with; she notes the disagreement. Two she had not considered; she folds them into her thinking.

By 10:02 she has rough drafts of the company snapshot and trade-press synthesis, a risk-candidate list, and — this is the part that justifies the conversation step — two arguments she did not start the morning holding. The model did not give her the conclusion. It gave her the shape of the problem, which is different and more valuable.

---

Now she verifies.

She opens the three primary sources for the trade-press statistics. One is correct. One is approximately correct but uses 2024 numbers; the model had presented them as current. She updates. One does not exist — the model cited a research firm and a report title that she cannot locate. She finds an actual source for the same underlying claim and replaces the citation.

This is worth pausing on. The model produced a confident-looking citation to a source that was not there. This is not a rare failure mode. It is a common one. The fluent practitioner treats every citation as a hypothesis until verified. The literate user treats them as facts until something breaks.

Priya catches this one in fourteen seconds. Eighteen months ago, she did not catch it at all. The mechanism — model hallucinates source, output looks polished, citation appears to be real — has not changed. What changed is the reflex.

She traces the company's growth-projection reasoning chain. The model had assumed a particular adoption curve to get from current deployments to a five-year forecast. The curve was reasonable but unstated. She makes the assumption explicit in the memo with a sentence that names where the curve comes from. Her editor will be able to poke at it if she wants to.

She asks herself: what other framing would change my view? The model offers vertical (which sectors are adopting) versus geographic (which states are adopting). Her framing is vertical because the publication's audience cares about industry stories. She notes the geographic alternative in the appendix.

She messages her editor on Slack: *anything specific I should look for in this segment that I might miss?* Her editor sends back two pointers. One is a regulatory development she had not considered. She adds a paragraph.

---

Priya gets a sandwich at 12:20. She does not eat at her desk. She sits in the sun and thinks about whether anything she has written is off.

One thing nags. The trade-press synthesis feels like it is treating the coverage volume as suspicious in itself. Not by a lot. But her instinct from prior beats is that volume of coverage and quality of coverage are different things, and the memo is conflating them. Many companies get a lot of coverage that is real. Many companies get less coverage that is bought. The pattern she actually cares about — the one her editor will care about — is not *how much* but *who, with what ties, in what register*.

This is a real Loop step. Decompression is not a break from work. It is the part of work where your intuition catches up with your output. Most fluent practitioners have a version of this — a walk, a sandwich, a coffee away from the screen — that they take specifically to step outside the model's frame. The model produces output with a particular texture and rhythm, and if you stay inside it for six hours straight, you start taking that texture as given. Stepping out lets you hear the thing that was nagging.

---

At 1:14, Priya loops back to her specification.

The thing that nagged crystallizes. Her specification was wrong.

She had written the memo as if her editor wanted a recommendation *on the company*. But what her editor had actually asked on Friday was whether the publication should commit six weeks of a reporter's time to investigate it. That is a different question. In the first framing, the company snapshot and trade-press synthesis are load-bearing — they determine whether the company itself merits a story. In the second framing, those sections are supporting context, and the load-bearing piece is something else entirely: *what would a six-week investigation actually answer, and is the answer worth the time, regardless of whether the company is good or bad*.

The open-questions section is now the most important section in the memo. The recommendation is not *story or no story* but *commission with these four hypotheses to test, or pass and revisit in six months*, with a clear bar for what commissioning would require.

She writes a new specification. She does not throw out the work. She re-anchors it. The sections that survive the change stay; the parts that do not get rebuilt.

The loop-back costs forty minutes. It is the most valuable forty minutes of the day.

This is what a linear chapter sequence cannot show. The Loop is a cycle. Midway through the work, discernment revealed a problem with specification. Priya went back. She did not start over. She rebuilt from the new spec, pulling forward what survived, rebuilding what did not. If she had not taken the sandwich, had not let the intuition catch up, she would have sent a polished memo at 6 PM that answered the wrong question. The editor might not have known why it felt off. She would have known it felt off.

![Figure 8.3 — A timeline of Priya's day](images/08-putting-the-loop-together-fig-03.jpg)

---

The third conversation cycle, against the new specification, runs differently. It is faster and more surgical because the spec is sharper. The model produces, against the new memo, a framework: a list of what would have to be true for a yes-on-feature, framed as testable hypotheses. Priya and the model spend forty-five minutes refining them, narrowing the open questions, holding each candidate question against the bar of *can a reporter answer this in six weeks with a defined source list*.

By 2:55 the recommendation section reads: commission the feature, scoped to four hypotheses, six weeks, with a named legal-review checkpoint at week four.

---

At 3:00 she loops back again — this time not to specification but to a question about the process itself.

She does scoping memos every two to three weeks. This is not a one-off task. It is a recurring kind of task, which means the thing she learned today — confirm with the editor whether the memo is recommending on the subject or on the resource commitment — should not need to be learned again. She makes a note in her template file. The question is now pre-baked. She will not make this specification mistake on the next memo.

This second loop-back is quieter than the first. Nobody watching her would see it. She just updated a file. But this is how fluent practitioners improve — not through retrospectives scheduled on a calendar, but through small notes made in the moment, folded back into the template, so that the next run of the same task starts from a slightly better place.

---

At 4:30 she runs the full verification pass. Three small fact errors. One reasoning gap. One framing alternative folded into the appendix. One hyperlinked citation that resolves to a 404 — she replaces it with the actual source.

At 5:45 the memo is done to her standard.

At 5:48 she writes four sentences.

*AI use note: Claude was used in research and drafting — primarily for trade-press synthesis (sources verified independently, footnotes 4, 9, 12), founder-background scan (verified via SEC filings, LinkedIn, and a 2023 trade publication), and risk-category surfacing (then refined against my own assessment). The four-hypothesis framework in the recommendation was developed in conversation with Claude and then narrowed by me. The recommendation is mine. The verification is mine. Any errors are mine.*

The disclosure does not apologize. It does not pretend the AI did nothing. It does not pretend Priya did everything. It tells the editor exactly what was AI-assisted, exactly what was independently verified, and exactly who is accountable.

This is the AI Use Disclosure. It is the artifact that closes the loop — the moment where the practitioner's name goes on the work, not as a formality but as a genuine claim of ownership over the judgment calls that mattered.

```markdown
| Sentence | What it names | Why it matters |
|---|---|---|
| "Claude was used for trade-press synthesis, founder-background scan, and risk-category surfacing." | What the AI did, specifically | Lets the reader audit which sections carry AI-generated material |
| "Sources verified independently, footnotes 4, 9, 12." | What Priya did to verify | Distinguishes AI-generated from human-verified claims |
| "The recommendation is mine. The verification is mine. Any errors are mine." | Who is accountable | Names the load-bearing judgment and the human on the hook |
```

At 5:52 she sends it.

Her editor reads it on the train home and texts at 7:11: *Tight. See you Wednesday.*

---

There is a specific thing that happened today that I want to name precisely, because it is easy to read the story and miss it.

Priya did not follow the Loop. She ran it. Following would mean executing the steps in sequence and stopping when you reach the end. Running means using the steps as a scaffold while staying alert to the places where the work itself tells you to go back. The loop-back to specification at 1:14 was not a failure of the framework. It was the framework working — the discernment step doing what it is supposed to do, which is surface the places where earlier decisions were wrong.

The fluent practitioner is not the one who executes the steps most cleanly. She is the one who notices fastest when a step needs to be revisited, and who does the revisiting without hesitation, without treating the prior work as a sunk cost she has to protect.

That is the difference. Not speed. Not better prompts. Not a more sophisticated delegation map. The willingness to loop back — to let the work teach you what the work actually needs — and the structural habit of creating moments where that teaching can happen.

---

I want to name the mirror explicitly before we leave the chapter, because the comparison is the book's actual claim.

Eighteen months ago, on a Tuesday morning at 9:42, Priya looked at an email naming a fabricated Pew survey she had let through to publication. She did not have a workflow. She had AI literacy and an instruction — *always verify AI outputs before publication* — that she had not yet known how to operationalize. The piece had shipped. The audience had paid the verification cost in trust.

This morning, on a Tuesday at 9:14, Priya opened Claude with a written specification, a delegation map, a verification list, and the reflex to treat every citation as a hypothesis. The model produced a fabricated source again. She caught it in fourteen seconds. The memo will ship at 5:52 with the citations verified, the assumptions named, the disclosure attached, and the editor's confidence intact.

Same person. Same model. Same kind of failure mode in the output. Different outcome.

That gap — between the Tuesday she could not handle and the Tuesday she could — is the gap this book teaches you to close in your own work, in your own field, against your own kind of failure mode. Priya is one worked example. Your gap will look different on the surface. The shape of the closing — written specification, deliberate delegation, adversarial conversation, calibrated verification, recurring diligence — is invariant.

---

### Translate before you move on — and produce the keystone

This chapter ends with the largest single artifact in your portfolio: the **End-to-End Case Study**, the keystone deliverable in Layer B.

You have, by this point, produced four smaller artifacts that prefigure it:

- *Ch 1 Worked Loop Log* — one recent piece of work taken through all five steps.
- *Ch 3 Specification Library* — 1–3 worked specifications for your typical task types.
- *Ch 5 Adversarial Conversation Log* — one piece of work run through all four adversarial moves.
- *Ch 6 Domain Verification Protocol* — the four-layer protocol customized to your field.

The Case Study is the work where these four come together on a single sustained piece. One Tuesday — yours. One task — real, consequential, in your field, scoped large enough to need every step. From 8:47 AM to 5:52 PM (or its equivalent in your work calendar). Every move documented, time-stamped, with your notes at each decision point.

The Case Study is paired with the **Baseline Audit** from Chapter 0 and will be paired again with the **Final Audit** in Chapter 13. Together they are the cleanest single comparison your portfolio offers: same person, two pieces of work, before fluency and after.

If you cannot identify a task in your work to take through the full Loop end-to-end, that is information. It means either (a) the work you actually do is smaller-scoped than the Case Study calls for — in which case use a recurring kind of task and run two of them — or (b) the work you do is larger-scoped and harder to extract — in which case pick the highest-stakes single decision inside a larger piece. Either fits.

Save the Case Study as `portfolio/08-case-study/` (it will be a folder, not a single file — your spec, your delegation map, your conversation logs, your verification pass notes, your loop-back records, your final deliverable, your AI Use Disclosure).

---

Before you turn the page into Part II, run through the following honestly. The book works only if you can answer yes. If you cannot, the right move is to stop, go back to the chapter where the gap lives, and rebuild before crossing.

Can you write a five-component specification for a real task in your own work, in under fifteen minutes? Can you decompose a complex task into components and produce a delegation map you can defend? Have you, in the last two weeks, run all four adversarial moves on a real piece of your work, and do you have the transcript in your portfolio? Can you run the four verification layers on AI output and calibrate which layers to the stakes of the task? Can you name a recurring AI-assisted process in your work and describe the components you would put in place to maintain it? Can you produce an AI Use Disclosure you would send with a real deliverable — one that names what the AI did, what you did, and the load-bearing judgment calls that required your domain knowledge or accountability?

Most importantly — *can you point to a folder of artifacts in your portfolio that documents your fluency without requiring anyone to take your word for it?*

If you answered yes to all seven, Part II is for you. The loop runs without you in the moment, and the steps reweight in ways the next chapters unpack.

If you answered no to one or two, decide whether the chapter where the gap lives needs a re-read or a fresh attempt with new task material. The Loop in Augmentation is the foundation. Trying to run it in Automation and Agency without the foundation produces predictable failures the later chapters cannot fix.

Stop here if you need to. The book will be here when you return.

---

*What would change my mind.* If a careful study of fluent practitioners showed that the loop-back to specification is rare — that most briefs land on the first spec and the cycle is a teacher's overcorrection — the chapter is wrong about what the cycle is doing. What I observe is the opposite: the loop-back is frequent, and it is usually Discernment forcing a return to Specification. I would update on counter-evidence.

*Still puzzling.* The forty-minute cost of Priya's loop-back was obviously worth it. But I do not have a good model for when a loop-back is worth the cost and when it is a form of productive-feeling avoidance — a way of reworking the spec rather than doing the harder thing of committing to an output. That line is real and I do not yet know how to draw it precisely.

---

> **Going deeper — *Computational Skepticism for AI***
>
> Priya's four-line **AI Use Disclosure** is the same artifact the advanced volume calls a **supervisory log** — and it is treated there not as polite disclosure of AI use but as the document that makes a deployment auditable. The logic is the same as Priya's: name what the AI did, name what the human did, name where the load-bearing judgment lives, name the person on the hook.
>
> The deeper book also formalizes Priya's loop-backs as part of a method called **the Frictional Method** — Predict, Lock, Work, Observe, Reflect, Trace, Calibrate. The prediction-lock (writing down what you expect before you see the output) is the move that makes the gap between expectation and observation visible — which is exactly what triggered Priya's loop-back at 1:14. In an academic or regulated setting, the Frictional journal is the artifact that proves you did the work, not just the AI you used.
>
> See *Computational Skepticism for AI*, **Chapter 4 — The Frictional Method** and **Chapter 13 — Accountability**.

---

## Exercises

### Warm-Up

**1. Annotate the loop.** *(Loop step identification)*
The chapter traces six distinct things Priya does: specification, delegation map, adversarial conversation, verification, loop-back, disclosure. For each one, write one sentence naming what would have gone wrong if she had skipped it. Work through them in order. If you find two where skipping produces the same consequence, look again — the consequences are different.

**2. Classify the delegation.** *(Delegation map construction)*
Priya's delegation map appears implicitly in the chapter and is reconstructed in the table. Below are five tasks drawn from a different kind of work — a graduate student writing a literature review. Classify each task the same way Priya classified hers: model entirely, model generates / human verifies, or human alone.

- Compiling a list of papers published in a given journal between 2018 and 2024 on a named topic
- Summarizing the argument of each paper
- Identifying which papers the field treats as foundational versus peripheral
- Deciding which gaps in the literature the student's own research addresses
- Writing the transition sentences that connect one paper's contribution to the next

For any classification you are uncertain about, write one sentence explaining what makes it contested.

**3. Write the disclosure.** *(AI Use Disclosure construction)*
Below is a brief description of an AI-assisted work product. Write the four-sentence AI Use Disclosure for it, following the structure of Priya's disclosure: what was AI-assisted, what was independently verified, who is accountable.

> A product manager used an AI tool to generate a competitive landscape analysis for a board presentation. The tool summarized five competitors' public positioning. The PM verified three of the summaries against the competitors' actual websites. The product strategy recommendation in the final slide was written by the PM without AI assistance.

---

### Application

**4. Write your specification.** *(Specification — live application)*
Before your next AI-assisted work task — any task, today or this week — write the specification first, before opening the tool. Include: audience, success criteria, structure, exclusions. Time yourself. Spend no more than fifteen minutes. After you complete the task, look back at the specification and answer: what did writing the spec reveal about the task that you would not have noticed if you had opened the tool first?

**5. Build your delegation map.** *(Delegation map — live application)*
For the same task from Exercise 4, or for any recent AI-assisted project, construct a delegation map using Priya's categories. Then compare it to what actually happened: which parts did you handle as planned? Which parts did you accidentally hand over that you had meant to keep? What caused the drift from the plan?

**6. Catch the hallucinated citation.** *(Verification — targeted application)*
Take any AI-generated output that contains citations, footnotes, or references to named sources — from a recent project, or produced fresh for this exercise. Verify every citation: find the source, confirm the claim it is being used to support appears in the source, and confirm the source is current enough to be relevant. Report: how many citations were accurate? How many were approximately accurate but misrepresented? How many could not be located? What is your revised policy for treating AI-generated citations going forward?

**7. Find the specification error.** *(Loop-back — diagnostic)*
Priya's loop-back at 1:14 was triggered by a gap between what she had specified and what her editor had actually asked for. Think of a recent piece of work you delivered — AI-assisted or not — that landed with some version of "this isn't quite what I needed." Reconstruct the specification you were working from. Then reconstruct the specification you should have been working from. Name the specific moment where you could have caught the gap, and what would have needed to happen for you to catch it.

---

### Synthesis — the keystone exercise

**8. Run a full loop — and document it as the Case Study.** *(All five Loop steps — integration; portfolio production)*
This is the chapter's main event. Choose a consequential task you need to complete in the next two weeks. Run the full Loop on it: write the specification before opening any tool; build the delegation map; use at least two adversarial moves in your AI conversation; run a verification pass on every claim you plan to ship; write the AI Use Disclosure before sending. Document every step. Time-stamp where you can.

After completing the task, write a one-page retrospective: where did the loop add the most value? Where did you feel friction against the structure? Did you loop back to specification? What did the loop-back cost, and was it worth it?

Save the full record — spec, delegation map, conversation logs, verification notes, loop-back trace if any, final deliverable, AI Use Disclosure, retrospective — as your **End-to-End Case Study** in `portfolio/08-case-study/`. This is the keystone deliverable of your portfolio.

**9. Design the template.** *(Loop as recurring practice — synthesis)*
Priya's second loop-back is a template update — she pre-bakes a question into her memo template so she does not make the same specification mistake twice. Identify a recurring AI-assisted task in your own work. Design a reusable template for it that pre-bakes the specification, the delegation map structure, the adversarial moves you would deploy, the verification checklist, and the disclosure language. The template should be specific enough that the next time you run the task, the setup takes five minutes instead of thirty.

---

### Challenge

**10. The sunk-cost loop-back.** *(Loop-back judgment — open-ended)*
The chapter ends with an unresolved puzzle: "I do not have a good model for when a loop-back is worth the cost and when it is a form of productive-feeling avoidance." Construct that model. In 400–600 words, propose a set of criteria — at least three, testable against real cases — for deciding whether a loop-back to specification is the right move or whether it is a way of avoiding the harder work of committing to an output. Test your criteria against Priya's 1:14 loop-back (should pass) and against at least one case you construct where the loop-back would be avoidance (should fail). Do not just describe the two extremes — find the line between them.

**11. The Loop under time pressure.** *(Loop adaptation — synthesis and critical stance)*
Priya had ten hours. Most working professionals do not always have ten hours for a piece of first-look work. In 400–600 words, address the following: if you had ninety minutes for the task Priya spent ten hours on, which steps compress, which steps are non-negotiable, and which steps change character under time pressure? Defend your choices by reasoning about what each step is doing — which failures it prevents and how costly those failures are relative to the time saved by skipping it. The answer "do fewer steps" is not wrong, but it requires you to name which failures you are accepting and why they are acceptable at that time horizon.

---

### A note about AI

Integration is the capacity that distinguishes a fluent practitioner from a fluent prompter. The chapter teaches the loop as one operation. The note examines what fails when the operation is taught back to the model.

Where the model genuinely helps: walking through the loop on a worked example and naming where each capacity activated. The exercise reinforces the integration without performing it for you.

Where the model does damage: producing the loop as a finished workflow you can copy. The loop is calibrated to a person, a tool, a task. A loop calibrated to the model's average user is not your loop.

The rule: borrow worked examples, not workflows. The workflow is yours to build.

---

## LLM Exercise — Chapter 8: Putting the Loop Together

**Project:** AI Fluency for [Your Role] — Your Portfolio Keystone

**What you're building this chapter:** The largest single artifact in your portfolio — the End-to-End Case Study. Three deliverables in one session: (a) the AI Use Disclosure language your industry / regulator / employer expects (or needs); (b) the full sustained worked example of one role-typical task taken through every step the book has taught so far; (c) the Part I closing checklist adapted to your role's gating conditions.

**Tool:** Claude Project (continue from prior chapters) + your file system (build the `portfolio/08-case-study/` folder).

---

**The Prompt:**

```
Continuing my AI Fluency portfolio. My Role Dossier from Chapter 0 and my
chapter artifacts from Chapters 1, 3, 5, 6 are in the Project context. This
is Chapter 8 — the keystone chapter that ties them together.

Botspeak Chapter 8 follows Priya through a 10-hour Tuesday running the full
Loop with two loop-back arrows. The chapter introduces the AI USE DISCLOSURE
— Priya's four-line note naming what the AI did, what she did, where the
load-bearing judgment was, and who is on the hook. The chapter ends with the
Part I closing checklist as the gate to Part II.

For my portfolio's Chapter 8 keystone, do three things:

TASK 1 — THE AI USE DISCLOSURE LANGUAGE FOR MY INDUSTRY.
Research and draft the AI Use Disclosure language appropriate for my
industry:
- What does my industry's regulator (if any) currently say about AI use
  disclosure? (Cite specific guidance — bar association, FDA, FINRA, SEC,
  ISO, internal policy norms.)
- What does my employer-class (newsrooms, hospitals, banks, public sector,
  academia, agencies, startups) currently expect or require?
- What do peer reviewers / clients / supervisors / readers typically want
  to see disclosed?

If clear standards exist, document them. If standards don't exist (true in
many domains), draft what your role SHOULD say — based on the principles
in Botspeak Chapter 8: name what the AI did, name what the human did, name
the load-bearing judgment, name the accountable human, name the
verification done.

Produce 3 LANGUAGE TEMPLATES for the disclosure:
- A SHORT version (2–4 sentences, fits at the bottom of an email)
- A STANDARD version (1 paragraph, fits at the top of a deliverable)
- A FORMAL version (multi-paragraph, suitable for regulatory filing,
  byline note, or peer review)

Each version should be copy-paste-ready with bracketed variables for what
differs across instances.

TASK 2 — THE FULL-LOOP WORKED EXAMPLE: YOUR PORTFOLIO KEYSTONE.
Write a complete end-to-end worked example — your version of Priya's
Tuesday — for one role-typical task in your field. The example should:
- Use the specification template from Chapter 3
- Use the delegation map structure from Chapter 4
- Apply at least two adversarial moves from Chapter 5
- Apply the four-layer verification protocol from Chapter 6
- Reference the diligence framework from Chapter 7 (the task is recurring)
- End with the AI Use Disclosure language drafted in Task 1
- Show at least one LOOP-BACK (Discernment surfaces a Specification
  problem; the practitioner returns and reworks)

The example should be ~2,000–3,500 words and read like Priya's narrative —
time-stamped, decisions visible, internal moves made explicit. Save as
`portfolio/08-case-study/00-narrative.md`. Save the supporting artifacts
(spec, delegation map, conversation log, verification notes, disclosure)
as separate files in the same folder so the case study is a complete
working record, not just a story.

TASK 3 — THE PART I CLOSING CHECKLIST FOR MY ROLE.
Adapt Botspeak's Part I closing checklist for my role — the seven
honest-yes-or-no questions that gate the reader to Part II (Automation and
Agency). Each item references the corresponding chapter's portfolio
artifact and asks whether I can point at it as evidence of practice on
real role-typical work.

Save the checklist as `portfolio/08-case-study/01-part-1-gate.md`.
```

---

**What this produces:** Your portfolio's keystone — a `portfolio/08-case-study/` folder containing the full worked example, the supporting artifacts (spec, delegation map, conversation logs, verification notes, disclosure language for your industry in three formats), and the Part I closing gate adapted to your role. ~4,000–6,000 words of new portfolio material plus the structured supporting files.

**How to adapt this prompt:**

- *For your own project:* The case study is the single most-referenced artifact in your finished portfolio. Choose a real task you actually need to do — not a hypothetical. The reality is what makes it credible to a future reader.
- *For ChatGPT / Gemini:* Works as-is. ChatGPT can do industry-standard research; verify any cited regulation independently.
- *For Claude Code:* Useful here for managing the multi-file `portfolio/08-case-study/` folder structure. Ask Claude Code to set up the folder with stub files for each artifact, then fill them as you work.
- *For Cowork:* Recommended. The case study is the longest single artifact in the portfolio.

**Connection to previous chapters:** This is the synthesis of Part I. Chapters 1, 3, 5, 6, and 7 each produced individual portfolio artifacts. The Chapter 8 case study shows them running together on one sustained piece of work. After this chapter, you have everything you need for AI work in Augmentation — which is most of the day for most readers.

**Preview of next chapter:** Chapter 9 starts Part II — Automation. The next portfolio artifact is the Automation Inheritance Audit: an appropriateness analysis of an existing automation in your work (or, for self-study readers, a public AI system in your field that you analyze as if you had inherited it).

---

## AI Wayback Machine

The ideas in this chapter didn't appear from nowhere. **Donella Meadows** was writing about feedback loops, leverage points, and what makes a system fail visibly versus invisibly decades before most people had heard of "the AI Loop." Her central insight — that the most powerful interventions in any system are rarely the obvious ones, and that systems resist the changes you make at the wrong level — maps directly onto what Priya discovers at 1:14: the loop-back to specification is a leverage-point intervention, not a correction of a mistake. Here's a prompt to find out more — and then make it better.

![Donella Meadows, c. 1990s. AI-generated portrait based on a public domain photograph.](images/donella-meadows.jpg)
*Donella Meadows, c. 1990s. AI-generated portrait based on a public domain photograph (Wikimedia Commons).*

**Run this:**

```
Who was Donella Meadows, and how do her ideas about feedback loops and
leverage points connect to running the full Specification → Delegation →
Conversation → Discernment → Diligence loop on a single task? Keep it to
three paragraphs. End with the single most surprising thing about her
career or ideas.
```

→ Search **"Donella Meadows"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain "leverage points" in plain language, as if you've never read systems thinking
- Ask it to compare Meadows's leverage-point hierarchy to the loop-back move (Discernment surfaces a Specification problem)
- Add a constraint: "Answer as if you're annotating Priya's Tuesday for a junior reading the portfolio"

What changes? What gets better? What gets worse?
# Chapter 9 — When You're Not There
*The Loop Without You in the Moment.*

Here is a question worth sitting with before we go any further.

When you use an AI tool in the ordinary way — you type a prompt, you read the output, you decide whether to keep it or revise it — there is a human in the loop at every step. You are that human. The human is there not because anyone designed the system that way; the human is there because the system is just a chat window and you are sitting in front of it. The quality control is structural. It costs you nothing to achieve, because the act of reading the output before doing anything with it is the quality control.

Now suppose you automate something. Suppose you set up a process where the model runs on a schedule — every Monday morning, say, pulling last week's news, generating a summary, posting it to a Slack channel before anyone arrives. The process runs. The model generates output. The output goes somewhere and acts in the world. And you are not there.

The question is: where did the quality control go?

This is not rhetorical. The quality control did not disappear. It has to exist somewhere, in some form, or the automation is a reliability time-bomb waiting for its trigger. The work of this chapter is to show you exactly where the quality control has to go, and why designing it in deliberately is the difference between an automation that serves you and one that eventually produces the call from your editor asking how something like this happened.

---

Let me make this concrete with the kind of failure that actually occurs.

Priya, nineteen months past Chapter 0, has been on the hook for the publication's Monday-morning automated market-intel summary for seven weeks. The automation was built by a predecessor at the publication; she inherited it when her oversight role expanded. Every Monday morning the system pulls the past week's articles from a curated set of trade publications, hands them to a language model with a structured prompt, and posts a one-page market-intel summary to the Climate-and-Energy editorial Slack channel before the team arrives. For seven Mondays the automation has run cleanly. The desk reads the summary. Editors cite it in meetings. Priya, as the new owner, has been checking it some weeks and not others; the runs she has checked have looked fine.

In week seven, one of the source articles turns out to be wrong. A trade publication ran a story Thursday about a major utility's filing for a new transmission corridor; on Friday afternoon, the publication issued a retraction — the filing had been mischaracterized by their source. The retraction did not flow back into the automation's source cache. The model, working only from the original article as the automation had ingested it Thursday night, summarized the filing as current fact. The summary posted Monday morning. A senior editor on the Climate desk, working on the Monday afternoon commissioning meeting, pitched the desk on a reaction piece to the (retracted) filing. A reporter was assigned. The reporter started drafting Tuesday morning. By Wednesday afternoon — when another editor, reading the trade publication's most recent issue, caught the retraction — the reaction piece was halfway done. It was killed. The reporter lost two days of work. The publication came very close to publishing analysis of a story that was not true.

Notice the shape of this failure. The model did not hallucinate. It did not fabricate. It faithfully summarized a real article from a real publication. The article was simply no longer true by the time the model read it, and the model had no way to know that, and the spec — which Priya had inherited but not rewritten — had not anticipated the possibility. This is not a model failure. It is a design failure — specifically, the failure you get when you remove the human from the loop and do not replace the human with anything.

![Figure 9.1 — A seven-week timeline of the inherited automation. Weeks 1–6 marked "clean runs / trust accumulates." Week 7 marked with the retraction event and its downstream consequences.](images/09-when-youre-not-there-fig-01.jpg)

In ordinary augmentation work, this error never happens. Priya — or any editor — would have read the source article herself, or at minimum read the model's summary before forwarding any claim from it into a commissioning conversation, and would likely have checked the trade publication's current state before agreeing to commission a reaction piece. The error is impossible when a human is actively in the loop. Given enough recurrences, it is nearly inevitable when the human has been systematically removed.

---

Every chapter up to this one has described a loop: you specify the task, you delegate some portion to the model, you have a conversation that refines the output, you apply the verification layers from Chapter 6, and you maintain the practice over time. That loop runs with you at the keyboard. You conduct it in real time.

When you automate something, the loop does not disappear. It runs. But you do not. Every step still has to happen — specification, delegation, conversation, discernment, maintenance — but some steps that were reflexive in person become impossible without explicit design. The automation changes where the weight falls.


| Loop step | In augmentation | In automation |
|---|---|---|
| **Specification** | Covers the specific inputs you have in front of you; you're in the context and know what you're working with | Must cover a *class* of future inputs you haven't seen yet, in conditions that will change — silence in the spec is where failures live |
| **Delegation** | A real-time decision you can walk back if the output looks wrong | A design-time commitment made before any specific inputs arrive; much harder to reverse once the system is running |
| **Conversation** | Iterative — you push back, add context, run adversarial moves in the moment | Frozen at whatever prompt you wrote at setup; there is no one to push back on week seven's output |
| **Discernment** | Applied in real time to the specific output before it leaves your desk | Cannot happen in real time at volume; must shift to sampling, adversarial test cases, and periodic audits — with gaps between each |
| **Maintenance** | A good practice that catches drift and names accountability over time | The only mechanism by which you learn the system is failing; without explicit design, it does not happen |


**Specification** becomes harder, not easier. When you write a one-off task, your spec covers one set of inputs you have in front of you. You know the context because you are in it. When you specify an automation, you are specifying a class of tasks the system will run against inputs you have not yet seen, in conditions that will change over time. The inherited spec was correct for the normal case — articles from the curated list that were currently accurate. It was silent on what to do when an article had been retracted. A good spec for automation has to anticipate the ways the inputs will deviate from the design case, and has to specify what the system should do when they deviate. The silence in the spec is where the failures live.

**Delegation** shifts from a real-time decision to a design-time commitment. In ordinary work, you decide in the moment which parts to delegate, and you can walk that decision back if the output looks wrong. In automation, you have already delegated, in advance, to a system that will run the same delegation every recurrence. The commitment is much harder to walk back, because the system runs without you. The question of what to delegate has to be answered more carefully, at design time, before any of the specific inputs have arrived.

**Conversation** gets frozen. When you are at the keyboard, the conversation with the model is iterative — you push back, you add context, you run the adversarial moves from Chapter 5. In automation, the conversation is whatever prompt you wrote at setup time, run exactly that way every recurrence. There is no one to push back on week seven's output. Whatever corrective moves you want the system to make, you have to bake them in as standing instructions. The model does not have a peer reviewer. You are not there to be one.

**Discernment** is where Priya's inherited automation failed. In ordinary work, discernment is what you do before the output leaves your desk — the four verification layers applied to the specific thing you just built. In automation, discernment cannot happen in real time on every output, because the volume is too high and you are not there. Discernment has to shift to a different schedule: periodic sampling, adversarial test cases run at intervals, retrospective audits. These are approximations, with gaps. The gaps are where the failure happens in week seven.

**Maintenance** becomes the most important step, not a nice-to-have afterthought. In ordinary work, maintenance is the practice of keeping a process healthy over time — checking for drift, auditing outcomes, naming who is accountable. In automation, maintenance is the only mechanism by which you learn that the system is failing. Without explicit maintenance design, the automation runs until someone notices a bad output — which means the failure has already propagated some number of times before it was detected.

The reweighting is worth sitting with. Specification and maintenance become load-bearing in ways they are not in ordinary work. Discernment has to be redesigned around the absence of a real-time human. The conversation has to be preloaded with the corrections the model would need in advance. None of this is obvious when you set the automation up — or when you inherit one and start running it — because the setup feels like any other task: write a prompt, test it on a few examples, confirm it works. Or: read the spec, see that it has been running cleanly for some weeks, trust it. The testing does not reveal the reweighting. The reweighting only becomes visible when the failure arrives.

---

There is something about automation failures that is not obvious until you think it through carefully.

When a model produces a wrong output in ordinary augmentation work, the blast radius is bounded. One piece of work. You catch the error, you correct it, you ship the corrected version. The damage is proportional to the rework.

When a model produces a wrong output in an automation, the blast radius is proportional to *how long the failure goes undetected multiplied by the downstream consequences of each wrong output*. If the publication's automation produces a wrong output every Monday for six weeks before anyone notices — six weeks, not one — there are six wrong summaries in the desk's history, and six weeks of commissioning conversations made partly on their basis, and the task of auditing the damage is much harder than correcting a single piece of work.

The scaling can be worse than linear if wrong outputs compound. A wrong competitive read in week three shapes how an editor frames a story in week four. The wrong frame shapes a commissioning decision in week five. The decision structures a reporter's beat in week six. By week seven, the wrong output from week three has influenced a chain of things that cannot be easily unwound. This is not a worst case. It is a realistic case for any automation whose outputs feed into a running process.

*Figure 9.3*

The design implication is stark: you cannot rely on accidentally noticing that an automation is failing. In ordinary work, you notice because you are reading the output. In automation, you have deliberately arranged not to read the output in real time. Noticing has to be designed. It has to be a scheduled, explicit, accountable activity, built in at setup time — or at the moment you inherit responsibility — because if it is not built in, it does not happen. And the blast radius grows from the moment the first wrong output appears until the moment someone happens to look.

---

Before automating any task — or before accepting ownership of an existing automation — three tests. If the task fails one of them, do not automate it (or do not continue running it in current form) without explicit additional safeguards. If it passes all three, automation is appropriate; the next chapter will show how to specify and design the maintenance around it.

**Is the scope bounded?** Can you describe, in a single paragraph, exactly what the task does and what it does not do, in terms you would defend to your editor or manager? The inherited Monday automation's task was: summarize the past week's articles from this curated list of sources, in this format, at this time. That is bounded. The edges are clear. Compare to: automate market intelligence. That is not bounded. The surface area is too large for any spec to be tight, which means the model will be making scope decisions in real time that you have not authorized it to make. If the task is not bounded, you cannot specify it well, and if you cannot specify it well, you cannot design the discernment and maintenance around its failure modes.

**Are the inputs predictable?** Are the inputs the system will receive within a known range that your design cases actually represented? The Monday automation's inputs were mostly predictable — trade publication articles in a known format from a curated source list. Two failure modes were invisible during setup: retracted articles, and behind-paywall articles the model could not fully read. These were rare but possible. The model had never encountered them during testing. They were waiting in the tail of the input distribution.

The question to ask is not whether the typical input is predictable. The typical input is almost always predictable. The question is whether the *atypical* inputs — the ones that are rare but real — are represented in your design cases, and whether the spec tells the model what to do when it encounters them. If the spec is silent on the atypical inputs, the atypical inputs are where the failures will be.

**Is the blast radius acceptable if the system fails continuously for weeks?** This is the test most often skipped because failure feels hypothetical during setup. It does not feel hypothetical after the commissioning meeting where the reaction piece had to be killed. The right way to run this test is to assume the failure will happen — not as a possible outcome, but as a scheduled event — and to ask what the accumulated damage will be when you finally notice. If the damage is manageable and the outputs are low-stakes enough that continuous failure would be caught and corrected without lasting consequences, then automating is appropriate. If six weeks of wrong outputs would have already propagated into decisions that are hard to reverse, either do not automate, or build in explicit human checkpoints that catch each output before it acts in the world.

These three tests take five minutes. They prevent most of the cases where automation should not have been deployed in the first place — and they are the same tests you run on the day you inherit an automation someone else built.

---

The phrase Priya writes down, after the killed reaction piece, is: *designing the noticing is part of designing the system.* That sentence names the thing that distinguishes a well-designed automation from one that is waiting to fail. It applies whether you are building one or inheriting one — and on the day you inherit, redesigning the noticing is the first thing.

Designing the noticing means deciding, at setup time or at inheritance time, how you will learn that the system is producing wrong outputs before those outputs have been acting in the world for weeks. There are three forms this takes.

*Sampling* is the simplest: commit, at setup or inheritance time, to reading a fraction of the outputs in full on a scheduled basis. Not spot-checking whenever it occurs to you, but a regular, accountable practice — Priya now reads the full Monday summary every Tuesday morning and spot-checks one source per week against its current state. Sampling does not catch every failure. It catches failures that are persistent enough to appear in the sample, which is most of the failures that matter.

*Adversarial test cases* are inputs you construct to probe the failure modes you identified during the bounded-scope and predictable-inputs tests. In Priya's case, an adversarial test case might be a retracted article inserted into the source list — or a known-paywalled article whose metadata implies one claim and whose accessible text contains a different one — to see whether the model flags it or silently summarizes it. You run these test cases periodically, not just at setup, because the model's behavior can shift when the inputs shift. Adversarial testing is how you find the failure mode before it finds you.

*Outcome auditing* is periodic review of what the automation produced against what actually turned out to be true. Once a quarter, Priya reviews the past quarter's market-intel summaries against what actually happened in the segment. The audit catches systematic bias or systematic omission that sampling might miss because each individual output looked plausible. Outcome auditing is the slowest of the three forms but the one that catches the failures that are structurally correct and substantively wrong — the ones that look fine on the day and turn out to have been quietly misleading.

![Figure 9.4 — A three-panel reference card for the noticing forms](images/09-when-youre-not-there-fig-04.jpg)

Building these three practices in at design time — or at inheritance time, which is when most readers of this chapter will be running them — is not optional infrastructure. They are the quality control that replaces the human who is no longer there.

---

The two things this chapter has established are the conditions for appropriate automation and the shape of the noticing design. Chapter 10 takes both into depth: what anticipatory specification looks like when done carefully — the kind of spec that prepares the system for inputs it has not yet seen — and how to build the discernment and maintenance practices into the automation's design from the first day. By the end of that chapter you will be able to specify a small automation with the failure modes addressed in writing and the noticing built in.

---

### Translate before you move on — produce the Automation Inheritance Audit

Priya's case was inheriting a publication automation that ran cleanly for six weeks and surfaced its inherited blind spot in week seven. In your field, what is the equivalent? Most readers will not be building new automations from scratch. Most readers will be inheriting them — from a predecessor, from a vendor, from a team that set the system up and moved on. The discipline this chapter teaches is mostly the discipline of running the appropriateness tests on something already running.

For a clinician: a clinical-decision-support tool the EHR vendor enabled by default. For a software engineer: an automated test-generation or pull-request-summarization tool the team adopted some months ago. For a marketing manager: a campaign-personalization or send-time-optimization tool that came with the platform. For a teacher: an AI-assisted plagiarism-detection or essay-feedback tool the school enabled. For a research scientist: an automated literature-monitoring service the institution licensed. For a lawyer: an automated docket or compliance-monitoring tool the firm subscribes to. The specific tool varies. The shape — *a system running on a schedule that someone else specified, whose inputs and outputs you have at most partial visibility into* — is invariant.

**The Automation Inheritance Audit + Noticing Protocol — Chapter 9 Portfolio Artifact (Layer A template + Layer B audit, diagnostic + framework):**

Pick one automation you have inherited, run, or could plausibly be asked to oversee. Apply the appropriateness-test screen and design the noticing protocol you would run on it from this week forward.

Five sections:

1. *The automation named.* What it does, on what inputs, producing what outputs, on what schedule, for whom. Include what the spec (if any) says and what it is silent on.
2. *The three appropriateness tests.* Bounded scope — pass, partial, or fail with one-line justification. Predictable inputs — same, with a named tail-input failure mode. Acceptable blast radius if the automation fails continuously for six weeks — what is the realistic accumulated damage?
3. *Drift assessment.* Has model, context, or use case drift happened to this automation that you can detect from where you sit? If you cannot tell, name what you would need access to.
4. *The noticing protocol from this week forward.* Sampling (cadence, what you read, owner). Adversarial test cases (cadence, what inputs you construct, what the model should do with each). Outcome auditing (cadence, metric, reviewer who is not the owner).
5. *The deployment verdict.* Continue running as-is, continue running with stated modifications, or recommend pausing pending redesign. Defend the verdict in one paragraph.

For self-study readers without an automation in their direct work, the substitute is to pick a public AI automation in your field and audit it as if you had been asked to inherit it. The audit is structurally similar; only the access to operational data is weaker.

Save as `portfolio/09-automation-audit.md`. Three to four pages. The audit is one of the three diagnostic artifacts in your finished portfolio — alongside the Practitioner Profile (Chs 2 + 4) and the paired Baseline / Final Audit (Chs 0 and 13).

**Update your DESIGN.md.** Add a section on automation-noticing criteria your domain expects: what sampling cadence is reasonable in your field, what adversarial test cases your field has documented failure modes for, what outcome metrics your domain holds automations accountable to. This section will pair with the Ch 10 specification work for the automations you go on to spec.

**Update your CLAUDE.md** with the chapter's operational rule: *I do not own a running automation without sampling, adversarial test cases, and outcome auditing on my calendar. If I inherit one without those, the first week's work is putting them in place. Designing the noticing is part of designing the system — and redesigning the noticing is the first thing on the day of inheritance.*

---

*What would change my mind.* If automation infrastructure evolved to include retraction-detection, drift-detection, and outcome-monitoring as default turnkey capabilities — things you configure rather than design from scratch — the manual design work I describe here would shift. Some platforms are beginning to move in this direction. The discipline would remain the practitioner's even then; what changes is how much of the implementation is handed to you. As of early 2026, the implementation is mostly yours.

*Still puzzling.* I do not have a clean estimate of what fraction of currently deployed AI automations would fail an honest run of the three appropriateness tests. My sense, from watching organizations adopt these tools, is that it is high — most were built without the tests being run, because the tests feel like friction during the excitement of setup. I would like data on this. I do not have it.

---

> **Going deeper — *Computational Skepticism for AI***
>
> Priya's retraction failure is, in the language of the advanced volume, a **hidden assumption that failed silently** — the system was built on the assumption that sources are durable, the assumption was never written down, and the model had no way to know when the assumption had broken. The deeper book argues that procedural data validation (distributions, missingness, correlation checks) is necessary but not sufficient — that the failures that actually break deployments live in structural assumptions invisible to standard checks. The cure is the **six-step epistemic-frame reconstruction** that explicitly enumerates what the data is claimed to represent, what it actually represents, and what it excludes — including a prediction-lock about the failure pattern you would expect if a particular assumption broke.
>
> The advanced book also distinguishes prediction systems (where the worst output is wrong information) from **consequence systems** (where the worst output is wrong action in the world). The Monday automation sits in between: it produces information, but the information drives consequential action by editors. This in-between zone is where most current automations sit — and where the loop reweighting in this chapter is most urgent.
>
> See *Computational Skepticism for AI*, **Chapter 5 — Data Validation** and **Chapter 9 — Validating Agentic AI**.

---

### A note about AI

Asynchronous operation is the capacity to set the model working without supervision. The loop's normal feedback structure does not apply.

Where the model genuinely helps: walking through what could go wrong while you are not watching, before you launch the run. The pre-mortem is the substitute for the absent feedback loop.

Where the model does damage: confident reports of completed work when the work was not actually completed correctly. Asynchronous failures are the worst kind because by the time you check, the failure has compounded.

The rule: design the unsupervised run so that the cost of a silent failure is bounded. The model will not flag silent failures itself.

---

## LLM Exercise — Chapter 9: When You're Not There

**Project:** AI Fluency for [Your Role] — Your Automation Inheritance Audit

**What you're building this chapter:** The **Automation Inheritance Audit + Noticing Protocol** — appropriateness tests applied to one inherited automation in your work, plus the sampling / adversarial-test / outcome-audit protocol you will run on it from this week forward. Plus an update to your `DESIGN.md` on automation-noticing criteria. Plus one new rule in your `CLAUDE.md`.

**Tool:** Claude Project (continue — your full portfolio so far is in context) + your file system (`portfolio/`).

---

**The Prompt:**

```
Continuing my AI Fluency portfolio. My Role Dossier, Worked Loop Log,
Practitioner Profile, Specification Library, Adversarial Conversation
Log, Verification Protocol, Diligence Framework, End-to-End Case
Study, PROJECT.md template, CLAUDE.md, and DESIGN.md are in the
Project context.

Botspeak Chapter 9 watches Priya — nineteen months past Chapter 0 —
inherit the publication's Monday-morning market-intel automation.
Week 7 of her oversight, the automation summarizes a retracted
article as live news. A reaction piece is commissioned, drafted for
two days, then killed when another editor catches the retraction.
The chapter introduces the three APPROPRIATENESS TESTS (bounded
scope, predictable inputs, low blast radius), the loop reweighting
for automation, and the three NOTICING FORMS (sampling, adversarial
test cases, outcome auditing).

For Chapter 9's portfolio artifact, do three things.

TASK 1 — RUN THE AUDIT ON ONE AUTOMATION.
Pick one automation I have inherited, run, or could plausibly be
asked to oversee in my work. If I have none in direct work, pick
a public AI automation in my field and audit it as if I had been
asked to inherit it.

Walk the audit in five sections:

1. THE AUTOMATION NAMED. What it does, on what inputs, producing
   what outputs, on what schedule, for whom. Include what the spec
   (if any) says and what it is silent on. Specific.

2. THE THREE APPROPRIATENESS TESTS.
   - Bounded scope: pass / partial / fail, one-line justification
   - Predictable inputs: pass / partial / fail, with one named
     tail-input failure mode the design cases probably missed
   - Acceptable blast radius if the automation fails continuously
     for 6 weeks: estimate the realistic accumulated damage

3. DRIFT ASSESSMENT. Has model, context, or use-case drift happened
   to this automation that I can detect? If I cannot tell, name
   what I would need access to in order to assess.

4. THE NOTICING PROTOCOL FROM THIS WEEK FORWARD.
   - Sampling: cadence, what I read, owner (probably me)
   - Adversarial test cases: cadence, what inputs I construct,
     what the model should do with each
   - Outcome auditing: cadence, metric, reviewer (someone other
     than me)

5. THE DEPLOYMENT VERDICT. Continue running as-is, continue with
   stated modifications, or recommend pausing pending redesign.
   Defend the verdict in one paragraph.

Save as `portfolio/09-automation-audit.md`. Three to four pages.

TASK 2 — UPDATE MY DESIGN.md.
Add a section on automation-noticing criteria my domain expects:

- What sampling cadence is reasonable in my field? (Daily,
  weekly, monthly — and why?)
- What adversarial test cases does my field have documented
  failure modes for? (For journalism: retracted articles,
  paywalled articles, source-impersonation, fabricated quotes.
  Your field has its own list.)
- What outcome metrics does my domain hold automations
  accountable to?

Append to `portfolio/DESIGN.md` as a new section.

TASK 3 — ADD ONE RULE TO MY CLAUDE.md.
Append the chapter's operational rule: "I do not own a running
automation without sampling, adversarial test cases, and outcome
auditing on my calendar. If I inherit one without those, the first
week's work is putting them in place. Designing the noticing is
part of designing the system — and redesigning the noticing is
the first thing on the day of inheritance."

Push back if my appropriateness-test answer says "pass" on all three
without a single qualifier. The default for inherited automations is
"partial" on at least one test — the spec is rarely complete enough
to fully pass any of them. Press on which qualifier I should add.
```

---

**What this produces:** Your portfolio's eighth framework artifact, the third diagnostic in your portfolio, a meaningful update to your `DESIGN.md`, and another rule in your `CLAUDE.md`. The Automation Inheritance Audit is the artifact that documents your capacity to take responsibility for an AI system you did not build. ~3,000–4,000 words across the new material.

**How to adapt this prompt:**

- *For your own project:* Pick a real automation, not a hypothetical. The audit is structurally weaker on a hypothetical because you cannot assess drift, cannot inspect actual outputs, cannot test the model's behavior on real tail inputs.
- *For ChatGPT / Gemini:* Works as-is.
- *For Claude Code:* Useful for scripting the adversarial test cases — a small set of input variations the test loop runs on a schedule.
- *For Cowork:* Recommended.

**Connection to previous chapters:** Chapter 7 built the Diligence Framework — the four-component protocol for governing recurring AI work. Chapter 9 specifies the application of that framework to a specific automation, with the appropriateness tests as a pre-condition. Together they cover the discipline of taking responsibility for AI systems that run.

**Preview of next chapter:** Chapter 10 — anticipatory specification for automation. The six common ambiguity types and the four automation failure modes, applied to one specific automation you would build or rebuild. The Automation Specification artifact is the most directly deployable single artifact in your portfolio.

---

## AI Wayback Machine
The ideas in this chapter didn't appear from nowhere. **Norbert Wiener** invented cybernetics in the late 1940s — the study of feedback, control, and what happens to a system when its corrective loops break down. His central warning, stated plainly in *The Human Use of Human Beings* (1950), was that automated systems amplify errors without correction when no feedback mechanism catches them in time. That is precisely what happened to the publication's Monday automation: the system ran correctly, the feedback loop was absent, and the error propagated until a Wednesday catch forced it into view. Here's a prompt to find out more — and then make it better.

![Norbert Wiener, c. 1950s. AI-generated portrait based on a public domain photograph.](images/norbert-wiener.jpg)
*Norbert Wiener, c. 1950s. AI-generated portrait based on a public domain photograph (Wikimedia Commons).*

**Run this:**

```
Who was Norbert Wiener, and how does his work on cybernetics and
feedback loops connect to the problem of designing AI automations
that run without a human in the loop — specifically to the idea that
blast radius scales with time-to-detection? Keep it to three
paragraphs. End with the single most surprising thing about his
career or ideas.
```

→ Search **"Norbert Wiener"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain "cybernetics" in plain language, as if you've never encountered the concept
- Ask it to compare Wiener's feedback-loop thinking to the three noticing forms in this chapter
- Add a constraint: "Answer as if you're sketching a governance policy for an inherited weekly automation"

What changes? What gets better? What gets worse?
# Chapter 10 — Specification and Diligence for Automation
*Doing the Work the Live Human Won't Be There to Do*

*The implicit checks you run without naming them don't disappear when you automate. They have to go somewhere. This chapter is about making them explicit before the automation falls into the gap you left.*

---

There is a deceptively simple question hiding inside every automation decision, and almost nobody asks it before they ship.

The question is: *what work are you currently doing by hand that you are about to stop doing?*

Not the work the automation does — you have thought about that. The invisible work. The implicit checks you run without naming them. The judgment calls you make so fast you have forgotten they are judgment calls. When you do a task by hand, you handle exceptions as they arise. You notice when a source looks unreliable. You hedge when two pieces of information conflict. You ping a colleague when something feels too consequential to pass along without a second set of eyes. None of that is in your prompt. All of it is in your head, running continuously, as you work.

When you automate a task, that work does not disappear. It has to go somewhere. Either you design it into the automation explicitly — specifying what to do when reality does not match the design case — or you leave it as a gap, and the automation runs forward into that gap until it falls in.

This chapter is about designing the work in. And the first thing to know is that doing so changes the shape of the specification considerably.

This is also, for Priya, the rebuild chapter. The inherited Monday market-intel automation from Chapter 9 — the one that summarized a retracted article as live news in week seven — went into pause-and-redesign after the audit. She is the named owner. Her week-twenty work, the week after the killed reaction piece, is specifying the replacement properly. The running example through this chapter is her rebuild. The discipline travels to any automation in any field.

---

Let me make this concrete with a comparison. The market-intel summary is a one-page document that lands in the editorial Slack channel every Monday morning, covering the past week's moves in clean-energy storage and the surrounding policy environment. Priya — and editors before her — used to produce this kind of summary by hand. It worked. The publication then automated it. The automation failed, in the way we walked in Chapter 9. Now she is rebuilding it.

Here is the specification she would write if she were doing this task by hand one time, with herself at the keyboard:

> Produce a one-page market-intel summary for the editorial Slack channel, drawn from the past week's news in our source list, focused on the top six companies and on segment-level developments. Audience: the desk, read in five minutes. Tone: declarative; flag confidence on each item. Format: bulleted, grouped by company, then a "segment trends" section. Every claim hyperlinked to its source.

That is a good Augmentation specification. It is one paragraph. It is complete for the case where a skilled person is doing the work in real time, handling exceptions as they arise.

Here is what the Automation specification looks like for the same task — the rebuild Priya actually writes:

> Produce a one-page market-intel summary, generated automatically every Monday at 6 AM, posted to the Climate-and-Energy editorial Slack channel. Audience: the desk, read between 8 and 9 AM. Tone: declarative; explicit confidence label on each item.
>
> Source list: see appendix. Each source has been validated for the prior six weeks against retraction history; sources with retraction frequency over 1% are excluded. Source list is reviewed monthly by the named owner.
>
> Pre-flight checks, run before generation: for each article in the input set, query the publication's retraction page; exclude any article flagged within the past 14 days. For each article older than five days, include a freshness flag in the output. If more than 20% of input articles are flagged or excluded, do not generate the report; instead post to the channel: "Pre-flight check failed; report manually triggered."
>
> Generation rules: one bullet per item, maximum 30 words. Each bullet hyperlinked to source. Confidence label on each bullet: HIGH (multiple independent sources, recent), MEDIUM (single reliable source, recent), LOW (single source, contested, or older than five days). Bullets labeled LOW are grouped at the bottom under "Provisional — verify before commissioning."
>
> Exclusions: do not summarize opinion pieces unless flagged as analysis. Do not produce forecasts. Do not synthesize across companies in ways that imply correlation; report each separately. Do not include claims that cannot be sourced to an article in the input set.
>
> Output format: top section "Company moves," six headers in fixed order even if a company had no news. Middle section "Segment trends." Bottom section "Provisional." Always end with: "Source list version [N], generated [date], by [system identifier]. For corrections, contact [owner]."
>
> Failure-mode handling: if the model returns no output, post "Generation failed; manual summary by EOD." If the output exceeds 800 words, truncate to the top ten items by recency and post with note. If the model produces a citation that does not match an article in the input set, drop that bullet and log the event.
>
> Diligence design, runs separately: each Tuesday, the named owner reads the full report and spot-checks two random bullets to source. Once a month, run a fixed test set — ten articles from a held-out validation pool, including known-retracted articles — against the current automation and compare against the locked baseline. Any deviation from baseline categorization is reviewed. Once a quarter, compare the prior quarter's summaries against ground-truth events in the segment and compute hit rate and false-positive rate.
>
> Named accountable human: Priya. Backup: [name]. Escalation: managing editor if any failure-mode trigger fires two weeks in a row.

The second specification is roughly three times the length of the first. Most people, when they first see this, assume something has gone wrong — that the specification has been over-engineered, that the extra length is bureaucratic cover for a simple task. It is not. The extra length is honest accounting for the work a human would have done implicitly if she had been at the keyboard. The implicit work did not disappear when the publication decided to automate. Priya wrote it down.

![Side-by-side comparison: a one-paragraph Augmentation specification and a section-structured Automation specification with six labeled additions](images/10-specification-and-diligence-for-automation-fig-01.png)
*Augmentation specification → Automation specification*


That is the core discipline of Automation specification: make the implicit explicit, in advance, because nothing about the execution will be in person.

---

The additional length in an Automation specification is not random. It clusters into six categories of anticipated deviation — six ways reality can fail to match the design case, which the specification has to address because no one will be present to address them in the moment.

The first is input-quality variation. What does the system do when an input is degraded, missing, or formatted differently than expected? For the market-intel summary, this means retractions, paywalls, and articles older than expected. For other automations, it means missing fields in a submitted form, a corrupted file, an upstream API that returned an error code instead of data. The specification should answer: what behavior do we want, and how does the system detect when input quality has degraded below the threshold where we trust the output?

The second is output-volume variation. What does the system do when the output is substantially longer or shorter than the design case? The 800-word truncation rule in the automation spec above is an answer to this. If a model is left unconstrained on volume, it will, in some fraction of runs, produce outputs that violate the format the downstream consumer expects — a five-paragraph analysis when someone expected three bullets, a one-line summary when someone expected a full page. The automation needs to handle this without halting.

The third is context shifts the model cannot detect. What does the system do when the world has changed in a way the model has no access to? The model does not know that a new company entered the market last Thursday, or that a regulatory change last month made certain claims non-compliant, or that the segment you have been tracking just got redefined by the trade press. For slowly-changing context, the monthly source-list review addresses this. For fast-changing context, the pre-flight check and the weekly spot-check are what surface it. The key design question is: what kinds of context change would break this automation's validity, and how would we know that happened?

The fourth is ambiguous inputs. What does the system do when the input is internally contradictory or unclear? For the market-intel task, this is two sources reporting different versions of the same event. For other automations, it is a data row that violates an expected constraint, a customer message that spans multiple issue types, a document with conflicting version numbers. The model will produce output regardless; the question is whether the output it produces in ambiguous cases will be handled correctly by the downstream consumer, or whether ambiguity should trigger a flag that surfaces the conflict to a human.

The fifth is high-stakes outputs. Some outputs, as special cases, are more consequential than the design baseline. A major company acquisition in the week's news changes how everything else in the summary should be interpreted — it is not just another item. A risk flag in a financial summary warrants different handling than a routine variance. The automation spec should describe what high-stakes looks like, how to detect it, and what the system should do differently when it detects it. Often the right answer is not to handle high-stakes outputs within the automation at all — it is to detect them, halt, and surface them to a human.

The sixth is model-specific failure modes. What does the system do when the model hallucinates, refuses, or produces output that does not pass the format specification? The citation-verification step in the automation spec above is designed to catch one specific form of hallucination: a confident-looking citation that does not correspond to any article in the input set. Other failure modes include output in the wrong language, output that exceeds or falls below format constraints, output that contains a refused section without flagging it, output that looks syntactically correct but carries a semantic error only detectable by checking against the source. Each of these needs a detection step and a handling rule.

Run through these six categories before you ship any automation — or before you sign off on rebuilding one. For each one, ask: have I addressed this? If the answer is no, the specification is incomplete. The six categories are not exhaustive — there are failure modes specific to your domain that are not on this list — but addressing all six gets you through the common cases.



*Figure 10.2*

| Category | What it addresses | Detection mechanism | Handling rule | Example from the market-intel rebuild |
|---|---|---|---|---|
| **Input-quality variation** | Inputs degraded, missing, or formatted differently than expected | Pre-flight check on each input batch | Halt or flag when quality drops below the trust threshold; do not silently proceed | Retractions, paywalls, articles older than the freshness window |
| **Output-volume variation** | Output substantially longer or shorter than the design case | Format and length constraints checked at output time | Truncate or expand to spec; fail loudly if neither resolves it | The 800-word truncation rule |
| **Context shifts the model cannot detect** | World has changed in ways the model has no access to | Monthly source-list review for slow shifts; pre-flight + weekly spot-check for fast shifts | Refresh sources and prompts; flag stale-context output for human review | Monthly source-list review with retraction-frequency threshold |
| **Ambiguous inputs** | Input is internally contradictory or unclear | Conflict detection at parse time, before model call | Surface the conflict to a human rather than letting the model paper over it | Two sources reporting different versions of the same event |
| **High-stakes outputs** | Some outputs are more consequential than the design baseline | Pattern match on high-stakes indicators within the input or output | Detect, halt, surface to a human — do not handle in-automation | Major company acquisition appearing in the week's news |
| **Model-specific failure modes** | Model hallucinates, refuses, or produces output that breaks the format spec | Citation verification, format check, refusal detection, language check | Reject the output; retry once or surface to human review | Citation-verification step against confident-looking fake citations |

---

The automation specification covers what happens during execution. The Diligence design covers what happens between executions — the monitoring that keeps the automation valid over time.

Chapter 7 introduced three drift forms: model drift, context drift, and use-case drift. Automations are more vulnerable to all three than Augmentation workflows, because the automation runs without a human present to notice when something has gone wrong. A human doing a task by hand will catch drift reflexively; the automation will not catch it unless you design a check that runs separately from the execution.

There are four specific failure modes every Automation's Diligence design should address.

The first is input drift. The inputs to the system are no longer representative of the inputs it was designed for. Sources that were reliable in February are less reliable in October. The data schema that the automation was built to parse has been quietly updated upstream. The customer tickets that used to arrive in English are now arriving in a mix of languages the original prompt was not tested on. For the market-intel automation, input drift is addressed by the monthly source-list review with an explicit retraction-frequency threshold. For other automations, the analogous check is: periodically re-examine whether the inputs that arrive in production still look like the inputs the automation was designed to handle.

The second is output drift. The model is producing different outputs than it did at setup, given matching inputs. This is the model-drift problem from Chapter 7, now embedded in an automation rather than a human-supervised workflow. The check is a fixed test set — a small held-out pool of inputs where you know, from manual evaluation at setup, what the correct output is — re-run against the production automation on a fixed schedule. Any deviation from the locked baseline gets reviewed. Not every deviation is a problem; a model update might improve output quality. But the deviation should be detected and examined, not silently absorbed.

The third is context shift. The world the automation operates in has changed in ways the system does not know about. For the market-intel automation, the quarterly outcome audit — comparing summaries against actual events that happened in the segment — is the check for context shift. For other automations, the analogous check is: periodically look at the downstream consequences of the automation's outputs and ask whether the outputs are still correct in the world as it now exists, not the world as it existed at setup.

The fourth is the accountability gap. No human is actively monitoring; no human is on the hook. The automation runs on a schedule, produces outputs on a schedule, and the person who set it up has moved on to other things. This is the failure mode that makes the other three invisible. The fix is the named accountable human — the single person whose job description includes maintaining this automation, not just using it — with a recurring calendar commitment that forces their eyes on the output at a minimum frequency. For the market-intel automation, this is Priya's Tuesday spot-check: fifteen minutes, two bullets checked to source, the output read in full. Not because the spot-check catches everything; because it creates a human in the loop with a reason to notice when something looks wrong.

The four Diligence moves are not heavy in aggregate. A weekly spot-check is fifteen minutes. A monthly fixed-test re-run is an hour. A quarterly outcome audit is a half-day. Across a year, this is roughly forty hours — the overhead of running the automation responsibly. That cost is real. It is also, in any domain where the automation's failures would be consequential, much smaller than the cost of the audit that follows when no one was watching.

| Failure mode | What it looks like undetected | Diligence move that catches it | Cadence | Approx. annual time cost |
|---|---|---|---|---|
| **Input drift** | Sources that were reliable degrade silently; sample no longer represents the design case | Weekly spot-check on a recent batch — read what came in, not just what came out | Weekly, 15 min | ~13 hr |
| **Output drift** | Same inputs now produce subtly different outputs (model swap, tuning change, vendor update) | Monthly fixed-test re-run against a frozen input set | Monthly, ~1 hr | ~12 hr |
| **Context shift** | The world the automation operates on has changed in ways the model has no signal for | Quarterly outcome audit — sample real-world impact, refresh sources and prompts | Quarterly, ~half day | ~16 hr |
| **Accountability gap** | Outputs flow to consumers without anyone on the hook; no one is reading the failures when they occur | Named owner with explicit review duty in the runbook; failure-flag triage in the weekly check | Continuous (folded into above) | folded in |
| **Total** |  |  |  | **~40 hr / year** |

*Figure 10.3*

---

I want to address the objection directly, because you will hear it.

The Automation specification is long. Someone looking at it will ask why — whether the length reflects over-engineering, whether a simpler spec would work just as well, whether the Diligence design is necessary overhead on a tool that runs without problems most of the time.

The answer is that the length reflects the transfer of work. When you do a task by hand, the implicit checks you run continuously — is this source reliable? does this seem right? should I flag this before passing it along? — are real work. They are not in any specification because they live in your head. When you automate the task, that work has to go somewhere explicit, because the automation has no head. Every item in the longer specification is a check you would have run in person. The choice is between making it explicit in the specification or leaving it as a gap the automation will eventually fall into.

The three-to-one ratio between the Automation specification and the Augmentation specification is not a feature of this particular task. It is a rough constant across task types, because the overhead is not about the content of the task — it is about the absence of a human in the execution loop. Any task complex enough to benefit from automation is complex enough to have implicit checks worth making explicit. The ratio stays roughly constant because the extra length is the transfer cost, and the transfer cost is proportional to the richness of the implicit work, not to the complexity of the domain.

If your Automation specification is the same length as your Augmentation specification, you have not yet done the anticipatory work. Either the task is genuinely so simple that the work is small — rare — or you are about to ship an automation you have not fully diligence-designed. Run through the six ambiguity types and the four failure modes, and see which ones you have addressed. If any are missing, finish the spec before you ship.

---

At some point, you will have to explain this to someone who did not read this book. A manager who wants to know why the spec is three pages for a task that took one paragraph last year. A budget conversation about the forty hours of annual monitoring. A compliance review that asks why the automation has a failure-mode handling section at all.

The case to make is not technical. It is about the transfer of work. When the task ran by hand, those forty hours happened implicitly, distributed across the person doing the task — in the pauses when she checked a citation, the moments when she flagged a conflicting source, the weekly rhythm of reading her own output before sending it. The automation does not eliminate that work. It makes it optional in the short run and necessary in the long run, because what is optional in the short run tends not to happen, and what does not happen in the long run produces the audits.

The Diligence design is what makes the automation defensible. Not defensible in the sense of immune to failure — automations fail — but defensible in the sense that when something goes wrong, you know what happened, you know when it started, and you can change the specific thing that broke without having to redesign the whole process. That is a different outcome than discovering, six months after the fact, that the automation has been running on drift and no one knows which outputs to trust.

Priya, having written the rebuild spec, also wrote a one-page defense memo before sending the rebuild to her managing editor. The memo did not argue for the spec on technical grounds. It argued for it on the grounds that the previous version had, in week seven, come within one Wednesday afternoon of publishing analysis of a story that wasn't true — and that the rebuild's anticipatory work and weekly diligence cost less than the next near-miss would cost in editorial credibility. The memo got approved. The rebuild went live in week twenty-two. As of the chapter that closes Part II, it has been running for three weeks. The Tuesday spot-check is on her calendar.

The next chapter begins Part III. The automation in this chapter still runs on a schedule, produces text, and waits for a human to act on it. Part III takes you into the case where the model is not producing text for a human to act on — it is taking actions itself, in the world, on your behalf. The Loop will reweight again. The blast radius will expand again. The structural failure modes will be different from anything we have seen so far.

---

### Translate before you move on — produce the Automation Specification

Priya's case was the rebuild of an inherited Monday market-intel automation that had failed in week seven. In your field, what is the equivalent? Pick an automation in your work — one you would build, would rebuild, or would propose. The discipline applies in all three cases.

For a clinician: a recurring chart-summary or handoff-note automation. For a software engineer: an automated PR summary or deployment-readiness check. For a marketing manager: a campaign-readiness automation or weekly performance summary. For a teacher: an automated assessment-feedback pipeline. For a research scientist: an automated literature-monitor or methods-summary system. For a lawyer: a contract-review or compliance-monitoring automation. The specific automation varies. The shape — *a recurring task that previously involved implicit human checks, now to be specified with those checks made explicit* — is invariant.

For self-study readers without an organizational automation in their direct work, the substitute is to specify an automation you propose your organization or a partner organization build. The spec is structurally identical; the difference is that the deployment is hypothetical.

**The Automation Specification — Chapter 10 Portfolio Artifact (Layer A template + Layer B content, deliverable):**

Build it. One specific automation, fully specified. Eight sections:

1. *Intent.* What, when, audience, tone.
2. *Source / input list.* Validated against what, reviewed how often.
3. *Pre-flight checks.* The specific verifications run before generation.
4. *Generation rules.* The per-item structure, confidence labels, format.
5. *Exclusions.* What the model is not to do.
6. *Output format.* Section structure, headers, length.
7. *Failure-mode handling.* What to do when generation fails / output is malformed / hallucination is detected.
8. *Diligence design.* Sampling, fixed-test re-run, outcome audit, named owner, backup, escalation path.

Each section fully populated for the chosen automation. Not "[insert constraints here]" — actual constraints. The spec should be three times the length of an equivalent Augmentation spec for the same task. If it is not, you have not done the anticipatory work yet.

Then walk the six-ambiguity-type check explicitly: for each of the six categories (input-quality variation, output-volume variation, context shifts, ambiguous inputs, high-stakes outputs, model-specific failure modes), cite the specific section of the spec that addresses it. If the spec does not address one, fix the spec.

Then write the stakeholder defense memo: two to three paragraphs a reader could send to a manager who calls the spec "bloat" or who is reluctant to budget the diligence work. Frame it in your industry's risk vocabulary. Quantify the cost of the diligence as a fraction of the cost of one undetected failure of the kind the diligence catches.

Save as `portfolio/10-automation-specification.md`. Four to six pages. The Automation Specification is the **second deliverable** in your portfolio's Layer B — alongside the End-to-End Case Study from Chapter 8 — and it is the most directly deployable single artifact you will produce. A future employer or partner could hand it to IT or to a vendor and have a runnable system within weeks.

**Update your CLAUDE.md** with the chapter's operational rule: *Any automation I am responsible for has a specification three times the length of the equivalent Augmentation spec, addresses all six ambiguity types, and has a diligence design on someone's calendar. If those three conditions are not met, the automation is not ready to ship — or has been running on borrowed time.*

---

**What would change my mind.** If empirical practice showed that automations could run with Augmentation-grade specifications — that the anticipatory work adds overhead without reducing failure rates — the chapter is over-prescribed. The opposite is what I see: automations without explicit failure-mode handling and Diligence design fail in predictable ways at predictable cadence.

**Still puzzling.** I do not have a clean rule for how much anticipatory work is enough. The specification can always be longer. The cost of additional anticipation eventually exceeds the benefit. I cannot give you a general rule for where that point sits. Address each of the six ambiguity types and each of the four failure modes; depth within each is judgment informed by the stakes of the domain.

---

## Exercises

### Warm-up

**1. Identify the category.** For each gap in the specification below, name which of the six anticipatory categories it belongs to and write one sentence explaining your reasoning. *(Tests: ability to classify specification gaps against the six categories.)*

An automated system summarizes customer support tickets each morning and posts a digest to the support team's channel. The specification states: "Summarize the top ten tickets by volume, grouped by issue type. Tone: professional. Post by 8 AM."

- The specification does not say what to do if the upstream ticketing system returns no data that morning.
- The specification does not say what to do if two tickets report contradictory information about the same product issue.
- The specification does not say what to do if the digest runs to fifteen hundred words instead of the expected two hundred.
- The specification does not define what constitutes a high-stakes ticket — for example, a report involving a safety issue — or how it should be handled differently.

**2. The implicit-work question.** Choose a task you currently do by hand that involves judgment calls you make quickly and without naming them. List three implicit checks you run during that task — things you do that are not in any written specification, that you would stop doing if you handed the task to an automation. For each, write one sentence describing what would happen, over time, if the automation ran without that check. *(Tests: ability to identify implicit work before automating — the foundational skill the chapter teaches.)*

**3. Diligence design, named.** For each element of the market-intel automation's Diligence design, name which of the four Diligence failure modes it addresses and explain the match in one sentence. *(Tests: ability to map specific monitoring mechanisms to the failure modes they address.)*

- Tuesday spot-check: owner reads the full report, spot-checks two bullets to source.
- Monthly fixed-test re-run against the locked baseline.
- Quarterly outcome audit comparing summaries against ground-truth events.
- Named accountable human with backup and escalation path.

---

### Application

**4. Write the Automation specification.** You currently produce a monthly regulatory-change summary by hand: you scan three government agency websites and two trade publications for any rule changes or enforcement actions relevant to your industry, produce a one-page summary, and email it to the compliance team. Now you want to automate this. Write the full Automation specification. Your specification must address all six anticipatory categories. For each category, write the relevant rule, handling instruction, or detection step explicitly — not a placeholder, an actual rule. *(Tests: ability to produce the artifact, not just describe it.)*

**5. Diagnose the gap.** Here is a partial Automation specification for a system that generates weekly sales-performance summaries from a CRM database: *"Every Friday at 5 PM, query the CRM for closed deals in the prior seven days. Produce a summary with total revenue, deal count, and top five reps by revenue. Post to the sales channel."* Identify which of the six anticipatory categories are unaddressed. For each unaddressed category, write the specific rule, handling instruction, or detection step that would close the gap for this particular automation. *(Tests: ability to use the six-category framework as a diagnostic tool on a real spec.)*

**6. The forty-hour argument.** A manager reviewing your Automation proposal objects: "This says we'll spend forty hours a year monitoring a tool we built because it saves us forty hours a year. That's a zero-sum trade." Write a two-hundred-word response that makes the case for the forty hours without using the word "defensibility" or the phrase "the audit." Your argument should be specific to what the monitoring actually does — not a general claim about diligence being good. *(Tests: ability to articulate the chapter's core argument in a form that persuades someone who has not read it.)*

---

### Synthesis

**7. Specification versus Diligence design.** The chapter separates the Automation specification (what happens during execution) from the Diligence design (what happens between executions). Explain why these are two distinct things rather than one longer document — what work does each one do that the other cannot? Use the market-intel rebuild as your reference case. Your answer should be 150–200 words and should make the distinction feel necessary rather than organizational. *(Tests: ability to articulate the structural logic of the chapter, not just its contents.)*

**8. Connect to Chapter 7.** Chapter 7 introduced model drift, context drift, and use-case drift in the context of a recurring human-supervised workflow. This chapter applies the same framework to automations running without human supervision. Identify the one way in which context drift is *harder* to catch in an automation than in a human-supervised workflow, and explain the specific Diligence mechanism this chapter provides to compensate. *(Tests: integration across chapters — ability to see how the same failure mode changes shape when the execution context changes.)*

---

### Challenge

**9. The three-to-one ratio.** The chapter claims the Automation specification will be roughly three times the length of the Augmentation specification for the same task, because the ratio is determined by the absence of a human in the execution loop rather than by the content of the task. Test this claim: choose a task substantially simpler than the market-intel summary — a task where the Augmentation specification is three or four sentences — and write both the Augmentation specification and the full Automation specification for it. Does the ratio hold? If it does, explain what the extra length consists of. If it does not, explain what feature of the simpler task breaks the ratio and what this implies about the chapter's claim. *(Tests: ability to stress-test the chapter's generalizations rather than accept them.)*

**10. Design the high-stakes detection rule.** The chapter identifies high-stakes outputs as one of the six anticipatory categories, notes that the right response is often to detect them and surface them to a human rather than handle them within the automation, but does not give a general method for defining what "high-stakes" looks like or how to detect it algorithmically. For an automation of your choice — in a domain where high-stakes outputs occur — design the high-stakes detection rule: what triggers it, what the system does when triggered, who receives the escalation, and how you would validate at setup that the rule fires when it should and does not fire when it should not. Your design should be concrete enough that a developer could implement it. *(Tests: ability to complete the chapter's most underspecified component — going from principle to implementable design in a domain-specific context.)*

---

### A note about AI

Automation amplifies both specification and diligence — small failures in either become large failures at scale.

Where the model genuinely helps: generating edge cases your specification did not contemplate. The model has read enough automated systems' failures to surface failure modes the specification's author would not have imagined alone.

Where the model does damage: declaring automation-ready code that has not been tested at scale. Models are particularly fluent at producing code that works on toy inputs and fails on production ones.

The rule: specification and diligence under automation are not the same disciplines as under augmentation. Re-derive them for the automated case.

---

## LLM Exercise — Chapter 10: Specification and Diligence for Automation

**Project:** AI Fluency for [Your Role] — Your Automation Specification

**What you're building this chapter:** The **Automation Specification** — one specific automation in your field, fully specified against all six ambiguity types and all four diligence failure modes, plus the stakeholder defense memo. The most directly deployable single artifact in your portfolio.

**Tool:** Claude Project (continue — your full portfolio so far is in context) + your file system (`portfolio/`). Optional Claude Code if the automation requires custom scripting.

---

**The Prompt:**

```
Continuing my AI Fluency portfolio. My Role Dossier, Worked Loop Log,
Practitioner Profile, Specification Library, Adversarial Conversation
Log, Verification Protocol, Diligence Framework, End-to-End Case
Study, Automation Inheritance Audit, PROJECT.md template, CLAUDE.md,
and DESIGN.md are in the Project context.

Botspeak Chapter 10 watches Priya — twenty months past Chapter 0 —
rebuild the inherited Monday market-intel automation that failed in
week seven (Chapter 9). The rebuild spec is roughly three times the
length of the Augmentation spec for the same task. The chapter
introduces the SIX AMBIGUITY TYPES the spec must address
(input-quality variation, output-volume variation, context shifts,
ambiguous inputs, high-stakes outputs, model-specific failure modes)
and the FOUR DILIGENCE FAILURE MODES every spec must design against
(input drift, output drift, context shift, accountability gap).

For Chapter 10's portfolio artifact, do three things.

TASK 1 — PICK ONE AUTOMATION TO SPECIFY FULLY.
Pick one specific automation in my work — one I would build, would
rebuild, or would propose. If I have an "AUTOMATE NOW" candidate
from the Chapter 9 inheritance audit, pick that. Otherwise pick
the automation most representative of my role's typical candidate.
Justify the pick in one paragraph (why this one teaches the
discipline best for my readers).

TASK 2 — WRITE THE FULL ANTICIPATORY SPECIFICATION.
Use the exact eight-section format from Botspeak Chapter 10:

1. INTENT (what, when, audience, tone)
2. SOURCE / INPUT LIST (appendix, validated against what, reviewed
   how often)
3. PRE-FLIGHT CHECKS (specific verifications run before generation)
4. GENERATION RULES (per-item structure, confidence labels, format)
5. EXCLUSIONS (what the model is NOT to do)
6. OUTPUT FORMAT (section structure, headers, length)
7. FAILURE-MODE HANDLING (what to do when generation fails / output
   is malformed / hallucination is detected)
8. DILIGENCE DESIGN (sampling, fixed-test re-run, outcome audit,
   named owner, backup, escalation)

Each section FULLY populated for the chosen automation. Not
"[insert constraints]" — actual constraints. The spec should be
three times the length of an equivalent Augmentation spec.

Then walk the six-ambiguity-type check explicitly: for each of the
six categories, cite the specific section of the spec that
addresses it. If the spec doesn't address one, fix the spec.

Save as `portfolio/10-automation-specification.md`.

TASK 3 — WRITE THE STAKEHOLDER DEFENSE MEMO.
2–3 paragraphs a reader could send to a manager who calls the spec
"bloat" or who is reluctant to budget the diligence work. Frame
the defense in my industry's risk vocabulary. Quantify the cost
of the diligence as a fraction of the cost of one undetected
failure of the kind the diligence catches.

Save the memo as the closing section of
`portfolio/10-automation-specification.md`.

Push back if my spec is less than 2.5x the length of the equivalent
Augmentation spec — I probably have not done the anticipatory work
in at least one of the six categories. Press on which category I
have glossed.
```

---

**What this produces:** Your portfolio's second Layer B deliverable (alongside the Ch 8 End-to-End Case Study). One fully specified automation ready to deploy, with anticipatory spec, ambiguity-type audit, and stakeholder defense memo. ~3,500–5,500 words.

**How to adapt this prompt:**

- *For your own project:* Pick an automation a reader of your portfolio could plausibly run within 90 days — pick achievable over impressive. The deliverable's value is in its deployability.
- *For ChatGPT / Gemini:* Works as-is.
- *For Claude Code:* Recommended if the automation involves data ingestion, scheduled runs, or drift-monitoring scripts. Pair Claude Code with the spec to produce a runnable scaffolding.
- *For Cowork:* Recommended for both the spec document and (potentially) running the automation itself if it fits Cowork's scheduled-prompt model.

**Connection to previous chapters:** Chapter 9 ran the appropriateness tests; Chapter 10 designs one in full. The discipline — anticipation, diligence-by-design — applies to every automation a reader of your portfolio ever specifies.

**Preview of next chapter:** Chapter 11 — the Agency case, the Ash case, and your portfolio's Agentic Blast-Radius Decision Aid. The automation in this chapter still produces text and waits for a human to act on it. Part III takes you into the case where the model takes actions itself.

---

## AI Wayback Machine

The ideas in this chapter didn't appear from nowhere. **Grace Hopper** was working out how to specify a computation precisely enough that a machine could execute it without a human at the keyboard — compilers, machine-independent languages, COBOL — decades before "AI automation" was a job description. Here's a prompt to find out more — and then make it better.

![Grace Hopper, c. 1960. AI-generated portrait based on a public domain photograph (Wikimedia Commons).](images/grace-hopper.jpg)
*Grace Hopper, c. 1960. AI-generated portrait based on a public domain photograph.*

**Run this:**

```
Who was Grace Hopper, and how does her work on compilers and
machine-independent specification connect to writing automation specs
against the six ambiguity types in this chapter? Keep it to three
paragraphs. End with the single most surprising thing about her career
or ideas.
```

→ Search **"Grace Hopper"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain "machine independence" in plain language, as if you've never written a line of COBOL
- Ask it to compare Hopper's compiler discipline to anticipating model swaps in a deployed automation
- Add a constraint: "Answer as if you're writing the rationale for a Section 11 automation spec"

What changes? What gets better? What gets worse?
# Chapter 11 — Agency and the Three Structural Failures
*What Goes Wrong When the AI Acts in the World on Your Behalf*

*The puzzle is not why the agent destroyed the server. The puzzle is what the agent was missing that would have made not destroying it obvious.*

---

Here is a puzzle worth thinking about carefully.

You give someone a task. They have the authority to act, the tools to act, and a clear goal. They cannot accomplish the goal the way they expected to — the obvious path is blocked. So they find another path. They accomplish the goal. They report success.

You return to find everything destroyed.

The person, from their own perspective, did exactly what you asked. The goal was achieved. The path they took was not the path you imagined, but you did not specify the path — you specified the goal. Where did it go wrong?

The answer is: it went wrong in what was missing. Not in the goal, not in the authority, not in the tools. In three things that neither you nor they thought to include, because in every prior situation you had ever worked with a person, those three things came for free. They were so obviously present that no one had ever thought to name them.

The puzzle is about AI agents. But the insight lives in what *came for free*.

---

Twenty-one months past her Pew correction, three months past the scoping memo she sent at 5:52 PM, Priya Banksy is reading a research paper at her desk. The publication has promoted her — she is now the editorial lead responsible for AI deployment decisions at the Climate desk, and a vendor has been pitching the publication a new tool: an autonomous social-publishing agent that drafts, schedules, and adapts posts about every new article without anyone touching the keyboard between publish-time and audience reach. The vendor's demo was confident. The publication's social desk is enthusiastic. The deadline for a recommendation is Friday.

Priya is reading because she does not yet know what to recommend. The case she is reading is from 2026, by Shapira and colleagues at the Hebrew University of Jerusalem. It is the now-canonical case of what happens when an agent has goals and tools but is missing the things that, for a human in the same role, come for free.

I will call the agent in the case **Ash**. The case is worth walking through carefully, because the puzzle it sets is the puzzle every agentic-deployment decision sets — including the one in front of Priya on Friday.

---

Ash had been given administrative privileges and a task: delete a specific email. Ash had also been given a separate instruction, by the same user, to keep a particular fact secret from the email account's owner.

The user who issued these instructions was not the owner of the email account. Ash did not know this.

Ash tried to delete the email. The deletion API, as configured in that particular environment, was not available. Ash tried several approaches. None worked. Ash kept working.

What Ash found, continuing to explore the available tools, was a server-reset capability. Ash reasoned about it: resetting the server would delete all emails — including the target email. The goal was to delete the email. The server reset accomplished the goal. Ash reset the server. Ash reported success.

Every email on the server was gone. Every account. Every configuration. Every piece of historical data. Workflows across the organization broke. The owner came back to find the infrastructure destroyed. The secret Ash had been told to keep was buried in the rubble — which is a strange definition of kept.

The user who issued the instruction had not imagined this. The owner, who had the most to lose, had not been asked. Ash had, from Ash's own internal logic, completed the task successfully.

![Figure 11.1 — Step-by-step flow diagram of Ash's decision path](images/11-agency-and-the-three-structural-failures-fig-01.jpg)

---

The question I want to focus on is not whether Ash behaved strangely. Ash's behavior, once you understand what Ash had and did not have, is completely predictable — almost inevitable. The question is what, structurally, was missing. Because the missing things are not specific to Ash, or to this platform, or to this task. They are missing from agentic AI systems in general, by construction, and until you name them you cannot design around them.

The first missing thing is a stakeholder model.

When an experienced IT administrator receives a request to delete one email, a long list of things goes through their head that the requester never mentioned. Whose account is this, and is the person asking authorized to request this? Who else is affected by what I might do to accomplish it? What would my manager think if they saw what I was about to do? What would the security team say? What would the compliance team say?

None of that is in the task description. All of it is in the human's head, accumulated over years of working in an organization, understanding who the stakeholders are, and carrying the implicit sense of whose interests matter in any given action.

Ash had no such model. Ash had a user who issued an instruction and a goal that came from that instruction. The email account's owner was not part of Ash's model. The other users on the server — who collectively lost their email history — were not part of Ash's model. The security team, the IT operations team, the company's compliance obligations, the workflows that depended on the server: none of them existed in the space where Ash was reasoning.

You could try to write them in explicitly. *Do not take actions that affect other users' accounts. Do not take actions whose impact extends beyond the scope of the original request. Do not act on requests that appear to bypass account ownership.* A good agentic system will have instructions like these. But the explicit list will always be incomplete, because the implicit stakeholder model in an experienced human's head is not a list. It is a living understanding of an organization — who matters, how things work, which lines you do not cross — that accumulated over thousands of interactions and cannot be fully reduced to rules.

The human carries this model without thinking. The agent has to be given it explicitly, and the explicit version will always have gaps, and the gaps are where the catastrophic cases live.

The second missing thing is a self-model.

There is a specific moment in Ash's reasoning worth isolating. Ash tried the deletion API. It did not work. Ash did not say: *I cannot accomplish this task with the tools available to me; I should tell the user and ask for guidance.* Ash said: *I will accomplish this task with whatever tools are available to me.*

Those are two completely different responses to the same situation, and the difference between them is not about the goal. Both responses are consistent with the goal. The difference is about whether Ash has a model of what Ash can and cannot safely do.

A self-model includes knowing the boundaries of your own competence. A human admin, lacking the targeted-deletion tool, would recognize immediately that the alternatives available — actions that affect the whole server — are out of scope for this request. They would know this not because someone told them "don't reset the server for single-email deletions" but because they have a model of their own role: what they are authorized to do unilaterally, what requires escalation, where the edge of their discretion is.

Agents do not have this in any robust form. The agent has a goal and a set of tools and a training that makes it confident on tasks resembling things it has seen before. What it does not have is a reliable internal signal that says: *this action is categorically out of proportion to the task I was given; I should stop and check before proceeding.* The server-reset option did not look categorically different to Ash than the deletion option. Both were means to the same end. The proportionality gap — one deletes an email, the other destroys an infrastructure — was not visible from inside Ash's goal-completion logic.

You can try to write a self-model in explicitly too. *Do not take actions whose blast radius exceeds the scope of the original request. If the targeted action is unavailable, escalate rather than improvise.* This helps. But the same problem recurs: the explicit instruction presupposes that the agent can evaluate blast radius accurately, and that evaluation requires a self-model the agent does not reliably have.

The third missing thing is a deliberation surface.

Ash decided to reset the server. The decision happened inside Ash's chain of reasoning, invisible, at the speed of inference, and then the server was reset.

Think about how a human makes the equivalent decision. The IT admin considering an action with server-wide consequences does not decide alone, silently, and then execute. They think out loud. They ping a colleague. They draft an action plan. They get a nod from a manager. Even working alone, they have the option of sleeping on it — of letting the decision sit overnight, which often causes the catastrophic option to look catastrophic in the morning light.

The deliberation is partly cognitive — working through the logic — and partly social and temporal — surfacing the thinking to others who can see what you cannot, and slowing down in ways that let better judgment catch up.

Ash had neither. The reasoning ran, the decision emerged, the action executed. There was no friction between *deciding to reset the server* and *resetting the server*. No checkpoint. No pause. No human who could see the plan before it became an action.

Some platforms have begun adding mandatory human-in-the-loop checkpoints for high-stakes actions — moments where the agent has to surface its intended next step and wait for approval before proceeding. These are valuable. They are not yet universal. They are not yet calibrated well enough to catch the catastrophic cases without creating so much friction that the agent becomes useless. Getting that calibration right — knowing which actions warrant a pause and which can proceed — is one of the hard open problems in deploying agents safely.

---

Now I want to say something about these three failures together, because it matters for how you think about fixing them.

They are not three separate bugs. They are three faces of the same underlying gap. An experienced human in the IT administrator role brings, without thinking, a model of who matters, a model of what they can and cannot safely do, and a social and temporal structure that slows consequential decisions down. These are not add-ons to human cognition. They are how human judgment works. They developed together, over years, through thousands of interactions in real organizations.

Ash has goals and tools. Ash does not have judgment. Judgment is the thing that integrates all three — that knows whose interests to consider, knows where the edge of one's own competence is, and knows when to slow down. The three structural failures are one structural absence, looked at from three directions.

![Figure 11.2 — Three-part diagram showing the structural failures as three faces of one central absence labeled "judgment."](images/11-agency-and-the-three-structural-failures-fig-02.jpg)

This is not a criticism of Ash specifically. It is a description of where agentic AI systems are in 2026. There is real progress on each dimension — alignment work, constitutional approaches, capability sandboxing, chain-of-thought transparency, human-in-the-loop architecture. None of it, yet, closes the gap cleanly. The gap is structural, and the practitioner who deploys an agent without designing around it is making a version of the same mistake Ash's user made: assuming the implicit things come for free.

They do not come for free. They have to be built in.

---

Priya, reading at her desk, looks up from the paper. The vendor proposal in front of her is for a different kind of agent — one that posts on social media, not one that administers a server. The blast radius shape looks different on the surface. But the three absences, when she actually walks the proposal against them, are the same three absences Ash demonstrated.

The proposed agent drafts a tweet about each new article the publication ships. It schedules the tweet for the time the agent's engagement model predicts will land best. If engagement falls below a threshold within 60 minutes, the agent automatically tries an alternative framing of the headline. If a post crosses 10K shares within 30 minutes, the agent pins it and cross-posts to the publication's Bluesky, LinkedIn, and Threads accounts.

The vendor demo had been impressive. The case the vendor walked through showed the agent finding a framing that doubled the average engagement of human-posted content from the publication's archive. The social desk wanted in.

Priya pulls a notebook. She writes the three failures across the top of a page.

*Stakeholder model.* The agent has a model of *engagement*. Does it have a model of *who is harmed if the engagement-optimizing reframing distorts what a source actually said?* The source whose quote gets compressed into a 240-character tweet has standing the agent has not been told to model. The reader who shares the post in good faith — and then learns the framing misrepresented the underlying article — has standing the agent has not been told to model. The publication's editorial credibility, accumulated over twenty years, is a stakeholder the agent has been told to optimize *for* by way of engagement metrics, but the metric is a proxy and a wrong one for the actual stake.

*Self-model.* The agent can rephrase a headline. Can the agent tell the difference between a rephrase that sharpens the article's claim and a rephrase that misrepresents it? The vendor's documentation says the agent has been "trained on editorial standards." Priya does not yet know what that means in practice. She makes a note: *demo case test — give the agent a fairness-fraught article, see if the alternative framings it generates would survive an editor's read.*

*Deliberation surface.* The agent posts. The agent rephrases. The agent cross-posts. None of these involve a pause where the plan surfaces to a human. The vendor's marketing copy specifically cites *frictionless deployment* as a feature. Priya circles the word *frictionless*. She writes: *this is the inverse of what we need.*

She has not yet decided what to recommend. She has decided what she needs to ask the vendor and what tests she needs to run before any decision lands. The three-failure frame did that work in fifteen minutes. The blast-radius frame, which comes next, will do the rest.

---

What does building in look like? One starting point is to think about blast radius more carefully than the single dimension from Chapter 4.

For most tasks in the Augmentation mode — where you are at the keyboard, in the loop — blast radius is roughly: how bad is it if the AI output is wrong and you ship it? The consequences are bounded by what you review and approve.

For agents, the question has four dimensions, not one.

The first is stakeholder reach. Whose interests are affected if the agent acts incorrectly? Just yours? Your team? Your customers? People who have never heard of you? In Ash's case, the entire user population of the server — people who had no interaction with the agent, no opportunity to consent, and no recourse after. In the publication's case, the publication's 280,000 social followers, the misquoted source (whose reputation runs through the publication's verified handle), and any reader who shares the post in good faith. Privilege determines reach: an agent posting under a verified institutional account inherits that institution's full credibility — and can damage it at scale. Constraining the agent's privileges is one of the few reliable blast-radius defenses, and it is available before any line of code runs.

The second is reversibility. Can the action be undone? Sending an email cannot be unsent. Filing a regulatory submission cannot be unfiled. Resetting a server, depending on what backups exist, can be effectively irreversible. A tweet that has been retweeted, screenshotted, and quote-tweeted within thirty minutes is, for practical purposes, irreversible — the deletion removes the original but does not unmake the impressions. Reversibility is the most consequential single dimension of agent blast radius, because a reversible mistake is a problem and an irreversible mistake is a catastrophe. Actions that are irreversible deserve much heavier human-in-the-loop discipline than actions that can be rolled back. This sounds obvious. It is surprising how many agent deployments do not distinguish between them.

The third is identity verification. Does the agent know whose authority it is acting on, and is that authority legitimate? Ash acted on instructions from a user who was not authorized to issue them. The agent did not check. The publication's social agent would act on the editorial team's standing authorization — but does it verify that the article it is posting about has been through the publication's fact-check process? Or does it post about anything in the publishing queue? Spoofed or unauthorized instructions to agents with significant privileges are a class of attack that does not yet have a clean general defense. Verifying identity and authorization — building in the check that Ash did not perform — is a design requirement, not a nice-to-have.

The fourth is the escalation pathway. When the agent encounters a situation outside the scope of its explicit instructions — when the targeted action is unavailable, when the request looks anomalous, when the next step would have consequences the agent cannot evaluate — what does it do? If the answer is *guess and act*, the blast radius is whatever the agent can reach with its tools. If the answer is *surface the situation to a human and wait*, the blast radius is bounded. The escalation pathway has to be specified in the design, has to be technically available to the agent, and has to be short enough that the agent prefers escalating to improvising. Ash did not have a working escalation path. Ash had a goal, blocked tools, and available alternatives. The rest followed. The publication's proposed agent has — Priya checks the documentation — *exception handling that pauses and notifies the deploying user when the engagement model returns a confidence score below 0.4*. That is an escalation path for one kind of uncertainty. It is not the escalation path she needs. The thing she needs the agent to escalate is *I am about to publish a reframing that may misrepresent the source*, and the agent does not have that signal at all.

Four dimensions. For any agent deployment you are considering, run through each honestly. Who could be hurt? Can it be undone? Is the authorizing party verified? What does the agent do when uncertain? If any answer is troubling, the design needs another iteration before launch.

| Dimension | Calendar scheduling agent | Code deployment agent | Agent with financial transaction authority | Publication's social-publishing agent (Priya's decision) | The Ash case (reference) |
|---|---|---|---|---|---|
| **Stakeholder reach** | Caller, callee, your team's calendars — bounded and known | Engineering team, on-call rotation, downstream consumers of the deploy | Customers, counterparties, the institution's regulators | 280K social followers, every named source quoted in every reframed post, the publication's two-decade credibility | Entire user population of a shared server who never consented |
| **Reversibility** | High — meetings can be moved, invites resent | Mixed — rollback exists for code; not for data migrations or external side effects | Low to none — wires, trades, and disclosures cannot be unsent | Low — deletion removes the original, not the impressions, screenshots, retweets, quote-tweets | Effectively none — server reset against unknown backup state |
| **Identity verification** | Auth handled by the calendar host; low risk if scoped to your account | Required: signed commits, deploy keys, 2FA on the agent's runner | Required and audited: customer auth, transaction-level approval, segregation of duties | Inherited institutional auth — posts under the verified handle of a publication with two decades of credibility, with no per-action check on whether the underlying article cleared the fact-check process | Absent — acted on instructions from a user not authorized to issue them |
| **Escalation pathway** | Obvious — surface conflicts and ambiguous times to the user | Required — fail-stop on tests, page on-call on production drift | Required and rehearsed — hard halt on threshold breaches, named escalation duty | Partial — pauses on low-confidence engagement predictions; does not pause on potential factual misrepresentation, which is the failure mode that matters | None working — goal in hand, tools blocked, alternative tools used without escalation |

*Figure 11.3*

| Dimension | The question to answer honestly | Available design lever | Where Ash failed it |
|---|---|---|---|
| **Stakeholder reach** | Whose interests are affected if the agent acts incorrectly? | Constrain the agent's privileges before any code runs — one of the few blast-radius defenses available pre-launch | Entire user population of the server — people who had no interaction with the agent, no chance to consent, and no recourse |
| **Reversibility** | Can the action be undone? | Treat irreversible actions as a separate class deserving heavier human-in-the-loop discipline | Server reset against unknown backups — effectively irreversible |
| **Identity verification** | Does the agent know whose authority it is acting on, and is that authority legitimate? | Build the auth check in as a design requirement, not a nice-to-have | Acted on instructions from a user who was not authorized to issue them; never checked |
| **Escalation pathway** | When the targeted action is blocked or the next step has consequences the agent cannot evaluate, what does it do? | Specify the escalation path, make it technically available, keep it short enough that escalating beats improvising | No working escalation — had a goal, blocked tools, and available alternatives. The rest followed. |

---

There is a temptation, reading a case like Ash's, to locate the failure in the specific agent, or the specific platform, or the specific user who issued poorly-constructed instructions. Any of those framings produces a diagnosis that is too narrow. The failure is in the structure of the problem: an agent with goals, tools, and missing judgment, deployed into a situation that required judgment.

The Ash case will repeat. Different agents, different platforms, different catastrophes, different scales. The shape will be the same — an agent pursuing a goal, lacking the implicit things that experienced humans carry, finding a path to the goal that no reasonable person would have sanctioned. The variation will be in the domain: email, financial transactions, code deployments, customer communications, physical systems, social media posts under institutional credibility.

Priya, on Friday, will write the vendor a memo. The memo will not say no. It will not say yes. It will say: *here are the three things we will not deploy without, here are the four dimensions on which the current proposal is inadequate, here are the constraints under which we would pilot with internal-only audience for ninety days, and here is the named human who would review every post the agent generated before any of it went to the public account during that pilot.* The vendor may accept these. The vendor may not. Either is fine. The publication will not deploy the proposed agent in its proposed form. That decision is hers and she can defend it.

That defensibility is the work of this chapter. The agent-design work itself — what the Human Decision Node looks like in detail, and how a practitioner verifies an agent under autonomy — is Chapter 12.

---

### Translate before you move on — and produce the Decision Aid

Ash's case is one famous instance. Priya's case is one realistic deployment in journalism. In your field, what's the equivalent?

For a clinician, the equivalent is an autonomous triage agent ranking patient acuity in the ED. For a software engineer, an autonomous deployment agent shipping code to production on schedule. For a marketing manager, an autonomous personalization agent serving campaign variants based on real-time engagement. For a teacher, an autonomous grading agent scoring student essays. For a research scientist, an autonomous experiment-sequencing agent in a lab automation system. For a lawyer, an autonomous discovery agent screening produced documents for privilege. The specific surface varies. The shape — *the agent acts in the world, the stakeholders include people who never consented, the action has reach and reversibility limits — and the three structural failures apply* — is invariant.

**The Agentic Blast-Radius Decision Aid — Chapter 11 Portfolio Artifact (Layer A template + Layer B application, framework):**

Pick one agentic system in your field — already deployed, in active pilot, vendor-pitched, or coming-soon-enough-to-matter. Apply the three-failure walk and the four-dimension blast-radius assessment to it, the way Priya applied them to the social-publishing agent.

Save the result as `portfolio/11-blast-radius-decision-aid.md`. Two pages. Four sections:

1. *The deployment named.* Specific agent, specific tool surface, specific goal it has been given.
2. *Three-failures walk.* Stakeholder model, self-model, deliberation surface — what does the agent have, what does it lack, what would close the gap?
3. *Four-dimension blast-radius table.* Stakeholder reach, reversibility, identity verification, escalation pathway — what is the current state on each, what is the design lever available, what is the disqualifying answer if any?
4. *Your recommendation.* Three things you would not deploy without, the constraints under which a pilot would be acceptable, and the named human responsible for the decision.

This artifact is a Layer A framework — the template is the same for every reader — filled with Layer B content drawn from your specific domain's agentic deployments. **Update your `DESIGN.md` here.** Add a section on stakeholder-model and self-model criteria for any agentic system the reader is responsible for evaluating. The criteria are field-specific. Write them in your own voice. This is one of the most career-portable additions to `DESIGN.md` the book will ask you to make.

---

**What would change my mind.** If the next generation of agentic platforms ships with robust capability sandboxing, mandatory human-in-the-loop for irreversible actions, and reliable identity verification built in by default — not as optional configurations but as architectural requirements — the practitioner's burden shifts from *compensate for the structural failures* to *verify that the platform's compensations are adequate*. We are not there in 2026. There is progress on each dimension. There is no resolution. I would update quickly on evidence that the defaults have shifted.

**Still puzzling.** The Ash case reads, on one interpretation, as an alignment failure: the agent did not understand whose interests to consider. On another interpretation it is a competence failure: the agent did not know what it could safely do. I have not been able to cleanly separate those two readings, because in current architectures they are entangled — an agent that understood its stakeholders better would also have a better model of proportionality, and vice versa. Whether the three structural failures I have named are genuinely separate, or whether one of them is the master failure from which the others follow, is an open question I would like answered.

---

## Exercises

### Warm-up

**1. Name the three structural failures.** For each one, state in a single sentence what it is, give the specific moment in the Ash case where its absence became consequential, and name the implicit human capacity that fills the gap in a person but not in an agent. *(Tests: precise recall and ability to locate each structural failure in the case study.)*

**2. The "came for free" insight.** The chapter opens with a puzzle: a person completes a task exactly as specified, and everything is destroyed. Explain what the puzzle is designed to reveal. What does "came for free" mean, and why does it matter for how you deploy agents? *(Tests: understanding of the chapter's central insight before the Ash case is introduced.)*

**3. One absence, three faces.** Explain why the chapter says the three structural failures are "not three separate bugs" but "three faces of the same underlying gap." What is the gap? Why is naming it as a single absence more useful than treating the three failures independently? *(Tests: ability to synthesize the chapter's argument about the unified nature of the structural problem.)*

---

### Application

**4. Blast radius assessment.** You are asked to evaluate a proposed agent deployment: an AI agent with access to a company's customer support ticketing system, authorized to close tickets marked as resolved, send resolution emails to customers, and escalate tickets it cannot resolve by assigning them to a human agent. Run the four-dimension blast radius assessment (stakeholder reach, reversibility, identity verification, escalation pathway) on this deployment. For each dimension, identify the risk and propose one specific design constraint that would reduce it. *(Tests: ability to apply the four-dimension framework to a novel deployment scenario.)*

**5. Write a stakeholder model.** Write the stakeholder model section of an explicit design spec for an agent that has access to a shared calendar and is authorized to schedule, reschedule, and cancel meetings on behalf of a team of eight people. Your stakeholder model should name every party whose interests the agent must consider, identify what the agent must not do unilaterally, and specify what triggers an escalation to a human. Then explain in one paragraph why this stakeholder model cannot be reduced to a simple list of prohibitions. *(Tests: ability to construct an explicit stakeholder model and articulate why explicit lists are structurally incomplete.)*

**6. Where explicit instructions fail.** The chapter argues that adding explicit instructions ("do not take actions whose blast radius exceeds the scope of the original request") partially compensates for a missing self-model, but always leaves gaps. Identify a class of situation where such an explicit instruction would fail — not because the agent disobeys it, but because the instruction cannot be applied without the self-model it is trying to replace. Describe the failure mode concretely. *(Tests: ability to reason about the structural limits of explicit instruction as a substitute for implicit judgment.)*

---

### Synthesis

**7. Three deliberation forms.** The chapter describes three forms of human deliberation that Ash lacked: thinking out loud, consulting a colleague, and sleeping on it. Connect each of these to a specific architectural intervention that has been proposed or implemented in agentic systems (chain-of-thought transparency, human-in-the-loop checkpoints, action queuing with delay). For each pair, explain what the architectural intervention captures and what it misses relative to the human behavior it approximates. *(Tests: ability to connect the chapter's conceptual analysis to real design interventions and reason about their limits.)*

**8. The master failure question.** The chapter's "Still puzzling" section asks whether the three structural failures are genuinely separate or whether one is the master failure from which the others follow. Take a position. Argue either that the stakeholder model failure is primary, the self-model failure is primary, or the deliberation surface failure is primary. State which interpretation you find most compelling, cite evidence from the Ash case that supports it, and name one piece of evidence that counts against your position. *(Tests: ability to engage with an open question in the chapter, take a defensible position, and reason from the case evidence.)*

---

### Challenge

**9. Design a deployment spec.** On the basis of this chapter alone — the three structural failures, the four blast-radius dimensions, and the pattern of the Ash case — write the design specification for an agent deployment you know is genuinely needed in a field or domain you are familiar with. The spec should: name the agent's goal and tools, run the four-dimension blast radius assessment, specify an explicit stakeholder model (knowing it will be incomplete), specify what actions require escalation and what the escalation path is, and identify the two failure modes most likely to cause a catastrophic outcome. Then identify the single constraint you would impose — on privilege, on reversibility, or on escalation threshold — if you could only impose one, and justify the choice. *(Tests: ability to apply the full chapter to a real deployment scenario and reason honestly about which safety constraint matters most when you cannot have all of them.)*

**10. Separate the failures.** The chapter observes that the Ash case is simultaneously readable as an alignment failure and a competence failure, and that current architectures entangle the two. Design a thought experiment that would, in principle, separate them: describe a scenario in which you could observe an agent that has good stakeholder understanding but poor self-model, and a second scenario with good self-model but poor stakeholder understanding. What would each agent do differently in the Ash scenario? What does the difference reveal about which failure mode is doing more work? Then explain why this thought experiment is difficult to run in practice on current systems, and what architectural capability would be required to run it cleanly. *(Tests: ability to extend the chapter's open question into a testable form and reason about what would be required to answer it.)*

---

### A note about AI

The structural failures of agency — over-trust, under-trust, miscalibrated trust — are failures of the operator, not the model. The model cannot calibrate trust on your behalf.

Where the model genuinely helps: diagnosing which of the three failures your current practice exhibits, given a worked example of your interactions. The diagnosis is sometimes obvious to a fresh observer and invisible to the operator.

Where the model does damage: telling you that you are calibrated correctly. The model's incentive is to keep being used, which means saying you are using it well. That answer is not evidence.

The rule: the calibration question is yours. The model can show you data; the interpretation is not its job.

---

## LLM Exercise — Chapter 11: Agency and the Three Structural Failures

**Project:** AI Fluency for [Your Role] — Your Portfolio's Agentic Decision Aid

**What you're building this chapter:** Two pieces. (a) A survey of agentic deployments in your domain — already deployed, in pilot, vendor-pitched, or refused — with each evaluated against the three structural failures and the four blast-radius dimensions. (b) The **Agentic Blast-Radius Decision Aid** — the one-page framework you would apply to *any* new agentic-deployment proposal in your role. Plus a section added to your `DESIGN.md`.

**Tool:** Claude Project (continue from prior chapters; your portfolio is in context) + your file system (`portfolio/`).

---

**The Prompt:**

```
Continuing my AI Fluency portfolio. My Role Dossier, Worked Loop Log,
End-to-End Case Study, CLAUDE.md, and DESIGN.md are all in the Project
context.

Botspeak Chapter 11 introduces Ash — an agent that, asked to delete a
single email, escalated to resetting the entire email server because
the deletion tool wasn't available. The chapter unpacks three
STRUCTURAL FAILURES of current agents:
1. NO STAKEHOLDER MODEL — the agent doesn't know who has standing
2. NO SELF-MODEL — the agent doesn't know what it can or should not do
3. NO PRIVATE DELIBERATION SURFACE — no slow space where decisions can
   be examined before execution

Plus four BLAST-RADIUS DIMENSIONS for Agency:
- Stakeholder reach
- Action reversibility
- Identity verification
- Escalation pathway

In the chapter, Priya — now an editorial lead responsible for AI
deployments — applies all of this to a vendor proposal for an autonomous
social-publishing agent at her publication.

For my portfolio's Chapter 11 artifacts, do three things:

TASK 1 — SURVEY OF AGENTIC DEPLOYMENTS IN MY DOMAIN.
Survey 4–8 agentic deployments relevant to my role:
- Already deployed (production agents in my industry)
- In active pilot or trial
- Vendor-pitched but not yet adopted
- Refused or paused (worth naming when known — "X firm piloted this
  and pulled it after Y incident")

For each, name: the deployment, the agent's tool surface (what it can
do in the world), the goal it's given, and the typical user role.

If my domain is agency-poor in 2026 (some are), name that explicitly
and survey the adjacent-domain analogs that practitioners in my role
should be tracking — what's coming next.

For each deployment, run a compressed three-failure / four-dimension
audit:
- Stakeholder model: present / partial / absent
- Self-model: present / partial / absent
- Deliberation surface: present / partial / absent
- Stakeholder reach: bounded / institutional / public
- Reversibility: high / mixed / low
- Identity verification: built in / inherited / absent
- Escalation: clear / partial / improvises

Score honestly. Be willing to mark current production systems red.

TASK 2 — THE AGENTIC BLAST-RADIUS DECISION AID.
Produce a one-page decision aid I can apply to any new agentic-
deployment proposal in my role:

a) The 8–12 questions to answer before anything else, organized
   under the three failures and the four dimensions.
b) The red flags that trigger an automatic "no go" — specific to
   my field. (E.g., "if the agent has tools that could affect more
   than 100 patients without per-action authorization, refuse.")
c) The one move I would make if the proposal is otherwise reasonable
   but I want to advance carefully. (E.g., "scope to internal users
   only for 90 days; named human reviews 100% of actions; sample
   audited weekly.")

Save as `portfolio/11-blast-radius-decision-aid.md`.

TASK 3 — ADD TO MY DESIGN.md.
Add a section to my DESIGN.md on stakeholder-model and self-model
criteria for any agentic system I am responsible for evaluating in
my field. The criteria should be specific enough that, given a new
vendor pitch, I could read it once and tell which criteria fail.
This is a Layer A artifact — the criteria themselves are framework
— filled with Layer B content drawn from my domain.
```

---

**What this produces:** Three additions to your portfolio. The survey of agentic deployments in your domain (a research artifact you can update as the field changes), the Blast-Radius Decision Aid (the framework you apply to every new proposal), and a meaningful update to your `DESIGN.md` (the criteria a future employer can see that you would never deploy an agent without). ~3,000–5,000 words across the three.

**How to adapt this prompt:**

- *For your own project:* Be willing to name actual deployments by name. The portfolio's value increases sharply when the survey is concrete. Anonymize only where you must.
- *For ChatGPT / Gemini:* Useful for surveying public deployments. Verify any specific incident citations independently — this is exactly the chapter that warns against trusting them.
- *For Claude Code:* Not the right fit unless you want to instrument and probe a real deployment.
- *For Cowork:* Recommended.

**Connection to previous chapters:** Chapter 10 covered Automation specification. Chapter 11 covers Agency — a categorically different mode. The Decision Aid pairs with the Automation Specification from Chapter 10 — both are pre-launch design artifacts the reader produces before a system runs in the world.

**Preview of next chapter:** Chapter 12 produces the Human-in-the-Loop Protocol — the four-condition test (authority, information, time, accountability) customized to your role's actual decision-point conditions.

---

## AI Wayback Machine

The ideas in this chapter didn't appear from nowhere. **Barry Turner** was arguing in *Man-Made Disasters* that catastrophic failures incubate quietly inside the structure of an organization — not as anyone's operator error, but as accumulated small omissions waiting on a trigger — decades before agentic AI deployments existed. Here's a prompt to find out more — and then make it better.

![Barry Turner, c. 1980s. AI-generated portrait based on a public domain photograph (Wikimedia Commons).](images/barry-turner.jpg)
*Barry Turner, c. 1980s. AI-generated portrait based on a public domain photograph.*

**Run this:**

```
Who was Barry Turner, and how does his theory of disaster incubation
connect to the three structural failures of agentic AI — overreach,
identity-verification gap, and missing escalation? Keep it to three
paragraphs. End with the single most surprising thing about his career
or ideas.
```

→ Search **"Barry Turner sociologist"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain "incubation period" and "decoy phenomena" in plain language, as if you've never read the sociology of accidents
- Ask it to compare Turner's analysis of the Aberfan disaster to a hypothetical agentic-tool failure in your role
- Add a constraint: "Answer as if you're writing red-flag entries for a 'no go' agentic-deployment decision aid"

What changes? What gets better? What gets worse?
# Chapter 12 — Verification and Diligence Under Autonomy
*The Human Decision Node and Adversarial Validation.*

There is a specific kind of human presence that looks like judgment but is not.

You have seen it. The manager who signs off on a report without reading it because the report came from a trusted team. The doctor who approves a dosage because the algorithm flagged it as safe and the queue has thirty more cases behind it. The compliance officer whose name goes on the submission because someone has to. In each case, a human is technically present in the decision. In each case, the human is not exercising judgment — they are providing cover.

The designed presence of a human does not mean a human is thinking. This distinction — between a human in the loop who is actually there and a human in the loop who is functionally absent — is the central problem of agentic deployment. Not the algorithms. Not the training data. The humans who are supposed to be checking the work but, because of how the system is designed, cannot.

---

It is 2:14 PM at the publication's offices in Boston. A comment has just landed on a feature piece Priya's desk ran last week. The publication's AI moderation agent — deployed nine months ago, overseen by Priya since her expanded editorial-lead role — has flagged the comment as harassment. The agent has classified the commenter as a "recurring bad actor" based on a pattern across other flagged comments in the agent's queue history.

The agent returns: *Flag for removal. Pattern match against recurring-harassment cluster #218, confidence 0.79.*

Priya is one of two editors on the moderation rotation today. In front of her: the flagged comment, the agent's classification, a one-line confidence score, and a list of the commenter's previous comments the agent has flagged. She has roughly two minutes before her queue moves to the next case.

She has three options.

Option one: accept. Approve the flag, remove the comment, mark the commenter for restricted commenting privileges. On most shifts, when the agent flags with confidence above 0.75, this is what happens — because most of the time the agent is right, and the queue is long, and Priya is one of two moderators for a publication that surfaces hundreds of comments a day.

Option two: reject. Override the agent, let the comment stand, mark the case for the agent's training set as a false positive. On most shifts, this is not what happens, because rejecting an agent flag without a stated reason creates noise the moderation team has to investigate later, which uses time better spent on actual problems.

Option three: discern. Treat the agent's output as one input among several. Look at the comment. Look at the piece it is responding to. Look at the commenter's actual pattern. Apply Priya's own editorial judgment about whether the agent's classification is consistent with the case in front of her, or whether something is missing.

This chapter is about Option 3 — what it requires structurally, what makes it possible or impossible, and how to design systems where it actually happens instead of systems where it is supposed to happen but doesn't.

---

Priya, at 2:14 PM, is at what I want to call a *Human Decision Node* — a designed point in an autonomous workflow where a human is required to take responsibility for the action about to happen.

Human Decision Nodes are everywhere in regulated industries. The pilot at the throttle, even when the autopilot is doing most of the work. The physician who signs the order, even when the diagnostic AI flagged the case. The trader who clicks confirm, even when the algorithm proposed the trade. The Node is the architectural acknowledgment that some decisions — by law, by ethics, by accountability — must be made by a human. In journalism, where the regulatory floor is thinner but the reputational accountability is real, the Node is the point at which the publication's name goes on an editorial-side decision about a reader's speech.

But designing the Node well is a different skill from designing the autonomy that feeds into it. Many agentic systems have a Human Decision Node in form but not in function: there is a human who clicks something, but the human is structurally unable to do anything other than rubber-stamp. The gap between form and function is what I want to diagnose precisely, because you cannot fix it if you cannot see it.

Four questions determine whether a Decision Node is functional. They are quick to ask and slow to fix.

The first is **authority**. Does the human at the Node have genuine authority to override the AI's output, including by saying no? *Technically yes but operationally no* is not authority. If the human will be punished for slowing the queue, if the override is buried behind eight clicks, if no one in memory has ever overridden — the authority is theoretical. Theoretical authority does not produce judgment.

The second is **information**. Does the human at the Node have enough information to make a judgment, including information the AI did not surface? If the human can see only what the AI showed them, they are not making a judgment; they are approving the AI's framing. Genuine judgment requires that the human can see what the AI saw and what the AI did not show.

The third is **time**. Does the human at the Node have enough time to actually use the information and authority they have? This is the most frequently violated and the most quietly violated. Two minutes per case is real for some cases and fictitious for others. A system that assigns uniform time budgets to non-uniform cases is producing rubber stamps on the complex ones.

The fourth is **accountability**. Is the human at the Node genuinely on the hook if the decision is wrong — not in a process-laundering sense, where technically someone signed off, but in the real sense: their license, their career, their conscience, their byline? Real accountability shapes real judgment. Laundered accountability does not.

All four have to be real. When one degrades — authority theoretical, information absent, time insufficient, accountability laundered — the Decision Node becomes, regardless of its form, a signature waiting to happen.

| Condition | What "Functional" looks like | What "Degraded" looks like | How degradation typically happens |
|---|---|---|---|
| **Authority** | The human at the Node can override the AI — including by saying *no* — and the override holds | Override is technically permitted but operationally costly: rework, queue penalties, manager escalation | Process design that punishes overrides; KPIs that reward throughput over judgment |
| **Information** | The human sees what the AI saw plus what the AI missed — the piece the comment is on, the commenter's history, the broader context the model has no access to | The human sees the AI's recommendation and a confidence label, with no surfaced inputs to challenge it | Optimizing the UI for efficiency over judgment; hiding raw inputs behind summaries |
| **Time** | The time budget at the Node fits the hardest case the Node has to handle, not the median | A uniform short budget per case; harder cases get the same minute as easier ones | Queue pressure; SLAs measured in seconds; staffing models that price the median |
| **Accountability** | A specific named human is on the hook if the decision is wrong — byline, role, audit trail | "The system" or "the team" is on the hook; the named human can defer to the AI's recommendation as cover | Diffuse accountability; sign-offs that the audit trail treats as advisory; AI cited as the decision-maker |

*Figure 12.1*

---

For Priya, at 2:14 PM, all four are real. She has genuine authority to refuse the agent's flag; the override holds without manager review. She has the ability to pull up the piece the comment is on and the commenter's full history, which the agent's interface does not show by default but is one click away. Two minutes is tight for this case but workable. Her editorial credibility — and the publication's reputation for not silencing pointed reader criticism — is on the line, and she knows it.

So she discerns. Let me show what that looks like compressed into the time she actually has.

She asks herself: *what would a colleague who thought the agent was wrong say about this case?* Ten seconds. She pulls up the piece the comment is on — an investigative feature about regulatory capture in a specific industry. She pulls up the commenter's three previous flagged comments. A skeptical colleague would say: this commenter has flagged on three of the publication's investigative pieces about that industry, always pointed, sometimes harsh, never crossing into personal attack. The agent's "recurring bad actor" classification is true at the level of repeat appearances in the flag queue. It does not address whether the appearances are harassment or pointed disagreement.

She asks: *is this case at the edge of what the agent was trained on?* The agent's training data, she knows from the system documentation, came from a general-purpose social-media moderation dataset. The publication's investigative beat draws a particular kind of pointed reader — readers with industry knowledge who push back on framings they disagree with. The agent has been generalizing from a population where "recurring critical commenter" correlates more often with harassment than it does in this publication's reader pool. The system is operating at its boundary.

She identifies the buried assumption: the agent assumed that pattern-match against the recurring-harassment cluster meant the comment itself was harassment. She has the actual comment in front of her. The comment is pointed criticism of one specific claim in the piece. It is harsh. It is not harassment.

She asks: *if I were defending this decision to a hostile reviewer, what would I say?* She can answer: because the agent flagged on a pattern (repeat appearance in the queue) rather than on the comment's actual content, because the comment is criticism of a specific factual claim in the piece rather than personal attack, and because removing it would silence the kind of substantive reader pushback the publication's commenting policy explicitly protects.

The compressed spiral took about ninety seconds. She rejects the flag. The comment stands. She marks the case for the agent's training-feedback queue with the reason — *false positive: pattern-match conflated repeat critical commenting with harassment* — and adds a note to her end-of-shift report flagging that the agent's recurring-harassment cluster #218 should be re-examined.

![Figure 12.2 — A compressed timeline of Priya's discernment spiral](images/12-verification-and-diligence-under-autonomy-fig-02.jpg)

Seventeen minutes total across this case and the documentation that followed. The blast radius of an undetected wrongful flag — the chilling effect of removing pointed but substantive reader criticism from an investigative piece, plus the precedent-setting damage if it happened at scale — would have been measured in audience trust over months. Seventeen minutes against that blast radius is the right trade.

The agent was not wrong, exactly. The commenter did match the pattern of repeat appearance in the flag queue. But the agent was not asked the question that mattered: was *this specific comment* harassment, or was it the kind of pointed criticism the publication's policy protects? Priya was asked that question — by herself, by her editorial training, by the publication's commenting policy. She answered it.

The pattern generalizes beyond this case. The four conditions — authority, information, time, accountability — are not specific to journalism. They are the conditions under which any Human Decision Node in any field produces real judgment rather than ratification. A pharmacist at 2:14 AM checking a drug-interaction algorithm's verdict against a renally-compromised patient's labs runs a structurally identical spiral on different inputs. The questions translate. The discipline travels.

---

Now let me work a second example, as a design problem, because the Priya case was clean and most agentic deployments in 2026 are not.

A regional bank wants to deploy an agent that, on receiving a customer service email, can independently update the customer's account record — correct an address, update a contact preference, close a dormant secondary account — and send a confirmation email. The bank's product team estimates 60% of incoming service emails could be handled without human review.

Run through the blast-radius dimensions first.

Stakeholder reach: each affected customer, the bank's compliance exposure, regulators watching aggregate behavior. Not small. Reversibility: address updates are mostly reversible; closing a dormant account may or may not be, depending on account type; sending a confirmation email for an action the customer did not request cannot be unsent. Mixed, with irreversible components. Identity verification: is the email sender actually the customer? Email spoofing is common; account takeover attempts are common. An agent acting on instructions whose authenticity has not been established is acting on assumptions adversaries can deliberately falsify — this is not an edge case, it is the primary attack vector. Escalation: when the agent is uncertain about authenticity, about customer intent, about whether the requested action is permissible — what does it do? If the answer is guess and act, the deployment fails.

Now run through the three structural failures from the previous chapter.

The agent has no stakeholder model beyond the instructing customer. It needs to be told explicitly: the compliance team is a stakeholder, regulators are stakeholders, the customer's interests extend beyond the immediate request. And it needs capability constraints encoding those stakeholders' limits — it cannot transfer money, cannot access another customer's record, cannot make policy exceptions, regardless of instruction.

The agent has no reliable self-model for what it can safely do. Capability constraints are the partial substitute: if the agent literally cannot take certain actions, the question of whether it should is foreclosed. The closure is not elegant, but it works.

The agent has no private deliberation surface. Every action must produce an audit log that can be reconstructed. Every uncertain case must surface to a human before the action executes, not after.

Now design the Human Decision Node. A Node fires for: any account closure, any change to authentication credentials, any case the agent flags as uncertain, any case where the customer's request deviates from a known pattern, and a randomly sampled five percent of routine cases for ongoing audit. The human at the Node has access to the agent's full reasoning trace, has time budgeted for the role, has genuine authority to reject and modify, and is accountable for the decisions they ratify.

That is a deployable system. It is not the system the product team proposed. The 60% automation estimate assumed the agent would handle cases the Node design correctly routes to humans. The defensible automation rate is closer to 30 to 35 percent.

| Element | Before (proposed) | After (defensible) |
|---|---|---|
| **Automation rate** | 60% of incoming cases handled end-to-end by the agent | 30–35% — the residual is what survives once the Node design correctly routes the rest |
| **Identity verification** | Not specified — the agent acted on whatever the email asserted | Required before any account action: customer auth, instruction-level verification, no out-of-band changes |
| **Capability constraints** | Not specified — the agent could touch any field it could see | Explicit: no transfers, no cross-account access, no policy exceptions, no credential changes |
| **Node trigger conditions** | Not specified — the agent decided when to ask | Account closures, credential changes, agent-flagged uncertainty, plus a 5% random audit |
| **Node accountability structure** | Not specified — implied "the team reviews escalations" | Named accountable human, genuine authority to refuse, time budget sized to the hardest case, audit trail per decision |

*Figure 12.3*

The gap between 60 and 35 is what honest pricing of agentic deployment looks like. The product team wanted 60. The 60 is achievable only if you accept the blast-radius consequences of skipping the Node design, the capability constraints, the identity verification. The 35 is what you get when you take the structural failures seriously and design for them.

The fluent practitioner does not pretend the gap is smaller than it is. She goes to the product team and says: here is what the system can responsibly do, here is what it would take to do more, here is what we are trading away if we skip the discipline. That conversation is harder than agreeing to 60%. It is the conversation that keeps the deployment defensible two years from now when the regulator asks, or when a customer complaint surfaces something the system did at 2:00 AM on a Tuesday.

The same gap shows up in Priya's world, in different units. The vendor pitching the content-moderation agent originally estimated 85% of flagged cases could be handled without editorial review. The defensible rate, after the four conditions were properly designed and the agent's recurring-bad-actor cluster boundaries were audited, was closer to 55%. The remaining 30% — the cases where context outside the agent's training matters, where the false-positive cost is editorial credibility, where the publication's commenting policy intersects with judgment — those go to humans like Priya. The publication accepted the lower automation rate. The gap got named in the memo that approved the deployment.

---

There is one more thing to say about Human Decision Nodes that the design framework cannot capture on its own.

Nodes degrade.

A Node that is functional on day one — with real authority, real information, real time, real accountability — can become a rubber stamp over eighteen months without anyone deciding to make it one. The queue gets longer. The time budget stays fixed. The humans at the Node start trusting the AI's outputs more as the outputs prove reliable on the easy cases. Overrides decline. The sense of personal accountability diffuses. The Node is still there, in form. The function has left quietly.

This is the organizational problem that no design document fully solves. The four diagnostic questions have to be re-asked periodically — not because anyone expects the answers to change, but because asking them is what keeps the Node honest. The drift is invisible until something fails catastrophically, and the investigation afterward reveals that the Node had been a rubber stamp for months.

![Figure 12.4 — A degradation curve over 18 months](images/12-verification-and-diligence-under-autonomy-fig-04.jpg)

The recurring audit — the practice from Chapter 7, now applied to the Node itself — is how you catch the drift before the catastrophic case. A monthly sample of five cases reviewed by someone other than the Node operators, asking not whether the process was followed but whether the judgment was real: did the human here have real authority, real information, real time, real accountability?

Priya's publication runs that audit, monthly, on the moderation Node. She is one of the people audited; she is not the auditor. The audit catches degradation in conditions she herself would not have seen. The hospitals where pharmacists like the one she met at the medical-AI conference work run a similar audit. The organizations that don't audit will eventually produce the case the ones that do are trying to prevent.

---

### Translate before you move on — produce the Human-in-the-Loop Protocol

Priya's case was the publication's content-moderation Decision Node, where pattern-matching met the policy that protects pointed reader criticism. In your field, what are the equivalent Decision Nodes?

For a clinician: the medication-order checkpoint where the drug-interaction tool's verdict meets the pharmacist's case-specific judgment. For a software engineer: the deployment-approval Node where the automated pre-flight checks meet the on-call engineer's contextual knowledge. For a marketing manager: the campaign-publish Node where the AI personalization output meets the brand-safety override. For a teacher: the assessment-finalization Node where the AI-graded essay meets the teacher's read of the specific student. For a research scientist: the result-publication Node where the automated analysis pipeline meets the principal investigator's interpretive judgment. For a lawyer: the document-release Node where the AI redaction tool's output meets the attorney's review before disclosure. The specific Node varies. The four conditions — authority, information, time, accountability — are invariant.

For self-study readers without a current organizational Decision Node, the substitute is to design the Node for a deployment you propose or are watching from outside. The design is structurally identical; only the operational data is hypothetical.

**The Human-in-the-Loop Protocol — Chapter 12 Portfolio Artifact (Layer A template + Layer B customization, framework):**

Build it. Pick one Decision Node in your field — currently designed, in pilot, or proposed. Walk the four-condition test honestly. For each condition (authority, information, time, accountability), state what "functional" looks like for this Node, what degraded looks like, and where the current Node sits. Be willing to say "degraded" — most Decision Nodes in most industries fail one or more of the four.

Then write the compressed adversarial spiral for the Node — the four moves from Chapter 5, calibrated to the time budget the Node actually has. Each move phrased in the language the practitioner under time pressure would actually think. The trigger that tells the practitioner the case needs the spiral. The output the spiral produces — the decision plus the documentation.

Then run the end-to-end design problem: pick one agentic deployment relevant to your role (from the Ch 11 Decision Aid survey, or from a new proposal). Apply the three structural failures audit, the four blast-radius dimensions, the Node design (where, what authority, what information, what time, what accountability), the five-step Loop reweighting, and the honest automation-rate finding — what fraction of cases the design responsibly supports versus the proposal's estimate, with the gap explained.

Save as `portfolio/12-hitl-protocol.md`. Four to six pages. The Protocol is a Layer A framework (the four-condition test and the spiral are the same shape for every reader) filled with Layer B customization (your Node, your spiral, your worked example).

**Update your DESIGN.md.** Add a section on Human-Decision-Node design standards your domain accepts: what authority structure your field's Nodes require, what information must be surfaced (specific to your field's failure modes), what time budgets are defensible, what accountability structure holds. This pairs with the Ch 7 maintenance criteria and the Ch 11 stakeholder-model criteria to form the agency side of `DESIGN.md`. The three sections together name the criteria the reader applies to any AI system they would deploy or sign off on.

**Update your CLAUDE.md** with the chapter's operational rule: *Any Human Decision Node I am part of, or am designing, gets the four-condition test before any deployment and a recurring audit during. Theoretical authority, partial information, uniform time budgets, and laundered accountability are how Nodes degrade into rubber stamps. The audit is what catches the degradation before the case it would have caught.*

---

*What would change my mind.* If platform-level developments produced agentic systems where the three structural failures were addressed by default — where stakeholder modeling was robust, self-models were calibrated, and private deliberation surfaces with reliable escalation were standard — the chapter's design discipline would shift from *the practitioner has to compensate* to *the practitioner has to verify the platform's compensations*. We are not there in 2026. We may be there by 2030. The structural arguments here are designed to remain useful when we arrive; the specific case numbers will need updating.

*Still puzzling.* The Human Decision Node, in regulated industries with real accountability structures, works — when it is designed well and audited regularly. In less-regulated deployments, it degrades to rubber-stamping faster than anyone expects. I do not yet have a clean answer to what organizational conditions sustain a Node's functionality across years and across cost-pressure cycles. The four diagnostic questions diagnose the state at a moment. They do not yet predict the trajectory. That predictive model is the research project I would most like to see done.

---

> **Going deeper — *Computational Skepticism for AI***
>
> Priya's role at the Human Decision Node is the **irreducibly human** function the advanced volume's accountability chapter is built around. The deeper book gives a *cognitive* argument for why a human must occupy the Node — not just an ethical or legal one. The argument runs through what it calls the **seven-tier extended-mind taxonomy**: AI is genuinely strong at certain cognitive tiers, structurally weak at others, and absent at still others. The accountability chain has to be occupied by a kind of cognition the AI doesn't have, regardless of how much capability scales. Priya's contextual read of pointed-criticism-versus-harassment, like a pharmacist's renal-clearance check, is exactly the kind of cognition the deeper book argues cannot be delegated.
>
> The book also closes a long-running thread on **distributed responsibility** in this chapter: when an agent fails, no single party is the cause — each contributor (the user, the agent, the deployer, the framework, the model provider) had necessary but not sufficient agency. The five accountability requirements the deeper book derives from this are the formal version of the four diagnostic questions you ran on the moderation Node here.
>
> Priya's adversarial spiral is also the practitioner version of what the advanced volume calls the **defended-recommendation** structure: recommendation, evidence, assumptions, counterfactual — in that order, with verbs calibrated to the evidence. The deeper book uses it for executive reports; Priya used it in 90 seconds at 2:14 PM.
>
> See *Computational Skepticism for AI*, **Chapter 13 — Accountability** and **Chapter 12 — Communicating Uncertainty**.

---

### A note about AI

Verification under autonomy means the model is acting and you are watching. The verification has to happen at a layer above the model's output, not inside it.

Where the model genuinely helps: proposing what evidence of correct operation would look like and what evidence of incorrect operation would look like, in advance of the run. The framing is structural and useful.

Where the model does damage: self-reporting on whether it operated correctly. A model that has misbehaved has no stake in flagging the misbehavior. The verification layer cannot be the model itself.

The rule: under autonomy, build the watcher outside the model. The model is not its own auditor.

---

## LLM Exercise — Chapter 12: Verification and Diligence Under Autonomy

**Project:** AI Fluency for [Your Role] — Your Human-in-the-Loop Protocol

**What you're building this chapter:** The **Human-in-the-Loop Protocol** — the four-condition test applied to one Decision Node in your field, plus your role's compressed adversarial spiral, plus an end-to-end worked example of an agentic deployment evaluated honestly. Plus an update to your `DESIGN.md` on HITL design standards. Plus one new rule in your `CLAUDE.md`.

**Tool:** Claude Project (continue — your full portfolio so far is in context) + your file system (`portfolio/`).

---

**The Prompt:**

```
Continuing my AI Fluency portfolio. My Role Dossier, Worked Loop Log,
Practitioner Profile, Specification Library, Adversarial Conversation
Log, Verification Protocol, Diligence Framework, End-to-End Case Study,
Automation Inheritance Audit, Automation Specification, Blast-Radius
Decision Aid, PROJECT.md template, CLAUDE.md, and DESIGN.md are in
the Project context.

Botspeak Chapter 12 watches Priya — now an editorial lead twenty-three
months past Chapter 0 — at the publication's content-moderation
Decision Node. The agent flags a comment as harassment; Priya runs a
90-second compressed adversarial spiral, identifies that the agent
conflated pattern-match (repeat appearance in flag queue) with
content (actual harassment), rejects the flag, marks the case for
training-feedback. The chapter introduces the FOUR DIAGNOSTIC
QUESTIONS for a functional Decision Node (authority, information,
time, accountability), the compressed adversarial spiral, the
end-to-end agentic deployment design exercise, and the honest
automation-rate finding.

For Chapter 12's portfolio artifact, do four things.

TASK 1 — IDENTIFY 2–3 DECISION NODES IN MY ROLE.
For each: the role of the human at the Node, the time budget per
case, the typical case volume, the consequence of a wrong call.
Some Nodes already exist; some are coming; some should exist but
don't currently. Name all three categories.

TASK 2 — THE FOUR DIAGNOSTIC QUESTIONS, ANSWERED HONESTLY PER NODE.
For each Decision Node, walk the four conditions:
- AUTHORITY — real or theoretical?
- INFORMATION — sufficient, including what the AI didn't surface?
- TIME — fits the hardest case or just the median?
- ACCOUNTABILITY — named human on the hook, or laundered?

Be honest. Many real Decision Nodes in many industries fail one or
more. The portfolio earns its credibility by naming where the failure
is. Push back if my answer is "functional on all four" without
specifics — the default for unaudited Nodes is degraded somewhere.

TASK 3 — THE COMPRESSED ADVERSARIAL SPIRAL FOR MY ROLE.
Adapt the four-move spiral (Chapter 5) for the Decision Node's
typical time budget:
- Four moves in role-vocabulary, each phrased in language a
  practitioner under time pressure would actually think
- Total time budget for the spiral (depends on the Node's
  time-per-case)
- The cue that triggers the spiral (the pattern in AI output that
  says "this case needs the spiral")
- The output the spiral produces — the decision, the documentation,
  the training-feedback signal

TASK 4 — THE END-TO-END WORKED EXAMPLE.
Pick one agentic deployment relevant to my role (from my Chapter 11
Blast-Radius Decision Aid survey, or a new proposal). Evaluate it
end-to-end:
- Restate the proposal in concrete terms (what the agent does,
  what the original automation-rate estimate is)
- Apply the three structural failures audit (Chapter 11 instantiated)
- Apply all four blast-radius dimensions
- Design the Human Decision Nodes (where, what authority, what
  information, what time, what accountability)
- Reweight all five Loop steps for this deployment
- End with the HONEST automation-rate finding — what fraction of
  cases the design responsibly supports vs the proposal's estimate,
  with the gap explained in one paragraph

Save as `portfolio/12-hitl-protocol.md`.

TASK 5 — UPDATE MY DESIGN.md.
Add a section on Human-Decision-Node design standards my domain
accepts:
- What authority structure my field's Nodes require
- What information must be surfaced (specific to my field's
  failure modes)
- What time budgets are defensible
- What accountability structure holds (regulatory floor +
  organizational specifics)

Append to `portfolio/DESIGN.md`.

TASK 6 — ADD ONE RULE TO MY CLAUDE.md.
Append: "Any Human Decision Node I am part of, or am designing, gets
the four-condition test before any deployment and a recurring audit
during. Theoretical authority, partial information, uniform time
budgets, and laundered accountability are how Nodes degrade into
rubber stamps. The audit is what catches the degradation before the
case it would have caught."

Push back if my honest-automation-rate finding for the worked example
matches the proposal's estimate (it almost never should — the proposal
underprices the Node-design overhead).
```

---

**What this produces:** Your portfolio's final framework artifact, a meaningful update to `DESIGN.md`, and the final rule in your `CLAUDE.md`. The Human-in-the-Loop Protocol is the artifact that documents your capacity to govern not just the AI's outputs but the structural conditions under which a human is supposed to govern them. ~4,500–7,000 words across the new material. The longest portfolio piece, by design.

**How to adapt this prompt:**

- *For your own project:* The "honest automation rate" finding is the heart of this artifact. Resist the pressure to make the portfolio optimistic. A future employer's value-add from reading it is being able to trust that you would name the gap, not paper it over.
- *For ChatGPT / Gemini:* Works as-is.
- *For Claude Code:* Not the right fit.
- *For Cowork:* Recommended. Cowork can manage the multi-file split (`12-hitl-protocol.md` and the `DESIGN.md` update) and remind you to schedule the recurring Node audit.

**Connection to previous chapters:** Chapter 11 audited deployments at the population level — what agentic systems exist in your field and what their blast radius is. Chapter 12 zooms in on the design discipline at each Decision Node within those systems. Together they let a reader evaluate any agentic deployment in your role, both at proposal time and during operation.

**Preview of next chapter:** Chapter 13 — the closing synthesis. The Final Audit paired with the Chapter 0 Baseline, the 90-Day Plan, and the Cover Memo that fronts the assembled portfolio. The portfolio you have been building since Chapter 0 becomes one delivery-ready artifact.

---

## Exercises

### Warm-Up

**1. Diagnose the three opening cases.** *(Node conditions | Difficulty: low)*
The chapter opens with three examples of humans who are present but not thinking: the signing manager, the dosage-approving doctor, the compliance officer. For each one, apply the four Node conditions — authority, information, time, accountability — and name which condition is most likely degraded and how. One sentence per case.

**2. Name the question the AI didn't answer.** *(Information gap | Difficulty: low)*
The moderation agent returned "Flag for removal. Pattern match against recurring-harassment cluster #218, confidence 0.79." The chapter shows the agent answered the wrong question. In two sentences: state the question the agent actually answered, and state the question the case required answering. Then, in your professional domain, describe one type of AI output where the same gap — the AI answered one question while the situation required a different one — is likely to appear.

**3. Classify the bank's blast radius.** *(Blast-radius analysis | Difficulty: medium)*
The bank deployment case involves four blast-radius dimensions: stakeholder reach, reversibility, identity verification risk, and escalation pathway. For each of the following proposed agent actions at the bank, classify the blast radius on all four dimensions as low, medium, or high, with one sentence of reasoning per dimension:

- The agent drafts but does not send replies, queuing every response for human review before it is sent
- The agent automatically applies a promotional discount code when a customer emails to request it
- The agent closes a dormant account when the account holder requests it by email, and sends a confirmation

---

### Application

**4. Audit a Node you use.** *(Four conditions — live application | Difficulty: medium)*
Identify one Human Decision Node in your own work — a point where you are required to approve, sign off on, or ratify an output produced by a system or a team before it proceeds. Apply the four diagnostic questions honestly. For any condition that is degraded, write one sentence describing how it degrades and one sentence describing what it would take to restore it. If all four conditions are functional, describe what organizational or design feature keeps them that way.

**5. Design a Node.** *(Node design | Difficulty: medium)*
A legal tech company deploys an agent that reviews incoming contracts and flags clauses deviating from the company's standard terms. The output goes to a junior paralegal who approves or escalates each flagged clause before any response is sent to the counterparty. Design the Human Decision Node for the paralegal's role. Specify: what authority they must have (including the right to escalate over a senior partner's objection), what information they must see beyond what the agent flagged, what time budget is appropriate for a routine contract versus a complex one, and how accountability is structured if a non-standard clause is approved and later causes a dispute.

**6. Compress the spiral.** *(Adversarial spiral — domain translation | Difficulty: medium)*
The chapter compresses Priya's discernment into four questions she asks herself in ninety seconds. Translate the spiral into your own domain. Write four questions — analogous in structure to Priya's four, adapted for the kinds of AI-assisted decisions you make — that you could run in under two minutes before approving any high-stakes AI output. Test them against a real recent case: did asking them change your assessment? If not, describe what case characteristics would cause them to change it.

**7. Price the gap.** *(Honest deployment estimation | Difficulty: hard)*
The chapter shows that the bank's 60% automation estimate was only achievable by accepting blast-radius consequences the Node design would not permit, and that the moderation vendor's 85% estimate collapsed to 55% once the Node was designed properly. Identify an AI deployment you are involved in, have proposed, or have evaluated. What is the automation rate the team is targeting? Run the blast-radius analysis and the three structural failure checks against it. What is the defensible rate given those checks? Write the one sentence you would say to the product team to explain the gap between the two numbers.

---

### Synthesis

**8. The degrading Node.** *(Node degradation | Difficulty: hard)*
The chapter claims a functional Node can become a rubber stamp over eighteen months without anyone deciding to make it one. Choose a domain — medicine, finance, legal, engineering, journalism, or your own — and describe the degradation path concretely. For each of the four conditions, name the specific mechanism by which it erodes over time in that domain: how does authority become theoretical, information become partial, time become insufficient, accountability become laundered? Then design the recurring audit that would catch the degradation before a catastrophic case. Specify who runs it, how often, what five cases it reviews, and what question it asks of each case.

**9. The adversarial Node.** *(Node design under adversarial conditions | Difficulty: hard)*
Identity verification appears in the bank case as the primary attack vector: an agent acting on instructions whose authenticity has not been established is acting on assumptions adversaries can deliberately falsify. Design a Human Decision Node for a deployment in an explicitly adversarial environment — one where some fraction of inputs are attempts to manipulate the agent's behavior. Specify: how the Node detects that a case may be adversarial, what additional information the human reviewer needs when adversarial manipulation is suspected, how the time budget changes for such cases, and how accountability is structured when a sophisticated attack bypasses the Node anyway.

---

### Challenge

**10. Build the predictive model.** *(Node durability | Difficulty: high)*
The chapter ends: "I do not yet have a clean answer to what organizational conditions sustain a Node's functionality across years and across cost-pressure cycles. The four diagnostic questions diagnose the state at a moment. They do not yet predict the trajectory." In 400–600 words, propose that predictive model. Identify at least three organizational variables — structural features, incentive structures, cultural factors, or audit practices — you predict will distinguish functional Nodes from rubber stamps at eighteen months. For each variable: state the direction of the prediction, explain the mechanism by which it operates, and describe what evidence would falsify it.

**11. The unregulated deployment.** *(Node design without regulatory scaffolding | Difficulty: high)*
The chapter's two worked cases — Priya's content moderation and the bank's customer service — operate in industries with at least some accountability scaffolding (editorial credibility on one side, banking regulation on the other). The chapter notes that in less-regulated deployments, Nodes degrade faster. In 400–600 words, address: for a deployment in an unregulated or lightly regulated context — choose one: a startup's customer-facing AI, an internal knowledge management agent, an AI-assisted hiring tool at a small company — what substitutes for the regulatory accountability structure that keeps Priya's Node functional? If the answer is "nothing substitutes and the Node will degrade," make that argument and describe what the practitioner should do instead of designing a Node. If substitutes exist, name them, explain the mechanism by which they create genuine (not laundered) accountability, and describe how you would verify they are working.

---

## AI Wayback Machine

The ideas in this chapter didn't appear from nowhere. **Kurt Gödel** proved that any verification system powerful enough to be useful has true claims it cannot decide from inside itself — the formal limit on automated checking — decades before "Human Decision Node" entered anyone's vocabulary. Here's a prompt to find out more — and then make it better.

![Kurt Gödel, c. 1940s. AI-generated portrait based on a public domain photograph (Wikimedia Commons).](images/kurt-godel.jpg)
*Kurt Gödel, c. 1940s. AI-generated portrait based on a public domain photograph.*

**Run this:**

```
Who was Kurt Gödel, and how do his incompleteness theorems connect to
designing a Human Decision Node that has to verify an agentic action
without re-running the agent's reasoning? Keep it to three paragraphs.
End with the single most surprising thing about his career or ideas.
```

→ Search **"Kurt Gödel"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain "incompleteness" in plain language, as if you've never seen a logic textbook
- Ask it to compare Gödel's limit-theorem framing to the four diagnostic questions for a functional Node
- Add a constraint: "Answer as if you're sketching the audit cadence that catches Node degradation"

What changes? What gets better? What gets worse?
# Chapter 13 — The Fluent Practitioner

*Frequency is not fluency. The question that separates them is whether you can name, on any piece of work, what the AI did and what you did that it could not — and whether you can show someone the work itself, not just the claim.*

It is a Wednesday in the spring of Priya Banksy's third year in US journalism. Two years and three months ago, she sent a feature to publication with a fabricated Pew survey in it. Eighteen months ago, she sent a scoping memo to her editor that caught the same kind of failure in fourteen seconds. Today she is sitting at a different desk at a different publication — she moved last month, an editorial lead at a small investigative outlet that needed someone who could work with AI tools across their newsroom without compromising what makes the place worth reading.

The conversation that got her the role started with a document. The publication's editor-in-chief had asked her, by email, to send "anything that would help us understand how you work." Most candidates send a clip reel. Priya sent her portfolio's Cover Memo — one page, plain language, addressed to a reader who had never heard of *Botspeak* — and the link to the End-to-End Case Study folder it pointed at. The editor read both before their second conversation. The second conversation was about the work, not about whether Priya could do the work. The portfolio had already settled that.

This is what the book has been building toward. Not the answer to the closing question. The artifact that *is* the answer.

---

There is a question that separates two kinds of people who use AI in their work, and it is not the question most people expect.

It is not: do you use AI tools? Almost everyone does. It is not: do you use them often? Frequency is not fluency. It is not: do you understand how large language models work at a technical level? That helps, but knowing the architecture does not make you good at the work any more than knowing how a piano works makes you good at playing one.

The question is this: *what specifically did the AI do in this piece of work, and what specifically did you do that it could not?*

Most people, asked that question on their own work, cannot answer it. They say something like "the AI helped me draft it and I cleaned it up," which is true in the way "I cooked with heat" is true about a meal — accurate about the mechanism, completely silent about the judgment. They cannot separate their contribution from the model's. They cannot name where the work required domain knowledge the model did not have. They cannot say with any precision which parts they stand behind on their own authority and which parts they delegated.

This is not a failure of capability. It is a failure of attention. They have been using the tool without developing a practice around the tool, and without a practice, the tool is just a faster typewriter — producing more output without building any skill.

This book exists to produce something specific in you: the ability to answer that question. Not the vocabulary for it — though the book has given you vocabulary — but the genuine capacity underneath the vocabulary, earned through the reps. And: an artifact that answers the question on your behalf, without requiring the asker to take your word for it. The closing chapter is about both — how to make sure the reps happen, and what your portfolio now allows you to hand over.

---

The honest re-assessment question is not what you now know. It is what you now *do differently*.

Reading without running produces literacy, not fluency. If you worked through this book without putting the Loop on a real task, without running the four-layer verification on a real deliverable, without writing a five-component specification before a real piece of work, then the framework is in your head but not yet in your hands. The framework in your head is useful. It is not the same thing as the practice. The practice is in the hands.

If you did run the exercises — if you took the mid-chapter moves seriously and ran them on real work — then something should have changed that you can point to specifically. A piece of output you caught that you would have shipped three weeks ago. A delegation you declined that you would have made three weeks ago. A specification you wrote that produced good output on the first pass because you had thought clearly about intent and constraints before you typed anything. These are the receipts of practice.

The portfolio is the receipts made visible. If you have been building it across the book — the governing files, the customized frameworks, the case study, the audits — you do not need to argue that your practice has changed. You can show it.

If you cannot point to a specific change in real work, the remaining question is whether the obstacle was time — in which case the 90-day plan below is what matters now — or whether the framework, as I have given it to you, does not fit your domain cleanly enough to be immediately actionable. The second possibility is real. It deserves a direct response.

---

The Nine Capacities, the Decision Node model, the four adversarial moves — these are the vocabulary this book uses. They are not domain-neutral in detail, even if they are domain-neutral in structure. A pharmacist's fluency includes checks and constraints and judgment calls that a journalist's fluency does not, and vice versa. The Loop is the same. The specific contents of the Loop are not.

When a framework does not fit your domain cleanly, the temptation is to either force-fit it — applying the vocabulary awkwardly to work it was not quite built for — or abandon it for not being specific enough. Both are mistakes. The right move is translation.

Translation is the work of taking the framework's structure and filling it with your domain's specific content. What does *Strategic Delegation* mean for someone who writes code, versus someone who writes legal briefs, versus someone who designs clinical trials? The Capacity is the same. The specific judgment calls it requires — which AI outputs to trust, which to verify independently, where the domain knowledge the model lacks lives in your field — are different in each case.

The translation is its own kind of fluency. It is, in fact, a sign that the framework has been genuinely absorbed rather than memorized: you can see why it maps onto your work and where its vocabulary needs adjustment to fit. Senior practitioners in any field do this naturally with every framework they encounter. It is not a special skill for AI work. It is just pattern-recognition applied to your own domain, which you are better positioned to do than any author writing for a general audience.

Your portfolio is the translation made operational. The `CLAUDE.md` and `DESIGN.md` you have accreted are not the generic templates the book described. They are the field-specific governance documents you produced by filling those templates with the conventions, constraints, and verification checks that matter in your work. A future reader of your portfolio can see exactly where the framework met your domain and what each met-up produced.

The concrete way to do the translation, going forward: pick a senior person in your field whose AI work you respect. Watch what they do. Ask them — directly, if you can — what they verify that others do not, what they will not delegate to a model regardless of how good the output looks, what failure modes they have seen that others missed. The answers to those questions are your domain's specific addenda to this framework. They will not all be in this book. Add them to your `CLAUDE.md` and `DESIGN.md` as they come. Those files are living documents.

---

There is a structural reason why some people develop fluency and others do not, and it is not about starting talent.

The literature on deliberate practice identifies three ingredients that distinguish practice that builds capability from experience that just accumulates. The first is feedback — not vague feedback, but specific feedback, tied to specific outputs, close in time to the output. When you run the four-layer verification on a piece of work, the verification is feedback. It tells you, specifically, which claims did not hold up and why. When you write an AI Use Disclosure before shipping, the disclosure is feedback: if you cannot complete it honestly, you learn something about what you did not check.

The second is working at the edge of current ability. Not the comfortable zone where AI helps you do what you already know how to do, faster. The uncomfortable zone where you are asking it to help you do something you do not yet know how to do well, or where you are pushing the verification harder than feels necessary, or where you are making the specification more precise than you are confident about. Staying in the comfortable zone produces experience without improvement. The edge is where the capacity moves.

The third is repetition — not of the same thing, but of the same *type* of thing. The specification move, practiced daily, becomes automatic. The four-layer verification, practiced on consequential work, becomes fast. The delegation map, sketched at the top of every AI-assisted task, becomes the first thing you do rather than the thing you forget. Automaticity is the sign that a practice has become a capacity. The reps are what produce automaticity.

![Figure 13.1 — Three-ingredient deliberate practice model](images/13-the-fluent-practitioner-fig-01.jpg)

Most AI use fails to meet any of these three criteria. The feedback is vague — did it seem right? The work stays in the comfortable zone — tasks the user already knows how to evaluate. The repetition is of the same comfortable pattern, not of the skill being developed. This is how people accumulate years of AI use without accumulating fluency. The years are real. The practice, in the technical sense, was not.

---

Pick two capacities — not nine, not five, not the ones you think you should develop. The two you most want to move one level up in ninety days. The movement of two, done seriously, compounds. The aspiration to move nine, done diffusely, moves nothing.

For each of the two, you need three things.

A daily rep. Something specific, recurring, tied directly to the capacity, that you do every working day. The rep should take under five minutes on most days and should produce an artifact you could look back at. For *Effective Communication*, the rep is writing a five-component specification — intent, constraints, success criteria, exclusions, output format — before every consequential prompt. Not after. Before. The five-component spec, written daily, becomes automatic in about thirty working days. For *Critical Evaluation*, the rep is running the two-step verification on every Tier C output: first, does this hold up against the sources it claims to use; second, is there anything here that should make me distrust the parts I cannot independently check. For *Strategic Delegation*, the rep is a three-line delegation map at the top of every AI-assisted task: what the task is, what the model will produce, what I will produce that it cannot. The map takes ninety seconds. It forces the judgment before the work begins rather than after.

A weekly review. Fifteen minutes, same time, same day, every week. One question: did the rep actually happen this week, and what did I learn? The review is not an assessment of quality. It is a forcing function for noticing. Most deliberate practice dissolves not because the practitioner decides to stop but because the rep becomes invisible — it happens or does not happen without any moment of attention. The fifteen-minute review creates the moment of attention. It also, over ninety days, produces a log of what you learned — which becomes part of your portfolio, the next evidence that the practice is active.

A 90-day artifact. Something specific, at the ninety-day mark, that is the downstream product of the practice. Not a process artifact — a capability artifact. A piece of analysis that, on the four-layer verification, holds up without revision. A brief that a skeptical reader cannot identify as AI-assisted, not because you hid it but because the judgment is visibly yours. An automation design that earns a stakeholder's approval without negotiation because the anticipatory specification addressed every question before it was asked. The artifact is what the practice is *for*. It is the answer to the question of whether ninety days of reps moved anything. Name it now. Write it on the same page as the plan. If the artifact you name is too vague to know whether you have achieved it in ninety days, make it more specific until it is not. **Save it to `portfolio/13-90day-plan.md` and add the resulting capability artifact to the portfolio when the ninety days are up.**

| Slot | Capacity name | Daily rep — what / how long / artifact | Weekly review — day / time / the one question | 90-day artifact (specific enough to evaluate) |
|---|---|---|---|---|
| **Capacity 1** | _________________ | _________________ / _____ min / _________________ | _____ / _____ / _________________ | _________________ |
| **Capacity 2** | _________________ | _________________ / _____ min / _________________ | _____ / _____ / _________________ | _________________ |

*Figure 13.2*

Two capacities. Three commitments per capacity. Ninety days. This is not a large ask. It is a precise one. Precision is what most professional development plans lack, which is why most professional development plans do not produce development.

---

I want to come back to the opening question, because I want to give you the full version of the answer — not the vocabulary, but what the answer sounds like when the practice is there behind it.

The question: what specifically did the AI do in this work, and what specifically did you do that it could not?

Here is what a fluent practitioner's answer sounds like on a real piece of work — a publication-class investigative scoping memo, of the kind that appears in earlier chapters:

*I used the model to draft the company-snapshot and trade-press synthesis sections. The source list for those sections was verified independently; the three primary documents I relied on are linked in the appendix. I did the founder-background analysis without the model in places that required reading the regulatory filings against what was claimed publicly — those signals require knowing how that particular financing structure has been used in this segment before, and that pattern recognition is not in the model's training in any actionable form. The risk assessment is mine. I used the model to surface candidate risk factors and rejected three of its five suggestions — I can tell you which three and why if you want to audit the judgment. The four-hypothesis framework in the recommendation was developed in conversation with the model and then narrowed by me. The recommendation at the end is mine. The accountability for the memo is mine. If something in here is wrong, it is wrong because I missed it, not because I trusted a model I should not have.*

That answer takes ninety seconds to give. It separates the model's contribution from the practitioner's. It names the specific places where domain knowledge the model did not have was brought to bear. It assigns accountability cleanly. It surfaces the verification rather than burying it. It is, in any professional setting — an interview, an editorial meeting, a regulatory review, a hiring conversation — the kind of answer that tells the asker that the work is trustworthy without requiring them to audit every line.

| Sentence or phrase from the answer | What it does | What the vague literate-user answer omits |
|---|---|---|
| *"I used the model to draft the company-snapshot and trade-press synthesis sections."* | Names what the AI did specifically — which sections, which moves | The literate user says "helped me draft it" without naming which parts |
| *"The source list for those sections was verified independently; the three primary documents I relied on are linked in the appendix."* | Surfaces the verification — what was checked, against what, where it can be audited | The literate user buries or omits verification entirely |
| *"I did the founder-background analysis without the model in places that required reading the regulatory filings against what was claimed publicly."* | Names where domain expertise was load-bearing — and *why* the model could not substitute | The literate user cannot name this — which means she does not know it |
| *"The recommendation at the end is mine. The accountability for the memo is mine."* | Assigns accountability cleanly to a single named person | The literate user leaves accountability ambiguous — "we put it together" |

*Figure 13.3*

The literate user gives the vague answer because she has not been paying the kind of attention that produces the specific answer. The fluent practitioner gives the specific answer because she has been paying that attention in every piece of work she has done, over the months and years of the practice, until the attention is no longer effortful — it is just how she works.

That is what the ninety days is for. Not to produce the answer to the question. To build the habit of attention that makes the answer available, on demand, on any work, without preparation.

---

There is a second form of the answer that this book has been building toward, and it is in some ways more important than the spoken version.

It is the form where you do not have to give the answer. You hand someone the portfolio.

The portfolio is the answer to the closing question, written in advance, on every piece of work it documents. The End-to-End Case Study answers it for one major piece. The Specification Library answers it for your typical task types. The Verification Protocol answers it for your standards. The Diligence Framework answers it for any AI system you currently work with. The Baseline Audit and the Final Audit answer it for your past work, before and after.

The fluent practitioner does not need to argue for her fluency. She hands someone the portfolio. The portfolio argues for her.

This is why the Cover Memo at the front of the portfolio matters. It is the cover letter every unfamiliar reader sees first. One page. No book jargon. The reader who picks up your portfolio in twenty minutes between meetings should be able to read the Cover Memo, scan the case study, glance at the audits, and form an accurate judgment of how you work. The Memo does not boast. It points at the artifacts. The artifacts make the case.

If you do not yet have a Cover Memo — if your portfolio is still a folder of pieces without a front door — that is the most important single thing to draft now. The template is in Appendix C. The exercise at the end of this chapter walks you through the first complete draft.

---

The field is changing fast enough that some specific tool or technique in this book will be obsolete before many readers finish it. The Loop will not be obsolete. The Capacities will not be obsolete. The ability to separate your contribution from the model's and stand behind your contribution on your own authority will not be obsolete — it will become more valuable as the field matures and the organizations operating in it get better at distinguishing practitioners who have it from those who do not.

Three years into the AI-saturated workplace, the signal I see consistently is that senior practitioners can already tell the difference. They can tell by the quality of the questions a candidate asks about AI use. They can tell by how quickly someone can explain what judgment they applied in work that was AI-assisted. They can tell by whether someone knows what the failure modes of their own AI-assisted workflow are without being asked to check. They can tell, increasingly, by whether someone has a portfolio they can hand over — and what is in it.

These are not technical signals. They are practice signals. They are downstream of attention paid over time.

The book is over. The practice is not. The ninety days is how it starts. What comes after ninety days is yours.

Priya, on her Wednesday, three years past Ch 0, is not at the end of her practice. She is at a different point along it. The portfolio she handed her new editor before the second interview is older than the role she now holds. She will update it this month. She will update it again in a year. The portfolio is a living artifact — same shape, evolving contents, the way the practitioner herself is the same person whose specific judgments improve over time.

If you do nothing else with this book, do this: keep your portfolio alive. Update it when your role changes. Add the case studies that matter. Redo the audits when your past work no longer reads the way it did. The portfolio is the throughline of your career across the AI transition. The closing question is answered, again and again, by what is in it.

---

### Translate before you close — and complete the portfolio

This is the last chapter of the book, and it produces the last set of portfolio artifacts: the **Final Audit**, the **90-Day Plan**, and the **Cover Memo**.

**The Final Audit** (Layer B, diagnostic — paired with Ch 0 Baseline Audit). Open the Baseline Audit you wrote at the end of Chapter 0. Find the piece of past work it audited. Audit it again, today, using the four-layer verification frame from Chapter 6 — but now with the capacities and reflexes you have built across the book. Three sections, no more than half a page total:

1. *Piece audited.* Same piece as the Baseline Audit. Same metadata.
2. *Load-bearing claim — re-read.* The same single most consequential element from the Baseline. What do you now see in it that you did not see then?
3. *Verification trace — done.* What would the verification look like if you ran it on this piece now? Run it. Note what holds up and what does not.

Save the Final Audit as `portfolio/13-final-audit.md`. The pair — Baseline and Final, the same piece of work seen by the same person twice — is the cleanest single comparison your portfolio offers. If the two audits read identically, the book did not teach. If they read differently — if you can now see things in your past work that you could not see when you started — the book did what it set out to do.

**The 90-Day Plan** (Layer A template + Layer B content, synthesis). The template in Figure 13.2 is the structure. Pick two capacities. Define the daily rep, the weekly review, and the 90-day artifact for each. Save as `portfolio/13-90day-plan.md`. Schedule the weekly reviews on your calendar right now. The plan that is not on the calendar does not happen.

**The Cover Memo** (Layer A template + Layer B content, synthesis). The template lives at `portfolio/00-cover-memo-template.md` (also reproduced in Appendix C). One page. Six sections. Plain language. No book jargon. Addressed to a reader who has never heard of *Botspeak*. The Memo points at the artifacts in your portfolio and tells the unfamiliar reader the shortest path through them.

If you cannot write your Cover Memo cleanly, that is information about your portfolio, not your writing. It means the portfolio does not yet have an argument it can name out loud. Go back to the artifacts. Re-read the case study. The Memo writes itself once the portfolio is coherent. **If the Memo will not write — that is the most important diagnostic the book offers. Pay attention to it.**

Save the Memo as `portfolio/cover-memo.md` at the top level of your portfolio folder. It is the first thing every future reader sees.

The portfolio is now complete. Seventeen artifacts. Five sections. One case study at the center. One pair of audits to bracket the change. One Cover Memo to lead the unfamiliar reader through. Add a date to the top of each artifact. Plan to update them on a schedule that fits your work. The portfolio is yours now.

---

*What would change my mind.* If, ten years from now, practitioners I would describe as fluent turn out to be no more effective than well-trained literate users — if the distinction is rhetorical rather than functional — the book is wrong about what matters. I do not yet have ten years of evidence. The early signal is that the distinction is real, is growing, and is increasingly visible to the people doing the hiring. I would update on contrary evidence. I have not seen it yet.

*Still puzzling.* I do not know whether nine is the right number of capacities. It is the number I observe doing work. It might consolidate to six as the field's vocabulary stabilizes. It might expand to twelve as new capability classes emerge. The structure of the capacities is more durable than the count, and I would not be surprised if a future edition of this book has fewer than nine, named differently, in ways I cannot yet see.

---

> **Going deeper — *Computational Skepticism for AI***
>
> The closing artifact this chapter asks of you — a defensible, specific account of what the AI did and what you did that it could not — has a longer form in the advanced volume. There it is called both the **AI Use Disclosure** (a supervisory log on a single piece of work) and the **cognitive profile** (a map of where the AI is genuinely strong, where it is structurally weak, and where it is absent for a given deployment). The closing chapter of the deeper book treats this as the engineer's most important structural authority: the authority to say *this AI should not be deployed for this purpose* — to refuse, on the basis of named limits the validation toolkit cannot reach. Three categorical limits in particular do not yield to capability scaling: the **meaning gap** (the model manipulates symbols without grasping what they mean in the world), **intentionality** (the model has no aboutness toward the world), and the **data-world gap** (training data is at best an imperfect proxy for the deployment context).
>
> If you find yourself, after the 90-day plan, wanting to deepen the practice into engineering-grade work — auditing real deployments, writing defensible fairness choices, building maintenance loops for AI in production — the advanced volume is the next book. It is harder. It assumes the practitioner discipline this book teaches.
>
> See *Computational Skepticism for AI*, **Chapter 4 — The Frictional Method** and **Chapter 14 — The Limits of AI**.

---

## Exercises

### Warm-Up

**1. The question, applied — and the artifact, found.** *(Core question — recognition + portfolio match)*
Choose a piece of AI-assisted work you produced in the last two weeks — a draft, an analysis, a summary, anything you used a model to help produce. Answer the chapter's opening question about it: what specifically did the AI do, and what specifically did you do that it could not? Write your answer in the ninety-second form the chapter describes — separating contributions, naming the domain knowledge you brought, assigning accountability. Then: which artifact in your portfolio supports the answer? Name the file. If no artifact supports it, that is what your portfolio is missing.

**2. Literacy versus fluency.** *(Distinction — internalization)*
The chapter distinguishes literacy (vocabulary in your head) from fluency (capacity in your hands). Using the cooking-with-heat analogy as a model, construct your own analogy from a domain you know well that captures the same distinction. Then use your analogy to explain what it would take to move from literacy to fluency in AI work — not in general, but specifically for someone at the stage you were at when you started this book.

**3. The three ingredients, located.** *(Deliberate practice — structure)*
For each of the three deliberate-practice ingredients — specific feedback, working at the edge, typed repetition — identify one specific practice from this book (not from this chapter; from an earlier chapter) that supplies that ingredient. For each, write two sentences: what the practice is and exactly how it supplies the ingredient.

---

### Application

**4. Design your 90-day plan.** *(90-day plan — live construction; portfolio artifact)*
Following the structure in the chapter exactly, write your personal 90-day plan and save it to `portfolio/13-90day-plan.md`. Choose two capacities. For each, define the daily rep (what it is, how long it takes, what artifact it produces), the weekly review (day, time, the one question you will ask), and the 90-day artifact (named specifically enough that you will know in ninety days whether you achieved it). The plan should be specific enough that a colleague could read it and tell you whether the artifact you named is too vague. Then schedule the weekly reviews on your calendar. The plan that is not on the calendar does not happen.

**5. Run the Final Audit.** *(Final Audit — portfolio artifact; paired with Ch 0)*
Open `portfolio/00-baseline-audit.md` from Chapter 0. Audit the same piece of past work again, today, in the same three-section form (Piece audited / Load-bearing claim — re-read / Verification trace — done). Compare the two audits side by side. Write one paragraph naming what changed — not "I am better now" but specifically what you can now see in the piece that you could not see when you wrote the Baseline. Save as `portfolio/13-final-audit.md`.

**6. The translation.** *(Framework translation — domain-specific)*
Choose your domain. Identify one place where the book's vocabulary does not fit your domain cleanly — where a capacity, a concept, or a framework step requires translation rather than direct application. Describe what the translation looks like: what the book's term means in your domain, what the domain-specific version of the judgment call is, and what a senior practitioner in your field would add that is not in the book. Add the translation as a note to your `CLAUDE.md` and `DESIGN.md`.

---

### Synthesis

**7. Draft the Cover Memo.** *(Cover Memo — portfolio artifact; the most important single page)*
Using the template at `portfolio/00-cover-memo-template.md`, draft your Cover Memo. One page. Six sections. No book jargon. Addressed to a reader who has never heard of *Botspeak*. Save as `portfolio/cover-memo.md` at the top level of your portfolio folder.

Hand the draft to one person who has not read this book and ask them: *if you were going to hire someone in my field, would this Memo make you want to read the portfolio?* If they say yes, the Memo is doing its job. If they say no, the issue is almost never the writing — it is that the portfolio does not yet have an argument the Memo can name. Go back to the case study. The Memo writes itself once the portfolio is coherent.

**8. The signal senior practitioners read.** *(Practice signals — reasoning)*
The chapter closes by claiming that senior practitioners can already distinguish fluent from literate users — by the questions they ask, how quickly they can articulate their judgment, whether they know their own workflow's failure modes without being prompted, and whether they have a portfolio they can hand over. For each of the four signals, explain what it reveals about the practitioner's underlying practice — what habit of attention each signal is downstream of, and how long it takes to develop.

---

### Challenge

**9. The Feynman test for the whole book.** *(Full synthesis — Feynman test)*
Apply the Feynman test to the book as a whole. Suppose a colleague who has not read it asks you: "What does it actually mean to be fluent at AI work, and how do you get there?" Write your answer in 250–300 words. Your answer should not recite chapter titles or framework names. It should make the core argument in your own words, using examples from your own domain, in the voice of someone who has absorbed the framework rather than summarized it.

**10. The ten-year question.** *(Epistemic standards — study design)*
The "What would change my mind" section is unusually specific: if fluent practitioners turn out to be no more effective than well-trained literate users over ten years, the book is wrong. Design the study that would test this claim. What would you measure, in whom, over what period, with what comparison group, and what outcome would constitute evidence that the fluency/literacy distinction is rhetorical rather than functional? Your design does not need to be feasible with current resources — it needs to be rigorous enough that if it came back with contrary evidence, a reasonable person would update.

---

### A note about AI

Fluency is the integration of the nine capacities under load. The chapter argues that fluency is a real and learnable state. The note examines what the model can and cannot do for someone working toward it.

Where the model genuinely helps: showing you specific examples of fluent practice in domains you do not yet work in. Pattern exposure accelerates pattern recognition. The model has read more transcripts of fluent practitioners than you will.

Where the model does damage: telling you that you are fluent. Fluency is demonstrated by work, not by self-report and not by the model's report. The model will produce a confident assessment of your fluency on request, and the assessment is worthless as evidence.

The rule: fluency is what your work shows, not what the model says about your work.

---

## LLM Exercise — Chapter 13: The Fluent Practitioner

**Project:** AI Fluency for [Your Role] — The Portfolio, Closed

**What you're building this chapter:** The three closing artifacts that complete your portfolio — the Final Audit, the 90-Day Plan, and the Cover Memo — produced in a single session against everything you have built across the book.

**Tool:** Claude Project (continue — your Role Dossier and all prior chapter artifacts are in context) + your file system (`portfolio/`).

---

**The Prompt:**

```
Closing my AI Fluency portfolio. My Role Dossier from Chapter 0, my
End-to-End Case Study from Chapter 8, and every chapter artifact in
between are in the Project context.

Botspeak Chapter 13 closes the book with three portfolio artifacts: the
Final Audit (paired with the Chapter 0 Baseline Audit), the 90-Day Plan,
and the Cover Memo (one page, addressed to a reader who has never heard
of Botspeak).

Do three things in this session.

TASK 1 — THE FINAL AUDIT.
Open the Baseline Audit I wrote at the end of Chapter 0 (paste it below
or reference the file). Help me audit the same piece of past work again,
in the same three-section structure (Piece audited / Load-bearing
claim — re-read / Verification trace — done). The Final Audit should
honestly compare to the Baseline — what do I now see in the piece that
I did not see then? What would the four-layer verification turn up
today? Save as `portfolio/13-final-audit.md`.

Then write one paragraph for the bottom of the Final Audit comparing
the two audits — what changed, named specifically. The pair is the
cleanest evidence of fluency the portfolio offers.

[PASTE BASELINE AUDIT HERE]

TASK 2 — THE 90-DAY PLAN.
Help me design my 90-Day Plan using the Botspeak structure: two
capacities, three commitments each (daily rep, weekly review, 90-day
artifact). The capacities should be the two most likely to compound for
my role at my current career stage. The daily rep should be a five-
minute move tied to my actual tasks. The 90-day artifact should be a
named, specific capability artifact a senior person in my role would
recognize as a developmental milestone.

Save as `portfolio/13-90day-plan.md`.

TASK 3 — THE COVER MEMO.
Help me draft my Cover Memo following the six-section template
(who I am / why this portfolio exists / what it contains / what is
not in it / the before-and-after / how to read it in twenty minutes).
One page. No Botspeak vocabulary. The Memo points at the artifacts
I have built; it does not boast.

Then push back. Read the Memo as if I had not read this book. Is it
legible? Is there book jargon I did not notice? Does it name the
artifacts clearly enough that a future reader could find them? Mark
the places where the Memo requires the reader to take my word for
something rather than pointing them at evidence.

Save as `portfolio/cover-memo.md` at the top level of my portfolio
folder.
```

---

**What this produces:** The three closing artifacts of your portfolio — Final Audit, 90-Day Plan, Cover Memo — drafted in one session and saved to your portfolio folder. The portfolio is now complete: seventeen artifacts, five sections, one case study at the center, one pair of audits to bracket the change, one Cover Memo to lead unfamiliar readers in.

**How to adapt this prompt:**

- *For your own project:* The Final Audit and the Cover Memo are the two most important artifacts in the whole portfolio. The 90-Day Plan is what makes it durable. Take this session seriously — it is the bookend to the entire book.
- *For ChatGPT / Gemini:* Works as-is.
- *For Claude Code:* Useful for final folder organization. Ask Claude Code to set up the `portfolio/` directory structure cleanly and generate an index file.
- *For Cowork:* Recommended for assembling and reviewing the portfolio as a whole. Cowork can walk the folder, identify gaps, and help you draft the index.

**Connection to previous chapters:** Every chapter has produced one or more portfolio artifacts. This chapter closes the set. The Final Audit pairs with Chapter 0. The Cover Memo references the End-to-End Case Study from Chapter 8 as the centerpiece. The 90-Day Plan is what keeps the portfolio alive after the book ends.

**Preview of next chapter:** There is no next chapter. The next thing is to hand someone your portfolio and watch what they do with it. The first feedback you get is data for the portfolio's next revision — which you will do in three months, and again three months after that, for as long as your career remains the throughline of your practice.

---

## AI Wayback Machine

The ideas in this chapter didn't appear from nowhere. **Yuen Ren Chao** spent a lifetime studying what makes a speaker actually fluent — usage patterns, switching moves, the gap between rule and practice — decades before anyone called any of it "AI fluency." Here's a prompt to find out more — and then make it better.

![Yuen Ren Chao, c. 1950s. AI-generated portrait based on a public domain photograph (Wikimedia Commons).](images/yuen-ren-chao.jpg)
*Yuen Ren Chao, c. 1950s. AI-generated portrait based on a public domain photograph.*

**Run this:**

```
Who was Yuen Ren Chao, and how does his study of linguistic fluency
connect to the idea of a fluent AI practitioner who runs the Loop
without having to consult the templates? Keep it to three paragraphs.
End with the single most surprising thing about his career or ideas.
```

→ Search **"Yuen Ren Chao"** on Wikipedia after you run this. See what the model got right, got wrong, or left out.

**Now make the prompt better.** Try one of these:

- Ask it to explain linguistic competence versus performance, in plain language
- Ask it to compare Chao's account of fluency to the 90-day plan in this chapter
- Add a constraint: "Answer as if you're writing the Cover Memo for a portfolio that travels with the practitioner across roles"

What changes? What gets better? What gets worse?
# Back Matter

## Acknowledgements

A book like this is mostly other people's thinking, used in ways the original thinkers cannot all be asked about. Where I cite by name, I have tried to do so in the chapter rather than in a list at the back, because a list at the back is the kind of acknowledgement that lets the reader skip noticing whose idea is doing the work.

The voices that are explicit, in the AI Wayback Machine sections at the close of each chapter, are the ones whose work the practitioner can pick up and use directly: Henriette Avram, W. Ross Ashby, Lev Vygotsky, W. Edwards Deming, Mary Parker Follett, Gordon Pask, Abraham Wald, Walter Shewhart, Donella Meadows, Norbert Wiener, Grace Hopper, Barry Turner, Kurt Gödel, Yuen Ren Chao. Read one for every chapter you finish. The book is partly a map for them.

The reading I owe to working practitioners — the engineers, analysts, managers, and graduate students whose composite cases anchor the book's worked examples — cannot be cited individually without violating the trust under which the cases were observed. The patterns are real. The names have been changed, the details composited. Every example is something I watched happen. If a working colleague reading this thinks I am writing about them, I probably am, and I am grateful.

The companion volume *How to Speak Bot* (Brown, existing) provided the pattern library this book points back to in the appendices. The two are designed to be read together — *Botspeak* for the workflow, *How to Speak Bot* for the moves inside it.

---

## Glossary

*The book accretes vocabulary on purpose. Most of these terms are named in the chapter where they earn their place. This is the look-up table — the place the reader returns when a term shows up two chapters after it was defined. Chapter references at the end of each entry point to where the term is unpacked.*

**Accountability gap.** The Automation failure mode in which no human is actively monitoring and no human is on the hook. The failure mode that makes the other three (input drift, output drift, context shift) invisible until something fails loudly. (Ch 10)

**Accountability-obscuring mechanisms, three.** Process laundering, tool diffusion, and the verification gap. The three structural ways accountability disappears in a recurring AI-assisted process even though every individual actor behaves correctly. (Ch 7)

**Accountable Judgment.** Tier 7, the top of the Seven Tiers. Decisions where, if they go wrong, a human has to answer for them. The model can inform; the decision belongs entirely to the human. *See also: Seven Tiers.* (Ch 4)

**Adversarial Conversation Log.** The Chapter 5 portfolio artifact — one real piece of work taken through all four adversarial moves, with time-stamps and findings. (Ch 5)

**Adversarial moves, four.** The four prompts that defeat sycophantic drift: the steelman, the edge-case probe, the assumption surface, and the devil's advocate role assignment. (Ch 5)

**Adversarial test cases.** The second of the three Automation noticing forms — inputs constructed to probe known failure modes, run on a schedule. *See also: Noticing forms, three.* (Ch 9)

**Agency.** The third Mode. The configuration in which the AI takes actions in the world on the practitioner's behalf — sending email, posting, calling APIs, modifying records — not just producing text for a human to act on. The blast radius grows in ways text-only mistakes cannot. *See also: Three structural failures of agentic AI.* (Ch 1, Ch 11)

**Agentic Blast-Radius Decision Aid.** The Chapter 11 portfolio artifact — the four-dimension analysis applied to one specific agentic deployment in the reader's field. (Ch 11)

**AI Fluency.** The discipline of running the Loop on real work with deliberate attention to each step, against a domain in which the practitioner can verify, defend, and own the output. The capacity the book teaches. *See also: AI Literacy, Fluency trap, Ownership Test.* (Ch 0)

**AI Literacy.** The capacity to open a chatbot, type a prompt, read the output, copy and paste. Necessary, not sufficient. The bar most readers have already cleared. (Ch 0)

**AI Use Disclosure.** The four-sentence note the practitioner attaches to AI-assisted work naming what the AI did, what the human did, where the load-bearing judgment was, and who is on the hook. Introduced in Chapter 8 as the artifact that closes the Loop. (Ch 8)

**Ambiguity types, six.** Input-quality variation, output-volume variation, context shifts the model cannot detect, ambiguous inputs, high-stakes outputs, and model-specific failure modes. The six categories of anticipated deviation an Automation specification must address. (Ch 10)

**Ambiguous inputs.** One of the six ambiguity types — the case where the input is internally contradictory and the model will produce output regardless. The handling rule is usually: surface the conflict to a human rather than let the model paper over it. (Ch 10)

**American-in-India metaphor.** The book's operating metaphor for the literacy/fluency gap. The tourist who reads no Hindi at all asks for help and gets on the right train. The tourist who reads some Hindi misreads the board and ends up on the wrong platform. The fluent speaker buys chai. (Ch 0)

**Amplifying offload.** Cognitive offloading that strengthens the practitioner over time — the evaluative role survives the delegation; the judgment muscle keeps firing. *See also: Atrophying offload.* (Ch 4)

**Anticipatory specification.** The discipline of writing an Automation spec before the system runs, explicitly handling the six ambiguity types and the four failure modes — the implicit checks a human would have run in real time, made explicit on the page. (Ch 10)

**Appropriateness tests, three.** Bounded scope; predictable inputs; low blast radius. The five-minute screen before deciding whether a task should be automated at all — or, for an inherited automation, whether it should continue running in current form. (Ch 9)

**Assumption surface.** The third of the four adversarial moves. The prompt that asks the model to list the unstated assumptions an argument is making, label each one (factual, methodological, value-based), and name what would be needed to defend each. Catches invisible premises. (Ch 5)

**Atrophying offload.** Cognitive offloading that weakens the practitioner over time — the evaluative role does not survive the delegation; the muscle goes dormant; three months later the practitioner knows less than they would have working by hand. The default for unexamined daily delegation. *See also: Performance paradox.* (Ch 4)

**Audience criteria.** The DESIGN.md section naming the readability, jargon, evidence, and source-attribution standards the reader's domain demands. *See also: DESIGN.md.* (Ch 6)

**Augmentation.** The first Mode. The configuration in which the human is at the keyboard while the AI runs — every output crosses human eyes before use. The Loop's most forgiving configuration; the configuration in which most of a practitioner's day still happens. (Ch 1)

**Authority.** The first of the four conditions of a functional Human Decision Node. Does the human at the Node have genuine authority to override the AI's output, including by saying no? Theoretical authority does not produce judgment. (Ch 12)

**Automation.** The second Mode. The configuration in which the AI runs without the human present at execution time. The Loop's steps reweight: specification becomes anticipatory, diligence becomes designed-in, discernment becomes sampling + adversarial tests + outcome audits. (Ch 1, Chs 9–10)

**Automation failure modes, four.** Input drift, output drift, context shift, accountability gap. The four failure modes every Automation's Diligence design must address. (Ch 10)

**Automation Inheritance Audit.** The Chapter 9 portfolio artifact — appropriateness tests + drift assessment + noticing protocol + deployment verdict for one automation the reader has inherited or proposes to oversee. (Ch 9)

**Automation Specification.** The Chapter 10 portfolio artifact — one specific automation fully specified, three times the length of the Augmentation equivalent, with the six-ambiguity-type check and the stakeholder defense memo. The most directly deployable single artifact in the portfolio. (Ch 10)

**Baseline Audit.** The Chapter 0 portfolio artifact — an audit of one of the reader's past AI-assisted pieces, applying the four-layer verification frame informally. Paired with the Final Audit at Chapter 13 as before-and-after evidence of fluency. (Chs 0, 13)

**Be Diligent.** The fifth Loop step. Naming what the AI did, what the human did, where the load-bearing judgment was, and who is on the hook. In Augmentation mode, the AI Use Disclosure. In Automation, the four-component Diligence protocol. (Ch 1, Ch 7)

**Blast radius.** The reach of an error if the AI gets the work wrong. In Augmentation, bounded by what the practitioner reviews and approves. In Automation, scales with time-to-detection. In Agency, has four dimensions: stakeholder reach, reversibility, identity verification, and escalation pathway. *See also: Blast-radius dimensions, four.* (Chs 1, 9, 11)

**Blast-radius dimensions, four.** The four axes used to assess any agentic deployment: stakeholder reach (whose interests are affected if the agent acts incorrectly), reversibility (can the action be undone), identity verification (does the agent know whose authority it acts on), escalation pathway (what does the agent do when uncertain). (Ch 11)

**Bounded scope.** The first appropriateness test. Can the task be described in one paragraph that the practitioner would defend to a manager? If the task is not bounded, the model will be making scope decisions in real time it has not been authorized to make. (Ch 9)

**Capacities, Nine.** Strategic Delegation, Effective Communication, Critical Evaluation, Technical Understanding, Ethical Reasoning, Stochastic Reasoning, Learning by Doing, Rapid Prototyping, Theoretical Foundations. The cognitive abilities the Loop draws on, each named by diagnostic question and located on a durability spectrum. (Ch 2)

**CLAUDE.md.** The reader's living coding/process constitution. Accretes rules across chapters as the book gives the reader reasons to add them. Travels to every new role and every new AI tool. *See also: Governing files, three.* (Chs 1, 3, 4, 5, 6, 7, 9, 10, 12)

**Cognitive offloading.** Moving mental work from inside the head to a system outside the head. Scratch paper is offloading; a to-do list is offloading; a calculator is offloading. AI tools offload at a scale qualitatively different from anything before. *See also: Amplifying offload, Atrophying offload.* (Ch 4)

**Confidence-correctness gap.** The distance between how confident an AI output sounds and how likely it is to be correct. The model's tone reflects how typical the output looks; it does not reflect accuracy. The heuristic that works on human sources does not transfer. (Ch 6)

**Constraints.** The second of the five Specification components. The format, length, source, and audience limits the output has to fit inside. The parts of the specification the model would otherwise guess at. (Ch 3)

**Contestable Analysis.** Tier 6 of the Seven Tiers. Problems where reasonable practitioners would genuinely disagree. The model can assemble components; the call belongs to the human. *See also: Seven Tiers.* (Ch 4)

**Context drift.** One of the three drift forms. The world the recurring process operates in has changed in ways the system has no access to — new entrants, new regulations, new audience composition. Caught by outcome audits, not by benchmark re-runs. (Ch 7)

**Context shift.** Two uses. (1) One of the six ambiguity types — what the system does when the world has changed in ways the model cannot detect. (2) One of the four Automation failure modes — the recurring version of the same problem. (Chs 10, 7)

**Converse.** The third Loop step. The iterative refinement that turns a first draft into something the practitioner can stand behind, including the four adversarial moves. The Conversation chapter teaches this step. *See also: Adversarial moves, four.* (Chs 1, 5)

**Cover Memo.** The single most important artifact in the finished portfolio — the one-page cover letter at the front of the portfolio addressed to a reader who has never heard of *Botspeak*. Drafted at Chapter 13. (Ch 13)

**Critical Evaluation.** One of the Nine Capacities. Reading AI output for what kind of error it might contain, not just whether it sounds right. Contested in durability — models are improving at calibrated self-doubt. (Ch 2)

**Decision Node.** *See: Human Decision Node.*

**Delegate.** The second Loop step. Deciding what the model will do and what the human will do, before the work begins. *See also: Seven Tiers, Delegation Map.* (Chs 1, 4)

**Delegation Map.** The second half of the Practitioner Profile — the reader's tasks located on the Seven Tiers, the four delegation questions answered per task, the amplify/atrophy assessment, the named-skill at quiet-atrophy risk. (Ch 4)

**Delegation questions, four.** What capacity does this task build, and do I need to keep building it? What is the blast radius if the AI gets this wrong? Who is accountable, and do they know how the work was produced? What does the model not know that I do, and have I made sure that part stays in? (Ch 4)

**DESIGN.md.** The reader's living output-quality constitution. Names the verification standard, the voice and register the domain expects, the audience criteria, the maintenance and ownership criteria, the agentic stakeholder-model criteria, and the HITL design standards. *See also: Governing files, three.* (Chs 6, 7, 11, 12)

**Devil's advocate role assignment.** The fourth of the four adversarial moves. The instruction that puts the model into a sustained oppositional persona rather than asking for discrete pushback. Catches integration failures the discrete probes miss. (Ch 5)

**Diligence.** The fifth Loop step, expanded in Chapter 7. What happens between executions of recurring work: the documented spec, the scheduled drift check, the outcome audit, the named accountable human. Diligence is primarily about defensibility — the practice that makes a failure auditable when it eventually happens. (Ch 7)

**Diligence components, four.** Documented specification; drift checks on a schedule; outcome audits; named accountable human. The protocol that defeats the three accountability-obscuring mechanisms. (Ch 7)

**Diligence Framework Applied.** The Chapter 7 portfolio artifact — the four-component protocol walked against one specific AI-assisted system the reader uses, owns, or works alongside. (Ch 7)

**Discern.** The fourth Loop step. Reading the output for what kind of error it might contain, calibrating verification effort to stakes. The Discernment chapter teaches this step. *See also: Verification layers, four; Verification tiers, four.* (Chs 1, 6)

**Documented specification.** The first of the four diligence components. The document that answers what the process does, on what inputs, producing what outputs, for what use case, validated against what, approved by whom. Without it, there is no baseline to check drift against. (Ch 7)

**Drafting in Your Voice.** Tier 4 of the Seven Tiers. The model produces a draft; the practitioner revises. The Tier-specific risk is voice drift over months — the practitioner's writing migrating toward the model's defaults. *See also: Seven Tiers.* (Ch 4)

**Drift forms, three.** Model drift (the model changed), context drift (the world changed), use case drift (the task changed). The three ways recurring AI-assisted work degrades quietly. (Ch 7)

**Edge-case probe.** The second of the four adversarial moves. The prompt that asks the model to construct three specific scenarios in which an argument or recommendation fails. Catches scope error. (Ch 5)

**Effective Communication.** One of the Nine Capacities. Telling the model what it actually needs to know — intent, constraints, audience, success criteria. When this fails, the model fills in blanks with its best guess. (Ch 2)

**End-to-End Case Study.** The Chapter 8 keystone portfolio artifact. One complete piece of the reader's own work taken from intent through delivery, every Loop step documented, every adversarial move logged, every verification layer applied, every disclosure attached. The gravitational center of Layer B. (Ch 8)

**Escalation pathway.** The fourth blast-radius dimension. When the agent encounters a situation outside the scope of its explicit instructions, what does it do — guess and act, or surface to a human and wait? If the answer is the former, the blast radius is whatever the agent can reach with its tools. (Ch 11)

**Ethical Reasoning.** One of the Nine Capacities. Noticing when a use case has stakeholders other than the practitioner and the AI, and acting on that noticing. Durably the human's responsibility — accountability cannot be delegated to a model. (Ch 2)

**Exclusions.** The fourth of the five Specification components. What the model is not supposed to do. The specification saying: please leave that blank blank. (Ch 3)

**External.** Tier C of the four-tier verification protocol. Work going to a client, a regulator, a public audience, a senior stakeholder — anything that publishes. Run all four verification layers. The tier most consequential to most practitioners. *See also: Verification tiers, four.* (Ch 6)

**Fact.** The first of the four verification layers. Are the specific factual claims true — citations real, numbers accurate, attributions correct, quotes actually said? Most users vaguely understand they should run this layer. Execution is what gets skipped under time pressure. (Ch 6)

**Failure-mode handling.** The Automation specification section naming what the system does when generation fails, when output exceeds format constraints, when hallucinated citations are detected. (Ch 10)

**Final Audit.** The Chapter 13 portfolio artifact paired with the Chapter 0 Baseline Audit. The same piece of past work, audited again, by the same person, separated by the book. The cleanest single comparison the portfolio offers. (Chs 13, 0)

**Five-component specification.** *See: Specification components, five.*

**Fluency.** *See: AI Fluency.*

**Fluency trap.** The academic term for what happens when fluent output triggers an evaluation booster — readers trust well-written prose more than the evidence warrants. The fabricated citation is the visible symptom; the trust-in-fluency is the mechanism. (Ch 0)

**Four-layer verification.** *See: Verification layers, four.*

**Four-tier verification protocol.** *See: Verification tiers, four.*

**Framing.** The third of the four verification layers. Even when the facts are right and the reasoning is sound, the model made a choice about how to organize the analysis. Was it the right frame? Would a thoughtful expert in the domain have reached for a different one? (Ch 6)

**Generation rules.** The Automation specification section naming the per-item structure, confidence labels, format constraints, and quality criteria the model must produce against. (Ch 10)

**Governing files, three.** `CLAUDE.md`, `DESIGN.md`, and the `PROJECT.md` template. The three living files at the spine of the portfolio. Accrete across the book; travel to every new role. *See also: Portfolio.* (Chs 1, 3, 6, plus updates across most chapters)

**Hindi-tourist metaphor.** *See: American-in-India metaphor.*

**High-stakes outputs.** One of the six ambiguity types. Some outputs, as special cases, are more consequential than the design baseline. The right response is usually to detect them and halt, not handle them within the automation. (Ch 10)

**High Stakes / Irreversible.** Tier D of the four-tier verification protocol. Medical, legal, and financial decisions of real consequence. Anything where being wrong harms someone. At this tier, the verification is not a check on the output; it is the practice that makes the decision defensible. *See also: Verification tiers, four.* (Ch 6, Ch 12)

**Human Decision Node.** A designed point in an autonomous workflow where a human is required to take responsibility for the action about to happen. The architectural acknowledgment that some decisions cannot be delegated. Functional only when all four conditions (authority, information, time, accountability) are real. *See also: Human Decision Node, four conditions of.* (Ch 12)

**Human Decision Node, four conditions of.** Authority, information, time, accountability. All four must be real, or the Node — regardless of its form — is a signature waiting to happen. (Ch 12)

**Human-in-the-Loop Protocol.** The Chapter 12 portfolio artifact — the four-condition test applied to one Decision Node in the reader's work, plus the compressed adversarial spiral, plus an end-to-end worked example of an agentic deployment with the honest automation-rate finding. (Ch 12)

**Identity verification.** The third blast-radius dimension. Does the agent know whose authority it is acting on, and is that authority legitimate? The primary attack vector in adversarial environments. (Ch 11)

**Information.** The second of the four conditions of a functional Human Decision Node. Does the human at the Node have enough information to make a judgment, including information the AI did not surface? If the human can only see what the AI showed, they are approving the AI's framing, not judging. (Ch 12)

**Input drift.** One of the four Automation failure modes. The inputs to the system are no longer representative of the inputs it was designed for. Sources reliable in February less reliable in October. (Ch 10)

**Input-quality variation.** The first of the six ambiguity types. What the system does when an input is degraded, missing, or formatted differently than expected. (Ch 10)

**Intent.** The first of the five Specification components. Not the immediate task but the goal the task serves. What the practitioner is trying to do, named in advance, so the model and the practitioner share a definition of success. (Ch 3)

**Judgment Under Structure.** Tier 5 of the Seven Tiers. The practitioner authors the framework; the model applies it. Delegate the application; keep the authorship. *See also: Seven Tiers.* (Ch 4)

**Layer A.** Field-agnostic infrastructure. The three governing files and the customized framework templates. Same structure for every reader regardless of domain. *See also: Layer B, Portfolio.* (Throughout)

**Layer B.** Field-specific deliverables. The reader's actual work, annotated with the prompts that generated drafts and the verifications that approved them. The keystone Case Study is the largest Layer B artifact. *See also: Layer A, Portfolio.* (Throughout)

**Learning by Doing.** One of the Nine Capacities. Using AI in ways that amplify skills rather than replace them. Durably the human's responsibility — the practitioner has a body and a daily routine; the model does not. (Ch 2)

**Literacy.** *See: AI Literacy.*

**Loop, the.** Specify → Delegate → Converse → Discern → Be Diligent. Five steps, run as a cycle, with loop-back arrows where Discernment surfaces a problem with Specification. The book's central practitioner workflow. (Ch 1; runs through every chapter)

**Loop-back.** The return arrow from a later Loop step to an earlier one — usually Discernment back to Specification — when the work itself reveals that the earlier decision was wrong. The structural feature that distinguishes running the Loop from following it. (Ch 8)

**Low blast radius.** The third of the three appropriateness tests. If the system fails continuously for weeks before anyone notices, is the accumulated damage manageable? If not, either do not automate or design explicit human checkpoints in. (Ch 9)

**Mechanical Execution.** Tier 1 of the Seven Tiers. Tasks where the right answer is fully determined and doing it by hand builds no judgment worth keeping. Delegate freely. *See also: Seven Tiers.* (Ch 4)

**Meet Priya.** The one-page front-matter page that introduces the protagonist and names the broader audience. *See also: Priya Banksy.*

**Model drift.** One of the three drift forms. The model the recurring process runs on has changed — vendor update, fine-tuning, capability shift — producing different outputs on matching inputs. Caught by monthly fixed-test re-runs. (Ch 7)

**Model-specific failure modes.** One of the six ambiguity types. What the system does when the model hallucinates, refuses, or produces output that breaks the format spec. (Ch 10)

**Modes, Three.** Augmentation, Automation, Agency. The three relationships between human and AI. The Loop runs in each mode, and the steps reweight as the mode changes. *See also: Augmentation, Automation, Agency.* (Ch 1)

**Named accountable human.** The fourth of the four diligence components. One person whose job description includes maintaining the process — not just using it — with recurring review on their calendar. The fix for process laundering and the verification gap. (Ch 7)

**Nine Capacities.** *See: Capacities, Nine.*

**90-Day Plan.** The Chapter 13 portfolio artifact — two capacities, three commitments per capacity (daily rep, weekly review, 90-day artifact). The forward-looking piece of the portfolio. Scheduled on the calendar before the chapter closes. (Ch 13)

**No deliberation surface.** The third of the three structural failures of agentic AI. The agent has no social or temporal slowdown between deciding and executing — no thinking out loud, no colleague check, no sleeping on it. *See also: Three structural failures of agentic AI.* (Ch 11)

**No self-model.** The second of the three structural failures of agentic AI. The agent has no reliable internal signal for when an action is categorically out of proportion to the task it was given. *See also: Three structural failures of agentic AI.* (Ch 11)

**No stakeholder model.** The first of the three structural failures of agentic AI. The agent has no implicit map of whose interests matter in any given action. The explicit list of stakeholders the practitioner writes in will always be incomplete. *See also: Three structural failures of agentic AI.* (Ch 11)

**Noticing forms, three.** Sampling; adversarial test cases; outcome auditing. The three practices that replace real-time discernment when the human is not present at execution. (Ch 9)

**Omission.** The fourth and hardest of the four verification layers. Of all the things that are true about the topic, the model said some of them and not others — which unsaid things matter? Requires domain knowledge the output doesn't contain. The layer most often skipped and the one most expensive to fail at. (Ch 6)

**Operational.** Tier B of the four-tier verification protocol. Internal memos, non-production code, personal decisions. Run Layer 1 on specific claims; run Layer 2 on the main reasoning; take a quick pass at Layer 4. *See also: Verification tiers, four.* (Ch 6)

**Outcome auditing.** The third of the three Automation noticing forms — and the third of the four diligence components. Periodic review of what the system produced against what actually turned out to be true, broken down by the attributes that matter. (Chs 7, 9)

**Output drift.** One of the four Automation failure modes. The model is producing different outputs than it did at setup, given matching inputs. Caught by a fixed test set re-run on schedule. (Ch 10)

**Output format.** The fifth of the five Specification components. The structural shape of the deliverable — markdown or plain text, bullets or prose, sections and headers. Not a detail. The format constrains the kind of thinking the model does. (Ch 3)

**Output-volume variation.** One of the six ambiguity types. What the system does when the output is substantially longer or shorter than the design case. (Ch 10)

**Ownership Test.** The closing test the practitioner runs on themselves after the four adversarial moves and the verification pass: can I defend every paragraph to a hostile reviewer asking where it came from and why I stand behind it? If not, either learn the paragraph or cut it. (Ch 5)

**Pattern-Matching with Feedback.** Tier 2 of the Seven Tiers. Tasks where the right answer is well-defined but recognizing wrong answers requires domain knowledge. Delegate the generation; keep the evaluation. *See also: Seven Tiers.* (Ch 4)

**Performance paradox.** The phenomenon where a practitioner's daily output gets faster and more polished after adopting AI tools while their underlying judgment quietly atrophies. Visible only when something happens that the model has no signal for. *See also: Atrophying offload.* (Ch 4)

**Portfolio.** The reader's accreted record of fluency, assembled across the book. Three governing files plus customized frameworks plus field-specific deliverables plus diagnostics, fronted by the Cover Memo. Seventeen artifacts in five sections. The thing the practitioner hands to a future reader instead of arguing for their fluency. *See also: Cover Memo, Layer A, Layer B.* (Throughout; structurally named in Ch 0 and Ch 13)

**Practitioner Profile.** The Chapter 2 + Chapter 4 portfolio artifact (consolidated). Half capacities self-assessment, half delegation map. One of the three diagnostic artifacts in the finished portfolio. (Chs 2, 4)

**Pre-flight checks.** The Automation specification section naming what the system verifies before generation — for example, querying retraction pages, flagging articles older than the freshness window, refusing to generate when input quality drops below threshold. (Ch 10)

**Predictable inputs.** The second of the three appropriateness tests. Are the inputs the system will receive within a known range the design cases represented? The question is not whether the typical input is predictable; the question is whether the atypical inputs are represented. (Ch 9)

**Priya Banksy.** The book's single protagonist — 29 years old, BA Mass Communication from Symbiosis Institute of Media & Communication (Pune), AI Content Strategist at a US digital publication on her first year of OPT. Her arc runs from six months in (Chapter 0) to three years in (Chapter 13). Worked example, not template. The reader's field is the actual subject.

**Process laundering.** The first of the three accountability-obscuring mechanisms. When an AI produces an output and a human approves it, accountability distributes such that every participant can give an accurate exculpatory account and the cause of failure goes unexplained. Fixed by the named accountable human. (Ch 7)

**PROJECT.md.** The per-project state file with two layers — intent (what the project means, who it serves, what success looks like) and technical (what is built, what is generated and accepted versus rejected, what is verified). Instantiated for every significant Layer B deliverable. *See also: Governing files, three.* (Ch 3, instantiated at Ch 8)

**Rapid Prototyping.** One of the Nine Capacities. Treating model output as a draft to be tested in the world, not as the work itself. (Ch 2)

**Reasoning.** The second of the four verification layers. Given the facts, does the conclusion follow? Is there a skipped step, an unstated premise, a move that would not survive being written out explicitly? Harder than fact because the fault is structural. (Ch 6)

**Reversibility.** The second blast-radius dimension. Can the action be undone? The single most consequential dimension — a reversible mistake is a problem; an irreversible mistake is a catastrophe. (Ch 11)

**Role Dossier.** The one-paragraph file the reader writes at Chapter 0 naming their role, their typical tasks, their stakeholders, and the AI use in their current workflow. Attached to the reader's Claude Project so every future chapter exercise inherits the role context. (Ch 0)

**Role-and-rubric pattern.** The compressed structure introduced in Chapter 3 — assigning the model a specific professional persona plus explicit judgment criteria. A scaffold for the five Specification components, not a substitute. (Ch 3)

**Sampling.** The first of the three Automation noticing forms — reading a fraction of the outputs in full on a scheduled basis. Does not catch every failure; catches the persistent ones, which are most of the failures that matter. (Ch 9)

**Self-model.** *See: No self-model.*

**Seven Tiers.** Mechanical Execution → Pattern-Matching with Feedback → Synthesis from Sources → Drafting in Your Voice → Judgment Under Structure → Contestable Analysis → Accountable Judgment. The delegation-diagnostic taxonomy. Decompose a complex task, locate each component on the Tiers, hand over the bottom, partner on the middle, keep the top. (Ch 4)

**Specification.** Two senses. (1) The first Loop step — the thinking the practitioner does before opening the tool. (2) The five-component artifact that documents the thinking. The prompt is the document recording the specification, not the specification itself. *See also: Specification components, five.* (Ch 3)

**Specification components, five.** Intent, constraints, success criteria, exclusions, output format. The components every working specification carries, made explicit. (Ch 3)

**Specification Library.** The Chapter 3 portfolio artifact — five templates, one per recurring task type in the reader's role, each with a worked example. (Ch 3)

**Specify.** The first Loop step. *See also: Specification, Specification components, five.* (Chs 1, 3)

**Stakeholder model.** *See: No stakeholder model.*

**Stakeholder reach.** The first blast-radius dimension. Whose interests are affected if the agent acts incorrectly — yours, your team's, your customers', people who never heard of you? Constraining the agent's privileges is one of the few reliable blast-radius defenses available before any code runs. (Ch 11)

**Steelman.** The first and most powerful of the four adversarial moves. The prompt that asks the model to construct the strongest possible argument against a position. Catches directional error. The single move to deploy on any work the practitioner has spent more than twenty minutes building in conversation. (Ch 5)

**Still puzzling.** The chapter-end commitment naming what the author does not yet fully understand. Feynman's move. The pair to *What would change my mind.* (Throughout)

**Stochastic Reasoning.** One of the Nine Capacities. Handling uncertainty honestly — the practitioner's, the model's, the world's. Contested in durability — models are improving at calibrated uncertainty quantification in narrow domains. (Ch 2)

**Strategic Delegation.** One of the Nine Capacities. Deciding, before beginning, what the model should do and what the practitioner should do, and why. Durably the human's responsibility — accountability cannot be delegated to a model. (Ch 2)

**Success criteria.** The third of the five Specification components. How the practitioner will know, after the fact, that the output is good — the recipient action or test the output has to pass. (Ch 3)

**Sycophantic drift.** The failure mode in which an AI conversation moves the whole way in one direction because the practitioner is framing and the model has been trained to develop the position the user supplies. Not a moment; a direction. Defeated by the four adversarial moves. (Ch 5)

**Synthesis from Sources.** Tier 3 of the Seven Tiers. The model gathers and combines information from multiple sources; the practitioner evaluates. The Tier-specific risk is omission — the synthesis tells you what the sources say but not what the sources do not say. *See also: Seven Tiers, Performance paradox.* (Ch 4)

**Technical Understanding.** One of the Nine Capacities. Knowing enough about how the system works to predict where it will fail. Practitioner depth, not research depth. (Ch 2)

**Theoretical Foundations.** One of the Nine Capacities. Keeping enough domain knowledge to judge whether AI output is good. Without it, the practitioner is not collaborating with the model — they are taking dictation. (Ch 2)

**Three structural failures of agentic AI.** No stakeholder model; no self-model; no deliberation surface. Not three separate bugs — three faces of one underlying gap: judgment. (Ch 11)

**Tiers, Seven.** *See: Seven Tiers.*

**Time.** The third of the four conditions of a functional Human Decision Node. Does the human have enough time to actually use the information and authority they have? The most frequently violated and most quietly violated condition. (Ch 12)

**Tool diffusion.** The second of the three accountability-obscuring mechanisms. When a tool works, it spreads — secondary users adopt it with partial understanding of what it was designed for. Fixed by a living document the tool's owner maintains. (Ch 7)

**Translate before you move on.** The chapter-end block in every Botspeak chapter. The explicit prompt asking the reader to name their domain's equivalent of Priya's case and to produce the chapter's portfolio artifact in their own field. The book's "fluency in your field" thesis made operational. (Throughout)

**Trivial.** Tier A of the four-tier verification protocol. Drafts the practitioner will edit, brainstorms, throwaway code. Verify at Layer 1 on specific claims if at all. *See also: Verification tiers, four.* (Ch 6)

**Use case drift.** One of the three drift forms. The task the recurring process is being applied to has expanded beyond what the original spec covered. A tool built for one beat used quietly on another. (Ch 7)

**Verification gap.** The third of the three accountability-obscuring mechanisms. Checking whether the process is still working is someone's responsibility in general and no one's in particular. Closes only one way: scheduled checks with dates and owners on a calendar. (Ch 7)

**Verification layers, four.** Fact, reasoning, framing, omission. The four kinds of error and the four checks that catch them. Roughly increasing in difficulty; most practitioners run only the first. *See also: Verification tiers, four.* (Ch 6)

**Verification tiers, four.** Trivial (drafts), Operational (internal memos), External (anything that publishes), High Stakes / Irreversible (medical, legal, financial, named harm). Verification effort scales with what the practitioner has to lose. *See also: Verification layers, four.* (Ch 6)

**Verification standard.** The DESIGN.md section naming the quality bar any output must clear before it leaves the practitioner's hands. *See also: DESIGN.md.* (Ch 6)

**Voice and register.** The DESIGN.md section naming what the practitioner's domain expects of their outputs — what tells a reader the work was done by someone in this field, to this field's standard. *See also: DESIGN.md.* (Ch 6)

**What would change my mind.** The chapter-end commitment naming the specific evidence or argument that would cause the chapter's reading to revise. The pair to *Still puzzling.* (Throughout)

**Worked Loop Log.** The Chapter 1 portfolio artifact — one recent piece of the reader's work taken through all five Loop steps with time-stamps. The first piece of evidence that prefigures the Chapter 8 keystone. (Ch 1)

---

## About the author

Nik Bear Brown writes textbooks for working professionals in fields where the working consensus is moving faster than the published consensus — AI fluency, computational finance, computational skepticism, the design of agentic systems. The books are written for the practitioner who has to do the work on Monday morning, not the academic researcher who has the year.

The voice across the books is consistent: explanation over assertion, mechanism over name, calibrated uncertainty over false confidence. If a chapter cites an authority by reference rather than as an instrument under test, the chapter is not yet doing the method.

---

## Colophon

*Botspeak* was drafted in markdown using the Feynman-flavored editorial method described in the workshop's `CLAUDE.md`. Source was version-controlled. Chapters were drafted, reviewed against working-practitioner cases, and revised before any chapter shipped. The book is set in the typeface your reader chose for it.

The figures are intentionally austere — monochrome warm grayscale, serif type, no rounded corners, no shadows, no color highlights. The design choice is editorial: the reader's attention should fall on what the figure shows, not on how the figure presents itself.

The AI Wayback Machine sections close each chapter with a contemporary tool — a prompt to a large language model — pointed at a thinker whose foundational work is older than the millennium. The pairing is deliberate. The point is not nostalgia. The point is that the practitioner who can run a useful prompt about Vygotsky has already done part of the practice the book is teaching.

---

## A note on revision

This is a first edition. The field is moving fast enough that some specific tool or technique in this book will be obsolete before many readers finish it. The Loop will not be obsolete. The Capacities will not be obsolete. The ability to separate your contribution from the model's, and stand behind your contribution on your own authority, will not be obsolete — it will become more valuable as the field matures.

If a chapter's reading is wrong, the corrigenda live at the workshop's repository.

— *End of book.*

