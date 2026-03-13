---
name: session-notes
description: Save notes from the current session to a project's session-notes folder. Use this skill whenever the user types /sessionNotes, /session-notes, "save session notes", "save notes for this session", "log what we did", or "capture this session". Captures a summary of the session — what was worked on, files changed, decisions made, and next steps — and writes it to a dated markdown file in the appropriate project's session-notes/ folder.
---

# Session Notes

Your job is to capture the current session as a useful, scannable note and save it to the right place. Think of this as writing a handoff document for your future self.

## Step 1 — Ask Rod which project folder to save to

**Always ask before saving** — never infer silently. First list existing project folders:

```bash
# Try cowork VM path first, then local Mac path
ls /sessions/*/mnt/Documents/"Second Brain"/"20 - Projects"/ 2>/dev/null || ls "$HOME/Library/Mobile Documents/iCloud~md~obsidian/Documents/Second Brain/20 - Projects/" 2>/dev/null
```

Then ask:
> "Which project should I save these notes to? Existing projects: [list them]. Or tell me a new project name and I'll create it."

Wait for Rod's answer, then use `Second Brain/20 - Projects/[chosen-project]/` as the target.

If no projects folder exists yet, suggest creating one and confirm before proceeding.

## Step 2 — Ensure the project folder exists

The notes go directly in the project root `[project-folder]/`. Create the project folder if it doesn't exist:

```bash
mkdir -p "[project-folder]"
```

## Step 3 — Write the session note

Create a markdown file in the project root named `session-note-YYYY-MM-DD-[short-topic-slug].md` (e.g., `session-note-2026-03-09-travel-dashboard-documents.md`).

**Derive the topic slug** from the main theme of the session — 2-4 words in kebab-case. If the session covered many unrelated things, use `general` or `mixed`.

**Template:**

```markdown
# Session Notes — [Date] · [Short Title]

**Date:** [Full date, e.g., Mon March 9, 2026]
**Project:** [Folder or project name]
**Session focus:** [One sentence summary of what this session was about]

---

## What was accomplished

[Prose or bullets — what got done. Be specific. Mention confirmation numbers, file names, feature names, etc. if relevant.]

## Files created or modified

[List key files touched, relative to the project folder. One line each with what changed.]

## Key decisions & context

[Anything important that shaped the work: why a certain approach was chosen, what was discovered, what changed from the original plan. This is the "why" that won't be obvious from the files alone.]

## Pending / next steps

[What's still in flight, what should happen next, any known issues or follow-up items.]

## Notes for next session

[Anything the next session needs to know to pick up smoothly — gotchas, active state, where things stand.]
```

**Writing guidelines:**
- Be concrete. File names, confirmation numbers, exact values are better than vague descriptions.
- Keep each section tight. The goal is a 60-second read that puts someone in context, not a full transcript.
- Skip sections that have nothing meaningful to say (e.g., "Pending" can be omitted if everything is done).
- Use the session history to fill in the content — don't ask the user for information you can derive yourself.

## Step 4 — Confirm

Tell the user where you saved the notes (path relative to their folder), and give a one-line summary of what you captured.

Example:
> Saved session notes to `session-note-2026-03-09-travel-dashboard-documents.md` — covers the Chicago trip dashboard update, 4 HTML confirmation files, and the pending CLAUDE.md fix.
