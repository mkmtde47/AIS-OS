# Sheahaircare Daily Health — 2026-08-27

**Status:** HEALTHY
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 0
**Uptime:** 100% prod (10/10 production deploys READY; 1 preview ERROR, retried successfully)
**Top Issue:** Mongoose deprecation warning on `/api/consumer/signup` — `new` option deprecated since Mongoose 8; not a crash but needs a 1-line fix.
**Recommendation:** Replace `{new: true}` with `{returnDocument: 'after'}` in the `findOneAndUpdate` call on `/api/consumer/signup`. Then connect PostHog to restore booking funnel visibility.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1285 `fix/generate-static-params-db-guard` — READY. 10/10 prod deploys READY. 1 preview ERROR (PR #1279 first attempt — redeployed immediately and passed). |
| MongoDB | HEALTHY | 0 Sentry errors. SHEAHAIRCARE-5 (idle-pool race) has not fired. Appears resolved. |
| Sentry | HEALTHY | 0 error events in 24h. 0 open unresolved issues. Clean. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors

**0 hard errors** in last 24h.

**1 Mongoose deprecation warning** on `/api/consumer/signup`:
```
[MONGOOSE] Warning: the `new` option for `findOneAndUpdate()` is deprecated.
Use `returnDocument: 'after'` instead.
```
- Count: 1 | Last seen: 2026-08-26 16:43 UTC
- First seen: 2026-06-16 — has persisted for 2+ months without crashing
- Fix: swap `{new: true}` → `{returnDocument: 'after'}` in the consumer signup handler

---

## Yesterday's Shipping Activity (2026-08-26 security sprint)

10 PRs merged — the biggest security hardening day in the log. All production deploys READY.

| PR | Title | Status |
|---|---|---|
| #1285 | fix(build): fail soft when generateStaticParams cannot reach the DB | Prod READY |
| #1284 | fix(auth): pin JWT session lifetime (7-day rolling, was 30-day default) | Prod READY |
| #1283 | fix(security): bump mongoose to 9.9.4 (GHSA-664h-wqgq-64gw prototype pollution) | Prod READY |
| #1279 | fix(assistant): pin maxDuration on streaming chat routes | Prod READY |
| #1278 | chore(security): ignore unreachable js-yaml 3.14.2 from gray-matter | Prod READY |
| #1276 | fix(security): set authTagLength in decryptSecret for GCM compliance | Prod READY |
| #1275 | fix(security): clear 16 transitive dependency advisories via overrides | Prod READY |
| #1274 | docs(deploy): clear TEST webhook URL during live cutover (root cause SHEAHAIRCARE-1K) | Prod READY |
| #1273 | fix(paystack): report which mode sent a rejected webhook | Prod READY |
| #1272 | fix(paystack): name the cause of a rejected webhook signature | Prod READY |

---

## Action Items

- [ ] **Fix Mongoose deprecation** on `/api/consumer/signup` — swap `{new: true}` with `{returnDocument: 'after'}`. 1-line fix. Has been logged since 2026-06-16; now surfacing daily.
- [ ] **Connect PostHog** — Appointment count still unavailable. Booking funnel visibility is a blind spot.
- [ ] **Close SHEAHAIRCARE-5** — MongoDB idle-pool race has not fired in 38+ days. Safe to close if still open.

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
| **2026-08-27** | **HEALTHY** | **0 Sentry errors. 10 PRs merged yesterday (major security sprint). Mongoose deprecation warning on signup (non-crashing).** |

---

_Generated: 2026-08-27 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=level%3Aerror&field=count%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
