# Sheahaircare Daily Health — 2026-09-22

**Status:** HEALTHY
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 3
**Uptime:** ~100% (19/20 READY, 1 CANCELED by superseding push)
**Top Issue:** SHEAHAIRCARE-1Q — IndexedDB error on `/login` (3 events, 0 users affected)
**Recommendation:** Investigate SHEAHAIRCARE-1Q. Connect PostHog to restore appointment visibility.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1291 `chore(ci): retire typecheck.yml` — READY. 19/20 recent deploys READY. 1 CANCELED (normal — superseded by faster push). |
| MongoDB | HEALTHY | No MongoDB-specific Sentry errors in 24h. |
| Sentry | HEALTHY | 3 error events in 24h. 1 open unresolved issue (SHEAHAIRCARE-1Q). Below 5-error threshold. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors

**3 errors** in last 24h.

### SHEAHAIRCARE-1Q — UnhandledRejection on `/login`

> `Non-Error promise rejection captured with value: Object Not Found Matching Id:3, MethodName:update, ParamCount:4`

- 3 events, 0 users affected
- First seen: ~22h ago (2026-09-21 ~08:00 SAST)
- Last seen: ~22h ago
- Likely a browser-side IndexedDB state error, not a server failure
- No user impact reported but could affect some login flows

### Auth errors (background, not new)

- `CredentialsSignin` recurring on `/api/auth/[...nextauth]` — expected auth errors from users entering wrong credentials. 14 unique users total (since June). Not an app failure.

---

## Today's Deployment Activity (2026-09-22)

Latest 20 prod deploys — all READY. Recent merges:

| PR | Title | Status |
|---|---|---|
| #1292 | chore: retrofit verify-kit | Prod READY |
| #1291 | chore(ci): retire typecheck.yml, superseded by verify.yml | Prod READY |
| #1289 | test(conventions): ratchet four rules + close second open endpoint | Prod READY |
| #1288 | docs: handoff for security-remediation + www TLS outage session | Prod READY |
| #1287 | fix(security): authorize subscription-cleanup actions; write README | Prod READY |
| #1286 | perf(inngest): stop OFF-feature crons from burning free-tier executions | Prod READY |

---

## Action Items

- [ ] **Investigate SHEAHAIRCARE-1Q** — IndexedDB error on `/login`. 0 users affected but worth understanding. Could be a stale service worker or auth state bug. [View in Sentry](https://fl4ll.sentry.io/issues/SHEAHAIRCARE-1Q)
- [ ] **Connect PostHog** — Appointment count unavailable since the last time this was flagged. Booking funnel is a persistent blind spot.
- [ ] **Monitor CredentialsSignin** — 14 unique users have hit bad-password errors since June. Consider a "forgot password" nudge on repeated failures.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-15 | HEALTHY | Subscription billing resolved. url.parse() only open issue. |
| 2026-07-16 | HEALTHY | 0 errors. 9 prod deploys. Security fix (#864) shipped. |
| 2026-07-17 | HEALTHY | 0 errors. 0 new deploys. App stable after billing sprint. |
| 2026-07-18 | HEALTHY | 0 errors. 9 prod deploys. Paystack billing sprint complete. |
| 2026-07-19 | WARNING | 1 Sentry error. SHEAHAIRCARE-5 recurring. 4 PRs shipped. |
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs merged (security + legal compliance sprint). |
| 2026-09-22 | HEALTHY | 3 errors (below threshold). SHEAHAIRCARE-1Q IndexedDB login error (0 users). 6+ PRs recently shipped. |

---

_Generated: 2026-09-22 08:13 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=&field=count%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
_Sentry Issues: [View open issues](https://fl4ll.sentry.io/issues/?query=is%3Aunresolved+lastSeen%3A-24h)_
