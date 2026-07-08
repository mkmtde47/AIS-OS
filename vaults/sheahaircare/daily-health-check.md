# Sheahaircare Daily Health — 2026-07-08

**Status:** WARNING
**Appointments (24h):** N/A (PostHog not connected)
**Errors (24h):** 7 error groups — threshold exceeded (>5)
**Uptime:** 100% (production deployment READY)
**Top Issue:** MongoNetworkTimeoutError at 21:41 UTC — DB connection timed out (18s, above 10s limit)
**Recommendation:** Check MongoDB Atlas cluster health and IP allow-list. Auth errors are secondary but recurring.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Production READY. New deployment (PR #692) QUEUED. |
| Sentry | HEALTHY | 0 errors captured for sheahaircare in last 24h. |
| PostHog | NOT CONNECTED | Appointment count unavailable. |
| MongoDB | DEGRADED | 1 MongoNetworkTimeoutError at 21:41 UTC — secureConnect timed out (18.2s). |

---

## Runtime Errors (Last 24h)

| Error | Count | Last Seen | Route |
|---|---|---|---|
| MongoNetworkTimeoutError — secureConnect timed out (18.2s) | 1 | 2026-07-07 21:41 UTC | `/[slug].rsc` (storefront) |
| CredentialsSignin — auth failure | 4 | 2026-07-07 21:10 UTC | `/api/auth/[...nextauth]` |
| Auth stack trace error | 3 | 2026-07-07 20:37 UTC | `/api/auth/[...nextauth]` |
| Auth error (newer deployment) | 1 | 2026-07-07 21:10 UTC | `/api/auth/[...nextauth]` |
| MissingCSRF — signout token missing | 1 | 2026-07-07 13:47 UTC | `/api/auth/[...nextauth]` |
| Auth error (older deployment) | 1 | 2026-07-07 13:47 UTC | `/api/auth/[...nextauth]` |
| Mongoose deprecation warning | 1 | 2026-07-07 09:22 UTC | `/api/consumer/signup` |

**Total error events in 24h: 12 across 7 groups — above the >5 flag threshold.**

---

## Vercel Deployments

| Deployment | Status | Commit |
|---|---|---|
| dpl_v9F4v8tXfiKyHPBdQ8dyYE8U24nE | **READY (active prod)** | PR #691 — feat: Pulse social feed |
| dpl_3NA86DV3ZEbrB6kwfSZN4AL3KUua | **QUEUED (next prod)** | PR #692 — feat: Studio couture UI |
| dpl_C2h2FQYQU6V2f4MKpzEcBVLaQNv6 | BUILDING | PR #692 branch |

---

## Sentry Note

0 errors captured in Sentry for `sheahaircare` project in last 24h, while Vercel runtime shows 12 errors. Sentry SDK may not be integrated — errors are only appearing in Vercel logs.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-05 | WARNING | DYNAMIC_SERVER_USAGE on `/find/[city]/[service]` — 500s |
| 2026-07-06 | HEALTHY | /find issue quiet. 0 errors. |
| 2026-07-07 | HEALTHY | 0 Sentry errors. Active build week. |
| **2026-07-08** | **WARNING** | **MongoNetworkTimeoutError + 12 auth errors in 24h.** |

---

## Open Action Items

- [ ] **Investigate MongoDB timeout** — secureConnect timed out at 21:41 UTC. Check Atlas cluster status, IP allow-list, and connection pool settings.
- [ ] **Auth errors recurring** — CredentialsSignin + MissingCSRF errors on `/api/auth`. May be failed login attempts or a session config issue.
- [ ] **Wire Sentry SDK** — Vercel runtime errors not reaching Sentry. Add `@sentry/nextjs` if not already initialised.
- [ ] **Add PostHog token** — unlocks appointment tracking. 5 min task.

---

_Generated: 2026-07-08 08:00 SAST_
_Sentry: fl4ll org. [View dashboard](https://fl4ll.sentry.io/issues/)_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
