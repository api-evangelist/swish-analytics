---
name: Price a bet or parlay with Swish Analytics
description: Request Swish Analytics pricing for a single market or a multi-leg parlay (accumulator) via the bet-request endpoint.
api: openapi/swish-analytics-sportsbook-openapi.yml
operations: [getBetRequest, getBetRequestResults]
generated: '2026-07-21'
method: generated
---

# Price a bet or parlay

Use this skill to get Swish Analytics pricing for a single market or a parlay.

## Auth
Send your key in the `ApiKey` request header on every call. Base URL `https://api.swishanalytics.com`.

## Steps
1. Call `getBetRequest` (`GET /bet-request`). Set `parlay=true` for a multi-leg accumulator or `parlay=false` for a single market, and pass the market/selection identifiers documented in the endpoint's parameters.
2. Read the priced odds/probabilities from the JSON `data` payload.
3. To reconcile settled outcomes later, call `getBetRequestResults` (`GET /bet-request/results`) for the same request.

## Rules
- All calls are HTTP GET and read-only (idempotent) — safe to retry.
- Errors come back in the custom envelope `{status, endpoint, error:{message}, data}` — check `error.status` before trusting `data`. See errors/swish-analytics-problem-types.yml.
- A missing/invalid `ApiKey` returns 401.
