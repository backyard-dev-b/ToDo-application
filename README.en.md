# Anti-Vision ToDo

[🇯🇵 日本語](./README.md) | [🇺🇸 English](./README.en.md)

A to-do / habit-tracking app built around **loss aversion**, the behavioral-economics principle that people feel the pain of losing something more strongly than the pleasure of gaining something equivalent.

Instead of painting an idealized future like a vision board, this app has you write down the **future you want to avoid** — what happens if nothing changes — and then log the actions you take to steer away from it.

## Why "Anti-Vision"

Most habit-tracking apps are built around positive reinforcement: achievements, streaks, badges. This app takes the opposite approach, leaning on loss aversion:

- Your avoided future stays written out, in concrete terms, always visible
- Instead of recording *why* you're doing a task, you record *what you actually did* afterward
- Your sense of "am I keeping this up?" is made unflinchingly visible through a calendar and hard numbers

## Features

- **Multiple Anti-Visions** — each Anti-Vision keeps its own independent log, calendar, and streak (switch between them with tabs)
- **Action log** — record what you did, where, how long it took, how deep the effort was, and a free-text reflection. Time can be picked manually or measured live with a built-in stopwatch
- **Custom categories** — location tags, task categories, and the depth-of-effort levels (name, count, and order) are all freely editable, with drag-to-reorder that works on both mouse and touch
- **Monthly calendar** — a color-coded calendar reflecting whether and how deeply you acted each day, with month-to-month paging
- **Continuity dashboard** — current streak, best streak, continuity rate, total time, average quality, and more
- **JSON export** — back up all your data as a single JSON file

## Tech stack

- Plain HTML / CSS / JavaScript only — no framework, no build step
- No external libraries (only a Google Fonts stylesheet is loaded)
- All data lives in the browser's `localStorage`. Nothing is ever sent to a server

## Usage

Double-clicking `anti-vision-todo.html` will technically run it, but when a page is loaded from a `file://` URL, `localStorage` behavior is undefined and inconsistent across browsers (this is explicitly documented by MDN). Your data may disappear if you switch browsers or move the file. We recommend instead:

- **Running a simple local server** (from this folder):
  ```
  python3 -m http.server
  ```
  then open `http://localhost:8000/anti-vision-todo.html`
- Opening it with the **Live Server** extension in VS Code

## How data storage works

All data is stored using the browser's **localStorage** feature. There is no server or database involved anywhere.

- **Format**: the app's full state (Anti-Visions, action logs, categories, etc.) is bundled into a single object and serialized with `JSON.stringify()` under the key `anti-vision-todo-state-v3`:
  ```js
  localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
  ```
- **Where it physically lives**: as real files on your device's disk, in a browser-specific format (LevelDB for Chrome/Edge, SQLite for Firefox, etc.)
- **Scope**: isolated per browser *origin* (protocol + domain). Other sites, and even other browsers on the same machine, can't see it
- **Not synced across devices**: even with Chrome Sync signed in and enabled, localStorage is not part of what gets synced — opening the app on a different device starts from an empty state
- **Not the same as cache**: clearing your browser's "cached images and files" won't touch it; clearing "cookies and site data" will

## Data & privacy

All data (your Anti-Vision text, action logs, everything) is stored only inside your own browser. Nothing is ever transmitted to an external server. Clearing your browser's site data will delete your saved records, so keep that in mind.

## Contributing

Improvements, bugs, ideas — Issues and Pull Requests are all welcome. Feel free to leave a comment with anything.

## License

MIT License. See [LICENSE](./LICENSE) for details.
