# Settings

Edit these. The engine reads this file at the start of every procedure.

```yaml
# What to call you.
name: [YOUR NAME]

# The Bible translation to quote. Translations are under copyright: the engine checks quotes
# against a real Bible or fetches them from a source the harness can reach, and gives you the
# citation to read yourself rather than inventing text it cannot verify.
translation: NIV

# How much the partner says per turn. Short is the point.
words_per_turn: 100-150

# What each time tier means, in minutes. The engine asks which one you have at the start of
# every session; the answer sets how many questions get asked.
tiers:
  quick: 5-10
  standard: 15-20
  deep: 30+

# Where completed sessions and reflections are filed.
#   folder   — markdown files in ./journal/ (default, nothing else needed)
#   obsidian — the same files, inside an Obsidian vault; set journal_path
#   notion   — also mirrored to a Notion database; see adapters/notion.md
#   none     — no journal entries written at all
journal: folder
journal_path: ./journal

# Your timezone, and when you'd like to be nudged to study. The engine does not schedule
# anything by itself; see adapters/nudge.md for wiring this to a cron job or a phone alarm.
timezone: Europe/London
nudge: 07:30 daily
```
