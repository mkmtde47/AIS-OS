# Sheahaircare Daily Health — 2026-09-26

**Status:** WARNING
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 1 active error group (CredentialsSignin — last event 06:00 UTC today)
**Uptime:** ~100% (latest prod deployment READY; no new prod deploys in ~17 days — app stable)
**Top Issue:** CredentialsSignin errors on `/api/auth/[...nextauth]` — 17 users affected since June, last fired 06:00 UTC today
**Recommendation:** Confirm whether auth failures are normal wrong-password traffic or a broken sign-in flow. If users are reporting login issues, audit the credentials provider config.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1291 `chore/retire-typecheck-workflow` — READY. All recent deploys READY. App stable, no new prod push in ~17 days. |
| Runtime Errors | WARNING | CredentialsSignin fired at 06:00 UTC today. 17 unique users across lifetime. Stack trace points to NextAuth `/api/auth/[...nextauth]`. |
| MongoDB | UNKNOWN | Sentry not accessible (needs OAuth). No DB errors visible from Vercel runtime logs. |
| Sentry | NOT ACCESSIBLE | Requires OAuth re-auth in an interactive session. Go to claude.ai connector settings. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors (Vercel)

**Error group 1:** `[auth][error] CredentialsSignin`
- Route: `/api/auth/[...nextauth]`
- Count: 17 | Users: 17 (1 error per unique user)
- First seen: 2026-06-19 | Last seen: **2026-09-26 06:00 UTC (today)**
- Deployment: `dpl_2HD2D6WwNL87TdeFbsWeNidQHXFX` (PR #1291)

**Error group 2:** Stack trace — same auth route, same count
- First seen: 2026-09-04 | Last seen: 2026-09-26 06:00 UTC
- Same 17 users; this is the stack trace variant of the same error

**Assessment:** 17 errors over 3+ months is low volume, but the recurrence today and the consistent 1:1 user:error ratio suggests real users failing to sign in — not bots. Could be: wrong passwords, expired sessions, or a silent NextAuth misconfiguration after the verify-kit CI changes (PR #1292, merged ~Sept 8).

---

## Recent Deployment Activity

All production deployments READY. No new prod pushes in ~17 days (app stable after CI restructure sprint).

| PR | Title | State |
|---|---|---|
| #1291 | chore(ci): retire typecheck.yml, superseded by verify.yml | Prod READY |
| #1292 | chore: retrofit verify-kit | Prod READY |
| #1289 | test(conventions): ratchet four rules (+ close open endpoint) | Prod READY |
| #1288 | docs: handoff for security-remediation + www TLS outage | Prod READY |
| #1287 | fix(security): authorize subscription-cleanup actions | Prod READY |
| #1286 | perf(inngest): stop OFF-feature crons burning free-tier executions | Prod READY |

---

## Action Items

- [ ] **Investigate CredentialsSignin errors** — 17 users, last event today 06:00 UTC. Check if login is broken by testing manually. Start with NextAuth credentials provider config.
- [ ] **Connect Sentry** — Re-authorize via claude.ai connector settings (interactive session required). MongoDB health is invisible without it.
- [ ] **Connect PostHog** — Appointment count unavailable. Can't measure booking funnel health.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-15 | HEALTHY | Subscription billing resolved. 4 PRs shipped. |
| 2026-07-16 | HEALTHY | 0 Sentry errors. 9 prod deploys. |
| 2026-07-17 | HEALTHY | 0 errors. 0 new deploys. App stable. |
| 2026-07-18 | HEALTHY | 0 errors. 9 prod deploys. Paystack billing sprint done. |
| 2026-07-19 | WARNING | 1 Sentry error — /consumer render fail. SHEAHAIRCARE-5 recurring. |
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs merged (security + legal compliance sprint). |
| 2026-09-26 | **WARNING** | **CredentialsSignin active today. 17 users affected since June. Sentry/PostHog offline.** |

---

_Generated: 2026-09-26 08:10 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: Needs re-auth — [Connector settings](https://claude.ai/settings/connectors)_
