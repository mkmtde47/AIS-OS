# Sheahaircare Daily Health — 2026-11-18

**Status:** WARNING
**Appointments (24h):** UNAVAILABLE — PostHog not configured
**Errors (24h):** 0 (Vercel runtime errors; Sentry needs re-auth)
**Uptime:** READY — latest production deployment live
**Top Issue:** Sentry disconnected + PostHog credentials not set
**Recommendation:** Re-auth Sentry at claude.ai connector settings; add PostHog API credentials to `references/posthog-api.md`

---

## Detail

### Vercel Deployment
- **State:** READY
- **Latest deploy:** `dpl_FfX2JvVwZpdWYfDN5Cp4uVWRrEqd`
- **Commit:** fix(scripts): drop emailVerified from the purge safety gate (PR #1296)
- **Branch:** main
- **Last 4 deployments:** 3 READY, 1 BLOCKED (old — May 2026, unrelated)

### Runtime Errors (Vercel, last 24h)
- **Count:** 0
- No errors detected

### Sentry (last 24h)
- **Status:** UNAVAILABLE — session needs re-auth
- Action: sign in at claude.ai connector settings to restore

### PostHog (last 24h)
- **Status:** NOT CONFIGURED — API credentials are placeholders
- Action: add project token + host to `references/posthog-api.md` and `.env`

### MongoDB
- **Status:** NOT DIRECTLY CHECKABLE — no MCP or script connected
- Listed as "setup pending" in connections.md
- Action: wire up a health-check script in `scripts/`

---

*Generated automatically — 2026-11-18 06:11 UTC*
