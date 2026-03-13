---
name: reflect
description: End-of-day reflection and debrief. Reads today's daily note, summarizes what happened vs what was planned, asks a few reflection questions, and saves a debrief file. Use when Rod says "/reflect", "end of day", "daily debrief", "how'd today go", "wrap up the day", or similar intent to close out the day.
user_invocable: true
---

# Daily Reflect — End of Day Debrief

## What you do

You help Rod close out his day with a quick, ADHD-friendly reflection. No guilt, no overwhelm — just an honest snapshot.

## Steps

### 1. Read today's daily note

Read the daily note at:
```
~/Library/Mobile Documents/iCloud~md~obsidian/Documents/Second Brain/10 - Daily Notes/YYYY-MM-DD.md
```
Use today's date.

### 2. Generate the debrief summary

Present this to Rod in chat (don't save yet — he may want to adjust):

**Intentions** — List what was in the Intention section. For each, note whether it was addressed today or not. No judgment.

**Agenda** — List agenda items. Note which happened.

**Tasks completed** — List all tasks checked off today across all sections (Priority, Maybe, Hopefully, Claude/AI).

**Tasks still open** — List unchecked tasks, grouped by section. Keep it brief — just the task text, no commentary.

**Quick stats** — e.g., "7 of 12 tasks done" or "3 of 5 agenda items completed"

### 3. Ask reflection questions

Ask Rod these questions (he can answer briefly or skip any):

1. What's one thing that went well today?
2. What felt hardest or got avoided?
3. Anything you want to carry forward to tomorrow with extra priority?

Wait for Rod's answers before proceeding.

### 4. Save the debrief

After Rod responds (or says skip/save), write the debrief file to:
```
~/Library/Mobile Documents/iCloud~md~obsidian/Documents/Second Brain/10 - Daily Notes/YYYY-MM-DD-reflect.md
```

Use this format:

```markdown
# Daily Reflect — YYYY-MM-DD

## Intentions
- [list with status]

## Agenda
- [list with status]

## Completed
- [checked off tasks]

## Still Open
- [unchecked tasks by section]

## Stats
[quick stats line]

## Reflections
**Went well:** [Rod's answer or skipped]
**Hardest/avoided:** [Rod's answer or skipped]
**Carry forward:** [Rod's answer or skipped]
```

### 5. Confirm

Tell Rod the file is saved. Keep it brief. Wish him a good night if it's evening.

## Rules

- Keep everything short and scannable. Bullets, not paragraphs.
- No guilt about unfinished tasks. Frame as "still open" not "incomplete" or "failed."
- Don't add tasks, suggestions, or process improvements unless Rod asks.
- If Rod skips the questions, that's fine — save without the reflections section.
- **Never use checkbox syntax** (`- [ ]` or `- [x]`) in the debrief file. Use plain list items (`-`). Checkboxes cause the daily note rollover script to pick up tasks as duplicates.
