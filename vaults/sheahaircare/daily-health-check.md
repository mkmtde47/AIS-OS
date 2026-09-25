# Sheahaircare Daily Health — 2026-09-25

**Status:** WARNING
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 21+ auth failures (CredentialsSignin — active this morning)
**Uptime:** ~100% (20/20 deployments READY)
**Top Issue:** 21 users hit `CredentialsSignin` on `/api/auth/[...nextauth]` in last 24h — last fired 06:09 SAST today. Possible brute-force, credential stuffing, or a login regression.
**Recommendation:** Check Auth logs for IP clustering. If IPs are diverse (multiple users), it's likely legitimate failed logins or a UX regression. If one IP, block it. Either way — investigate before dismissing.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | 20/20 deployments READY. 2 prod deploys merged today (PR #1291 typecheck retire, PR #1292 verify-kit). |
| Runtime Errors | WARNING | 21 `CredentialsSignin` events, 21 unique users, last 24h. Also 17 matching stack trace events — likely same auth failures, different chunk. All on `/api/auth/[...nextauth]`. |
| MongoDB | UNKNOWN | Sentry offline (needs OAuth re-auth). No DB connection errors in Vercel runtime logs. |
| PostHog | NOT CONNECTED | Appointment count unavailable. |
| Sentry | NOT CONNECTED | Session requires OAuth re-auth — not available in automated run. |

---

## Runtime Errors Detail

**3 error groups active in last 24h:**

### 1. `[auth][error] CredentialsSignin`
- **Count:** 21 | **Unique users:** 21
- **Route:** `/api/auth/[...nextauth]`
- **Last seen:** 2026-09-25 06:09:45 UTC (this morning, active)
- **First seen:** 2026-06-19 (recurring cluster)
- **Deployment:** `dpl_2HD2D6WwNL87TdeFbsWeNidQHXFX` (latest prod)

### 2. Stack trace — `_1yqmejq._.js:405` (same auth route)
- **Count:** 17 | **Unique users:** 17
- **Route:** `/api/auth/[...nextauth]`
- **Last seen:** 2026-09-25 06:09:45 UTC
- **Note:** Same route + timing as above — these are likely the inner cause stack for the CredentialsSignin error.

### 3. Stack trace — `_1adp_3b._.js:405` (older chunk)
- **Count:** 4 | **Unique users:** 4
- **Route:** `/api/auth/[...nextauth]`
- **Last seen:** 2026-09-24 22:32:44 UTC
- **Note:** Older deployment chunk. Fading out.

---

## Today's Shipping Activity

2 PRs merged to main since yesterday's check:

| PR | Title | Status |
|---|---|---|
| #1292 | chore: retrofit verify-kit | Prod READY |
| #1291 | chore(ci): retire typecheck.yml, superseded by verify.yml | Prod READY |

Recent context (last sprint):
- #1289 — test(conventions): ratchet four prose rules
- #1288 — docs: handoff for security-remediation + www TLS outage session
- #1287 — fix(security): authorize subscription-cleanup actions
- #1286 — perf(inngest): stop OFF-feature crons burning free-tier executions
- #1285 — fix(build): fail soft when generateStaticParams cannot reach DB

---

## Action Items

- [ ] **Investigate auth failures** — 21 unique users hit `CredentialsSignin` in 24h (last at 06:09 SAST). Check Vercel logs for IP clustering. If pattern is suspicious, consider rate-limiting the credentials endpoint or adding CAPTCHA.
- [ ] **Re-auth Sentry** — MCP requires interactive OAuth. Run `/mcp` in a live Claude Code session to reconnect. Without it, MongoDB health and error alerting are blind spots.
- [ ] **Connect PostHog** — Appointment count still unavailable. Booking funnel visibility is a blind spot.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-10 | HEALTHY | 0 unresolved issues. Hydration error resolved. 7 PRs shipped. |
| 2026-07-11 | WARNING | SHEAHAIRCARE-Y (hooks violation, signin). 1 build failure. |
| 2026-07-12 | WARNING | MongoNetworkTimeoutError on marketplace (4 events). |
| 2026-07-14 | WARNING | Vault 401 Unauthorized — Inngest marketing sync broken. |
| 2026-07-15 | HEALTHY | Subscription billing resolved. |
| 2026-07-16 | HEALTHY | 0 errors. Security fix shipped. |
| 2026-07-17 | HEALTHY | 0 errors. App stable. |
| 2026-07-18 | HEALTHY | 0 errors. Paystack billing sprint complete. |
| 2026-07-19 | WARNING | 1 Sentry error — /consumer render fail. SHEAHAIRCARE-5 recurring. |
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs merged (security + legal compliance sprint). |
| **2026-09-25** | **WARNING** | **21 CredentialsSignin auth failures in 24h. 21 unique users. Active at 06:09 SAST.** |

---

_Generated: 2026-09-25 08:19 SAST (automated)_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Note: Sentry + PostHog offline — email delivery skipped (Gmail not wired). Reconnect Sentry via interactive /mcp session._
