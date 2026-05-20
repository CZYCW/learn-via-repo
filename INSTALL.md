# Install Guide

> This skill follows the [Agent Skills open standard](https://agentskills.io), is discoverable on the [skills.sh marketplace](https://skills.sh), and works across 51+ agent runtimes.

---

## Recommended: install in one line with `npx skills` (works for all agents)

[Vercel Labs' `skills` CLI](https://github.com/vercel-labs/skills) is the standard install tool for the entire Agent Skills ecosystem — it **auto-detects the agent you're using and puts files in the right path**. You don't need to know any paths.

### Simplest one-liner (interactive)

```bash
npx skills add CZYCW/learn-via-repo
```

The CLI will ask you:

1. **Which agents to install for?** (It auto-detects what you have — Claude Code / Cursor / Codex / Gemini CLI etc — and lets you check boxes)
2. **Project or Global?** (Project = only for the current project, shared via git; Global = available in every project)
3. **Symlink or Copy?** (Recommended: symlink — multiple agents share one source, easier to update)

Answer those and it installs to the right location. Done.

### Advanced options

```bash
# Install globally for Claude Code, skip all prompts (CI/CD friendly)
npx skills add CZYCW/learn-via-repo -g -a claude-code -y

# Install for multiple agents at once
npx skills add CZYCW/learn-via-repo -g -a claude-code -a cursor -a codex

# List skills in the repo without installing
npx skills add CZYCW/learn-via-repo --list

# Install for current project (not global)
npx skills add CZYCW/learn-via-repo  # default is project scope
```

Full CLI reference: [vercel-labs/skills README](https://github.com/vercel-labs/skills#readme).

### Restart the agent (critical step!)

After installing, you **must fully restart the agent** — agents only scan the skills directory at startup.

- **Claude Code CLI**: `exit` the current session, then `claude` to reopen
- **Claude Code desktop app**: ⌘Q to fully quit, then launch again
- **Cursor / VSCode-based agents**: restart the IDE
- **Other CLI agents**: exit the current session and reopen

### Verify

After restarting, in the agent type:

```
/learn-via-repo
```

Or just say "use this repo to teach me AI agents" — the skill will kick off the Phase 0 flow.

---

## Manual install (when you can't use npm)

If you don't have Node.js, or you're in a restricted-network environment, you can clone and symlink manually.

### Step 1: clone this repo

```bash
cd ~/projects  # wherever you keep things
git clone https://github.com/CZYCW/learn-via-repo.git
```

### Step 2: link or copy the skill to your agent's path

The table below comes from [vercel-labs/skills supported agents](https://github.com/vercel-labs/skills#supported-agents) — **this is the source of truth**:

| Agent | Global path (`-g`) | Project path (default) |
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

For the other 30+ agents, see the full table in [vercel-labs/skills README](https://github.com/vercel-labs/skills#supported-agents).

### Step 3: symlink it

For **Claude Code, global**:

```bash
mkdir -p ~/.claude/skills
ln -s ~/projects/learn-via-repo ~/.claude/skills/learn-via-repo
```

For **Cursor, current project**:

```bash
mkdir -p ./.agents/skills
ln -s ~/projects/learn-via-repo ./.agents/skills/learn-via-repo
```

### Step 4: fully restart the agent and verify

Same as the last two steps of "Recommended: npx skills" above.

---

## Troubleshooting: `/learn-via-repo` doesn't show up

Work through this list in order — 90% of the time the answer is in the first three.

### 1. Check that the file actually lives in the path your agent reads

Figure out which agent you're using, look up the path in the table above. For Claude Code global:

```bash
ls -la ~/.claude/skills/learn-via-repo/SKILL.md
```

You should see the file. If you get "No such file" — you installed to the wrong location. Reinstall.

**Most common mistake**: you think you installed to the Claude Code path but actually installed to another agent's. `npx skills add` tells you where it put files during install — scroll up and read the output.

### 2. Check that the SKILL.md frontmatter isn't broken

```bash
head -5 ~/.claude/skills/learn-via-repo/SKILL.md  # adjust path for your agent
```

You should see:

```
---
name: learn-via-repo
description: "..."
---
```

If the `name:` line is missing or wrong, the agent won't recognize the skill.

### 3. Fully restart the agent

**This is the step people skip most often.** Agents scan the skills directory **at startup** — a new skill won't show up until you restart.

- CLI: `exit` the current session, then reopen
- Desktop app: ⌘Q to fully quit, then launch again
- IDE plugin: restart the IDE

Then try `/learn-via-repo` again.

### 4. Check with `npx skills list`

```bash
npx skills list
```

This lists every skill installed across every agent. Look for `learn-via-repo`.

If it's not there → go back to steps 1-3.

### 5. Use the agent's own diagnostics

Each agent has its own:

- **Claude Code**: run `/doctor` in the agent and look at the skills list
- **Cursor**: Settings → Skills

### 6. Still no luck? Open an issue

Paste the full output of `npx skills list` plus what you ran in steps 1-5 into a [new issue](https://github.com/CZYCW/learn-via-repo/issues/new) and I'll take a look.

---

## Uninstall

### If you installed via npx skills

```bash
npx skills remove learn-via-repo
```

It'll ask which agents to uninstall from. Confirm and you're done.

### If you installed manually

```bash
rm ~/.claude/skills/learn-via-repo  # or wherever you put it
# Symlink: this only removes the link, the source repo is untouched
# Clone: rm -rf the whole directory if you no longer need it
```

---

## Update to the latest version

### If you installed via npx skills

```bash
npx skills update learn-via-repo
# or update everything
npx skills update
```

### If you installed manually (symlink)

```bash
cd ~/projects/learn-via-repo  # the source you cloned to
git pull
```

All the symlinked agents see the update automatically.

### If you installed manually (copy)

```bash
cd ~/projects/learn-via-repo
git pull
cp -r . ~/.claude/skills/learn-via-repo  # recopy
```

---

## FAQ

### Q: I already installed to `~/.agents/skills/learn-via-repo/` from an older version of the docs. How do I fix it?

`~/.agents/skills/` is the global path for a few specific agents (Cline / Dexto / Warp) — **not** the path Claude Code reads. Claude Code reads `~/.claude/skills/`.

Fix:

```bash
# 1. Remove the wrong location
rm -rf ~/.agents/skills/learn-via-repo

# 2. Reinstall via npx skills
npx skills add CZYCW/learn-via-repo

# 3. Fully restart the agent
```

Sorry the older docs were wrong — too many cross-agent paths to verify one by one. This version follows the vercel-labs/skills supported-agents table, which is the source of truth.

### Q: My agent runtime isn't in the table above. What do I do?

The `npx skills` CLI supports 51+ agents, so yours might already be in there. Try `npx skills add CZYCW/learn-via-repo` and see if the CLI auto-detects it.

If it can't — check your agent's official docs for the skills directory path, then symlink to it following manual install Step 3.

If your agent has no support for the Agent Skills standard at all — your only fallback is to paste the contents of `SKILL.md` into the runtime's system prompt / custom instructions / context config. **You lose the progressive disclosure benefit this way** (everything loads up front), which might blow your context window.

### Q: Can I install both a main version and a dev version side by side?

Yes — change the `name:` field in the dev version's `SKILL.md` frontmatter from `name: learn-via-repo` to `name: learn-via-repo-dev`, then install it with `npx skills add`. Two different names don't conflict.

### Q: Where do the generated teaching artifacts get saved?

The skill asks where to put them. Default is `~/Desktop/learning/{repo-name}/` — you can pick anywhere else. The artifacts are completely separate from the skill itself; they don't pollute the skills directory.

### Q: The skill calls WebSearch / WebFetch, but my agent doesn't support those. What now?

The skill's Phase 2 / 2C uses WebSearch + WebFetch to find candidate repos. If your agent doesn't have those tools, the skill falls back to:

1. Asking you to provide repo candidates yourself (paste GitHub URLs)
2. Using the seed candidates in `references/multi-domain-examples.md` as suggestions

But you lose the core "AI runs a real search and gives you vetted candidates to evaluate" step. If you can, use an agent with WebSearch (Claude Code / Cursor / Codex all support it).

---

## Feedback

Hit a problem while testing? See the feedback template in [TESTING.md](./TESTING.md), or [open an issue](https://github.com/CZYCW/learn-via-repo/issues/new).
