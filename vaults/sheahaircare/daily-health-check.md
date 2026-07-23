# Sheahaircare Daily Health — 2026-07-23

**Status:** HEALTHY
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 0 (Sentry clean)
**Uptime:** ~100% (18/20 READY, 2 CANCELED by superseding pushes)
**Top Issue:** Mongoose `findOneAndUpdate` deprecation + `url.parse()` security warning (both fired today/yesterday — low severity but needs a cleanup pass)
**Recommendation:** Schedule a 1-hour deprecation cleanup sprint: replace `findOneAndUpdate({new:true})` with `returnDocument:'after'` across the app, and replace `url.parse()` with `new URL()` in `/api/inngest` and `/api/webhook/paystack`.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #997 `fix/tiplate-reminders-optin-and-silent-failure` — READY. 18/20 recent deploys READY. 2 CANCELED (normal — superseded). |
| MongoDB | HEALTHY | DB connected (Mongoose active). 0 Sentry DB errors. Deprecation warning logged (non-breaking today). |
| Sentry | HEALTHY | 0 error events in 24h. 0 new unresolved issues. Clean. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors (Vercel — cumulative groups, last 24h activity)

**4 error groups tracked, 0 new Sentry-captured errors:**

| Error | Count (all-time) | Last Seen | Route | Severity |
|---|---|---|---|---|
| CredentialsSignin (bad login) | 4 events / 3 users | 2026-07-22 18:10 UTC | `/api/auth/[...nextauth]` | LOW — user error, not app bug |
| Auth handler crash (same event) | 4 events / 3 users | 2026-07-22 18:10 UTC | `/api/auth/[...nextauth]` | LOW — same root as above |
| Mongoose `new` option deprecated | 3 events / 3 users | 2026-07-22 16:06 UTC | `/api/consumer/signup` | MEDIUM — will break on Mongoose v8 |
| `url.parse()` security deprecation | 3 events / 3 users | **2026-07-23 05:45 UTC** | `/api/inngest`, `/api/webhook/paystack` | MEDIUM — security-flagged by Node |

Auth errors (rows 1+2) are the same single failed login attempt; user-side issue, not an app bug. The deprecation warnings (rows 3+4) are the actionable items — both have been accumulating since May/June and fired again today.

---

## Today's Shipping Activity

10 PRs merged to main overnight. Heavy Tiplates rename + a11y sprint complete.

| PR | Title | Status |
|---|---|---|
| #999 | fix(ci): grant orphan sweep pull-requests:read | Preview READY |
| #997 | fix(tiplates): report reminder push failures, offer reminders at join | **Prod READY** |
| #996 | fix(tiplates): strip Mongo _id from encouragement across RSC boundary | Prod READY |
| #995 | fix(ci): add scheduled orphan sweep | Prod READY |
| #994 | docs(agents): record passkey enrolment dead-end session | Prod READY |
| #993 | docs(debug): land two 2026-06-21 write-ups | Prod READY |
| #992 | docs(agents): record Tiplates naming completion | Prod READY |
| #991 | fix(tiplates): sweep remaining admin/provider Tiplates copy | Prod READY |
| #990 | fix(a11y): give PWA prompts real modal semantics | Prod READY |
| #989 | docs(agents): record placeLabel POPIA wiring | Prod READY |

---

## Action Items

- [ ] **Deprecation sprint** — Replace `findOneAndUpdate({new:true})` → `returnDocument:'after'` (hits `/api/consumer/signup` and likely more). Replace `url.parse()` → `new URL()` in `/api/inngest` + `/api/webhook/paystack`. One PR, low risk.
- [ ] **Connect PostHog** — Appointment count still a blind spot. No visibility into booking funnel performance.
- [ ] **Monitor PR #999** — Orphan sweep's CI read permission fix; watch next scheduled cron run to confirm it now detects stale branches correctly.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-15 | HEALTHY | 0 Sentry errors. url.parse() only open issue. |
| 2026-07-16 | HEALTHY | 0 errors. 9 prod deploys. Security fix (#864) shipped. |
| 2026-07-17 | HEALTHY | 0 errors. 0 new deploys. App stable. |
| 2026-07-18 | HEALTHY | 0 errors. 9 prod deploys. Paystack billing sprint complete. |
| 2026-07-19 | WARNING | 1 Sentry error — /consumer render fail. SHEAHAIRCARE-5 recurring. |
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs merged (security + legal compliance sprint). |
| 2026-07-21 | — | No check run. |
| 2026-07-22 | — | No check run. |
| **2026-07-23** | **HEALTHY** | **0 Sentry errors. 10 PRs merged (Tiplates + a11y sprint). Deprecation warnings need cleanup sprint.** |

---

_Generated: 2026-07-23 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=is%3Aunresolved&field=count%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
