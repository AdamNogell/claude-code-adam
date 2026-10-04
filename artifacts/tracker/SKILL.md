---
name: tracker
description: Build or update a living tracker dashboard as a claude.ai artifact, with summary tiles, a progress bar, phases of collapsible checklist items with severity stripes, filters, a decisions log and a changelog. Use when the user asks for a tracker, worklist, checklist or to-do dashboard, wants to track a multi-step piece of work (a manuscript revision, an analysis audit, a migration, a bug list), or asks to update an existing tracker after finishing work.
argument-hint: "[what to track | URL of a tracker to update]"
---

# Tracker

You build and maintain a tracker: one artifact page for one piece of work, kept current for as long as the work runs. The user reads it to see where things stand. You keep it true: after each piece of tracked work, you tick items, record the evidence, and republish to the same URL.

Request: $ARGUMENTS

Files in this skill:

- `${CLAUDE_SKILL_DIR}/template.html` is the complete page: styles, script, and fictional example content that shows every component. Every new tracker starts as a copy of it.
- `${CLAUDE_SKILL_DIR}/palettes.md` has font and color presets and the rules for a new palette. Read it when choosing the look.

## 1. New tracker or update

Update an existing tracker when any of these holds:

- the request contains a claude.ai artifact URL;
- the user refers to an existing tracker, or the project's CLAUDE.md names one;
- an `Artifact` call with `action: "list"` shows a tracker for the same work.

Otherwise create a new one. If you can't tell, ask.

## 2. Gather the items

Read before you write. Items come only from sources you read in this session: the conversation, files in the repository, a reviewer letter, an issue list, logs, command or test output. For each item, note what it is, where it is (file, function, section, text to search for), why it matters, and what done looks like.

- Never invent tasks, numbers, paths, names or dates. If you cannot find the scope, ask one question.
- Write absolute dates (2026-10-04), never "today" or "last week".
- Anything you did not check goes in the footer under "Not verified", never into an item as fact.

## 3. Structure

- **Phases** group items in the order they should be done. Use ordinals `01`, `02` only when the order matters. Otherwise use short codes (`F`, `D`) or drop the badge. Two to six phases is typical.
- **IDs** are short and stable: a phase letter plus a number (`B1`, `R1.3`, `S2`). Never renumber or reuse an ID, even after an item is archived. New items take the next free number.
- **Severity** is `data-sev`: `1` blocker (stops other work or changes a result), `2` high, `3` medium, `4` low. Chip text: Blocker, High, Medium, Low.
- **Decisions the user must make** get `data-decision="true"` and the chip "Your call". The body lists the options with their costs, then your recommendation.
- **Items waiting on someone** get class `waiting` and the chip "Waiting". Say who, what was asked, when, and the fallback.
- **Dependencies** go last in the body: `<p class="needs">needs B1 B2</p>`.
- **Summary callouts** sit above the toolbar. Next up holds the 2 to 4 items to do next, each starting with `<a class="ref" href="#ID">ID</a>`. Waiting on lists blocked items. Decided is the decision log (`D1 · date.` …), appended to and never rewritten. Leave out a callout that would be empty.

## 4. Build a new tracker

1. Copy the template to your scratchpad directory (or a temporary directory), never into the user's repository: `cp "${CLAUDE_SKILL_DIR}/template.html" <scratchpad>/<slug>.html`. The published artifact is the source of truth, and a copy in the repository goes stale the first time the page is updated.
2. Replace all example content from `<div class="page"` through `</footer>`. Keep every class name, `id` and `data-*` pattern the script reads: tiles `t-open`, `t-block`, `t-dec`, `t-done`; `bar-track`, `bar`, `bar-note`; `empty`, `copybox`, `toast`; the toolbar buttons; `.phase`, `.phase-count`, `.item[data-id]`. Leave the `<script>` unchanged.
3. Set `data-tracker-key="<slug>.v1"` on `.page`, unique per tracker, so ticks from two trackers never collide.
4. Choose the look: read `palettes.md`, then replace the Google Fonts link and the three token blocks with the preset that suits the subject, or derive a new palette by its rules. If the user names a look, or the project's CLAUDE.md or a theme file defines colors and fonts, fill the tokens from those instead. Change no other CSS unless you need a component the template lacks, and then build it from the tokens.
5. Name it. `<title>` and `<h1>` carry the tracker's name: two to four specific words, such as "ExP Point 4 Tracker" or "Uniparental aDNA Worklist". Use the user's own name for the work if they have one. Never add an explanation after a dash.
6. Write the masthead. The eyebrow is `project / context / updated YYYY-MM-DD`. The standfirst is one or two sentences on what stands between now and done.
7. Give each item `id` and `data-id` equal to its ID (so `#R1.3` links open it), and its checkbox `id="c-<ID>"`.
8. Write the footer: Changelog (first entry "Tracker created from …", naming the sources), Basis (what you read, when, at which commit or version), and Not verified.

An open item:

```html
<li class="item" id="B2" data-id="B2" data-sev="1">
  <input type="checkbox" id="c-B2">
  <details>
    <summary>
      <span class="id">B2</span>
      <span class="t">Outcome-style title: what will be true when this is done</span>
      <span class="chips"><span class="chip s1">Blocker</span></span>
    </summary>
    <div class="detail">
      <section><h4>Where</h4><p>File, function or section, and the text to search for.</p></section>
      <section><h4>Steps</h4><ol><li>…</li></ol></section>
      <section><h4>Done when</h4><p>The check that proves it.</p></section>
      <p class="flag">A caveat or risk, if there is one.</p>
      <p class="needs">needs B1</p>
    </div>
  </details>
</li>
```

Other building blocks inside `.detail`: `<div class="facts"><div><span>label</span><span>value</span></div></div>` for measured numbers, `<pre>` for command output or before/after tables, and further `<section><h4>…</h4>…</section>` blocks such as "Why it matters", "Options" and "Recommendation". Chips: `s1` to `s4`, `dec` (Your call), `wait` (Waiting), `new` (New), `done` (Done).

## 5. Publish

- Publish with the `Artifact` tool: `file_path` is the HTML file, `icon` is `"checklist"`, and `description` is one sentence on what the tracker covers. Publishing wraps the file in its own `<!doctype html>`, `<head>` and `<body>`, so the file contains none of these.
- Give the user the link. Then offer to add one line to the project's CLAUDE.md, `Tracker: <url> (update it with /tracker after finishing tracked work)`, so later sessions update this page instead of starting a new one. Edit CLAUDE.md only if they agree.
- If the `Artifact` tool is unavailable (no claude.ai login, an API-key or cloud-provider session, or artifacts turned off), wrap the page as `<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1"></head><body>…</body></html>`, save it as `<slug>.html` in the current directory (or where the user says), and tell the user artifacts were unavailable and why.

## 6. Update an existing tracker

1. Read the live page first, with `Artifact` `action: "read"` and the URL. Build on the saved file the read returns. Never regenerate the page from memory or from the template: that loses every change made since.
2. Tick only with evidence. An item is done when you have seen proof in this session: the file content, a test or command result, a published record. Then:
   - add `data-default-done="true"` to the `<li>` and replace its severity chip with `<span class="chip done">Done</span>`;
   - put `<section class="done-note"><h4>Done · YYYY-MM-DD</h4><p>What was done and how you checked it.</p></section>` first in its `.detail`, and keep the original context below it.
   - For a partly done item, keep it open and put what is left at the top of its detail.
3. Add new work as a new item with the next free ID and `<span class="chip new">New</span>`. Remove "New" at the following update.
4. When every item in a phase is done, move its whole `<section class="phase">` into `<details class="archive">` (newest first). Remove its checkboxes and its `.phase-count`, and update the count in the archive's summary. Create the archive block if there is none.
5. Refresh the summary: the eyebrow date, Next up, Waiting on, and Decided (append only).
6. Add a changelog entry at the top: `<li><b>YYYY-MM-DD.</b> What changed, what was verified, what is left.</li>`. Update Basis and Not verified.
7. Republish with `url` set to the tracker's URL, or the same `file_path` if you published it earlier in this session. Tell the user in one or two lines what changed.

The user's own checkbox ticks live only in their browser, and you cannot read them. If they say they finished something, verify it like any other item before shipping it as done.

## Writing

- Use plain, specific sentences. Name the file, the place in it, and the text to search for.
- Titles state outcomes or actions: "Report a 95% interval for every FST value in Table 2", not "FST CIs".
- Every number names its source: which file, run or commit it was measured from.
- Keep one tracker per piece of work. Suggest splitting once a page passes about 40 open items.

## Ticks and shared state

Checkbox ticks are stored in each viewer's browser (localStorage). They are a personal convenience: they never reach other viewers or devices. What everyone sees is the shipped state (`data-default-done`). If the user wants ticks shared across people or devices, load the `artifact-capabilities` skill and check what this account offers before changing the page.
