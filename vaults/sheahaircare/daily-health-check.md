# Sheahaircare Daily Health — 2026-07-24

**Status:** HEALTHY
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 0
**Uptime:** ~100% (16/20 READY, 4 CANCELED by superseding pushes)
**Top Issue:** url.parse() DEP0169 on /api/inngest — ongoing, low priority
**Recommendation:** Ship an Inngest SDK update to clear the url.parse() deprecation. Connect PostHog to unlock appointment funnel visibility.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1035 `docs/agents-md-perfumery-tiplates` — READY. 16/20 recent deploys READY. 4 CANCELED (normal — superseded by faster pushes). No failed builds. |
| MongoDB | HEALTHY | 0 Sentry errors today. No MongoNetworkTimeoutError events. DB connectivity inferred healthy from clean deploys. |
| Sentry | HEALTHY | 0 error events in 24h. 0 open unresolved issues in sheahaircare project. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors

**0 Sentry errors** in last 24h.

**1 Vercel runtime warning** (ongoing since 2026-06-06):
- `[DEP0169] url.parse()` on `/api/inngest` — last seen 2026-07-23 07:00 UTC. Not a crash, not customer-facing. Fix: upgrade Inngest SDK to a version using the WHATWG URL API.

---

## Today's Shipping Activity (2026-07-23/24 sprint)

8 PRs merged to main. All production deploys READY.

| PR | Title | Status |
|---|---|---|
| #1035 | docs(agents): record Perfumery category + Tiplates storefront showcase | Prod READY |
| #1034 | docs(agents): current-context entry for OAuth revocation follow-up | Prod READY |
| #1033 | feat(marketplace): add Perfumery provider category + promote Tiplates on storefronts | Prod READY |
| #1032 | fix(calendar): revoke Google OAuth grant at the source on disconnect + deletion | Prod READY |
| #1031 | feat(season-one): provider demand board (Phase 1c) | Prod READY |
| #1030 | docs(agents): current-context entry for the legal docs re-alignment | Prod READY |
| #1029 | feat(season-one): instrument the anonymous discovery surfaces (Phase 1b) | Prod READY |
| #1027 | fix(find): disclose paid Promoted placement on city + service SEO pages | Prod READY |

---

## Action Items

- [ ] **Upgrade Inngest SDK** — url.parse() DEP0169 has been open since 2026-06-06. Low priority but security-adjacent. One version bump closes it.
- [ ] **Connect PostHog** — Appointment count still unavailable. Booking funnel visibility is a blind spot. Wire up before any user acquisition push.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-15 | HEALTHY | 0 Sentry errors. 4 PRs shipped. url.parse() only open issue. |
| 2026-07-16 | HEALTHY | 0 Sentry errors. 9 prod deploys. Security fix (#864) shipped. |
| 2026-07-17 | HEALTHY | 0 errors. 0 new deploys. App stable after billing sprint. |
| 2026-07-18 | HEALTHY | 0 errors. 9 prod deploys. Paystack billing sprint complete. |
| 2026-07-19 | WARNING | 1 Sentry error — /consumer render fail 23:41 UTC. SHEAHAIRCARE-5 recurring. 4 PRs shipped. |
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs merged (security + legal compliance sprint). 2 preview PRs pending merge. |
| 2026-07-21 | — | No check run. |
| 2026-07-22 | — | No check run. |
| 2026-07-23 | — | No check run. |
| **2026-07-24** | **HEALTHY** | **0 errors. 8 PRs merged (Perfumery + Season One Phase 1b/1c + Calendar OAuth revoke). url.parse() still open.** |

---

_Generated: 2026-07-24 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=level%3Aerror&project=4511344680304640&field=count%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
