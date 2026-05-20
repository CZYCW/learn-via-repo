# learn-via-repo Teaching Methodology

> This is the core methodology of the learn-via-repo skill. Every step the skill takes — generating teaching artifacts and actually teaching — must follow this document.
>
> The methodology is abstracted from `~/Desktop/projects/openclaw/docs/learning/TEACHING-STYLE.md` and validated in AI-agent teaching (OpenClaw). **V3 generalized it to any software engineering domain** — examples in this doc are mostly AI-agent flavored; cross-domain anchors live in `multi-domain-examples.md` §1 (which maps each concept to web frameworks / database internals / OS kernels / compilers / game engines / distributed systems / ...).

---

## Table of Contents

- **§1. Teaching philosophy** — three success criteria + the fundamental taboo
- **§2. Concept and principle teaching philosophy**
  - §2.1 Feynman technique — don't accept "I get it"; check with one sentence, no jargon
  - §2.2 External-material driven — bring in authoritative material to land the core Why
  - §2.3 Semantic waves — concept → concrete → back to concept
- **§3. Three-layer progression** — why / what / how
- **§4. Minimal Comparison Method (core method)**
  - §4.0 Step 0: high-level code map
  - §4.1 Step 1: find an authoritative minimal implementation — three-tier priority, AI doesn't improvise
  - §4.2 Step 2: show the target repo's matching code (file:line + comments)
  - §4.3 Step 3: write a three-column comparison table
  - §4.4 Step 4: write the "industrial-strength enhancements" explanation
- **§5. Code navigation** — always start from one request's path
- **§6. Lesson pacing (one 45-60 min lesson)** — where Checkpoints A/B fire
- **§7. Core requirement for test questions** — must be code-verifiable
- **§8. The methodology's scope and what can't be compromised**

---

## §1. Teaching philosophy

**Core goal**: the student can **trace code on their own**, not just "follow what the teacher said."

Three criteria for whether teaching worked — can the student, independently:

1. Open an unfamiliar module file in the target repo and locate the core logic
2. Explain in their own words "what this code is doing and why it's written this way"
3. Map the code's behavior to a domain concept they already know

**The fundamental taboo**: leaving the student with "I listened, but the code still doesn't make sense." That's a teaching failure, not a learning-ability problem.

---

## §2. Concept and principle teaching philosophy

Concepts and principles are the foundation of the whole teaching system — if the foundation is shaky, all the code understanding on top of it floats.

### §2.1 Feynman technique

**Core belief**: if you can't explain something in the simplest possible language, you don't really understand it yet.

Three operating rules during teaching:

1. **Don't teach the definition; teach "why this problem exists"**
   - Wrong: `ReAct = Reasoning + Acting combined`
   - Right: `What happens if an LLM only reasons and never acts? (Hallucination.) What happens if it only acts without reasoning? (Blind.) ReAct is the minimal solution to that tension.`

2. **Don't accept "I think I get it" — use Feynman to verify**
   - The check: "In one sentence, no jargon, tell me what problem this thing solves."
   - The student can't say it clearly → you've found the blind spot → that's where to focus next
   - The student can say it clearly → bring them back to the term layer (Repack) → that's when the concept is really internalized

3. **Better slow than fast**
   - Better to take 2x as long to land one concept than rush through 5
   - A cognitively overloaded student will fake understanding — that's more dangerous than "I don't get it"

### §2.2 External-material driven

The concept / principle layer isn't built in isolation — sometimes one figure from a paper does more than 1000 words of explanation.

**Operating rules**:
- For each core concept, actively search for authoritative material that "directly answers this Why"
- Not "material related to this topic," but "material that lands the core insight in one sentence"
- After bringing in the material, immediately map it to the target repo's implementation (no islands of external knowledge)

**Example** (using the AI agent domain):

| Concept | Material to bring in | Core insight |
|------|------------|---------|
| Why does ReAct need Reason + Act combined | ReAct paper (Yao 2022) experimental data | Pure CoT has high hallucination / pure Act has weak reasoning |
| Why is memory layered into three tiers | Lilian Weng's cognitive-science framework | Biological analogy: sensory / working / long-term memory |
| Why use graph memory | Mem0 + Zep papers | Vector retrieval has a blind spot for relational reasoning |
| Why tool design needs poka-yoke | Anthropic's ACI article | Tools = agent's cognitive interface; as important as HCI |

### §2.3 Semantic waves

Source: computing-education research (Maton 2013, Legitimation Code Theory).

A good explanation traces a full wave:

```
High abstraction              technical term
(low concreteness)         (high complexity)
     │                          ↑
     │   "ReAct = reason+act"   │ ← Repacking (pack it back up)
     │                          │
     ▼   concrete example        │
(high concreteness)         (low complexity)
  "It's like writing a report while
   you're looking things up — you don't
   wait until you've read everything"
```

**Cross-domain analogies** (same pattern applies; AI agents are just one example):
- Web frameworks: "`app.use((req,res,next)=>...)` middleware" unpacks to "every station on the factory line does something to the package then passes it on"; repacks to "onion model / chain of responsibility"
- Databases: a B-tree node split unpacks to "the shelf is full, split the books across two shelves and add a pointer in the index"; repacks to "B-tree balance"
- Compilers: lexical analysis unpacks to "splitting a sentence into individual characters"; repacks to "tokenization"

**Two forbidden mistakes**:

- ❌ **Down only** ("descending elevator"): lots of concrete examples, never back to terms → the student can't transfer to other situations
- ❌ **Up only** ("stuck in the clouds"): all abstract definitions and architecture diagrams, no concrete examples → cognitive overload, nothing lands

**The right move**: for every concept, explicitly Unpack (turn the term into a concrete example) and then Repack (turn the example back into the term).

**Check**: "Can the student now describe the concrete example we just did using the technical term?"

---

## §3. Three-layer progression

Every concept must be taught in this three-layer order. Never skip a layer:

```
Layer 1: Why? (panorama)
  - What happens if this thing doesn't exist? (Reverse argument)
  - In this tech domain's ecosystem, what's the standard solution?
  - What did the target repo choose, and why?

Layer 2: What? (architecture)
  - Core concept definition (one sentence)
  - Component relationship diagram (text or ASCII / mermaid)
  - Key design decisions (at most 3, ADR format: Context → Decision → Consequence)

Layer 3: How? (implementation)
  ⓪ First: high-level code map
  ① Then: minimal implementation (skeleton)
  ② Then: the target repo's matching code (comparison)
  ③ Explain: industrial-strength enhancements (the diff)
```

**Never allowed**: jumping past layers 1-2 into layer 3, or showing the repo's complex code without first laying down a minimal implementation.

---

## §4. Minimal Comparison Method (core method)

This is the most important method in the whole teaching system. Every stage-3-walkthroughs/ lesson must contain the full five-step Minimal Comparison Method.

### §4.0 Step 0: high-level code map

Give the student a map before asking them to walk.

- List the core files involved (3-5)
- Draw the main function-call chain (not internal logic — A calls B calls C)
- Say where data comes in and where it goes out
- Format: a text path diagram, each node tagged with `file.ts:line`

Goal: before the student sees the minimal skeleton, they already know "where the real code lives, roughly in what order" — that prevents a disconnect between the minimal version's concepts and the real code files.

### §4.1 Step 1: find an authoritative minimal implementation (V2 upgrade — three-tier priority)

> **Important change (V2)**: the old approach (AI writes 30-100 lines on the fly) is deprecated. Reason: AI-improvised code looks right but may not run, may not match the authoritative implementation, and forces the student to verify it. New approach: **every "minimal implementation" must come from real, runnable, community-vetted code**, found via the three-tier priority below.

#### Three-tier priority

| Priority | Source | When to use |
|--------|------|--------|
| 1 | **The beginner repo code learned in stage-0** | Preferred. The student already ran it, read it, knows it best. Reference form: `stage-0-fundamentals/{repo-name}/{path}:{line}` |
| 2 | **A domain-authoritative "minimal implementation" repo** (user-evaluated and confirmed — AI doesn't unilaterally pick) | Backup. **Qualifying types**: educational repos by well-known authors (big-name engineers / course authors), minimal-implementation repos that target "a few hundred lines of teaching code" (e.g., `nano-*` / `mini-*` / `tiny-*` naming), single-notebook complete teaching examples. **Disqualifying types**: cookbook / API SDK docs / production demos — those are reference materials, not progressive teaching (see `forbidden-list.md` §5b meta-lesson 2). Reference form: `{owner}/{repo}/{path}:{line}` |
| 3 | **AI-simplified version (only when 1 and 2 both fail)** | Last resort. AI makes an annotated/summary version based on an authoritative implementation from 1 or 2 and **must** mark it `"based on X, simplified for explanation, not independently verified to run"`. Never "write one from scratch out of memory." |

#### Selection criteria (used for priorities 1 and 2)

- ✅ **First principles**: directly calls a low-level API (any underlying provider) + standard library; the **core control flow of the domain is visible** (skeleton elements vary by domain — for AI agents it's `messages.append + tool_use dispatch`, for web frameworks it's `next() chain`, for databases it's `cursor + opcode loop` — see `multi-domain-examples.md` §1)
- ✅ **Companion teaching content**: complete README / companion blog post / video / issue Q&A
- ✅ **Authoritative backing**: Star ≥ 1k or big company / known engineer / known course
- ✅ **Actively maintained**: commits in the last 6 months
- ❌ **Mature-framework abstractions that hide the core control flow** — frameworks that wrap the domain's core logic into a few API calls (different domains have different "wrapper-crime suspects" — for AI agents it's the langchain family, for web it's NestJS / Spring, for databases it's sqlalchemy / typeorm, etc. See `forbidden-list.md` §5 for the judgment method + the per-domain disqualifying-framework list)
- ❌ Just an article collection without runnable code

Details: `forbidden-list.md` §5.

#### Writing standard

When referencing source code, **show the original code** plus a **5-10 line pseudocode summary**:

````markdown
**Minimal implementation source** (**the actual recommended repo comes from Phase 2C web search + user evaluation**; below is a real example from OpenClaw teaching):
  Leonie Monigatti notebook (Anthropic API, 4-component progression)
**File location**: `iamleonie/website/blob/main/blog/ai-agent-from-scratch-in-python.ipynb` Section 4
**Why this is the authoritative minimal implementation**: author has an ML engineer background;
  4-component clean progression (LLM / memory / tool / agent loop);
  no framework end-to-end (calls anthropic SDK directly); same API family as most modern AI agent repos.

---

**5-10 line pseudocode summary** (only an aid for understanding the skeleton — to run the code, go back to the real file above):

```python
# Adapted from Leonie's notebook Section 4. Strips error handling / streaming, keeps the ReAct triplet skeleton.
def act():
    """ReAct loop core: until the LLM stops producing tool_use"""
    response = call_llm(messages, tools)
    if response.stop_reason == "tool_use":
        result = execute_tool(...)
        messages.append(result)
        return act()  # recurse
    return response.text  # done
```

> **Cross-domain analogy**: the above is an AI-agent example of "minimal skeleton." Other domains have the same "a few lines reveal the core control flow":
> - Web frameworks: 3-5 lines is enough to see `middleware → next() → handler`
> - Databases: 5-10 lines of cursor operations show B-tree traversal
> - Compilers: 10 lines of tokenize + AST construction reveal the parsing skeleton
> - OS kernels: trap entry + scheduler queue can be expressed in 20 lines of pseudocode
>
> See `multi-domain-examples.md` §1 "skeleton elements" column — every domain has a "few lines that show the essence" version.
````

**Why this design**:
- The student **first sees real, runnable code** (authoritative repo's file:line)
- The 5-10 lines the AI writes are just a "translation" into a more compact form, to help the teacher walk through the skeleton — explicitly labeled "this is a summary, not a runnable version"
- If the student wants to run it, modify it, verify it — go back to the real repo

#### Anti-examples: things forbidden in v2

```
❌ Drop 80 lines of AI-improvised Python into walkthrough §4.1 with no "source"
   Consequence: doesn't run / diverges from the authoritative implementation / student doesn't know where to verify

❌ Reference a repo without a precise file:line, just "similar to X's implementation"
   Consequence: the student can't find it

❌ Reference a langchain-based beginner repo
   Consequence: what the student learns is framework APIs, not the underlying skeleton
```

### §4.2 Step 2: show the target repo's matching code (file:line + comments)

- Give the precise `file.ts:line` reference
- Annotate "which line / which function of the authoritative minimal version this corresponds to"

```typescript
// OpenClaw example (minimal-implementation source: {stage-0 recommended repo}/path/to/react-loop.py:42-78
//  — the recommended repo is filled in after Phase 2C web search + user evaluation, AI doesn't unilaterally pick):

// attempt.ts:991
// Corresponds to authoritative minimal version's: messages = [] ({stage-0}/react-loop.py:15)
sessionManager = guardSessionManager(SessionManager.open(params.sessionFile), { ... });

// attempt.ts:1627
// Corresponds to authoritative minimal version's: act() recursive entry ({stage-0}/react-loop.py:60)
await abortable(activeSession.prompt(effectivePrompt));
```

> **Methodology iron-rule (V2 addition)**: the AI must not declare a repo "qualified as an authoritative minimal implementation" from memory. It must run a real Phase 2C search, use WebFetch to verify the README has no `from langchain import ...` or similar framework imports, hand 3-5 candidates to the user for evaluation, and only after user confirmation write the reference into §4.1 / §4.2. See `forbidden-list.md` §5.

### §4.3 Step 3: write a three-column comparison table

Always three columns: minimal version / repo code location / explanation

**Example (AI agent domain / OpenClaw as target repo)**:

```markdown
| Minimal version | Repo code location | Explanation |
|---------|-------------|------|
| `messages = []` | `SessionManager.open(jsonl)` in `attempt.ts:991` | In-memory list → disk persistence |
| `call_llm()` | `activeSession.prompt()` in `attempt.ts:1627` | Direct call → wrapped in pi-agent-core |
| `execute_tool()` | `tool.execute()` via pi-agent-core | Simple dispatch → type check + permissions + timeout |
```

**Cross-domain example** (the three-column table works the same for other domains):

| Domain | Minimal version (example) | Target repo code location (example) | Explanation |
|------|------|----------|------|
| Web frameworks | `function handler(req, res) { res.send('hi') }` | `app.use('/x', fn)` in `application.js:280` | Direct handling → middleware chain + route matching |
| Databases | `for row in table: yield row` | `BtreeNext()` in `btree.c:7234` | In-memory traversal → disk page IO + cursor state machine |
| Compilers | `tokens = src.split(' ')` | `Scanner::Scan()` in `scanner.cc:412` | Naive split → character-class lookup + state machine |
| OS kernels | `def schedule(): next_proc.run()` | `swtch(&old.ctx, &new.ctx)` in `swtch.S:8` | Function call → register context switch |

### §4.4 Step 4: write the "industrial-strength enhancements" explanation

Use a "diff text diagram," not a Markdown table (because the content is too long to lay out well):

```
Minimal version (N lines)     Repo enhancements (M lines)
─────────────────              ──────────────────────────
xxx = yyy             →    industrial feature 1 + industrial feature 2
aaa()                 →    more complex implementation
                            + extra cases considered
─────────────────              ──────────────────────────
Core principle: the extra lines aren't "more concepts" — they're "doing the same thing more robustly"
```

**Core belief**:

> "More lines of code = doing the same thing more robustly, safely, flexibly.
> Not more new concepts.
> Once you understand the 80-line skeleton, you understand the intent of the 1600-line version."

Say this every time you're about to face complex code.

---

## §5. Code navigation

Telling the student "where to start reading the code" matters more than "explaining what the code does."

### §5.1 Standard code-navigation format

```
Round 1 (30 min): [specific goal, e.g., "trace one message"]
1. Open src/xxx/yyy.ts, search for functionName (around line N)
2. Focus on these lines (give a line range)
3. What's happening here? (one sentence)

Round 2 (30 min): [specific goal, e.g., "understand the ReAct loop"]
...
```

### §5.2 "Always start from one request's path"

**Always start from "one request's path"**, not from `entry.ts` or `index.ts` — that's where the noise is.

Why:
- `entry.ts / index.ts` is initialization code; it has nothing to do with "what this repo does"
- The student follows a real request from its entry point — that's how they feel "what the system is doing"
- Data flow has direction; following the data = following the real business logic

### §5.3 Code path diagram format

```
User sends a message
    │
    ▼
src/foo/bar.ts:730      ← what the entry does (one sentence)
    │ (calls)
    ▼
src/baz/qux.ts:235      ← what the next hop does
    │
    └── Focus on these lines here:
        - line 991: acquireSessionWriteLock()  ← why? prevent concurrent writes
        - line 1068: createAgentSession()      ← which step of the minimal version this maps to
        - line 1627: activeSession.prompt()    ← this is the key one!
```

### §5.4 file:line reference spec

When referring to a code location in prose, always use `filename:line` or Markdown link form:

```
Inline: `attempt.ts:1627` or [attempt.ts:1627](src/agents/pi-embedded-runner/run/attempt.ts#L1627)
Code block comment: // attempt.ts:1627
Path diagram: src/agents/pi-embedded-runner/run/attempt.ts:1627
```

---

## §6. Lesson pacing (one 45-60 min lesson)

```
0-5 min: panoramic question
  "Imagine X doesn't exist. What happens?"
  → make the student feel why this module needs to exist

5-20 min: concepts and architecture (Layer 1 + 2)
  - One ASCII / mermaid architecture diagram
  - 2-3 core concepts, each: one-sentence definition + concrete example (semantic-wave Unpack)
  - 1-2 key design decisions (ADR format)
  - Bring in external high-quality material (core insight from a paper / authoritative blog)

  ★ Checkpoint A: concept understanding check (BEFORE going to code!)
    "In one sentence, no jargon, tell me what problem this [concept] solves."
    - Student says it clearly → bring them back to the term layer (semantic-wave Repack) → continue
    - Student can't say it → found the blind spot → add examples / external materials until they can
    - Strictly no skipping this checkpoint to go straight to code

20-40 min: minimal comparison (Layer 3)
  - Step 0: high-level code map (file:line path diagram, 3-5 core files)

  ★ Checkpoint B: code-skeleton check
    "Open [file]. Can you find where the request comes in?"
    - Found it → continue, show the minimal implementation
    - Can't find it → rebuild the file relationships, give more path hints

  - Step 1: show the minimal implementation (code + explanation)
  - Steps 2-4: show the repo's matching code (file:line + comparison table + industrial-strength enhancements)

40-50 min: code navigation
  - Concrete steps to read the code (in rounds)
  - file:line reference for each key file

50-60 min: test
  - 3 standard questions (see exercises-template.md)
  - Have the student answer out loud; find the points they didn't get
```

For detailed scenario templates (what to do when the student is stuck, how to teach a deep-read of one file), see `checkpoints-and-scenarios.md`.

---

## §7. Core requirement for test questions

After each module, the test questions must be **code-verifiable** — not pure concept questions.

```
✅ Good test questions:
- "Open attempt.ts, find the line that starts the ReAct loop. What's it called?"
- "The minimal version's `messages = []` corresponds to which function call in the repo?"
- "Why is JSONL better than JSON for session storage? Give one scenario."

❌ Bad test questions:
- "Do you understand ReAct?" (too subjective)
- "Explain the role of pi-agent-core." (too broad)
```

See `exercises-template.md`.

---

## §8. The methodology's scope and what can't be compromised

**Scope**: all stage-3-walkthroughs/ teaching, content generation for stage-1-foundations/ and stage-2-architecture/, migration discussions in stage-4-applied/.

**Non-negotiable**: the methodology itself (the five steps of the Minimal Comparison Method, Checkpoint A/B, Feynman check, semantic-wave Unpack/Repack, three-layer progression, file:line spec) cannot be overridden by "user preference."

What user preference CAN override:
- Language (English / Chinese / bilingual)
- How many analogies
- Lesson length (45 vs 60 min)
- Whether to recap last lesson at the start of each one

But **cannot override**:
- "Concept Feynman check before going to code"
- "Show the minimal implementation before showing the repo code"
- "Code references must include file:line"
- "Don't start the lesson from entry.ts / index.ts"
