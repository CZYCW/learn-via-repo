# exercises/ 题库模板

> 每生成完一篇 `stage-3-walkthroughs/{NN}-{topic}.md`，立刻在 `exercises/` 三个文件中追加该主题的题。题目按 `## {NN}-{english-short-title}` 章节组织，与 walkthrough 文件名一一对应。**生成顺序**：先 walkthrough，再 exercises 三道追加，原子地完成同一主题。
>
> 题目示例以 AI Agent 领域为主（教学验证过），其他领域同结构——见本文档 §6 跨领域示例附录。

---

## 题库目录结构

```
exercises/
├── README.md              ← 题库说明 + 难度图例 + 使用方法
├── concept-checks.md      ← Feynman 式（概念是否真理解）
├── code-finding.md        ← file:line 定位（能否独立追踪代码）
└── transfer.md            ← 迁移到用户项目（能否应用）
```

---

## §1. concept-checks.md 模板（Feynman 式）

**目的**：检验学生是否真的理解概念，而不是"以为自己懂了"。
**何时做**：每完成一篇 walkthrough 的 §1-§3 后，进入 §4 代码前。这是教学节奏中的"检查点 A"。
**通过标准**：用一句话不用术语解释 + 反向论证 + 用术语 Repack 都能做。

### 模板（每个 topic 3 道）

```markdown
## {NN}-{english-short-title}

### 概念检查 1：Feynman 一句话解释

**问题**：用一句话，**不用任何术语**，告诉我 {核心概念} 解决了什么问题？

**通过标准**：
- 不用 `{术语 1}` `{术语 2}` `{术语 3}` 等词
- 一句话讲清楚痛点和解法
- 让一个不懂这个领域的人也能听懂

**通过后追问**：
"现在用术语重新表达一次"——必须能 Repack，否则说明概念还没内化。

---

### 概念检查 2：反向论证

**问题**：如果没有 {核心概念}，会发生什么最糟糕的事？

**通过标准**：能描述至少 2 个具体场景，每个场景对应一个被 {核心概念} 解决的问题。

---

### 概念检查 3：边界探测

**问题**：{核心概念} 在什么情况下会失效？或：什么场景下不应该用 {核心概念}？

**通过标准**：能识别该方案的局限，说明学生不是死背"X 是好的"，而是理解了 trade-off。
```

### 3 个完整示例（基于 OpenClaw 教学）

```markdown
## 02-react-loop-and-subagents

### 概念检查 1：Feynman 一句话解释

**问题**：用一句话，不用 "ReAct"、"工具"、"循环"、"递归" 等术语，告诉我 ReAct 解决了什么问题？

**通过标准**：能说出类似"让 AI 像人一样边查资料边写报告，而不是先全部查完再写或者干脆瞎编"。

**通过后追问**："现在用 Reasoning、Acting、Observation 三个术语描述刚才说的过程。"


### 概念检查 2：反向论证

**问题**：如果 LLM 只会推理不会行动，会发生什么？如果只会行动不会推理呢？

**通过标准**：
- 只推理不行动 → 幻觉（编造事实，因为模型只能用训练时的知识）
- 只行动不推理 → 盲目（不知道该用哪个工具，工具间无法串联）


### 概念检查 3：边界探测

**问题**：什么任务用 ReAct 反而是 over-engineering？

**通过标准**：能说出"一次性回答类任务"（如"3+5等于几"）—— 这种任务不需要工具，纯 LLM 即可。
```

---

## §2. code-finding.md 模板（file:line 定位）

**目的**：检验学生能否独立打开 repo 文件找到关键代码——这是"独立追踪代码"能力的核心。
**何时做**：每完成一篇 walkthrough 的 §4-§5 后。这是教学节奏中的"检查点 B+"。
**通过标准**：3 题至少 2 题答对，且能给出精确 `file:line`。

### 模板（每个 topic 3 道）

```markdown
## {NN}-{english-short-title}

### 代码定位 1：核心入口

**问题**：打开 `{file}`，找到 {function/class/concept} 的实现行号。

**期望答案**：`{file}:{line}`（{function_or_concept_name}）

**追问**：这一行对应最简版的什么？

---

### 代码定位 2：最简版映射

**问题**：最简版的 `{minimal_var_or_func}` 在 repo 里变成了什么？

**期望答案**：`{file}:{line}` 的 `{class.method}()`，因为 {为什么 repo 把它变成这样：通常是为了 并发安全 / 持久化 / 类型检查 / 错误处理 等}。

---

### 代码定位 3：工业级增强追踪

**问题**：repo 在 `{file}:{line}` 附近多做了一件最简版没做的事——是什么？为什么？

**期望答案**：
- 多做的事：{并发锁 / 超时控制 / TTL 缓存 / 等}
- 为什么需要：{具体场景，如"两条消息同时进入同一 session 会写坏 transcript"}
```

### 3 个完整示例（基于 OpenClaw 教学）

```markdown
## 02-react-loop-and-subagents

### 代码定位 1：核心入口

**问题**：打开 `src/agents/pi-embedded-runner/run/attempt.ts`，找到触发 ReAct 循环的那一行。

**期望答案**：`attempt.ts:1627`，`await abortable(activeSession.prompt(effectivePrompt));`

**追问**：这一行对应最简版的什么？
**期望答案**：对应最简版的 `act()` 递归调用入口——`activeSession.prompt()` 内部跑完整的 LLM→tool_use→execute_tool→continue 循环。


### 代码定位 2：最简版映射

**问题**：最简版的 `messages = []` 在 OpenClaw 的 ReAct 入口附近变成了什么？

**期望答案**：`attempt.ts:991` 的 `SessionManager.open(params.sessionFile)`——把内存列表换成了磁盘 JSONL 持久化，因为多消息间需要持久状态 + 重启恢复。


### 代码定位 3：工业级增强追踪

**问题**：`attempt.ts:991` 附近多做了一件最简版没做的事——是什么？为什么？

**期望答案**：
- 多做的事：`guardSessionManager(...)` 包裹 + `acquireSessionWriteLock`（前面几行）
- 为什么需要：防止同一 session 的两条并发消息同时写 transcript 导致错乱
```

---

## §3. transfer.md 模板（迁移到用户项目）

**目的**：检验学生能否把学到的 repo 模式迁移到自己的目标项目——这是 Bloom 分类法的"Create"层。
**何时做**：每完成一篇 walkthrough 的 §7 后，或全部 walkthrough 完成后整体复盘。
**通过标准**：无标准答案，但学生能说出"这个模式在我的项目里这样用 / 这个模式不适合我的项目，因为...，我要这样改"，就算通过。

### 模板（每个 topic 2 道）

```markdown
## {NN}-{english-short-title}

### 迁移应用 1：直接复用

**问题**：repo 的 `{核心模式}` 在你的项目（{user_project}）里可以怎么用？

**思考方向**：
- 你项目里有没有类似 {repo 的问题场景} 的需求？
- 直接照搬可行吗？需要调哪些参数？
- 用你项目的具体场景描述一遍这个模式的应用。

---

### 迁移应用 2：识别不适用 + 改造

**问题**：repo 的 `{核心模式}` 在你的项目里**不能直接用**，原因可能是 {不适用原因示例}。识别这个差异，并提出改造方案。

**思考方向**：
- repo 假设了什么前提（如单用户 / 本地部署 / markdown 友好）？
- 你的项目有什么不同前提（多用户 / 云部署 / 结构化数据）？
- 在你的前提下，这个模式应该怎么改？要保留什么、要替换什么？
```

### 3 个完整示例（基于 OpenClaw → Mnemos / AI 教练）

```markdown
## 03-session-and-memory

### 迁移应用 1：直接复用

**问题**：OpenClaw 的"三层记忆"（Bootstrap 热 / Semantic 温 / Episodic 冷）在 Mnemos 里可以怎么用？

**思考方向**：
- Mnemos 的"用户档案"对应 OpenClaw 的什么？（→ Bootstrap）
- Mnemos 的"历史咨询事件"对应什么？（→ Episodic）
- Mnemos 的"按主题检索"对应什么？（→ Semantic）
- 三层各自的容量上限和检索策略，你怎么定？


### 迁移应用 2：识别不适用 + 改造

**问题**：OpenClaw 的"文件即真相 + SQLite 索引"在 Mnemos 里**不能直接用**，因为 Mnemos 是多用户云服务。识别这个差异，并改造。

**思考方向**：
- OpenClaw 假设了"单用户 + 本地文件 + 用户可直接编辑 markdown"——你的多用户场景这些都不成立
- 改造方向：Postgres + pgvector 替代 SQLite + sqlite-vec，但保留"导出为 markdown"接口让用户可审查
- 必须保留的设计：三层架构（不变）、Hybrid + MMR + Temporal Decay（不变）、Memory Flush（思想保留，实现升级为写结构化记忆）
- 必须改的设计：单文件存储→分用户分表、文件系统 watcher→Postgres trigger / CDC
```

---

## §4. README.md（exercises/）模板

```markdown
# Exercises 题库使用指南

## 三类题的差异

| 类型 | 检验 | 何时做 | 通过标准 |
|------|------|--------|---------|
| concept-checks | 概念真理解（Feynman） | 学完每篇 walkthrough 的 §1-§3 后 | 一句话不用术语+反向论证+Repack |
| code-finding | 代码定位能力 | 学完每篇 walkthrough 的 §4-§5 后 | 3 题至少 2 题给出精确 file:line |
| transfer | 迁移到自己项目 | §7 之后或整体复盘 | 无标准答案，能说出"我项目里怎么用" |

## 难度图例

- 🟢 简单：能在 1 分钟内回答
- 🟡 中等：需要思考 2-5 分钟
- 🔴 困难：需要回到代码或文档查证 5-15 分钟

## 与 walkthrough 的对应

每个 `## {NN}-{english-short-title}` 章节对应 `stage-3-walkthroughs/{NN}-{english-short-title}.md`。

学完一篇 walkthrough 后，按顺序做：
1. concept-checks.md#{NN}-{topic}（如果卡住，回到 walkthrough §1-§3）
2. code-finding.md#{NN}-{topic}（如果卡住，回到 walkthrough §4-§5）
3. transfer.md#{NN}-{topic}（无答案，但要说出来）
```

---

## §5. 反例：什么样的检验题不合格

```
❌ "你理解 ReAct 了吗？"
   问题：太主观，学生可以撒谎说"理解了"
   修正：用 Feynman 一句话检验

❌ "解释 pi-agent-core 的作用。"
   问题：太宽泛，没有明确通过标准
   修正：拆为多个精确的 file:line 定位题

❌ "ReAct Loop 中需要哪些 tools？"
   问题：开放设计题，不可验证
   修正：改为"找到 attempt.ts 里组装工具列表的那个函数，它叫什么"

❌ "如果让你设计一个 ReAct 系统，你会怎么做？"
   问题：太大，学生可以无穷展开
   修正：归为 transfer.md，限定到"在你的项目场景下"
```

---

## §6. 跨领域示例附录（V3 新增）

上面 §1-§4 示例以 AI Agent 领域为主。其他领域同结构，下面是各领域 1 道示例：

### concept-checks 跨领域示例

| 领域 | 概念 | Feynman 一句话题 |
|------|------|----------------|
| Web 框架 | middleware 链 | "用一句话不用'middleware/next'术语，告诉我 `app.use(...)` 解决了什么问题？" |
| 数据库内核 | B-tree | "用一句话不用'B-tree/page'术语，告诉我 B-tree 为什么比链表快？" |
| 编译器 | tokenization | "用一句话不用'token/lexer'术语，告诉我编译器为什么先把源码切成片段？" |
| OS 内核 | context switch | "用一句话不用'寄存器/堆栈'术语，告诉我 OS 怎么让多个程序同时跑？" |

### code-finding 跨领域示例

| 领域 | 定位题 | 期望答案格式 |
|------|------|------------|
| Web 框架 | "打开 Express 的 application.js，找到 `app.use` 的实现行" | `application.js:228` |
| 数据库内核 | "打开 SQLite 的 btree.c，找到 cursor 的入口函数" | `btree.c:5234` 的 `sqlite3BtreeNext` |
| 编译器 | "打开 Acorn 的 parser/expression.js，找到表达式解析入口" | `parser/expression.js:90` |
| OS 内核 | "打开 xv6 的 trap.c，找到系统调用分发的那一行" | `trap.c:67` 附近 `syscall()` |

### transfer 跨领域示例

| 领域 | 迁移题 |
|------|------|
| Web 框架 | "目标 repo 的中间件链在你的项目里可以怎么用？比如你的 API gateway / 自己写 web app 时怎么复用？" |
| 数据库内核 | "目标 repo 的 cursor 抽象在你的项目里可以怎么用？比如你做流式数据处理时怎么借鉴？" |
| 编译器 | "目标 repo 的 AST visitor 模式在你的项目里可以怎么用？比如你做配置解析时怎么借鉴？" |
| OS 内核 | "目标 repo 的进程调度算法在你的项目里可以怎么用？比如你的 worker pool 怎么借鉴？" |

具体某个领域更详细的示例题，可在 walkthrough 配套生成时按本附录格式动态扩充。
