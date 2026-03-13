# Contributing

Thanks for contributing! Here's how to add your stuff.

## Adding a Skill

1. Create a folder in `skills/` with your skill name (kebab-case)
2. Include a `SKILL.md` file — this is what Claude Code reads
3. Update the skills table in `README.md`
4. Note any dependencies (CLI tools, APIs, etc.) in your SKILL.md

## Adding a Prompt

1. Create a markdown file in `prompts/`
2. Include the raw prompt in a code block so people can copy-paste it
3. Add a brief explanation of what it does and when to use it

## Adding Config Examples

1. Add to `claude-config/`
2. Clearly mark what's an example vs. what's copy-paste ready
3. Redact any personal info (emails, API keys, paths)

## Guidelines

- **Keep it self-contained.** Each contribution should work on its own.
- **Document dependencies.** If it needs `yt-dlp` or an API key, say so upfront.
- **Note customization needed.** Mark what users need to change (paths, names, etc.).
- **Simple over clever.** If it needs a 20-step setup, simplify it first.
