# alpharigel Agent Skills

Reusable skills for coding agents. Works with [Claude Code](https://docs.anthropic.com/en/docs/claude-code) and [OpenAI Codex CLI](https://github.com/openai/codex).

## Available Skills

| Skill | Description |
|-------|-------------|
| [ios-e2e-skill](https://github.com/alpharigel/ios-e2e-skill) | End-to-end iOS app testing — UI automation, simulator management, accessibility-driven interactions |
| [ios-feedback-skill](https://github.com/alpharigel/ios-feedback-skill) | Add an in-app feedback button with automatic GitHub issue creation |

## Setup

### Claude Code

Add this as a plugin marketplace, then install individual skills:

```
/plugin marketplace add alpharigel/agent-skills
/plugin install ios-e2e-skill
/plugin install ios-feedback-skill
```

Or install a skill directly by repo URL:

```
/plugin add https://github.com/alpharigel/ios-feedback-skill
```

Once installed, invoke a skill with its slash command (e.g. `/ios-feedback-button`).

### OpenAI Codex CLI

Codex uses the same `SKILL.md` format. To use these skills with Codex:

**Option 1 — Clone into your project's `.agents/skills/` directory:**

```bash
# From your project root
mkdir -p .agents/skills
git clone https://github.com/alpharigel/ios-e2e-skill.git .agents/skills/ios-e2e-skill
git clone https://github.com/alpharigel/ios-feedback-skill.git .agents/skills/ios-feedback-skill
```

Codex auto-discovers skills in `.agents/skills/` and makes them available via `$skill-name`.

**Option 2 — Copy just the SKILL.md into your project:**

```bash
mkdir -p .agents/skills/ios-feedback-button
curl -o .agents/skills/ios-feedback-button/SKILL.md \
  https://raw.githubusercontent.com/alpharigel/ios-feedback-skill/main/skills/ios-feedback-button/SKILL.md
```

**Option 3 — Use as a personal skill (all projects):**

Copy the skill directory to your Codex user config:

```bash
# Location varies by OS — check ~/.codex/ or Codex docs
cp -r ios-feedback-skill/skills/ios-feedback-button ~/.codex/skills/
```

Once available, invoke with `$ios-feedback-button` in any Codex session.

## Skill format

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

The `SKILL.md` file uses YAML frontmatter (`name`, `description`) followed by markdown instructions — this format is compatible with both Claude Code and Codex CLI.

## License

MIT
