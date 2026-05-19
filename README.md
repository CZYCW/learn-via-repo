# learn-via-repo

> **一个 [Agent Skills](https://agentskills.io) 标准的 skill**，帮你通过**深入读懂一个开源项目**来系统学习一个软件工程方向。

不管你想学的是 AI Agent、Web 框架、数据库内核、操作系统、编译器、游戏引擎还是分布式系统——只要这个方向有合适的开源 repo，这个 skill 都能帮你把"光看代码看不懂"转变成"能独立读、独立改、能解释为什么这样设计"。

兼容所有支持 Agent Skills 标准的 agent runtime——包括 Claude Code、Claude.ai、Cursor、GitHub Copilot、Codex、Gemini CLI、Goose、OpenHands、Roo Code、Letta、Kiro、Workshop 等 30+ 个平台。完整兼容列表见 [agentskills.io/clients](https://agentskills.io/clients)。

---

## 为什么会有这个 skill

如果你试过下面这些场景中的任何一个，你大概知道这种感觉：

- 想学 AI Agent，打开 LangChain 源码——里面全是 framework 封装，看了半天不知道 agent 本质上在做什么
- 想读懂某个工业级 repo（redis、postgres、v8），打开后几十万行代码不知从哪起步，README 假设你已经懂
- 跟着 tutorial 跑了个 hello-world，跑通了但**不知道为什么是这样**，再换一个项目又得从头摸索

这些场景的共同问题是：**缺乏一个"先建立心智模型、再动手验证、再读真实代码、最后能迁移到自己项目"的渐进路径**。市面上的资源要么太抽象（论文/博客没代码），要么太具体（直接读源码没铺垫）。

这个 skill 把"通过一个 repo 学一个领域"这件事变成一个 5 阶段流程：先动手跑一个简单 repo 找感觉（stage-0），再建立领域全局心智模型（stage-1），再读目标 repo 的架构原理（stage-2），再老师带你精读代码（stage-3），最后应用到你自己的项目（stage-4）。

---

## 你会得到什么

skill 触发后会生成一套完整的教学产物（10 个一级目录的 markdown 文件），按你的水平和目标定制：

```
{你的学习项目目录}/
├── README.md                    ← 第一个打开看的：欢迎页 + 学习路径
├── meta/                        ← 教学方法论 + 推荐学习路径 + 你的进度跟踪
├── stage-0-fundamentals/        ← 动手前置：跑一个无框架的 beginner repo
├── stage-1-foundations/         ← 领域全局心智模型（不读代码）
├── stage-2-architecture/        ← 目标 repo 架构原理（架构图 + 关键设计决策）
├── stage-3-walkthroughs/        ← 老师带读代码（最简对照法五步）
├── stage-4-applied/             ← 应用到你自己的项目（仅当你提供项目 PRD）
├── reference/                   ← 横切查阅：代码地图 / 数据流 / 术语表
├── exercises/                   ← 横切题库：概念检验 / 代码定位 / 迁移应用
└── resources/                   ← 横切外部材料：论文 / 高质量博客 / 视频
```

生成完产物后 skill 会停下，等你说"开始 stage-0"或"开始 stage-1"触发实际教学。

---

## 快速开始

一行装好（适用所有 51+ agent runtime——Claude Code / Cursor / Codex / Gemini CLI 等都行）：

```bash
npx skills add CZYCW/learn-via-repo
```

CLI 会**自动检测**你装了哪些 agent，让你选装到哪里，自动放对路径。完全不用记路径。

完成后**完全重启** agent（CLI 用 `exit` 重开；桌面 app ⌘Q 后再 launch；IDE 插件重启 IDE），然后在 agent 里输入 `/learn-via-repo` 或直接说"用这个 repo 教我 AI agent"——skill 会按 Phase 0 流程开口问你。

### 想要更多控制？

- 完整 CLI 选项（指定 agent / 全局 vs 项目 / 跳过确认等）见 [INSTALL.md](./INSTALL.md)
- 不能用 npm 的环境（无网络 / 限制环境）：[INSTALL.md 手动安装段](./INSTALL.md#手动安装不能用-npm-时的备选)
- 装好但 `/learn-via-repo` 不出来？看 [INSTALL.md 故障排查](./INSTALL.md#故障排查learn-via-repo-找不到怎么办)——90% 问题是没完全重启 agent。

### 在 marketplace 上发现

也可以在 [skills.sh](https://skills.sh) 搜 "learn-via-repo" 看页面再点装。

---

## 用法示例

### 场景 1：完全小白想学 AI Agent

```
你："我想学 AI Agent，但完全不懂，应该从哪开始？"

skill 会：
1. 问你水平（A 级——完全没接触过该领域的代码）
2. 给你 3-5 个 AI Agent 方向的目标 repo 候选让你评估
3. 选完目标 repo 后，再帮你找 3 个简单的入门 repo（stage-0）
4. 生成完整教学产物
5. 告诉你"先做 stage-0 动手跑通，再来 stage-1"
```

### 场景 2：Go 工程师想学数据库内核

```
你："教我读 redis"

skill 会：
1. 反向定位 redis 是"数据库内核 / kv 存储"领域 + 工业级复杂度
2. 问你水平（D 级——做过数据库小项目）
3. 判断 D 级 + 工业级 → 推荐 stage-0 轻量版
4. 帮你找一个无框架的数据库内核 beginner repo
5. 生成产物，stage-2 架构按 redis 模块分章
```

### 场景 3：前端 5 年了想学编译器

```
你："我搞前端，最近对编译器好奇，能教我吗？"

skill 会：
1. 用对话式探询帮你定方向（babel？typescript？v8？还是更底层的 LLVM？）
2. 选完方向后帮你找目标 repo 候选
3. 评估你水平（B 级——看过文章但没动手编译器）
4. 推荐 stage-0 跑一个 nano 编译器（如 chibicc 类）
5. 生成完整产物
```

---

## 设计哲学（如果你想了解为什么这样设计）

skill 的方法论基于教育学和信息架构领域的 11 个理论（Feynman 技术、语义波、认知负荷、脚手架、对照学习、C4 模型、Diátaxis 文档框架、认知学徒制、Bloom 分类法、Wayfinding、Constructionism）。详见 [references/theory.md](./references/theory.md)。

但有几个核心原则你需要知道：

1. **动手优先**（Papert 的 Constructionism）：A/B 级小白会被强制走 stage-0 动手——光读代码会非常抽象
2. **AI 不临场写代码**：所有"最简实现"都引用现成、可运行、有社区背书的代码，不让你看 AI 编出来跑不通的版本
3. **AI 不独断挑 repo**：所有推荐 repo 都先经过 WebSearch 验证，再以 3-5 候选给你评估
4. **永远从一条请求的路径开始**：不从 entry.ts / index.ts 这种"配置初始化"开始读
5. **缩写词第一次出现一定解释**：不抛 ADR / ACI / MMR / RAG 这种术语让你猜
6. **对话风格像真人老师**：不堆砌"语义波 + 对照学习 + 脚手架"这种概念名

---

## 项目状态

🚧 **早期阶段，找朋友测试中**。

如果你是被作者请来测试的朋友，请看 [TESTING.md](./TESTING.md)——里面有测试任务清单和反馈表。

已验证的领域：
- ✅ AI Agent（OpenClaw 教学验证过，2-3 个月实战）

待验证的领域（方法论应该适用，但还没真实学生跑过完整流程）：
- ⚠️ Web 框架
- ⚠️ 数据库内核
- ⚠️ OS 内核
- ⚠️ 编译器 / 解释器
- ⚠️ 游戏引擎
- ⚠️ 分布式系统

如果你在某个待验证领域跑通了完整流程（stage-0 → stage-4），欢迎给我提 issue 反馈，让我把该领域升级为"已验证"。

---

## 文档结构

| 文件 | 谁该看 | 干嘛的 |
|------|------|-------|
| [README.md](./README.md) | 所有人 | 你正在看的——介绍 |
| [INSTALL.md](./INSTALL.md) | 想用的人 | 不同 agent runtime 的安装步骤 |
| [TESTING.md](./TESTING.md) | 测试朋友 | 怎么测 + 反馈模板 |
| [SKILL.md](./SKILL.md) | Agent runtime / 高级用户 | skill 主入口，定义 skill 的行为 |
| [references/methodology.md](./references/methodology.md) | 想懂教学方法的人 | 最简对照法 + Feynman + 语义波 + 三层递进 |
| [references/output-structure.md](./references/output-structure.md) | 想懂产物结构的人 | 10 个一级目录每个干嘛的 |
| [references/walkthrough-template.md](./references/walkthrough-template.md) | 写 stage-3 教案的人 | 单篇 walkthrough 的九章模板 |
| [references/walkthrough-examples-multi-domain.md](./references/walkthrough-examples-multi-domain.md) | 想看跨领域示例的人 | Web / DB 两个完整 walkthrough 缩略示例 |
| [references/exercises-template.md](./references/exercises-template.md) | 写题库的人 | 三类检验题模板 |
| [references/checkpoints-and-scenarios.md](./references/checkpoints-and-scenarios.md) | 教学执行人 | 检查点 A/B + 6 种教学场景模板 |
| [references/forbidden-list.md](./references/forbidden-list.md) | 所有人 | 教学红线（绝不允许的事） |
| [references/multi-domain-examples.md](./references/multi-domain-examples.md) | 跨领域用 | 5+ 领域的抽象概念→具体实现映射表 |
| [references/theory.md](./references/theory.md) | 好奇方法论根源的人 | 11 个教育学/IA 理论支撑 |

---

## Agent Skills 标准

这个 skill 严格遵循 [Agent Skills 开放标准](https://agentskills.io/specification)：

- ✅ 标准 `SKILL.md` frontmatter（`name` + `description`）
- ✅ 标准目录结构（SKILL.md + references/）
- ✅ Progressive disclosure（agent 启动时只加载 name+description，匹配到任务才加载完整内容）
- ✅ 跨 runtime 兼容（任何符合标准的 agent 都能用）

发布到任何 skill marketplace（[skills.sh](https://skills.sh) / [SkillsMP](https://skillsmp.com) / [ClawHub](https://clawhub.io) / Anthropic 官方 [github.com/anthropics/skills](https://github.com/anthropics/skills)）都可以。

---

## License

[MIT](./LICENSE) — 自由使用，自由改造，自由分发。

---

## 致谢

- 11 个教育理论支撑来自计算机教育研究领域的几十年积累——感谢 Papert / Maton / Sweller / Vygotsky / Bloom / Bayer / Procida / Brown / Newman / Simon Brown / Morville 等学者
- 这个 skill 由 Claude（Anthropic）协作产出，方法论作者全程参与设计决策
- 感谢 Anthropic 发起并开源 [Agent Skills 标准](https://agentskills.io)，让这个 skill 能跨 30+ agent runtime 复用

如果你觉得有用，star 一下让其他人也能发现。
