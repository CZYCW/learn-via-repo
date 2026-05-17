# 安装指南

> 这个 skill 遵循 [Agent Skills 开放标准](https://agentskills.io)，理论上任何符合标准的 agent runtime 都能用。不同 runtime 装的方式略有不同——下面分别说。

## 通用步骤（所有 runtime 都做）

### 步骤 1：clone 这个 repo

```bash
cd ~/projects  # 或任意你喜欢的位置
git clone https://github.com/CZYCW/learn-via-repo.git
```

### 步骤 2：放到 agent 能找到的 skills 目录

不同 runtime 的 skills 目录不一样。下面按 runtime 分。

---

## 不同 runtime 的安装方式

### Claude Code（CLI / IDE 插件 / 桌面 app）

```bash
mkdir -p ~/.agents/skills
ln -s ~/projects/learn-via-repo ~/.agents/skills/learn-via-repo
```

触发：直接对话 `用这个 repo 教我 X` 或 slash command `/learn-via-repo`。

详细文档：[code.claude.com/docs/en/skills](https://code.claude.com/docs/en/skills)

---

### Claude.ai（网页版）

在 Project 设置里上传 skill：

1. 打开你的 Project
2. Settings → Skills → Upload Custom Skill
3. 上传整个 `learn-via-repo/` 目录（zip 后上传）

触发：在 Project 内直接对话即可。

详细文档：[platform.claude.com/docs/en/agents-and-tools/agent-skills](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview)

---

### Cursor

```bash
mkdir -p ~/.cursor/skills
ln -s ~/projects/learn-via-repo ~/.cursor/skills/learn-via-repo
```

触发：在 Cursor chat 里说"用这个 repo 教我 X"。

详细文档：[cursor.com/docs/context/skills](https://cursor.com/docs/context/skills)

---

### GitHub Copilot

GitHub Copilot 的 skills 通过 `.github/copilot-skills/` 项目级管理，或通过 VS Code 全局配置。

详细文档：[docs.github.com/en/copilot/concepts/agents/about-agent-skills](https://docs.github.com/en/copilot/concepts/agents/about-agent-skills)

---

### OpenAI Codex

```bash
mkdir -p ~/.codex/skills
ln -s ~/projects/learn-via-repo ~/.codex/skills/learn-via-repo
```

详细文档：[developers.openai.com/codex/skills](https://developers.openai.com/codex/skills/)

---

### Gemini CLI

按 Gemini CLI 的 skills 配置文件（通常在 `~/.config/gemini/skills/`）放置。

详细文档：[geminicli.com/docs/cli/skills](https://geminicli.com/docs/cli/skills/)

---

### 其他兼容 runtime

下面这些 agent runtime 都支持 Agent Skills 标准，按各自文档配置 skills 目录即可：

| Runtime | 文档链接 |
|---------|---------|
| Goose | [block.github.io/goose/docs/guides/context-engineering/using-skills](https://block.github.io/goose/docs/guides/context-engineering/using-skills/) |
| OpenHands | [docs.openhands.dev/overview/skills](https://docs.openhands.dev/overview/skills) |
| Roo Code | [docs.roocode.com/features/skills](https://docs.roocode.com/features/skills) |
| Letta | [docs.letta.com/letta-code/skills](https://docs.letta.com/letta-code/skills/) |
| Kiro | [kiro.dev/docs/skills](https://kiro.dev/docs/skills/) |
| Workshop | [docs.workshop.ai](https://docs.workshop.ai/core-concepts/working-with-the-agent) |
| Junie | [junie.jetbrains.com/docs/agent-skills.html](https://junie.jetbrains.com/docs/agent-skills.html) |
| fast-agent | [fast-agent.ai/agents/skills](https://fast-agent.ai/agents/skills/) |
| Amp | [ampcode.com/manual#agent-skills](https://ampcode.com/manual#agent-skills) |
| Mistral Vibe | [github.com/mistralai/mistral-vibe](https://github.com/mistralai/mistral-vibe) |

完整支持列表见 [agentskills.io/clients](https://agentskills.io/clients)。

---

## 验证安装

不管哪个 runtime，验证步骤都一样：

1. 在 agent chat 里输入：`用这个 repo 教我学一下 AI agent`
2. 如果 skill 装好了，agent 会按 Phase 0 流程开口问你："你目前是哪种情况——已经知道想读哪个 repo 了 / 知道想学什么方向但不知道选哪个 repo / 还在探索"
3. 如果 agent 没有按这个流程问，可能是：
   - skill 没被加载（检查 `SKILL.md` 是否在正确目录）
   - SKILL.md frontmatter 缺失（检查顶部 `--- name: learn-via-repo --- description: ...` 是否完整）
   - runtime 需要重启让它扫描新 skill

---

## 卸载

不管哪个 runtime，删掉对应目录的软链接 / skill 文件即可：

```bash
# Claude Code
rm ~/.agents/skills/learn-via-repo

# Cursor
rm ~/.cursor/skills/learn-via-repo

# 其他 runtime 按各自路径
```

源 repo（你 `git clone` 那一份）不受影响。

---

## 更新

如果是软链接方式安装：

```bash
cd ~/projects/learn-via-repo
git pull
# 更新立即生效，无需重启 agent（部分 runtime 可能需要重启）
```

---

## 常见问题

### Q: 我用的 agent runtime 不在上面列表里，怎么办？

只要 runtime 支持 Agent Skills 标准（即认 SKILL.md 作为入口），原则上都能用。看它的 skills 文档找到 skills 目录路径，把 `learn-via-repo/` 整个目录放进去就行。

如果 runtime 不支持 Agent Skills 标准——把整个 SKILL.md + references/ 的内容贴进 runtime 的 "system prompt" / "custom instructions" / "context" 配置。**但这种 fallback 方式会丢失 progressive disclosure 的优势**（所有内容一次性加载），可能撑爆 context。

### Q: 我已经在用其他 skill 了，会冲突吗？

不会。Agent Skills 标准设计上每个 skill 独立目录，互不影响。Agent 根据 description 选择激活哪个 skill。

### Q: 我可以同时装多个版本（如 main + dev）吗？

可以——把 dev 版的 SKILL.md frontmatter 里 `name: learn-via-repo` 改成 `name: learn-via-repo-dev`，软链接到不同目录即可。

### Q: 生成的教学产物存到哪？

skill 会问你"教学产物目录放哪儿"——默认 `~/Desktop/learning/{repo-name}/`，你可以自定义。教学产物完全独立于 skill 本身，不会污染 skill 目录。

### Q: skill 调用了 WebSearch / WebFetch，但我用的 runtime 不支持，怎么办？

skill 的 Phase 2 / 2C 需要 WebSearch + WebFetch 找 repo 候选。如果 runtime 不支持这两个工具，skill 会：
1. 退化为让你自己提供 repo 候选名（你贴 GitHub URL）
2. AI 用已知的 (multi-domain-examples.md §1 的) 起点 candidate 作为推荐

但**会损失"AI 给你真实搜+验证后的候选评估"这个核心步骤**。建议尽量用支持 WebSearch 的 runtime。

---

## 反馈

测试中遇到问题？看 [TESTING.md](./TESTING.md) 的反馈模板，或者直接提 issue。
