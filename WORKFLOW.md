# My AI Product Management Workflow

My current best workflow for unlocking AI agents to turn ideas into tangible solutions.

Pull requests welcome! Let's build a community of joy through creation of awesome things.

---

## What You Need

**A coding agent subscription.** I'm using Claude Code with a Max subscription. It has enough tokens that if I run out, I really should go touch grass. Codex is performing quite well on coding benchmarks, and I'm sure in the length of time it would take an apple to go bad, the tools will all shuffle again. But any way you slice it, you need a good coding agent — pick one, pay for the highest quality model available, and start cooking.

**A development environment.** A computer with a terminal. I'll share my specific setups for Windows and Mac below, but the important thing is that it works for you. Spend 80% of your time working on your projects in your current most effective workflow, and 20% looking to optimize it. Things are changing fast enough that it's always worth trying new approaches alongside just getting stuff done.

**An idea you want to see realized.** A new website, an iOS app, or maybe just a better workflow for your day-to-day — it's all possible now.

---

## Computer Setup

There's no single right answer here, so I'll share what's worked for me.

### Windows

WSL (Windows Subsystem for Linux) is the key unlock. While Claude can write PowerShell, its native language is Bash, and even after being told it's in a Windows environment, it will often default to Bash syntax before self-correcting. You can install WSL directly from the Microsoft Store, then download Ubuntu as the most commonly used OS for this type of workflow.

Microsoft's Terminal app works well enough for me right now. Install it from the Store if you don't have it, set Ubuntu as your default profile, and fix the color scheme in settings — darken up the purple and make the blues lighter, and your eyes will thank you.

### Mac

macOS is Unix-based, so the terminal works natively without any special configuration. **Homebrew** is the tool of choice for installing additional software — it should be available by default, but if not, install it from [brew.sh](https://brew.sh).

I recently switched to **Ghostty** for my terminal app. I got tired of juggling too many windows. Full screen, split into quarters, with reasonable font sizes lets me see everything that's going on without constantly switching contexts.

---

## Coding Agent

I've been using **Claude Code** at both home and work and love it. That said, Codex has been performing well in coding benchmarks, and Snowflake just showed me their new Cortex environment which looks promising. Gemini and Cursor also have CLIs for their agents, so we're rich with options.

Follow the instructions from your provider's website to install the CLI into your environment.

---

## Tech Stack

Here are the specific choices I've landed on and why. These will evolve — that's the nature of moving fast right now — but each one has earned its spot through real project work.

### Analytical Environment / Business Logic

**Python** remains the best general-purpose language for data work and business logic, and it's the language AI agents write most fluently.

**uv** for environment management. It's dramatically faster than pip or virtualenv, and keeps dependency resolution clean. Note: Claude likes to fall back to pip by default, so make sure to tell it to use uv.

**FastAPI** for both RESTful and WebSocket connections. It's lightweight, async-native, and agents can scaffold a working API in minutes.

### Web App

**React 19 + Next.js 15** — the ecosystem support is deep, agents know it cold, and server components give you a clean architecture for data-heavy PM tools.

**TypeScript** — the type safety catches many agent mistakes before they become runtime bugs.

**Tailwind CSS 4 + shadcn/ui** for polished, consistent component design without spending hours on custom styling.

**Vitest** for testing — fast, compatible with the React ecosystem, and agents write good Vitest specs.

### iOS App

**Swift + SwiftUI** — SwiftUI's declarative syntax maps well to how agents think about UI.

**Axe** for automated testing — this is the key unlock for agents to verify iOS apps are actually working correctly in the simulator.

**TestFlight + GitHub Actions** for dev deployment. Push to main, Actions builds and uploads, TestFlight notifies you when it's ready.

### Infrastructure

**GitHub** for repository and issue management. Issues are central to the parallel development workflow — more on this below.

**dotenvx** for secret management. It encrypts and decrypts environment variables so you can check them directly into your repo. You end up with just a single decrypt key set across your various environments, which is much cleaner than managing .env files everywhere.

**Railway** for cloud hosting. The CLI is great because after giving Claude access to the API key, it handles all the configuration. After a push to main, changes show up on the live site within two minutes.

---

## Development Process

The core loop is: **create an issue → spin up a worktree → let the agent investigate, plan, implement, test, and PR → review PR and merge**

### Starting a new project

Create a new directory for each project:

```bash
mkdir -p ~/dev/project-name
cd ~/dev/project-name
```

### Working on a feature

Each feature or bug fix starts as a GitHub Issue. When it's time to work on one, I launch Claude Code in a dedicated worktree for that issue:

```bash
dotenvx run -- claude -w "issue-42" "Please investigate GitHub issue #42..."
```

The `-w` flag creates a git worktree, so each issue gets its own isolated branch without touching your main working directory. `dotenvx run` injects your encrypted environment variables so the agent has access to live API keys for testing.

Here's the full prompt I use:

```
Please investigate GitHub issue #42 for this repo and go into plan mode to 
address it. Use files from this worktree (don't go back to the base directory) 
to research the codebase. Don't use multiline commands or scripts, or command 
substitution or redirection — use ./tmp instead. Search online to research 
implementation paths, and use context7 to investigate libraries. Make sure to 
include verification steps in the plan. Use TDD, feature flags, and e2e 
testing. Once the implementation is complete, run the verification steps 
yourself, starting dev servers on new ports as needed. This environment has 
access to live API keys so make sure to unset these variables when writing 
the e2e configuration files, but use them to verify everything is working 
yourself. Once verified, please commit, push to origin, and create a pull 
request. Mark in the pull request the verification tests you ran.
```

Replace `#42` with whatever issue number you're working on. The prompt is designed to keep the agent on rails: it plans before coding, tests its own work, and produces a PR you can review rather than a pile of uncommitted changes.

### Scaling to parallel agents

This is where it gets fun. Because each issue runs in its own worktree, you can have multiple agents working simultaneously on different features. I regularly run three to four agents in parallel — one per terminal pane in Ghostty — each tackling a different issue. My job becomes reviewing implementation plans and pull requests rather than writing code.

With a fairly extensive "allowed tools" list (Python, uv, Node and npm commands) and accept-edits enabled, I rarely need to hit "yes" for the agent to progress. I'm currently enhancing this workflow to run development in isolated Docker containers and use `--dangerously-skip-permissions` for fully autonomous operation.

---

*This document is kept up to date as my workflow evolves. If you've found something that works better, please open an issue — let's figure this out together.*
