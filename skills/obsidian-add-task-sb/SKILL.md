---
name: obsidian-add-task-sb
description: >
  Add a task to Rod's Second Brain Obsidian daily note. Use this skill ANY time Claude needs to add, capture,
  log, or suggest a task or follow-up for Rod — whether from a conversation, a briefing, an email
  review, or any other context. Always places the task in today's "Hopefully (~)" section and always
  appends [Claude] so Rod knows it came from Claude. Never add tasks to Priority or Maybe sections
  unless Rod explicitly asks. Trigger on any intent to "add a task", "remind me to", "don't forget to",
  "log this", "capture this", "add to my list", or whenever Claude proactively wants to suggest a follow-up action.
---

# Obsidian Add Task — Second Brain

Adds a Claude-generated task to Rod's Second Brain Obsidian daily note.

## Rules (always follow these)
- Section: always **"Hopefully (~)"** — never Priority or Maybe unless Rod explicitly asks
- Tag: always append **`[Claude]`** at the end
- Format: `- [ ] task description [Claude]`
- Note: today's `YYYY-MM-DD.md` in the Second Brain vault at `10 - Daily Notes/`

## Steps

### 0. Always confirm first
Before adding anything, ask Rod:
> "Want me to add *[task description]* to your daily note?"

Wait for confirmation before proceeding. Only add the task if Rod says yes.

### 1. Find today's note
```bash
# Try cowork VM path first, then local Mac path
VAULT=$(find /sessions/*/mnt/Documents/"Second Brain" -maxdepth 0 -type d 2>/dev/null | head -1)
if [ -z "$VAULT" ]; then
  VAULT="$HOME/Library/Mobile Documents/iCloud~md~obsidian/Documents/Second Brain"
fi
TODAY=$(date +%Y-%m-%d)
NOTE="$VAULT/10 - Daily Notes/$TODAY.md"
```

### 2. Check the note exists
If `$NOTE` doesn't exist, tell Rod and stop — don't create it (the rollover task handles that).

### 3. Add the task to the Hopefully section
Read the file, find the `**Hopefully (~)**` line, and insert the new task immediately after it
(before any existing tasks in that section so it appears at the top of Hopefully).

Use Python for reliability:
```bash
python3 - <<'EOF'
import re, os, glob
from datetime import date

# Try cowork VM path first, then local Mac path
vaults = glob.glob("/sessions/*/mnt/Documents/Second Brain")
if vaults:
    vault = vaults[0]
else:
    vault = os.path.expanduser("~/Library/Mobile Documents/iCloud~md~obsidian/Documents/Second Brain")

daily_notes_dir = os.path.join(vault, "10 - Daily Notes")
note_path = os.path.join(daily_notes_dir, f"{date.today().strftime('%Y-%m-%d')}.md")
task = "TASK_PLACEHOLDER"  # replace with actual task text

if not os.path.exists(note_path):
    print(f"Today's note does not exist: {note_path}")
    exit(1)

with open(note_path, "r") as f:
    content = f.read()

# Append at the END of the Hopefully section (before the next section header)
new_task_line = f"- [ ] {task} [Claude]\n"
lines = content.splitlines(keepends=True)

# Find the Hopefully header
hopefully_idx = None
for i, line in enumerate(lines):
    if "**Hopefully (~)**" in line:
        hopefully_idx = i
        break

if hopefully_idx is None:
    print("Could not find Hopefully section")
    exit(1)

# Find the end of the Hopefully section (next blank line followed by non-list content)
insert_idx = len(lines)
for i in range(hopefully_idx + 1, len(lines)):
    stripped = lines[i].rstrip()
    if stripped == "":
        # Check if next non-blank line is a new section (not a list item)
        for j in range(i + 1, len(lines)):
            next_stripped = lines[j].rstrip()
            if next_stripped == "":
                continue
            if not next_stripped.startswith("- ") and not next_stripped.startswith("* "):
                insert_idx = i  # insert before the blank line gap
                break
            break
        if insert_idx != len(lines):
            break

lines.insert(insert_idx, new_task_line)
content = "".join(lines)

with open(note_path, "w") as f:
    f.write(content)

print(f"✓ Task added to Hopefully section in {note_path}")
EOF
```

### 4. Confirm to Rod
Tell Rod the task was added to today's Hopefully list, e.g.:
> "Added to your Hopefully list: *follow up with Steve about ISO AI sec extension* `[Claude]`"

## Examples

**User says:** "remind me to call the dentist"
→ Adds: `- [ ] call the dentist [Claude]`

**User says:** "add a task to look into firecrawl CLI"
→ Adds: `- [ ] look into firecrawl CLI [Claude]`

**Claude proactively notices a follow-up needed:**
→ Adds without being asked, confirms to Rod what was added
