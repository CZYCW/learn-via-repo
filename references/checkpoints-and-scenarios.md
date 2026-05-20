# Checkpoint A/B and Teaching Scenario Templates

> The real-time playbook during teaching. `methodology.md` defines "how it should be taught"; this doc defines "how to operate in a specific situation."

---

## Table of Contents

- **§1. Checkpoint A: concept understanding check** — must pass before going to code; "explain in one sentence, no jargon"
- **§2. Checkpoint B: code skeleton check** — must pass before showing the minimal implementation; the student grep's to a file:line independently
- **§3. Scenarios A-C: standard teaching templates**
  - §3.1 Scenario A: teaching a new module (student's first contact) — standard 6-stage rhythm
  - §3.2 Scenario B: answering questions (student has a specific question) — 4-step flow
  - §3.3 Scenario C: code walkthrough (student opens code and follows along) — 4-step flow
- **§4. Scenario D: unblocking strategies (student is stuck)**
  - §4.1 When Checkpoint A fails — reverse argument / switch example / find prerequisite concept / fall back to design docs
  - §4.2 When Checkpoint B fails — demo navigation / give precise keyword / hand-hold then independent / simplify the target
- **§5. Scenario E: 60-minute single-file deep read template** — set expectations / teach by functional block / industrial enhancements / verify
- **§5b. Scenario F: companion pacing during stage-0 hands-on** — added in V2, multi-session companion + graduation-check gate (cross-domain version)
- **§6. Common closing: standard actions at the end of every lesson** — update progress.md / preview next / log open questions

---

## §1. Checkpoint A: concept understanding check

### When it fires

In the lesson rhythm, **at the end of the 5-20 minute segment, before entering the code layer (after the 20-minute mark)**.

```
0-5    Panoramic question
5-20   Teach concepts and architecture (Layer 1 + 2)
        ↓
        ★ Checkpoint A (mandatory)
        ↓
20-40  Minimal Comparison Method (Layer 3)
```

### Standard operation

Teacher asks:
> "In one sentence, **without any jargon**, tell me what problem this {core concept} solves."

Branch based on the student's answer:

**Result A: said it clearly**
- Immediately Repack: "Good — now say it again using {term 1}, {term 2}, {term 3}"
- Student can Repack → pass, move to the next section
- Student can't Repack → concept not fully internalized; give another example, guide the Repack

**Result B: didn't say it clearly (or mixed jargon into the answer)**
- **Absolutely don't skip** ahead to the code — every line of code after would be floating
- Trigger "Scenario D-A: unblocking strategy when concept understanding fails" (see §4)

### Pass criteria (refined)

- One sentence ≤ 25 words
- No jargon (including acronyms like ReAct / RAG / LLM)
- Must describe both "pain point + solution"
- Not a tautology like "X is for doing Y"

---

## §2. Checkpoint B: code skeleton check

### When it fires

In the lesson rhythm, **after the code map (Step 0) is done, before showing the minimal implementation (Step 1)**.

```
20-40  Minimal Comparison Method
   §4.0 High-level code map
        ↓
        ★ Checkpoint B (mandatory)
        ↓
   §4.1 Minimal implementation
   §4.2 Repo's matching code
   §4.3 Comparison table
   §4.4 Industrial enhancements
```

### Standard operation

Teacher says:
> "Open `{file}`, search for `{key_function}` — can you find it? Tell me roughly which line it's around."

The student actually does it in their editor / CLI. Branch based on result:

**Result A: found it**
- Have them say in one sentence "roughly what this function is doing" (looking at the signature + 1-2 lines around it)
- Pass, move to the minimal implementation

**Result B: can't find it, or found the wrong place**
- Trigger "Scenario D-B: unblocking strategy when code skeleton check fails" (see §4)

### Pass criteria (refined)

- Can open the file independently
- Can use grep / IDE search to find the target line
- Can give the exact line number (within ±5 lines)
- Doesn't rely on the teacher saying "let me find it for you"

---

## §3. Scenarios A-C: standard teaching templates

### §3.1 Scenario A: teaching a new module (student's first contact)

Use case: every time you open a new walkthrough.

```
0-3 min: Problem scenario
  → "If {this module} didn't exist, what would the developer have to do by hand?"
  → Make the student feel the pain

3-13 min: Minimal version
  → Show 20-50 lines of minimal implementation
  → Explain the skeleton line by line (not industrial code!)
  → Repack using §0's external material: this minimal version corresponds to the domain's {core concept}

  ★ Checkpoint A (5 min)

13-23 min: The repo's implementation
  → Three-column comparison table (minimal / repo location / explanation)
  → Use comments to mark "this corresponds to which line of the minimal version"
  → Every file:line is precise

  ★ Checkpoint B (5 min)

23-28 min: Industrial enhancements
  → Diff diagram: repo has N more lines than minimal; where do they go?
  → For each extra line, explain "why industrial scale needs it"
  → Emphasize: "Not more concepts — more robust."

28-38 min: Code navigation
  → In rounds; each round one specific goal + file:line
  → Student opens the actual code and follows

38-43 min: Test
  → Do 3 questions from exercises/code-finding.md#{topic}
  → Getting 1 wrong is fine; 2-3 wrong → go back to the relevant section and re-teach
```

### §3.2 Scenario B: answering questions (student has a specific question)

Use case: the student is self-studying stage-1/2 or reading code independently, and hits a specific question.

```
1. Pin down the boundary of the question (1 min)
   → "Where are you stuck? Concept? Architecture? Or specific code?"
   → Concept question → go to the concept layer (don't paste code yet)
   → Architecture question → architecture diagram + ADR
   → Code question → give file:line directly

2. Explain with the minimal version first (3 min)
   → Reduce the question to the smallest example
   → Don't reach for the repo's complex version straight away

3. Then map to the repo (3 min)
   → Give file:line, point at the code that answers the question
   → Explain "what industrial scale adds here"

4. Verify understanding (2 min)
   → "Now can you find where {specific feature} lives in the repo by yourself?"
   → Student opens it and finds it independently = question answered
```

### §3.3 Scenario C: code walkthrough (student opens code, follows along)

Use case: the student has read the stage-2 design doc for the module and is now following the teacher through the code section of the stage-3 walkthrough.

```
1. Set expectations first (2 min)
   → "The core responsibility of this function/file is X; it corresponds to the minimal version's Y"
   → "Today we'll only look at the most critical M of these N lines (not all N)"
   → "After this, you should be able to say: this file does these 3 things"

2. Teach by functional block (5-15 lines per block)
   → Don't go line by line! Group by "what does this block do"
   → At the start of each block: "What's this block doing? Take a minute to guess"
   → Student guesses, then teacher fills in 1-2 key lines of explanation, skips the rest
   → At the end of each block: "Which step of the minimal version does this map to?" — student says it

3. Highlight key lines
   → "Line N is the key one — it corresponds to the minimal version's Z"
   → ≤5 key lines per file

4. Explain industrial details
   → "There's extra error handling / timeout / lock here because..."
   → Every extra line has a "why" — if there isn't one, skip it
```

---

## §4. Scenario D: unblocking strategies (student is stuck)

### §4.1 When Checkpoint A fails (student can't explain the concept in their own words)

**Symptoms**: student says "I get it" but can't articulate what; or mixes jargon into the explanation; or answers a different question.

**Strategy** (try in order, 5 min max per step):

#### Step 1: switch to a "reverse argument" angle

Ask: "If {this concept} didn't exist, what's the worst thing that would happen?"

**Why this works**: it shifts the student from "what is it" to "why do we need it" — usually easier to trigger understanding. "What is it" is a definition question; "why" is a motivation question; motivation questions surface real understanding.

#### Step 2: give a smaller concrete example

Don't switch concept, switch example. Shrink the example to the smallest understandable unit, and **use a domain the student already knows**:

```
Original example (student stuck):
  "ReAct is a Reasoning + Acting loop"

Fall back to a domain the student knows:
  "When you're writing code and hit an API you don't know, what do you do?
   You guess how to use it (reasoning) → run it and see the error (action) →
   look at the error and guess again (reasoning) → run again (action). Until
   it works. That's ReAct — looking things up while writing code, not reading
   everything before you start, and not writing blindly."

Immediately Repack:
  "This 'look-it-up-while-writing' loop is called ReAct in the literature."
```

#### Step 3: find the prerequisite concept behind the blind spot

The reason they're stuck might not be that this concept is hard — it might be that a prerequisite concept never landed.

Ask: "Can you explain {prerequisite concept}?"
- Yes → the blind spot is in the new concept itself; go back to steps 1-2
- No → back up, land the prerequisite first

#### Step 4: last resort — fall back to the design doc

"Let's go back to `stage-2-architecture/{matching doc}.md` §1-§2; read it out loud to me."

Have the student **read it themselves**, asking questions as they go — active reading is 3x more efficient than passive listening.

#### General principle

- Spend at most 20 minutes stuck at Checkpoint A
- Over 20 minutes → say "Let's set this aside, look at the code, come back to this concept later" — that's a legitimate exit, not failure
- Getting stuck is normal, not shameful

### §4.2 When Checkpoint B fails (student can't find the code entry)

**Symptoms**: student opens the file and doesn't know where to look; searched for the wrong keyword; scrolled for 10 minutes still wandering between import statements.

**Strategy** (try in order):

#### Step 1: don't teach content, demo "how to navigate"

Open the file; use grep / IDE search to find the entry:

```
"In attempt.ts, search for runEmbeddedAttempt. See it?"
```

**Goal**: learn the tool, not understand the content — finding it matters more than understanding it.

#### Step 2: give a more precise search keyword

```
Wrong:
  "Go find where the ReAct loop is." (too abstract)

Right:
  "Search for activeSession.prompt — that's the line that triggers the ReAct loop."
```

One keyword at a time; don't give multiple targets at once.

#### Step 3: hand-hold once, independent next time

```
"Let me show you: line 1627, can you see it? Good — now close it and find it yourself."
```

**Verification criterion**: the student can repeat the action independently, not that the teacher gave the answer.

#### Step 4: simplify the navigation target

If the whole file is too complex, shrink the target:

```
"Forget the rest — just find this one line: attempt.ts:991. Can you find it?"
```

Finding one line = passing Checkpoint B.

#### General principle

- Most Checkpoint B failures are "file too big + no map"
- Give precise line numbers, not "roughly somewhere in the middle"
- If they still can't find it after repeated precise line numbers, the tool isn't familiar — teach the tool first (IDE jumps, grep)

---

## §5. Scenario E: 60-minute single-file deep read template

Use case: the student has passed Checkpoint B and is ready to deeply read a core file (e.g., OpenClaw's `attempt.ts`, vLLM's `core/scheduler.py`).

### 0-10 min: set expectations

```
"The core responsibility of this file is X; it corresponds to the minimal version's Y."
"Today we'll only look at the most critical M of the N total lines (not all N)."
"After this, you should be able to say: this file does these 3 things."
```

**Why these 10 minutes determine the efficiency of the next 50**: the student knows the endpoint, so they won't get lost in the middle.

### 10-40 min: teach by functional block (5-15 lines each, 4-6 blocks)

For each block:

1. Tell the student the line range: `lines 754-796`
2. Ask: "What's this block doing?" (give 1 min for them to guess)
3. Explain the key 1-2 lines, skip the rest: "Line 756 is the key one; the rest is parameter config"
4. Ask: "Which step of the minimal version does this map to?" (student says it, not the teacher)

**Key principle**:

> Don't go line by line! Line-by-line is information transfer, not understanding.
> The student saying "this block does X" is 10x more effective than the teacher saying "line i does a, line i+1 does b."

### 40-55 min: industrial enhancements explanation

```
"Our minimal version needs 5 lines here; the repo uses 50. The extras are:"
```

List the enhancements (max 5), each 1-2 sentences:

- Concurrency lock: prevents two messages writing at the same time
- Event subscription: streams tokens to the user interface
- Tool filtering: handles format differences between LLM providers
- Sandbox config: working-directory isolation
- System prompt reporting: observability for debugging

**Key phrasing**: "Each one is 'same thing, just sturdier' — not a new concept."

### 55-60 min: verify

Give 3 precise test questions:

1. **file:line location**: "Find the line that triggers the ReAct loop." (Expected: `attempt.ts:1627`)
2. **Concept mapping**: "What does the minimal version's `messages=[]` become in this file?" (Expected: `SessionManager.open`, line 991)
3. **Enhancement understanding**: "Why does this code need a file lock when the minimal version doesn't?" (Expected: concurrent scenario, multiple messages writing simultaneously)

**Pass criteria**:
- All 3 correct → this file's deep read is done
- One wrong → go back to the relevant functional block and re-teach (max 10 min)

---

## §5b. Scenario F: companion pacing during stage-0 hands-on (added in V2)

Use case: Phase 2.5 has assessed the student as A/B/C/D-level; they've cloned the stage-0 recommended repo and are getting hands-on.

The teacher's role in stage-0 is **different from stage-1/2/3** — it's not "teacher explains, student listens"; it's "student runs code, teacher answers questions + verifies." Principle: **let the student get stuck and struggle a bit first, then answer** — hands-on failure is part of learning.

### Stage-0 overall pacing (multiple sessions, total 3-15 hours)

```
Opening (1 session, 30 min): set expectations
  1. Walk the student through stage-0-fundamentals/README.md
  2. Confirm the recommended repo (if multiple) → have the student pick a main line
  3. Explain why stage-0 matters (hands-on = muscle memory = openclaw won't feel abstract)
  4. Walk through prerequisites.md → set up the environment together (config the LLM inference style the student picked)
  5. Have the student run hello-world (smallest runnable example) — first session ends

Companion sessions (as-needed, 20-45 min each): student gets stuck, finds teacher
  - Student works through chapter N independently
  - Stuck for over 15 minutes with no resolution → find the teacher
  - Teacher follows "Scenario B answer-questions" 4-step flow

Checkpoint (every 3-4 chapters / every core milestone):
  Teacher proactively reaches out, verifies against graduation-check.md

Graduation check (after stage-0 is done):
  Go through graduation-check.md item by item. All pass → move to stage-1
```

### Key teacher actions during stage-0

| Action | When | How |
|------|------|-------|
| **Don't proactively explain concepts** | During stage-0 | Concepts are taught in stage-1. In stage-0, the student feels through their hands |
| **Use 5W for Q&A** | When student is stuck | "What command did you run?" "What did you expect?" "What did you actually see?" "Did the previous step work?" "Did you change the environment?" |
| **Don't give the answer directly** | When student is stuck | Guide them to read the error, check the README, solve it themselves. Failure + self-rescue = real understanding. **Stuck max 20 min before giving the answer directly** |
| **Force a system prompt change** | After they finish the core ReAct chapter | "Now don't just follow the repo — change the system prompt to make the agent behave differently" — proves they get it |
| **Force adding a new tool** | After the tool-use chapter | "The repo has calculator and search — add a 'get_weather' tool yourself" — proves they can extend |
| **Run graduation-check.md item by item** | Before stage-0 ends | No pass, no stage-1 |

### Stage-0 → stage-1 transition check (graduation criteria)

**Universal template (domain-agnostic)** — graduation-check.md should include 5 questions:

1. **Basic understanding**: without referencing the README, can you explain the stage-0 repo's **core control flow**? (≤1 sentence, no jargon)
2. **Code location**: in `{stage-0-repo}/{file}`, find where the domain's **key skeleton element** is implemented (concrete skeleton elements: see `multi-domain-examples.md` §1).
3. **Can modify but not yet build**: change the repo's **key config / behavior parameter** from X to Y, and describe the behavior difference. (Must be describable.)
4. **Can extend**: add a **new functional unit** (specific feature varies by domain) on top of the stage-0 repo, run it, commit the modified code.
5. **Can ask the right question**: in one sentence, "if you wanted to add `{stage-1 core concept}` to this repo, how would you change `{skeleton element}`?" (**This question is the hook into stage-1**.)

**Domain-specific examples**:

| Domain | Q1 (core control flow) | Q2 (skeleton element location) | Q3 (modify) | Q4 (extend) | Q5 (stage-1 hook) |
|------|------|------|------|------|------|
| AI agent | "In one sentence, without 'agent/tool', explain what loop the repo is running" | Find where the ReAct triplet is implemented | Change system prompt, observe behavior diff | Add a new tool | "How would you add memory to this agent (without a built-in memory tool)?" |
| Web framework | "In one sentence, without 'middleware', explain how a request goes from browser to handler" | Find where `next()` is called in the chain | Change route priorities | Add a new middleware | "How would you add session support (without a built-in)?" |
| Database internals | "In one sentence, without 'cursor/page', explain how a SELECT finds its data" | Find where cursor operations live | Change page size, observe performance diff | Add a new opcode | "How would you add indexing (without a built-in index module)?" |
| Compilers | "In one sentence, without 'token/AST', explain how source becomes something runnable" | Find the tokenizer entry | Add a new keyword | Add a new optimization pass | "How would you add debug info (without built-in debug info)?" |
| OS kernels | "In one sentence, without 'register', explain how the OS runs multiple programs at once" | Find the context switch | Change the scheduling algorithm | Add a new syscall | "How would you add virtual memory (without a built-in MMU)?" |

All 5 pass → stage-1. Any one fails → go back to the corresponding chapter and redo.

**Key principle**: the **structure** of the 5 questions (understand / locate / modify / extend / hook question) is cross-domain consistent; the **content** is customized per domain.

### Common teacher mistakes during stage-0 (taboos, cross-domain)

```
❌ Teaching the domain's core theory / papers during stage-0
   (AI agent: explaining the ReAct paper; web: explaining RFC 7231; DB: explaining ACID formalism)
   Consequence: student gets stuffed with concepts before feeling anything → enters stage-1 cognitively overloaded

❌ Giving the answer after the student has been stuck for 5 minutes
   Consequence: student didn't go through "struggle → self-rescue" → no muscle memory built → target repo still feels abstract

❌ Letting the student run through every chapter of the repo before verifying
   Consequence: misses the concept blind spots along the way → graduation check is full of "I don't know"

❌ Skipping graduation-check and going straight to stage-1
   Consequence: student didn't go through "hands-on feel → describe with the term" → Checkpoint A in stage-1 will fail
```

### Stage-0 → stage-3 connection

The code learned in stage-0 will be the **preferred** reference in stage-3 §4.1, used repeatedly. In stage-3, the teacher should actively connect the dots:

> "Remember the `act()` recursion in `{repo}/{file}:{line}` you ran in stage-0? OpenClaw's `attempt.ts:1627` triggers the same thing — just wrapped inside the pi-agent-core library."

The student hears "remember the one you ran..." and immediately gets an experiential anchor — cognitive load drops by half. That's the biggest payoff of investing time in stage-0.

---

## §6. Common closing: standard actions at the end of every lesson

Regardless of Scenario A/B/C/E, at the end of every lesson:

1. **Update `meta/progress.md`**
   - Mark what was learned today
   - Record where the student got stuck, what they internalized
   - Write down the next starting point

2. **Preview the next lesson**
   - "Next time we'll look at {next walkthrough}; the prep material is `stage-2-architecture/{matching doc}.md`"
   - Give the student an explicit "assignment" (what to read, what to think about)

3. **If there are unresolved questions**
   - Don't pretend they're resolved
   - Write them to the "open questions" list in `meta/progress.md`
   - Review for 1 minute at the start of next lesson
