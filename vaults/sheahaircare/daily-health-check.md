# Sheahaircare Daily Health — 2026-07-12

**Status:** WARNING
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 4 real errors (MongoNetworkTimeoutError, marketplace pages)
**Uptime:** 100% — prod READY, no build failures
**Top Issue:** MongoNetworkTimeoutError on `/` marketplace facets + stylist list — 4 events, 3 users affected (last hit 02:31 SAST)
**Recommendation:** Check MongoDB Atlas connection pool and cluster health. This error cluster (`SystemOverloadedError + RetryableError`) is recurring — first appeared 2026-07-10, hit again this morning.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Prod READY (PR #828). 9 PRs shipped. 1 CANCELED (superseded). No build errors. |
| MongoDB | WARNING | 4 MongoNetworkTimeoutError events on marketplace pages. Last hit 02:31 SAST today. |
| Sentry | OFFLINE | MCP authentication expired — error tracking blind. Re-auth needed. |
| PostHog | NOT CONNECTED | Appointment count unavailable. 5-min task to add token. |

---

## MongoDB Errors (24h) — 4 events

### MongoNetworkTimeoutError — marketplace-facets (3 events, 2 users)
- **Route:** `/` (homepage marketplace facets)
- **Error:** `Socket 'secureConnect' timed out after ~11-12s (connectTimeoutMS: 10000)`
- **Labels:** `SystemOverloadedError`, `RetryableError`
- **First:** 2026-07-10T17:50 UTC | **Last:** 2026-07-11T20:20 UTC
- **Impact:** Marketplace specialty/suburb filters fail to load on homepage

### MongoNetworkTimeoutError — marketplace-list-stylists (1 event, 1 user)
- **Route:** `/` (stylist listing)
- **Error:** `Socket 'secureConnect' timed out after 299s` (extreme)
- **Labels:** `SystemOverloadedError`, `RetryableError`
- **First/Last:** 2026-07-12T02:31 UTC (this morning, 4:31 SAST)
- **Impact:** Marketplace stylist list fails to render

### Mongoose deprecation warning (2 events — not a real error)
- `findOneAndUpdate()` using deprecated `new` option → use `returnDocument: 'after'`
- Routes: `/admin/customers`, `/api/consumer/signup`

### Node.js url.parse() DeprecationWarning (1 event — not a real error)
- Route: `/api/inngest`
- Low priority. Switch to WHATWG URL API when touching that module.

Error threshold (>5 real errors): **NOT triggered** — 4 events in 24h. But recurring.

---

## Vercel — Current Production

| Deployment | Status | PR | Change |
|---|---|---|---|
| dpl_F6bbfdRE5kWW16X7dYwRAo8J1p43 | **READY (PROD)** | #828 | docs(agents): record Tiplates provider-side session |
| dpl_3JZWrDv8UGZuGJNodVWC4kaPbEUn | READY (preview) | #828 | preview build |
| dpl_3JZWrDv8UGZuGJNodVWC4kaPbEUn | READY (rollback) | #827 | feat(landing): sparkle nav + Login role chooser |
| dpl_AfqbxqBFozqdmE6HJ4w1ktKro3Qb | **CANCELED** | #820 | superseded by #821 (race condition on merge) |

---

## Yesterday's Shipping Activity (PRs #820–#828)

9 PRs. **Full Tiplates provider feature shipped.**

| PR | Change | Status |
|---|---|---|
| #828 | docs(agents): record Tiplates provider-side session (PRs #820-#825) | ✅ PROD |
| #827 | feat(landing): sparkle For-specialists nav + Login role chooser | ✅ PROD |
| #826 | fix(paystack): env-drive pro/freemium plan codes + boot preflight | ✅ PROD |
| #825 | fix(tiplates): AI draft failed on full journeys (output-token truncation) | ✅ PROD |
| #824 | feat(tiplates): provider imagery — owner-scoped generate/upload/remove (PR 3/3) | ✅ PROD |
| #823 | feat(tiplates): AI safety review + submit→publish lifecycle (PR 2/3) | ✅ PROD |
| #822 | fix(tiplates): one Shea on journey pages (hide duplicate floating bubble) | ✅ PROD |
| #821 | perf(home): preload Spectral display font to cut landing LCP | ✅ PROD |
| **#820** | feat(tiplates): provider builder foundation — Pro-gated dashboard + AI-draft + full edit (PR 1/3) | ⚠️ CANCELED (superseded) |

---

## Open Action Items

- [ ] **Investigate MongoDB timeouts** — `SystemOverloadedError` on marketplace pages. Recurring since 2026-07-10. Check Atlas cluster CPU/connection pool. Consider raising `connectTimeoutMS` or enabling connection pooling keep-alive.
- [ ] **Re-authenticate Sentry MCP** — error tracking is blind without it. Go to claude.ai connector settings and reconnect Sentry.
- [ ] **Check SHEAHAIRCARE-Y** — hooks violation on `/consumer/signin` was open yesterday. Can't verify resolution without Sentry. Manually test signin flow.
- [ ] **Add PostHog token** — appointment tracking still unavailable. 5-min task.
- [ ] **Fix Mongoose deprecation** — `findOneAndUpdate()` new option → `returnDocument: 'after'`. Low priority but clean.
- [ ] **Fix url.parse() in /api/inngest** — switch to WHATWG URL API. Low priority.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-07 | HEALTHY | 0 Sentry errors. Active build week. |
| 2026-07-08 | WARNING | MongoNetworkTimeoutError + 12 auth errors. |
| 2026-07-09 | WARNING | Hydration error on appointments page. PR #728 in progress. |
| 2026-07-10 | HEALTHY | 0 unresolved issues. Hydration error resolved. 7 PRs shipped. |
| 2026-07-11 | WARNING | SHEAHAIRCARE-Y (hooks violation, signin). 1 build failure auto-recovered. 8 PRs shipped. |
| **2026-07-12** | **WARNING** | **MongoNetworkTimeoutError on marketplace (4 events, 3 users). Sentry offline. 9 PRs shipped — full Tiplates provider launch.** |

---

_Generated: 2026-07-12 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: OFFLINE — re-auth needed at claude.ai connector settings_
