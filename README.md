# learn-via-repo

> **An [Agent Skills](https://agentskills.io) standard skill** that helps you systematically learn a software engineering domain by deeply reading one open-source project.

> The skill and its docs are written in English. The teaching artifacts the skill generates for you adapt to your language — say "教我 redis" and the materials come back in Chinese; say "teach me redis" and you get English.

Whether you want to learn AI agents, web frameworks, database internals, operating systems, compilers, game engines, or distributed systems — as long as a decent open-source repo exists for that domain, this skill turns "I'm staring at this code and have no idea what's going on" into "I can read it, modify it, and explain why it's designed this way."

Compatible with every agent runtime that supports the Agent Skills standard — Claude Code, Claude.ai, Cursor, GitHub Copilot, Codex, Gemini CLI, Goose, OpenHands, Roo Code, Letta, Kiro, Workshop, and 30+ others. Full compatibility list at [agentskills.io/clients](https://agentskills.io/clients).

---

## Why this skill exists

If you've ever been in one of these situations, you know the feeling:

- You want to learn AI agents, you open the LangChain source, and after an hour you still can't tell what the agent is actually doing — it's all framework wrappers
- You want to read an industrial-scale repo (redis, postgres, v8), you open it, and there are hundreds of thousands of lines with no obvious starting point. The README assumes you already know.
- You followed a tutorial, ran the hello-world, it worked — but you have no idea **why** it works that way. Pick up another project and you're starting from zero again.

The common problem: **there's no gradual path that goes "first build a mental model, then get hands-on, then read the real code, then transfer it to your own project."** The resources out there are either too abstract (papers and blogs without code) or too concrete (raw source without buildup).

This skill turns "learning a domain through one repo" into a 5-stage flow: get hands-on with a simple repo to get a feel for the domain (stage-0), build a mental model of the whole domain (stage-1), study the target repo's architecture (stage-2), have an "instructor" walk you through the code (stage-3), then apply it to your own project (stage-4).

---

## What you get

When the skill triggers, it generates a complete teaching system (markdown files across 10 top-level directories), tailored to your level and goals:

```
{your-learning-project}/
├── README.md                    ← The first thing you open: welcome + learning path
├── meta/                        ← Teaching methodology + recommended path + your progress
├── stage-0-fundamentals/        ← Hands-on prerequisite: run a no-framework beginner repo
├── stage-1-foundations/         ← Domain-wide mental model (no code reading yet)
├── stage-2-architecture/        ← Target repo's architecture (diagrams + key design decisions)
├── stage-3-walkthroughs/        ← Instructor walks you through code (Minimal Comparison Method)
├── stage-4-applied/             ← Apply it to your own project (only if you bring a PRD)
├── reference/                   ← Cross-cutting lookup: code map / data flow / glossary
├── exercises/                   ← Cross-cutting problem set: concept checks / code-finding / transfer
└── resources/                   ← Cross-cutting external materials: papers / quality blogs / videos
```

Once the artifacts are generated, the skill stops and waits for you to say "start stage-0" or "start stage-1" before actually teaching.

---

## Quick start

One line to install (works for all 51+ agent runtimes — Claude Code / Cursor / Codex / Gemini CLI etc):

```bash
npx skills add CZYCW/learn-via-repo
```

The CLI **auto-detects** which agents you have installed, asks where to install, and puts files in the right place. No need to memorize paths.

Once it's done, **fully restart** your agent (CLI users: `exit` and reopen; desktop app users: ⌘Q and relaunch; IDE plugin users: restart the IDE), then type `/learn-via-repo` or just say "use this repo to teach me AI agents" — the skill kicks off the Phase 0 flow.

### Want more control?

- Full CLI options (pick specific agents / global vs project / skip prompts etc) — see [INSTALL.md](./INSTALL.md)
- No npm access (offline / restricted network) — see [INSTALL.md manual install section](./INSTALL.md#manual-install-when-you-cant-use-npm)
- Installed but `/learn-via-repo` doesn't show up? See [INSTALL.md troubleshooting](./INSTALL.md#troubleshooting-learn-via-repo-doesnt-show-up) — 90% of the time it's just that you didn't fully restart the agent.

### Find it on the marketplace

You can also search "learn-via-repo" on [skills.sh](https://skills.sh) and install from the page.

---

## Usage examples

### Scenario 1: Total beginner who wants to learn AI agents

```
You: "I want to learn AI agents, but I'm a complete beginner. Where should I start?"

The skill will:
1. Ask your level (A — total beginner, never touched code in this domain)
2. Give you 3-5 candidate target repos in the AI agent space and let you pick
3. Once you pick a target repo, find 3 simple intro repos for stage-0
4. Generate the full teaching artifacts
5. Tell you: "Run stage-0 hands-on first, then come back for stage-1"
```

### Scenario 2: Go engineer who wants to learn database internals

```
You: "Teach me to read redis"

The skill will:
1. Reverse-locate that redis is in the "database internals / kv store" domain at industrial scale
2. Ask your level (D — built small database projects)
3. Decide D + industrial-scale → recommend a lightweight stage-0
4. Find you a no-framework beginner database repo
5. Generate artifacts, with stage-2 architecture organized by redis modules
```

### Scenario 3: Frontend dev who got curious about compilers

```
You: "I've been doing frontend for 5 years, recently got curious about compilers. Can you teach me?"

The skill will:
1. Use a conversational approach to narrow down (babel? typescript? v8? lower-level LLVM?)
2. Once you pick a direction, find target repo candidates
3. Assess your level (B — read articles but haven't touched a compiler)
4. Recommend running a nano compiler in stage-0 (like chibicc)
5. Generate full artifacts
```

---

## Design philosophy (if you care about why it's built this way)

The methodology rests on 11 ideas from education and information architecture (Feynman technique, semantic waves, cognitive load, scaffolding, comparison learning, C4 model, Diátaxis, cognitive apprenticeship, Bloom taxonomy, wayfinding, Constructionism). Details in [references/theory.md](./references/theory.md).

A few core principles you should know:

1. **Hands-on first** (Papert's Constructionism): A/B-level beginners are pushed through stage-0 first — reading code without context is brutally abstract
2. **AI doesn't make up code on the fly**: Every "minimal implementation" references a real, runnable, community-vetted piece of code. No AI improvisations that might not even compile.
3. **AI doesn't unilaterally pick repos**: Every recommended repo goes through WebSearch verification first, then 3-5 candidates are handed to you to evaluate
4. **Always start from one request path**: Don't start reading from entry.ts / index.ts (which is just init code)
5. **Always explain acronyms the first time**: No throwing ADR / ACI / MMR / RAG at you and making you guess
6. **Conversational style like a real teacher**: No piling up phrases like "semantic waves + comparison learning + scaffolding"

---

## Document map

| File | Who reads it | What it is |
|------|------|-------|
| [README.md](./README.md) | Everyone | What you're reading — intro |
| [INSTALL.md](./INSTALL.md) | People who want to install | Setup steps for each agent runtime |
| [TESTING.md](./TESTING.md) | Test buddies | How to test + feedback template |
| [SKILL.md](./SKILL.md) | Agent runtimes / advanced users | Skill entry point, defines skill behavior |
| [references/methodology.md](./references/methodology.md) | People who want to understand the teaching method | Minimal Comparison Method + Feynman + semantic waves + three-layer progression |
| [references/output-structure.md](./references/output-structure.md) | People who want to understand the artifact structure | What each of the 10 top-level directories is for |
| [references/walkthrough-template.md](./references/walkthrough-template.md) | People writing stage-3 lessons | Nine-section template for a single walkthrough |
| [references/walkthrough-examples-multi-domain.md](./references/walkthrough-examples-multi-domain.md) | People who want cross-domain examples | Web / DB — two full mini walkthroughs |
| [references/exercises-template.md](./references/exercises-template.md) | People writing the problem set | Templates for the three problem categories |
| [references/checkpoints-and-scenarios.md](./references/checkpoints-and-scenarios.md) | People running the lessons | Checkpoint A/B + 6 teaching scenario templates |
| [references/forbidden-list.md](./references/forbidden-list.md) | Everyone | Teaching red lines (things you must not do) |
| [references/multi-domain-examples.md](./references/multi-domain-examples.md) | Cross-domain use | Abstract-concept-to-concrete-implementation mapping for 5+ domains |
| [references/theory.md](./references/theory.md) | People curious about the methodology's roots | 11 education / IA theories backing the method |

---

## Agent Skills standard

This skill strictly follows the [Agent Skills open standard](https://agentskills.io/specification):

- ✅ Standard `SKILL.md` frontmatter (`name` + `description`)
- ✅ Standard directory layout (SKILL.md + references/)
- ✅ Progressive disclosure (agent loads only name+description at startup; full content loads when a task matches)
- ✅ Cross-runtime compatible (works on any spec-compliant agent)

Publishable to any skill marketplace ([skills.sh](https://skills.sh) / [SkillsMP](https://skillsmp.com) / [ClawHub](https://clawhub.io) / Anthropic's official [github.com/anthropics/skills](https://github.com/anthropics/skills)).

---

## License

[MIT](./LICENSE) — use it, modify it, distribute it.

---

## Acknowledgments

- The 11 education theories backing the methodology are the result of decades of computer-science-education research — thanks to Papert, Maton, Sweller, Vygotsky, Bloom, Bayer, Procida, Brown, Newman, Simon Brown, Morville, and many others
- This skill was built with Claude (Anthropic) as a collaborator; the methodology author was involved in every design decision
- Thanks to Anthropic for opening up the [Agent Skills standard](https://agentskills.io), which is what lets this skill work across 30+ agent runtimes

If you find it useful, drop a star so others can find it.
