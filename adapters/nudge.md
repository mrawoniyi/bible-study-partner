# Adapter — nudges

The engine never schedules anything. It runs when you start a session. If you want a daily prompt,
wire it up outside the package. `settings.md` carries a `nudge:` line so the engine knows what time
you meant, but nothing reads it automatically.

Pick whichever of these you will actually keep.

## A phone alarm

The one most people stick with. An alarm or a repeating reminder at your study time, labelled with
the trigger phrase, so you open the chat and type "let's study". No setup, no machine that has to be
awake, and it reaches you wherever you are.

## An OS scheduler

If the partner runs on a machine that is on anyway, schedule a command that starts the session and
leaves the result where you will see it.

- **macOS**: a `launchd` agent with `StartCalendarInterval`, or `cron` if you already use it.
- **Linux**: a `systemd` timer, or a `cron` entry.
- **Windows**: Task Scheduler, daily trigger.

What the scheduled command does depends on the harness. Usually it is the CLI in non-interactive
mode with a short prompt: start today's session for the active plan and send me the opening. Send
the output somewhere you read, not to a log file you will never open.

## A scheduler inside your harness

Some harnesses have their own recurring-task feature. If yours does, use it: it already has the
context, and it will not silently stop working when a path changes.

## Two cautions

**A nudge must not start the session without you.** The time check is the first step for a reason:
the tier comes from how much time you actually have this morning, and nothing can guess that. A
nudge opens the door. You walk through it.

**A missed day is not a broken plan.** The pointer holds `current_day` until a session completes, so
a plan waits as long as it needs to. Do not build a streak counter. Whatever you are studying is
worth more than the streak, and a streak turns a missed morning into a reason to stop.
