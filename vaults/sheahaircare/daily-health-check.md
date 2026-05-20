# Sheahaircare Daily Health — 2026-05-20

**Status:** WARNING
**Appointments (24h):** N/A — PostHog not wired
**Errors (24h):** 4 events, 1 open issue (SHEAHAIRCARE-R)
**Uptime:** UNKNOWN — custom domain ECONNREFUSED; .vercel.app returns 403 (deployment exists, auth-protected)
**Top Issue:** `SecurityError: The operation is insecure.` — 4 events, new today
**Recommendation:** Investigate SHEAHAIRCARE-R. Likely a cross-origin or iframe security policy issue. Check browser console on staging.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | UNKNOWN | Personal account — no team ID. Custom domain (sheahaircare.co.za) ECONNREFUSED. .vercel.app responds 403 (deployment live, auth-protected). |
| MongoDB Atlas | ASSUMED OK | No DB errors in Sentry today. Same as yesterday. |
| PostHog | UNKNOWN | SDK-only — no MCP. Appointment count unavailable. |
| Sentry | WARNING | 4 error events. 1 open issue (new). Below 5-error threshold but new issue type. |

---

## Sentry Events (last 24h)

| Issue | Error | Events | Status |
|---|---|---|---|
| SHEAHAIRCARE-R | SecurityError: The operation is insecure. | 4 | New — open |

**Total events:** 4 (threshold: >5 to flag)

> `SecurityError: The operation is insecure.` typically fires from cross-origin access attempts — an iframe, localStorage, or cookie being read across domains. New today. Worth a look before it spikes.

---

## Trend

| Date | Events | Issues | Top Problem |
|---|---|---|---|
| 2026-05-13 | 22 | 3 | NextAuth Invalid URL |
| 2026-05-15 | 97 | 12 | Broken build chunk + MongoDB down |
| 2026-05-16 | 48 | 16 | MongoDB DNS timeout + component ReferenceErrors |
| 2026-05-18 | 8 | 1 | MONGODB_URI env var not defined |
| 2026-05-19 | 4 | 0 | Stale Server Action hashes (post-deploy noise) |
| 2026-05-20 | 4 | 1 | SecurityError: The operation is insecure. |

Event count flat vs yesterday. New issue type appeared. Not spiking yet.

---

## Monitoring Gaps

| Gap | Fix | Effort | Priority |
|---|---|---|---|
| Vercel uptime | Wire Sheahaircare .vercel.app URL to `mcp__Vercel__get_deployment` with correct project ID | 5 min | P1 |
| Custom domain | Confirm sheahaircare.co.za DNS points to Vercel — currently ECONNREFUSED | 10 min | P1 |
| PostHog appointments | Replace placeholder token; wire MCP or cron script | 15 min | P2 |
| MongoDB health ping | Add `scripts/mongo-ping.js` to verify connection each run | 20 min | P3 |

---

_Generated: 2026-05-20 08:00 SAST_
