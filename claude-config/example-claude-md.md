# Example CLAUDE.md for an Obsidian Vault

> Drop a file named `CLAUDE.md` in your vault root. Claude Code reads it at the start of every session.

```markdown
# Claude Instructions

## Identity
- User: [Your Name] ([your@email.com])
- Obsidian vault path: [path to your vault]
- Daily notes format: YYYY-MM-DD.md in `10 - Daily Notes/`

## Vault Structure
Second Brain/
├── 00 - Inbox/          # Unsorted captures
├── 10 - Daily Notes/    # YYYY-MM-DD.md daily notes
├── 20 - Projects/       # Active projects (one subfolder each)
├── 30 - Areas/          # Ongoing responsibilities
├── 40 - Resources/      # Reference material
├── 50 - Archives/       # Completed/inactive items
├── 60 - People/         # Contact notes
├── 70 - Ideas/          # Loose ideas, someday/maybe
├── ~Attachments/        # Images, PDFs, etc.
├── ~System/             # Scripts, config, skills
└── ~Templates/          # Obsidian templates

## Communication Style
- Lead with the answer, not the reasoning
- Bullets, short sentences, white space
- One recommendation, not five options
- Keep it concise — no walls of text

## Skills
| Skill | What it does |
|---|---|
| (list your installed skills here) |

## Projects
Scan `20 - Projects/` to discover active projects.
```

## Tips

- Keep it under 200 lines. Claude reads this every session — bloat slows things down.
- Put project-specific instructions in `20 - Projects/[project]/CLAUDE.md` instead of the root file.
- Update it when your workflow changes. Stale instructions are worse than none.
