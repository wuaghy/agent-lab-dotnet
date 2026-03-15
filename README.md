# Soc Ops

> **Social Bingo for in-person mixers** — find people who match the squares and get 5 in a row.
> Also a hands-on lab for building with **GitHub Copilot agents** in VS Code.

<div align="center">

[![Play the Game](https://img.shields.io/badge/🎮_Play_the_Game-Live_Demo-4f46e5?style=for-the-badge)](https://dotnet-presentations.github.io/vscode-github-copilot-agent-lab/)
[![Lab Guide](https://img.shields.io/badge/📚_Lab_Guide-Read_Online-0ea5e9?style=for-the-badge)](https://dotnet-presentations.github.io/vscode-github-copilot-agent-lab/docs/)

</div>

---

```
  ┌───────────────────────────────────────────────────┐
  │                 🎮  SOC OPS  🎮                   │
  │           Social Bingo — Find Your People         │
  ├─────────┬─────────┬─────────┬─────────┬─────────┤
  │  Loves  │  Early  │  Side   │  Reads  │  Has a  │
  │  spicy  │  riser  │  hustle │  paper  │   pet   │
  │  food   │    ✓    │         │  books  │         │
  ├─────────┼─────────┼─────────┼─────────┼─────────┤
  │  Used   │ Speaks  │         │  Built  │  Bikes  │
  │  Linux  │   2+    │  FREE   │  a CLI  │   to    │
  │         │  langs  │  SPACE  │  tool   │  work   │
  ├─────────┼─────────┼─────────┼─────────┼─────────┤
  │  Night  │  Has a  │  Wrote  │  Loves  │  Moved  │
  │   owl   │  mech   │    a    │  dark   │  city   │
  │   🦉    │   kb    │  blog   │  mode   │   ✈    │
  └─────────┴─────────┴─────────┴─────────┴─────────┘
               Tap a square. Find a match.
```

---

## What is this?

**Soc Ops** is a Blazor WebAssembly app that turns networking events into a game. Each player gets a randomised 5×5 bingo card filled with icebreaker prompts — *"has a mechanical keyboard"*, *"moved cities for a job"*, *"loves spicy food"* — and races to find real people who match each square.

Pull it up on your phone, hand it to someone at your next meetup or conference, and watch conversations start themselves.

---

## The Lab

This repo is also a **GitHub Copilot Agent Lab** — a structured workshop that teaches you to build with agentic AI workflows:

| # | Part | What You Build | Time |
|---|------|----------------|------|
| [01](https://dotnet-presentations.github.io/vscode-github-copilot-agent-lab/docs/step.html?step=01-setup) | **Setup & Context Engineering** | Workspace instructions, linting agent, README | 15 min |
| [02](https://dotnet-presentations.github.io/vscode-github-copilot-agent-lab/docs/step.html?step=02-design) | **Design-First Frontend** | Full UI redesign using Plan Mode | 15 min |
| [03](https://dotnet-presentations.github.io/vscode-github-copilot-agent-lab/docs/step.html?step=03-quiz-master) | **Custom Quiz Master** | Agent that generates themed question sets | 10 min |
| [04](https://dotnet-presentations.github.io/vscode-github-copilot-agent-lab/docs/step.html?step=04-multi-agent) | **Multi-Agent Development** | TDD + UX review running in parallel | 20 min |

> Offline? All guides are in the [`workshop/`](workshop/) folder.

---

## Quick Start

**Prerequisites:** [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0), VS Code, GitHub Copilot

```bash
# Clone and open
git clone https://github.com/dotnet-presentations/vscode-github-copilot-agent-lab
cd vscode-github-copilot-agent-lab
code .

# Run the app
cd SocOps && dotnet run
# → http://localhost:5166
```

Then open the **Chat panel** in VS Code and run `/setup` to verify your environment.

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Language | C# 13 / .NET 10 |
| Framework | Blazor WebAssembly |
| Styling | Custom utility CSS (no npm, no CDN) |
| Persistence | `localStorage` via JSInterop |
| CI/CD | GitHub Actions → GitHub Pages |
| AI Tooling | GitHub Copilot (agents, instructions, prompts) |

---

## Agents Included

Four custom Copilot agents ship with this repo, each demonstrating a different agentic pattern:

| Agent | What it does |
|-------|-------------|
| **TDD Supervisor** | Orchestrates a red → green → refactor loop across sub-agents |
| **Quiz Master** | Generates themed icebreaker questions and writes them to `Questions.cs` |
| **UI Review** | Opens a Playwright browser, screenshots the app, and gives design feedback |
| **Pixel Jam** | Iterates on visual design with Plan Mode, applying a chosen theme end-to-end |

---

<div align="center">

Made for VS Code Dev Days &nbsp;·&nbsp; Blazor &nbsp;·&nbsp; .NET 10 &nbsp;·&nbsp; GitHub Copilot

</div>
