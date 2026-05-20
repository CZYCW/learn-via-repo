# exercises/ Problem Set Template

> Each time you finish a `stage-3-walkthroughs/{NN}-{topic}.md`, immediately append the topic's questions to all three files in `exercises/`. Questions are organized under `## {NN}-{english-short-title}` headings, one-to-one with the walkthrough filenames. **Generation order**: walkthrough first, then the three exercise files — atomically complete the same topic.
>
> Examples are mostly from the AI agent domain (the validated case); other domains use the same structure — see §6 cross-domain examples appendix.

---

## Problem set directory structure

```
exercises/
├── README.md              ← How to use + difficulty legend + usage
├── concept-checks.md      ← Feynman-style (does the student really understand)
├── code-finding.md        ← file:line location (can they trace code independently)
└── transfer.md            ← Transfer to user's project (can they apply)
```

---

## §1. concept-checks.md template (Feynman-style)

**Goal**: check whether the student really understands the concept, not "thinks they do."
**When**: after §1-§3 of each walkthrough, before entering §4 code. This is Checkpoint A in the teaching rhythm.
**Pass criteria**: can explain in one sentence without jargon + reverse argument + Repack using jargon.

### Template (3 per topic)

```markdown
## {NN}-{english-short-title}

### Concept check 1: Feynman one-sentence explanation

**Question**: In one sentence, **without any jargon**, tell me what problem {core concept} solves.

**Pass criteria**:
- No use of `{term 1}` `{term 2}` `{term 3}` etc
- One sentence covers both pain point and solution
- A non-expert in this domain can follow

**Follow-up after passing**:
"Now describe it again using the terms" — must be able to Repack, otherwise the concept isn't internalized yet.

---

### Concept check 2: reverse argument

**Question**: If {core concept} didn't exist, what's the worst that would happen?

**Pass criteria**: can describe at least 2 concrete scenarios, each matching a problem that {core concept} solves.

---

### Concept check 3: boundary probe

**Question**: In what situation does {core concept} fail? Or: in what scenario shouldn't you use {core concept}?

**Pass criteria**: can identify the approach's limitations, showing the student didn't just memorize "X is good" but understood the trade-off.
```

### 3 complete examples (based on OpenClaw teaching)

```markdown
## 02-react-loop-and-subagents

### Concept check 1: Feynman one-sentence explanation

**Question**: In one sentence, no "ReAct" / "tools" / "loop" / "recursion" jargon, tell me what problem ReAct solves.

**Pass criteria**: something like "lets the AI look things up while writing a report, instead of looking everything up first or just making it up."

**Follow-up**: "Now describe the same process using Reasoning, Acting, Observation."


### Concept check 2: reverse argument

**Question**: If an LLM only reasoned and never acted, what would happen? What about acting without reasoning?

**Pass criteria**:
- Only reason, no action → hallucination (fabricates facts because the model only knows training-time data)
- Only act, no reason → blindness (doesn't know which tool to use, can't chain tools)


### Concept check 3: boundary probe

**Question**: What kind of task is over-engineered with ReAct?

**Pass criteria**: can identify "one-shot Q&A" tasks (e.g., "what's 3+5") — those don't need tools, plain LLM works.
```

---

## §2. code-finding.md template (file:line location)

**Goal**: check whether the student can independently open a repo file and find the key code — that's the core of "independently tracing code."
**When**: after §4-§5 of each walkthrough. This is Checkpoint B+ in the teaching rhythm.
**Pass criteria**: at least 2 of 3 correct, with precise `file:line`.

### Template (3 per topic)

```markdown
## {NN}-{english-short-title}

### Code finding 1: core entry

**Question**: Open `{file}`, find the line that implements {function/class/concept}.

**Expected answer**: `{file}:{line}` ({function_or_concept_name})

**Follow-up**: Which step of the minimal version does this correspond to?

---

### Code finding 2: minimal-version mapping

**Question**: What did the minimal version's `{minimal_var_or_func}` turn into in the repo?

**Expected answer**: `{file}:{line}`'s `{class.method}()`, because {why the repo turned it into this — usually concurrency safety / persistence / type checking / error handling}.

---

### Code finding 3: industrial-enhancement trace

**Question**: Near `{file}:{line}` the repo does one extra thing the minimal version doesn't — what is it? Why?

**Expected answer**:
- Extra: {concurrency lock / timeout / TTL cache / etc}
- Why needed: {concrete scenario, e.g., "two messages entering the same session simultaneously would corrupt the transcript"}
```

### 3 complete examples (based on OpenClaw teaching)

```markdown
## 02-react-loop-and-subagents

### Code finding 1: core entry

**Question**: Open `src/agents/pi-embedded-runner/run/attempt.ts`, find the line that triggers the ReAct loop.

**Expected answer**: `attempt.ts:1627`, `await abortable(activeSession.prompt(effectivePrompt));`

**Follow-up**: Which step of the minimal version does this correspond to?
**Expected answer**: corresponds to the minimal version's `act()` recursive entry — `activeSession.prompt()` runs the full LLM → tool_use → execute_tool → continue loop inside.


### Code finding 2: minimal-version mapping

**Question**: What did the minimal version's `messages = []` turn into near OpenClaw's ReAct entry?

**Expected answer**: `attempt.ts:991`'s `SessionManager.open(params.sessionFile)` — swaps the in-memory list for disk JSONL persistence, because multi-message scenarios need persistent state + restart recovery.


### Code finding 3: industrial-enhancement trace

**Question**: Near `attempt.ts:991` the repo does one extra thing the minimal version doesn't — what is it? Why?

**Expected answer**:
- Extra: `guardSessionManager(...)` wrapping + `acquireSessionWriteLock` (a few lines earlier)
- Why needed: prevents two concurrent messages on the same session from corrupting the transcript by writing simultaneously
```

---

## §3. transfer.md template (transfer to user's project)

**Goal**: check whether the student can transfer the repo's patterns to their own target project — this is the "Create" level of Bloom's taxonomy.
**When**: after §7 of each walkthrough, or in a full review after all walkthroughs.
**Pass criteria**: no standard answer, but the student can say "I'll use this pattern in my project this way" / "this pattern doesn't fit my project because ..., so I'll change it to ..." — passes.

### Template (2 per topic)

```markdown
## {NN}-{english-short-title}

### Transfer 1: direct reuse

**Question**: How can the repo's `{core pattern}` be used in your project ({user_project})?

**Direction**:
- Does your project have a similar scenario to {the repo's problem scenario}?
- Can you copy it directly? Which parameters need to change?
- Describe the pattern's application using a concrete scenario from your project.

---

### Transfer 2: identify when it doesn't fit + redesign

**Question**: The repo's `{core pattern}` **can't be used directly** in your project — possibly because {example reason}. Identify the gap and propose a redesign.

**Direction**:
- What did the repo assume (single user / local deploy / markdown-friendly)?
- What's different in your project (multi-user / cloud / structured data)?
- Under your assumptions, how should the pattern change? Keep what, replace what?
```

### 3 complete examples (based on OpenClaw → Mnemos / AI coach)

```markdown
## 03-session-and-memory

### Transfer 1: direct reuse

**Question**: How can OpenClaw's "three-tier memory" (Bootstrap hot / Semantic warm / Episodic cold) be used in Mnemos?

**Direction**:
- What in Mnemos corresponds to OpenClaw's "user profile"? (→ Bootstrap)
- What corresponds to "historical consultation events"? (→ Episodic)
- What corresponds to "topic-based retrieval"? (→ Semantic)
- What capacity limit and retrieval strategy would you set for each tier?


### Transfer 2: identify when it doesn't fit + redesign

**Question**: OpenClaw's "file is the source of truth + SQLite index" **can't be used directly** in Mnemos because Mnemos is a multi-user cloud service. Identify the gap and redesign.

**Direction**:
- OpenClaw assumes "single user + local files + user can edit markdown directly" — none of these hold in your multi-user scenario
- Redesign direction: Postgres + pgvector instead of SQLite + sqlite-vec, but keep "export as markdown" so users can audit
- Must keep: three-tier architecture (unchanged), Hybrid + MMR + Temporal Decay (unchanged), Memory Flush (idea kept, implementation upgraded to write structured memory)
- Must change: single-file storage → per-user table partitioning, file system watcher → Postgres trigger / CDC
```

---

## §4. README.md (exercises/) template

```markdown
# Exercises Guide

## Difference between the three types

| Type | Checks | When | Pass criteria |
|------|------|--------|---------|
| concept-checks | Real concept understanding (Feynman) | After §1-§3 of each walkthrough | One sentence no jargon + reverse argument + Repack |
| code-finding | Code-location ability | After §4-§5 of each walkthrough | At least 2 of 3 with precise file:line |
| transfer | Transfer to your project | After §7 or overall review | No standard answer; can say "how I'd use it in my project" |

## Difficulty legend

- 🟢 Easy: answer in 1 minute
- 🟡 Medium: think for 2-5 minutes
- 🔴 Hard: go back to code or docs for 5-15 minutes

## Correspondence with walkthroughs

Each `## {NN}-{english-short-title}` heading maps to `stage-3-walkthroughs/{NN}-{english-short-title}.md`.

After finishing a walkthrough, in order:
1. concept-checks.md#{NN}-{topic} (if stuck, go back to walkthrough §1-§3)
2. code-finding.md#{NN}-{topic} (if stuck, go back to walkthrough §4-§5)
3. transfer.md#{NN}-{topic} (no answer key, but say it out loud)
```

---

## §5. Anti-examples: what makes a question disqualified

```
❌ "Do you understand ReAct?"
   Problem: too subjective; student can lie and say "yes"
   Fix: use a Feynman one-sentence check

❌ "Explain the role of pi-agent-core."
   Problem: too broad, no clear pass criterion
   Fix: split into multiple precise file:line questions

❌ "Which tools are needed in the ReAct Loop?"
   Problem: open-ended design question, not verifiable
   Fix: change to "find the function that assembles the tool list in attempt.ts"

❌ "If you were designing a ReAct system, how would you do it?"
   Problem: too big; the student can ramble indefinitely
   Fix: move to transfer.md, constrain to "in your project's scenario"
```

---

## §6. Cross-domain examples appendix (added in V3)

Examples in §1-§4 above are mostly AI-agent flavored. Other domains use the same structure — here's one example from each domain:

### concept-checks cross-domain examples

| Domain | Concept | Feynman one-sentence question |
|------|------|----------------|
| Web framework | middleware chain | "In one sentence, no 'middleware/next' jargon, tell me what problem `app.use(...)` solves." |
| Database internals | B-tree | "In one sentence, no 'B-tree/page' jargon, tell me why a B-tree is faster than a linked list." |
| Compiler | tokenization | "In one sentence, no 'token/lexer' jargon, tell me why a compiler first slices the source into pieces." |
| OS kernel | context switch | "In one sentence, no 'register/stack' jargon, tell me how the OS runs multiple programs at once." |

### code-finding cross-domain examples

| Domain | Location question | Expected answer format |
|------|------|------------|
| Web framework | "Open Express's application.js, find the implementation of `app.use`" | `application.js:228` |
| Database internals | "Open SQLite's btree.c, find the cursor entry function" | `btree.c:5234`'s `sqlite3BtreeNext` |
| Compiler | "Open Acorn's parser/expression.js, find the expression-parsing entry" | `parser/expression.js:90` |
| OS kernel | "Open xv6's trap.c, find the syscall dispatch line" | near `trap.c:67`, `syscall()` |

### transfer cross-domain examples

| Domain | Transfer question |
|------|------|
| Web framework | "How can the target repo's middleware chain be used in your project? E.g., when you build your API gateway / your own web app, how would you reuse it?" |
| Database internals | "How can the target repo's cursor abstraction be used in your project? E.g., how would you borrow from it when doing streaming data processing?" |
| Compiler | "How can the target repo's AST visitor pattern be used in your project? E.g., how would you borrow from it when building a config parser?" |
| OS kernel | "How can the target repo's process scheduling algorithm be used in your project? E.g., how would your worker pool borrow from it?" |

For more detailed per-domain questions, expand dynamically following this appendix's format when generating the walkthrough companion.
