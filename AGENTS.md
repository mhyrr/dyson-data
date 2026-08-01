# AGENTS.md — Dyson Sensor Network Data

## What This Is

The data output repo for Dyson's financial intelligence sensor network. All scan results are pushed here by automated Hermes cron jobs via `git commit + push`. No human edits needed — but Greg can browse everything on GitHub.

This is a **record of collected intelligence**. No trading signals, no positions, no P&L. Raw scan JSON + daily digests.

## Repo Layout

```
scans/
  YYYY/MM/DD/
    13f/        # 13F holdings scan JSON (daily)
    earnings/   # Earnings news scan JSON (2x daily weekdays)
    web/        # Web search scan JSON (2x daily)
    youtube/    # YouTube interview scan JSON (pending API key)
    x/          # X/Twitter scan JSON (pending xurl auth)
  latest/       # Most recent scan per type (overwritten each run)
    13f_latest.json
    earnings_latest.json
    web_latest.json
  state/        # Dedup watermarks (.seen files)
digests/        # Daily markdown + HTML summaries
  YYYY-MM-DD.md
  YYYY-MM-DD.html
alerts/         # High-signal items flagged for review
docs/           # GitHub Pages site (HTML digests, index page)
  index.html
  digests/
    YYYY-MM-DD.html
  style.css
README.md
```

## How Data Gets Here

1. Hermes cron triggers `run_scan.sh <type>` in the engine repo
2. Scanner writes JSON to engine `data/<type>/latest.json`
3. `run_scan.sh` copies it to `scans/YYYY/MM/DD/<type>/<type>_YYYYMMDD_HHMMSS.json`
4. `run_scan.sh` copies to `scans/latest/<type>_latest.json`
5. `push_data.sh` does `git add -A && git commit && git push`

Every scan = one commit. Commit history is the timeline.

## Reading the Data

- **Start here:** `digests/YYYY-MM-DD.md` — human-readable daily summary
- **Latest state:** `scans/latest/` — what the most recent scan of each type found
- **Historical:** `scans/YYYY/MM/DD/` — browse any day's raw scans
- **Actionable:** `alerts/` — items flagged as high-signal
- **GitHub Pages:** `docs/index.html` — styled HTML digest viewer at `https://mhyrr.github.io/dyson-data/`

## JSON Schema (per signal type)

### 13F (`scans/.../13f/13f_*.json`)
```json
{
  "run_time": "ISO timestamp",
  "funds_checked": 10,
  "filings_extracted": 8,
  "new_filings": 8,
  "watchlist_matches": [
    {"fund": "...", "ticker": "...", "value": 0, "rank_in_fund": 1, "is_new_filing": false}
  ]
}
```

### Earnings (`scans/.../earnings/earnings_*.json`)
```json
{
  "run_time": "ISO timestamp",
  "tickers_checked": 29,
  "new_items_count": 3,
  "new_items": [
    {"ticker": "...", "title": "...", "link": "...", "date": "...", "source": "yahoo_finance"}
  ]
}
```

### Web (`scans/.../web/web_*.json`)
```json
{
  "run_time": "ISO timestamp",
  "queries_run": 34,
  "results_count": 0,
  "results": [
    {"title": "...", "url": "...", "query": "...", "sector": "...", "sector_label": "..."}
  ]
}
```

## What Not to Do

- Don't edit scan JSON files manually — they're machine-generated
- Don't delete `scans/state/` files — those track dedup watermarks
- Don't change the directory structure — scanners depend on it
- Don't add `.gitignore` rules for JSON or markdown — those ARE the data

## Source of Truth

- Engine repo: `mhyrr/dyson-trading` (scripts, config, docs)
- Architecture doc: `mhyrr/dyson-trading/docs/dyson-data-architecture.md`
- The agent writes here but never modifies the engine repo's config from here
