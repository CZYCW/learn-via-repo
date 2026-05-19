# 安装指南

> 这个 skill 遵循 [Agent Skills 开放标准](https://agentskills.io)，可通过 [skills.sh marketplace](https://skills.sh) 发现，支持 51+ agent runtime。

---

## 推荐方式：用 `npx skills` 一行装好（适用所有 agent）

[Vercel Labs 出的 `skills` CLI](https://github.com/vercel-labs/skills) 是整个 Agent Skills 生态的标准安装工具——**自动检测你用的 agent，自动放对路径**。你不用懂任何路径。

### 最简一行（交互式）

```bash
npx skills add CZYCW/learn-via-repo
```

CLI 会问你：

1. **装到哪些 agent？**（它会自动检测你装了 Claude Code / Cursor / Codex / Gemini CLI 等，让你勾选）
2. **Project 还是 Global？**（Project = 仅当前项目可用、跟 git 一起共享；Global = 所有项目都能用）
3. **Symlink 还是 Copy？**（推荐 symlink——多个 agent 共享一份，更新方便）

回答完自动装到正确路径。完成。

### 进阶选项

```bash
# 全局装到 Claude Code，跳过所有确认（CI/CD 友好）
npx skills add CZYCW/learn-via-repo -g -a claude-code -y

# 同时装到多个 agent
npx skills add CZYCW/learn-via-repo -g -a claude-code -a cursor -a codex

# 先列出 repo 里有什么 skill 不装
npx skills add CZYCW/learn-via-repo --list

# 装到当前项目（不是全局）
npx skills add CZYCW/learn-via-repo  # 默认是 project 范围
```

完整 CLI 命令见 [vercel-labs/skills README](https://github.com/vercel-labs/skills#readme)。

### 重启 agent（关键步骤！）

装完之后**必须完全重启 agent**——agent 启动时才扫 skills 目录。

- **Claude Code CLI**：`exit` 退出当前 session，再 `claude` 重开
- **Claude Code 桌面 app**：⌘Q 完全退出，再 launch
- **Cursor / VSCode-based agents**：重启 IDE
- **其他 CLI agent**：退出当前 session 再重开

### 验证

重启后在 agent 里输入：

```
/learn-via-repo
```

或者直接说"用这个 repo 教我 AI agent"——skill 会按 Phase 0 流程开口问你。

---

## 手动安装（不能用 npm 时的备选）

如果你没装 Node.js，或在限制网络的环境，可以手动 clone + symlink。

### 步骤 1：clone 这个 repo

```bash
cd ~/projects  # 你习惯的位置
git clone https://github.com/CZYCW/learn-via-repo.git
```

### 步骤 2：按你用的 agent 把 skill 链接 / 复制到对应路径

下表来自 [vercel-labs/skills 的 supported agents 列表](https://github.com/vercel-labs/skills#supported-agents)——**这是官方真相**：

| Agent | 全局路径（`-g`） | 项目路径（默认） |
|-------|----------------|----------------|
| **Claude Code** | `~/.claude/skills/` | `./.claude/skills/` |
| **Cursor** | `~/.cursor/skills/` | `./.agents/skills/` |
| **Codex** | `~/.codex/skills/` | `./.agents/skills/` |
| **Gemini CLI** | `~/.gemini/skills/` | `./.agents/skills/` |
| **GitHub Copilot** | `~/.copilot/skills/` | `./.agents/skills/` |
| **Goose** | `~/.config/goose/skills/` | `./.goose/skills/` |
| **OpenHands** | `~/.openhands/skills/` | `./.openhands/skills/` |
| **OpenCode** | `~/.config/opencode/skills/` | `./.agents/skills/` |
| **Continue** | `~/.continue/skills/` | `./.continue/skills/` |
| **Windsurf** | `~/.codeium/windsurf/skills/` | `./.windsurf/skills/` |
| **Roo Code** | `~/.roo/skills/` | `./.roo/skills/` |
| **Kiro CLI** | `~/.kiro/skills/` | `./.kiro/skills/` |
| **Junie** | `~/.junie/skills/` | `./.junie/skills/` |
| **Mistral Vibe** | `~/.vibe/skills/` | `./.vibe/skills/` |
| **Amp / Kimi / Replit / Universal** | `~/.config/agents/skills/` | `./.agents/skills/` |
| **Cline / Dexto / Warp** | `~/.agents/skills/` | `./.agents/skills/` |
| **Antigravity** | `~/.gemini/antigravity/skills/` | `./.agents/skills/` |

剩下 30 多个 agent 的路径见 [vercel-labs/skills README 完整表](https://github.com/vercel-labs/skills#supported-agents)。

### 步骤 3：用软链接关联

以 **Claude Code 全局** 为例：

```bash
mkdir -p ~/.claude/skills
ln -s ~/projects/learn-via-repo ~/.claude/skills/learn-via-repo
```

以 **Cursor 当前项目** 为例：

```bash
mkdir -p ./.agents/skills
ln -s ~/projects/learn-via-repo ./.agents/skills/learn-via-repo
```

### 步骤 4：完全重启 agent + 验证

跟上面"npx skills 推荐方式"的最后两步一样。

---

## 故障排查：`/learn-via-repo` 找不到怎么办

按下面顺序逐条排查，90% 的问题在前 3 项。

### 1. 确认文件确实在你 agent 看的路径里

先确认你用的是什么 agent，对照上表找路径。例如你用 Claude Code 全局：

```bash
ls -la ~/.claude/skills/learn-via-repo/SKILL.md
```

应该看到这个文件存在。如果"No such file"——上一步装错位置了，重新装。

**最常见错误**：你以为装到了 Claude Code 路径，实际装到了别的 agent 路径。`npx skills add` 装的时候会告诉你装到哪里——看回放。

### 2. 确认 SKILL.md 的 frontmatter 没坏

```bash
head -5 ~/.claude/skills/learn-via-repo/SKILL.md  # 路径按你 agent 替换
```

应该看到：

```
---
name: learn-via-repo
description: "..."
---
```

如果 `name:` 那一行缺失或拼错，agent 不认这个 skill。

### 3. 完全重启 agent

**这是最常被忽略的一步**。agent **启动时**才扫 skill 目录——新增 skill 后必须重启。

- CLI：`exit` 退出当前 session，再重新开
- 桌面 app：⌘Q 完全退出，再 launch
- IDE 插件：重启 IDE

重启后再试 `/learn-via-repo`。

### 4. 用 `npx skills list` 检查

```bash
npx skills list
```

这会列出你所有 agent 装了哪些 skill。看看 `learn-via-repo` 是不是在列表里。

不在 → 回到 1-2-3 步。

### 5. 用 agent 自带的诊断命令

各 agent 有自己的诊断方式：

- **Claude Code**：在 agent 里跑 `/doctor`，看 skill 列表
- **Cursor**：Settings → Skills，看是否出现

### 6. 还不行，提 issue

把 `npx skills list` 完整输出 + 上面 1-5 步的输出贴到 [issue 区](https://github.com/CZYCW/learn-via-repo/issues/new) 我帮你看。

---

## 卸载

### 用 npx skills 装的

```bash
npx skills remove learn-via-repo
```

会问你从哪些 agent 卸载，选完确认。

### 手动装的

```bash
rm ~/.claude/skills/learn-via-repo  # 或者你装到的位置
# 软链方式：上面这条只删软链，不影响源 repo
# clone 方式：rm -rf 整个目录
```

---

## 更新到最新版

### 用 npx skills 装的

```bash
npx skills update learn-via-repo
# 或者更新所有 skill
npx skills update
```

### 手动装的（软链方式）

```bash
cd ~/projects/learn-via-repo  # 你 clone 的源位置
git pull
```

软链关联的所有 agent 都会自动看到更新。

### 手动装的（copy 方式）

```bash
cd ~/projects/learn-via-repo
git pull
cp -r . ~/.claude/skills/learn-via-repo  # 重新拷贝
```

---

## 常见问题

### Q: 我已经按旧文档装到 `~/.agents/skills/learn-via-repo/` 了，怎么修？

那是 Cline / Dexto / Warp 几个特定 agent 的全局路径——**不是 Claude Code 看的路径**。Claude Code 看的是 `~/.claude/skills/`。

修法：

```bash
# 1. 卸掉错误位置
rm -rf ~/.agents/skills/learn-via-repo

# 2. 用 npx skills 重新装
npx skills add CZYCW/learn-via-repo

# 3. 完全重启 agent
```

抱歉之前的文档错了，跨 agent 路径太多我没逐一验证。这次按 vercel-labs/skills 的 supported-agents 表写，是真相。

### Q: 我用的 agent runtime 不在上面列表里，怎么办？

`npx skills` CLI 支持 51+ agent，可能你的也在里面。先跑 `npx skills add CZYCW/learn-via-repo` 看 CLI 是否能自动检测到你的 agent。

如果检测不到——查你 agent 的官方文档找 skills 目录路径，按"手动安装"步骤 3 软链上去。

如果 agent 完全不支持 Agent Skills 标准——只能 fallback 到把 `SKILL.md` 的内容贴进 runtime 的 system prompt / custom instructions / context 配置。**这种方式会丢失 progressive disclosure 的优势**（所有内容一次性加载），可能撑爆 context window。

### Q: 我可以同时装多个版本（main + dev）吗？

可以——把 dev 版的 `SKILL.md` frontmatter 里 `name: learn-via-repo` 改成 `name: learn-via-repo-dev`，再用 `npx skills add` 装。两个 name 不冲突，能并存。

### Q: 生成的教学产物存到哪？

skill 会问你"教学产物目录放哪儿"——默认 `~/Desktop/learning/{repo-name}/`，你可以自定义。教学产物完全独立于 skill 本身，不会污染 skills 目录。

### Q: skill 调用了 WebSearch / WebFetch，但我用的 agent 不支持，怎么办？

skill 的 Phase 2 / 2C 需要 WebSearch + WebFetch 找 repo 候选。如果 agent 不支持这两个工具，skill 会：

1. 退化为让你自己提供 repo 候选名（你贴 GitHub URL）
2. AI 用 `references/multi-domain-examples.md` 的起点 candidate 作为推荐

但**会损失"AI 给你真实搜+验证后的候选评估"这个核心步骤**。建议尽量用支持 WebSearch 的 agent（Claude Code / Cursor / Codex 都支持）。

---

## 反馈

测试中遇到问题？看 [TESTING.md](./TESTING.md) 的反馈模板，或直接[提 issue](https://github.com/CZYCW/learn-via-repo/issues/new)。
