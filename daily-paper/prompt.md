# Daily paper — task prompt

Fill in the five lines in **Your details**, then copy everything from "Your details" down to the end of Step 5 into the task's prompt (see [README.md](README.md) for where it goes). Leave the rest of the wording as it is: each sentence is there for a reason, and the Notes section below explains the less obvious ones.

The category descriptions are what the task searches with, so be specific. Name organisms, methods, periods, regions, labs or companies, not just a field name.

---

**Your details**

- Reader: [YOUR NAME]
- Category (a), your core research topic: [ONE OR TWO LINES]
- Category (b): [ONE LINE]
- Category (c): [ONE LINE]
- Category (d): [ONE LINE]

You are producing the daily "one paper to read today" digest for the reader named in "Your details" above (called "the reader" below). This is a recurring weekday-morning task, and you are running in a brand-new session with no memory of previous runs except what is stored in Claude's persistent memory tool (the mcp__memory__* tools). Follow these steps in order.

Step 1 — Check rotation history: Read the memory file /areas/morning-review-paper-log.md with mcp__memory__memory_read. If it doesn't exist yet, treat the history as empty and proceed. This file logs, one line per weekday run, the date, the category chosen, and the paper's title — roughly the last 10-15 entries. If the mcp__memory__* tools are not available in this session at all, skip this step and Step 5, pick the category in Step 2 by weekday instead (Monday (a), Tuesday (b), Wednesday (a), Thursday (c), Friday (d)), and add one line at the end of the digest saying the rotation log was unavailable.

Step 2 — Pick today's category: The categories are the four listed in "Your details": (a) is the reader's core research topic (this is their main research area, so it should come up often but not every single day); (b), (c) and (d) are their broader interests. Look at the log and avoid repeating the same category that was used on the immediately preceding 1-2 weekday runs, so the reader gets variety across the week rather than a run of near-identical days. Exception: if there's a genuinely major, newsworthy new paper directly in the core topic, it's fine to pick it even if that category was used recently.

Step 3 — Find one real paper: Use WebSearch (and PubMed / bioRxiv / journal sites where useful) to find one real, currently retrievable paper matching today's category. Strongly prefer review papers — the reader explicitly wants reviews over primary research papers because they teach more, especially outside the core project. A brand-new, highly notable primary research paper is an acceptable substitute for a review if it's the kind of paper people are currently talking about. Prioritize papers that are genuinely interesting, and either highly relevant to the reader's core research or high-impact / widely discussed in the field or in society. Never invent a paper, author, journal, date, or DOI — report only a paper you actually found via search in this session, exactly as retrieved.

Step 4 — Write the digest (this is the message the reader will read): give the paper's title, authors, journal/venue, publication date, and a working link or DOI. Write a concise plain-prose summary (a few sentences) of what the paper covers and its key points, and one sentence on why it matters to the reader — either for their core research or for their broader interests — or why it's currently a big deal. State plainly whether it is a peer-reviewed review, a peer-reviewed primary study, or a preprint, and flag if its findings are preliminary or contested. Close with a short confidence & sourcing note that includes the link, so the reader (or an auditor) could verify it. Keep the whole message to one paper, not a menu of options, since they'll read it before their workday.

Step 5 — Log it: append one line to /areas/morning-review-paper-log.md via mcp__memory__memory_append (use mcp__memory__memory_write instead if the file doesn't exist yet), recording today's date, the category you picked, and the paper's title. If the file is getting long, rewrite it (mcp__memory__memory_write) keeping only the most recent ~10-15 entries.

---

## Notes on the wording

- **The rotation log** (Steps 1 and 5) is what gives you variety. Each run starts with no memory, so without the log it would pick the same kind of paper every day. The log also stops it from sending you a paper it already sent.
- **"Never invent a paper…"** (Step 3) is the most important sentence. Keep it.
- **"Strongly prefer review papers"** is a preference. If you would rather get the newest primary research, rewrite that sentence and the one after it.
- **Fewer or more categories** work too. List them under "Your details" and adjust the weekday fallback in Step 1 so the core topic still comes up most often.
- **The weekday fallback** at the end of Step 1 is the one addition to the original prompt. It only applies when the memory tools are missing, as they may be if you set this up as a Claude Code routine instead of a Cowork task.
