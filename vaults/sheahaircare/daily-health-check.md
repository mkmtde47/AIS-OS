# Sheahaircare Daily Health — 2026-05-15

**Status:** CRITICAL
**Appointments (24h):** UNKNOWN — PostHog not connected
**Errors (24h):** 97 events across 12 unresolved issues
**Uptime:** UNKNOWN — Vercel personal account not resolvable via MCP
**Top Issue:** `Cannot find module './6141.js'` — 58 events (broken build/deployment)
**Recommendation:** Redeploy immediately. A broken build chunk is cascading into 58+ errors. Separately, MongoDB DNS is timing out — check Atlas for cluster pause or network issue.

---

## Detail

| System | Status | Note |
|---|---|---|
| Vercel | UNKNOWN | Personal account; no team ID; MCP can't resolve without one |
| Sentry | CRITICAL | 97 error events, 12 unresolved issues — up from 22 two days ago |
| MongoDB | CRITICAL | DNS timeout: `querySrv ETIMEOUT _mongodb._tcp.cluster0.slbpldp.mongodb.net` |
| PostHog | UNKNOWN | Token still placeholder in references/posthog-api.md |

---

## Sentry Issues (last 24h)

| Issue | Title | Events | Culprit |
|---|---|---|---|
| JAVASCRIPT-NEXTJS-7 | Cannot find module './6141.js' | 58 | `/_error` |
| SHEAHAIRCARE-4 | Dynamic server usage: /[slug] can't render statically | 17 | `/(public)/[slug]` |
| SHEAHAIRCARE-5 | Server Components render error (digest omitted) | 6 | `/(public)/[slug]/page` |
| JAVASCRIPT-NEXTJS-3 | Server Action not found on server | 5 | `/onboarding` |
| JAVASCRIPT-NEXTJS-6 | Unknown error | 3 | `/:slug` |
| SHEAHAIRCARE-9 | TypeError: Cannot read properties of undefined (reading 'call') | 2 | `/_error` |
| SHEAHAIRCARE-7 | next/image: hostname not configured | 2 | `/[slug]` |
| SHEAHAIRCARE-A | TypeError: __webpack_require__.a is not a function | 1 | `/dashboard/[slug]` |
| SHEAHAIRCARE-8 | **querySrv ETIMEOUT** _mongodb._tcp.cluster0.slbpldp.mongodb.net | 1 | `/` (Page Server Component) |
| JAVASCRIPT-NEXTJS-5 | Hydration Error | 1 | `localhost:3000/96-locks-n-styles` |
| JAVASCRIPT-NEXTJS-4 | Hydration failed — SSR/client mismatch | 1 | `/:slug` |
| SHEAHAIRCARE-6 | eval | 1 | `/_error` |

**Total events:** 97 (threshold: >5 → flag; >50 → critical)
**Org:** fl4ll.sentry.io | [View in Sentry](https://fl4ll.sentry.io/issues/?query=is%3Aunresolved+lastSeen%3A-24h)

---

## Root Cause Analysis

### Issue 1: Broken build chunk (PRIMARY — fix first)
`JAVASCRIPT-NEXTJS-7` — `Cannot find module './6141.js'` with 58 events is the dominant issue. This is a webpack chunk that's referenced in the build manifest but missing from the output. It cascades into several `/_error` and `getInitialProps` failures across the site.

**Fix:**
1. Trigger a fresh Vercel deployment (force redeploy — clear cache)
2. If it persists, check recent commits for dynamic imports or code splitting changes
3. Confirm error stops after redeploy

### Issue 2: MongoDB unreachable (INFRASTRUCTURE)
`SHEAHAIRCARE-8` — `querySrv ETIMEOUT` means DNS resolution for the MongoDB Atlas cluster is failing. The app homepage (`/`) hits the DB on load — this makes the homepage broken for any user that hits this.

**Fix:**
1. Log into MongoDB Atlas — check if cluster is paused (free tier auto-pauses after 60 days idle)
2. If paused: resume cluster
3. If running: check Atlas network access list for Vercel IP ranges
4. Long-term: add MongoDB health-check script to `scripts/`

### Issue 3: Dynamic server usage on /[slug]
`SHEAHAIRCARE-4` — 17 events. The slug route is trying to read `searchParams` in a statically rendered page. This is a Next.js 15 breaking change.

**Fix:**
1. Await `searchParams` properly: `const params = await searchParams`
2. Or add `export const dynamic = 'force-dynamic'` to the route

### Issue 4: next/image unconfigured hostname
`SHEAHAIRCARE-7` — `encrypted-tbn0.gstatic.com` not in `next.config.js`. Low priority but easy fix.

**Fix:** Add hostname to `images.remotePatterns` in `next.config.js`

---

## Trend

| Date | Errors | Issues | Top Problem |
|---|---|---|---|
| 2026-05-13 | 22 | 3 | NextAuth Invalid URL |
| 2026-05-15 | 97 | 12 | Broken build chunk + MongoDB down |

Errors up **4.4x** in 2 days. Previous auth issue appears resolved but replaced by a build regression and infrastructure failure.

---

## Monitoring Gaps (Day 5 — still unresolved)

| Gap | Fix | Effort |
|---|---|---|
| Vercel | Add Sheahaircare project ID to connections.md | 5 min |
| PostHog | Replace placeholder token; add script in `scripts/` | 15 min |
| MongoDB | Add connection string to `.env`; add health-check script | 20 min |

---

_Generated: 2026-05-15 08:00 SAST_
