# Sheahaircare Daily Health — 2026-08-08

**Status:** WARNING
**Appointments (24h):** N/A (PostHog not connected)
**Errors (24h):** 2
**Uptime:** 100% (all production deployments READY)
**Top Issue:** PAYSTACK_SECRET_KEY is not a live key — production payments may be failing
**Recommendation:** Set PAYSTACK_SECRET_KEY in Vercel env vars to a `sk_live_` key. Verify under sheahaircare > Settings > Environment Variables. Test a real payment after fixing.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod deploy READY. All recent production deploys green. |
| Sentry | WARNING | 1 open issue (SHEAHAIRCARE-16) — Paystack key not live in prod. 2 events today. |
| MongoDB | UNKNOWN | No direct check. App serving normally suggests connection is healthy. |
| PostHog | NOT CONNECTED | Appointment count unavailable. |

---

## Runtime Errors

**2 errors** in last 24h — 1 issue.

| Issue | Events | First seen | Last seen |
|---|---|---|---|
| SHEAHAIRCARE-16: `[env-preflight] PAYSTACK_SECRET_KEY is not a live key` | 2 | ~19h ago | ~12h ago |

[View in Sentry](https://fl4ll.sentry.io/issues/SHEAHAIRCARE-16)

**Impact:** Paystack in test mode means real card payments are not processing. Revenue is at risk while this is unresolved.

---

## Vercel Deployment Activity

Latest production deploy: `dpl_7D6qi3y69v8Ve3PxaSuyVNAGCJHZ` — **READY**

Recent production merges to main:
- PR #1191 `docs(agents): record enforcement-layer session` — READY
- PR #1190 `fix(dashboard): make theme controls say which surface they change` — READY
- PR #1188 `fix(assistant): stop serving a lapsed stylist a paid AI budget` — READY
- PR #1186 `fix(privacy): stop serving customer likeness from public URLs (POPIA s19)` — READY
- PR #1185 `fix(access): stop honouring paid features after subscription lapses` — READY
- PR #1184 `chore(eslint): add lint layer, incident rules only` — READY

All production deployments in READY state. 0 failed builds. Uptime: **100%**.

---

## Action Items

- [ ] **URGENT: Fix PAYSTACK_SECRET_KEY** — SHEAHAIRCARE-16 shows Paystack is running with a test key in production. Go to Vercel > sheahaircare > Settings > Environment Variables and replace the current key with your live `sk_live_` key. Test a payment after deploying.
- [ ] **Connect PostHog** — Appointment/booking count still a blind spot. Wire up the API key to get funnel visibility.
- [ ] **Add `/api/health` endpoint** — MongoDB status currently unverifiable from external monitoring. A lightweight ping endpoint would give definitive DB status.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-15 | HEALTHY | Subscription billing resolved. 4 PRs shipped. |
| 2026-07-16 | HEALTHY | 0 errors. 9 prod deploys. Security fix shipped. |
| 2026-07-17 | HEALTHY | 0 errors. App stable after billing sprint. |
| 2026-07-18 | HEALTHY | 0 errors. 9 prod deploys. Paystack billing sprint complete. |
| 2026-07-19 | WARNING | 1 error — /consumer render fail. SHEAHAIRCARE-5 recurring. |
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs merged (security + legal compliance sprint). |
| **2026-08-08** | **WARNING** | **SHEAHAIRCARE-16: Paystack not in live mode in production. 2 errors. 6 PRs shipped.** |

---

_Generated: 2026-08-08 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/issues/SHEAHAIRCARE-16)_
