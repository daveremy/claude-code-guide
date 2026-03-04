# Claude Code — Quick Reference Cheat Sheet

## Windows Users: WSL Required

Claude Code runs on Linux/macOS. On Windows, you need **WSL (Windows Subsystem for Linux)**.

```powershell
# In PowerShell (as Administrator):
wsl --install

# Restart your PC, then open "Ubuntu" from Start menu
# You're now in a Linux terminal — all commands below run here
```

> **Important:** Always work inside WSL, not in PowerShell/CMD. Your projects live in the Linux filesystem (e.g., `~/projects/`), not on `/mnt/c/`. This avoids performance issues and path problems.

---

## Prerequisites

| Tool | Install (macOS) | Install (WSL/Ubuntu) | What it is |
|------|----------------|----------------------|------------|
| **Node.js** | `brew install node` | `curl -fsSL https://deb.nodesource.com/setup_lts.x \| sudo -E bash - && sudo apt-get install -y nodejs` | Required runtime (v18+) |
| **Git** | `brew install git` | `sudo apt-get install git` | Version control |
| **GitHub CLI** | `brew install gh` | `sudo apt-get install gh` (or see [gh install docs](https://github.com/cli/cli/blob/trunk/docs/install_linux.md)) | Repos, PRs, issues from terminal |
| **Claude Code** | `npm install -g @anthropic-ai/claude-code` | Same | AI coding agent — Claude Opus/Sonnet |
| **Codex CLI** | `npm install -g @openai/codex` | Same | OpenAI's agent — for code review |
| **Gemini CLI** | Check latest install method | Same | Google's AI CLI — for code review |

> **Model knowledge cutoff**: Claude, Codex, and Gemini all have training data cutoff dates. They may not know the latest library versions or APIs. Always specify "use the latest stable version" for dependencies.

---

## Bootstrapping a Project from This Repo

This repo is your reference guide. Here's how to use it to kick off new projects:

```bash
# 1. Create your project directory
mkdir my-project && cd my-project

# 2. Start Claude Code, pointing it at this guide repo for context
claude --dangerously-skip-permissions

# 3. Your first prompt — tell Claude to use this repo as a reference:
```

**Paste this as your first prompt (edit the description):**

```
Read the bootstrapping guide at https://github.com/daveremy/claude-code-guide
for workflow and best practices context.

I want to build: [YOUR PROJECT DESCRIPTION HERE]

Features:
- [feature 1]
- [feature 2]

Tech stack: [your preferences, or "suggest appropriate tech"]
Use latest stable versions of all dependencies.

Please enter plan mode and create an implementation plan.
Follow the workflow described in the guide.
```

> **Tip:** After cloning this repo locally, you can also reference the files directly:
> `Read the guide at ~/claude-code-guide/claude-code-guide.md for workflow context.`

---

## Starting a Project (Quick Version)

```bash
# 1. Create and enter project directory
mkdir my-project && cd my-project

# 2. Start Claude Code (skip permission prompts for solo work)
claude --dangerously-skip-permissions

# 3. Inside Claude, your first prompt should describe the project
#    and ask to enter plan mode (see Workflow below)
```

---

## Essential Claude Code Commands

| Command | What it does |
|---------|-------------|
| `claude` | Start Claude Code in current directory |
| `claude --dangerously-skip-permissions` | Start without permission prompts |
| `/plan` | Enter plan mode (design before coding) |
| `/commit` | Commit staged changes with AI-generated message |
| `/simplify` | Run code simplifier — finds improvements |
| `/help` | Show all available commands |
| `Ctrl+C` | Cancel current operation |
| `Escape` | Back out / cancel |

---

## The Workflow (memorize this)

```
 1. DESCRIBE  →  Write project/feature description, ask for plan mode
 2. PLAN      →  Claude creates implementation plan
 3. REVIEW    →  Get AI reviews from Codex + Gemini on the plan
 4. LOOP      →  Revise plan until all reviewers approve
 5. BUILD     →  Claude implements the approved plan
 6. SIMPLIFY  →  Run /simplify, loop until clean
 7. REVIEW    →  AI code reviews with Codex + Gemini
 8. LOOP      →  Revise code until all reviewers approve
 9. TEST      →  Ensure tests exist and pass
10. VERIFY    →  Manual testing with provided instructions
11. COMMIT    →  Commit with clear message
```

---

## Git Practices

```bash
# Commit early and often
# Use clear, descriptive commit messages
# Create a repo on GitHub early
git init
gh repo create my-project --public --source=. --push

# Good commit rhythm:
#   - After plan is approved
#   - After each feature/component works
#   - After code review fixes
#   - After tests pass
```

---

## Key Files

| File | Purpose |
|------|---------|
| `CLAUDE.md` | Instructions for Claude — project context, conventions, rules |
| `README.md` | Project documentation — also helps AI understand your project |
| `ROADMAP.md` | For bigger projects — tracks phases and progress |

---

## CLAUDE.md Starter Template

```markdown
# Project Name

## Description
[What this project does in 2-3 sentences]

## Tech Stack
- [Language/framework]
- [Key dependencies — specify versions if needed]

## Conventions
- [Coding style preferences]
- [File organization rules]

## Rules
- Use latest stable versions of all dependencies
- Write tests for all new features
- Keep functions small and focused
```

---

## Prompt Tips

| Do this | Not this |
|---------|----------|
| "Build a REST API with Express that handles user CRUD operations" | "Build an API" |
| "Enter plan mode and design a todo app with React and local storage" | "Make me a todo app" |
| "Use the latest stable version of Next.js" | "Use Next.js" (may use outdated version) |
| "Break this into 3 phases: auth, dashboard, settings" | Trying to build everything at once |

---

## When AI Doesn't Know Something

- **Outdated dependency info** → Tell Claude: "use latest stable version of X"
- **New API/framework features** → Use Context7: Claude can fetch live docs
- **Conflicting advice from reviewers** → You make the final call
- **Hallucinated APIs** → Always verify with official docs if something looks off

---

## Big Project Strategy

```
Phase 1: Core functionality     → build, review, commit
Phase 2: Secondary features     → build, review, commit
Phase 3: Polish & edge cases    → build, review, commit
Phase 4: Testing & documentation → test, document, commit

Update ROADMAP.md after completing each phase.
```

---

## WSL Tips

- **Always work in the Linux filesystem** (`~/projects/`), not `/mnt/c/` — much faster
- **VS Code integration**: Install "Remote - WSL" extension, then `code .` from WSL opens VS Code connected to WSL
- **Copy/paste in terminal**: `Ctrl+Shift+C` / `Ctrl+Shift+V` (not `Ctrl+C`/`Ctrl+V`)
- **Access Windows files if needed**: They're at `/mnt/c/Users/YourName/`
- **If npm permissions fail**: `sudo chown -R $(whoami) ~/.npm`

---

*Generated with Claude Code — March 2026*
