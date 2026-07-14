# Sheahaircare Daily Health — 2026-07-14

**Status:** WARNING
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 28+ occurrences across 9 error groups (threshold >5 triggered)
**Uptime:** 100% — all prod deployments READY, 5 PRs shipped today
**Top Issue:** Vault 401 Unauthorized — Inngest marketing sync jobs failing since 04:30 SAST (GitHub token likely expired)
**Recommendation:** Check and rotate the GitHub PAT used by the vault integration (`src/lib/marketing/github-vault.ts`). Also investigate DYNAMIC_SERVER_USAGE errors on `/find` pages — SEO risk.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | All deploys READY. Latest prod: PR #850 (billing quotas). |
| MongoDB | RECOVERING | PR #844 fix deployed — awaiting clean 24h window to confirm resolved. |
| Sentry | OFFLINE | MCP authentication expired. Error tracking blind. Re-auth needed. |
| PostHog | NOT CONNECTED | Appointment count unavailable. |

---

## Runtime Errors (24h) — 9 groups, 28+ occurrences

### CRITICAL — Vault 401 Unauthorized (Inngest marketing sync)
- **Routes:** `/api/inngest`
- **Error:** `vault list failed for 06_Marketing/Social/Playbooks: 401 Unauthorized`
  Also hitting: `06_Marketing/Social/Strategy` and `06_Marketing/Brand`
- **Count:** 4+1+1 = 6 occurrences | **First:** 04:30 SAST today | **Last:** 04:35 SAST today
- **Root cause:** GitHub PAT used by `github-vault.ts` has expired or been revoked
- **Impact:** Inngest marketing sync function fully broken. Playbooks/Strategy/Brand content not syncing.
- **Fix:** Rotate the GitHub PAT in Vercel env vars and redeploy.

### WARNING — Inngest step/function errors
- **Route:** `/api/inngest`
- **Count:** 5+1 = 6 occurrences | **Window:** 04:30–04:35 SAST today
- **Cause:** Downstream of the vault 401 failures above. Fix the token, these clear.

### WARNING — DYNAMIC_SERVER_USAGE on /find pages
- **Route:** `/find/[city]/[service]` — specifically `/find/pretoria/kids`
- **Count:** 6+2 = 8 occurrences | **Last:** 05:33 SAST today
- **Impact:** Discovery pages throwing Server Components render errors. SEO risk — these pages should be statically renderable.
- **Fix:** Audit `/find/[city]/[service]` for any `cookies()`, `headers()`, or `searchParams` access inside a cached Server Component.

### INFO — CredentialsSignin errors
- **Route:** `/api/auth/[...nextauth]`
- **Count:** 6+2+2 = 10 occurrences | **Last:** 03:52 SAST today
- **Likely cause:** User wrong-password attempts + possible bot traffic. Not a code bug.
- **Monitor:** If count spikes above 20/day, consider rate limiting login endpoint.

### LOW — Mongoose deprecation warnings
- **Route:** `/api/consumer/signup`
- `findOneAndUpdate()` using deprecated `new` option → use `returnDocument: 'after'`
- Non-breaking. Clean up when touching that file.

---

## Today's Shipping Activity (PRs #846–#850)

5 PRs merged to production.

| PR | Change | Status |
|---|---|---|
| #850 | feat(billing): per-tier stylist AI-generation quotas (Grow 5, Pro 40, Scale ∞) | ✅ PROD |
| #849 | docs(agents): Tiplates monetization (M1-M3) + live-QA polish | ✅ PROD |
| #848 | fix(consumer): remove hardcoded portal announcement strip | ✅ PROD |
| #847 | feat(tiplates): monetization M3 — storefront Journeys section | ✅ PROD |
| #846 | fix(signup): inline field validation + surface stylist email-dedup message | ✅ PROD |

Notable: Tiplates monetization M1-M3 fully live. Paystack split payments wired. AI generation quotas per tier active.

---

## Open Action Items

- [ ] **URGENT: Rotate GitHub PAT for vault integration** — Inngest marketing sync is broken. Likely the env var `GITHUB_VAULT_TOKEN` or similar. Update in Vercel project env vars and redeploy. (`src/lib/marketing/github-vault.ts`)
- [ ] **Fix DYNAMIC_SERVER_USAGE on /find pages** — Audit `/find/[city]/[service]` for dynamic API usage inside cached Server Components. SEO impact.
- [ ] **Re-authenticate Sentry MCP** — error tracking blind. Go to claude.ai connector settings and reconnect.
- [ ] **Add PostHog token** — appointment tracking unavailable. 5-min task.
- [ ] **Monitor MongoDB** — PR #844 fix is live. Watch for any recurrence of `MongoNetworkTimeoutError` on marketplace pages.
- [ ] **Fix Mongoose deprecation** — `findOneAndUpdate()` `new` option → `returnDocument: 'after'`. Low priority.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-10 | HEALTHY | 0 unresolved issues. Hydration error resolved. 7 PRs shipped. |
| 2026-07-11 | WARNING | SHEAHAIRCARE-Y (hooks violation, signin). 1 build failure auto-recovered. 8 PRs shipped. |
| 2026-07-12 | WARNING | MongoNetworkTimeoutError on marketplace (4 events, 3 users). Sentry offline. 9 PRs shipped. |
| 2026-07-13 | — | No check run. |
| **2026-07-14** | **WARNING** | **Vault 401 Unauthorized — Inngest marketing sync broken. DYNAMIC_SERVER_USAGE on /find pages. 5 PRs shipped (Tiplates monetization complete).** |

---

_Generated: 2026-07-14 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: OFFLINE — re-auth needed at claude.ai connector settings_
