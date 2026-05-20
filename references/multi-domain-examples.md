# Multi-Domain Examples Library

> This skill's methodology is domain-agnostic, but learners most easily understand abstract principles by mapping "the domain I know + a similar domain." This doc establishes "abstract concept → concrete implementation" mappings for 5-6 common software-system domains, **referenced** (not duplicated) by `methodology.md` / `walkthrough-template.md` / `forbidden-list.md`.

---

## §1. Core mapping table (5 required + 2 optional)

Each domain provides 5 dimensions of concreteness:

| Dimension | AI Agent | Web Framework (Express/Koa style) | Database Internals (SQLite style) | Compiler / Interpreter (V8/Lua style) | OS Kernel (xv6 style) | Game Engine (optional) | Distributed Systems (optional) |
|------|---------|---------|---------|---------|---------|---------|---------|
| **Core control flow** | ReAct loop (LLM ↔ tool ↔ observation recursion) | request → middleware chain → handler → response | parser → planner → VM opcode loop | tokenize → parse AST → bytecode/IR → execute | syscall trap → scheduler → context switch → return | input → update → render game loop | leader election → consensus round → state replication |
| **Core entry file** (example) | `attempt.ts` / `agent.py` | `app.js` / `application.js` | `main.c` / `vdbeapi.c` | `parser.cc` / `interpreter.c` | `proc.c` / `trap.c` | `engine.cpp` / `main.cpp` | `raft.go` / `consensus.rs` |
| **Key skeleton elements** (visible = first principles; invisible = framework hides it) | `messages.append({role, content})` + `if stop_reason == "tool_use": execute_tool(...)` | `next(err)` chain + `req` / `res` object passing | B-tree cursor ops + opcode dispatch loop | TokenScanner + ASTNode construction + Visitor pattern | trap frame save + scheduler queue + page table switch | game loop tick + ECS component queries + render queue | log entry append + AppendEntries RPC + commit index advance |
| **Qualified beginner repo examples** (**verification status below** — AI still runs Phase 2C search + user evaluation) | ✅ Verified: rohitg00/ai-engineering-from-scratch Phase 14 / pguso/ai-agents-from-scratch / Leonie Monigatti notebook | ⚠️ Unverified candidate: koajs/koa / expressjs/express early commits | ⚠️ Unverified candidate: cstack/db_tutorial / sql-js/sql.js / erikgrinaker/toydb | ⚠️ Unverified candidate: acornjs/acorn / chibicc / craftinginterpreters/craftinginterpreters | ⚠️ Unverified candidate: mit-pdos/xv6-riscv | ⚠️ Unverified candidate: handmade hero / pico-8 tutorials | ⚠️ Unverified candidate: ongardie/raftscope |
| **Disqualifying framework examples** (mature wrappers that hide the skeleton; non-exhaustive — use forbidden-list.md §5 judgment for new frameworks) | langchain / langgraph / llamaindex / crewai / autogen / smolagents / openai-agents-sdk | NestJS / Hapi (deeply abstracted) / Adonis / Spring | sqlalchemy / typeorm / prisma / hibernate | babel (heavily wrapped modern) / TypeScript compiler (black box) | docker / k8s (not OS kernels — high-level schedulers) / systemd (init framework) | Unity / Unreal Engine (engine black box) / Godot (partially) | k8s controller-runtime / spring-cloud / consul-template |

---

### §1.5 The difference between "Verified" and "Unverified" (important)

In the V3 upgrade, the AI agent row's beginner repos went through the real Phase 2C 4-step flow (search → WebFetch verify README → 3-5 candidates to user → user evaluation), so they're marked ✅ Verified.

Other domains' beginner repos are "starting candidates" listed by me (the V3 author) based on community impressions — **not validated through the real Phase 2C 4-step flow**. These candidates have several possibilities:
- Genuinely qualified (e.g., xv6 / Crafting Interpreters are recognized teaching classics in their domains, likely OK)
- No longer maintained or now using a framework (need re-evaluation)
- Better candidates exist that I didn't list

So when the AI actually runs Phase 2C:
1. ⚠️ Unverified candidates **can serve as search starting points** but can't be used directly
2. Must be verified using forbidden-list.md §5's judgment method (can you see the domain's skeleton elements in the README? are there mature-framework imports?)
3. Must give the student 3-5 candidates to evaluate — not just write one into stage-0
4. After verification, change the status from ⚠️ to ✅, with verification date / link

This table grows more accurate as the skill is used — each real teaching session in a new domain upgrades that row.

---

## §2. How to use this table

### §2.1 In `methodology.md`

After each abstract principle, add one sentence:

> Cross-domain examples: in AI agents this is X; the same principle in web frameworks is Y (see `multi-domain-examples.md` §1 row N), in databases is Z (same table)

Don't duplicate the table in methodology.md.

### §2.2 In `walkthrough-template.md` §0 / §4.1

When the AI generates a walkthrough, it reads the row matching **the target repo's domain** from this table as the example skeleton:

- Target repo is redis? → Read the "Database Internals" row
- Target repo is vue/express? → Read the "Web Framework" row
- Target repo is v8? → Read the "Compiler / Interpreter" row

### §2.3 In `forbidden-list.md` §5

Third-party framework blacklist is grouped by this table's "Disqualifying framework examples" column; each group says "this kind of framework hides what skeleton." Judge **new frameworks** with §3's method.

---

## §3. Cross-domain unified "is it a qualified beginner repo" judgment

Regardless of domain, run these 3 checks on any candidate beginner repo:

### Step 1: can you see the domain's core skeleton elements?

Open the README example code:

- AI agent: can you see `messages.append` + `tool_use` dispatch? ✅
- Web framework: can you see the `app.use((req, res, next) => ...)` middleware signature? ✅
- Database: can you see cursor operations + row/page IO? ✅
- Compiler: can you see token stream + AST node construction? ✅
- OS: can you see trap handler + scheduler queue? ✅

If you only see `framework.run(config)` / `agent.execute(task)` black-box APIs → disqualified.

### Step 2: is the core control flow visible enough to teach?

Does the repo have **one core loop / function / entry point** that implements the domain's "heart" in 50-200 lines?

- Qualified: teaching repos usually have a single readable entry like `agent.py` / `main.c` / `parser.cc`
- Disqualified: spread across 200+ files / heavy decorator abstractions / lots of dependency injection — the skeleton is hidden

### Step 3: is the dependency list restrained?

Open `requirements.txt` / `package.json` / `Cargo.toml`:

- Qualified: ≤ 5 dependencies, all low-level (e.g., `requests` / `anthropic` SDK / standard library)
- Disqualified: ≥ 20 dependencies including mature frameworks (e.g., `langchain` / `react` / `vue` / `django` / `rails`) — those frameworks are themselves the "skeleton" being learned; a beginner repo shouldn't pile another framework on top

---

## §4. What if the domain isn't in this table?

If the student wants to learn a domain not in §1 (e.g., blockchain / recommender systems / computer vision / quantum computing):

1. **AI doesn't make things up** — each row in this table is from accumulated teaching experience. Don't list examples from memory for a new domain.
2. **Phase 2C real search**: same as other domains — WebSearch + WebFetch to find candidate "framework-free beginner repos" in that domain, let the user evaluate.
3. **If mature candidates emerge**: backfill into this table (a contribution to the open-source skill), so the next student in that domain benefits.
4. **If no mature candidate exists**: tell the user honestly "I didn't find any ≥1k star + framework-free teaching repo in this domain. Suggestions: (a) run the full Phase 2C 4 steps — might find one (b) pick the simplest module in the target repo as a stage-0 substitute (c) skip stage-0 and go straight to stage-1."

See `forbidden-list.md` §5b meta-lesson 3 ("the AI cannot unilaterally pick repos").

---

## §5. Table extension rules (contributor guide)

Future contributors adding new domains follow these:

- Each row must have at least 1 qualified beginner repo example (not AI memory — must have been verified)
- Each row's "skeleton elements" must use terms that **real practitioners** in the domain use (not AI fabrications)
- Each row's "disqualifying frameworks" must pass §3 Step 1 verification — those frameworks really do hide the skeleton
- When adding a new domain, also update the "cross-domain examples" section links in `methodology.md` / `walkthrough-template.md` / `forbidden-list.md`

---

## §6. Current coverage

| Domain | Coverage | Notes |
|------|------|------|
| AI Agent | ⭐⭐⭐⭐⭐ | Complete, validated through OpenClaw teaching |
| Web framework | ⭐⭐⭐ | Skeleton elements + disqualifying frameworks listed; beginner repo examples need user verification before backfilling |
| Database internals | ⭐⭐⭐ | Same as above |
| Compiler / interpreter | ⭐⭐⭐ | Same as above |
| OS kernel | ⭐⭐⭐ | xv6 is the recognized standard; other examples need verification |
| Game engine | ⭐⭐ | Few examples |
| Distributed systems | ⭐⭐ | Few examples |

When you go through beginner-repo selection for any domain in real teaching, remember to backfill this table to benefit future students.
