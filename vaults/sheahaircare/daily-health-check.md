# Sheahaircare Daily Health — 2026-08-03

**Status:** WARNING
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 4 raw events / 12 open issues
**Uptime:** ~100% (all READY; 4 CANCELED = auto-superseded, not failures)
**Top Issue:** PAYSTACK_SECRET_KEY is a test key in production (sk_test_…) — payments not going live
**Recommendation:** Set PAYSTACK_SECRET_KEY to sk_live_… in Vercel environment variables immediately. Also set NEXT_PUBLIC_SITE_URL.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1136 `fix/dashboard-duplicate-nav-clearance` — READY. 5 PRs merged today. All production deploys READY. |
| MongoDB | HEALTHY | No connection errors in Sentry. auth.syncPlan DB divergence (SHEAHAIRCARE-1C) means DB is reachable — data inconsistency, not outage. |
| Sentry | WARNING | 4 raw errors / 12 unresolved issues in 24h. Two high-volume issues (170 events each) are env-preflight alerts. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors

**4 error events** / **12 unresolved issues** in last 24h.

| Issue | Events | Summary | Severity |
|---|---|---|---|
| SHEAHAIRCARE-16 | 170 | PAYSTACK_SECRET_KEY is test key — not `sk_live_` in production | CRITICAL |
| SHEAHAIRCARE-17 | 170 | NEXT_PUBLIC_SITE_URL not set — SEO canonicals falling back to hardcoded default | HIGH |
| SHEAHAIRCARE-1A | 15 | Rate-limit backend using Upstash env key mismatch | MEDIUM |
| SHEAHAIRCARE-1B | 12 | CSP: worker-src blocked blob (PDF/service worker) | MEDIUM |
| SHEAHAIRCARE-1C | 2 | auth.syncPlan: DB says paid / Paystack says empty — NOT auto-downgrading | MEDIUM |
| SHEAHAIRCARE-1D | 2 | CSP: connect-src blocked Google Maps API | LOW |
| SHEAHAIRCARE-15 | 2 | TimeoutError: view transition timed out on /contact | LOW |
| SHEAHAIRCARE-V | 1 | Hydration error on /?source=pwa | LOW |
| SHEAHAIRCARE-19 | 1 | Paystack webhook payload failed shape validation | LOW |
| SHEAHAIRCARE-18 | 1 | Paystack refund.failed — synthetic QA sweep (expected) | INFO |
| SHEAHAIRCARE-1E | 1 | CSP: img-src blocked Google Maps autocomplete icon | LOW |
| FL4LL-CONTROL-4 | 1 | failed to pipe response on /api/inngest | LOW |

---

## Today's Shipping Activity

5 PRs merged to main. Active build momentum.

| PR | Title | Status |
|---|---|---|
| #1136 | fix: drop dashboard page-level padding duplicated by app-nav-clearance | Prod READY |
| #1134 | docs(agents): record PR #1129 and two-mechanism stacking invariants | Prod READY |
| #1132 | docs: record navbar clearance invariants in AGENTS.md | Prod READY |
| #1131 | feat(services): price-list import — extraction pipeline (1/2) | Prod READY |
| #1127 | fix: drop per-page bottom padding duplicated by app-nav-clearance | Prod READY |

---

## Action Items

- [ ] **FIX NOW — PAYSTACK_SECRET_KEY** — Test key detected in production (SHEAHAIRCARE-16, 170 events, 21h). Go to Vercel → sheahaircare → Settings → Environment Variables → set `PAYSTACK_SECRET_KEY` to your `sk_live_…` key. Redeploy. Revenue operations are in test mode until this is fixed.
- [ ] **Set NEXT_PUBLIC_SITE_URL** — SEO canonicals falling back to hardcoded default (SHEAHAIRCARE-17, 170 events). Set the correct production URL in Vercel env vars.
- [ ] **Investigate SHEAHAIRCARE-1C** — auth.syncPlan sees a paid user in DB but Paystack shows empty. Could be a webhook miss or a sync timing issue. Could be related to Paystack test key (#1 above). Check after fixing the key.
- [ ] **CSP: add worker-src blob** — SHEAHAIRCARE-1B (12 events). Add `blob:` to worker-src in your CSP config to stop blocking the service worker.
- [ ] **Connect PostHog** — Appointment count still unavailable. Booking funnel visibility remains a blind spot.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-15 | HEALTHY | Subscription billing resolved. 4 PRs shipped. |
| 2026-07-16 | HEALTHY | 0 Sentry errors. 9 prod deploys. Security fix (#864) shipped. |
| 2026-07-17 | HEALTHY | 0 errors. 0 new deploys. App stable after billing sprint. |
| 2026-07-18 | HEALTHY | 0 errors. 9 prod deploys. Paystack billing sprint complete. |
| 2026-07-19 | WARNING | 1 Sentry error — /consumer render fail. SHEAHAIRCARE-5 recurring. |
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs merged. 2 preview PRs pending (#906 POPIA, #907 legal). |
| 2026-08-03 | **WARNING** | **Paystack test key in production (170 events). 4 raw errors / 12 issues. 5 PRs shipped.** |

---

_Generated: 2026-08-03 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/issues/?query=is%3Aunresolved+lastSeen%3A-24h)_
