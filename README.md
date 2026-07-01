# 📚 Study Coach

A personal, no-login study planner that builds a day-by-day exam plan for you,
tracks what you actually get done, and reshuffles the rest automatically. It is a
single HTML file that runs entirely in your browser and works great on a phone.

## What it does

- **Builds your plan.** You add each exam with its exercise sheets / lectures and a
  rough hour estimate for each. The coach schedules the work backward from every
  exam date, soonest exams first.
- **Splits big items across days.** Anything longer than one study session is broken
  into parts (e.g. "Sheet 3 · part 2/4") and spread across several days so nothing
  ever exceeds your daily time limit.
- **Respects your time.** You set how many hours you can study per day (default 5.5)
  and your session length (default 45 min). The plan never books more than that.
- **Works around your days off.** Mark weekdays you never study and specific away
  dates. Those days are skipped and the work is packed into the days you are around.
  Off days are shown in the plan so you can see them being respected.
- **Follows what you did and updates the plan.** Tick sessions off as you finish them.
  Anything you do not finish is automatically redistributed across your remaining days
  the next time the plan rebuilds.
- **Keeps you motivated.** A countdown to your next exam, overall progress %, a daily
  study streak 🔥, and rotating encouragement.

## How to use it

1. **Open `index.html`** in any browser (double-click the file, or open the deployed URL).
2. Go to the **Exams** tab and add an exam:
   - Exam name and date.
   - One row per exercise sheet / lecture: a **name**, a **type**
     (Exercise sheet, Lecture, Reading, Revision, Practice exam, Other), and the
     estimated **hours** it will take.
3. The app jumps to the **Plan** tab and shows your full day-by-day schedule.
4. Each day, open the **Today** tab and check off sessions as you complete them.
5. Set your days off and daily hours under **Progress → Settings / Days off**.
6. Watch your streak and progress grow under the **Progress** tab.

## The four tabs

| Tab | What it shows |
| --- | --- |
| **Today** | Motivation banner, exam countdown, and today's sessions to tick off. |
| **Plan** | The full upcoming schedule, day by day, with days off marked. |
| **Exams** | Add / edit / delete exams and their items; per-exam progress. |
| **Progress** | Overall %, streak, hours studied, plus Settings and Days off. |

## How the scheduling works (in plain terms)

1. Every item's estimated hours are chopped into session-sized chunks.
2. Chunks are sorted by exam date (soonest first), keeping each item's parts in order.
3. Starting today, each chunk is dropped into the earliest day that still has free
   time and is not a day off, without exceeding your daily hour limit.
4. If something cannot fit before its exam, it is still scheduled but flagged
   **⚠ tight** so you know to add time or trim scope.
5. Whenever you tick a session off or change your settings, the remaining work is
   re-planned automatically.

## Your data & privacy

- Everything you enter is stored **only in the browser on your device**
  (via `localStorage`). There is no account, no server, and no database.
- Because of that, use the app in **one place** (e.g. your phone) as its home.
- **Export backup** (Progress tab) saves a dated JSON file of everything. The app
  shows when you last backed up and nudges you after a week.
- **Import backup** restores from one of those files — use it to recover your data or
  move it to another device/browser.
- **Reset everything** under Progress wipes all local data.

## Running / hosting

It is just one static file, so there is nothing to build.

- **Locally:** open `index.html` in a browser.
- **On your phone:** open the file or a hosted URL, then use *Add to Home Screen*
  so it behaves like an app.
- **Deployed (Vercel):** this repo can be imported at
  [vercel.com/new](https://vercel.com/new) with all default settings (no build step).
  Every push to `main` then redeploys automatically. Vercel only serves the static
  file over HTTPS; your study data stays on your device.

## Tech

- A single self-contained `index.html`: HTML, CSS, and vanilla JavaScript.
- No frameworks, no dependencies, no build tooling.
- State persisted in `localStorage` under the key `studyCoach.v1`.
