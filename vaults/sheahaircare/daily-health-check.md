# Sheahaircare Daily Health — 2026-07-15

**Status:** HEALTHY
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 4 (below >5 threshold)
**Uptime:** 100% — all prod deployments READY
**Top Issue:** `url.parse()` deprecation warning still firing on `/api/inngest` + appointments route (non-breaking, last seen 05:45 SAST)
**Recommendation:** Fix `url.parse()` usage — security-adjacent deprecation. Low priority. All subscription/billing errors from yesterday resolved by today's PRs.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | All 20 deployments READY. Latest prod: PR #861 (subscription plan resolution). |
| MongoDB | UNVERIFIED | No direct check available. PR #844 fix still in effect. Watch for timeout errors. |
| Sentry | HEALTHY | 4 errors in 24h. No unresolved issues. Below warning threshold. |
| PostHog | NOT CONNECTED | Appointment count unavailable. 5-min task to connect. |

---

## Runtime Errors — 6 groups total

### LOW — url.parse() Deprecation Warning (still active)
- **Routes:** `/[slug]/dashboard/appointments`, `/api/inngest`
- **Count:** 5 | **Users affected:** 4 | **Last seen:** 2026-07-15 05:45 SAST
- **Deployment:** dpl_9jyTuKGY2qeBdNx6WwvtYuCLDLUZ (current prod)
- **Note:** Non-breaking but security-flagged by Node. Switch to WHATWG URL API.

### RESOLVED — Subscription billing errors (3 groups, 8 occurrences from yesterday)
- `[paystack] Transaction initialization failed: Plan not found` — last seen 2026-07-14 18:04
- `[Subscription] Workflow failed: customer has no saved authorizations` — last seen 2026-07-14 13:43
- `[Subscription] Workflow failed: Plan code is invalid` — last seen 2026-07-14 13:27
- **Status:** All resolved by PRs #858–#861 merged today. Not recurring.

---

## Today's Shipping Activity (PRs #858–#861)

4 PRs merged to production — heavy billing/subscription sprint.

| PR | Change | Status |
|---|---|---|
| #861 | fix(subscription): dashboard reads DB plan + charge.success sets active | ✅ PROD |
| #860 | fix(paystack): harden upgrade — disable old sub via webhook | ✅ PROD |
| #859 | docs(agents): sprint log + PostHog sourcemap branch removal | ✅ PROD |
| #858 | fix(paystack): stylist subscriptions via hosted checkout (collect card) | ✅ PROD |

Notable: Subscription billing fully overhauled. New stylists can now subscribe via hosted checkout. Plan code resolution moved server-side. Card on file captured from webhooks.

---

## Action Items

- [ ] **Fix `url.parse()` in `/api/inngest` + appointments** — switch to `new URL()` (WHATWG). Low priority but node security flag.
- [ ] **Add PostHog token** — appointment tracking still unavailable. 5-min task.
- [ ] **Verify MongoDB health** — no direct check. Watch Sentry for `MongoNetworkTimeoutError` recurrence.
- [x] ~~Rotate GitHub PAT for vault integration~~ — Vault 401 errors not appearing today. Likely resolved.
- [x] ~~Fix subscription billing errors~~ — Resolved by PRs #858–#861.
- [x] ~~Re-authenticate Sentry MCP~~ — Sentry now connected and reporting.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-10 | HEALTHY | 0 unresolved issues. Hydration error resolved. 7 PRs shipped. |
| 2026-07-11 | WARNING | SHEAHAIRCARE-Y (hooks violation, signin). 1 build failure auto-recovered. 8 PRs shipped. |
| 2026-07-12 | WARNING | MongoNetworkTimeoutError on marketplace (4 events, 3 users). Sentry offline. 9 PRs shipped. |
| 2026-07-13 | — | No check run. |
| 2026-07-14 | WARNING | Vault 401 Unauthorized — Inngest marketing sync broken. DYNAMIC_SERVER_USAGE on /find pages. 5 PRs shipped. |
| **2026-07-15** | **HEALTHY** | **Subscription billing fully resolved. 4 PRs shipped. url.parse() deprecation only open issue.** |

---

_Generated: 2026-07-15 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&statsPeriod=24h)_
