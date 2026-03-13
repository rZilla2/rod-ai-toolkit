# Obsidian Vault Scaffold Prompt

> Give this prompt to Claude Code (or any AI assistant) to create a PARA-inspired Obsidian vault from scratch.

## The Prompt

```
Create an Obsidian vault using a PARA-inspired folder structure. Create all folders
and the daily note template exactly as specified below. Do NOT create any notes
other than the template.

## Folder Structure

Create these top-level folders inside the current directory:

- 00 - Inbox/
- 10 - Daily Notes/
- 20 - Projects/
- 30 - Areas/
- 40 - Resources/
- 50 - Archives/
- 60 - People/
- 70 - Ideas/
- ~Attachments/
- ~System/
  - ~System/scripts/
  - ~System/skills/
  - ~System/workflows/
- ~Templates/

## Daily Note Template

Create this file at `~Templates/Daily Note.md`:

#### **Intention**
*

#### **Agenda**

#### **Priority (1-3 with top-top highlighted)**
 - [ ]
 - [ ]
 - [ ]

#### **Maybe (3-5)**
- [ ]
- [ ]
- [ ]

#### **Hopefully (~)**
- [ ]

### **### Dump ### ###

## What each folder is for

| Folder | Purpose |
|---|---|
| 00 - Inbox | Unsorted captures — everything lands here first |
| 10 - Daily Notes | One note per day (YYYY-MM-DD.md), created from template |
| 20 - Projects | Active projects, one subfolder each |
| 30 - Areas | Ongoing responsibilities (health, finances, career, etc.) |
| 40 - Resources | Reference material, how-tos, saved articles |
| 50 - Archives | Completed or inactive items moved here |
| 60 - People | Contact/relationship notes |
| 70 - Ideas | Loose ideas, someday/maybe |
| ~Attachments | Images, PDFs, embedded files |
| ~System | Scripts, skills, workflows, automation configs |
| ~Templates | Obsidian templates (Templater or core Templates plugin) |

The ~ prefix keeps system folders sorted to the bottom in Obsidian's file explorer.
The numbered prefixes enforce visual sort order for the main folders.

After creating, confirm the structure with a tree listing.
```

## Why this structure?

- **PARA-inspired**: Projects, Areas, Resources, Archives — Tiago Forte's organizational framework, extended with Inbox, People, and Ideas
- **Numbered prefixes** (00-70): Forces consistent sort order across devices and file explorers
- **~ prefix** for system folders: Pushes utility folders to the bottom, out of the way
- **Daily Note template**: Designed for ADHD-friendly task management — intention setting, tiered priorities, and a dump zone for brain overflow

## Recommended Obsidian Plugins

After creating the vault, install these community plugins:

| Plugin | Why |
|---|---|
| Templater | Powers the daily note template with dynamic dates/logic |
| Tasks | Query and filter tasks across your entire vault |
| Omnisearch | Fast full-text search across all notes |
