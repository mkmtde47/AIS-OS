# Sheahaircare Daily Health — 2026-05-21

**Status:** WARNING
**Appointments (24h):** N/A — PostHog not wired
**Errors (24h):** UNKNOWN — Sentry MCP approval required
**Uptime:** UNKNOWN — Vercel MCP approval required
**Top Issue:** SHEAHAIRCARE-R (`SecurityError: The operation is insecure.`) — carried from yesterday, unresolved
**Recommendation:** Approve Sentry + Vercel MCP tools in Claude Code settings to enable live data. Investigate SHEAHAIRCARE-R cross-origin issue before error count spikes.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | UNKNOWN | MCP call blocked — needs approval. Yesterday: custom domain ECONNREFUSED, .vercel.app 403 (auth-protected deployment live). |
| MongoDB Atlas | ASSUMED OK | No DB errors reported in Sentry trend data over past 3 days. Last confirmed incident: 2026-05-16. |
| PostHog | UNKNOWN | SDK-only — no MCP connection. Appointment count unavailable. |
| Sentry | UNKNOWN | MCP call blocked — needs approval. Yesterday: 4 events, 1 open issue (SHEAHAIRCARE-R). |

---

## Known Open Issues

| Issue ID | Error | First Seen | Status |
|---|---|---|---|
| SHEAHAIRCARE-R | `SecurityError: The operation is insecure.` | 2026-05-20 | Open — unresolved |

> Cross-origin access violation. Likely triggered by iframe, localStorage, or cookie access across domains. New yesterday, not yet spiking. Check browser console on production and staging.

---

## Trend (last 7 days)

| Date | Events | Issues | Top Problem |
|---|---|---|---|
| 2026-05-13 | 22 | 3 | NextAuth Invalid URL |
| 2026-05-15 | 97 | 12 | Broken build chunk + MongoDB down |
| 2026-05-16 | 48 | 16 | MongoDB DNS timeout + component ReferenceErrors |
| 2026-05-18 | 8 | 1 | MONGODB_URI env var not defined |
| 2026-05-19 | 4 | 0 | Stale Server Action hashes (post-deploy noise) |
| 2026-05-20 | 4 | 1 | SecurityError: The operation is insecure. |
| 2026-05-21 | — | — | Live pull blocked (MCP approval required) |

Error trend is strongly positive (97 → 4). One new unresolved issue type introduced yesterday.

---

## Monitoring Gaps

| Gap | Fix | Effort | Priority |
|---|---|---|---|
| Vercel + Sentry MCP blocked | Enable auto-approval for `mcp__Vercel__*` and `mcp__Sentry__*` in Claude Code settings | 2 min | P0 |
| Custom domain down | Confirm sheahaircare.co.za DNS → Vercel. Was ECONNREFUSED on 2026-05-20. | 10 min | P1 |
| PostHog appointments | Replace placeholder token; wire MCP or cron script | 15 min | P2 |
| MongoDB health ping | Add `scripts/mongo-ping.js` to verify connection each run | 20 min | P3 |

---

_Generated: 2026-05-21 08:00 SAST_
