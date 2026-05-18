# 安装指南

> 这个 skill 遵循 [Agent Skills 开放标准](https://agentskills.io)。下面分 runtime 给安装步骤——以 Claude Code 为主（验证过），其他 runtime 列出官方文档链接让你自查路径。

---

## Claude Code（验证过的方式）

Claude Code 在三个位置查找 skill（[官方文档](https://code.claude.com/docs/en/skills)）：

| 安装位置 | 路径 | 适用范围 |
|---------|------|---------|
| **Personal**（推荐） | `~/.claude/skills/<skill-name>/SKILL.md` | 你所有项目都能用 |
| **Project** | `<your-project>/.claude/skills/<skill-name>/SKILL.md` | 仅当前项目 |
| **Plugin** | 通过 `/plugin marketplace` 安装 | 整个 plugin 启用范围 |

### 推荐方式：clone 到 Personal 目录

一行搞定（确认你的 GitHub 能访问，没装过同名 skill）：

```bash
mkdir -p ~/.claude/skills && git clone https://github.com/CZYCW/learn-via-repo.git ~/.claude/skills/learn-via-repo
```

这条命令做了：
1. 确保 `~/.claude/skills/` 目录存在
2. 把整个 repo clone 到 `~/.claude/skills/learn-via-repo/`
3. clone 后 `SKILL.md` 就在 `~/.claude/skills/learn-via-repo/SKILL.md`——Claude Code 会自动扫到

### 验证安装成功（3 步）

#### Step 1：确认文件确实在正确位置

```bash
ls ~/.claude/skills/learn-via-repo/SKILL.md
```

应该看到这个文件存在。如果"No such file"——上一步 clone 没成功，重跑。

#### Step 2：确认 SKILL.md 的 frontmatter 没坏

```bash
head -3 ~/.claude/skills/learn-via-repo/SKILL.md
```

应该看到：

```
---
name: learn-via-repo
description: "Systematically learn any software engineering domain..."
```

如果 `name:` 那一行缺失或拼错，Claude Code 不认。

#### Step 3：在 Claude Code 里验证

**完全重启 Claude Code**（不是只关窗口——CLI 用户 `exit` 退出后重开；桌面 app 用户 quit 再 launch）。这一步关键，因为 Claude Code 启动时才扫 skill 目录。

重启后在 Claude Code 里输入 `/`，应该在弹出的命令列表里看到 `learn-via-repo`。或者直接输入：

```
/learn-via-repo
```

如果 skill 装好了，Claude 会按 Phase 0 流程开口问你"你目前是哪种情况"。

### 第二种方式：clone 到任意位置 + 软链接（推荐给开发者）

如果你想把源 repo 放在自己习惯的工作目录，软链到 skills 目录：

```bash
# clone 到你习惯的位置
cd ~/projects
git clone https://github.com/CZYCW/learn-via-repo.git

# 软链到 Claude Code 看的位置
mkdir -p ~/.claude/skills
ln -s ~/projects/learn-via-repo ~/.claude/skills/learn-via-repo

# 验证软链有效
ls -la ~/.claude/skills/learn-via-repo/SKILL.md
```

好处：以后 `cd ~/projects/learn-via-repo && git pull` 就能更新——软链让两边自动同步。

---

## Claude.ai（网页 / 桌面 app）

按 [Use skills in Claude 官方说明](https://support.claude.com/en/articles/12512180-use-skills-in-claude) 在 Project 设置里上传 zip 包：

```bash
# 1. 在本地打包
cd ~/projects
zip -r learn-via-repo.zip learn-via-repo -x "learn-via-repo/.git/*"
```

2. 浏览器打开你的 Claude.ai Project → Settings → Skills → Upload Custom Skill → 选 `learn-via-repo.zip`

---

## 其他 Agent Skills 兼容 runtime

下面这些 runtime 都支持同一份 SKILL.md 格式，但各自的安装路径不同。**我不在这里写具体路径**（因为我没逐一验证过），请按各自官方文档操作：

| Runtime | 官方 skills 文档 |
|---------|---------------|
| Cursor | https://cursor.com/docs/context/skills |
| GitHub Copilot | https://docs.github.com/en/copilot/concepts/agents/about-agent-skills |
| OpenAI Codex | https://developers.openai.com/codex/skills/ |
| Gemini CLI | https://geminicli.com/docs/cli/skills/ |
| Goose | https://block.github.io/goose/docs/guides/context-engineering/using-skills/ |
| OpenHands | https://docs.openhands.dev/overview/skills |
| Roo Code | https://docs.roocode.com/features/skills |
| Letta | https://docs.letta.com/letta-code/skills/ |
| Junie | https://junie.jetbrains.com/docs/agent-skills.html |
| Kiro | https://kiro.dev/docs/skills/ |
| Workshop | https://docs.workshop.ai/core-concepts/working-with-the-agent |
| fast-agent | https://fast-agent.ai/agents/skills/ |
| Amp | https://ampcode.com/manual#agent-skills |
| Mistral Vibe | https://github.com/mistralai/mistral-vibe |

完整 30+ 兼容 runtime 列表见 [agentskills.io/clients](https://agentskills.io/clients)。

每个 runtime 通用步骤大致是：
1. 找到该 runtime 的 skills 目录路径
2. clone 这个 repo 到那个路径下，或者 clone 到任意位置再软链
3. 重启 runtime（部分 runtime 支持热加载，不需要重启）
4. 验证 skill 出现在命令列表

---

## 故障排查（`/learn-via-repo` 找不到怎么办）

按下面顺序逐条排查，90% 的问题在前 3 项。

### 1. 检查文件路径

```bash
ls -la ~/.claude/skills/learn-via-repo/SKILL.md
```

**期望输出**：文件存在，权限至少 `-rw-r--r--`。

**没看到文件**：clone 失败或装到了错误目录。**特别注意**：我之前文档里写过 `~/.agents/skills/`——这是错的，那不是 Claude Code 看的路径。如果你装在那里，删掉，重新装到 `~/.claude/skills/`：

```bash
# 删错的位置（如果存在）
rm -rf ~/.agents/skills/learn-via-repo

# 装到正确位置
mkdir -p ~/.claude/skills && git clone https://github.com/CZYCW/learn-via-repo.git ~/.claude/skills/learn-via-repo
```

### 2. 检查 frontmatter

```bash
head -5 ~/.claude/skills/learn-via-repo/SKILL.md
```

**期望**：前 3 行是 `---` / `name: learn-via-repo` / `description: "..."`。

**如果缺 `name:` 或拼错**：Claude Code 不认这个 skill。手动用编辑器修。

### 3. 完全重启 Claude Code

**这是最常被忽略的一步**。Claude Code **启动时**才扫 skill 目录——新增 skill 后必须重启。

- CLI：`exit` 退出当前 session，再重新 `claude` 启动
- 桌面 app：⌘Q 完全退出，再 launch
- IDE 插件：重启 IDE

重启后再试 `/learn-via-repo`。

> Claude Code 文档：[**"Live change detection"** 章节](https://code.claude.com/docs/en/skills#live-change-detection) 说"创建新的 skill 顶级目录需要重启 Claude Code"。我们的情况就是这种——`~/.claude/skills/learn-via-repo/` 是新目录。

### 4. 用 `/doctor` 诊断

在 Claude Code 里跑：

```
/doctor
```

这会列出你的 Claude Code 配置 + 所有加载的 skill。看看 `learn-via-repo` 是不是在列表里。如果**列表里没有**——回到 1-2-3 步排查。如果**列表里有但 `/learn-via-repo` 仍不响应**——可能是别的 skill 同名冲突，往下看 5。

### 5. 检查命名冲突

```bash
find ~/.claude/skills -name "SKILL.md" -exec grep -l "name: learn-via-repo" {} \;
find ./.claude/skills -name "SKILL.md" -exec grep -l "name: learn-via-repo" {} \; 2>/dev/null
```

**期望**：只有一个文件出现（`~/.claude/skills/learn-via-repo/SKILL.md`）。

**如果有多个**：某地方有同名 skill，按 Claude Code 优先级规则（enterprise > personal > project）会被覆盖。删掉重复的。

### 6. 还不行，提 issue

把 `/doctor` 的完整输出截图 + 上面 1-5 步的命令输出贴到 [issue 区](https://github.com/CZYCW/learn-via-repo/issues/new) 我帮你看。

---

## 卸载

```bash
# 如果是 clone 方式装的：
rm -rf ~/.claude/skills/learn-via-repo

# 如果是软链方式装的：
rm ~/.claude/skills/learn-via-repo  # 删软链（不影响源 repo）
```

重启 Claude Code 让它扫到目录已经空了。

---

## 更新到最新版

如果是 clone 方式装的：

```bash
cd ~/.claude/skills/learn-via-repo
git pull
```

如果是软链方式装的：

```bash
cd ~/projects/learn-via-repo  # 你 clone 的源位置
git pull
```

[Live change detection](https://code.claude.com/docs/en/skills#live-change-detection)：Claude Code 监听 skill 目录的文件变化——`git pull` 之后**当前 session 内立即生效**，不需要重启。

---

## 常见问题

### Q: 我已经用旧文档（`~/.agents/skills/`）装过了，怎么修？

```bash
# 1. 删旧位置
rm -rf ~/.agents/skills/learn-via-repo

# 2. 装到正确位置
mkdir -p ~/.claude/skills && git clone https://github.com/CZYCW/learn-via-repo.git ~/.claude/skills/learn-via-repo

# 3. 重启 Claude Code
```

抱歉之前的文档错了。这次修对了，麻烦再装一次。

### Q: 我用的 agent runtime 不在上面列表里，怎么办？

只要 runtime 支持 [Agent Skills 标准](https://agentskills.io) （认 SKILL.md 作为入口），原则上都能用。看它的官方 skills 文档找到 skills 目录路径，把 `learn-via-repo/` 整个目录放进去就行。

如果 runtime 不支持 Agent Skills 标准——把 SKILL.md 的内容贴进 runtime 的 system prompt / custom instructions / context 配置。**但这种 fallback 方式会丢失 progressive disclosure 的优势**（所有 SKILL.md 内容一次性加载），可能撑爆 context window。

### Q: 我能不能用 `/plugin marketplace add CZYCW/learn-via-repo` 装？

**目前不行**。这个 repo 是**单 skill 直接安装**结构，不是 Claude Code plugin marketplace 结构。Plugin marketplace 需要 repo 顶部有 `plugins/` 目录组织多个 plugin，复杂度高一些。我可能在 V5 改造成 marketplace 结构——届时 `/plugin marketplace add CZYCW/learn-via-repo` 就能用了。

### Q: 我可以同时装多个版本（main + dev）吗？

可以——把 dev 版的 `SKILL.md` frontmatter 里 `name: learn-via-repo` 改成 `name: learn-via-repo-dev`，clone 到 `~/.claude/skills/learn-via-repo-dev/`。两个 skill name 不冲突，能并存。

### Q: 生成的教学产物存到哪？

skill 会问你"教学产物目录放哪儿"——默认 `~/Desktop/learning/{repo-name}/`，你可以自定义。教学产物完全独立于 skill 本身，不会污染 `~/.claude/skills/` 目录。

### Q: skill 调用了 WebSearch / WebFetch，但我用的 runtime 不支持，怎么办？

skill 的 Phase 2 / 2C 需要 WebSearch + WebFetch 找 repo 候选。如果 runtime 不支持这两个工具，skill 会：
1. 退化为让你自己提供 repo 候选名（你贴 GitHub URL）
2. AI 用 `references/multi-domain-examples.md` 的起点 candidate 作为推荐

但**会损失"AI 给你真实搜+验证后的候选评估"这个核心步骤**。建议尽量用支持 WebSearch 的 runtime。

---

## 反馈

测试中遇到问题？看 [TESTING.md](./TESTING.md) 的反馈模板，或直接[提 issue](https://github.com/CZYCW/learn-via-repo/issues/new)。
