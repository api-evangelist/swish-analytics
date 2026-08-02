---
name: Load pre-match match/team markets from Swish Analytics
description: Retrieve pre-match match and team betting markets for a sport and slate of games.
api: openapi/swish-analytics-sportsbook-openapi.yml
operations: [getMlbMatchesMarketsPrematch, getNflMatchesMarketsPrematch]
generated: '2026-07-21'
method: generated
---

# Load pre-match markets

Use this skill to pull pre-match match/team markets for a slate.

## Auth
Send your key in the `ApiKey` request header. Base URL `https://api.swishanalytics.com`.

## Steps
1. Call the sport's pre-match operation, e.g. `getMlbMatchesMarketsPrematch` (`GET /mlb/matches/markets/prematch`) or `getNflMatchesMarketsPrematch` (`GET /nfl/matches/markets/prematch`).
2. Filter by `date` and/or `game` (multi-value supported) to scope the slate.
3. Read priced markets from the `data` payload; map market/enumeration ids via vocabulary/swish-analytics-reference.yml.

## Rules
- GET-only and idempotent.
- Custom error envelope — check `error.status` before consuming `data`; 401 means the ApiKey header is missing/invalid.
