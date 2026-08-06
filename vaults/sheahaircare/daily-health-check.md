# Sheahaircare Daily Health — 2026-08-06

**Status:** WARNING
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 0 crash events (1 active config warning)
**Uptime:** ~100% (18/20 READY, 2 CANCELED by superseding pushes)
**Top Issue:** SHEAHAIRCARE-16 — PAYSTACK_SECRET_KEY is not a live key in production (test mode active)
**Recommendation:** Set PAYSTACK_SECRET_KEY to sk_live_ key in Vercel environment variables immediately. Payments are failing silently.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1191 `docs/agents-md-enforcement-layer` — READY. 18/20 recent deploys READY. 2 CANCELED (normal — superseded by faster pushes). |
| MongoDB | HEALTHY | 0 DB errors in 24h. SHEAHAIRCARE-5 still silent. |
| Sentry | WARNING | 0 crash events. 1 active config warning: SHEAHAIRCARE-16 (Paystack test key in prod). |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Active Warnings

### SHEAHAIRCARE-16 — Paystack running in test mode on production
- **Symptom:** `[env-preflight] PAYSTACK_SECRET_KEY is not a live key (does not start with sk_live_) in production`
- **Events:** 2 events. First seen ~3h ago. Last seen ~38min ago.
- **Impact:** All payment attempts on production are using test credentials. Real transactions will not process. Revenue is at risk.
- **Fix:** In Vercel project settings → Environment Variables → set `PAYSTACK_SECRET_KEY` to the live key (`sk_live_...`). Redeploy to apply.
- [View in Sentry](https://fl4ll.sentry.io/issues/SHEAHAIRCARE-16)

---

## Today's Shipping Activity (2026-08-05/06 sprint)

Active enforcement-layer sprint. 10 PRs shipped across security, privacy, access control, and legal compliance.

| PR | Title | Status |
|---|---|---|
| #1191 | docs(agents): record enforcement-layer session, prune to 3 sprint entries | Prod READY |
| #1190 | fix(dashboard): make the two theme controls say which surface they change | Prod READY |
| #1189 | chore(eslint): remove 62 dead disable directives, drop the stubs | Prod READY |
| #1188 | fix(assistant): stop serving a lapsed stylist a paid AI budget | Prod READY |
| #1187 | chore: make the verification gate one command | Prod READY |
| #1186 | fix(privacy): stop serving customer likeness from public URLs (POPIA s19) | Prod READY |
| #1185 | fix(access): stop honouring paid features after a subscription lapses | Prod READY |
| #1184 | chore(eslint): add a lint layer, incident rules only | Prod READY |
| #1183 | fix(legal): correct five statements the documents made about our own system | Prod READY |
| #1182 | feat(branding): wire "Find my look" — the quiz, in language a stylist uses | Prod READY |

---

## Action Items

- [ ] **URGENT: Fix PAYSTACK_SECRET_KEY** — Test key detected in production (SHEAHAIRCARE-16). Go to Vercel env vars and swap in the `sk_live_` key. Payments are broken until this is resolved.
- [ ] **Connect PostHog** — Appointment count still unavailable. Booking funnel is a blind spot for 3+ weeks.
- [ ] **Watch SHEAHAIRCARE-5 one more day** — MongoDB idle-pool race still silent. Close the issue if no events today.

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
| **2026-08-06** | **WARNING** | **SHEAHAIRCARE-16: Paystack test key in production. 0 crash events. 10 PRs shipped (enforcement-layer sprint).** |

---

_Generated: 2026-08-06 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=level%3Aerror&field=count%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
_Sentry active issues: [SHEAHAIRCARE-16](https://fl4ll.sentry.io/issues/SHEAHAIRCARE-16)_
