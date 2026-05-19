# Walkthrough 模板（stage-3-walkthroughs/ 单篇标准结构）

> 每篇 `stage-3-walkthroughs/{N}-{topic}.md` **必须**严格遵循本模板的 §0-§8 九章结构。这是最简对照法五步的完整落地。
>
> 模板中的占位符用 `{...}` 标记。**示例以 AI Agent 领域（OpenClaw）为主**（教学验证过），跨领域类比锚点见 `multi-domain-examples.md` §1。任何领域（Web 框架 / 数据库 / OS / 编译器 / 游戏引擎 / 分布式 等）都套用同一九章结构。
>
> **跨领域完整 walkthrough 示例**（缩略版，每章 5-15 行说明，展示同九章模板在不同领域的实际呈现）见 `walkthrough-examples-multi-domain.md`：
> - 示例一：Web 框架 / Express middleware 链
> - 示例二：数据库内核 / SQLite B-tree cursor
>
> 生成实际 walkthrough 时，对照该文件的语气、术语密度、骨架元素呈现方式。

---

## 目录（Table of Contents）

- **文件命名** —— `{NN}-{english-short-title}.md`
- **文件标准结构（9 章）** —— 单篇 walkthrough 严格按此九章模板
  - §0 通用视角（领域背景）—— 外部权威材料 + Repack 到目标 repo
  - §1 这个模块解决什么问题 —— 反向论证 + 业界三种通用解法对比 + 一句话定位
  - §2 核心概念 —— 关键术语表 + 通用概念→repo 实现对照表
  - §3 整体架构 —— 组件关系图（mermaid）+ ADR 设计决策（≤3 个）
  - §4 最简对照法实战（5 步） —— 核心章节
    - §4.0 高层级代码框架（代码地图）
    - §4.1 Step 1：权威最简实现（**引用 + 摘要双区块**，不写 AI 临场代码）
    - §4.2 Step 2：目标 repo 对应代码
    - §4.3 Step 3：三列对照表（最简版 / repo 代码位置 / 说明）
    - §4.4 Step 4：工业级增强差异图
  - §5 代码导航 —— 分轮次（30 min 一轮）+ file:line
  - §6 检验问题 —— 链接到 exercises/ 三类题
  - §7 对用户目标项目的启发 —— 可复用 / 需改造 / 独有需求 三块
  - §8 延伸阅读 —— Tier 1/2/3 分级
- **每章的质量检验问题** —— 生成完一篇后的自检清单
- **反例：什么样的 walkthrough 不合格** —— 6 个常见错误

---

## 文件命名

`stage-3-walkthroughs/{NN}-{english-short-title}.md`

- `NN` 是两位序号（01, 02, ...）
- 英文短标题，用连字符
- 例：`01-message-end-to-end.md`、`02-react-loop-and-subagents.md`、`03-session-and-memory.md`

---

## 文件标准结构（9 章）

```markdown
# {NN} {中文主题}

> {30-60 分钟} 读完。读完你应能回答：
> 1. {核心问题 1}
> 2. {核心问题 2}
> 3. {核心问题 3}

---

## §0. 通用视角（领域背景）

> {1-2 句话引出"在该领域，这个问题被怎么处理"}

**学术/工程界的核心洞察**：{引用 Tier 1 权威材料 + 一句话击穿核心 Why}

> 示例（OpenClaw 教 ReAct）：
> 2022 年 Google/Princeton 的 Yao 等人在 [ReAct 论文](https://arxiv.org/abs/2210.03629) 证明：
> 推理（CoT）和行动（Action）交织进行比各自单独效果更好。
> 纯 CoT 在 HotpotQA 上的幻觉率比 ReAct 高 20%；纯 Action 在 ALFWorld 上比 ReAct 低 34%。

**Repack 到目标 repo**：{1 句话说明该 repo 是怎么实现这个洞察的}

**最简骨架预览**（语义波 Repack 锚点）：
```python
# 一眼看懂的 N 行最简实现
def {core_function}():
    ...
```

**延伸阅读**：参见 `resources/papers/{paper}.pdf` | `stage-1-foundations/{N}-{topic}.md`

---

## §1. 这个模块解决什么问题

### §1.1 反向论证

如果没有这个模块，{用户/开发者}要做什么？{1 段话描述痛点}

### §1.2 业界三种通用解法对比

| 方案 | 特点 | 代表 |
|------|------|------|
| {方案 A} | {特点} | {代表系统} |
| {方案 B} | {特点} | {代表系统} |
| {方案 C} | {特点} | **{目标 repo}** |

### §1.3 一句话定位

**{这个模块}是 {做什么的} 的 {什么东西}。**

---

## §2. 核心概念

### §2.1 关键术语

| 术语 | 英文 | 一句话定义 |
|------|------|-----------|
| {术语 1} | {Term 1} | {定义} |
| {术语 2} | {Term 2} | {定义} |
| ... | ... | ... |

### §2.2 通用概念 → 目标 repo 实现的对照表

| 通用概念 | {repo} 里的实现 |
|---------|----------------|
| {通用概念 1} | {repo 实现 1} |
| {通用概念 2} | {repo 实现 2} |
| ... | ... |

---

## §3. 整体架构

### §3.1 组件关系图

```mermaid
flowchart TB
  ...
```

### §3.2 关键设计决策（ADR 格式，最多 3 个）

#### ADR-1：{决策标题}

**Context**：{这个决策面临的约束是什么}
**Decision**：{选择了什么}
**Consequence**：
- ✅ {正向后果 1}
- ✅ {正向后果 2}
- ❌ {负向后果 1}（缓解：{怎么缓解}）

#### ADR-2 / ADR-3 同结构

---

## §4. 最简对照法实战

### §4.0 高层级代码框架（代码地图）

先看一张地图：

```
{入口事件}
    │
    ▼
{file1.ts:line1}      ← 一句话职责
    │ (调用)
    ▼
{file2.ts:line2}      ← 一句话职责
    │
    └── 关注这里的几行：
        - line {X}: {function}()  ← 为什么关键
        - line {Y}: {function}()  ← 对应最简版的哪一步
        - line {Z}: {function}()  ← 这是核心！
```

### §4.1 Step 1：权威最简实现（引用 + 摘要双区块，V2 升级）

> **V2 重要变更**：旧版让 AI 临场写 30-100 行——已废弃。AI 临场代码看着像但跑不通、跟权威实现也有差距。新版必须**引用现成、可运行、有社区背书的代码**。详见 `methodology.md` §4.1。

#### 区块 A：引用源（必填）

```markdown
**最简实现来源**：{repo-owner}/{repo-name}（{star 数} stars{，权威背书：xxx}）
**文件位置**：`{path/to/file.{py,ts,go}}:{start_line}-{end_line}`
**为什么这是权威最简实现**：{1-2 句话——通常是"作者是 X 大牛 / 该 repo 是 Y 课程 / Z 文章的官方代码"}
```

来源选取的**三级优先级**（详见 `methodology.md` §4.1）：

1. **stage-0 学过的 beginner repo**（学生跑过、改过、最熟悉）
2. **领域权威 nano-* / mini-* / 简洁实现 repo**（用户评估认可过——AI 不独断指认）
3. **AI 简化版**（仅当 1、2 都没有，**必须**标 `"基于 X 简化，未独立验证运行"`）

#### 区块 B：5-10 行伪代码摘要（必填）

> **不是运行版**——只是骨架的"翻译"，方便老师讲解 ReAct 三元组 / messages 列表等核心结构。学生想跑、想改、想验证——回到区块 A 的真实文件。

```python
# 改编自 {repo}/{path}:{lines}，剥离 error handling/streaming/concurrency，保留 {核心模式} 骨架
def {core_function}():
    """{1 句话职责}"""
    response = call_llm(messages, tools)
    if response.stop_reason == "tool_use":
        ...
```

#### 区块 A 的示例（OpenClaw 教学场景的真实推荐组合）

OpenClaw 学习场景下，stage-0 三件套推荐（**由 Phase 2C 网络搜索 + 用户评估确认**，AI 不独断）：

```markdown
**最简实现来源（之一）**：
  rohitg00/ai-engineering-from-scratch Phase 14 Lesson 01（7.8k stars，"raw API first"）
**文件位置**：`14-agent-engineering/lesson-01/agent.py:1-120`
**为什么权威**：作者明确"120 lines of pure Python, no dependencies"；后续 lessons 才引入
  LangGraph，确保 Lesson 01 是纯 raw API。学生先在 stage-0 跑通这个文件，再来对照。

**最简实现来源（之二）**：
  pguso/ai-agents-from-scratch（3.5k stars，JS 14 课系统教程）
**文件位置**：`examples/06-react-agent.js:1-95`（路径示意，实际以 stage-0 确认为准）
**为什么权威**：JS 跟 OpenClaw（TS）同源，14 课递进结构最系统，
  example 06 是 ReAct 完整实现且可切到 OpenAI API。

**最简实现来源（之三）**：
  Leonie Monigatti notebook（个人项目但 ML engineer 背景，Anthropic API 体系）
**文件位置**：`iamleonie/website/blob/main/blog/ai-agent-from-scratch-in-python.ipynb` Section 4
**为什么权威**：与 OpenClaw 同 Anthropic API 体系；4 组件递进（LLM/memory/tool/agent loop）
  直接对应 OpenClaw 的 LLM call + transcript + memory_tool + ReAct loop。
```

#### 反例（V2 禁止）

```
❌ §4.1 直接贴 80 行 AI 临场写的 Python，没"来源"字段
   → 学生跑不通时不知道找谁验证

❌ 引用了某个 repo 但不给精确 file:line，只说"类似 X 的实现"
   → 学生找不到对应位置

❌ AI 凭自己印象指认某个 repo 是"权威最简实现"，没经过 Phase 2C 搜索 + 用户评估
   → 例：把 microsoft/ai-agents-for-beginners 当合格示例（实际它基于 Microsoft Agent Framework）
   → 例：把 anthropic-cookbook 当"教学主线"（实际它是 cookbook 不是 curriculum）

❌ 引用了基于 langchain/langgraph/llamaindex/crewai/smolagents 的 beginner repo
   → 学生学到框架 API，不是骨架原理
```

### §4.2 Step 2：目标 repo 对应代码

```{language}
// {file}:{line}
// 对应最简版的：{最简版第几行/哪个函数}
{repo 实际代码片段}

// {file}:{line}
// 对应最简版的：{最简版第几行/哪个函数}
{另一段}
```

### §4.3 Step 3：三列对照表

| 最简版本 | {repo} 代码位置 | 说明 |
|---------|---------------|------|
| `{minimal_var}` | `{function}()` in `{file}:{line}` | {增加了什么} |
| `{minimal_func}()` | `{class.method}()` in `{file}:{line}` | {增加了什么} |
| ... | ... | ... |

### §4.4 Step 4：工业级增强差异图

```
最简版本 ({N} 行)              {repo} 增强 ({M} 行)
─────────────────              ──────────────────────────
{minimal_func}        →    + {增强 1：错误处理}
                                + {增强 2：超时}
                                + {增强 3：并发锁}
{minimal_var}         →    + {增强 1：持久化}
                                + {增强 2：TTL 缓存}
─────────────────              ──────────────────────────
核心原则：多出来的不是"更多概念"，是"把同样的事做得更健壮"
```

逐条解释（每条 1-2 句话）：
1. **{增强 1}**：为什么工业级需要这个（{具体原因}）
2. **{增强 2}**：...

---

## §5. 代码导航

### 第 1 轮（30 分钟）：{具体目标，如"追踪一条消息进入 ReAct 循环"}

1. 打开 `{file}`，搜索 `{function_name}`（约第 {N} 行附近）
2. 关注 line {X}-{Y}：{这块做什么，一句话}
3. 找到 line {Z}：`{key_function}()` —— 这是 {对应最简版的什么}

### 第 2 轮（30 分钟）：{具体目标}

1. ...
2. ...

### 第 3 轮（可选，30 分钟）：{具体目标}

...

---

## §6. 检验问题

学完本章后，去以下题库做对应主题的检验：

- **概念检查**：参见 `exercises/concept-checks.md#{NN}-{english-short-title}`
- **代码定位**：参见 `exercises/code-finding.md#{NN}-{english-short-title}`
- **迁移应用**：参见 `exercises/transfer.md#{NN}-{english-short-title}`

老师在带读完后，按以下顺序检验：
1. 先做概念检查（Feynman 式，进入下一个 walkthrough 的前提）
2. 再做代码定位（验证能独立打开文件找到位置）
3. 最后做迁移应用（探索性，无标准答案）

---

## §7. 对用户目标项目的启发

### §7.1 可以直接复用的设计

| {repo} 的设计 | 在你项目里怎么用 |
|--------------|-----------------|
| {设计 1} | {应用方式} |
| {设计 2} | {应用方式} |

### §7.2 需要改造的地方

| {repo} 的设计 | 为什么不适合你 | 怎么改 |
|--------------|--------------|-------|
| {设计 1} | {不适合的原因} | {改造方向} |
| ... | ... | ... |

### §7.3 你项目独有的需求（{repo} 没解决）

1. **{需求 1}** —— {为什么 repo 没解决，你需要怎么补}
2. **{需求 2}** —— ...
3. **{需求 3}** —— ...

---

## §8. 延伸阅读

### Tier 1（必读）

- [{论文/官方文档标题}]({URL}) —— {一句话说明为什么必读}

### Tier 2（深入）

- [{高质量博客标题}]({URL}) —— {一句话说明}

### Tier 3（参考）

- ...

### 本套相关文档

- `stage-2-architecture/{对应模块}.md` —— 这个模块的设计原理（架构层）
- `stage-3-walkthroughs/{相邻 walkthrough}.md` —— {相邻的代码主题}
- `reference/code-map.md` —— 全 repo 关键 file:line 索引
```

---

## 每章的质量检验问题

生成完一篇 walkthrough 后，作者（skill 自己）自检：

**§0**：
- 是否引入了 Tier 1 权威材料？
- 是否在 30 秒内能让读者理解"这是 Why"？
- 是否在引入外部材料后立即 Repack 到目标 repo？

**§1**：
- §1.1 是否用"反向论证"激发好奇心，而不是直接定义？
- §1.2 是否列出至少 3 种业界方案做对比？
- §1.3 是否能用一句话定位本模块？

**§2**：
- 术语表每条是否一句话？
- 通用概念→repo 实现的对照表是否清晰？

**§3**：
- 是否有 mermaid 架构图？
- ADR 是否 ≤3 个？每个是否完整三段（Context/Decision/Consequence）？
- Consequence 是否同时含 ✅ 和 ❌？

**§4**：
- §4.0 代码地图是否含 3-5 个核心 file:line？
- §4.1 最简实现是否 30-100 行？是否只有骨架无细节？
- §4.2 是否每段 repo 代码都有"对应最简版的什么"注释？
- §4.3 对照表是否严格三列？
- §4.4 是否用差异图而非表格？是否解释了每条增强的"为什么"？

**§5**：
- 是否分至少 2 轮？
- 每轮是否有明确目标 + 时间估计 + file:line？

**§6**：
- 是否链接到 exercises/ 三个文件的对应章节？

**§7**：
- 是否包含"可复用 / 需改造 / 独有需求"三块？
- 如果用户没提供 prd，§7 是否退化为"假设你做 {合理示例项目}"？

**§8**：
- Tier 1/2/3 是否都有？每条是否带"为什么读"？

---

## 反例：什么样的 walkthrough 不合格

```
❌ 没有 §0 通用视角，直接进入 §1 业务问题
   后果：学生不知道这个 repo 的方案在业界处于什么位置

❌ §4.1 最简实现写成 200 行 async/await/error-handling 全配的工业级代码
   后果：失去"最简对照"的意义，学生看不到骨架

❌ §4.2 展示 repo 代码不给 file:line
   后果：学生无法回到 repo 验证

❌ §4.4 把工业级增强写成表格，每项只有一个词
   后果：学生不理解"为什么"工业级需要这些

❌ §5 代码导航说"自己去看 attempt.ts 的核心循环"
   后果：违反"代码禁忌"——必须给精确行号

❌ §7 写成"对 AI Agent 开发者的启发"等宽泛话
   后果：失去"对用户目标项目"的针对性
```
