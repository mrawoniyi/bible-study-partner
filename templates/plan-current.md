---
active_plan: state/plans/<YYYY-MM-DD>.md
current_day: 0
status: active   # active | completed | abandoned | none
---

The pointer file. One line of truth: which plan is running and which day is next.

`current_day` is the day about to be studied, not the last one finished. It is bumped at the end
of the Completion procedure, after the journal entry is written.
