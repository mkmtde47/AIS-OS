# Sheahaircare Daily Health — 2026-09-12

**Status:** HEALTHY
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 0
**Uptime:** 100% (20/20 READY)
**Top Issue:** www TLS redirect inverted — `www → 307 → apex` breaks POST webhooks (standing since 2026-08-25 outage)
**Recommendation:** Fix www redirect priority before any webhook-dependent launch activity. All other systems green.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1292 `chore/verify-kit-retrofit-v2` — READY. 20/20 recent deploys READY. No new deploys in last 24h (last push ~2026-09-08). |
| MongoDB | HEALTHY | 0 Sentry errors. No DB events seen. Atlas connection stable. |
| Sentry | HEALTHY | 0 error events in last 24h. 0 open unresolved issues. Clean. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors

**0 errors** in last 24h.

Sentry clean. No events, no unresolved issues. MongoDB appears stable — no SHEAHAIRCARE-5 recurrence.

---

## Recent Shipping Activity (since last check)

3 PRs merged since 2026-07-20. All production deploys READY.

| PR | Title | Status |
|---|---|---|
| #1292 | chore: retrofit verify-kit | Prod READY |
| #1291 | chore(ci): retire typecheck.yml, superseded by verify.yml | Prod READY |
| #1289 | test(conventions): ratchet four rules that were prose-only | Prod READY |
| #1288 | docs: handoff for security-remediation + www TLS outage session | Prod READY |
| #1287 | fix(security): authorize subscription-cleanup actions; write a real README | Prod READY |
| #1286 | perf(inngest): stop OFF-feature crons from burning free-tier executions | Prod READY |
| #1285 | fix(build): fail soft when generateStaticParams cannot reach the DB | Prod READY |
| #1284 | fix(auth): pin JWT session lifetime (7d rolling, was 30d default) | Prod READY |
| #1283 | fix(security): bump mongoose to 9.9.4 (GHSA-664h-wqgq-64gw) | Prod READY |

---

## Standing Issues

### www TLS Redirect (HIGH — pre-launch blocker)
From PR #1288 handoff (2026-08-25 outage):
- Vercel domain re-add inverted the redirect: `www → 307 → apex` instead of `apex → 308 → www`
- All env vars and third-party callbacks (Paystack, auth, webhooks) are built around `www`
- A 307 (temporary) redirect breaks POST webhooks — the method is not preserved
- **Action:** Fix in Vercel dashboard. Set `www.sheahaircare.co.za` as primary domain, redirect apex → www with 308 Permanent. Verify Paystack webhook endpoint resolves correctly after change.

---

## Action Items

- [ ] **Fix www → apex redirect** — invert back to apex → 308 → www. Paystack + auth callbacks depend on www. Do before any user acquisition or payment testing.
- [ ] **Connect PostHog** — Appointment count still unavailable. Booking funnel is a blind spot.
- [ ] **Watch SHEAHAIRCARE-5** — No recurrence seen. If clean through end of this week, close the issue.

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
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs merged (security + legal compliance sprint). 2 preview PRs pending merge (#906 POPIA, #907 legal copy). |
| **2026-09-12** | **HEALTHY** | **0 errors. 20/20 deploys READY. Security sprint complete (9 PRs). Standing: www redirect inverted from TLS outage.** |

---

_Generated: 2026-09-12 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=level%3Aerror&field=count%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
