---
name: Poll live player props from Swish Analytics
description: Fetch and incrementally refresh in-play player proposition prices for a sport using the players/props/inplay endpoints and modifiedAtGreater delta sync.
api: openapi/swish-analytics-sportsbook-openapi.yml
operations: [getNflPlayersPropsInplay, getNbaPlayersPropsInplay, getMlbPlayersPropsInplay]
generated: '2026-07-21'
method: generated
---

# Poll live player props

Use this skill to pull and keep in-play player-prop prices fresh for a sport.

## Auth
Send your key in the `ApiKey` request header. Base URL `https://api.swishanalytics.com`.

## Steps
1. Choose the sport operation: `getNflPlayersPropsInplay` (`GET /nfl/players/props/inplay`), `getNbaPlayersPropsInplay` (`GET /nba/players/props/inplay`), or `getMlbPlayersPropsInplay` (`GET /mlb/players/props/inplay`).
2. Scope the request with `date` and/or `game` (both accept multiple values).
3. Track the maximum `modifiedAt` (UTC microseconds) in the returned payload.
4. On each subsequent poll, pass that value as `modifiedAtGreater` to receive only markets updated since the last payload — the efficient live-refresh pattern.

## Rules
- GET-only and idempotent; safe to poll on an interval.
- Resolve enum ids (sportId, marketOpenId, gameStatusId, ...) against vocabulary/swish-analytics-reference.yml.
- Validate `error.status` in the response envelope before using `data`.
