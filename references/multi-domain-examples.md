# 多领域示例库

> 本 skill 的方法论是领域无关的，但学习者最容易通过"我熟悉的领域 + 类似领域"的对照来理解抽象原则。本文档为 5-6 个常见软件系统领域建立"抽象概念 → 具体实现"映射，供 `methodology.md` / `walkthrough-template.md` / `forbidden-list.md` 等其他文档**引用**而非各自重复。

---

## §1. 核心映射表（5 个必备领域 + 2 个可选）

每个领域提供 5 个维度的具体化：

| 维度 | AI Agent | Web 框架 (Express/Koa 风格) | 数据库内核 (SQLite 风格) | 编译器/解释器 (V8/Lua 风格) | OS 内核 (xv6 风格) | 游戏引擎 (可选) | 分布式系统 (可选) |
|------|---------|---------|---------|---------|---------|---------|---------|
| **核心控制流** | ReAct loop（LLM↔tool↔observation 递归） | request → middleware 链 → handler → response | parser → planner → VM 字节码循环 | tokenize → parse AST → bytecode/IR → execute | syscall trap → scheduler → context switch → return | input → update → render game loop | leader election → consensus round → state replication |
| **核心入口文件**（示例） | `attempt.ts` / `agent.py` | `app.js` / `application.js` | `main.c` / `vdbeapi.c` | `parser.cc` / `interpreter.c` | `proc.c` / `trap.c` | `engine.cpp` / `main.cpp` | `raft.go` / `consensus.rs` |
| **关键骨架元素**（看见这些 = 第一性原理；看不见 = 被框架掩盖） | `messages.append({role, content})` + `if stop_reason == "tool_use": execute_tool(...)` | `next(err)` 链调用 + `req` / `res` 对象传递 | Btree cursor 操作 + opcode dispatch loop | TokenScanner + ASTNode 构造 + Visitor 模式 | trap frame 保存 + 调度队列 + page table 切换 | game loop tick + ECS 组件查询 + 渲染队列 | log entry append + AppendEntries RPC + commit index 推进 |
| **合格 beginner repo 示例**（**验证状态见下方分级**——AI 在 Phase 2C 仍需独立搜索 + 用户评估） | ✅ 已验证：rohitg00/ai-engineering-from-scratch Phase 14 / pguso/ai-agents-from-scratch / Leonie Monigatti notebook | ⚠️ 待验证 candidate：koajs/koa / expressjs/express 早期 commit | ⚠️ 待验证 candidate：cstack/db_tutorial / sql-js/sql.js / erikgrinaker/toydb | ⚠️ 待验证 candidate：acornjs/acorn / chibicc / craftinginterpreters/craftinginterpreters | ⚠️ 待验证 candidate：mit-pdos/xv6-riscv | ⚠️ 待验证 candidate：handmade hero / pico-8 教程 | ⚠️ 待验证 candidate：ongardie/raftscope |
| **不合格框架示例**（掩盖骨架的成熟封装；非穷举，按 forbidden-list.md §5 判断方法识别新框架） | langchain / langgraph / llamaindex / crewai / autogen / smolagents / openai-agents-sdk | NestJS / Hapi（深度抽象） / Adonis / Spring | sqlalchemy / typeorm / prisma / hibernate | babel（高度封装的现代版） / TypeScript compiler（黑盒） | docker / k8s（不是 OS 内核，是高层调度） / systemd（启动框架） | Unity / Unreal Engine（引擎黑盒） / Godot（部分） | k8s controller-runtime / spring-cloud / consul-template |

---

### §1.5 关于 "已验证" 和 "待验证" 的区别（重要）

V3 升级时，AI Agent 那一行的 beginner repo 是真实跑过 Phase 2C 4 步流程（搜索 → WebFetch 验证 README → 给用户 3-5 候选 → 用户评估）确认的，所以标 ✅ 已验证。

其他领域的 beginner repo 是我（V3 作者）根据社区印象列的"起点 candidate"——**没有经过 Phase 2C 4 步流程的真实验证**。这些 candidate 有几种可能：
- 真的合格（如 xv6 / Crafting Interpreters 在领域内公认是教学经典，大概率 OK）
- 已不再维护或转向用框架了（需要重新评估）
- 还有更好的候选没被我列进来

所以当 AI 实际跑 Phase 2C 时：
1. ⚠️ 待验证 candidate **可以作为搜索起点**，不能直接拿来用
2. 必须按 forbidden-list.md §5 的判断方法验证（看 README 能否见到该领域骨架元素、有无成熟框架 import）
3. 必须给学生 3-5 个候选评估，不是直接拿一个就写进 stage-0
4. 验证通过的，把状态从 ⚠️ 改为 ✅，并在状态后加上验证日期 / 链接

这样表会随着 skill 被使用而越来越准确——每次真实教学一个新领域，那一行就升级一次。

---

## §2. 怎么用这张表

### §2.1 在 `methodology.md` 里

每个抽象原则讲完后，加一句：

> 跨领域示例：以 AI Agent 为例 X；同样原则在 Web 框架是 Y（参见 `multi-domain-examples.md` §1 第 N 行）、在数据库是 Z（同表）

不在 methodology.md 重复表格。

### §2.2 在 `walkthrough-template.md` §0 / §4.1 里

学生生成 walkthrough 时，AI 根据**目标 repo 所在领域**从本表读出对应行作为示例骨架：

- 目标 repo 是 redis？→ 看"数据库内核"行
- 目标 repo 是 vue/express？→ 看"Web 框架"行
- 目标 repo 是 v8？→ 看"编译器/解释器"行

### §2.3 在 `forbidden-list.md` §5 里

第三方框架黑名单按本表"不合格框架示例"列分组，每个分组说"这类框架掩盖了什么骨架"。判断**新框架**用 §3 的判断方法。

---

## §3. 跨领域统一的"是否合格 beginner repo"判断方法

不论领域，对任何候选 beginner repo 做以下 3 步检查：

### 步骤 1：能否看见该领域的核心骨架元素？

打开 README 的示例代码：

- AI Agent：能看见 `messages.append` + `tool_use` 分发？✅
- Web 框架：能看见 `app.use((req, res, next) => ...)` 中间件签名？✅
- 数据库：能看见 cursor 操作 + 行/页 IO？✅
- 编译器：能看见 token 流 + AST 节点构造？✅
- OS：能看见 trap handler + 调度队列？✅

如果只看见 `framework.run(config)` / `agent.execute(task)` 这种黑盒 API → 不合格。

### 步骤 2：核心控制流是否教学可见？

repo 是否有一个**核心循环 / 核心函数 / 核心入口**，用 50-200 行实现该领域的"心脏"？

- 合格：教学型 repo 通常有 `agent.py` / `main.c` / `parser.cc` 等单一入口可读
- 不合格：分散在 200+ 文件 / 大量装饰器抽象 / 大量依赖注入的，骨架被掩盖

### 步骤 3：依赖列表是否克制？

打开 `requirements.txt` / `package.json` / `Cargo.toml`：

- 合格：依赖 ≤ 5 个，都是底层（如 `requests` / `anthropic` SDK / 标准库）
- 不合格：依赖 ≥ 20 个，含成熟框架（如 `langchain` / `react` / `vue` / `django` / `rails`）—— 这些框架本身就是被学习的"骨架"，beginner repo 不应再叠加框架

---

## §4. 领域不在本表怎么办？

如果学生想学的领域不在 §1（如：区块链 / 推荐系统 / 计算机视觉 / 量子计算）：

1. **AI 不要瞎填**——本表的每行都是有教学积累的领域。新领域不要凭印象列示例。
2. **Phase 2C 真实搜索**：跟其他领域一样，WebSearch + WebFetch 找该领域的"无框架 beginner repo"候选，让用户评估。
3. **如有成熟候选**：回填到本表（作为开源 skill 的贡献），让下次该领域的学生受益。
4. **如无成熟候选**：诚实告诉用户"该领域我没找到 ≥1k stars + 无框架的教学 repo，建议：(a) 用 Phase 2C 完整 4 步走一遍可能找到 (b) 选目标 repo 里最简的一个模块作为 stage-0 替代 (c) 跳过 stage-0 直接 stage-1"。

详见 `forbidden-list.md` §5b 元教训 3（"AI 不能独断指认 repo"）。

---

## §5. 表格扩展规则（贡献者指南）

未来其他贡献者要在本表加新领域时遵循：

- 每行至少有 1 个 合格 beginner repo 示例（不是 AI 凭印象，必须验证过）
- 每行的"骨架元素"必须是该领域**真实从业者**会用的术语（不是 AI 编造的）
- 每行的"不合格框架"必须按 §3 步骤 1 验证过——这些框架确实掩盖了骨架
- 新增领域时同步更新 `methodology.md` / `walkthrough-template.md` / `forbidden-list.md` 中"跨领域示例"段的链接

---

## §6. 当前覆盖度

| 领域 | 覆盖度 | 备注 |
|------|------|------|
| AI Agent | ⭐⭐⭐⭐⭐ | 完整，OpenClaw 教学验证过 |
| Web 框架 | ⭐⭐⭐ | 骨架元素 + 不合格框架已列；beginner repo 示例待用户验证后回填 |
| 数据库内核 | ⭐⭐⭐ | 同上 |
| 编译器/解释器 | ⭐⭐⭐ | 同上 |
| OS 内核 | ⭐⭐⭐ | xv6 是公认的标杆；其他示例待验证 |
| 游戏引擎 | ⭐⭐ | 示例较少 |
| 分布式系统 | ⭐⭐ | 示例较少 |

实战中遇到任何领域的 beginner repo 选材过程，记得回填本表，让后续学生受益。
