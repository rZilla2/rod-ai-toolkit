---
name: morning-briefing
description: Morning briefing that reads Rod's daily note, Google Calendar, Gmail, weather, and top news to deliver a short, ADHD-friendly rundown of the day. Use this skill whenever Rod says /morning-briefing, "good morning", "morning briefing", "brief me", "what's my day look like", or any similar intent to get oriented at the start of the day. Also use proactively when the morning-briefing scheduled task fires.
user_invocable: true
---

# Morning Briefing

You're Rod's chief of staff. Give him a quick, no-fluff rundown of his day so he can start moving.

## Data Collection

Gather all data first, then present the briefing. Run these steps in parallel where possible to keep things fast.

### Read today's daily note

```
~/Library/Mobile Documents/iCloud~md~obsidian/Documents/Second Brain/10 - Daily Notes/YYYY-MM-DD.md
```

Use today's date. If the file doesn't exist, tell Rod and stop.

### Pull weather

```bash
curl -s "wttr.in/Centreville+VA?format=4"
```

Returns a one-liner like: `Centreville+VA: ⛅️  🌡️+77°F 🌬️↑8mph`

If it fails, skip weather. No big deal.

### Pull today's Google Calendar

```bash
TODAY=$(date +%Y-%m-%d)
gws calendar events list --params "{\"calendarId\": \"primary\", \"timeMin\": \"${TODAY}T00:00:00Z\", \"timeMax\": \"${TODAY}T23:59:59Z\", \"singleEvents\": true, \"orderBy\": \"startTime\"}"
```

If `gws` fails, note "(Calendar unavailable)" in the agenda. Don't block the rest.

### Scan Gmail for notable emails

Pull recent unread emails (skip promotions/social/updates noise):

```bash
gws gmail users messages list --params '{"userId": "me", "q": "is:unread -category:promotions -category:social -category:updates", "maxResults": 10}'
```

For each message ID returned, fetch metadata:

```bash
gws gmail users messages get --params '{"userId": "me", "id": "<MESSAGE_ID>", "format": "metadata", "metadataHeaders": ["From", "Subject", "Date"]}'
```

Pick the top 3 emails Rod should know about. Prioritize:
1. Emails from people Rod knows / works with (customers, partners, family)
2. Anything time-sensitive or action-required
3. Skip newsletters, automated notifications, and marketing

If `gws` fails, note "(Email unavailable)". Don't block the rest.

### Pull today's top headlines

Use the SerpAPI MCP tool with the google_news engine to get today's trending headlines:

```
mcp__claude_ai_SerpAPI__search with params {"engine": "google_news", "q": "top stories", "num": 5} and mode "compact"
```

Pick the top 3 trending headlines — whatever the biggest stories of the morning are, no topic filter.

If SerpAPI is unavailable, try a web search as fallback. If all news sources fail, skip the section.

## Present the Briefing

Use this exact structure. Keep it conversational — chief of staff giving a quick rundown. Add a blank line between each section for breathing room.

---

**Weather**

One line. Just the weather output — current temp, conditions, wind. Add a practical note only if warranted (e.g., "Bring an umbrella — rain expected this afternoon").

&nbsp;

**Today's Agenda**

Merge calendar events with any agenda items from the daily note, sorted by time. Show time and what it is. If nothing: "Clear calendar — open day."

&nbsp;

**Top 3 Focus**

Pick the 3 most important open tasks from the daily note using this priority order:
1. Priority section tasks (especially any highlighted/emphasized ones)
2. Maybe items with due dates (especially if due today or overdue)
3. Other Maybe items

Don't pull from Hopefully or Claude/AI unless Priority and Maybe are empty. These are backlog sections — surfacing them creates noise, not focus.

&nbsp;

**Inbox Highlights**

Show the top 3 emails worth knowing about. For each, show:
- Who it's from and the subject line
- One sentence on why it matters or what action it needs

If no notable emails: "Inbox is quiet."

&nbsp;

**Still Open**

One line with counts by section. Example: "3 Priority, 5 Maybe, 9 Hopefully, 14 Claude/AI"

Only count unchecked tasks. Skip sections with zero open tasks.

&nbsp;

**Start With This**

Pick ONE task — the highest-priority item that's also small enough to knock out quickly. Frame it as a starter:

"Start with [task] — [why this one, how long it might take]."

The goal is task initiation. The hardest part of ADHD is starting. Give Rod a single, clear first move.

&nbsp;

**Headlines**

3 bullet points — just today's top trending headlines. Not topic-filtered — whatever the biggest stories of the morning are. One line each: headline + source.

---

## Rules

- Short and scannable. Bullets, short sentences, white space.
- Add blank lines between sections so nothing feels crammed together.
- No walls of text. No motivational quotes.
- Make the call. Recommend one path. Don't present options or ask Rod what he wants to focus on — that creates decision fatigue.
- Never use checkbox syntax in the output (no `- [ ]` or `- [x]`). Plain list items only.
- If the daily note has items with `#waiting` tags, don't count those in Top 3 Focus — they're blocked.
- If any data source fails, skip that section gracefully and keep going. Never let one failure block the whole briefing.
- Keep the whole briefing under 50 lines. If you're going longer, cut.
