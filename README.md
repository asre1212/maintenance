# Toolbox

A clean, local-first iPhone web app for tracking items and their maintenance schedules. All data lives in your phone's browser storage — nothing is uploaded anywhere.

## Features

- iOS-style design that looks at home on iPhone (light + dark mode)
- Table-of-contents list view with status dots, search, and filter tabs
- Card view when an item is selected, with notes, dates, schedule, and next-due date
- Add a maintenance schedule per item — every N days, weeks, months, or years
- Color-coded status: green (on track), amber (due within 30 days), red (overdue)
- Quick stats dashboard: Overdue · Due Soon · On Track
- One-tap **Mark Done Today** to bump the schedule
- Export / Import a full JSON backup to move between phones
- Export everything to a real Excel `.xlsx` file
- Works offline once loaded (PWA service worker)
- "Add to Home Screen" makes it look like a native app

## Install on iPhone

1. Push this folder to a GitHub repo (see below).
2. Enable **GitHub Pages** for the repo.
3. Open the published URL in **Safari** on your iPhone.
4. Tap the **Share** button → **Add to Home Screen**.
5. Launch it from the home screen — it runs full-screen like a native app.

## Deploy to GitHub Pages

```bash
# from inside the toolbox folder
git init
git add .
git commit -m "Initial commit: Toolbox"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

Then in the repo on github.com:

1. **Settings → Pages**
2. Under **Build and deployment**, set **Source** to `Deploy from a branch`
3. Select branch **main** and folder **/ (root)** — or **/docs** if you put files there
4. Save. Your site will be live at `https://<user>.github.io/<repo>/` in ~1 minute.

If you want the URL to be just `https://<user>.github.io/<repo>/toolbox/`, push the whole repo (with the `toolbox/` folder inside) and visit that subpath.

## Transferring data to a new phone

1. On the **old** phone: open Toolbox → ⚙ Settings → **Export Backup (JSON)**.
2. AirDrop / email / iCloud-Drive that `.json` file to your new phone.
3. On the **new** phone: install Toolbox the same way, open Settings → **Import Backup (JSON)**, and pick the file. Your items merge in.

## How statuses work

Each item can optionally have a maintenance schedule. The "next due" date is computed as `last-done-date + interval`. The status is then:

- **Overdue** (red) — past the due date
- **Due Soon** (amber) — within 30 days
- **On Track** (green) — more than 30 days away
- **No Schedule** (gray) — no schedule set; just a logged item with notes

Tapping **Mark Done Today** sets the date to today, which slides the next-due date forward.

## File layout

```
toolbox/
  index.html       — entire app (HTML + CSS + JS)
  manifest.json    — PWA manifest
  sw.js            — service worker (offline cache)
  icon.svg         — vector icon (wrench)
  icon-192.png     — PWA icon
  icon-512.png     — PWA icon
  README.md        — this file
```

## Privacy

Everything is stored in `localStorage` on your device. The Excel export uses a JS library loaded from a CDN once and then cached. There is no server, no account, no analytics.
