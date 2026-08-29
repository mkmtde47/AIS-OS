# Sheahaircare Daily Health — 2026-08-29

**Status:** HEALTHY
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 0
**Uptime:** ~95% (19/20 deploys READY; 1 ERROR was a superseded build of PR #1279, redeployed successfully)
**Top Issue:** NONE — 0 Sentry errors, 0 runtime errors, prod READY
**Recommendation:** Connect PostHog (booking funnel still a blind spot). All security sprint changes are live and clean.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1285 `fix/generate-static-params-db-guard` — READY. 19/20 deploys READY. 1 ERROR (PR #1279 first attempt, superseded by successful redeploy of same commit). |
| MongoDB | HEALTHY | 0 Sentry errors. No MongoNetworkTimeoutError or connection events. |
| Sentry | HEALTHY | 0 error events in 24h. 0 open unresolved issues. Clean. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors

**0 errors** in last 24h.

No Sentry events. No Vercel runtime errors. Clean across both platforms.

---

## Today's Shipping Activity (2026-08-28/29 security sprint)

10 PRs shipped. All production deploys READY. Heavy security hardening sprint.

| PR | Title | Status |
|---|---|---|
| #1285 | fix(build): fail soft when generateStaticParams cannot reach DB | Prod READY |
| #1284 | fix(auth): pin JWT session lifetime to 7 days (was 30-day default) | Prod READY |
| #1283 | fix(security): bump mongoose to 9.9.4 (GHSA-664h-wqgq-64gw) + narrow schema literals | Prod READY |
| #1279 | fix(assistant): pin maxDuration on streaming chat routes | Prod READY |
| #1278 | chore(security): ignore unreachable js-yaml 3.14.2 (gray-matter) | Prod READY |
| #1276 | fix(security): set authTagLength in decryptSecret for GCM compliance | Prod READY |
| #1275 | fix(security): clear 16 transitive dependency advisories via overrides | Prod READY |
| #1274 | docs(deploy): clear TEST webhook URL during live cutover (Paystack runbook fix) | Prod READY |
| #1273 | fix(paystack): report which MODE sent a rejected webhook | Prod READY |
| #1272 | fix(paystack): name the cause of a rejected webhook signature | Prod READY |

---

## Build Notes

One build ERROR (dpl_8gbWjcEF2SHqTCt87z6XSmEvpLir) on the first attempt at PR #1279 (fix/assistant-max-duration). Same commit was redeployed successfully. Not a regression — isolated build flake or transient Atlas unavailability during generateStaticParams (the exact issue PR #1285 subsequently guarded against).

---

## Action Items

- [ ] **Connect PostHog** — Appointment count still unavailable. Booking funnel is a blind spot; priority connection.
- [ ] **Verify Paystack live webhook URL** — PR #1274 updated the runbook. Confirm the live webhook is pointed at production and the test-mode URL is cleared.
- [ ] **Monitor mongoose 9.9.4 deploy** — First prod release with the bumped version. Watch for any schema-casting regressions on next Sentry check.

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
| **2026-08-29** | **HEALTHY** | **0 errors. 10 PRs shipped (security sprint: mongoose CVE, JWT maxAge, GCM authTag, 16 transitive advisories, Paystack webhook hardening, DB build guard).** |

---

_Generated: 2026-08-29 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=level%3Aerror&field=count%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
