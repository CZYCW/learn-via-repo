# Forbidden List (Things Never Allowed)

> Teaching red lines. When generating artifacts or actually teaching, **never cross** this list. Every item came from a real failure.

---

## §1. Concept taboos

### ❌ Show the repo's complex code without first showing a minimal implementation

**Why forbidden**: the student can't see the skeleton, just a pile of type signatures / error handling / concurrency locks — they'll think "complex = hard, I can't learn this."

**Right move**: write 30-100 lines of minimal version first, let the student see the skeleton; then show the repo's industrial version; finally explain "the extras make it more robust, not more concepts."

---

### ❌ Describe a concept for more than 3 sentences without giving matching code or an example

**Why forbidden**: abstract concept + no anchor = the student memorizes but doesn't understand.

**Right move**: every concept: one-sentence definition + one concrete example (Unpack) + one summary back to the term (Repack).

---

### ❌ Say "the code is complex but don't worry about the details"

**Why forbidden**: that phrase admits "I can't make this complexity clear" — a cover for teaching failure.

**Right move**: you must provide enough "skeleton" to make the complexity reasonable. If it really is complex, use the five steps of the Minimal Comparison Method to break it apart. If you still can't explain it, that means you don't fully understand it yourself — go figure it out and come back.

---

## §2. Code taboos

### ❌ Show code without a file:line reference

**Why forbidden**: the student can't go back to the repo to verify. Every code reference must be precisely locatable.

**Right move**: every repo code block must have a `// {file}:{line}` comment, or `attempt.ts:1627` style inline reference in prose.

---

### ❌ Show more than 50 lines of code without marking the key lines

**Why forbidden**: the student doesn't know what to focus on. 50 lines unmarked = 50 lines of noise.

**Right move**: long code blocks must mark 3-5 key lines with `// Key line:` or `// Corresponds to the minimal version's:` comments. The rest can be skipped.

---

### ❌ Skip the "industrial enhancements" explanation

**Why forbidden**: the student will feel the repo's code is mysterious, complex, something they couldn't write themselves. Loss of confidence.

**Right move**: every time you show repo code that's more complex than the minimal version, immediately explain why the extras exist (concurrency / error handling / performance / type safety etc). **Every extra line has a "why."**

---

### ❌ Start teaching from `entry.ts` or `index.ts`

**Why forbidden**: initialization code is the noisiest place — a pile of module imports, config loading, dependency injection — none of which is about "what this repo does." Starting here makes students get lost.

**Right move**: start from "one message's path." Find the user-input entry point (HTTP handler, CLI command), follow the data flow.

---

## §3. Pacing taboos

### ❌ Go more than 20 minutes without a check

**Why forbidden**: cognitive load peaks around 20 minutes. Without a check, the student is just passively receiving information.

**Right move**: a checkpoint every 15-20 minutes. Either a Feynman check, or a file:line location task, or "you summarize that block back to me."

---

### ❌ Move on when the student says "got it"

**Why forbidden**: "got it" is a social response, not evidence of understanding. Students fake understanding to not disappoint the teacher.

**Right move**: always use the Feynman check — "in one sentence, no jargon, tell me what problem that thing solves." Can't say it = doesn't get it.

---

### ❌ Teach more than 3 core concepts in one session

**Why forbidden**: cognitive-load theory (Sweller) proves working memory holds at most 4±1 chunks. Above 3 = overload.

**Right move**: at most 3 core concepts per lesson. When a 4th appears, either cut it or split it into the next lesson.

---

### ❌ Stop at the concrete example without returning to the technical term (semantic wave down only)

**Why forbidden**: the student understands the concrete example but can't transfer it. They took the elevator down to "concrete example" but never came back up to "technical term."

**Right move**: after every concrete example, immediately Repack — "now describe that example using {term 1} {term 2}."

---

### ❌ Skip the "high-level code map" and go straight to the minimal implementation

**Why forbidden**: map before skeleton. The student doesn't know where this code lives in the repo or how it connects to the surroundings — the minimal implementation feels isolated.

**Right move**: do Step 0 (code map: file:line call chain across 3-5 core files) first, then Step 1 (minimal implementation).

---

### ❌ Teach a concept without bringing in external high-quality material

**Why forbidden**: home-grown explanations often miss the mark — they skip the core insight a paper or authoritative blog has already nailed in one sentence.

**Right move**: for each core concept, actively search for 1 Tier 1 authoritative material (paper / big-company engineering blog / domain authoritative survey), cite its key data or figure, immediately Repack to the target repo.

---

## §4. Style taboos

### ❌ Use vague phrasing like "simply put" or "basically"

**Why forbidden**: those phrases are covers for "I didn't think this through clearly." When students hear them, their trust drops automatically.

**Right move**: use precise phrasing. If you can't think of precise phrasing, you don't have the idea clearly yet — go think, come back.

---

### ❌ Say "you can go look at the code yourself"

**Why forbidden**: that's "I'm done teaching, you figure it out." If the student could go look themselves, they wouldn't have come to you.

**Right move**: must give a concrete file:line and reading steps (in rounds, each round one goal + time estimate).

---

### ❌ Claim "the repo implements concept X" without a comparison table

**Why forbidden**: no comparison table = the student can't verify what you said is true.

**Right move**: every "the repo implements X" claim must come with a three-column comparison table (general concept / repo code location / explanation).

---

## §5. Beginner repo selection taboos (added in V2)

The beginner repos for `stage-0-fundamentals/` have specific hard constraints. Phase 2C search + user evaluation must enforce them strictly.

### ❌ Recommend mature framework abstractions that hide the domain's core control flow

**Abstract principle** (cross-domain): any mature framework that wraps the domain's **core control flow** behind "a few lines of API calls" is unsuitable. The student learns framework APIs, not first-principles.

**Judgment method** (cross-domain): open the repo's README example code. Can you see the **domain's skeleton elements**?

Each domain's skeleton elements are different — see `multi-domain-examples.md` §1 "key skeleton elements" column:

- **AI agents**: `messages.append({role, content})` + `if stop_reason == "tool_use": execute_tool(...)` + ReAct triplet
- **Web frameworks**: `next(err)` chain + `req` / `res` object passing + middleware signatures
- **Database internals**: B-tree cursor ops + opcode dispatch loop + row/page IO
- **Compilers / interpreters**: TokenScanner + ASTNode construction + Visitor pattern
- **OS kernels**: trap frame save + scheduler queue + page table switch
- **Game engines**: game loop tick + ECS component queries + render queue
- **Distributed systems**: log entry append + AppendEntries RPC + commit index advance

**Visible = qualified**; **invisible** (replaced by a single API call like `agent.run()` / `Agent(...).execute(...)` / `framework.handle(req)` / `engine.query(sql)`) = disqualified.

**Known disqualifying framework list (per domain, non-exhaustive)** — when you hit a new framework, apply the "judgment method" above:

#### AI agent domain
- LangChain family: `langchain` / `langchain_core` / `langchain_anthropic` / `langchain_openai`
- LangGraph: `langgraph`
- LlamaIndex: `llamaindex` / `llama_index`
- CrewAI: `crewai`
- AutoGen: `autogen` / `autogen_agentchat` / `autogen_core`
- Microsoft: `semantic_kernel` / `microsoft-agent-framework` / `azure-ai-foundry-agent`
- OpenAI: `agents` (OpenAI Agents SDK) / `openai-agents`
- HuggingFace: `smolagents`
- Haystack: `haystack`

#### Web framework domain (these frameworks aren't bad — they're just not what you learn the skeleton from in stage-0)
- Backend: `nestjs` / `hapi` / `adonisjs` / `spring` / `spring-boot` / `django` (high-level framework) / `rails` / `laravel`
- Frontend: `react` (to learn component principles → use mini-react) / `vue` (to learn reactivity → use mini-vue) / `angular` (highly abstract)
- Fullstack: `next.js` / `nuxt.js` / `remix` (routing + SSR all wrapped)

#### Database domain
- ORM family: `sqlalchemy` / `typeorm` / `prisma` / `hibernate` / `gorm` / `activerecord`
- High-level query wrappers: `mongoose` / `sequelize`
- Note: to learn database **internals** → beginner repo can't be an ORM; to learn ORM design → beginner repo can't be built on an existing ORM

#### Compiler / interpreter domain
- `babel` (highly wrapped modern version, bad for learning compiler principles) / `swc`
- TypeScript compiler (black box) / `tsc`
- LLVM high-level binding (like `inkwell`) — the LLVM C++ core is learnable, but the binding treats it as a black box

#### OS kernel domain
- `docker` / `k8s` (not an OS kernel — a high-level scheduling framework)
- `systemd` (init framework, not a kernel)
- Container runtimes like `runc` (built on the kernel, not the kernel itself)

#### Game engine domain
- `unity` / `unreal-engine` / `godot` (engine is a black box — you can't see the game loop / ECS / render pipeline)
- `phaser` / `pixi.js` (frontend game frameworks that wrap rendering)

#### Distributed systems domain
- `k8s controller-runtime` (wraps the reconcile loop)
- `spring-cloud` / `consul-template`
- Service mesh clients (like `istio-client`)

**Why forbidden**: see the "judgment method" above — these framework abstractions hide the domain's core control flow. The student learns framework APIs, not domain principles, and stage-3's deep reads of complex industrial code still feel abstract.

**Exception**: if the student is **already familiar** with the framework, and **the target repo is the framework itself** (e.g., learning LangChain → target repo is langchain), then stage-0 should pick **a simplified implementation of one of the framework's internal modules**, not an application built on the framework.

### ❌ AI declares a repo "qualified" from memory

Wrong examples (actually happened during the v2 upgrade):
- Treating `microsoft/ai-agents-for-beginners` as qualified (it's actually based on Microsoft Agent Framework + Azure AI Foundry)
- Treating `anthropic-cookbook` as the stage-0 main teaching line (it's a cookbook, not a curriculum)

**Right move**: Phase 2C uses WebSearch to find candidates → WebFetch verifies the README has no framework imports → 3-5 candidates handed **to the user** for evaluation → only after user confirmation, write into `stage-0-fundamentals/recommended-repos.md`. **The AI doesn't unilaterally pick.**

### ❌ Treat "authoritative producer" as automatically meaning "good for teaching"

Authority (star count, big-company backing) ≠ "good for teaching." The hard criteria for teaching are:
- Progressive structure (teach A then B)
- Concept setup (a paragraph of setup before each new concept)
- Minimal comparison (skeleton first, then complexity)

Counter-example: anthropic-cookbook (43.1k stars + official from Anthropic) is a **cookbook**, not a **curriculum** — 14 independent notebooks with no progression, each notebook drops the complete version with no setup. **As a Tier 1 reference it's perfect; as the stage-0 main teaching line it's disqualified.**

Applicable judgment:
- ✅ Teaching-type stage-0: progressive curriculum / step-by-step tutorial / companion blog or video
- ❌ Non-teaching type (goes into reference/): cookbook / quickstart / production demo

---

## §5b. Meta-lessons (3 summarized during the V2 upgrade)

These came from real mistakes during the v2 upgrade. The AI must internalize them to avoid repeats.

### Meta-lesson 1: LLM provider type is not an exclusion criterion

Mistake: treating "must be cloud API (OpenAI/Anthropic), don't accept local LLM (Ollama/GGUF)" as a hard constraint.

Why wrong: from "understanding agent principles" perspective, `ollama.chat()` and `openai.chat.completions.create()` have **the exact same skeleton** — both are "send a prompt, receive a response." What the student is learning is the agent-loop skeleton, not the LLM provider. Installing Ollama takes 5-10 minutes.

Right move: demote LLM provider from hard constraint to **a Phase 1 preference question**:
- "Would you like to install Ollama + download a GGUF model, or would you rather use an API key and run immediately?"
- Both paths teach agent principles; let the student pick

Strong candidates that were wrongly excluded and should be upgraded:
- rasbt/mini-coding-agent (850 stars + Sebastian Raschka big name + local Ollama)
- pguso/agents-from-scratch (Python, 703 stars + local GGUF)

### Meta-lesson 2: cookbook ≠ curriculum

Mistake: treating "authoritative producer + high star + relevant content" as equivalent to "good as the stage-0 main teaching line."

Why wrong: anthropic-cookbook (43.1k stars) is 14 **independent** notebooks, each solving a specific problem, with **no progressive structure**, **no concept setup**, **no minimal comparison**. The student enters and gets lost: "Which one do I look at first?"

Right move: clearly distinguish two types of doc:
- **Teaching-type** (curriculum / step-by-step) → stage-0/1/2/3 main line
- **Reference-type** (cookbook / quickstart / demo) → reference/ + stage-3 §4.1 reference source + resources/ Tier 1

Judgment: open the README and ask "did the author say 'first look at lesson 1, then lesson 2'?"

### Meta-lesson 3: the AI cannot unilaterally pick repos

Mistake: the AI declares "X repo is a qualified authoritative minimal implementation" based on training-data impressions.

Why wrong: training data may be stale; the AI may not have actually read the repo's README; a repo may have switched from framework-free to framework-based and the AI doesn't know.

Real case:
- Early in the v2 upgrade, the AI wrote "for example microsoft/ai-agents-for-beginners" in methodology.md as a qualified sample → user corrected: it's based on Semantic Kernel / AutoGen, not qualified.

Right move: Phase 2C must **actually execute**:
1. WebSearch for 5-10 candidates
2. WebFetch each candidate's README, verify the import list
3. Hand candidates + evaluation table to the user
4. After user evaluation, confirmation, or rejection — only then write into `stage-0-fundamentals/`

`SKILL.md` Phase 2C must make this interaction step explicit — cannot skip it.

---

## §6. Meta-taboos (taboos about taboos)

### ❌ Use "user preference" to bypass the forbidden list

**Why forbidden**: the forbidden list is the methodology's hard constraint, not a style preference.

The student can say "I prefer Chinese / English," "I prefer shorter lessons," "I don't want analogies" — those are style preferences, fine.

The student **cannot** say "I already get it, skip Checkpoint A" — that's using social pressure to make the teacher lower the bar, leading to teaching failure. The teacher must enforce the checkpoint.

---

### ❌ Use "this case is special" to grant exceptions

**Why forbidden**: every case is "special" — the forbidden list becomes decoration.

If you really need to make an exception, explicitly record it in `meta/progress.md`, and mark "the cost of the exception" — review at next lesson to confirm whether the exception was reasonable.

---

## §7. Self-check list

After every walkthrough generated or every lesson taught, check yourself against this list:

- [ ] Didn't show repo code without first showing a minimal implementation
- [ ] Every concept has a one-sentence definition + concrete example + term Repack
- [ ] Every code reference has file:line
- [ ] Long code blocks have ≤5 key-line annotations
- [ ] Every repo code section has an "industrial-enhancements why" explanation
- [ ] Didn't start from entry.ts / index.ts
- [ ] A checkpoint every ≤20 minutes during the lesson
- [ ] When the student says "got it," did a Feynman check
- [ ] ≤3 core concepts per lesson
- [ ] Every concrete example did a term Repack
- [ ] Showed the code map (Step 0) before showing code
- [ ] Every core concept brought in 1 Tier 1 external material
- [ ] No vague phrasing like "simply put" / "basically"
- [ ] Didn't tell the student "go read the code yourself"
- [ ] Every "the repo implements X" claim has a comparison table

### V2 additions (abstract principles)

- [ ] stage-0 recommended repos passed a real Phase 2C search (WebSearch + WebFetch verified README / imports) — not AI memory-based picks
- [ ] stage-0 recommended repos were confirmed by the user from 3-5 candidates — not AI unilateral picks
- [ ] stage-0 recommended repos start from **first principles** — only low-level API (remote hosted or local inference) + standard library, **not** covered by any framework abstraction that hides the agent-loop skeleton
- [ ] Teaching materials are judged by "**teaching structure**" (progression + concept setup + minimal comparison), **not** by authority / star / implementation completeness / other "easily confused metrics"
- [ ] **Reference-type resources** (cookbook / quickstart / API SDK docs / production demos) go into `reference/` or stage-3 §4.1 sources, **not** stage-0/1/2 main teaching lines
- [ ] walkthrough §4.1 always has "source-reference + summary as two code blocks"; the reference is real, runnable, community/author-vetted code — **not** AI improvisation
- [ ] §4.1's source references include precise file:line and "why this is the authoritative minimal implementation" explanation
