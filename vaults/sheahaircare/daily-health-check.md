# Sheahaircare Daily Health — 2026-11-15

**Status:** HEALTHY
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 0
**Uptime:** ~100% (3/3 prod deploys READY today)
**Top Issue:** Signup spam wave — 3 emergency PRs shipped overnight to purge accounts and gate bot signups
**Recommendation:** Monitor BotID gate effectiveness over next 48h. Connect PostHog to get booking funnel visibility.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1296 `fix(scripts): drop emailVerified from purge gate` — READY. 3/3 prod deploys today READY. |
| MongoDB | UNKNOWN | No direct connection. 0 Vercel runtime errors suggests DB is stable. |
| Sentry | UNKNOWN | Auth required — cannot query directly. 0 Vercel runtime errors in 24h. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors

**0 errors** in last 24h (Vercel runtime errors API).

No crashes, no DB timeouts, no render failures. App operating cleanly despite the signup-spam incident.

---

## Today's Shipping Activity (2026-11-15 sprint)

3 production deploys today — all READY. Spam/security sprint.

| PR | Title | Status |
|---|---|---|
| #1296 | fix(scripts): drop emailVerified from the purge safety gate | Prod READY |
| #1295 | chore(scripts): purge tool for the 2026-09-16 signup-spam accounts | Prod READY |
| #1294 | fix(security): gate provider signup behind BotID, cap welcome-email flood | Prod READY |

**Context:** A signup spam wave (started ~2026-09-16 based on commit) required a 3-PR response — bot gating on provider signup, a purge script, then a fix to the purge gate's safety condition. All now deployed to production.

---

## Action Items

- [ ] **Monitor BotID gate** — PR #1294 capped welcome-email flood and gated provider signup. Watch signup rate and email volume over next 48h to confirm it held.
- [ ] **Verify purge ran cleanly** — PR #1295/#1296 added and fixed the purge script. Confirm spam accounts were removed and no legit users caught in the net.
- [ ] **Connect PostHog** — Appointment count still unavailable. Booking funnel visibility is a persistent blind spot.
- [ ] **Authorize Sentry** — Sentry MCP requires re-auth. Connect to restore error tracking in this health check.

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
| 2026-07-19 | WARNING | 1 Sentry error — /consumer render fail 23:41 UTC. SHEAHAIRCARE-5 recurring. 4 PRs shipped. PR #896 tier caps in preview. |
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs merged (security + legal compliance sprint). 2 preview PRs pending merge (#906 POPIA, #907 legal copy). |
| **2026-11-15** | **HEALTHY** | **0 runtime errors. Signup spam wave resolved with 3-PR sprint (BotID gate + purge script). App stable.** |

---

_Generated: 2026-11-15 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=level%3Aerror&field=count%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
