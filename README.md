# AI Toolkit

Prompts, skills, and configurations for Claude Code + Obsidian workflows. Built for people with ADHD who want AI to actually help them get things done.

## What's in here

| Folder | What it is |
|---|---|
| `obsidian-setup/` | Vault scaffold prompt — recreate the full Obsidian folder structure in one shot |
| `skills/` | Claude Code skills (SKILL.md files) you can drop into `~/.claude/skills/` |
| `prompts/` | Reusable prompts for common workflows |
| `claude-config/` | Example CLAUDE.md files, hooks, and configuration patterns |

## Quick Start

### Set up an Obsidian vault
1. Open Claude Code in an empty directory
2. Paste the prompt from [`obsidian-setup/vault-scaffold-prompt.md`](obsidian-setup/vault-scaffold-prompt.md)
3. Open the folder in Obsidian

### Install a skill
1. Copy the skill folder into `~/.claude/skills/`
2. It auto-appears in Claude Code's available skills on next session

## Skills

| Skill | What it does | Customization needed |
|---|---|---|
| `youtube-research` | Research a topic via YouTube transcripts, write a synthesized report | None — works out of the box (needs `yt-dlp`) |
| `excalidraw-diagram` | Create Excalidraw diagrams that argue visually, not just display info | None |
| `notebooklm` | Full Google NotebookLM API access — notebooks, sources, podcasts, artifacts | None (needs `notebooklm-py`) |
| `session-notes` | Capture what happened in a work session and save to project folder | None |
| `reflect` | End-of-day debrief — summarize intentions vs reality, reflection questions | Adapt vault paths |
| `start-project` | Load project context at session start from project.md + session notes | Adapt vault paths |
| `morning-briefing` | ADHD-friendly morning rundown — calendar, email, weather, tasks, headlines | Adapt paths, calendar, location |
| `obsidian-add-task` | Add a task to your daily note from any conversation | Adapt section names and paths |

## ADHD Design Principles

Everything here follows a few rules:

- **Done over perfect.** Capture over categorize. Simple over organized.
- **Zero maintenance.** If it needs upkeep, simplify it.
- **One recommendation, not five options.** Decision fatigue is real.
- **Small starter steps.** Under 5 minutes to build momentum.
- **No rigid systems.** "Usually" not "always."

## Contributing

PRs welcome! If you've built a useful Claude Code skill, prompt, or workflow:

1. Fork the repo
2. Add your contribution to the appropriate folder
3. Update the README table if adding a skill
4. Open a PR with a short description of what it does

Keep contributions self-contained and documented. Include a brief description of what customization (if any) is needed.

## License

MIT — use it, share it, remix it.
