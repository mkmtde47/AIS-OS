# Sheahaircare Daily Health — 2026-09-13

**Status:** WARNING
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 0
**Uptime:** 100% (20/20 READY)
**Top Issue:** www→apex 307 redirect inversion — POST webhooks (Paystack callbacks) may be silently failing
**Recommendation:** Fix www redirect (restore apex→308→www). Check Paystack webhook delivery logs before any user acquisition push.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | 20/20 recent deploys READY. Last prod deploy ~4.5 days ago (PR #1291, 2026-09-08). |
| MongoDB | HEALTHY | 0 Sentry DB errors. No MongoNetworkErrors. |
| Sentry | HEALTHY | 0 error events in 24h. 0 open unresolved issues. Clean. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors

**0 errors** in last 24h.

Sentry is clean. No unresolved issues, no new events. 2nd consecutive clean period after the July 20 baseline.

---

## Recent Shipping Activity

No production deploys in the last 24h. Last 2 prod deploys:

| PR | Title | Merged |
|---|---|---|
| #1292 | chore: retrofit verify-kit | ~2026-09-08 |
| #1291 | chore(ci): retire typecheck.yml, superseded by verify.yml | ~2026-09-08 |

**Security sprint (Aug 25–Sep 08) highlights:**
- #1283 — mongoose bumped to 9.9.4 (GHSA-664h-wqgq-64gw prototype pollution)
- #1284 — JWT session maxage pinned to 7 days rolling
- #1287 — subscription-cleanup server actions now gated (were fully public endpoints)
- #1285 — generateStaticParams DB guard (prevents deploy failure on Atlas transient errors)
- #1286 — Inngest OFF-feature crons slowed (saves ~7,200 executions/month)
- #1289 — 4 convention ratchets promoted from prose to enforced tests (server-action-authorization, action-response-shape, keyset-pagination, entitlement-predicates)
- #1292 — verify-kit retrofit (3,684 tests / 398 files; harness now asserts file count)

---

## Open Issues

- **www→307→apex redirect inversion (CRITICAL path risk):** Per the 2026-08-25 TLS outage session handoff (#1288), the domain re-add inverted the redirect from `apex→308→www` (original) to `www→307→apex` (current). Every env var and third-party callback is built around `www`. A 307 redirect breaks POST webhooks — Paystack payment callbacks may be failing silently. Not yet fixed as of last handoff.
- **DAST gate STATIC-ONLY:** The security gate on record passed static analysis only — every dynamic probe failed during the outage window. With `hard_launch_gate: enforce`, this could pass a hard launch on incomplete data. Do a full dynamic DAST pass before any public launch.
- **Connect PostHog** — Appointment count and booking funnel visibility are still blind spots.

---

## Action Items

- [ ] **Fix www redirect** — Restore `apex→308→www`. Verify Paystack webhook delivery logs for missed callbacks since ~2026-08-26.
- [ ] **Re-run dynamic DAST** — Static gate passed; dynamic phases all failed during outage. Get a clean dynamic pass before hard launch.
- [ ] **Connect PostHog** — Without it, appointment counts and funnel metrics are invisible in this check.

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
| 2026-07-21 – 2026-09-12 | — | No daily check runs. |
| **2026-09-13** | **WARNING** | **0 errors. App stable. www→307→apex redirect inversion open — breaks POST webhooks. DAST gate incomplete.** |

---

_Generated: 2026-09-13 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=level%3Aerror&field=count%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
