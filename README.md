# Bible Study Partner

A personal Bible study partner that runs multi-day, personalised study programmes end to end, in
conversation, on top of whatever AI harness you already use. It is a folder of markdown files. There
is no app, no account, no server, and nothing to install beyond copying the folder.

It learns who you are from your own journal if you keep one, or from seven questions if you do not.
Then it proposes study concepts in your own language, chooses a plan length from the evidence rather
than a template, and guides one session a day: how much time have you got, the passages one at a
time with an optional exploration menu, reflection questions asked one at a time and tiered to your
time, and prayer prompts. When you say you're done, it pulls out what you found, uses it to write
tomorrow in full, and files a journal entry holding your answers verbatim.

The point of the whole thing is the second week. Most study apps meet you fresh every morning. This
one has read what you said on Day 2, and today is built out of it. That only works because every
session is written to a file on your machine, and every later day reads those files.

## Which harness

| Tier | What you get |
|---|---|
| **Agents with a local folder** — Claude Code, Codex CLI, Gemini CLI, OpenCode, ChatGPT Work in the desktop app with this folder attached | **Best.** The full experience. The agent reads and writes the state files itself, so sessions resume after an interruption and every programme feeds the next one. |
| **Chat-app projects** — a Claude Project, a custom GPT or ChatGPT on web or mobile, a Gemini Gem | **Works for one programme.** No filesystem, so state lives in a single pasteable note (`templates/state-note.md`). You lose automatic resume and long-term feed-forward across programmes. |
| **Messaging-bot runtimes** — an agent you already run in a chat app | **Full experience**, if you already have one. State lives on the machine running the bot; you study from your phone. See `adapters/messaging-bots.md`. |
| **Your own build** — an agent SDK, your own loop | **Full control, most work.** `SKILL.md` is the system prompt; give the model file read and write on this folder. |

## Install

**Claude Code.** Copy this folder into `.claude/skills/` in a project, or into `~/.claude/skills/`
to have it everywhere. Then just talk to it.

```
# if your installer supports it
npx skills add <your-fork>/bible-study-partner
```

**Codex CLI, Gemini CLI, OpenCode, and anything else that reads `AGENTS.md`.** Copy the folder
anywhere and start the agent inside it. `AGENTS.md` points at `SKILL.md`; that is the whole wiring.

**ChatGPT Work (desktop app).** Create a project, attach this folder to it, and add the folder as a
skill (it is already in the `SKILL.md` shape ChatGPT expects). ChatGPT can read and change files in
an attached folder, so `state/` and `journal/` work as on the CLIs. On web and mobile there is no
folder access, so use the chat-app steps below instead.

**Chat apps.** Paste the contents of `SKILL.md` into the project's custom instructions. Keep
`templates/state-note.md` somewhere you can copy from, paste it at the start of each session, and
paste the updated version back at the end.

## First run

Say anything. If `profile.md` does not exist, the partner starts with one question:

> Do you keep a journal, prayer diary or notes about your faith? If so, point me at it. If not,
> I'll ask you seven questions.

**If you have a journal** — a folder of markdown or text files, or an export from Notion, Day One,
Apple Notes or Google Docs — it reads it, writes a faith profile in your own phrases, and reads that
profile back to you for correction before it does anything else. Your entries are copied into
`journal/` as dated files. Then it asks only the questions your journal did not answer, which is
usually two.

**If you don't**, it asks the seven, one at a time, as a conversation rather than a form.

Both routes end at the same place: `profile.md`. Everything after that reads the profile, your
journal and your past sessions.

Open `example/` to see what a real first day looks like: a fictional person's profile, plan, session
file and journal entry.

## Saying things to it

| Say | It does |
|---|---|
| "new study plan" | Proposes five concepts from your own material. You can also just name your own topic. |
| "let's study" | Starts today's session. Asks how much time you have first. |
| "I'm done with Day 3" | Extracts insights, writes tomorrow in full using them, files your journal entry, moves the pointer. |
| "journal this…" | Files a free reflection, outside any session. |
| "what day am I on" | A two-line status. |

## Where everything lives

```
bible-study/
  SKILL.md                      the engine
  AGENTS.md                     pointer for agents that read AGENTS.md
  settings.md                   yours to edit
  profile.md                    written by onboarding
  state/
    plan-current.md             which plan, which day
    plans/<YYYY-MM-DD>.md       one file per programme
    sessions/<YYYY-MM-DD>.md    one file per session, written as it runs
  journal/
    <YYYY-MM-DD>-<slug>.md      one file per completed session, reflection or import
```

This layout is a contract, not a suggestion. Other tools can read these files, so the field names
in `SKILL.md` are fixed. Templates for each file are in `templates/`.

`settings.md` holds your name, your translation, how long each time tier means, and one line saying
where journal entries go: `folder` (the default), `obsidian`, `notion` or `none`. You are never
asked this during onboarding. Only the journal destination is ever adapted — `state/` is always
plain files right here. See `adapters/`.

## What each tier loses

**Chat apps** lose resume and feed-forward. An interrupted session restarts rather than picking up,
and the partner only knows what is in the note you pasted, so the eighth programme is no better
informed than the second. One programme at a time works well.

**`journal: none`** loses the compounding. The engine still runs, but there is nothing for the next
programme to be built from, and the final-day read-back will be thin.

**No web access** loses the BibleProject option in the exploration menu and makes passage lookup
harder. The partner will say so rather than inventing a video or a verse.

## Privacy

Everything stays on your machine. No accounts, no sync, no telemetry, nothing phoned home. The only
thing that leaves is whatever your AI harness already sends to its own model provider in the course
of the conversation, which is the same as any other chat you have with it. If you set
`journal: notion`, entries also go wherever you point that, and that is your choice to make.

If you fork this, `.gitignore` already keeps `profile.md`, `state/` and `journal/` out of git.

## Scripture accuracy

Language models misquote scripture. They misquote it fluently, which is worse. Translations are
under copyright too, so the engine is told to check a quote against a real Bible or fetch it from a
source your harness can reach, and to give you the citation to read yourself rather than producing
text it cannot verify. Keep a Bible next to you. If a quoted verse looks off, it may well be.

## Limitations

- **Imports are text only.** PDFs and photographs of handwritten journals are out of scope. If that
  is where your journal lives, use the questionnaire route and add entries as you go.
- **Models drift.** The same instructions produce noticeably different sessions on different models
  and different versions of the same model. Run one full session on your harness before trusting it
  with anything that matters, and check that it wrote the files it said it wrote.
- **Nothing is scheduled.** The partner runs when you start it. `adapters/nudge.md` covers wiring a
  reminder, and argues against building a streak counter.
- **It is not pastoral care.** The engine is told to drop all structure and suggest human support if
  you are in real distress, but it is a study partner, not a counsellor and not a substitute for
  your church, your friends or a crisis line.

## Licence

MIT. See `LICENSE`.
