# 教学产物目录结构规范

> learn-via-repo 生成的所有教学产物必须遵循本文档定义的目录骨架。结构基于 Diátaxis 框架（软件文档四象限）+ Cognitive Apprenticeship（认知学徒制 6 阶段）+ Bloom 分类法（认知层级）+ Information Architecture wayfinding 原则。理论依据见 `theory.md`。

---

## 目录（Table of Contents）

- **§1. 完整目录骨架** —— 10 个一级目录速览图
- **§2. 每个目录的职责**
  - §2.1 README.md（根目录）—— 学生入口，含"小白友好开场段"模板
  - §2.2 meta/ —— 教学方法论 + 学习路径 + 进度跟踪
  - §2.2b stage-0-fundamentals/ —— 动手前置（V2 新增，A/B/C/D 级学生生成）
  - §2.3 stage-1-foundations/ —— 领域全局认知（不读代码）
  - §2.4 stage-2-architecture/ —— repo 架构原理（不深入代码）
  - §2.5 stage-3-walkthroughs/ —— 老师带读代码（最简对照法五步）
  - §2.6 stage-4-applied/ —— 应用到用户目标项目
  - §2.7 reference/ —— 横切，事实查询
  - §2.8 exercises/ —— 横切，题库（与 walkthrough 配对生成）
  - §2.9 resources/ —— 横切，外部材料 Tier 1/2/3
- **§3. 产物之间的引用关系**
- **§4. 文件命名约定**
- **§5. 生成策略** —— Phase 3 的 6 批顺序

---

## §1. 完整目录骨架

```
{output_dir}/
├── README.md                          ← "You are here" + 学习路径建议
│
├── meta/                              ← 过程性资源：教学方法论 + 进度
│   ├── teaching-style.md              ← 本 skill 教学风格（从 methodology.md 派生为学生可读版）
│   ├── learning-path.md               ← 推荐学习顺序 + 各阶段毕业标准
│   └── progress.md                    ← 学生进度跟踪（每次教学后更新）
│
├── stage-0-fundamentals/              ← V2 新增：动手前置（仅当 Phase 2.5 决定生成）
│   ├── README.md                      ← clone 命令 + 推荐学习章节顺序 + 完成标准
│   ├── prerequisites.md               ← 准入条件（运行时版本 + LLM 推理方式配置）+ 环境准备
│   ├── recommended-repos.md           ← Phase 2C 搜出 + 用户评估确认的 1-3 个 beginner repo + 推荐理由
│   ├── learning-guide.md              ← 哪些章节重点看、哪些可略过
│   └── graduation-check.md            ← 走完后该能做什么（具体可验证）
│
├── stage-1-foundations/               ← Diátaxis: Explanation
│   ├── README.md
│   ├── 01-mental-model.md             ← 领域心智模型
│   ├── 02-design-patterns.md          ← 领域常见设计模式分类
│   └── 03-state-of-the-art.md         ← 行业现状与前沿
│
├── stage-2-architecture/              ← Diátaxis: Explanation
│   ├── README.md
│   ├── 00-overview.md                 ← 整体架构鸟瞰
│   ├── 01-{module}.md                 ← 每模块的设计原理 + 关键 ADR
│   └── ...
│
├── stage-3-walkthroughs/              ← Diátaxis: Tutorial
│   ├── README.md                      ← 阅读顺序、每篇预备知识
│   ├── 01-{topic}.md                  ← 严格按 walkthrough-template.md
│   └── ...
│
├── stage-4-applied/                   ← Diátaxis: How-to + Explanation
│   ├── README.md
│   ├── prd.md                         ← 用户项目 PRD（若 Phase 1 提供）
│   ├── reusable-patterns.md           ← repo 哪些设计可复用
│   ├── what-needs-change.md           ← repo 哪些设计不适合，怎么改
│   └── mvp-sketch.md                  ← MVP 设计草图
│
├── reference/                         ← Diátaxis: Reference（横切）
│   ├── code-map.md                    ← 全 repo 关键 file:line 索引
│   ├── data-flow.md                   ← 一条消息端到端路径
│   └── glossary.md                    ← 术语表（领域 + repo 专属）
│
├── exercises/                         ← 横切：检验题库（与 walkthrough 配对）
│   ├── README.md
│   ├── concept-checks.md              ← Feynman 式
│   ├── code-finding.md                ← file:line 定位题
│   └── transfer.md                    ← 迁移到用户项目
│
└── resources/                         ← Diátaxis: Reference（横切）
    ├── README.md                      ← Tier 1/2/3 分级索引
    ├── papers/
    ├── articles/
    └── videos.md
```

---

## §2. 每个目录的职责

### §2.1 README.md（根目录）

**职责**：学生第一次打开教学产物时的入口。
**Diátaxis 类型**：Wayfinding（不属于四象限，但 IA 原则之一）。
**语气**：**鼓励性、降低恐惧、用大白话**（V3 强化——本 skill 要给小白用，第一印象决定学生是否继续）。

#### 模板结构（V3 强化）

```markdown
# 欢迎来到 {领域} 学习之旅 🚀

你将通过深入读懂 [**{目标 repo}**]({repo URL}) 来系统学习 {领域}。

> **第一句话**：你不需要现在就懂 {领域}——这正是这套教学要解决的。
> 我（AI 老师）会按一套科学的方法论带你从零到能独立追踪代码。

---

## 这套教学是怎么工作的

**5 个阶段 + 4 个横切资源**（你不需要全读，按推荐路径走就行）：

{目录可视化（按 §1 骨架）}

**推荐学习路径**：

{根据 Phase 2.5 决定的 stage-0 是否生成，分两个模板：A 含 stage-0 / B 跳过 stage-0}

1. **stage-0 fundamentals**（仅当生成）：先动手跑一个简单 repo，把核心控制流跑通、改、玩
2. **stage-1 foundations**：不读代码，建立 {领域} 的全局心智模型
3. **stage-2 architecture**：读 {目标 repo} 的设计原理（架构图 + ADR），不深入代码
4. **stage-3 walkthroughs**：老师带你精读 {目标 repo} 的核心代码
5. **stage-4 applied**（仅当你提供了项目 PRD）：把学到的应用到你自己的项目

**横切资源**（随时用，不必按顺序）：
- 📚 `reference/` —— 查事实（code-map / data-flow / glossary）
- ✅ `exercises/` —— 做题验证理解（每篇 walkthrough 配套）
- 📖 `resources/` —— 外部权威材料（Tier 1/2/3 分级）
- ⚙️ `meta/` —— 教学方法论 + 进度跟踪

---

## 我（AI 老师）会怎么教你

- **绝不跳过基础**：A/B 级小白会被强制走 stage-0 动手——光读代码会非常抽象
- **用 Feynman 检验**：你说"我懂了"不算通过——要用一句话不用术语解释，证明真的内化
- **代码引用必带 file:line**：你能跟着我打开任何引用的代码行，不是抽象描述
- **永远从一条请求的路径开始**：不从 `entry.ts` / `index.ts` 这种"配置初始化"开始
- **不临场写代码**：所有"最简实现"都引用现成、可运行的代码，不让你看 AI 编出来跑不通的版本

详细方法论见 `meta/teaching-style.md`（5 分钟读完）。

---

## 你（学生）需要怎么配合

| 节奏阶段 | 你的动作 |
|---------|---------|
| 概念讲解 | 听完后用**自己的话**复述（Feynman 检验）。说不清楚 = 没真懂，告诉我 |
| 进代码前 | 我会让你"打开 {file}，找到 {function}"——你**真去操作**，找不到要说 |
| 代码走读 | 跟着代码看，**不要假装懂**——卡住立刻打断 |
| 工业级增强 | 听我解释"这里多 N 行做什么"——记住"不是更多概念，是更健壮" |
| 教学结束 | 做对应的 `exercises/` 题，做错回去复习 |

---

## 卡住了怎么办

**别硬撑**——卡住是学习的一部分。具体策略：

| 情况 | 怎么办 |
|------|-------|
| "概念我没听懂" | 直接说"我没懂，再换个角度"——我会给具体例子或反向论证 |
| "代码找不到" | 说"我打不到 {function}"——我会给精确行号 + 教你用 grep / IDE 跳转 |
| "动手 stage-0 报错卡了" | 卡 ≥ 15 分钟说出来——我用 5W 排查（你跑了什么命令？期望啥？实际啥？...） |
| "exercises 题做错了" | 说"我答错了，回去看哪段？"——我指向对应 walkthrough 区块 |
| "我跟不上节奏" | 说"放慢"——我会拆更小的段 |

---

## 何时开始

说 `开始 stage-0`（如果有）或 `开始 stage-1` 触发教学。
也可以先自由浏览所有产物。准备好了再开教。
```

#### 必须包含的元素清单

- ✅ 鼓励性开场（第一句话降低恐惧）
- ✅ 一句话说明"这套教学是关于什么 repo、什么领域、面向什么目标"
- ✅ 完整目录骨架的可视化
- ✅ 推荐学习路径（根据 stage-0 是否生成分两种模板）
- ✅ stage-0 是否生成的说明
- ✅ 横切资源什么时候用
- ✅ **"我会怎么教你"**（教学方法论的学生视角概述）
- ✅ **"你需要怎么配合"**（学生侧的动作指南）
- ✅ **"卡住了怎么办"**（场景 D 脱困策略的用户视角版）
- ✅ "何时开始"的触发指令

### §2.2 meta/

**职责**：教学元信息——方法论、路径、进度。
**生成时机**：Phase 3 最先生成（其他目录依赖 meta/learning-path.md 的路径定义）。

- **teaching-style.md**：从 `methodology.md` 派生的学生可读版。学生在被 Feynman 检验时不理解为什么这么严苛，回这里看依据。
- **learning-path.md**：推荐学习顺序 + 各阶段毕业标准。每阶段过渡的检验要求（如"进入 stage-3 前必须能口头复述 stage-2-architecture 的核心 4 张架构图"）。
- **progress.md**：学生进度跟踪文件，模板含"当前阶段 / 已完成 / 卡在哪 / 下次起点"。每次教学结束更新。

### §2.2b stage-0-fundamentals/（V2 新增）

**职责**：动手前置——学生在读 stage-1/2/3 之前先 clone 一个权威 beginner repo 跑通、改、玩，建立"我自己写过一个 agent"的肌肉记忆。
**Diátaxis 类型**：Tutorial（学着做）。
**Bloom 层级**：Apply（首先动手 = 应用）。
**Constructionism 理论支撑**：Papert 的"通过建造学习"——动手做比被动听课有效 10 倍。详见 `theory.md` §13。
**生成时机**：仅当 Phase 2.5 评估学生为 A/B/C/D 级时生成；E 级跳过。

#### 文件清单

- **README.md**：动手清单——clone 命令、推荐章节顺序、预计耗时、卡住怎么办
- **prerequisites.md**：准入条件
  - 语言运行时版本（具体取决于推荐 repo，如 Python ≥3.10 / Node ≥18 等）
  - **LLM 推理方式配置**：按学生在 Phase 1.6 选的偏好（远程托管 / 本地推理），写对应配置步骤
  - 环境变量 / 配置文件示例
  - **原则**：LLM 推理方式是配置偏好，不影响学习效果（详见 `forbidden-list.md` §5b 元教训 1）
- **recommended-repos.md**：**Phase 2C 搜出 + 用户评估确认**的 1-3 个 beginner repo
  - 每个 repo：URL、star、为什么权威、与目标 repo 的关联度
  - **AI 不独断指认**（详见 `forbidden-list.md` §5 元教训 3）
- **learning-guide.md**：针对每个推荐 repo
  - 哪些章节是 stage-3 §4.1 引用源（必看）
  - 哪些章节是补充（可略）
  - 推荐学习顺序（如果有多个 repo）
- **graduation-check.md**：走完后该能做什么（可验证）
  - "你能不参考代码独立写出 act() 递归吗？"
  - "你跑通了几个 demo？"
  - "你能改 system prompt 让 agent 行为变化吗？"
  - 通过条件 = 进入 stage-1 的前提

#### 与其他目录的关系

- **stage-0 → stage-3**：stage-0 学过的代码是 stage-3 §4.1 的**首选**引用源（"学生最熟悉的代码"）
- **stage-0 → reference**：stage-0 的具体 file:line 不进 code-map.md（code-map.md 是**目标 repo** 的索引，不是 beginner repo 的索引）
- **stage-0 → exercises**：stage-0 的检验题写入 graduation-check.md，**不**进 exercises/ 三类题库（exercises/ 是 stage-3 配对的）

#### 关键约束（详见 forbidden-list §5）

- **第一性原理约束**：推荐 repo 必须无 agent loop 抽象封装——`messages.append(...)` + `if stop_reason == "tool_use"` 等骨架可见。详见 `forbidden-list.md` §5 判断方法 + 不合格框架列表
- **LLM 推理方式不影响选材**：远程托管 / 本地推理两类 repo 都合格——agent loop 骨架与 LLM 调用解耦
- **教学价值 ≠ 权威性**：参考型资源（cookbook / quickstart / production demo）即使权威也不适合作为 stage-0 主线，应归 reference/。判断方法：README 有没有递进顺序（"先看 N，再看 N+1"）

#### OpenClaw 学习场景的真实推荐（示例，由 Phase 2C 搜出 + 用户评估确认）

```markdown
# stage-0-fundamentals/recommended-repos.md（OpenClaw 学习场景示例）

1. **rohitg00/ai-engineering-from-scratch** Phase 14 前 12 课（7.8k stars）
   - 系统化课程结构，"raw API first then framework"
   - 后续 lessons 13-18 主动跳过（引入 LangGraph）

2. **pguso/ai-agents-from-scratch** (JS, 3.5k stars)
   - 14 课最系统递进，JS 跟 OpenClaw TS 同源
   - 默认本地 LLM，可切到 OpenAI API

3. **Leonie Monigatti notebook + 博文**
   - 4 组件递进（LLM/memory/tool/agent loop），Anthropic API 体系
   - 与 OpenClaw 同 Anthropic 体系，无缝衔接
```

---

### §2.3 stage-1-foundations/

**职责**：领域全局认知——**不读代码**，建立心智模型。
**Diátaxis 类型**：Explanation。
**Bloom 层级**：Remember + Understand。

- **01-mental-model.md**：该领域的"五要素抽象"（如 AI Agent = LLM + Memory + Tools + Loop）
- **02-design-patterns.md**：该领域 3-5 个核心设计模式
- **03-state-of-the-art.md**：行业现状与前沿（基于网络调研）

**关键约束**：不出现任何 repo 的 file:line。学生学完这阶段，对该领域应该有完整的"行业从业者级"认知，可以独立讨论。

### §2.4 stage-2-architecture/

**职责**：目标 repo 的架构原理——**不深入代码细节**，建立架构层心智模型。
**Diátaxis 类型**：Explanation。
**Bloom 层级**：Understand + Apply。

- **00-overview.md**：整体架构鸟瞰（mermaid 图 + 四大支柱式归纳）
- **01-{module}.md** ~ **N-{module}.md**：每模块一篇

每篇结构推荐（不强制，与 walkthrough-template 区分）：
- §0 通用 AI Agent 视角（外部资料 + 该领域如何处理这个问题）
- §1 这个模块解决什么问题
- §2 核心概念 + 术语表
- §3 整体架构（含 mermaid）
- §4 关键设计决策（ADR 格式：Context / Decision / Consequence）
- §5 运行时场景（mermaid 时序图，1 个典型用例）
- §6 代码地图（高层级，3-5 个核心 file:line，**不展开**）
- §7 对用户目标项目的启发

**关键约束**：可以引用 file:line，但只能是"指向哪里有"，不能是"逐行讲解"。逐行讲解归 stage-3-walkthroughs。

### §2.5 stage-3-walkthroughs/

**职责**：老师带读代码——严格按最简对照法五步。
**Diátaxis 类型**：Tutorial。
**Bloom 层级**：Apply + Analyze。
**Cognitive Apprenticeship**：Modeling（老师示范）+ Scaffolding（最简对照法是脚手架）。

每篇必须严格遵循 `walkthrough-template.md` 的 §0-§8 九章模板。

**生成顺序**：跟着数据流方向逐模块深入。第 1 篇必须是"一条消息端到端"（建立全局流程感），第 2 篇开始按模块拆分。

### §2.6 stage-4-applied/

**职责**：把学到的 repo 模式应用到用户的目标项目。
**Diátaxis 类型**：How-to + Explanation 混合。
**Bloom 层级**：Create。
**Cognitive Apprenticeship**：Exploration（学生自主探索）。

- **prd.md**：用户项目的 PRD（若 Phase 1 提供则直接拷贝，否则留模板）
- **reusable-patterns.md**：repo 哪些设计可以直接复用（含三列对照：repo 的设计 / 在用户项目里怎么用 / 为什么适合）
- **what-needs-change.md**：repo 哪些设计不适合用户场景，怎么改（三列对照：repo 的设计 / 为什么不适合 / 怎么改）
- **mvp-sketch.md**：用户项目的 MVP 设计草图——用 stage-1/2/3 学到的模式拼

**关键约束**：本目录的内容**只在用户提供了目标项目 PRD 时生成**。否则只放 README.md 说明"如何应用学到的内容"。

### §2.7 reference/（横切）

**职责**：事实查询，不解释、不教学。
**Diátaxis 类型**：Reference。
**何时用**：学生在 stage-3 走读时忘了某个 file:line，回这里查。

- **code-map.md**：全 repo 核心 file:line 索引，按模块组织。每条带一句话说明。
- **data-flow.md**：一条消息从入口到 LLM 调用的端到端路径图（mermaid + file:line）。
- **glossary.md**：术语表——领域通用术语 + repo 专属术语，每条一句话定义。

### §2.8 exercises/（横切）

**职责**：检验学生是否真的理解了。
**生成时机**：每生成完一篇 stage-3-walkthroughs/{N}-{topic}.md，立即在三个文件中追加该 topic 的题（参见 `exercises-template.md`）。

- **concept-checks.md**：Feynman 式（"用一句话不用术语解释"+反向论证）。3 道/topic。
- **code-finding.md**：file:line 定位题（可验证）。3 道/topic。
- **transfer.md**：迁移到用户项目（开放但有方向）。2 道/topic。

题目按 `## {N}-{topic}` 章节组织，与 walkthrough 一一对应。

### §2.9 resources/（横切）

**职责**：外部材料的索引和归档。
**Diátaxis 类型**：Reference。

- **README.md**：Tier 1/2/3 分级索引
  - Tier 1（必读）：领域权威官方指南、被广泛引用的论文、领域权威深度文章
  - Tier 2（深入）：高质量技术博客、具体实现教程、框架官方文档
  - Tier 3（参考）：辅助材料、案例研究、竞品分析
- **papers/**：论文 PDF（若可下载）
- **articles/**：高质量博客（用 WebFetch 下载为 markdown）
- **videos.md**：视频链接清单（YouTube / B站等）

---

## §3. 产物之间的引用关系

```
README.md (root)
  ├─→ meta/learning-path.md (路径)
  ├─→ stage-1 / stage-2 / stage-3 / stage-4 (按顺序)
  └─→ reference / exercises / resources (横切随时)

stage-1-foundations/*.md
  └─→ resources/ (引用 Tier 1/2 材料)

stage-2-architecture/*.md
  ├─→ stage-1 (建立心智模型的前提)
  ├─→ reference/code-map.md (只引用，不展开)
  └─→ resources/

stage-3-walkthroughs/{N}-{topic}.md
  ├─→ stage-2 同主题文档（架构层）
  ├─→ §6 检验问题链接 → exercises/{三类}.md#{N}-{topic}
  ├─→ §4 代码 → reference/code-map.md（引用精确位置）
  ├─→ §0 通用视角 → resources/（引用 Tier 1 材料）
  └─→ §7 对你目标项目的启发 → stage-4-applied/

stage-4-applied/
  └─→ 引用所有 stage-3 同主题模式
```

---

## §4. 文件命名约定

- 阶段目录用 `stage-{N}-{name}/`，N 是 1-4
- 每阶段内文件用 `{两位序号}-{英文短标题}.md`
- 横切目录不用序号（如 `reference/code-map.md` 不是 `01-code-map.md`）
- README.md 一律小写
- 不使用空格、用连字符
- 中文标题写在文件内部一级标题，文件名用英文

---

## §5. 生成策略

Phase 3 的并行生成顺序：

```
第 0 批（V2 新增，仅当 Phase 2.5 决定生成）：
  - stage-0-fundamentals/README.md
  - stage-0-fundamentals/prerequisites.md
  - stage-0-fundamentals/recommended-repos.md（含 Phase 2C 搜出 + 用户评估的 1-3 个 repo）
  - stage-0-fundamentals/learning-guide.md
  - stage-0-fundamentals/graduation-check.md

第 1 批（最先，其他依赖它们）：
  - meta/learning-path.md
  - meta/teaching-style.md
  - resources/README.md（Tier 分级）
  - reference/glossary.md（先建术语表）

第 2 批（基于第 1 批）：
  - stage-1-foundations/*.md（基于 Phase 2 的网络调研）
  - reference/code-map.md（基于 Phase 2 的 repo 探索）
  - reference/data-flow.md（基于 Phase 2 的端到端追踪）

第 3 批（基于前两批）：
  - stage-2-architecture/00-overview.md
  - stage-2-architecture/01-{module}.md ... N-{module}.md

第 4 批（最重的）：
  - stage-3-walkthroughs/{N}-{topic}.md
  - 每生成一篇，同步追加 exercises/三个文件

第 5 批（最后，依赖 prd.md）：
  - stage-4-applied/*.md（仅当用户提供 prd）

最后：
  - README.md（根目录，作为索引）
  - meta/progress.md（初始空模板）
```

每批内的文件可以并行生成（独立的 Write 调用）。
