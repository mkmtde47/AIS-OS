# Sheahaircare Daily Health — 2026-08-22

**Status:** WARNING
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 7 (3 timeouts + 2 auth errors + 2 credential errors)
**Uptime:** 100% (20/20 deployments READY)
**Top Issue:** 300s timeout on `/find/pretoria.segments/_tree.segment.rsc` — RSC route hitting Vercel's execution limit
**Recommendation:** Investigate `/find` segment route performance. 3 timeouts in ~2 minutes (21:27–21:29 UTC) suggests a heavy or unbounded DB query on the Pretoria segments tree. Add a timeout guard or paginate the RSC fetch.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1240 `docs/agents-md-pwa-session-2026-08-22` — READY. 20/20 recent deploys READY. 3 PRs shipped today (PWA sprint). |
| MongoDB | UNKNOWN | Sentry unavailable (OAuth required). Timeout errors on `/find` may indicate a slow atlas query. Watch. |
| Sentry | UNAVAILABLE | OAuth authentication required — connect via claude.ai connector settings to restore error tracking. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors (Vercel — last 24h)

**7 errors** across 3 groups.

| Error | Count | Routes | Last Seen |
|---|---|---|---|
| Vercel Runtime Timeout (300s) | 3 | `/find/pretoria.segments/_tree.segment.rsc`, `/[slug]/dashboard` | 2026-08-21 21:29 UTC |
| Unhandled exception (auth handler) | 2 | `/api/auth/[...nextauth]` | 2026-08-21 15:19 UTC |
| CredentialsSignin auth error | 2 | `/api/auth/[...nextauth]` | 2026-08-21 15:19 UTC |

### Error Detail

**Timeout (CRITICAL — 3 events, 1 user, ~2 min burst):**
`/find/pretoria.segments/_tree.segment.rsc` timed out at exactly 300s. Three consecutive hits between 21:27 and 21:29 UTC, all on the same deployment (`dpl_6i9MvCnbyFHPHA2hNoP1zHNnzswV`). This is a pre-PWA deploy, so the PWA sprint didn't introduce it. The `.segments/_tree.segment.rsc` path pattern suggests a dynamic RSC route loading a segment tree — possibly an unbounded MongoDB read.

**Auth errors (2 events, 1 user):**
`CredentialsSignin` error on `/api/auth/[...nextauth]` at 15:19 UTC. Likely a failed login attempt rather than a system fault. The error is surfaced but non-critical.

---

## Today's Shipping Activity (2026-08-22 PWA sprint)

3 PRs merged to main. All production deploys READY.

| PR | Title | Status |
|---|---|---|
| #1240 | docs(agents): log PWA update-detection + badge session (PRs #1238-#1239) | Prod READY |
| #1239 | feat(pwa): badge the app icon from push, and badge customers too | Prod READY |
| #1238 | fix(pwa): apply service-worker updates without a reinstall | Prod READY |

**PWA sprint outcome:** SW now auto-applies updates via `controllerchange` + `registration.update()` on focus. Badge count pushed from server via `sendPushToUser`, so the icon updates when the app is closed. Customers now have their own badge counter.

---

## Action Items

- [ ] **Investigate `/find` timeout** — 3 × 300s timeouts on `pretoria.segments/_tree.segment.rsc` at 21:27–21:29 UTC. Add a DB query timeout or paginate the segment tree fetch. One user was affected. If it recurs today, treat as P1.
- [ ] **Reconnect Sentry** — OAuth authentication needed. Without it, MongoDB errors and exception counts are invisible. Connect via claude.ai connector settings.
- [ ] **Connect PostHog** — Appointment count unavailable. Booking funnel still a blind spot.
- [ ] **Verify PWA badge on real device** — Badge visibility unconfirmed on an installed PWA home-screen icon. Test on Android (Chrome) before marketing the notification feature.

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
| 2026-07-21 to 2026-08-21 | — | No check runs. |
| **2026-08-22** | **WARNING** | **7 runtime errors: 3 × /find timeout (300s), 2 × auth exception, 2 × CredentialsSignin. 3 PRs shipped (PWA sprint). Sentry unavailable.** |

---

_Generated: 2026-08-22 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: UNAVAILABLE — reconnect via claude.ai connector settings_
