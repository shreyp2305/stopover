# stopover

At the start of a new session, read `CHANGELOG.md` in this repo's root first
— it records what's actually been built and why, and is the fastest way to
get oriented without re-deriving context from scratch.

## What this project IS

`stopover` is a traveler-facing connection risk advisor: a frontend that
helps someone decide how worried to be about a layover. It's intentionally a
clean, single-purpose UI — not a dashboard, not a general flight-tracking
tool.

- **Input:** origin airport, connecting airport, layover duration.
- **Output:** a plain-English risk read, e.g. "45 min at ORD — moderate
  risk; ORD flights are running 12 min late on average right now, above
  this route's typical afternoon pattern."

## Dependency this service is built on

- **`tarmac`'s API** — the only backend this frontend talks to. `stopover`
  calls `tarmac`'s `GET /score/{origin}/{destination}` endpoint over HTTP
  and renders the result; it holds no scoring logic, no flight-data access,
  and no knowledge of how `tarmac` computes a score. All domain logic for
  "what does this score mean" lives server-side in `tarmac`'s response —
  `stopover`'s job is presentation, not computation.

## Tech stack

React + TypeScript.

## Suggested structure

```
src/
  api_client.ts     # thin wrapper around tarmac's API
  App.tsx
tests/
Dockerfile
```

## Working agreement

Explain a change and why it's shaped that way before writing code; wait for
confirmation before implementing — small, reviewed steps rather than large
generated diffs absorbed after the fact. Append new entries to
`CHANGELOG.md` at the top, short — what was built/decided and the one-line
reason, not a full diff.

**Keep this `CLAUDE.md` current.** It's a living document, not a one-time
setup artifact. Whenever a decision here changes, a new component gets
added, or an architecture choice shifts, update this file as part of the
work — not as a separate cleanup pass — so the next session starts from
accurate context instead of a stale snapshot.
