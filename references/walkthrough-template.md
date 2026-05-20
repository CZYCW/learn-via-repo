# Walkthrough Template (Standard Structure for stage-3-walkthroughs/)

> Every `stage-3-walkthroughs/{N}-{topic}.md` **must** strictly follow the §0-§8 nine-section structure of this template. This is the complete landing of the Minimal Comparison Method's five steps.
>
> Placeholders are tagged with `{...}`. **Examples are mostly from the AI agent domain (OpenClaw)** (the validated case). Cross-domain anchors live in `multi-domain-examples.md` §1. Any domain (web framework / database / OS / compiler / game engine / distributed system, etc) uses the same nine-section structure.
>
> For **full cross-domain walkthrough examples** (condensed, 5-15 lines per section, showing how the same nine-section template lands in different domains), see `walkthrough-examples-multi-domain.md`:
> - Example 1: web framework / Express middleware chain
> - Example 2: database internals / SQLite B-tree cursor
>
> When generating an actual walkthrough, match the tone, term density, and skeleton-element presentation of that file.

---

## Table of Contents

- **File naming** — `{NN}-{english-short-title}.md`
- **Standard file structure (9 sections)** — each walkthrough strictly follows this nine-section template
  - §0 General view (domain background) — external authoritative material + Repack to target repo
  - §1 What problem does this module solve — reverse argument + comparison of 3 common solutions + one-sentence positioning
  - §2 Core concepts — key glossary + general-concept-to-repo-implementation table
  - §3 Overall architecture — component diagram (mermaid) + ADR decisions (≤3)
  - §4 Minimal Comparison Method in action (5 steps) — core section
    - §4.0 High-level code map
    - §4.1 Step 1: authoritative minimal implementation (**reference + summary as two blocks**; no AI improvisation)
    - §4.2 Step 2: target repo's matching code
    - §4.3 Step 3: three-column comparison table (minimal / repo location / explanation)
    - §4.4 Step 4: industrial enhancement diff diagram
  - §5 Code navigation — in rounds (30 min each) + file:line
  - §6 Test questions — link to all three exercises/ files
  - §7 Implications for the user's target project — reusable / needs change / unique need (three blocks)
  - §8 Further reading — Tier 1/2/3
- **Per-section quality check** — self-check list after generating each piece
- **Anti-examples: what makes a walkthrough disqualified** — 6 common mistakes

---

## File naming

`stage-3-walkthroughs/{NN}-{english-short-title}.md`

- `NN` is a two-digit number (01, 02, ...)
- English short title, hyphenated
- Examples: `01-message-end-to-end.md`, `02-react-loop-and-subagents.md`, `03-session-and-memory.md`

---

## Standard file structure (9 sections)

````markdown
# {NN} {Topic title}

> {30-60 minutes} to read. After this you should be able to answer:
> 1. {Core question 1}
> 2. {Core question 2}
> 3. {Core question 3}

---

## §0. General view (domain background)

> {1-2 sentences introducing "how this problem is handled in this domain"}

**Academic / industry core insight**: {cite Tier 1 authoritative material + one sentence landing the core Why}

> Example (OpenClaw teaching ReAct):
> In 2022, Yao et al at Google/Princeton proved in the [ReAct paper](https://arxiv.org/abs/2210.03629):
> interleaving reasoning (CoT) with acting beats either alone.
> Pure CoT has 20% higher hallucination on HotpotQA than ReAct; pure action is 34% lower than ReAct on ALFWorld.

**Repack to target repo**: {one sentence on how this repo implements this insight}

**Minimal skeleton preview** (semantic-wave Repack anchor):
```python
# N-line minimal implementation, immediately readable
def {core_function}():
    ...
```

**Further reading**: see `resources/papers/{paper}.pdf` | `stage-1-foundations/{N}-{topic}.md`

---

## §1. What problem does this module solve

### §1.1 Reverse argument

If this module didn't exist, what would the {user / developer} have to do? {Paragraph describing the pain}

### §1.2 Comparison of 3 common industry solutions

| Solution | Characteristics | Representative |
|------|------|------|
| {Solution A} | {characteristics} | {representative system} |
| {Solution B} | {characteristics} | {representative system} |
| {Solution C} | {characteristics} | **{target repo}** |

### §1.3 One-sentence positioning

**{This module} is the {what kind of thing} for {doing what}.**

---

## §2. Core concepts

### §2.1 Key glossary

| Term | English | One-sentence definition |
|------|------|-----------|
| {term 1} | {Term 1} | {definition} |
| {term 2} | {Term 2} | {definition} |
| ... | ... | ... |

### §2.2 General-concept → target-repo implementation table

| General concept | Implementation in {repo} |
|---------|----------------|
| {general concept 1} | {repo implementation 1} |
| {general concept 2} | {repo implementation 2} |
| ... | ... |

---

## §3. Overall architecture

### §3.1 Component relationship diagram

```mermaid
flowchart TB
  ...
```

### §3.2 Key design decisions (ADR format, max 3)

#### ADR-1: {Decision title}

**Context**: {what constraints does this decision face}
**Decision**: {what was chosen}
**Consequence**:
- ✅ {positive 1}
- ✅ {positive 2}
- ❌ {negative 1} (mitigation: {how to mitigate})

#### ADR-2 / ADR-3 same structure

---

## §4. Minimal Comparison Method in action

### §4.0 High-level code map

Look at a map first:

```
{entry event}
    │
    ▼
{file1.ts:line1}      ← one-sentence responsibility
    │ (calls)
    ▼
{file2.ts:line2}      ← one-sentence responsibility
    │
    └── Focus on these lines here:
        - line {X}: {function}()  ← why key
        - line {Y}: {function}()  ← which step of the minimal version this maps to
        - line {Z}: {function}()  ← this is the core!
```

### §4.1 Step 1: authoritative minimal implementation (reference + summary as two blocks, V2 upgrade)

> **V2 important change**: the old version had the AI improvise 30-100 lines — deprecated. AI-improvised code looks right but doesn't run, and diverges from the authoritative implementation. The new version must **reference real, runnable, community-vetted code**. See `methodology.md` §4.1.

#### Block A: source reference (required)

```markdown
**Minimal implementation source**: {repo-owner}/{repo-name} ({star count} stars{, authority: xxx})
**File location**: `{path/to/file.{py,ts,go}}:{start_line}-{end_line}`
**Why this is the authoritative minimal implementation**: {1-2 sentences — usually "author is X big name / this repo is the official code for Y course / Z article"}
```

Source selection follows the **three-tier priority** (see `methodology.md` §4.1):

1. **The beginner repo from stage-0** (student has run it, modified it, knows it best)
2. **A domain-authoritative nano-* / mini-* / minimal-implementation repo** (user-vetted — AI doesn't unilaterally pick)
3. **AI-simplified version** (only if 1 and 2 are unavailable, **must** tag `"based on X, simplified, not independently verified to run"`)

#### Block B: 5-10 line pseudocode summary (required)

> **Not a runnable version** — just a "translation" of the skeleton, so the teacher can walk through the ReAct triplet / messages list / other core structures. If the student wants to run / modify / verify it, they go back to the real file in Block A.

```python
# Adapted from {repo}/{path}:{lines}, stripped of error handling / streaming / concurrency, kept the {core pattern} skeleton
def {core_function}():
    """{one-sentence responsibility}"""
    response = call_llm(messages, tools)
    if response.stop_reason == "tool_use":
        ...
```

#### Real example for Block A (the actual OpenClaw teaching scenario recommendation)

For the OpenClaw learning scenario, the stage-0 trio is recommended (**vetted by Phase 2C web search + user evaluation**, AI doesn't unilaterally pick):

```markdown
**Minimal implementation source (one of three)**:
  rohitg00/ai-engineering-from-scratch Phase 14 Lesson 01 (7.8k stars, "raw API first")
**File location**: `14-agent-engineering/lesson-01/agent.py:1-120`
**Why authoritative**: the author explicitly says "120 lines of pure Python, no dependencies"; later
  lessons introduce LangGraph, but Lesson 01 stays raw API. Student runs this file in stage-0, then comes back here.

**Minimal implementation source (two of three)**:
  pguso/ai-agents-from-scratch (3.5k stars, JS 14-lesson systematic tutorial)
**File location**: `examples/06-react-agent.js:1-95` (path indicative; actual path confirmed in stage-0)
**Why authoritative**: JS aligns with OpenClaw (TS); most systematic 14-lesson progression;
  example 06 is a complete ReAct implementation and can switch to OpenAI API.

**Minimal implementation source (three of three)**:
  Leonie Monigatti notebook (personal project but ML engineer background; Anthropic API)
**File location**: `iamleonie/website/blob/main/blog/ai-agent-from-scratch-in-python.ipynb` Section 4
**Why authoritative**: same Anthropic API family as OpenClaw; 4-component progression (LLM / memory / tool / agent loop)
  maps directly onto OpenClaw's LLM call + transcript + memory_tool + ReAct loop.
```

#### Anti-examples (V2 forbidden)

```
❌ §4.1 drops 80 lines of AI-improvised Python with no "source" field
   → student can't verify when it doesn't run

❌ Reference a repo without a precise file:line — just "similar to X's implementation"
   → student can't find the matching location

❌ AI declares a repo "authoritative minimal implementation" from memory, no Phase 2C search + user evaluation
   → Example: treating microsoft/ai-agents-for-beginners as qualified (it's actually based on Microsoft Agent Framework)
   → Example: treating anthropic-cookbook as the "main teaching line" (it's a cookbook, not a curriculum)

❌ Reference a beginner repo built on langchain / langgraph / llamaindex / crewai / smolagents
   → student learns framework APIs, not the skeleton
```

### §4.2 Step 2: target repo's matching code

```{language}
// {file}:{line}
// Corresponds to minimal version's: {which line / function in minimal}
{repo actual code snippet}

// {file}:{line}
// Corresponds to minimal version's: {which line / function in minimal}
{another snippet}
```

### §4.3 Step 3: three-column comparison table

| Minimal version | {repo} code location | Explanation |
|---------|---------------|------|
| `{minimal_var}` | `{function}()` in `{file}:{line}` | {what's added} |
| `{minimal_func}()` | `{class.method}()` in `{file}:{line}` | {what's added} |
| ... | ... | ... |

### §4.4 Step 4: industrial enhancement diff diagram

```
Minimal version ({N} lines)        {repo} enhanced ({M} lines)
─────────────────              ──────────────────────────
{minimal_func}        →    + {enhancement 1: error handling}
                                + {enhancement 2: timeout}
                                + {enhancement 3: concurrency lock}
{minimal_var}         →    + {enhancement 1: persistence}
                                + {enhancement 2: TTL cache}
─────────────────              ──────────────────────────
Core principle: the extras aren't "more concepts" — they're "doing the same thing more robustly"
```

Item-by-item explanation (1-2 sentences each):
1. **{enhancement 1}**: why industrial scale needs this ({specific reason})
2. **{enhancement 2}**: ...

---

## §5. Code navigation

### Round 1 (30 min): {specific goal, e.g., "trace one message into the ReAct loop"}

1. Open `{file}`, search for `{function_name}` (around line {N})
2. Focus on lines {X}-{Y}: {one-sentence what this block does}
3. Find line {Z}: `{key_function}()` — this is {which step of the minimal version}

### Round 2 (30 min): {specific goal}

1. ...
2. ...

### Round 3 (optional, 30 min): {specific goal}

...

---

## §6. Test questions

After this section, do the corresponding topic in each problem file:

- **Concept check**: see `exercises/concept-checks.md#{NN}-{english-short-title}`
- **Code finding**: see `exercises/code-finding.md#{NN}-{english-short-title}`
- **Transfer application**: see `exercises/transfer.md#{NN}-{english-short-title}`

After the walkthrough, the teacher verifies in this order:
1. Do the concept check first (Feynman-style; prerequisite for the next walkthrough)
2. Then the code-finding (verify the student can independently open files and find locations)
3. Last the transfer (exploratory, no standard answer)

---

## §7. Implications for the user's target project

### §7.1 Designs you can directly reuse

| {repo}'s design | How to use it in your project |
|--------------|-----------------|
| {design 1} | {how to apply} |
| {design 2} | {how to apply} |

### §7.2 Things that need to change

| {repo}'s design | Why it doesn't fit you | How to change |
|--------------|--------------|-------|
| {design 1} | {reason it doesn't fit} | {direction of change} |
| ... | ... | ... |

### §7.3 Your project's unique needs ({repo} doesn't address)

1. **{Need 1}** — {why the repo doesn't address it; how you should fill the gap}
2. **{Need 2}** — ...
3. **{Need 3}** — ...

---

## §8. Further reading

### Tier 1 (must read)

- [{paper / official doc title}]({URL}) — {one sentence why it's a must-read}

### Tier 2 (deep)

- [{high-quality blog title}]({URL}) — {one sentence}

### Tier 3 (reference)

- ...

### Related docs in this set

- `stage-2-architecture/{matching module}.md` — this module's design rationale (architecture layer)
- `stage-3-walkthroughs/{adjacent walkthrough}.md` — {adjacent code topic}
- `reference/code-map.md` — index of key file:line across the whole repo
````

---

## Per-section quality check

After generating a walkthrough, the author (the skill itself) self-checks:

**§0**:
- Did you bring in a Tier 1 authoritative material?
- Does the reader understand "this is the Why" within 30 seconds?
- Did you immediately Repack from external material to the target repo?

**§1**:
- Does §1.1 use a reverse argument to spark curiosity, not jump straight to a definition?
- Does §1.2 list at least 3 industry solutions for comparison?
- Does §1.3 position the module in one sentence?

**§2**:
- Is every glossary entry one sentence?
- Is the general-concept → repo-implementation table clear?

**§3**:
- Is there a mermaid architecture diagram?
- Are there ≤3 ADRs? Each with full three sections (Context / Decision / Consequence)?
- Does Consequence include both ✅ and ❌?

**§4**:
- Does §4.0 code map have 3-5 core file:line entries?
- Is §4.1's minimal implementation 30-100 lines? Skeleton only, no details?
- Does §4.2 have "corresponds to minimal version's what" comments on every repo code block?
- Is §4.3's comparison table strictly three columns?
- Does §4.4 use a diff diagram, not a table? Does each enhancement have a "why"?

**§5**:
- At least 2 rounds?
- Each round has a clear goal + time estimate + file:line?

**§6**:
- Links to the corresponding section in all three exercises/ files?

**§7**:
- Includes all three blocks ("reusable / needs change / unique need")?
- If user didn't provide a PRD, does §7 fall back to "suppose you build {reasonable example project}"?

**§8**:
- Has Tier 1/2/3? Each entry has a "why read"?

---

## Anti-examples: what makes a walkthrough disqualified

```
❌ No §0 general view; jumps straight into §1 business problem
   Consequence: student doesn't know where this repo's approach sits in the industry

❌ §4.1 minimal implementation is 200 lines of async/await/error-handling industrial code
   Consequence: loses the point of "minimal comparison"; student can't see the skeleton

❌ §4.2 shows repo code without file:line
   Consequence: student can't go back to the repo to verify

❌ §4.4 writes the industrial enhancements as a table with one word per row
   Consequence: student doesn't understand "why" industrial scale needs them

❌ §5 code navigation says "go look at attempt.ts's core loop yourself"
   Consequence: violates code taboos — must give exact line numbers

❌ §7 written as "implications for AI agent developers" or other generic phrasing
   Consequence: loses the targeting on "the user's project"
```
