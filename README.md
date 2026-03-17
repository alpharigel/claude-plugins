# Jay's Workflow and Agent Skills

A product manager's toolkit for agentic coding — reusable skills and an evolving workflow for turning ideas into tangible solutions with AI coding agents.

**📋 [Read the full PM-AI Workflow →](WORKFLOW.md)** — my current best process for going from idea to shipped feature, kept up to date as tools evolve.

If you're coming from my [Substack](https://jaydermody.substack.com), welcome! The workflow doc is the best place to start. The skills below are the reusable building blocks that make it all go faster.

---

## Available Skills

| Skill | Description |
|-------|-------------|
| [ios-e2e-skill](https://github.com/alpharigel/ios-e2e-skill) | End-to-end iOS app testing — UI automation, simulator management, accessibility-driven interactions |
| [ios-feedback-skill](https://github.com/alpharigel/ios-feedback-skill) | Add an in-app feedback button with automatic GitHub issue creation |

Have a skill you'd like to share? Open a PR or issue — contributions welcome.

---

## Setup

Each skill uses a `SKILL.md` file with YAML frontmatter — a format supported natively by all major coding agents. Pick yours below.

### Claude Code

Add as a plugin marketplace, then install individual skills:

```
/plugin marketplace add alpharigel/agent-skills
/plugin install ios-e2e-skill
/plugin install ios-feedback-skill
```

Or install a skill directly by repo URL:

```
/plugin add https://github.com/alpharigel/ios-feedback-skill
```

Invoke with `/skill-name` (e.g., `/ios-feedback-button`).

<details>
<summary><strong>OpenAI Codex CLI</strong></summary>

Clone into your project's `.agents/skills/` directory:

```bash
mkdir -p .agents/skills
git clone https://github.com/alpharigel/ios-e2e-skill.git .agents/skills/ios-e2e-skill
git clone https://github.com/alpharigel/ios-feedback-skill.git .agents/skills/ios-feedback-skill
```

Or copy just the SKILL.md:

```bash
mkdir -p .agents/skills/ios-feedback-button
curl -o .agents/skills/ios-feedback-button/SKILL.md \
  https://raw.githubusercontent.com/alpharigel/ios-feedback-skill/main/skills/ios-feedback-button/SKILL.md
```

For a personal skill (all projects): copy to `~/.codex/skills/`.

Invoke with `$skill-name` (e.g., `$ios-feedback-button`).

</details>

<details>
<summary><strong>Gemini CLI</strong></summary>

Clone into your project's `.gemini/skills/` directory:

```bash
mkdir -p .gemini/skills
git clone https://github.com/alpharigel/ios-e2e-skill.git .gemini/skills/ios-e2e-skill
git clone https://github.com/alpharigel/ios-feedback-skill.git .gemini/skills/ios-feedback-skill
```

Or copy just the SKILL.md:

```bash
mkdir -p .gemini/skills/ios-feedback-button
curl -o .gemini/skills/ios-feedback-button/SKILL.md \
  https://raw.githubusercontent.com/alpharigel/ios-feedback-skill/main/skills/ios-feedback-button/SKILL.md
```

For a personal skill (all projects): copy to `~/.gemini/skills/`.

Invoke with `/skill-name` (e.g., `/ios-feedback-button`).

</details>

<details>
<summary><strong>Cursor</strong></summary>

Clone into your project's `.cursor/skills/` directory:

```bash
mkdir -p .cursor/skills
git clone https://github.com/alpharigel/ios-e2e-skill.git .cursor/skills/ios-e2e-skill
git clone https://github.com/alpharigel/ios-feedback-skill.git .cursor/skills/ios-feedback-skill
```

Or copy just the SKILL.md:

```bash
mkdir -p .cursor/skills/ios-feedback-button
curl -o .cursor/skills/ios-feedback-button/SKILL.md \
  https://raw.githubusercontent.com/alpharigel/ios-feedback-skill/main/skills/ios-feedback-button/SKILL.md
```

For a personal skill (all projects): copy to `~/.cursor/skills/`.

Invoke with `/skill-name` (e.g., `/ios-feedback-button`).

</details>

---

## Skill Format

Each skill repo follows this structure:

```
skill-repo/
  .claude-plugin/
    plugin.json         # Plugin metadata (Claude Code)
  skills/
    skill-name/
      SKILL.md          # Skill instructions (YAML frontmatter + markdown)
      scripts/          # Optional helper scripts
  README.md
  LICENSE
```

The `SKILL.md` file uses YAML frontmatter (`name`, `description`) followed by markdown instructions. This format works across all major agents — write once, use everywhere.

| Agent | Project skills dir | Personal skills dir | Invoke |
|-------|-------------------|---------------------|--------|
| Claude Code | `.claude/skills/` | `~/.claude/skills/` | `/skill-name` |
| Codex CLI | `.agents/skills/` | `~/.codex/skills/` | `$skill-name` |
| Gemini CLI | `.gemini/skills/` | `~/.gemini/skills/` | `/skill-name` |
| Cursor | `.cursor/skills/` | `~/.cursor/skills/` | `/skill-name` |

---

## License

MIT
