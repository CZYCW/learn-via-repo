# learn-via-repo 教学方法论

> 这是 learn-via-repo skill 的核心方法论。skill 在生成教学产物以及实际教学时，每一步都要遵守本文档。
>
> 方法论从 `~/Desktop/projects/openclaw/docs/learning/TEACHING-STYLE.md` 抽象而来，已在 AI Agent 领域教学（OpenClaw）中验证有效。**V3 泛化到任何软件工程领域**——本文档示例以 AI Agent 为主，跨领域类比锚点见 `multi-domain-examples.md` §1（含 Web 框架 / 数据库内核 / OS 内核 / 编译器 / 游戏引擎 / 分布式系统 等领域的对应映射）。

---

## §1. 教学哲学

**核心目标**：让学生能**独立追踪代码**，而不只是"听懂了老师讲的"。

判断教学是否成功的 3 个标准——学生能否独立完成：

1. 打开目标 repo 的一个陌生模块文件，定位到核心逻辑
2. 用自己的话解释"这段代码在干嘛，为什么这样写"
3. 把代码行为和已知的领域概念对应起来

**根本禁忌**：让学生感到"听了但还是看不懂代码"。这是教学失败，不是学生学习能力不足。

---

## §2. 概念与原理教学哲学

概念和原理是整套教学体系的地基——地基不稳，后面的代码理解全部架空。

### §2.1 Feynman 技术

**核心信念**：如果你不能用最简单的语言解释一件事，说明你还没真正理解它。

教学时的 3 条操作规则：

1. **不教定义，教"为什么这个问题存在"**
   - 错误方式：`ReAct = Reasoning + Acting 的结合`
   - 正确方式：`如果 LLM 只推理不行动，会发生什么？（幻觉）如果只行动不推理，会怎样？（盲目）ReAct 是解决这个矛盾的最小方案。`

2. **不接受"我觉得明白了"——用 Feynman 检验**
   - 检验方法："用一句话，不用任何术语，告诉我这个东西解决了什么问题。"
   - 学生说不清楚 → 找到了知识盲点 → 这里是重点突破的地方
   - 学生说清楚了 → 带他用术语重新表达 → 概念才算真正内化

3. **宁慢勿快**
   - 宁可花 2 倍时间把一个概念讲透，不要快速刷过 5 个概念
   - 认知过载的学生会假装理解——这比"我不懂"更危险

### §2.2 外部资料驱动

概念和原理层不闭门造车——有时候一篇论文的一张图比 1000 字解释更有力。

**操作规则**：
- 讲每个核心概念时，主动搜索"最直接回答这个 Why"的权威材料
- 不是"关于这个主题的材料"，而是"能一句话击穿核心洞察的材料"
- 引入材料后，立刻映射到目标 repo 的实现（不能让外部知识成为孤岛）

**示例**（以 AI Agent 领域为例）：

| 概念 | 应引入的材料 | 核心洞察 |
|------|------------|---------|
| ReAct 为什么需要 Reason + Act 组合 | ReAct 论文（Yao 2022）实验数据 | 纯 CoT 幻觉率高 / 纯 Act 推理弱 |
| 记忆分层为什么是三层 | Lilian Weng 认知科学框架 | 感官/工作/长期记忆的生物学类比 |
| 为什么要用图记忆 | Mem0 + Zep 论文 | 向量检索的关系推理盲区 |
| Tool 设计为什么要 poka-yoke | Anthropic ACI 文章 | 工具 = Agent 的认知界面，与 HCI 同等重要 |

### §2.3 语义波（Semantic Waves）

来源：计算机教育研究（Maton 2013，Legitimation Code Theory）。

好的解释走完整的波形：

```
高抽象度                    技术术语
（低具体度）              （高复杂度）
     │                          ↑
     │   "ReAct = 推理+行动"    │ ← Repacking（打包回去）
     │                          │
     ▼   具体例子                │
（高具体度）              （低复杂度）
  "就像你边查资料边写报告，
   不是先查完所有资料再写"
```

**跨领域类比**（其他领域同样适用，AI Agent 只是示例之一）：
- Web 框架："`app.use((req,res,next)=>...)` 中间件" Unpack 为"工厂流水线上每个工位都对包裹做点什么再传给下一个"；Repack 回到"洋葱模型 / 责任链"
- 数据库：B-tree 节点分裂 Unpack 为"书架满了，把书分到两层，加一个目录指针"；Repack 回"B-tree balance"
- 编译器：词法分析 Unpack 为"把一句话拆成单个汉字"；Repack 回"tokenization"

**两个禁止错误**：

- ❌ **只下不上**（"下行电梯"）：讲了很多具体例子，从没回到技术术语 → 学生无法迁移到其他场景
- ❌ **只上不下**（"高空停留"）：全是抽象定义和架构图，没有具体例子 → 认知过载，听不进去

**正确做法**：每个知识点都要明确地 Unpack（把术语解包成具体例子）然后 Repack（把例子重新打包成术语）。

**检验**："学生现在能用专业术语描述刚才的具体例子吗？"

---

## §3. 三层递进结构

每个知识点必须按三层顺序讲解，绝不跳层：

```
层一：为什么？（全景层）
  - 没有这个东西会怎样？（反向论证）
  - 在该技术领域生态中，这个问题的通用解法是什么？
  - 目标 repo 选择了什么方案，为什么？

层二：是什么？（架构层）
  - 核心概念定义（一句话）
  - 组件关系图（文字或 ASCII / mermaid）
  - 关键设计决策（最多 3 个，ADR 格式：Context → Decision → Consequence）

层三：怎么实现？（实现层）
  ⓪ 先：高层级代码框架（代码地图）
  ① 再：最简实现（骨架）
  ② 后：目标 repo 对应代码（对照）
  ③ 解释：工业级增强（差异）
```

**绝不允许**：跳过层一层二直接进入层三，或在没有最简实现铺垫的情况下展示 repo 的复杂代码。

---

## §4. 最简对照法（核心方法）

这是本教学体系最重要的方法。所有 stage-3-walkthroughs/ 教案必须包含完整的最简对照法五步。

### §4.0 Step 0：高层级代码框架（代码地图）

先给学生一张地图，再让他们走路。

- 列出这个功能涉及的核心文件（3-5 个）
- 画出主要函数调用链（不是内部逻辑，是 A 调用 B 调用 C 的关系）
- 说明数据从哪里进、从哪里出
- 格式：文字路径图，每个节点带 `file.ts:line`

目的：让学生在看最简版骨架之前，先知道"真实代码分布在哪些文件、大致顺序是什么"，避免最简版概念和真实代码文件之间断层。

### §4.1 Step 1：找权威最简实现（V2 升级，三级优先级）

> **重要变更（V2）**：旧方法（AI 临场写 30-100 行）已废弃。原因：AI 临场代码看着像，跑起来不一定通，跟权威实现也有差距，学生还要去验证。新方法：**所有"最简实现"必须来自现成、可运行、有社区背书的代码**，按下面三级优先级查找。

#### 三级优先级

| 优先级 | 来源 | 何时用 |
|--------|------|--------|
| 1 | **stage-0 学过的 beginner repo 代码** | 首选。学生已经跑过、看过、最熟悉。引用形式：`stage-0-fundamentals/{repo-name}/{path}:{line}` |
| 2 | **领域权威的"简洁实现型"repo**（用户评估认可过——AI 不独断指认） | 备选。**合格类型**：作者出名的 educational repo（大牛 / 课程作者出品）、以"几百行教学代码"为目标的简洁实现 repo（如 `nano-*` / `mini-*` / `tiny-*` 命名风格）、单 notebook 形式的完整教学示例。**不合格类型**：cookbook / API SDK 文档 / production demo——这些是参考资料而非递进教学（详见 `forbidden-list.md` §5b 元教训 2）。引用形式：`{owner}/{repo}/{path}:{line}` |
| 3 | **AI 简化版（仅当 1、2 都没有）** | 兜底。AI 基于 1、2 中的某个权威实现做注释/摘要版，**必须**标注 `"基于 X 简化，仅供讲解，未独立验证运行"`。绝不"凭空写一个"。 |

#### 选材标准（用于优先级 1 和 2）

- ✅ **第一性原理**：直接调用底层 API（任何底层 provider）+ 标准库；该领域的**核心控制流骨架可见**（具体骨架元素按领域不同——AI Agent 是 `messages.append + tool_use 分发`，Web 框架是 `next() 链`，数据库是 `cursor + opcode loop`，详见 `multi-domain-examples.md` §1）
- ✅ **配套教学内容**：完整 README / 配套博文 / 视频 / Issue 解答
- ✅ **权威背书**：Star ≥ 1k 或大厂 / 大牛 / 知名课程出品
- ✅ **维护活跃**：最近 6 个月有提交
- ❌ **掩盖核心控制流骨架的成熟框架抽象**——把该领域的核心逻辑封装成几行 API 的框架（不同领域有不同的"封装犯罪嫌疑人"——AI Agent 领域是 langchain 系，Web 领域是 NestJS / Spring，数据库领域是 sqlalchemy / typeorm 等。详见 `forbidden-list.md` §5 的判断方法 + 按领域分类的已知不合格框架列表）
- ❌ 只是文章合集没有可运行代码

详见 `forbidden-list.md` §5。

#### 写法标准

引用源代码时，**展示原始代码** + 一段 5-10 行的**伪代码摘要**：

```markdown
**最简实现来源**（**实际推荐 repo 由 Phase 2C 网络搜索 + 用户评估确认**，下面是 OpenClaw 教学场景的真实示例）：
  Leonie Monigatti notebook (Anthropic API, 4-component progression)
**文件位置**：`iamleonie/website/blob/main/blog/ai-agent-from-scratch-in-python.ipynb` Section 4
**为什么是权威最简实现**：作者 ML engineer 背景；4 组件清晰递进（LLM/memory/tool/agent loop）；
  全程无框架（直接调 anthropic SDK）；与多数现代 AI Agent repo 同 API 体系。

---

**5-10 行伪代码摘要**（仅辅助理解骨架，跑代码请回到上面的真实文件）：

```python
# 改编自 Leonie notebook Section 4，剥离 error handling/streaming，保留 ReAct 三元组骨架
def act():
    """ReAct 循环核心：直到 LLM 不再生成 tool_use"""
    response = call_llm(messages, tools)
    if response.stop_reason == "tool_use":
        result = execute_tool(...)
        messages.append(result)
        return act()  # 递归
    return response.text  # 完成
```

> **跨领域类比**：上面是 AI Agent 领域的"最简骨架"示例。其他领域同样有"几行代码看清核心控制流"的最简版：
> - Web 框架：3-5 行就能看清 `middleware → next() → handler` 链
> - 数据库：5-10 行 cursor 操作就能看清 Btree 遍历
> - 编译器：10 行 tokenize + AST 构造就能看清解析骨架
> - OS 内核：trap 入口 + 调度队列也能用 20 行伪代码表达
>
> 详见 `multi-domain-examples.md` §1 "关键骨架元素" 列——每个领域都有"几行代码看到本质"的可能。
```

**为什么这样设计**：
- 学生**先看到真实可跑的代码**（权威 repo 的 file:line）
- AI 写的 5-10 行只是"翻译"成更紧凑的形式，方便老师讲骨架——明确标注"这是摘要不是运行版"
- 学生想跑、想改、想验证——回到真实 repo

#### 反例：哪些是 v2 禁止的

```
❌ 在 walkthrough §4.1 直接贴 80 行 AI 临场写的 Python，没有 "来源"
   后果：跑不通 / 跟权威实现有差距 / 学生不知道去哪验证

❌ 引用了某个 repo 但不给精确 file:line，只说 "类似于 X 的实现"
   后果：学生找不到对应位置

❌ 引用了基于 langchain 的 beginner repo
   后果：学生学到的是框架 API，不是骨架原理
```

### §4.2 Step 2：展示目标 repo 对应代码（file:line + 注释）

- 给出 `file.ts:line` 的精确引用
- 用注释标注"对应权威最简版的哪一行/哪个函数"

```typescript
// 以 OpenClaw 为例（最简实现来源：{stage-0 推荐 repo}/path/to/react-loop.py:42-78
//  —— 推荐 repo 由 Phase 2C 网络搜索 + 用户评估确认后填入，AI 不独断指认）：

// attempt.ts:991
// 对应权威最简版的：messages = []（{stage-0}/react-loop.py:15）
sessionManager = guardSessionManager(SessionManager.open(params.sessionFile), { ... });

// attempt.ts:1627
// 对应权威最简版的：act() 递归调用入口（{stage-0}/react-loop.py:60）
await abortable(activeSession.prompt(effectivePrompt));
```

> **方法论铁律（V2 补充）**：AI 不能凭印象指认某个 repo 是"合格的权威最简实现"。必须 Phase 2C 真实搜索、用 WebFetch 验证 README 没有 `from langchain import ...` 等框架引入、把 3-5 个候选给用户评估、用户确认后才能写入 §4.1 / §4.2 的引用。详见 `forbidden-list.md` §5。

### §4.3 Step 3：写三列对照表

始终使用三列：最简版本 / repo 代码位置 / 说明

**示例（以 AI Agent 领域 / OpenClaw 为目标 repo）**：

```markdown
| 最简版本 | repo 代码位置 | 说明 |
|---------|-------------|------|
| `messages = []` | `SessionManager.open(jsonl)` in `attempt.ts:991` | 内存列表 → 磁盘持久化 |
| `call_llm()` | `activeSession.prompt()` in `attempt.ts:1627` | 直接调用 → 封装在 pi-agent-core |
| `execute_tool()` | `tool.execute()` via pi-agent-core | 简单分发 → 类型检查 + 权限 + 超时 |
```

**跨领域示例**（其他领域同样套用三列对照表）：

| 领域 | 最简版本（示例） | 目标 repo 代码位置（示例） | 说明 |
|------|------|----------|------|
| Web 框架 | `function handler(req, res) { res.send('hi') }` | `app.use('/x', fn)` in `application.js:280` | 直接处理 → 中间件链 + 路由匹配 |
| 数据库 | `for row in table: yield row` | `BtreeNext()` in `btree.c:7234` | 内存遍历 → 磁盘页 IO + cursor 状态机 |
| 编译器 | `tokens = src.split(' ')` | `Scanner::Scan()` in `scanner.cc:412` | 简单分词 → 字符类查询 + 状态机 |
| OS 内核 | `def schedule(): next_proc.run()` | `swtch(&old.ctx, &new.ctx)` in `swtch.S:8` | 函数调用 → 上下文寄存器切换 |

### §4.4 Step 4：写"工业级增强"解释

使用"差异对比"的文本图，不用 Markdown 表格（因为内容太长不好排版）：

```
最简版本 (N 行)              repo 增强 (M 行)
─────────────────              ──────────────────────────
xxx = yyy             →    工业级功能1 + 工业级功能2
aaa()                 →    更复杂的实现
                            + 额外考虑的场景
─────────────────              ──────────────────────────
核心原则：多出来的不是"更多概念"，是"把同样的事做得更健壮"
```

**核心信念**：

> "更多的代码行数 = 把同样的事做得更健壮、更安全、更灵活。
> 不是更多的新概念。
> 理解了 80 行的骨架，你就理解了 1600 行的意图。"

每次面对复杂代码时都要先讲这句话。

---

## §5. 代码导航法

告诉学生"从哪里开始读代码"比"解释代码在干什么"更重要。

### §5.1 标准代码导航格式

```
第 1 轮（30 分钟）：[具体目标，如"追踪一条消息"]
1. 打开 src/xxx/yyy.ts，搜索 functionName（约 N 行附近）
2. 关注这几行（给出行号范围）
3. 这里做了什么？（一句话）

第 2 轮（30 分钟）：[具体目标，如"理解 ReAct 循环"]
...
```

### §5.2 "永远从一条消息的路径开始"原则

**永远从"一条消息的路径"开始**，不从 `entry.ts` 或 `index.ts` 开始——那里是噪音最多的地方。

为什么：
- `entry.ts/index.ts` 是初始化代码，跟"这个 repo 在做什么"无关
- 学生从一条真实消息的入口跟下去，才能感受到"这个系统在干嘛"
- 数据流是有方向的，跟着数据走 = 跟着真实业务走

### §5.3 代码路径图格式

```
用户发消息
    │
    ▼
src/foo/bar.ts:730      ← 说明入口的职责（一句话）
    │ (调用)
    ▼
src/baz/qux.ts:235      ← 说明下一跳的职责
    │
    └── 关注这里的几行：
        - line 991: acquireSessionWriteLock()  ← 为什么？防止并发写
        - line 1068: createAgentSession()      ← 对应最简版的哪一步
        - line 1627: activeSession.prompt()    ← 这是关键！
```

### §5.4 file:line 引用规范

正文中引用代码位置，始终用 `文件名:行号` 或 Markdown 链接格式：

```
正文引用：`attempt.ts:1627` 或 [attempt.ts:1627](src/agents/pi-embedded-runner/run/attempt.ts#L1627)
代码块注释：// attempt.ts:1627
路径图中：src/agents/pi-embedded-runner/run/attempt.ts:1627
```

---

## §6. 教学节奏（单次教学 45-60 分钟）

```
0-5 分钟：全景问题
  "想象没有 X，会发生什么？"
  → 让学生感受到这个模块存在的必要性

5-20 分钟：概念和架构（层一+层二）
  - 一张 ASCII / mermaid 架构图
  - 2-3 个核心概念，每个一句话定义 + 具体例子（语义波 Unpack）
  - 1-2 个关键设计决策（ADR 格式）
  - 引入外部高质量材料（论文/权威博客的核心洞察）

  ★ 检查点 A：概念理解检查（进入代码之前！）
    "用一句话，不用任何术语，告诉我这个[概念]解决了什么问题？"
    - 学生说清楚了 → 带他用术语重新表达（语义波 Repack）→ 继续
    - 学生说不清楚 → 找到盲点 → 补充例子/外部材料直到说清楚
    - 严禁跳过此检查点直接进入代码

20-40 分钟：最简对照（层三）
  - Step 0：高层级代码框架（file:line 路径图，3-5 个核心文件）

  ★ 检查点 B：代码框架检查
    "打开 [file]，你能找到这个请求从哪里进来的吗？"
    - 找到了 → 继续展示最简实现
    - 找不到 → 重新梳理文件关系，给更多路径提示

  - Step 1：展示最简实现（代码 + 解释）
  - Step 2-4：展示 repo 对应（file:line + 对照表 + 工业级增强）

40-50 分钟：代码导航
  - 给出读代码的具体步骤（分轮次）
  - 每个关键文件的 file:line 引用

50-60 分钟：检验
  - 3 个标准问题（参见 exercises-template.md）
  - 让学生口头回答，找出没理解的点
```

详细的场景模板（学生卡住怎么办、单文件精读怎么教）见 `checkpoints-and-scenarios.md`。

---

## §7. 检验问题的核心要求

每个模块结束后的检验问题必须是**可以用代码验证**的问题，不能是纯概念题。

```
✅ 好的检验问题：
- "打开 attempt.ts，找到启动 ReAct 循环的那一行，它叫什么？"
- "最简版的 messages = [] 对应 repo 的哪个函数调用？"
- "为什么 JSONL 比 JSON 更适合 session 存储？用一个场景说明。"

❌ 差的检验问题：
- "你理解 ReAct 了吗？"（太主观）
- "解释 pi-agent-core 的作用。"（太宽泛）
```

详见 `exercises-template.md`。

---

## §8. 这套方法论的适用范围与不可妥协性

**适用范围**：所有 stage-3-walkthroughs/ 教学、stage-1-foundations/ 和 stage-2-architecture/ 的内容生成、stage-4-applied/ 的迁移讨论。

**不可妥协**：方法论本身（最简对照法五步、检查点 A/B、Feynman 检验、语义波 Unpack/Repack、三层递进、file:line 引用规范）不可被"用户偏好"覆盖。

可被用户偏好覆盖的是：
- 语言（中/英/双语）
- 类比的多少
- 单次教学的时长（45 vs 60 分钟）
- 是否需要在每节课开头复习上节课

但**不可覆盖**：
- "进代码前先做概念 Feynman 检验"
- "展示 repo 代码前先展示最简实现"
- "代码引用必须带 file:line"
- "禁止从 entry.ts/index.ts 开教"
