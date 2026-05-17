# 教学方法论的理论依据

> repo-learner 的方法论（最简对照法、检查点 A/B、三层递进、Diátaxis 目录结构）不是凭感觉来的，每一条都对应成熟的教育学或信息架构理论。本文档列出 10 个理论依据，每个标明：核心论点 / 出处 / 在 skill 中对应的具体规则。

---

## §1. Feynman 技术（Feynman Technique）

**核心论点**：如果你不能用最简单的语言（不用术语）解释一件事，说明你还没真正理解它。

**出处**：Richard Feynman（诺贝尔物理学奖得主）的学习哲学，被 Cornell Notes / Mortimer Adler 等学习方法体系采纳。

**对应规则**：
- 检查点 A："用一句话不用术语解释"
- 学生说"明白了"不算通过——必须能用自己的话复述并通过 Feynman 检验
- 老师如果讲不清楚某个概念，先回去理解再讲，不能用"简单来说"遮羞

**反例**：背诵定义"ReAct = Reasoning + Acting"≠ 理解。能说"边查资料边写报告，不是先全部查完再写也不是闭着眼睛瞎写"才是。

---

## §2. 语义波（Semantic Waves）

**核心论点**：好的解释必须走完整的波形——从抽象技术（高复杂度）到具体例子（低复杂度）再回到技术概念（带新理解）。只下不上是"下行电梯"，学生会具体例子但无法迁移到其他场景。

**出处**：Karl Maton, "Knowledge-Building" (2013), Legitimation Code Theory。被计算机教育研究（如 SIGCSE）大量引用。

**对应规则**：
- 每个具体例子讲完，立刻 Repack 到术语
- 每个抽象概念讲完，立刻 Unpack 到具体例子
- 禁止"只下不上"——讲完例子不回到术语
- 禁止"只上不下"——只有抽象定义没有例子

**反例**：
- 只下不上：讲了 5 分钟"边查资料边写报告"的例子，从不说"这叫 ReAct" → 学生记住了"边查边写"，但下次看到 "ReAct" 这个词反应不过来
- 只上不下：连续讲 10 分钟 "Reasoning + Acting + Observation 的循环交织提升任务完成质量"，没有任何例子 → 学生认知过载，听不进去

---

## §3. 认知负荷理论（Cognitive Load Theory）

**核心论点**：人的工作记忆容量有限（约 4±1 个 chunk）。一次教太多概念会导致认知过载，学习效率断崖式下降。

**出处**：John Sweller (1988-2010 系列论文)，被 Cambridge / Harvard 等教育学院采纳为基础教学法。

**对应规则**：
- 一次教学最多 3 个核心概念
- 先展示最简版本（低认知负荷），再展示工业级版本（高认知负荷）
- 每 15-20 分钟设检查点，避免认知积压

**反例**：一节课讲 ReAct + Memory + Tools + Routing + Heartbeat 五个概念 → 学生只记住最后一个

---

## §4. 脚手架教学法（Scaffolding / Zone of Proximal Development）

**核心论点**：学生学习时需要"脚手架"——比当前能力略高的支撑物，逐步撤掉直到学生能独立完成。

**出处**：Lev Vygotsky 的 ZPD 理论（1978）；Wood, Bruner, Ross "Scaffolding" (1976) 应用到教学。

**对应规则**：
- 最简实现是脚手架（学生能看懂的 30-100 行）
- 工业级增强是逐步撤掉的过程（最简版 → +error handling → +concurrency → +monitoring）
- 检查点 A/B 验证脚手架是否可以撤掉

**反例**：一上来就让学生读 1600 行的 `attempt.ts` → 没脚手架，超出 ZPD，学生放弃

---

## §5. 对照学习（Comparative Learning / Contrasting Cases）

**核心论点**：通过对比两个相似但不同的案例，激活深度理解。比单独学习一个案例效果显著更好。

**出处**：Schwartz & Bransford "A time for telling" (1998)；Rittle-Johnson 系列研究。

**对应规则**：
- **最简对照法**的核心——最简版 vs repo 版的对照
- 三列对照表（最简 / repo 代码位置 / 说明）
- §1.2 业界三种通用解法对比

**反例**：只讲 repo 怎么实现 ReAct，不对比"最简版本"或"业界其他方案" → 学生不知道这个实现的取舍在哪

---

## §6. C4 模型（C4 Architecture Documentation）

**核心论点**：架构文档应分 4 个层次：System Context → Container → Component → Code。每层独立有意义，逐层 zoom in。

**出处**：Simon Brown, "Software Architecture for Developers" (2013-2025)。

**对应规则**：
- stage-1-foundations：System Context（领域层）
- stage-2-architecture：Container + Component（架构层）
- stage-3-walkthroughs：Code（代码层）
- 严格分层，不允许 stage-2 大量贴代码、stage-3 大量讲架构概念

**反例**：现有 OpenClaw `docs/learning/01-concepts.md` 既讲概念又贴代码——分层不清，学生反复横跳

---

## §7. Diátaxis 框架（Diátaxis Documentation Framework）

**核心论点**：软件文档应分为四种根本不同的类型，因为它们解答**不同性质的问题**：
- **Tutorial**（学习导向，行动型）：教初学者做事
- **How-to**（工作导向，行动型）：教熟手解决问题
- **Reference**（工作导向，认知型）：精确查询事实
- **Explanation**（学习导向，认知型）：理解为什么

每种类型有不同的写作风格、组织方式、读者期望。混合在一起会让所有读者都不满意。

**出处**：Daniele Procida (2014-2024)，被 Django、CNCF、Gatsby、Numpy 等大型开源项目采纳。https://diataxis.fr/

**对应规则**：
- stage-1-foundations / stage-2-architecture = Explanation（理解为什么）
- stage-3-walkthroughs = Tutorial（跟着做）
- stage-4-applied = How-to + Explanation（应用到自己的项目）
- reference / resources = Reference（查事实）

**反例**：现有 OpenClaw `lessons/` + `designs/` 双产物——两者都混了 Explanation 和 Tutorial，60% 内容重叠，学生不知道该读哪个

---

## §8. 认知学徒制（Cognitive Apprenticeship）

**核心论点**：学习复杂技能要走 6 个阶段：Modeling（老师示范）→ Coaching（老师指导）→ Scaffolding（脚手架）→ Articulation（学生说出来）→ Reflection（对比专家）→ Exploration（自主探索）。

**出处**：Collins, Brown, Newman "Cognitive apprenticeship: Teaching the crafts of reading, writing, and mathematics" (1989)。

**对应规则**：
- Modeling = stage-3-walkthroughs（老师带读代码示范）
- Coaching = 实时教学中的检查点 A/B + 场景 D 脱困策略
- Scaffolding = 最简对照法（脚手架式的最简版）
- Articulation = exercises/concept-checks.md（学生用自己的话说）
- Reflection = exercises/transfer.md 的"为什么不适合你项目" 题（对比专家方案与自己方案）
- Exploration = stage-4-applied/mvp-sketch.md（学生自主设计）

**反例**：缺 Articulation 阶段——学生只听课不说话，老师以为学生懂了 → 期末发现根本不懂

---

## §9. Bloom 分类法（Bloom's Taxonomy）

**核心论点**：认知能力分 6 个层级，从低到高：Remember → Understand → Apply → Analyze → Evaluate → Create。教学应按层级递进，每层有不同检验方式。

**出处**：Bloom et al. (1956)，修订版 Anderson & Krathwohl (2001)。

**对应规则**：
- stage-1-foundations：Remember + Understand（记住领域概念、理解术语）
- stage-2-architecture：Understand + Apply（理解 repo 设计、能在新场景应用类似设计）
- stage-3-walkthroughs：Apply + Analyze（能跑通代码、能分析每个设计决策）
- exercises/code-finding：Evaluate（验证理解的准确性）
- stage-4-applied：Create（创造自己的方案）

**反例**：直接让学生 Create（"设计 Mnemos 的核心 schema"）跳过 Remember → 学生没记住领域概念，设计不出合理方案

---

## §10. 高质量技术博客结构

**核心论点**：好的技术博客都遵循渐进复杂度——从小例子工作到完整案例。问题开头，不用答案开头。

**出处**：观察 Anthropic 工程博客 / Google AI Blog / Stripe Engineering / Vercel Engineering / Apple ML Research 等高质量内容，归纳的共性模式。

**对应规则**：
- walkthrough §0 通用视角：问题开头，引用权威材料
- walkthrough §1：反向论证激发好奇心
- walkthrough §4.1：最简实现（小例子）
- walkthrough §4.4：工业级增强（完整案例）
- 全文用 file:line 引用，可验证

**反例**：从"我们的系统支持 X / Y / Z"开头 → 读者不知道为什么要关心，直接关闭

---

## §11. Wayfinding（Information Architecture）

**核心论点**：信息架构里的"寻路"原则——每个页面要告诉读者：你在哪（You are here）、能去哪（Where can I go）、怎么回（How do I get back）。

**出处**：Peter Morville & Louis Rosenfeld, "Information Architecture for the World Wide Web" (1998-2015)。

**对应规则**：
- 每个目录有 README.md 显式标"You are here"
- stage-1/2/3/4 序号暗示路径
- walkthrough §6 链接到 exercises，§7 链接到 stage-4-applied
- 横切目录（reference / exercises / resources）任意阶段都可进入

**反例**：现有 OpenClaw `lessons/` 没有 README，学生不知道该从 00 还是 01 开始

---

## §12. Constructionism / 建造主义（V2 新增）

**核心论点**：通过**建造**（building）而非被动接受信息来学习。学习者亲手做出一个能跑的东西，比听 10 节课更有效。这条理论是 stage-0 存在的根本原因。

**出处**：Seymour Papert，"Mindstorms: Children, Computers, and Powerful Ideas" (1980) + "Constructionism" (1991)。MIT Media Lab 创始人。Papert 是 Logo 编程语言之父，相信学习是"在脑外构建可分享物品"的过程，而不只是"在脑内建立知识"。

**对应规则**：
- **stage-0-fundamentals/ 强制存在**（学生 A/B/C/D 级时）—— 先动手 clone 跑通一个 beginner repo，再读 stage-1 理论
- **stage-0 优先于 stage-1**：Papert 反对"先讲理论再做实验"的传统教学顺序——他主张"先建造再反思"
- **graduation-check.md 含"能改 + 能扩展"题**：单纯跑通 = 不够；必须能改 system prompt、加新 tool，才算真懂
- **stage-3 §4.1 引用 stage-0 代码**：因为学生**亲手跑过**这段代码，认知锚点最强（"还记得你跑过的那个 act() 吗？"）
- **场景 F**（伴学 stage-0）禁止老师 5 分钟内给答案——挣扎-自救循环是 Papert 强调的"productive failure"

**反例**（跨领域）：
- AI Agent：直接让学生读 OpenClaw 的 `attempt.ts`（1600+ 行工业代码），跳过 stage-0 动手 → 学生没有"自己写过 act()"的肌肉记忆，1600 行立刻认知过载
- Web 框架：直接让学生读 Express 的 application.js + router 几千行 → 学生没自己写过中间件，看到 `next()` 链各种 edge case 时无法定位"原型场景"
- 数据库：直接让学生读 SQLite 的 btree.c（数万行）→ 学生没自己实现过最简 cursor，看到 page 切换的复杂分支立刻迷失
- OS：直接让学生读 Linux scheduler → 学生没自己写过最简轮转调度，看到 CFS 红黑树的优化无从理解"为什么需要"

**与认知学徒制的区别**：
- Cognitive Apprenticeship 强调"老师示范 → 学生模仿"
- Constructionism 强调"学生先自己建造 → 老师只是支持者"
- learn-via-repo 同时用两者：stage-0 = Constructionism；stage-3 = Cognitive Apprenticeship

**关键引语**（Papert）：
> "Better learning will not come from finding better ways for the teacher to instruct, but from giving the learner better opportunities to construct."

这正是 stage-0 的设计哲学。

---

## §13. 经验主导的最重要一条信念

> "更多的代码行数 = 把同样的事做得更健壮、更安全、更灵活。
> 不是更多的新概念。
> 理解了 80 行的骨架，你就理解了 1600 行的意图。"

这条不是来自论文，是 OpenClaw 教学两个月的实战经验。每次面对"我看不懂这段 1600 行的代码"时都先讲这句话——学生立刻有了信心。

理论依据可以推演这条经验：

- **认知负荷理论**：1600 行的工业代码认知负荷远超 ZPD，必须先降到 80 行的最简版
- **对照学习**：80 行 vs 1600 行的对照激活深度理解
- **脚手架教学法**：最简版是脚手架，工业级是撤掉脚手架后的真实

---

## §14. 这些理论如何选择性应用

不是每节课都要应用全部理论。按场景选：

| 场景 | 最关键的理论 |
|------|-------------|
| **stage-0 动手前置** | **Constructionism（Papert）** + 认知学徒制 Modeling |
| 概念引入（stage-1） | Feynman + 语义波 + 外部材料 |
| 概念检验 | Feynman + Articulation |
| 代码讲解 | 脚手架 + 对照学习 + 认知负荷 |
| 代码验证 | Bloom Evaluate 层 + file:line 定位题 |
| 学生迁移 | Cognitive Apprenticeship Exploration |
| 文档组织 | Diátaxis + C4 + Wayfinding |
| 全局节奏 | 认知负荷（≤3 概念）+ 检查点（≤20 分钟） |

每个理论都是"在某个时刻最有用"，不是"无脑全部叠加"。

---

## §15. 延伸阅读

- Feynman 技术：[The Feynman Technique](https://fs.blog/feynman-technique/)
- 语义波：Karl Maton "Knowledge-Building" (2013)
- 认知负荷：John Sweller "Cognitive Load Theory" (2011)
- ZPD/Scaffolding：Wood, Bruner, Ross (1976)
- 对照学习：Schwartz & Bransford "A time for telling" (1998)
- C4 模型：[c4model.com](https://c4model.com/)
- Diátaxis：[diataxis.fr](https://diataxis.fr/)
- Cognitive Apprenticeship：Collins, Brown, Newman (1989)
- Bloom Taxonomy：Anderson & Krathwohl (2001) revised
- Information Architecture：Morville & Rosenfeld (2015)
- **Constructionism**：Seymour Papert "Mindstorms" (1980) + "Constructionism" (1991)
