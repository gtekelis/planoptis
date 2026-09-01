# Planoptis

**English** · [Ελληνικά](README.el.md) — [planoptis.com](https://www.planoptis.com)

A plain-text planning format for people who want a bullet-journal without an app.

One `.txt` file, indented with tabs, opened in an editor that folds by
indentation (Sublime Text, but any folding editor works). Collapse a month to see
the year, expand a day to see the work. No database, no lock-in, greppable
forever, syncs anywhere, survives every app that will ever be discontinued.

> **The name.** Planoptis is inspired by the Greek word "panoptis" — one who sees
> everything. Replace "pan" with "plan", and you get a planning system built
> around one idea: keeping your whole plan visible at all times.

Two demo files show the whole thing in use:

- [`planoptis-demo-en.txt`](planoptis-demo-en.txt)
- [`planoptis-demo-el.txt`](planoptis-demo-el.txt) — the format is language-agnostic

---

## File anatomy

A plan has three top-level sections, each opened by an icon heading:

| Section | Heading | Purpose |
|---|---|---|
| Projects | `💻 PROJECTS` | Standing projects and their intent. Rarely changes. |
| Monthly plan | `🗒️ MONTHLY PLAN` | One block per month. The month in focus is marked `🟩`. |
| Daily log | `🗓️ SEPTEMBER` | One block per month, then one block per day, then the work. |

Inside the daily log, each day is grouped by **topic / client**: a label line
followed by a `-----` rule, then the tasks for that topic.

```
🗓️ SEPTEMBER
=======================================================
=======================================================

	Tuesday 01-09-2026
	=============================================

		Website
		-----------------------------------------
		- ✅ Create repository
		- Responsive menu
		- Contact form
			| Validate before submit
```

---

## Indentation & folding

- **Indent with tabs.** One tab per level. Consistency is what makes folding and
  highlighting work.
- Fold/unfold from the editor's gutter triangles or its code-folding commands.
  Fold a section to skim, unfold to work.
- Keep lines short. Long lines run off the screen; push detail into `|` notes on
  the next level instead of writing one long sentence.

---

## Line vocabulary

### Structure

| Line | Meaning |
|---|---|
| `PLANOPTIS — …` | First line, the plan's title. |
| `💻` / `🗒️` / `🗓️` heading | One of the three top-level sections. |
| `SEPTEMBER` | Month heading. |
| `🟩 SEPTEMBER` | The **current month** — its name is highlighted. |
| `Tuesday 01-09-2026` | Day heading. Weekday + `DD-MM-YYYY`. |
| `Label` above a `-----` rule | Topic / client grouping within a day. |
| `=====` , `-----` | Visual separators. |

### Tasks

Every task is a `-` line. A marker is an emoji placed **right after the dash**:
`- <marker> text`. No marker means an ordinary open task.

| Marker | Line | Means | Colour |
|---|---|---|---|
| _(none)_ | `- Responsive menu` | Open task | default |
| `✅` | `- ✅ Create repository` | Done | green |
| `🆘` | `- 🆘 Renew server before expiration` | Urgent / blocking | red |
| `⚠️` | `- ⚠️ Check mobile layout` | Watch / risk / needs verifying | amber |
| `⏭️` | `- ⏭️ Prepare demo` | Deferred — do next / carried forward | accent |
| `➡️` | `- ➡️ Send figures to Maria` | Handed off / delegated | accent |

`⏩` is accepted as an alias of `⏭️`.

### Notes

| Line | Meaning |
|---|---|
| `\| detail` | A note or sub-detail under the task above it, one level deeper. |

Use `|` notes for sub-steps, acceptance criteria, decisions, and anything that
would otherwise make a task line too long.

---

## Marker placement rule

Markers always come **immediately after the `-`**, one per line:

```
- 🆘 Check available disk space      ✅ correct
🆘 - Check available disk space      ✗ old form (still highlighted, don't write new ones)
- Check available disk space 🆘      ✗ not recognised
```

---

## New-day template

Copy this block to start a new day in the daily log — day heading at one tab,
topic labels at two:

```
	Wednesday 03-09-2026
	=============================================

		Topic / Client
		-----------------------------------------
		- 
			| 
```

Rename the day, add one topic label per client or area, then list the tasks
under each. In Sublime you can save it as a `.sublime-snippet` with a
tab-trigger (e.g. `day`) so a fresh day is one keystroke.

---

## The weekly ritual

The format is nothing without the habit that keeps it honest:

- **End of day** — mark what's done `✅`. Anything untouched that still matters:
  `- ⏭️` and copy it under tomorrow.
- **End of week** (see the `Planning` topic in the demo) — review the week, move
  unfinished tasks into next week, capture new ideas, set Monday's priorities.
- **Start of month** — move the `🟩` to the new month in `MONTHLY PLAN`, break its
  goals into the first few days.

Nothing gets silently dropped: it's either `✅`, `⏭️` forward, `➡️` to someone
else, or deleted on purpose.

---

## Editor setup

### Sublime Text

**1. Install the syntax.** In Sublime, open *Preferences → Browse Packages…* —
this opens the `Packages/` folder. Copy
[`Planoptis.sublime-syntax`](Planoptis.sublime-syntax) into the `User/`
subfolder (`Packages/User/`). Sublime picks it up immediately; no restart.

**2. Apply it to a file.** Open your plan file, then either:

- click the syntax name at the bottom-right of the status bar and choose
  **Planoptis**, or
- use the menu *View → Syntax → Planoptis*.

**3. Make it automatic (optional).** With a plan file open and Planoptis
selected, choose *View → Syntax → Open all with current extension as… →
Planoptis*. From then on every file with that extension opens as Planoptis. Use
this with a dedicated extension like `.planoptis` rather than `.txt`, so you
don't turn *every* text file into a plan.

**4. Fold.** Use the triangles in the gutter, or *Edit → Code Folding*
(*Fold All* / *Unfold All*, and *Fold Level 1–9*).

### Other editors

There's no grammar bundled yet, but the format is designed to degrade
gracefully — it's just an indented text file:

- **VS Code** — set the file to plain text; folding follows indentation.
- **Vim / Neovim** — `:setlocal foldmethod=indent`.
- **Emacs** — `outline-minor-mode` or `origami.el`.

---

## License

[MIT](LICENSE) — use it, change it, ship it in anything, just keep the copyright
notice.
