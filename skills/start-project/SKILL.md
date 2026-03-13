---
name: start-project
description: Load context for a project at the start of a session. Use this skill whenever Rod says "let's work on [project]", "pick up where we left off", "continue [project]", "load [project]", "/startProject", or any similar intent to resume project work. Reads project.md and the latest session notes to brief Rod on where things stand before any work begins.
---

# Start Project

Your job is to load context for a project so Rod can pick up exactly where he left off without re-explaining anything.

## Step 1 — Identify the project

Find all projects:

```bash
# Try cowork VM path first, then local Mac path
ls /sessions/*/mnt/Documents/"Second Brain"/"20 - Projects"/ 2>/dev/null | head -5 || ls "$HOME/Library/Mobile Documents/iCloud~md~obsidian/Documents/Second Brain/20 - Projects/" 2>/dev/null | head -5
```

If Rod named a project (e.g. "let's work on claude-obsidian-setup"), match it to the folder. Fuzzy match is fine — "obsidian setup" matches `claude-obsidian-setup`.

If Rod didn't name a project, list the folders and ask:
> "Which project? I can see: [list]. Or is this something new?"

Wait for Rod's answer before proceeding.

## Step 2 — Read the project manifest

Look for `project.md` in the project folder. **Make sure to properly quote the entire path string when running cat to prevent space-parsing errors:**

```bash
cat "[projects-path]/[project-name]/project.md"
```

If it exists, read it for: project purpose, key files, relevant skills, connectors needed, and any standing preferences.

If it doesn't exist yet, note that and offer to create it at the end of the session.

## Step 3 — Read the latest session notes

Find the most recent session notes file (check both legacy folder and new root structure):

```bash
ls -t "[projects-path]/[project-name]/session-notes/"*.md "[projects-path]/[project-name]/"*session-note*.md 2>/dev/null | head -1
```

Read that file. If there are multiple recent ones (e.g. same week), read the latest two.

If no session notes exist yet, just say so — don't make anything up.

## Step 4 — Pre-load active files

If the `project.md` or `session-notes` explicitly mention specific files that are currently active, pending, or need fixing (e.g., "we need to update `src/components/Button.tsx`" or "pending CLAUDE.md fix"), use your tools to preemptively read those files into your context *before* delivering the briefing. This ensures you are immediately ready to answer questions or write code the second Rod replies.

## Step 5 — Deliver the briefing

Give Rod a concise briefing in this format — keep it tight, 60 seconds to read:

---

**Project:** [name]
**Last session:** [date from session notes]

**Where we left off:**
[2-3 sentences: what was being worked on, what state it's in]

**What's pending:**
[The actual pending items from session notes — be specific]

**Files to know about:**
[Key files from project.md or session notes — paths relative to Documents/]

**Skills / connectors for this project:**
[List from project.md]

---

Ready to continue. What would you like to work on?

---

## Step 6 — Handling New Projects

**Scenario A: Rod explicitly says this is a NEW project from scratch.**
Do NOT try to load old session notes. Instead, ask which methodology to use:

> "New project — got it. Which approach?
> - **GSD** — parallel subagents, spec-driven Plan → Execute → Verify phases. Fast, good for well-defined work.
> - **PAUL** — Plan-Apply-Unify loop. Single-session, mandatory reconciliation. Better context quality, good for complex/exploratory work.
> - **Lightweight** — just a project folder and scoping questions. No ceremony."

Wait for Rod's answer.

### Path 1: GSD Framework
If Rod picks GSD:
1. Create the project folder under `Second Brain/20 - Projects/[name]/` with a basic `project.md`
2. If the project will have code, also create `~/Projects/[name]/` and `git init`
3. Execute the GSD new-project workflow by reading and following `~/.claude/get-shit-done/workflows/new-project.md` directly. In Claude Code CLI, Rod can alternatively type `/gsd:new-project` as a slash command.
4. GSD runs its full flow (questioning → research → requirements → roadmap) and creates `.planning/` with all artifacts
5. Then execute `/gsd:plan-phase 1` (or read `~/.claude/get-shit-done/workflows/plan-phase.md`) to start building

### Path 2: PAUL Framework
If Rod picks PAUL:
1. Create the project folder under `Second Brain/20 - Projects/[name]/` with a basic `project.md`
2. If the project will have code, also create `~/Projects/[name]/` and `git init`
3. Initialize PAUL in the code directory by running `/paul:init`
4. PAUL creates `.paul/` with PROJECT.md, ROADMAP.md, STATE.md
5. Then run `/paul:plan` to create the first executable plan

### Path 3: Lightweight
If Rod picks lightweight:
1. Create the project folder under `Second Brain/20 - Projects/[name]/`
2. Ask 3 quick scoping questions:
   - **Goal:** What are we building and who is it for?
   - **Stack:** Any specific tech, APIs, or tools we need to use?
   - **First deliverable:** What does "done" look like for v1?
3. Create `project.md` from the answers
4. If the project will have code, also create `~/Projects/[name]/` and `git init`
5. Start building — no additional ceremony

**Scenario B: This is an existing project but it's just missing a project.md file.**
If the project folder exists but there is no `project.md` file, say:
> "No project manifest found. Want me to create one now? It'll make future session starts faster."

If yes, create `[projects-path]/[name]/project.md` using this template:

```markdown
# Project: [Name]

## Purpose
[What this project is for — one paragraph]

## Key files
[Important files, one per line with brief description]

## Skills used
[Skills that are relevant to this project]

## Connectors needed
[MCP connectors this project relies on]

## Standing preferences
[Any project-specific preferences or rules]
```
Fill in as much as you can from the session history and session notes. Ask Rod to fill in anything you can't infer.
