# CSK Info – Player Performance Analytics

A data-driven analytics dashboard for Chennai Super Kings players, built step by step as a learning project (frontend → database → API → analytics → real-time data → ML → predictions).

> **Status:** Level 1 (frontend) complete, with data loaded from a manually maintained Excel sheet. Backend, database, live data and ML are on the roadmap.

> **Disclaimer:** This is an unofficial fan project for learning. It is not affiliated with, endorsed by, or connected to Chennai Super Kings, the BCCI or the IPL. Statistics are entered manually and may contain errors.

## Screenshots

<!-- Add your screenshots to a docs/ folder and uncomment: -->
<!-- ![Home](docs/home.png) -->
<!-- ![Analytics](docs/analytics.png) -->
<!-- ![Current Form](docs/form.png) -->

## Features

- **Team** – full squad with role, nationality and age
- **Achievements** – championship history
- **Analytics** – batting and bowling leaderboards, all-rounder ranking, progress toward team targets (500 sixes / 500 wickets)
- **Current Form** – post-IPL impact-point ranking, plus performances in other competitions (e.g. The Hundred, England series)
- **Excel-powered data** – update one spreadsheet, run one command, and the site refreshes

## Tech stack

| Area | Tools |
|---|---|
| Frontend | React 18, Vite, React Router, lucide-react |
| Data import | Python 3, openpyxl |
| Data source (for now) | Manually maintained Excel workbook |

## Getting started

**Requirements:** Node.js 18+ and Python 3.

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
npm install
pip install openpyxl
npm run sync-data
npm run dev
```

Open http://localhost:5173.

## Updating the data

1. Edit `data/CSK_report_2027.xlsx` (**Sheet1** only) and save and close Excel.
2. Run `npm run sync-data` – this regenerates `src/data/stats.json`.
3. Refresh the browser.

The importer finds the *Batsmans*, *Bowlers*, *Target* and *last updated* sections by their labels, so rows can be added freely. Player names are validated against `src/data/players.json`; unknown or duplicate names stop the import with a clear error. Alternative spellings can be mapped in `ALIASES` inside `scripts/import_excel.py`.

## Project structure

```
├── data/                  Excel workbook (source of truth for now)
├── scripts/import_excel.py   Excel → JSON importer with name validation
├── src/
│   ├── data/              players.json (squad), stats.json (generated)
│   ├── pages/             Analytics.jsx, CurrentForm.jsx
│   ├── analytics.js       Metric calculations
│   ├── App.jsx            Layout, routing, Home/Team/Achievements
│   └── styles.css
└── package.json
```

## How "impact points" work

Players are ranked with a simple reference formula (not an official rating):

`6s×1 + 50s×8 + 100s×20 + wickets×2 + 5W×10 + hat-tricks×15`

Weights live in `src/analytics.js` and can be tuned. The workbook only has season totals, so strike rate, economy and true recent-match form are not available yet.

## Roadmap

- [x] **Level 1 – Frontend** (React dashboard)
- [ ] **Level 2 – Database** (PostgreSQL: players, matches, per-match performances)
- [ ] **Level 3 – Backend + API** (FastAPI, replace JSON with API calls)
- [ ] **Level 4 – Analytics** (averages, strike rates, rolling form from match-level data)
- [ ] **Level 5 – Near-real-time data** (licensed cricket data API + scheduled ingestion)
- [ ] **Level 6 – Machine learning** (baseline first, time-based train/test split)
- [ ] **Level 7 – Predictions** (probabilities exposed through the API)

## Data notes

- Ages in `players.json` are reference values; the plan is to store date of birth and calculate age.
- Scraping Cricbuzz is avoided due to terms-of-service risk; the plan is a licensed API plus free historical data (e.g. Cricsheet).

## License

<img width="1900" height="911" alt="Screenshot 2026-10-10 101341" src="https://github.com/user-attachments/assets/4f2d704b-a108-4d9d-99f0-32bc49118c76" />
<img width="1895" height="902" alt="Screenshot 2026-10-10 101354" src="https://github.com/user-attachments/assets/5c0b729a-7cea-48c2-b14c-9c76f0638e3b" />
<img width="1902" height="882" alt="Screenshot 2026-10-10 101408" src="https://github.com/user-attachments/assets/89baf9ac-94b0-4e1e-803b-c04e494873c1" />
<img width="1888" height="900" alt="Screenshot 2026-10-10 101423" src="https://github.com/user-attachments/assets/fdcbcabe-317c-4980-ad14-db62e60237b2" />
<img width="1892" height="952" alt="Screenshot 2026-10-10 101436" src="https://github.com/user-attachments/assets/754fa146-0ced-4d95-87ad-7af28f850c22" />






Add a license of your choice (for example MIT) before sharing publicly.

