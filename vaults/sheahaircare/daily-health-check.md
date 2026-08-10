# Sheahaircare Daily Health — 2026-08-10

**Status:** WARNING
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 0 error events (1 open config issue)
**Uptime:** ~100% (18/20 READY, 2 CANCELED by superseding pushes)
**Top Issue:** SHEAHAIRCARE-16 — Paystack is NOT using a live key in production (3 events, first seen ~20h ago)
**Recommendation:** Check PAYSTACK_SECRET_KEY in Vercel env vars. Must start with `sk_live_` for real payments. Payments may be silently failing or in test mode.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1191 `docs/agents-md-enforcement-layer` — READY. 18/20 recent deploys READY. 2 CANCELED (normal). |
| Sentry | WARNING | 0 error events in 24h. But SHEAHAIRCARE-16 is active — env-preflight flagging non-live Paystack key in prod. |
| MongoDB | HEALTHY | 0 Sentry DB errors. SHEAHAIRCARE-5 has been silent since 2026-07-20 — closing as resolved. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Active Issue

### SHEAHAIRCARE-16 — Paystack key not live in production

> `[env-preflight] PAYSTACK_SECRET_KEY is not a live key (does not start with sk_live_) in production`

- **First seen:** ~20 hours ago (2026-08-09 ~12:00 SAST)
- **Last seen:** ~28 minutes ago
- **Events:** 3
- **Users affected:** 0
- **Severity:** HIGH — if the key is a test key, all payments in production route to Paystack's sandbox. No real money moves.

**Fix:** Go to Vercel → sheahaircare → Settings → Environment Variables → find `PAYSTACK_SECRET_KEY` for Production. Replace with the live key from [Paystack dashboard](https://dashboard.paystack.com/#/settings/developer) (starts with `sk_live_`).

---

## Runtime Errors

**0 error events** in last 24h.

No exceptions, no crashes. The only active issue is a configuration warning from the env-preflight check, not a runtime crash.

---

## Recent Shipping Activity (Enforcement Layer Sprint — ~2026-08-04/05)

11 PRs deployed since last health check (2026-07-20). All production deploys READY.

| PR | Title | Status |
|---|---|---|
| #1191 | docs(agents): record enforcement-layer session, prune sprint | Prod READY |
| #1190 | fix(dashboard): disambiguate the two theme controls | Prod READY |
| #1189 | chore(eslint): remove 62 dead disable directives | Prod READY (CANCELED superseded) |
| #1188 | fix(assistant): stop serving lapsed stylist a paid AI budget | Prod READY |
| #1187 | chore: make verification gate one command (`npm run verify`) | Prod READY (CANCELED superseded) |
| #1186 | fix(privacy): stop serving customer likeness from public URLs (POPIA s19) | Prod READY |
| #1185 | fix(access): stop honouring paid features after subscription lapses | Prod READY |
| #1184 | chore(eslint): add lint layer — 6 incident rules only | Prod READY |
| #1183 | fix(legal): correct five false statements in published docs | Prod READY |
| #1182 | feat(branding): wire "Find my look" quiz | Prod READY |
| #1181 | docs: correct constitution against what the code actually does | Prod READY |

---

## Action Items

- [ ] **Fix PAYSTACK_SECRET_KEY in Vercel prod env** — Current key is not `sk_live_*`. Payments may be in test mode. [SHEAHAIRCARE-16](https://fl4ll.sentry.io/issues/SHEAHAIRCARE-16). **Do this before any user acquisition.**
- [ ] **Connect PostHog** — Appointment count still unavailable. Booking funnel is a blind spot. 3 weeks overdue.
- [x] **SHEAHAIRCARE-5** — MongoDB idle-pool race on `/consumer`. Silent since 2026-07-20 (21 days). Closing as self-resolved.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-10 | HEALTHY | 0 unresolved issues. 7 PRs shipped. |
| 2026-07-11 | WARNING | Hooks violation on signin. 1 build failure. |
| 2026-07-12 | WARNING | MongoNetworkTimeoutError (4 events, 3 users). |
| 2026-07-13 | — | No check run. |
| 2026-07-14 | WARNING | Vault 401 Unauthorized — Inngest sync broken. |
| 2026-07-15 | HEALTHY | Billing resolved. 4 PRs shipped. |
| 2026-07-16 | HEALTHY | 0 errors. 9 prod deploys. |
| 2026-07-17 | HEALTHY | 0 errors. App stable after billing sprint. |
| 2026-07-18 | HEALTHY | 0 errors. 9 prod deploys. Paystack billing complete. |
| 2026-07-19 | WARNING | 1 Sentry error — /consumer render fail. SHEAHAIRCARE-5 recurring. |
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs (security + legal compliance sprint). |
| 2026-07-21–2026-08-03 | — | No checks run (gap). |
| **2026-08-10** | **WARNING** | **0 runtime errors. SHEAHAIRCARE-16: Paystack non-live key in prod. 11 PRs shipped (enforcement sprint).** |

---

_Generated: 2026-08-10 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=level%3Aerror&field=count%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
_Sentry SHEAHAIRCARE-16: [View issue](https://fl4ll.sentry.io/issues/SHEAHAIRCARE-16)_
