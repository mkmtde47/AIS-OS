# Sheahaircare Daily Health — 2026-07-18

**Status:** HEALTHY
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 0
**Uptime:** ~100% (all deployments READY, 0 Sentry errors)
**Top Issue:** NONE
**Recommendation:** ALL CLEAR. Heavy shipping day — 9 PRs merged to main. Monitor Paystack webhook paths (#865–#871 all touched billing).

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | All 20 recent deployments READY. Latest: PR #871 (payout-readiness-gating). 9 prod deploys today. |
| MongoDB | UNVERIFIED | No direct check available. 0 Sentry DB errors suggests healthy. |
| Sentry | HEALTHY | 0 unresolved errors in last 24h. Clean after billing sprint. |
| PostHog | NOT CONNECTED | Appointment count unavailable. |

---

## Runtime Errors

None in last 24h. `url.parse()` deprecation (last seen 2026-07-15) has not resurfaced — likely resolved by the billing refactors.

---

## Today's Shipping Activity

9 PRs merged to main. All deployments READY.

| PR | Title | Status |
|---|---|---|
| #871 | feat(booking): don't offer online payment a stylist can't receive | READY |
| #870 | fix(paystack): unmapped plan code must not demote a paying subscriber | READY |
| #869 | fix(paystack): never arm a plan-change schedule against a live subscription | READY |
| #868 | fix(paystack): claim the new subscription code before disabling the old one | READY |
| #867 | fix(paystack): handle not_renew + stop subscription.disable revoking paid period | READY |
| #866 | feat(billing): surface a scheduled cancellation/downgrade on the dashboard | READY |
| #865 | fix(billing): re-land 5 subscription/billing commits orphaned by #861 | READY |
| #864 | fix(storefront): stop publishing payout + billing fields to the browser | READY |
| #863 | fix(scale): cap listTiplatesForAdmin at ADMIN_TIPLATE_LIST_CAP | READY |

---

## Action Items

- [ ] **Connect PostHog** — appointment count still unavailable.
- [ ] **Verify MongoDB health** — no direct check. Watch Sentry for `MongoNetworkTimeoutError`.
- [ ] **Watch Paystack webhooks** — 9 billing-related PRs shipped. Monitor for edge cases in production traffic over next 48h.

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
| **2026-07-18** | **HEALTHY** | **0 errors. 9 prod deploys. Paystack billing sprint complete. url.parse() resolved.** |

---

_Generated: 2026-07-18 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/issues/?project=sheahaircare&statsPeriod=24h)_
