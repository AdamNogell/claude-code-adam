# Claude Code: two things I use every day

Setup files for the two tips from the talk. Each folder is self-contained.

| Folder | What you get | Setup time |
| :- | :- | :- |
| [daily-paper/](daily-paper/) | One real paper (preferably a review) on your phone every weekday morning, rotating through four topics you choose | About 10 minutes |
| [artifacts/](artifacts/) | A `/tracker` skill that turns a multi-step piece of work into a living dashboard page, which Claude keeps up to date | About 2 minutes |

Both need a paid Claude plan (Pro, Max, Team or Enterprise) and your claude.ai account. Each folder's README lists the exact requirements, with links to the official documentation.

## Quick start

**Daily paper:** fill in your name and topics in [daily-paper/prompt.md](daily-paper/prompt.md), then follow [daily-paper/README.md](daily-paper/README.md) to schedule it in the Claude desktop app.

**Tracker:** from the root of this repository, run:

```bash
mkdir -p ~/.claude/skills && cp -R artifacts/tracker ~/.claude/skills/
```

Then, in Claude Code:

```text
/tracker <what you want to track, and where the material is>
```
