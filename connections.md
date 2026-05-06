# Connections

Registry of every system your AIOS can reach. Filled by `/onboard` from Q4-Q7 answers; expanded over time as you wire new tools. `/audit` checks this file for domain coverage and freshness.

| # | Domain | Tool | Mechanism | Auth | Last checked |
|---|---|---|---|---|---|
| 1 | Revenue / Financials | Paystack | dashboard + script | api key | 2026-05-06 |
| 2 | Customer interactions | Gmail | not yet connected | — | — |
| 3 | Calendar | Google Calendar | not yet connected | — | — |
| 4 | Communication | WhatsApp + Phone | not yet connected | — | — |
| 5 | Project / task tracking | GitHub Issues | mcp / gh cli | oauth | 2026-05-06 |
| 6 | Error tracking | Sentry | sdk | dsn | 2026-05-06 |
| 7 | Product analytics | Posthog | sdk | token | 2026-05-06 |
| 8 | Task / knowledge hub | Notion | api | token | 2026-05-06 |
| 9 | Tool automation | Make.com | scenarios | oauth | deferred |
| 10 | Knowledge / files | Google Drive + Desktop | not yet connected | — | — |
| 11 | Sheahaircare ops | Obsidian Vault | agent + docs | read-only | 2026-05-06 |
| 12 | Sheahaircare health | MongoDB + Paystack | api | credentials | setup pending |

**Mechanism options:** `mcp` (MCP server), `script` (Python/Bash hitting an API, in `scripts/`), `export` (CSV/JSON dump pipeline), `key+ref` (`.env` key + `references/{tool}-api.md` guide), `not yet connected`.

When you wire a new tool, also save `references/{tool}-api.md` capturing endpoints, auth flow, and common queries — researched-once-saved-forever.
