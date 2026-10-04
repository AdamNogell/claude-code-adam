# Tracker palettes

Each tracker gets its own look, so two trackers open side by side are easy to tell apart. Re-theme by replacing two things in the copied template, and nothing else:

1. the Google Fonts `<link rel="stylesheet" …>` line;
2. the three token blocks at the top of `<style>` (bare `:root`, the `prefers-color-scheme: dark` block, and `:root[data-theme="dark"]`).

Every other rule in the template reads colors and fonts from these tokens, so the rest of the page follows automatically.

## Field notebook (the template's default)

Already in `template.html`. Serif display (Newsreader) with IBM Plex, on a sage-tinted ground with a teal accent. Suits research analyses, data audits, pipelines, and anything you will read slowly and come back to.

## Blueprint

Suits manuscript revisions, reviewer responses, submissions, anything with a deadline and a paper trail.

Font link (replaces the `<link rel="stylesheet" …>` line):

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Barlow+Condensed:wght@600;700&family=IBM+Plex+Mono:wght@400;500;600&family=IBM+Plex+Sans:wght@400;500;600;700&display=swap">
```

Token blocks (replace the three blocks at the top of `<style>`):

```css
:root {
  --ground: #F4F7FB;
  --surface: #FFFFFF;
  --surface-2: #EEF3F9;
  --ink: #13203A;
  --ink-2: #44526A;
  --ink-3: #5E6B82;
  --rule: #D8E0EB;
  --rule-strong: #C2CEDD;
  --accent: #1D5EA8;
  --accent-ink: #154A87;
  --accent-wash: #E8F1FA;
  --on-accent: #FFFFFF;
  --decide: #5D3F98;
  --decide-wash: #EEE8F7;
  --sev-1: #B23A1E;
  --sev-1-wash: #F9E6E0;
  --sev-2: #9C5310;
  --sev-2-wash: #F8ECDD;
  --sev-3: #7A6510;
  --sev-3-wash: #F3EED6;
  --sev-4: #5B6B82;
  --sev-4-wash: #E9EEF4;
  --shadow: 0 1px 2px rgba(19, 32, 58, .05), 0 6px 18px rgba(19, 32, 58, .05);
  --font-display: "Barlow Condensed", "Arial Narrow", sans-serif;
  --font-body: "IBM Plex Sans", system-ui, -apple-system, "Segoe UI", sans-serif;
  --font-mono: "IBM Plex Mono", ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
  --radius: 6px;
}
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --ground: #0D1520;
    --surface: #142031;
    --surface-2: #1A293D;
    --ink: #E2EAF5;
    --ink-2: #B0BED0;
    --ink-3: #8C9CB3;
    --rule: #26364C;
    --rule-strong: #34475F;
    --accent: #80B3EA;
    --accent-ink: #A6CBF2;
    --accent-wash: #16283D;
    --on-accent: #07162B;
    --decide: #B9A3E3;
    --decide-wash: #241D38;
    --sev-1: #F07C58;
    --sev-1-wash: #2E1A14;
    --sev-2: #E0A062;
    --sev-2-wash: #2D2115;
    --sev-3: #D4B85C;
    --sev-3-wash: #2A2614;
    --sev-4: #8C9CB3;
    --sev-4-wash: #1B2636;
    --shadow: 0 1px 2px rgba(0, 0, 0, .3), 0 6px 18px rgba(0, 0, 0, .25);
    color-scheme: dark;
  }
}
:root[data-theme="dark"] {
  --ground: #0D1520;
  --surface: #142031;
  --surface-2: #1A293D;
  --ink: #E2EAF5;
  --ink-2: #B0BED0;
  --ink-3: #8C9CB3;
  --rule: #26364C;
  --rule-strong: #34475F;
  --accent: #80B3EA;
  --accent-ink: #A6CBF2;
  --accent-wash: #16283D;
  --on-accent: #07162B;
  --decide: #B9A3E3;
  --decide-wash: #241D38;
  --sev-1: #F07C58;
  --sev-1-wash: #2E1A14;
  --sev-2: #E0A062;
  --sev-2-wash: #2D2115;
  --sev-3: #D4B85C;
  --sev-3-wash: #2A2614;
  --sev-4: #8C9CB3;
  --sev-4-wash: #1B2636;
  --shadow: 0 1px 2px rgba(0, 0, 0, .3), 0 6px 18px rgba(0, 0, 0, .25);
  color-scheme: dark;
}
```

## Runbook

Suits server work, migrations, security fixes, step-by-step procedures where order and rollback matter.

Font link (replaces the `<link rel="stylesheet" …>` line):

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Bitter:wght@500;600;700&family=IBM+Plex+Mono:wght@400;500;600&family=Public+Sans:wght@400;500;600;700&display=swap">
```

Token blocks (replace the three blocks at the top of `<style>`):

```css
:root {
  --ground: #EAEEED;
  --surface: #FBFCFC;
  --surface-2: #DDE4E3;
  --ink: #0F1719;
  --ink-2: #3D4B4E;
  --ink-3: #5A6A6D;
  --rule: #C5D0CF;
  --rule-strong: #AEBCBB;
  --accent: #0D5B5F;
  --accent-ink: #0A4A4D;
  --accent-wash: #D3E5E5;
  --on-accent: #FFFFFF;
  --decide: #2C4F79;
  --decide-wash: #DBE4F0;
  --sev-1: #96291F;
  --sev-1-wash: #F3DCD9;
  --sev-2: #8A5410;
  --sev-2-wash: #F2E6D2;
  --sev-3: #6E6212;
  --sev-3-wash: #ECE8CF;
  --sev-4: #5A6A6D;
  --sev-4-wash: #E2E8E7;
  --shadow: 0 1px 2px rgba(15, 23, 25, .06), 0 6px 18px rgba(15, 23, 25, .05);
  --font-display: "Bitter", Georgia, "Times New Roman", serif;
  --font-body: "Public Sans", system-ui, -apple-system, "Segoe UI", sans-serif;
  --font-mono: "IBM Plex Mono", ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
  --radius: 6px;
}
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --ground: #0C1214;
    --surface: #141D1F;
    --surface-2: #1A2528;
    --ink: #E2EAE9;
    --ink-2: #BAC6C6;
    --ink-3: #8B9A9C;
    --rule: #2B3A3D;
    --rule-strong: #3A4C4F;
    --accent: #63BFC0;
    --accent-ink: #8AD3D3;
    --accent-wash: #15302F;
    --on-accent: #071314;
    --decide: #8AAEDE;
    --decide-wash: #18243A;
    --sev-1: #E08376;
    --sev-1-wash: #301A17;
    --sev-2: #D3A15A;
    --sev-2-wash: #2D2214;
    --sev-3: #CDBB66;
    --sev-3-wash: #2A2716;
    --sev-4: #8B9A9C;
    --sev-4-wash: #1E2A2C;
    --shadow: 0 1px 2px rgba(0, 0, 0, .3), 0 6px 18px rgba(0, 0, 0, .25);
    color-scheme: dark;
  }
}
:root[data-theme="dark"] {
  --ground: #0C1214;
  --surface: #141D1F;
  --surface-2: #1A2528;
  --ink: #E2EAE9;
  --ink-2: #BAC6C6;
  --ink-3: #8B9A9C;
  --rule: #2B3A3D;
  --rule-strong: #3A4C4F;
  --accent: #63BFC0;
  --accent-ink: #8AD3D3;
  --accent-wash: #15302F;
  --on-accent: #071314;
  --decide: #8AAEDE;
  --decide-wash: #18243A;
  --sev-1: #E08376;
  --sev-1-wash: #301A17;
  --sev-2: #D3A15A;
  --sev-2-wash: #2D2214;
  --sev-3: #CDBB66;
  --sev-3-wash: #2A2716;
  --sev-4: #8B9A9C;
  --sev-4-wash: #1E2A2C;
  --shadow: 0 1px 2px rgba(0, 0, 0, .3), 0 6px 18px rgba(0, 0, 0, .25);
  color-scheme: dark;
}
```

## Workbench

Suits software projects, issue lists, bug triage, feature work on a codebase.

Font link (replaces the `<link rel="stylesheet" …>` line):

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Archivo:wght@400;500;600;700&family=Bricolage+Grotesque:opsz,wght@12..96,600..700&family=IBM+Plex+Mono:wght@400;500;600&display=swap">
```

Token blocks (replace the three blocks at the top of `<style>`):

```css
:root {
  --ground: #ECEFEA;
  --surface: #F8FAF7;
  --surface-2: #E2E7DE;
  --ink: #161C17;
  --ink-2: #4C564D;
  --ink-3: #5F6A61;
  --rule: #D2D9CF;
  --rule-strong: #BCC5B8;
  --accent: #14705C;
  --accent-ink: #0D4D3F;
  --accent-wash: #D7E8E0;
  --on-accent: #F4FBF8;
  --decide: #2A5C78;
  --decide-wash: #DAE6EE;
  --sev-1: #A2382A;
  --sev-1-wash: #F0DCD8;
  --sev-2: #8E5A10;
  --sev-2-wash: #F1E4CF;
  --sev-3: #6F6514;
  --sev-3-wash: #EAE6CC;
  --sev-4: #5D685F;
  --sev-4-wash: #E2E7DE;
  --shadow: 0 1px 2px rgba(22, 28, 23, .05), 0 6px 18px rgba(22, 28, 23, .05);
  --font-display: "Bricolage Grotesque", "Archivo", system-ui, sans-serif;
  --font-body: "Archivo", system-ui, "Helvetica Neue", sans-serif;
  --font-mono: "IBM Plex Mono", ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
  --radius: 6px;
}
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --ground: #101413;
    --surface: #171D1A;
    --surface-2: #1F2622;
    --ink: #E6EBE6;
    --ink-2: #A4AEA6;
    --ink-3: #7D877F;
    --rule: #2B332D;
    --rule-strong: #3B453D;
    --accent: #3FB894;
    --accent-ink: #8FD8C2;
    --accent-wash: #16322A;
    --on-accent: #08140F;
    --decide: #6FADCC;
    --decide-wash: #172A33;
    --sev-1: #E07160;
    --sev-1-wash: #3A1F1B;
    --sev-2: #D9A341;
    --sev-2-wash: #33270F;
    --sev-3: #C9BC5E;
    --sev-3-wash: #2B2914;
    --sev-4: #8E988F;
    --sev-4-wash: #1F2622;
    --shadow: 0 1px 2px rgba(0, 0, 0, .3), 0 6px 18px rgba(0, 0, 0, .25);
    color-scheme: dark;
  }
}
:root[data-theme="dark"] {
  --ground: #101413;
  --surface: #171D1A;
  --surface-2: #1F2622;
  --ink: #E6EBE6;
  --ink-2: #A4AEA6;
  --ink-3: #7D877F;
  --rule: #2B332D;
  --rule-strong: #3B453D;
  --accent: #3FB894;
  --accent-ink: #8FD8C2;
  --accent-wash: #16322A;
  --on-accent: #08140F;
  --decide: #6FADCC;
  --decide-wash: #172A33;
  --sev-1: #E07160;
  --sev-1-wash: #3A1F1B;
  --sev-2: #D9A341;
  --sev-2-wash: #33270F;
  --sev-3: #C9BC5E;
  --sev-3-wash: #2B2914;
  --sev-4: #8E988F;
  --sev-4-wash: #1F2622;
  --shadow: 0 1px 2px rgba(0, 0, 0, .3), 0 6px 18px rgba(0, 0, 0, .25);
  color-scheme: dark;
}
```

## Making a new palette

Pick a preset when one fits the subject. When none does, derive a new one under these rules:

- **Fill every token in all three blocks.** The two dark blocks hold identical values. A token missing from bare `:root` leaves part of the page uncolored for most viewers.
- **Tint the neutrals.** `--ground`, `--surface*`, `--rule*` and `--ink*` lean slightly toward the accent's hue. Avoid pure mid-grey.
- **Keep severity semantic.** `--sev-1` (blocker) is a red, `--sev-2` (high) an orange or amber, `--sev-3` (medium) an ochre, and `--sev-4` (low) a neutral. `--decide` is its own hue, distinct from both the accent and the severities.
- **Check chip contrast.** Chips are 9.5px uppercase text on their `-wash` background. In light mode use dark, saturated text colors (around 4.5:1 against the wash). In dark mode use light tints on very dark washes.
- **Pick `--on-accent` for legibility.** It is the text color on a pressed filter button, so it must read on `--accent` in both themes: usually white in light mode and near-black in dark mode.
- **Pair three fonts**, all from Google Fonts with a real fallback stack: a characterful display face for `h1` and phase titles, a readable body face, and a monospace for IDs, chips and numbers. Avoid Inter and Space Grotesk as the default choice.
- **Avoid the generic looks:** warm cream with a serif and terracotta accent, near-black with one neon accent, or a purple-to-blue gradient.
