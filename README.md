# 🎯 Soc Ops — VS Code GitHub Copilot Agent Lab

> **A hands-on workshop where you build a Social Bingo game using VS Code's Agent Mode.**  
> Players find real people matching icebreaker prompts on a 5×5 bingo board — first to 5-in-a-row wins.

**Stack:** Python 3.13 · FastAPI · Jinja2 · HTMX · uv &nbsp;|&nbsp; **Level:** Intermediate &nbsp;|&nbsp; **Duration:** ~1 hour

---

## 🧠 What You'll Learn

| # | Skill | What you'll do |
|---|-------|----------------|
| 1 | **Context Engineering** | Teach AI about your codebase with custom instructions |
| 2 | **Agentic Primitives** | Use Copilot CLI sessions, cloud agents, and custom workflows |
| 3 | **Design-First Development** | Let AI iterate on UI while you steer the creative vision |
| 4 | **Test-Driven Development** | Use TDD agents to reliably build and verify new features |

---

## 📚 Lab Guide

| Part | Title | Time |
|------|-------|------|
| [**00 — Overview**](https://copilot-dev-days.github.io/agent-lab-python/docs/step.html?step=00-overview) | Prerequisites & checklist | — |
| [**01 — Setup**](https://copilot-dev-days.github.io/agent-lab-python/docs/step.html?step=01-setup) | Context Engineering | 15 min |
| [**02 — Design**](https://copilot-dev-days.github.io/agent-lab-python/docs/step.html?step=02-design) | Design-First Frontend | 15 min |
| [**03 — Quiz Master**](https://copilot-dev-days.github.io/agent-lab-python/docs/step.html?step=03-quiz-master) | Custom Agent Workflows | 10 min |
| [**04 — Multi-Agent**](https://copilot-dev-days.github.io/agent-lab-python/docs/step.html?step=04-multi-agent) | Multi-Agent Development | 20 min |

> 📝 Offline? All guides are available in the [`workshop/`](workshop/) folder.

---

## ✅ Prerequisites

Before you start, make sure you have:

- [ ] **VS Code v1.107+** (no pending updates)
- [ ] **GitHub Copilot** (Free, Pro, Business, or Enterprise)
- [ ] **Git** installed
- [ ] **Python 3.13** and **[uv](https://docs.astral.sh/uv/)** installed
- [ ] Chat panel open with Agent Mode ready

> 💡 **Tip:** Use the included [Dev Container](.devcontainer) for a fully pre-configured environment — no local setup needed.

> ⚠️ **Free-tier users:** Cloud Agents are not available on free-tier Copilot plans. Alternative instructions are provided wherever Cloud Agents are used.

---

## 🚀 Getting Started

**[→ Start with Part 00: Overview & Checklist](https://copilot-dev-days.github.io/agent-lab-python/docs/step.html?step=00-overview)**

```bash
# After cloning your repo, install dependencies and run the app:
uv sync
uv run uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

---

## 💡 Pro Tips

1. **Keep the browser open** — watch live updates as Copilot edits your code
2. **Commit often** — save working states so you can always roll back
3. **Use Checkpoints** — the chat panel's Undo/Checkpoint feature is your safety net
4. **Iterate on plans** — refine your prompt 2–3 times before asking Copilot to implement
