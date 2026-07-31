# Dyson Sensor Network — Data Repository

This repository receives automated scan output from the Dyson financial
intelligence agent. Data is pushed multiple times daily via Hermes cron jobs.

## Structure
- `scans/YYYY/MM/DD/<signal_type>/` — Raw scan JSON, date-partitioned
- `scans/latest/` — Most recent scan per signal type (overwritten each scan)
- `digests/YYYY-MM-DD.md` — Daily human-readable summary
- `alerts/` — High-signal items flagged for human review
- `scans/state/` — Dedup watermarks and seen-state

## How to read this
1. Start with `digests/` — the latest daily summary
2. Check `alerts/` for items flagged as actionable
3. Drill into `scans/latest/` for current raw data
4. Browse `scans/YYYY/MM/DD/` for historical scans

## Updates
Commits are automated. Each commit = one scan batch. See commit history
for the full timeline of what was collected and when.

## RSS Feed
Subscribe to: https://github.com/mhyrr/dyson-data/commits/main.atom
