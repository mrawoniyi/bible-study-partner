# Adapter — Obsidian

Obsidian is the simplest destination there is, because an Obsidian vault is a folder of markdown
files. This adapter changes nothing about how entries are written; it only changes where they land.

## Setup

In `settings.md`:

```yaml
journal: obsidian
journal_path: /path/to/your/vault/Bible study
```

Create that folder in your vault if it does not exist. Entries are written there with exactly the
same frontmatter and headings as the `folder` destination, so Obsidian's properties panel picks up
`type`, `date`, `plan` and `day` without any configuration.

## What this gets you

- **Backlinks.** Change `plan: state/plans/2026-01-05.md` to a wikilink if you want the plan to show
  its sessions in the graph.
- **Dataview.** `type` and `date` in frontmatter are enough for a table of every Daily Devotion, or
  a count by month.
- **Daily notes.** If you keep daily notes, link the entry from that day's note. Do this by hand or
  with a template; the engine does not write to anything outside `journal_path`.

## What does not move

`state/` stays where the package is. Plans, sessions and the pointer are working state, not
journalling, and they are never adapted. Keeping them out of the vault also keeps a half-finished
session out of your notes.

If you want the whole package inside the vault, that works too: put the folder in the vault and
leave `journal_path` as `./journal`. Just add `state/` to your Obsidian exclusion list so
in-progress session files do not clutter search.
