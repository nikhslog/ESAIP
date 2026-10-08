# DACH Signal Finder

Finds DACH companies (200–2,000 employees) that show buying signals for AI, using only free tools and public data.
No outreach happens anywhere in this tool.

## How it works

1. **Company pool**: pulls companies from Wikidata (free) filtered by country and employee count. You can also upload your own CSV (e.g. an Apollo export).
2. **Signals**: for each company, a free web search (DuckDuckGo, no API key) across 5 platforms (LinkedIn Jobs, StepStone, Indeed, XING, company careers page). Only job titles matching AI / data / automation / back-office keywords are kept.
3. **Verify**: opens every job page and reads its built-in job data (employer + date posted). Dead links and postings by other employers (e.g. recruiting agencies) are dropped. Sites that block bots (like Indeed) are flagged "check by hand".
4. **Clean**: drops postings older than 6 months, merges duplicates (same company + same job on 3 platforms = 1 event), and keeps the earliest date to show how long a role has been open.
5. **Score**: simple points per event (see `config.py`), ranked in the dashboard.

## Setup (10 minutes, one time)

1. Install Python 3.10+ from python.org (on Windows, tick "Add Python to PATH").
2. Open a terminal in this folder and run:
   ```
   pip install -r requirements.txt
   ```

## Run

```
streamlit run app.py
```
Your browser opens the dashboard. Go through tabs 1 → 2 → 3.

Results are saved in the `data/` folder, so you can close the app and come back.

## Scaling it

Everything you need to change is in `config.py`:
- **More platforms**: add a line to the signal's `platforms` (it's just a search query).
- **More signals** (new C-level, ERP migrations, AI programs…): copy the `hiring` entry in `SIGNALS` and change its queries and keywords.
- **Better scoring**: edit `SCORING`.
- **Better job matching**: add keywords to `categories`.
- **More companies**: raise "How many companies" in tab 1.

## Limits to know

- No API keys. If searches start failing, the search engine is asking you to slow down: raise `SECONDS_BETWEEN_SEARCHES` in `config.py` or wait 10 minutes.
- Wikidata misses some mid-sized companies. For better coverage, upload a CSV from Apollo's free tier.
- Always open the ⚠️ links yourself before sending results to anyone.
# ESAIP
