# Sheahaircare Daily Health — 2026-07-16

**Status:** HEALTHY
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 0 Sentry errors
**Uptime:** 100% — all 20 recent deployments READY
**Top Issue:** `url.parse()` deprecation still firing on `/api/inngest` (non-breaking, 40+ days open)
**Recommendation:** Fix url.parse() in Inngest handler — it's been open since June 6. Connect PostHog for appointment visibility.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | All 20 deployments READY. 9 prod deploys shipped yesterday. Latest: PR #871. |
| MongoDB | UNVERIFIED | No direct check available. 0 Sentry DB errors suggests healthy. |
| Sentry | HEALTHY | 0 unresolved errors in last 24h. Clean. |
| PostHog | NOT CONNECTED | Appointment count unavailable. |

---

## Runtime Errors

### LOW — url.parse() Deprecation Warning (still active, 40+ days)
- **Route:** `/api/inngest`
- **Count:** 1 | **Last seen:** 2026-07-15 06:45 UTC
- **First seen:** 2026-06-06
- **Note:** Non-breaking. Fix: replace `url.parse()` with `new URL()` in the Inngest route handler.

---

## Yesterday's Shipping Activity (PRs #863–#871)

9 PRs merged — billing/subscription + security sprint.

| PR | Change |
|---|---|
| #871 | feat(booking): payout readiness gating — block deposit for stylists with no payout setup |
| #870 | fix(paystack): unmapped plan code must not demote a paying subscriber |
| #869 | fix(paystack): never arm plan-change schedule against a live subscription |
| #868 | fix(paystack): claim new subscription code before disabling the old one |
| #867 | fix(paystack): handle not_renew + stop disable revoking a paid-up period |
| #866 | feat(billing): pending cancellation/downgrade banner on dashboard |
| #865 | fix(billing): re-land 5 subscription/billing commits orphaned by #861 |
| #864 | fix(storefront): stop leaking bank + billing fields in public page payload ⚠️ SECURITY |
| #863 | fix(scale): cap listTiplatesForAdmin at 500 |

**Notable:** PR #864 was a security fix — payout + billing fields (bankAccountNumber, bankCode, paystackSubaccountCode, etc.) were visible in the RSC payload of public storefront pages before this fix.

---

## Action Items

- [ ] **Fix `url.parse()` in `/api/inngest`** — switch to `new URL()` (WHATWG). Open 40+ days.
- [ ] **Connect PostHog** — appointment count still unavailable. 5-min task.
- [ ] **Verify MongoDB health** — no direct check. Watch Sentry for `MongoNetworkTimeoutError`.

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
| **2026-07-16** | **HEALTHY** | **0 Sentry errors. 9 prod deploys. Security fix (#864) shipped. url.parse() still open.** |

---

_Generated: 2026-07-16 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/issues/?project=sheahaircare&statsPeriod=24h)_
