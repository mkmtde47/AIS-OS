# Sheahaircare Daily Health — 2026-09-16

**Status:** HEALTHY
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 2 (performance + CSP, 0 user impact)
**Uptime:** 100% (20/20 deployments READY)
**Top Issue:** N+1 Query on homepage prerender (SHEAHAIRCARE-1P) — 1 event, 0 users affected
**Recommendation:** Investigate N+1 query on `(app)/` prerender route. Connect PostHog — booking funnel still a blind spot.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1292 `chore: retrofit verify-kit` — READY. 20/20 recent deploys READY. |
| MongoDB | HEALTHY | 0 connection errors in Sentry. N+1 query flagged (perf, not availability). |
| Sentry | HEALTHY | 2 open issues, both low severity, 0 user impact. No level:error events in 24h. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors

**2 unresolved issues** — neither a hard crash, neither affecting users.

| Issue | Category | Events | Users | First Seen |
|---|---|---|---|---|
| [SHEAHAIRCARE-1P](https://fl4ll.sentry.io/issues/SHEAHAIRCARE-1P) N+1 Query | db_query | 1 | 0 | 2h ago |
| [SHEAHAIRCARE-1J](https://fl4ll.sentry.io/issues/SHEAHAIRCARE-1J) CSP font-src blocked (perplexity.ai) | security | 1 | 0 | 6h ago |

**N+1 Query** fires on prerender of `(app)/` — the homepage. This runs at build time, not on live user requests, so there's no user-facing latency hit yet. Worth patching before traffic scales.

**CSP block** is a font from `frontend-cdn.perplexity.ai` — likely an AI widget or third-party embed that isn't in the Content-Security-Policy allowlist. Low urgency but clean it up.

---

## Today's Shipping Activity (2026-09-16)

2 PRs merged to main. Both production deploys READY.

| PR | Title | Status |
|---|---|---|
| #1292 | chore: retrofit verify-kit | Prod READY |
| #1291 | chore(ci): retire typecheck.yml, superseded by verify.yml | Prod READY |

CI tooling sprint today — verify-kit retrofitted with 3,684 tests across 398 files. typecheck.yml retired and replaced by verify.yml (superset).

---

## Action Items

- [ ] **Investigate SHEAHAIRCARE-1P** — N+1 query on homepage prerender. Fix before traffic scales. Check what query runs unbounded during `generateStaticParams` or layout data fetch on `(app)/`.
- [ ] **Fix CSP for perplexity.ai** — Add `font-src https://frontend-cdn.perplexity.ai` to the CSP header, or identify and remove the embed triggering it.
- [ ] **Connect PostHog** — Appointment count still unavailable. Booking funnel visibility is a blind spot. This has been open since July 20.

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
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs merged (security + legal compliance sprint). 2 preview PRs pending merge (#906 POPIA, #907 legal copy). |
| 2026-08-25 | — | No check run. Security audit sprint: 3 runs, 0C/0H pass (PRs #1275, #1284). TLS outage on www. |
| **2026-09-16** | **HEALTHY** | **2 low-severity Sentry issues (N+1 query + CSP block), 0 user impact. 2 PRs merged (CI tooling). 20/20 deploys READY.** |

---

_Generated: 2026-09-16 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View issues](https://fl4ll.sentry.io/issues/?query=is%3Aunresolved)_
