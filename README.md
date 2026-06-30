# P0/P1 Incident Tracker

A standalone web application for analyzing DispatchTrack P0/P1 bugs and outages.
Upload weekly CSV exports from Google Sheets, and the app categorizes issues,
extracts RCA from comments, and tracks repeat patterns over time.

## Features

- **Weekly CSV upload** — export your Google Sheet as CSV and drop it in
- **AI-powered analysis** — extracts RCA from comment threads, categorizes issues
- **Cumulative tracking** — data persists in the browser across sessions; each week merges in
- **Duplicate detection** — tickets already in the database are skipped on re-upload
- **Repeat pattern detection** — surfaces recurring issues by category and customer
- **Customer breakdown** — per-customer incident counts, P0 rate, and repeat rate
- **Insights** — auto-generated recommendations for product improvement
- **Export** — download full dataset as CSV anytime

## Hosting on GitHub Pages (free)

### Option 1 — New repository (recommended)

1. Go to [github.com](https://github.com) and sign in
2. Click **New repository**
3. Name it `p0p1-tracker` (or anything you like)
4. Set it to **Public** (required for free GitHub Pages)
5. Click **Create repository**
6. Click **uploading an existing file**
7. Drag and drop `index.html` into the upload box
8. Click **Commit changes**
9. Go to **Settings → Pages**
10. Under **Source**, select `Deploy from a branch`
11. Choose `main` branch and `/ (root)` folder
12. Click **Save**
13. Wait ~60 seconds, then visit `https://YOUR-USERNAME.github.io/p0p1-tracker`

### Option 2 — GitHub CLI

```bash
gh repo create p0p1-tracker --public
cd p0p1-tracker
cp /path/to/index.html .
git add index.html
git commit -m "Initial deploy"
git push
gh repo edit --enable-pages --branch main
```

### Option 3 — Netlify (drag and drop, no account needed for 100 sites)

1. Go to [app.netlify.com/drop](https://app.netlify.com/drop)
2. Drag the `index.html` file onto the page
3. You get a live URL instantly (e.g. `https://random-name-123.netlify.app`)
4. Optional: link a custom domain or rename the site in Netlify settings

## Setup: API key (optional but recommended)

The app works without an API key using keyword-based categorization.
For AI-powered RCA extraction from complex comment threads:

1. Get an API key from [console.anthropic.com](https://console.anthropic.com)
2. Open the app → **Settings** → paste your key
3. The key is stored only in your browser's `localStorage` — never sent anywhere except Anthropic's API

## How to export from Google Sheets

1. Open your weekly P0/P1 sheet
2. **File → Download → Comma Separated Values (.csv)**
3. Upload the downloaded `.csv` in the app

### Expected columns (app auto-detects these)

| Column | Used for |
|--------|----------|
| Issue key / Jira ID | Unique identifier, deduplication |
| Summary | Ticket title |
| Customer | Customer account name |
| Priority | P0 or P1 |
| Description | Issue description |
| Comment, Comment.1, Comment.2, ... | RCA is extracted from these |
| Week / Date | Optional — you can set a label at upload time |

## Data storage

All data is stored in the **browser's localStorage** on the device you use.

- Persists across page refreshes and browser restarts
- Private to your device — not synced to any server
- Export to CSV regularly as a backup
- To use on a different device, export CSV → clear data on new device → re-import

## Tech stack

- Pure HTML, CSS, and vanilla JavaScript — zero build step
- [PapaParse](https://www.papaparse.com/) for CSV parsing
- [Anthropic Claude API](https://docs.anthropic.com) for AI analysis (optional)
- Fonts from Google Fonts (Inter + JetBrains Mono)
