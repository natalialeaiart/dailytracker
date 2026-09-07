# Daily Tracker

A small offline app for tracking what you actually do each day — sport, study, job search, content, anything you decide matters. It runs entirely in the browser: no accounts, no server, no analytics. Your data never leaves your phone.

Made by [Natalia Le](https://www.instagram.com/nataliale_aiart) · [AI Test Tube on Telegram](https://t.me/AI_Test_Tube)

## How it works

- Open the link on your phone, set a 4-digit PIN, and start tracking.
- Everything is saved in your browser's local storage. Nobody else can see it — not even the person hosting the page.
- Each person who opens the link gets their own private copy with their own PIN.

## Install on your phone

Adding the app to your Home Screen makes it open like a native app, work offline, and — most importantly — protects your data from being cleared by the browser.

- **iPhone (Safari):** tap Share → *Add to Home Screen*.
- **Android (Chrome):** tap the ⋮ menu → *Add to Home screen* or *Install app*.

## Backups

Your data lives only in this browser. Clearing browser data erases it, and it won't follow you to a new phone by itself.

- **Backup** (Settings → Backup) saves everything to a `.json` file. Keep it somewhere safe.
- **Restore from backup** loads that file on any phone — metrics, full history, settings.
- The PDF report (coming in a later stage) is for reading, not for restoring.

## Deploy your own copy

This is a single `index.html` file with no build step. Any static host works.

### GitHub Pages

1. Create a new repository and add these files: `index.html`, `README.md`, `.github/workflows/deploy.yml`.
2. In the repository go to **Settings → Pages → Build and deployment → Source** and choose **GitHub Actions**.
3. Push to `main`. The workflow publishes the site at `https://<username>.github.io/<repository>/`.

### Cloudflare Pages

Create a project, connect the repository (or upload the folder directly), leave the build command empty, set the output directory to `/`. Done.

**One rule:** once you've shared the link with anyone, don't change the address. Data is tied to the domain — moving the app to a new URL means everyone starts from an empty tracker unless they restore from a backup.

## Data model

Three keys in `localStorage`:

| Key | Contents |
|---|---|
| `tracker.v1.settings` | PIN hash, language, week start, last backup date |
| `tracker.v1.metrics` | Your list of metrics — name, type, goal, category, order |
| `tracker.v1.entries` | `{ "YYYY-MM-DD": { metricId: value } }` |

Metric types: `check` (yes/no), `minutes`, `number`, `number_note` (number plus a short text), `note`.

The PIN is hashed before storage, but the data itself is not encrypted. It's a lock against casual access, not against someone with technical skills and your unlocked phone.

## Roadmap

| Stage | What | Status |
|---|---|---|
| 1 | Core app: PIN, today screen, day navigation, backup and restore, EN/RU | done |
| 2 | Add, edit, reorder and archive metrics | planned |
| 3 | Statistics: heatmap, streaks, category ring, per-metric charts | planned |
| 4 | Monthly PDF report | planned |
| 5 | Onboarding with presets, PWA install files, home-screen prompt | planned |
| 6 | Share your metric setup via link | planned |

## Tech

Plain HTML, CSS and JavaScript in one file. No frameworks, no dependencies, no build.
