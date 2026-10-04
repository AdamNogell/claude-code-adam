# Tracker dashboards with artifacts

A Claude Code skill that turns a messy, multi-step piece of work into a living tracker page. Examples: a manuscript revision, a data audit, a server migration, a bug list. You type `/tracker` and a description of the work. Claude reads your material and publishes the page as a private artifact on claude.ai. From then on, Claude keeps the same page up to date as the work progresses.

An **artifact** is a live, interactive web page that Claude Code publishes from your session to a private URL on claude.ai. It updates in place when Claude republishes it, and you can share it from the page header ([Claude Code docs: artifacts](https://code.claude.com/docs/en/artifacts)).

## What the tracker page has

- **Summary first:** tiles for Open, Blockers, Your call (decisions only you can make) and Done, plus a progress bar.
- **Next up, Waiting on, Decided:** what to do next, who you are waiting for, and a dated log of decisions already made.
- **Phases:** groups of items in working order. Each item is a card with a checkbox, a stable ID, a severity stripe (blocker / high / medium / low), and a collapsible body. The body says where the work is (file, section, what to search for), the steps, and what "done" means.
- **Filters and tools:** All / Open / Blockers / Your call / Done, Expand all, **Copy open** (the open items as a Markdown checklist, ready to paste into a new Claude session), and Reset ticks.
- **Changelog, Basis, Not verified:** what changed and when, what the page was built from, and what Claude did *not* check.
- Light and dark themes, works on a phone, and `#ID` links open a specific item.
- Each tracker gets its own font and color identity, from four presets or a new palette.

## Requirements

From the [artifacts documentation](https://code.claude.com/docs/en/artifacts#availability):

- A **Pro, Max, Team or Enterprise** plan. On Team and Enterprise, an organization Owner can turn artifacts off.
- Claude Code **signed in with your claude.ai account** (`/login`). Sessions using an API key or a cloud provider (Bedrock, Vertex, Foundry) cannot publish.
- The **Claude Code CLI**, or the **Claude desktop app** version 1.13576.0 or later.

Without artifacts, the skill falls back to saving the page as a local `.html` file.

## Install

Copy the `tracker` folder into your personal skills directory. Run this from the root of this repository:

```bash
mkdir -p ~/.claude/skills && cp -R artifacts/tracker ~/.claude/skills/
```

Claude Code picks up skills added under `~/.claude/skills/` without a restart. If that directory did not exist when your session started, run `/reload-skills` or start a new session ([skills docs](https://code.claude.com/docs/en/skills)).

To use it in one project only, copy the folder to `.claude/skills/tracker/` inside that repository instead. Committing it there shares it with everyone who works on the repository.

## Use

Start a tracker by telling Claude what to track and where the material is:

```text
/tracker the revision of our paper, from the reviewer letter in revision/decision_letter.pdf
```

```text
/tracker the open problems in this pipeline before we can publish the numbers
```

After a work session, ask for an update in plain words, or pass the tracker's link:

```text
/tracker update: I've re-run the PCA and fixed the legend numbering
```

```text
/tracker https://claude.ai/code/artifact/…
```

Claude reads the live page first, ticks only what it can verify, records how it checked each item, adds a changelog entry, and republishes to the same URL.

To find a tracker again, run `/artifacts` in Claude Code to list your artifacts (`o` opens one, `c` copies its link). Or open your gallery at [claude.ai/code/artifacts](https://claude.ai/code/artifacts) ([docs](https://code.claude.com/docs/en/artifacts#find-an-artifact-again)).

## Tips

- **One tracker per piece of work.** Keep a single page alive for weeks rather than starting a new one each session.
- **Let Claude keep it current.** End a work session with "update the tracker". The page stays trustworthy because items are only ticked with evidence, and anything unchecked is listed under Not verified.
- **Note the link in the project's CLAUDE.md.** Claude offers to add a line like `Tracker: <url>` when it publishes. New sessions then update the same page instead of creating a second one.
- **Share it from the page header.** A new artifact is visible only to you. On Team and Enterprise plans you can share it with specific people or your whole organization ([docs](https://code.claude.com/docs/en/artifacts#share-an-artifact)).
- **Your checkbox ticks are personal.** They are stored in your browser only. Other viewers see what Claude shipped as done, not your ticks.
- **Hand work back to Claude** with **Copy open**: it gives you the open items as a checklist to paste into a new session.

## Files

| File | What it is |
| :- | :- |
| `tracker/SKILL.md` | The instructions Claude follows when you run `/tracker` |
| `tracker/template.html` | The page: styles, behaviour, and fictional example content showing every component |
| `tracker/palettes.md` | Font and color presets, and rules for making a new palette |

To change the house style, edit `template.html` (layout and components) or `palettes.md` (looks). The skill copies the template every time, so your edits apply to every new tracker.

## Sources

- Artifacts, availability, updating, `/artifacts`, sharing: [code.claude.com/docs/en/artifacts](https://code.claude.com/docs/en/artifacts), retrieved 2026-10-04.
- Skill locations, frontmatter, live reload, `/reload-skills`: [code.claude.com/docs/en/skills](https://code.claude.com/docs/en/skills), retrieved 2026-10-04.
