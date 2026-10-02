# Movie Releases Calendar — Setup

A free, auto-updating iCal feed of upcoming US theatrical releases, built from
Wikipedia's "List of American films" pages. Subscribe once in Apple Calendar —
new movies appear automatically every week. No API keys, no accounts, no cost.

This package contains everything the GitHub repo needs. The `movies.ics` file
was freshly generated today (229 upcoming releases).

## Setup (about 10 minutes)

### 1. Create the GitHub repo

- On GitHub, create a new **public** repository named `movie-ical`.
- Upload all files from this folder, preserving the folder structure
  (`.github/`, `docs/`, `scripts/`). You can drag-and-drop in the GitHub web UI
  or push via git.

### 2. Enable GitHub Pages

- Repo Settings → Pages → Source: **Deploy from a branch** → Branch: `main`,
  folder: `/docs` → Save.
- Wait a minute for the first deploy.

### 3. Run the updater once

- Go to the **Actions** tab → **Update Movie Calendar** → **Run workflow**.
- Wait ~20 seconds. This commits a fresh `movies.ics`.

From here on, the workflow runs automatically every Monday at 8am UTC and
keeps the feed current forever.

### 4. Subscribe in Apple Calendar

**On Mac:** Calendar → File → New Calendar Subscription → enter:

```
https://YOUR-USERNAME.github.io/movie-ical/movies.ics
```

(replace YOUR-USERNAME with your GitHub username)

Set auto-refresh to **Every week**. Done.

**On iPhone/iPad:** Settings → Apps → Calendar → Calendar Accounts →
Add Account → Other → Add Subscribed Calendar → paste the same URL.

## How it works

- GitHub Actions runs weekly, scrapes Wikipedia's film release tables,
  rebuilds `movies.ics`, and commits it.
- GitHub Pages serves the file at a permanent public URL.
- Apple Calendar polls that URL and syncs new events automatically.

## Files

- `docs/movies.ics` — the calendar feed (regenerated weekly by the Action)
- `docs/index.html` — simple landing page for the Pages site
- `scripts/build.js` — the scraper (Node.js, no dependencies)
- `.github/workflows/update.yml` — the weekly schedule
