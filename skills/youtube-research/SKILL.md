---
name: youtube-research
description: >
  Research a topic by searching YouTube, pulling transcripts from the top videos,
  and writing a comprehensive report. Use this skill when Rod says things like
  "research [topic] on YouTube", "find the best YouTube videos about [topic]",
  "what does YouTube say about [topic]", "/youtube-research [topic]", or any
  intent to gather knowledge from YouTube videos on a subject.
---

# YouTube Research

Your job is to search YouTube for the best videos on a given topic, pull their transcripts, analyze them, and deliver a concise research report.

## Requirements

- `yt-dlp` must be installed (`brew install yt-dlp`)
- Internet access for YouTube search and transcript download

## Step 1 — Search YouTube

Search for the topic using yt-dlp. Pull up to 10 results, sorted by relevance (YouTube's default ranking factors in view count, engagement, and recency).

```bash
yt-dlp "ytsearch10:<TOPIC>" --flat-playlist --print "%(id)s | %(title)s | %(view_count)s | %(duration_string)s | %(upload_date)s"
```

Show Rod the list with view counts and ask if he wants to:
- Proceed with all of them
- Pick specific ones
- Adjust the search query

Wait for confirmation before downloading transcripts.

## Step 2 — Download transcripts

For each selected video, download the auto-generated English subtitles:

```bash
mkdir -p /tmp/yt-research
yt-dlp --write-auto-sub --sub-lang en --skip-download -o "/tmp/yt-research/%(id)s" "https://youtube.com/watch?v=VIDEO_ID"
```

## Step 3 — Clean transcripts

VTT files are messy. Clean each one into readable text:

```python
import re, glob, os

for vtt_path in glob.glob("/tmp/yt-research/*.vtt"):
    with open(vtt_path) as f:
        content = f.read()
    # Remove VTT header
    content = re.sub(r'WEBVTT.*?\n\n', '', content, count=1, flags=re.DOTALL)
    # Remove timestamps
    content = re.sub(r'\d{2}:\d{2}:\d{2}\.\d{3} --> \d{2}:\d{2}:\d{2}\.\d{3}.*\n', '', content)
    # Remove inline timing tags
    content = re.sub(r'<[^>]+>', '', content)
    # Dedup consecutive identical lines
    lines = [l.strip() for l in content.splitlines() if l.strip()]
    deduped = []
    for line in lines:
        if not deduped or line != deduped[-1]:
            deduped.append(line)
    txt_path = vtt_path.replace('.en.vtt', '.txt')
    with open(txt_path, 'w') as f:
        f.write('\n'.join(deduped))
```

## Step 4 — Analyze and report

Read each cleaned transcript. Then write a research report in this format:

---

# YouTube Research: [Topic]

**Date:** [today's date]
**Videos analyzed:** [count]
**Search query:** [what was searched]

## Key Findings

[The meat of the report. Synthesize across ALL videos — don't just summarize each one separately. What are the common recommendations? Where do creators agree? Where do they disagree? What surprised you?]

## Top Recommendations

[Numbered list of the strongest, most-agreed-upon recommendations with brief context for each]

## Notable Mentions

[Things that only one or two videos mentioned but seem worth knowing]

## Contrarian / Minority Views

[Where did any creator go against the consensus? This is often the most valuable section.]

## Sources

| # | Video | Creator | Views | Link |
|---|---|---|---|---|
| 1 | [title] | [channel] | [views] | https://youtube.com/watch?v=ID |

---

**Writing guidelines:**
- Synthesize, don't summarize. Rod wants insights, not video recaps.
- Be opinionated. If the research points to a clear answer, say so.
- Keep it scannable — bullets, short paragraphs, bold key terms.
- If Rod asked a specific question (e.g., "best plugins for X"), answer it directly at the top before the detailed breakdown.

## Step 5 — Offer to save

Ask Rod if he wants the report saved to his vault. If yes, save to `Second Brain/40 - Resources/` with filename `YYYY-MM-DD-[topic-slug]-youtube-research.md`.

## Step 6 — Cleanup

Remove the temp files:

```bash
rm -rf /tmp/yt-research
```
