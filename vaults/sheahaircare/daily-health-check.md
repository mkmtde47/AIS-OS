# Sheahaircare Daily Health — 2026-07-05

**Status:** WARNING
**Appointments (24h):** N/A (PostHog not connected)
**Errors (24h):** 2 (Vercel runtime — /find pages)
**Uptime:** 100% (all production deployments READY)
**Top Issue:** DYNAMIC_SERVER_USAGE on `/find/[city]/[service]` — hit `/find/pretoria/kids` at 14:28 UTC yesterday. Server Component using dynamic API during static render.
**Recommendation:** Audit `/find/[city]/[service]` route. Wrap any `headers()`, `cookies()`, or `searchParams` access in a dynamic boundary or move to a Client Component.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | WARNING | 100% deploy uptime. All production deployments READY. 2 runtime error groups on `/find/[city]/[service]` (DYNAMIC_SERVER_USAGE). Latest prod: PR #650 (Look Breakdown provider-agnostic). |
| Sentry | HEALTHY | 0 errors in last 24h. No open issues. Yesterday's /onboarding error (SHEAHAIRCARE-S) appears resolved. |
| PostHog | NOT CONNECTED | Token not configured. Appointment count unavailable. |
| MongoDB | UNVERIFIED | No direct ping tool. No Sentry/Vercel DB connection errors. Likely healthy. |

---

## Vercel Runtime Errors (Last 24h)

| Route | Error | Count | Last Seen |
|---|---|---|---|
| `/find/[city]/[service]` | `DYNAMIC_SERVER_USAGE` — Server Component dynamic API call during static render | 3 total (1 new: `/find/pretoria/kids`) | 2026-07-04 14:28 UTC |

**Root cause:** `DYNAMIC_SERVER_USAGE` digest means a Server Component called a dynamic API (`headers()`, `cookies()`, or accessed `searchParams`) in what Next.js expected to be a static segment. The `/find/pretoria/kids` path triggered this.

---

## Sentry — Error Trend

| Date | Errors (24h) | Open Issues | Status |
|---|---|---|---|
| 2026-06-17 to 2026-07-03 | 0 | 0 | HEALTHY — clean |
| 2026-07-04 | 2 | 1 (SHEAHAIRCARE-S) | WARNING — /onboarding server error |
| **2026-07-05** | **0** | **0** | **HEALTHY — Sentry clean. Vercel runtime errors on /find pages.** |

---

## Recent Deployments (Last 24h)

| PR | Description | Status |
|---|---|---|
| #650 | feat: Look Breakdown works for all providers + unblock publishing | READY (prod) |
| #649 | fix: allow TikTok Pixel domains in CSP (report-only) | READY (prod) |
| #648 | feat: TikTok Pixel + Events API (CAPI) with consent gating and dedup | READY (prod) |

---

## Open Action Items

- [ ] **Fix DYNAMIC_SERVER_USAGE on /find pages** — `/find/[city]/[service]` route crashes when `kids` is the service param. Likely a dynamic API (`headers()`, `searchParams`) called in a static segment. Add `export const dynamic = 'force-dynamic'` or wrap in Suspense. **High priority — real users hitting 500s on discovery pages.**
- [ ] **Add PostHog token** to `references/posthog-api.md` — unlocks appointment tracking (5 min)
- [ ] **Add `MONGODB_READONLY_URI`** to env — wires direct DB ping for future health checks

---

_Generated: 2026-07-05 08:00 SAST_
_Sentry: fl4ll org. [View dashboard](https://fl4ll.sentry.io/issues/)_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
