# Adapter — Notion

Optional. Set `journal: notion` in `settings.md` if you want completed sessions and reflections
mirrored into a Notion database as well as written to `journal/`.

The file in `journal/` is written either way. Notion is a mirror, never the source of truth, and
`state/` is never mirrored anywhere.

## What you need

A database with three properties. The names are yours; tell the engine which is which.

| Property | Type | Holds |
|---|---|---|
| Title | title | The entry title, without the "Day N:" prefix |
| Date | date | The entry's date |
| Type | select or multi-select | `Daily Devotion`, `Reflections`, `Imported` |

Two more are worth adding if you want to browse by them later: a select for the plan or concept
title, and a select or multi-select for the biblical book covered.

## How the body maps

The journal entry's markdown headings become the page's structure. The simplest mapping is
heading-for-heading: each `## …` in the entry becomes a heading block, with the verbatim text
beneath it. If you prefer a page you can scan, make each one a toggle instead and put the verbatim
text inside, so the page opens as a list of questions and you expand the ones you want to reread.

## Wiring it up

The engine does not ship an integration. Give it whatever Notion access your harness already has:
an MCP server, a CLI, or the REST API with your own integration token. Then tell it, once, in
`settings.md` or in a line at the top of this file, which database to write to and which property
is which. It will follow that on every completion.

Two things to check on your first entry, because they are where Notion writes usually go wrong:

- **Properties beyond the title are easy to drop.** Whatever route you use, create the page with
  the select and date properties in the same call, then open the page and confirm they are set.
  A title-only create that silently loses `Type` looks like a success.
- **Rollups and formulas are read-only.** If your date is a rollup from a related page rather than
  a real date property, it cannot be written. Use a plain date property for the entry's own date.

Run one full session and look at the result before trusting it. If the mirror fails, the entry is
still in `journal/`, and nothing is lost.
