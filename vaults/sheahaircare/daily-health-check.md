# Sheahaircare Daily Health — 2026-11-25

**Status:** HEALTHY
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 0
**Uptime:** ~100% (latest prod deploy READY, 0 runtime errors)
**Top Issue:** No deployments in ~60 days. Last deploy Sep 26 (PR #1296).
**Recommendation:** If no active sprint, verify app is still responding. Connect PostHog to get booking funnel visibility. Re-auth Sentry for error monitoring.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1296 `fix(scripts): drop emailVerified from purge safety gate` — READY. No new deployments in ~60 days (last: Sep 26, 2026). 9/11 recent deploys READY, 2 BLOCKED (old previews from May). |
| MongoDB | UNKNOWN | No Vercel runtime errors suggests no DB crashes, but Sentry offline — no direct signal. |
| Sentry | UNAVAILABLE | OAuth not configured in this session. Cannot pull 24h error count. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors

**0 errors** in last 24h (Vercel runtime logs).

No Vercel-side exceptions reported. Sentry offline — cannot confirm zero at the application layer.

---

## Recent Deployment Activity

Last production deployment was approximately 60 days ago (Sep 26, 2026). All recent prod deploys are READY. No build failures.

| Deploy | Branch | Status | Commit |
|---|---|---|---|
| dpl_FfX2JvVwZpdWYfDN5Cp4uVWRrEqd | main | READY (prod) | PR #1296 — fix(scripts): drop emailVerified from purge safety gate |
| dpl_89WzQFudqKYVjYRKmSh4YLGgzT91 | main | READY (prod) | PR #1295 — chore(scripts): purge tool for 2026-09-16 signup-spam accounts |
| dpl_5uEdRiJgaCUDmQ8UhVCDd9TUdVQR | main | READY (prod) | PR #1294 — fix(security): gate provider signup behind BotID, cap welcome-email flood |
| dpl_4xuRRkUpkDXchDaH2cMYJdz3XzW5 | main | BLOCKED | PR #215 — Revert motion experiments (old, May 2026) |

---

## Action Items

- [ ] **Verify app is live** — No deployments in 60 days. Quick sanity check: open the app and confirm booking flow works. Expected to be fine; worth confirming after a quiet period.
- [ ] **Re-auth Sentry** — Connect via claude.ai connector settings to restore error monitoring. Currently flying blind on application-layer errors.
- [ ] **Connect PostHog** — Appointment count unavailable. Booking funnel visibility is a persistent blind spot.
- [ ] **Review signup spam remediation** — PR #1295/#1296 addressed a 2026-09-16 signup-spam event. Confirm the purge ran and BotID gate (PR #1294) is holding.

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
| **2026-11-25** | **HEALTHY** | **0 Vercel runtime errors. Latest prod READY (PR #1296). No deploys in 60 days. Sentry offline.** |

---

_Generated: 2026-11-25 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: Requires re-auth — connect at claude.ai connector settings_
