# Effluent Radar

A personal job-tracking system for ETP / wastewater treatment / sustainability-compliance roles in Europe — built with [Claude](https://claude.ai).

**Live dashboard:** https://claude.ai/code/artifact/cbf49b3c-f95f-44df-ac00-38d86c7434b0

## What it is

A single-page dashboard (`index.html`) published as a Claude Artifact, backed by Claude's `db` runtime capability (a realtime document store scoped to the artifact — no separate backend to run or host).

It has three parts:

1. **Pipeline tracker** — every job you're watching, with a status (New → Interested → Applied → Interview → Offer / Rejected), a match-score gauge, tags, and a notes field. State is saved server-side, not in browser storage.
2. **Quick-search launchpad** — one-click, keyword-prefilled searches across LinkedIn, EURES, Indeed, TotalJobs, WaterJobsUK, Glassdoor, edie Jobs, GreenJobs, and the career pages of the major TIC/compliance firms (Bureau Veritas, SGS, Intertek, Control Union, QIMA, ELEVATE).
3. **Target-employer watchlist** — companies where the profile this was built for (ETP operations, ZDHC/Higg FEM compliance auditing, buyer-audit experience with H&M/Zara/Inditex/Next/C&A/HBI) is a strong fit.

## Automated scanning

A scheduled cloud routine (**Effluent Radar — Job Scan**, `trig_01HQnc7M8RMuY3hbfa1FZs5t`) runs independently on Anthropic's cloud infrastructure roughly every 3 days. Each run:

- reads the existing tracked jobs from the dashboard's database (to avoid duplicates),
- searches the sources above for current, open postings matching the target profile,
- verifies each listing is still live before including it,
- scores it for fit and writes only genuinely new matches back into the dashboard.

The routine's full prompt/instructions are not duplicated here — manage it at https://claude.ai/code/routines/trig_01HQnc7M8RMuY3hbfa1FZs5t.

## Notes / limitations

- No push notifications — new matches show up in the dashboard's sync banner and as "New"-status cards; check back periodically.
- The cloud routine has no memory of any conversation — it only knows what's in its stored prompt and what's already in the database.
- `index.html` here is the source of truth for the published artifact. To update the live dashboard after editing this file, republish it through Claude with the same artifact URL.
