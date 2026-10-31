# Sheahaircare Daily Health — 2026-10-31

**Status:** HEALTHY
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 0
**Uptime:** ~86% (12/14 non-canceled deploys READY; 2 BLOCKED are older/historical)
**Top Issue:** Signup spam attack cleanup in progress (BotID gate + purge script shipped)
**Recommendation:** Run the purge script live (PR #1296 is prod-ready). Confirm emailVerified fix is correct before deleting any accounts.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1296 `fix(scripts): drop emailVerified from purge safety gate` — READY. Production is live. |
| MongoDB | HEALTHY (inferred) | 0 runtime errors in 24h. No Sentry data available — needs re-auth. |
| Sentry | NOT CONNECTED | Requires re-authorization via claude.ai connector settings. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors

**0 errors** in last 24h.

No Vercel runtime errors. Production is clean.

---

## Recent Shipping Activity

Active security sprint against a signup spam attack (since 2026-09-16: ~165 fake provider accounts).

| PR | Title | Status |
|---|---|---|
| #1296 | fix(scripts): drop emailVerified from the purge safety gate | Prod READY |
| #1295 | chore(scripts): purge tool for the 2026-09-16 signup-spam accounts | Prod READY |
| #1294 | fix(security): gate provider signup behind BotID, cap welcome-email flood | Prod READY |
| #1293 | fix(proxy): forward x-pathname on the request so Entry lock can't loop | Prod READY (CANCELED by #1294 in the queue — normal) |

---

## Deployment Summary (last 15)

| State | Count | Notes |
|---|---|---|
| READY | 12 | Production is healthy |
| CANCELED | 1 | Normal — superseded by faster push |
| BLOCKED | 2 | Older deployments (Apr/May 2026) — historical, not current |

---

## Action Items

- [ ] **Run purge script live** — Dry run confirmed: 29 emailVerified rows protected (16s–27s gap). PR #1296 drops the emailVerified gate so actual spam accounts get deleted. Review CSV output before executing live delete.
- [ ] **Reconnect Sentry** — Needs re-authorization via claude.ai connector settings. MongoDB health is inferred, not confirmed.
- [ ] **Connect PostHog** — Appointment count is still a blind spot. Booking funnel visibility needed before any user acquisition push.
- [ ] **Monitor BotID gate (PR #1294)** — New provider signups now gated. Watch for false positives blocking legit stylists.

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
| **2026-10-31** | **HEALTHY** | **0 runtime errors. Signup spam attack cleanup active (#1294–1296). Production READY.** |

---

_Generated: 2026-10-31 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: Needs reconnection — see claude.ai connector settings_
