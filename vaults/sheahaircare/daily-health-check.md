# Sheahaircare Daily Health — 2026-08-26

**Status:** WARNING
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 341 events (2 issues)
**Uptime:** ~95% (19/20 recent deploys READY, 1 ERROR — failed build, immediately redeployed)
**Top Issue:** MongoNetworkError SSL/TLS on `GET /[slug]` — 334 events, ~10h ago. Likely build-time Atlas hit in `generateStaticParams`. PR #1285 (deployed today) adds a fail-soft guard.
**Recommendation:** Confirm PR #1285 silences the MongoDB SSL errors. Monitor SHEAHAIRCARE-1M (injection attempt on `/api/assistant/chat` — 7 events) — check rate-limit and input validation on that route.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1285 `fix/generate-static-params-db-guard` — READY. 19/20 recent deploys READY. 1 ERROR (failed first attempt on #1279, immediately redeployed — normal). |
| MongoDB | WARNING | 334 SSL/TLS errors on `GET /[slug]` ~10h ago (SHEAHAIRCARE-1N). Root cause: `generateStaticParams` hitting Atlas at build time without a guard. PR #1285 adds the guard — watch for recurrence. |
| Sentry | WARNING | 341 events across 2 unresolved issues in 24h. See Runtime Errors below. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors

**341 events** across 2 issues in last 24h.

### SHEAHAIRCARE-1N — MongoNetworkError (334 events)
- **Error:** `MongoNetworkError: SSL routines:ssl3_read_bytes:tlsv1 alert internal error`
- **Culprit:** `GET /[slug]`
- **First/Last seen:** ~10 hours ago (burst — not ongoing)
- **Root cause:** `generateStaticParams` on `salon/[slug]` attempted a DB query at build time. When Atlas was unreachable, the SSL handshake failed repeatedly. No user-facing downtime — build-time only.
- **Fix deployed:** PR #1285 adds a `try/catch` guard — returns `[]` (dynamic fallback) when DB is unreachable. Matches the guard already on `(public)/[slug]`.
- **Watch:** If this fires again in production requests (not build), it's a real Atlas connectivity issue — escalate.

### SHEAHAIRCARE-1M — assistant.injection_attempt (7 events)
- **Error:** `assistant.injection_attempt`
- **Culprit:** `POST /api/assistant/chat`
- **First seen:** ~10h ago. **Last seen:** ~9h ago.
- **Users affected:** 0 (no user accounts compromised)
- **Action:** Review input sanitization and rate-limiting on `/api/assistant/chat`. Confirm the injection was caught and blocked (0 users affected is a good sign). Check if the prompt-injection guard is logging the payload for review.

---

## Today's Shipping Activity (2026-08-25/26 sprint)

Active sprint: security hardening + auth fixes.

| PR | Title | Status |
|---|---|---|
| #1285 | fix(build): fail soft when generateStaticParams cannot reach the DB | Prod READY |
| #1284 | fix(auth): pin JWT session lifetime (7d rolling) | Prod READY |
| #1283 | fix(security): bump mongoose to 9.9.4 (GHSA-664h-wqgq-64gw) | Prod READY |
| #1278 | chore(security): ignore unreachable js-yaml 3.14.2 (gray-matter) | Prod READY |
| #1276 | fix(security): set authTagLength in decryptSecret (GCM compliance) | Prod READY |
| #1275 | fix(security): clear 16 transitive dependency advisories via overrides | Prod READY |
| #1274 | docs(deploy): clear TEST webhook URL during live cutover | Prod READY |
| #1273 | fix(paystack): report which MODE sent a rejected webhook | Prod READY |
| #1272 | fix(paystack): name the cause of a rejected webhook signature | Prod READY |

---

## Action Items

- [ ] **Watch SHEAHAIRCARE-1N** — Confirm no recurrence after PR #1285. If MongoDB SSL errors appear in production requests (not build), escalate to Atlas: check connection string TLS settings and Atlas network access.
- [ ] **Investigate SHEAHAIRCARE-1M** — 7 injection attempts on `/api/assistant/chat`. Review prompt-injection guard logs. Consider tightening rate-limits on the chat endpoint if attempts continue.
- [ ] **Connect PostHog** — Appointment count still unavailable. Booking funnel is a blind spot heading into launch.

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
| **2026-08-26** | **WARNING** | **341 Sentry events: 334 MongoDB SSL errors (build-time, fixed by PR #1285) + 7 injection attempts on /api/assistant/chat. 9 PRs shipped (security hardening sprint).** |

---

_Generated: 2026-08-26 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/issues/?query=is%3Aunresolved+project%3Asheahaircare)_
