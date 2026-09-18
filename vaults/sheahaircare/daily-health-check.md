# Sheahaircare Daily Health — 2026-09-18

**Status:** HEALTHY
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 0
**Uptime:** 100% (20/20 deployments READY)
**Top Issue:** www redirect inverted (307 → apex instead of 308 → www) — Paystack webhooks at risk
**Recommendation:** Verify Paystack webhook delivery. Fix www → apex 307 to apex → 308 → www before any user acquisition push.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1292 `chore: retrofit verify-kit` — READY. 20/20 recent deploys READY. |
| MongoDB | HEALTHY | 0 Sentry errors. DB build-time guard (PR #1285) in place. |
| Sentry | HEALTHY | 0 error events in 24h. 0 open unresolved issues. Clean. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel blind spot continues. |

---

## Runtime Errors

**0 errors** in last 24h.

No Sentry events. No open unresolved issues in the last 24h.

---

## Today's Shipping Activity (2026-09-18)

2 PRs merged to main. Both production deploys READY.

| PR | Title | Status |
|---|---|---|
| #1292 | chore: retrofit verify-kit | Prod READY (latest) |
| #1291 | chore(ci): retire typecheck.yml, superseded by verify.yml | Prod READY |

**CI infrastructure sprint summary:** verify-kit lands 3 new ratchet seeds (deferred-work, entitlement-predicates, keyset-pagination) not previously guarded. Test suite expanded 3,640 → 3,684 tests across 390 → 398 files. Harness now asserts file count — a glob matching nothing no longer exits 0 silently.

---

## Open Issue: www Redirect Inversion

Flagged in PR #1288 handoff (2026-08-25/26 session). Not yet resolved.

**Problem:** After the www TLS outage, the domain was re-added with the redirect inverted:
- Current: `www → 307 → apex`
- Expected: `apex → 308 → www`

Every env var and third-party callback (Paystack webhooks) is built around `www`. A 307 (temporary, no body) breaks POST webhooks — Paystack may be silently dropping payment events.

**Risk:** High. 0 Sentry errors could mean it's fine, or it could mean failures are uninstrumented.
**Action:** Check Paystack webhook delivery logs. Flip the redirect in Vercel domain settings.

---

## Action Items

- [ ] **Fix www redirect** — Flip `www → 307 → apex` to `apex → 308 → www` in Vercel domain settings. Verify Paystack webhook delivery before any bookings go live.
- [ ] **Connect PostHog** — Appointment count still unavailable. Booking funnel visibility remains a blind spot.
- [ ] **Verify security gate** — The `gate: pass` on record is STATIC-ONLY. Dynamic probes failed during the Aug 25 TLS outage. Do not use it as a hard-launch gate without a fresh DAST run.

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
| **2026-09-18** | **HEALTHY** | **0 errors. 2 PRs merged (CI infra sprint). www redirect inversion open — Paystack webhook risk.** |

---

_Generated: 2026-09-18 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=level%3Aerror&field=count%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
