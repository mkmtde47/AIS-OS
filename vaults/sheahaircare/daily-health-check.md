# Sheahaircare Daily Health — 2026-09-21

**Status:** WARNING
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 8 (threshold: >5)
**Uptime:** ~100% (19/20 READY, 1 CANCELED normal)
**Top Issue:** SHEAHAIRCARE-1R — "Failed to find Server Action" on POST /(home)/page (8 events, first/last seen ~18h ago)
**Recommendation:** Monitor SHEAHAIRCARE-1R — likely a post-deploy client/server version skew burst. If it recurs after the next deploy, add a hard refresh or revalidate the home route. Connect PostHog to close the booking funnel blind spot.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1291 `chore/retire-typecheck-workflow` — READY. 19/20 recent deploys READY. 1 CANCELED (normal — superseded). |
| MongoDB | HEALTHY | SHEAHAIRCARE-5 (idle-pool race) silent. 0 MongoDB errors in 24h. |
| Sentry | WARNING | 8 error events in 24h (threshold: >5). 1 unresolved issue: SHEAHAIRCARE-1R. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors

**8 errors** in last 24h.

### SHEAHAIRCARE-1R — Failed to find Server Action
- **Culprit:** `POST /(home)/page`
- **Events:** 8
- **Users affected:** 0
- **First seen:** ~18h ago
- **Last seen:** ~18h ago
- **Likely cause:** Post-deploy version skew — clients holding stale builds submitted a Server Action the new deployment no longer recognises. 8-event burst then stopped. Classic Next.js Server Actions behavior after a rapid deploy sequence.
- **Action:** Watch for recurrence on next deploy. If it spikes again, add `router.refresh()` on Server Action error or shorten ISR TTL on `/(home)/page`.

---

## Today's Shipping Activity

Latest prod deploy: **PR #1291** — `chore(ci): retire typecheck.yml, superseded by verify.yml`

Recent sprint (last visible deploys):
| PR | Title | Status |
|---|---|---|
| #1292 | chore: retrofit verify-kit | Prod READY |
| #1291 | chore(ci): retire typecheck.yml, superseded by verify.yml | Prod READY |
| #1289 | test(conventions): ratchet four rules + close open endpoint | Prod READY |
| #1288 | docs: handoff for security-remediation + www TLS outage | Prod READY |
| #1287 | fix(security): authorize subscription-cleanup actions; write README | Prod READY |
| #1286 | perf(inngest): stop OFF-feature crons burning free-tier executions | Prod READY |

---

## Action Items

- [ ] **Watch SHEAHAIRCARE-1R** — 8-event burst ~18h ago on `/(home)/page`. No new events since. If it fires after the next deploy, add `router.refresh()` on Server Action 404 or shorten ISR TTL on the home page.
- [ ] **Connect PostHog** — Appointment count still unavailable. Booking funnel is a blind spot. Wire up and re-run `/audit` once live.

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
| **2026-09-21** | **WARNING** | **8 errors — SHEAHAIRCARE-1R Server Action version skew burst (18h ago, stopped). 6 prod deploys since last check. SHEAHAIRCARE-5 silent.** |

---

_Generated: 2026-09-21 08:19 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=&field=count%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
_Sentry issue: [SHEAHAIRCARE-1R](https://fl4ll.sentry.io/issues/SHEAHAIRCARE-1R)_
