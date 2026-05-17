# 禁忌清单（绝不允许）

> 教学红线。skill 在生成产物和实际教学时，**任何情况下不可越过**本清单。每条禁忌都来自实战中失败的教训。

---

## §1. 概念禁忌

### ❌ 在没有展示最简实现的情况下，直接展示 repo 的复杂代码

**为什么禁止**：学生看不见骨架，只看到一堆类型签名 / 错误处理 / 并发锁，会觉得"复杂 = 难，我学不会"。

**正确做法**：先写 30-100 行最简版，让学生看到骨架；再展示 repo 的工业级版本；最后解释"多出来的是为了更健壮，不是更多概念"。

---

### ❌ 描述一个概念超过 3 句话，不给对应的代码或例子

**为什么禁止**：概念抽象 + 没有锚点 = 学生背诵但不理解。

**正确做法**：每个概念 1 句话定义 + 1 个具体例子（Unpack）+ 1 个回到术语的总结（Repack）。

---

### ❌ 说"代码很复杂但先别管细节"

**为什么禁止**：这句话承认"我没办法把复杂讲清楚"，是教学失败的遮羞布。

**正确做法**：必须给出足够的"骨架"让复杂度合理化。如果真的复杂，用最简对照法五步把复杂拆开。如果还是讲不清楚，说明你自己还没真正理解——回去理解再讲。

---

## §2. 代码禁忌

### ❌ 展示代码不给 file:line 引用

**为什么禁止**：学生无法回到 repo 验证。所有代码引用必须能精确定位。

**正确做法**：每段 repo 代码必须有 `// {file}:{line}` 注释，或文字中写 `attempt.ts:1627` 这种 file:line 格式。

---

### ❌ 展示超过 50 行代码而不用注释标注重点行

**为什么禁止**：学生不知道关注什么。50 行没标注的代码 = 50 行噪音。

**正确做法**：长代码段必须用 `// 关键行：` 或 `// 对应最简版的：` 注释标 3-5 个重点行，其余行可以略过。

---

### ❌ 跳过"工业级增强"解释

**为什么禁止**：学生会觉得 repo 的代码是神秘的、复杂的、自己写不出来的。失去信心。

**正确做法**：每展示一段比最简版复杂的 repo 代码，立刻解释多出的部分是为什么（并发 / 错误处理 / 性能 / 类型安全等）。**每条多出来的都有"为什么"**。

---

### ❌ 从 `entry.ts` 或 `index.ts` 开始讲

**为什么禁止**：初始化代码是噪音最多的地方——一堆模块导入、配置加载、依赖注入，跟"这个 repo 在做什么"无关。学生从这里开始会迷失。

**正确做法**：从"一条消息的路径"开始。找到用户输入的入口（如 HTTP handler、CLI 命令），跟着数据流走。

---

## §3. 节奏禁忌

### ❌ 超过 20 分钟不检验理解

**为什么禁止**：认知负荷在 20 分钟达到峰值。不检验，学生只是被动接受信息。

**正确做法**：每 15-20 分钟设一个检查点。要么是 Feynman 检验，要么是 file:line 定位，要么是"你来复述刚才那段"。

---

### ❌ 学生说"明白了"就继续

**为什么禁止**："明白了"是社交回应，不是理解证据。学生为了不让老师失望，会假装明白。

**正确做法**：永远用 Feynman 检验——"用一句话不用术语告诉我刚才那个东西解决了什么问题"。说不出来 = 没明白。

---

### ❌ 一次性讲超过 3 个核心概念

**为什么禁止**：认知负荷理论（Sweller）证明：人的工作记忆一次只能持有 4±1 个 chunk。超过 3 个就是认知过载。

**正确做法**：一次教学最多 3 个核心概念。第 4 个出现时，要么砍掉，要么拆成下一节课。

---

### ❌ 讲完具体例子不回到技术术语（语义波只下不上）

**为什么禁止**：学生会具体例子但无法迁移到其他场景。下了"具体例子"的电梯，没回到"技术术语"的楼层。

**正确做法**：每个具体例子讲完，立刻 Repack——"用 {术语 1} {术语 2} 重新表达刚才那个例子"。

---

### ❌ 讲代码时跳过"高层级代码框架"直接进入最简实现

**为什么禁止**：地图先于骨架。学生不知道这段代码在 repo 的哪个位置、跟周围怎么连，看到的最简实现也是孤立的。

**正确做法**：先 Step 0 代码地图（3-5 个核心文件的调用链 file:line 路径图），再 Step 1 最简实现。

---

### ❌ 讲概念不引入外部高质量材料

**为什么禁止**：闭门造车的解释往往不到位，错过了已经被论文/权威博客一句话击穿的核心洞察。

**正确做法**：每个核心概念，主动搜索 1 篇 Tier 1 权威材料（论文 / 大厂工程博客 / 领域权威综述），引用它的核心实验数据或图表，立刻 Repack 到目标 repo。

---

## §4. 风格禁忌

### ❌ 用"简单来说"、"基本上"这样的模糊措辞

**为什么禁止**：这些词是"我没想清楚怎么准确表达"的遮羞布。学生听到这些词会自动降低信任度。

**正确做法**：用准确的措辞。如果想不出准确措辞，说明你自己还没想清楚——回去想清楚再讲。

---

### ❌ 说"你可以自己去看代码"

**为什么禁止**：这是"我不教了，你自己摸索吧"。如果学生能自己看，他不会找你教。

**正确做法**：必须给出具体的 file:line 和读代码步骤（分轮次，每轮一个目标 + 时间估计）。

---

### ❌ 在没有对照表的情况下声称"repo 实现了 X 概念"

**为什么禁止**：没有对照表 = 学生没法验证你说的是真的。

**正确做法**：每个"repo 实现了 X 概念"的声明，必须配三列对照表（通用概念 / repo 代码位置 / 说明）。

---

## §5. Beginner repo 选材禁忌（V2 新增）

`stage-0-fundamentals/` 的 beginner repo 选材有专门的硬约束。Phase 2C 搜索 + 用户评估时严格执行。

### ❌ 推荐掩盖该领域核心控制流骨架的成熟框架抽象

**抽象原则**（跨领域统一）：任何把该领域的**核心控制流**封装到"几行 API 调用"背后的成熟框架都不合适。学生学到的是框架 API，不是底层原理。

**判断方法**（跨领域统一）：打开 repo README 的核心示例代码，能否看见**该领域的骨架元素**？

每个领域的骨架元素不同，详见 `multi-domain-examples.md` §1 "关键骨架元素"列：

- **AI Agent**：`messages.append({role, content})` + `if stop_reason == "tool_use": execute_tool(...)` + ReAct 三元组
- **Web 框架**：`next(err)` 链调用 + `req` / `res` 对象传递 + 中间件签名
- **数据库内核**：Btree cursor 操作 + opcode dispatch loop + 行/页 IO
- **编译器/解释器**：TokenScanner + ASTNode 构造 + Visitor 模式
- **OS 内核**：trap frame 保存 + 调度队列 + page table 切换
- **游戏引擎**：game loop tick + ECS 组件查询 + 渲染队列
- **分布式系统**：log entry append + AppendEntries RPC + commit index 推进

**看得见 = 合格**；**看不见**（被 `agent.run()` / `Agent(...).execute(...)` / `framework.handle(req)` / `engine.query(sql)` 等一行 API 替代）= 不合格。

**已知不合格框架列表（按领域分类，非穷举）**——遇到新框架按上面"判断方法"判断：

#### AI Agent 领域
- LangChain 系列：`langchain` / `langchain_core` / `langchain_anthropic` / `langchain_openai`
- LangGraph：`langgraph`
- LlamaIndex：`llamaindex` / `llama_index`
- CrewAI：`crewai`
- AutoGen：`autogen` / `autogen_agentchat` / `autogen_core`
- Microsoft：`semantic_kernel` / `microsoft-agent-framework` / `azure-ai-foundry-agent`
- OpenAI：`agents`（OpenAI Agents SDK）/ `openai-agents`
- HuggingFace：`smolagents`
- Haystack：`haystack`

#### Web 框架领域（不是说框架本身不好，是 stage-0 不应该用它们学骨架）
- 后端：`nestjs` / `hapi` / `adonisjs` / `spring` / `spring-boot` / `django`（高层框架）/ `rails` / `laravel`
- 前端：`react`（要学组件原理 → 用 mini-react）/ `vue`（要学 reactivity → 用 mini-vue）/ `angular`（高度抽象）
- 全栈：`next.js` / `nuxt.js` / `remix`（路由+SSR 都封装了）

#### 数据库领域
- ORM 类：`sqlalchemy` / `typeorm` / `prisma` / `hibernate` / `gorm` / `activerecord`
- 高级查询封装：`mongoose` / `sequelize`
- 注：学数据库**内核** → beginner repo 不能是 ORM；学 ORM 设计 → beginner repo 不能基于现成 ORM

#### 编译器/解释器领域
- `babel`（高度封装的现代版，不适合学编译器原理）/ `swc`
- TypeScript compiler（黑盒）/ `tsc`
- LLVM 高级 binding（如 `inkwell`）—— LLVM C++ 内核可以学，但 binding 把它当黑盒

#### OS 内核领域
- `docker` / `k8s`（不是 OS 内核，是高层调度框架）
- `systemd`（启动框架，不是内核）
- 容器 runtime 如 `runc`（基于内核，不是内核本身）

#### 游戏引擎领域
- `unity` / `unreal-engine` / `godot`（引擎黑盒，看不见 game loop / ECS / 渲染管线）
- `phaser` / `pixi.js`（前端游戏框架，封装了渲染）

#### 分布式系统领域
- `k8s controller-runtime`（封装了 reconcile loop）
- `spring-cloud` / `consul-template`
- 服务网格客户端（如 `istio-client`）

**为什么禁止**：详见上面"判断方法"——这些框架抽象掩盖了该领域的核心控制流骨架。学生学到 framework API 而非领域原理，进入 stage-3 走读复杂工业代码时仍然抽象。

**例外**：如果学生**已经熟悉**该框架，并且**目标 repo 就是这个框架本身**（如学 LangChain → 目标 repo 是 langchain），那么 stage-0 应该选**框架内部某个模块的简化实现**，不是基于框架的应用 repo。

### ❌ AI 凭印象指认某个 repo "合格"

错误示例（v2 升级期实际发生过）：
- 把 `microsoft/ai-agents-for-beginners` 当合格示例（实际它基于 Microsoft Agent Framework + Azure AI Foundry）
- 把 `anthropic-cookbook` 当 stage-0 教学主线（实际它是 cookbook 不是 curriculum）

**正确做法**：Phase 2C 用 WebSearch 搜出候选 → 用 WebFetch 验证 README 没有上述框架的 import → 把 3-5 个候选**给用户**评估 → 用户确认后才能写入 `stage-0-fundamentals/recommended-repos.md`。**AI 不独断指认**。

### ❌ 只是"权威机构出品"就当教学

权威性（star 数、大厂背书）不等于"适合教学"。教学的硬指标是：
- 递进结构（先教 A 再教 B）
- 概念铺垫（每个新概念前有 1 段铺垫）
- 最简对照（先展示骨架再加复杂度）

反例：anthropic-cookbook（43.1k stars + Anthropic 官方）是 **cookbook** 不是 **curriculum**——14 个独立 notebook 没递进，每个 notebook 直接上完整版没铺垫。**作为 reference Tier 1 完美，作为 stage-0 教学主线不合格**。

适用判断：
- ✅ 教学型 stage-0：递进 curriculum / step-by-step tutorial / 配套博文/视频
- ❌ 非教学型（归入 reference/）：cookbook / quickstart / production demo

---

## §5b. 元教训（V2 升级期总结的 3 条）

这些教训来自 v2 升级过程中实际犯过的错误，AI 必须内化避免再犯。

### 元教训 1：LLM provider 类型不是排除标准

错误：把"必须 cloud API（OpenAI/Anthropic），不接受本地 LLM（Ollama/GGUF）"当硬约束。

为什么错：从"理解 agent 原理"的角度，`ollama.chat()` 和 `openai.chat.completions.create()` **骨架完全一样**——都是"发 prompt 收 response"。学生学的是 agent loop 骨架，不是 LLM provider。装 Ollama 也就 5-10 分钟。

正确做法：把 LLM provider 从硬约束**降级为 Phase 1 偏好问题**：
- "你愿意装 Ollama + 下 GGUF 模型，还是想用 API key 立刻跑起来？"
- 两条路径都能学到 agent 原理，让学生选

被错误排除而应该升档的强候选：
- rasbt/mini-coding-agent（850 stars + Sebastian Raschka 大牛 + 本地 Ollama）
- pguso/agents-from-scratch (Python, 703 stars + 本地 GGUF)

### 元教训 2：cookbook ≠ curriculum

错误：把"权威机构出品 + 高 star + 内容相关"等同于"适合 stage-0 教学主线"。

为什么错：anthropic-cookbook (43.1k stars) 是 14 个**独立** notebook，每个解决一个具体问题，**没有递进结构**、**没有概念铺垫**、**没有最简对照**。学生进去会迷失："我先点哪个？"

正确做法：明确区分两种文档：
- **教学型**（curriculum / step-by-step）→ stage-0/1/2/3 主线
- **参考型**（cookbook / quickstart / demo）→ reference/ + stage-3 §4.1 引用源 + resources/ Tier 1

判断标准：打开 README，问"作者有没有说'先看第一课，再看第二课'？"

### 元教训 3：AI 不能独断挑选 repo

错误：AI 凭训练数据印象指认"X repo 是合格的权威最简实现"。

为什么错：训练数据可能过时；AI 可能没真读过该 repo 的 README；某个 repo 可能从无框架转向用框架但 AI 不知道。

实际案例：
- v2 升级初期，AI 在 methodology.md 里写"以 microsoft/ai-agents-for-beginners 为例"作为合格示例 → 用户指正：它基于 Semantic Kernel/AutoGen，不合格

正确做法：Phase 2C 必须**真实执行**：
1. WebSearch 搜出 5-10 个候选
2. WebFetch 每个候选的 README，验证 import 列表
3. 把候选 + 评估表给用户
4. 用户评估、确认或否决后才能写入 `stage-0-fundamentals/`

`SKILL.md` Phase 2C 必须明确这个交互步骤——不能省略。

---

## §6. 元禁忌（关于禁忌的禁忌）

### ❌ 用"用户偏好"来绕开禁忌清单

**为什么禁止**：禁忌清单是方法论的硬约束，不是风格偏好。

学生可以说"我喜欢中文/英文"、"我喜欢更短的课"、"我不要类比"——这些是风格偏好，可以接受。

学生**不能**说："我已经懂了，跳过检查点 A 吧"——这是用户在用社交压力让老师降低标准，会导致教学失败。老师必须坚持执行检查点。

---

### ❌ 用"这次特殊"来豁免禁忌

**为什么禁止**：每次都"特殊"，禁忌清单就变成了装饰品。

如果真的需要破例，必须显式记录在 `meta/progress.md`，并标注"破例的代价"——下次教学时回看，确认这次破例是否合理。

---

## §7. 自检清单

每次生成 walkthrough 或开展教学后，对照本清单自检：

- [ ] 没有在缺少最简实现的情况下展示 repo 代码
- [ ] 每个概念都有 1 句定义 + 具体例子 + 术语 Repack
- [ ] 所有代码引用都带 file:line
- [ ] 长代码段都有 ≤5 个重点行标注
- [ ] 每段 repo 代码都有"工业级增强为什么"解释
- [ ] 没有从 entry.ts/index.ts 开始
- [ ] 教学过程中每 ≤20 分钟有一个检查点
- [ ] 学生说"明白了"都做了 Feynman 检验
- [ ] 一次教学的核心概念 ≤3 个
- [ ] 每个具体例子都做了术语 Repack
- [ ] 讲代码前展示了代码地图（Step 0）
- [ ] 每个核心概念都引入了 1 篇外部 Tier 1 材料
- [ ] 没有用"简单来说"、"基本上"等模糊措辞
- [ ] 没有让学生"自己去看代码"
- [ ] 每个"repo 实现了 X"的声明都有对照表

### V2 新增检查项（抽象原则）

- [ ] stage-0 推荐 repo 经过 Phase 2C 真实搜索（WebSearch + WebFetch 验证 README/imports），不是 AI 凭训练数据印象指认
- [ ] stage-0 推荐 repo 由用户从 3-5 个候选中评估确认，不是 AI 独断挑选
- [ ] stage-0 推荐 repo 从**第一性原理**出发——只用底层 API（无论远程托管推理还是本地推理）+ 标准库，**不**被任何掩盖 agent loop 骨架的框架抽象覆盖
- [ ] 教学材料的判定基于"**教学结构**"（递进 + 概念铺垫 + 最简对照），**不**基于权威性 / star / 实现完整度等"易混淆指标"
- [ ] **参考型资源**（cookbook / quickstart / API SDK 文档 / production demo）归入 `reference/` 或 stage-3 §4.1 引用源，**不**作为 stage-0/1/2 教学主线
- [ ] walkthrough §4.1 必有"引用源 + 摘要双区块"，引用的是真实存在、可运行、有社区/作者背书的代码，**不是** AI 临场发挥
- [ ] §4.1 的引用源带精确 file:line 和"为什么是权威最简实现"说明
