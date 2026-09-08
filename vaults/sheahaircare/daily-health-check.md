# Sheahaircare Daily Health — 2026-09-08

**Status:** HEALTHY
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 0
**Uptime:** 100% prod (19/20 overall — 1 ERROR was a preview deploy, immediately redeployed successfully)
**Top Issue:** PR #1287 (subscription-cleanup auth guard) in preview — security fix, not yet merged
**Recommendation:** Merge PR #1287 today. Security action (`fixSubscriptions`) was callable unauthenticated — fix is ready and in preview.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1286 `perf(inngest-cron-usage)` — READY, deployed 07:14 SAST. 9/9 prod deploys READY. |
| MongoDB | HEALTHY | 0 Sentry errors. No DB connectivity issues reported. |
| Sentry | HEALTHY | 0 unresolved error events in 24h. Clean. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors

**0 errors** in last 24h.

Sentry returned zero unresolved issues. Cleanest run in weeks.

---

## Today's Deploy Activity (2026-09-08)

| Deploy | Branch | Target | Status |
|---|---|---|---|
| dpl_D9ZS2p8… | fix/subscription-cleanup-guard-and-readme (PR #1287) | Preview | READY |
| dpl_75KoD6F… | main (PR #1286 merge) | **Production** | READY |

**Latest prod commit:** `perf(inngest): stop OFF-feature crons from burning free-tier executions` — saves ~5,760+ Inngest free-tier executions/month by gating off-feature crons behind their feature flags.

**Preview READY:** PR #1287 — `fix(security): authorize subscription-cleanup actions` — `auditSubscriptions()` and `fixSubscriptions()` were exported from a `"use server"` file with no auth check. `fixSubscriptions()` can disable live Paystack subscriptions and mass-mutate stylist plan fields. Fix adds `requireAdminSection("revenue")` guard. **Merge before any subscription-related ops.**

---

## Action Items

- [ ] **Merge PR #1287** — Security: subscription-cleanup server actions were unauthenticated. Preview READY. Merge now.
- [ ] **Connect PostHog** — Appointment count still unavailable. Booking funnel is a blind spot. Wire up this week.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-10 | HEALTHY | 0 unresolved issues. Hydration error resolved. 7 PRs shipped. |
| 2026-07-11 | WARNING | SHEAHAIRCARE-Y (hooks violation, signin). 1 build failure. 8 PRs shipped. |
| 2026-07-12 | WARNING | MongoNetworkTimeoutError on marketplace (4 events, 3 users). Sentry offline. 9 PRs shipped. |
| 2026-07-13 | — | No check run. |
| 2026-07-14 | WARNING | Vault 401 Unauthorized — Inngest marketing sync broken. DYNAMIC_SERVER_USAGE on /find pages. |
| 2026-07-15 | HEALTHY | Subscription billing fully resolved. 4 PRs shipped. url.parse() only open issue. |
| 2026-07-16 | HEALTHY | 0 Sentry errors. 9 prod deploys. Security fix (#864) shipped. url.parse() still open. |
| 2026-07-17 | HEALTHY | 0 errors. 0 new deploys. url.parse() not seen. App stable after billing sprint. |
| 2026-07-18 | HEALTHY | 0 errors. 9 prod deploys. Paystack billing sprint complete. url.parse() resolved. |
| 2026-07-19 | WARNING | 1 Sentry error — /consumer render fail 23:41 UTC. SHEAHAIRCARE-5 recurring. 4 PRs shipped. |
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs merged (security + legal compliance sprint). 2 preview PRs pending merge. |
| **2026-09-08** | **HEALTHY** | **0 errors. 1 prod deploy (Inngest cron perf). PR #1287 security fix in preview — merge today.** |

---

_Generated: 2026-09-08 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=level%3Aerror&field=count%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
