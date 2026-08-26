# Sheahaircare Daily Health — 2026-08-26

**Status:** WARNING
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 374 error-level events (Sentry) / 568 events across 50 error groups (Vercel runtime errors)
**Uptime:** ~100% — 19/20 recent deploys READY, 1 build ERROR same-day auto-redeployed clean, no production downtime
**Top Issue:** MongoDB Atlas TLS/SSL handshake burst (`SystemOverloadedError` + `RetryableError`) — 48 of 50 error groups, ~541 occurrences in a short window around 2026-08-25 20:13 UTC. Hit `/[slug]` (booking pages) and `/api/auth/[...nextauth]`. No recurrence since — appears self-resolved.
**Recommendation:** Watch for a repeat Atlas SSL burst today. If it recurs, check Atlas cluster tier/connection pool sizing (errorLabelSet flags it as a system-overload condition, not a code bug). No action needed on the blocked injection attempt — the guardrail worked as designed.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1285 `fix(build): fail soft when generateStaticParams cannot reach the DB` — READY. 19/20 recent deploys READY. 1 ERROR (PR #1279 build, root-caused to the same Atlas flakiness) auto-redeployed successfully same session. |
| MongoDB | WARNING | Atlas TLS/SSL alert burst (`ssl3_read_bytes:tlsv1 alert internal error`, SSL alert 80) — 541+ occurrences in ~1 minute, tagged `SystemOverloadedError`/`RetryableError`. Affected 2 users on `/[slug]`. No events since. PR #1285 (merged, now in prod) hardens `generateStaticParams` against exactly this failure mode at build time. |
| Sentry | WARNING | 374 error-level events in 24h — almost entirely the Mongo SSL burst above. 2 unresolved issues: SHEAHAIRCARE-1N (Mongo SSL, 334 events) and SHEAHAIRCARE-1M (blocked prompt-injection attempt, 7 events, see below). |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors — Detail

**50 error groups, 568 total occurrences** (Vercel runtime error aggregation, last 24h):

- **48 groups / ~541 events** — `MongoNetworkError: ssl3_read_bytes:tlsv1 alert internal error` (SSL alert 80). All clustered in a single short burst around 2026-08-25T20:13 UTC, tied to deployment `dpl_D75LPJSC2ssTGpt91bC6HZRjybw3` (PR #1276, GCM auth-tag fix). Routes: `/[slug]` (bulk of it) and `/api/auth/[...nextauth]` (28 events). One occurrence also hit `/mcp`. Labeled by the driver as `SystemOverloadedError` + `RetryableError` — this reads as an Atlas-side connection storm, not an application bug.
- 1 group — `MissingCSRF` on an auth callback (Auth.js).
- 1 group — unidentified stack frame, low volume.

Sentry's matching issue (SHEAHAIRCARE-1N) shows the same burst: first seen and last seen both ~8 hours ago, no fresh occurrences — treating this as resolved-for-now, watching for recurrence tonight.

---

## Security Note — Blocked Prompt Injection

**SHEAHAIRCARE-1M** — `assistant.injection_attempt`, 7 events, `POST /api/assistant/chat`, anonymous user from Cape Town, ZA. `reason: developer-mode` — someone tried a "developer mode" jailbreak prompt against the AI concierge chat. The app's own injection guardrail caught and blocked it (logged as a `warning`, not an exploited error). No action needed — this is the defense working correctly — but worth tracking if the volume grows.

---

## Today's Shipping Activity

10 PRs merged to main in the latest deploy window — a security/compliance-heavy sprint:

| PR | Title |
|---|---|
| #1285 | fix(build): fail soft when generateStaticParams cannot reach the DB |
| #1284 | fix(auth): pin JWT session lifetime instead of inheriting the 30-day default |
| #1283 | fix(security): bump mongoose to 9.9.4 (prototype pollution, GHSA-664h-wqgq-64gw) |
| #1279 | fix(assistant): pin maxDuration on the streaming chat routes |
| #1278 | chore(security): ignore unreachable js-yaml 3.14.2 (gray-matter) |
| #1276 | fix(security): set authTagLength in decryptSecret for GCM compliance |
| #1275 | fix(security): clear 16 transitive dependency advisories via overrides |
| #1274 | docs(deploy): clear the TEST webhook URL during the live cutover |
| #1273 | fix(paystack): report which MODE sent a rejected webhook |
| #1272 | fix(paystack): name the cause of a rejected webhook signature |

Notably, #1284 fixes a real security gap (session tokens were living 30 days instead of 7), and #1283 clears a prototype-pollution CVE in mongoose — both worth knowing landed today.

---

## Action Items

- [ ] **Watch for Atlas SSL burst recurrence** — if it fires again tonight, escalate to Atlas support or raise `minPoolSize`/connection retry tuning. PR #1285 already hardens the build-time path; the runtime path during the burst is unconfirmed as fixed.
- [ ] **Connect PostHog** — appointment count still unavailable, booking funnel is a blind spot on every report.
- [ ] **Connect Gmail** — this report could not be emailed; Gmail is still listed as "not yet connected" in `connections.md`. Wire it up to get these briefings pushed instead of read manually.
- [ ] No action on SHEAHAIRCARE-1M (injection attempt) — guardrail held. Consider it noise unless volume rises.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs merged (security + legal compliance sprint). 2 preview PRs pending merge (#906 POPIA, #907 legal copy). |
| **2026-08-26** | **WARNING** | **Mongo Atlas SSL/TLS burst (541 events, self-resolved). Blocked prompt-injection attempt on assistant chat. 10 PRs merged incl. session-lifetime + mongoose CVE fixes.** |

---

_Generated: 2026-08-26 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=level%3Aerror&project=4511344680304640&field=count%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
_Sentry: [SHEAHAIRCARE-1N (Mongo SSL burst)](https://fl4ll.sentry.io/issues/SHEAHAIRCARE-1N)_
_Sentry: [SHEAHAIRCARE-1M (blocked injection attempt)](https://fl4ll.sentry.io/issues/SHEAHAIRCARE-1M)_

**Note:** Email delivery to mkmmogano@gmail.com was requested but Gmail is not yet connected to this AIOS — report saved to file only. Connect Gmail to enable email delivery of future briefings.
