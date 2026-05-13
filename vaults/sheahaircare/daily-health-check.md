# Sheahaircare Daily Health — 2026-05-13

**Status:** WARNING
**Appointments (24h):** UNKNOWN — PostHog not connected
**Errors (24h):** 22 events across 3 issues
**Uptime:** UNKNOWN — Vercel personal account not resolvable via MCP
**Top Issue:** TypeError: Invalid URL on `/api/auth/[...nextauth]` — 18 events (NextAuth misconfiguration)
**Recommendation:** Fix NextAuth config today. The auth route is throwing on every request — users cannot sign in or sign up.

---

## Detail

| System | Status | Note |
|---|---|---|
| Vercel | UNKNOWN | Personal account; no team ID; MCP can't resolve without one |
| Sentry | WARNING | 22 error events, 3 unresolved issues — auth route broken |
| PostHog | UNKNOWN | Token still placeholder in references/posthog-api.md |
| MongoDB | UNKNOWN | Listed as "setup pending" in connections.md |

---

## Sentry Issues (last 24h)

| Issue | Title | Events | Users | Culprit |
|---|---|---|---|---|
| SHEAHAIRCARE-2 | TypeError: Invalid URL | 18 | 0 | `GET /api/auth/[...nextauth]` |
| SHEAHAIRCARE-3 | TypeError: Invalid URL | 2 | 0 | `Page Server Component (/(auth)/signup)` |
| JAVASCRIPT-NEXTJS-2 | Server Components render error | 2 | 1 | `/signup` |

**Total events:** 22 (threshold: >5 → flagged)
**Org:** fl4ll.sentry.io
**First seen:** ~20 hours ago | **Last seen:** ~19 hours ago

### Root Cause (likely)
`SHEAHAIRCARE-2` — `TypeError: Invalid URL` on the NextAuth catch-all route (`/api/auth/[...nextauth]`) is the source. It's firing on every auth request and cascading into the signup Server Component. Most likely cause: `NEXTAUTH_URL` env var is missing, empty, or malformed in production.

### Fix
1. Check Vercel environment variables for `NEXTAUTH_URL` — must be the full production URL (e.g. `https://sheahaircare.vercel.app`)
2. Also check `NEXTAUTH_SECRET` is set
3. Redeploy after fixing env vars
4. Confirm SHEAHAIRCARE-2 stops firing

---

## Monitoring Gaps (Day 3)

| Gap | Fix | Effort |
|---|---|---|
| Vercel | Add Sheahaircare project URL or ID to connections.md | 5 min |
| PostHog | Replace placeholder token in posthog-api.md; add script in scripts/ | 15 min |
| MongoDB | Add connection string to .env; add health-check script | 20 min |

These gaps have persisted for 3 days. Until wired, appointment counts and uptime remain blind spots.

---

_Generated: 2026-05-13 08:00 SAST_
