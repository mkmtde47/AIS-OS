# Sheahaircare Daily Health — 2026-08-24

**Status:** HEALTHY
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 3 events (below threshold)
**Uptime:** 100% (20/20 READY)
**Top Issue:** CredentialsSignin — 1 user, 2 failed login attempts at 12:38 UTC
**Recommendation:** Monitor CredentialsSignin for spread to multiple users. Connect PostHog for appointment visibility.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1240 `docs/agents-md-pwa-session-2026-08-22` — READY. 20/20 recent deploys READY. 0 failures. |
| MongoDB | HEALTHY | No MongoDB errors in runtime logs. PR #1230 (mongoose connection pool drain on Fluid Compute suspend) shipped — directly addresses SHEAHAIRCARE-5 race. Second clean day confirms fix holding. |
| Sentry | UNAVAILABLE | Requires OAuth re-authorization. Authorize at claude.ai → Settings → Connectors. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors (Vercel — last 24h)

**3 error events** across 2 error groups. Below the >5 alert threshold.

| Error | Count | Route | Last Seen | Severity |
|---|---|---|---|---|
| `CredentialsSignin` | 2 | `/api/auth/[...nextauth]` | 2026-08-23 12:38 UTC | LOW — 1 user, 2 failed login attempts |
| `url.parse()` DeprecationWarning (DEP0169) | 1 | `/api/inngest` | 2026-08-23 07:00 UTC | INFO — chronic noise from inngest dependency |

**CredentialsSignin** — someone tried to log in with wrong credentials twice at 12:38 UTC yesterday. Not a server error; a user-side auth failure. Only 1 user affected. No action needed unless it spreads.

**url.parse() DEP0169** — persistent Node.js deprecation warning from the inngest SDK. Not a runtime crash. Known issue; fix is in inngest's hands or requires upgrading to a version using the WHATWG URL API.

---

## Active Shipping Activity (last 24h)

PWA sprint: 8 deploys to main, 20 total deploys in 24h. All READY.

| PR | Title | Status |
|---|---|---|
| #1240 | docs(agents): log PWA update-detection + badge session | Prod READY |
| #1239 | feat(pwa): badge the app icon from push, and badge customers too | Prod READY |
| #1238 | fix(pwa): apply service-worker updates without a reinstall | Prod READY |
| #1237 | docs(agents): log mobile zoom/maps/logout session | Prod READY |
| #1236 | fix(maps): pass placeholder to the Places element | Prod READY |
| #1235 | fix(maps): await genuine Places readiness instead of sampling once at onload | Prod READY |
| #1234 | fix(maps): reliable Places mount + revert over-styled autocomplete skin | Prod READY |
| #1233 | fix(mobile): input focus-zoom, maps autocomplete skin, advertiser sign-out | Prod READY |
| #1232 | feat(push): per-attempt delivery records + failure-ratio alarm | Prod READY |
| #1230 | feat(mongoose): drain connection pool on Fluid Compute suspend | Prod READY |

---

## Action Items

- [ ] **Watch CredentialsSignin** — 1 user, 2 failed attempts at 12:38 UTC. If multiple users start hitting this, investigate NextAuth credentials provider config.
- [ ] **Authorize Sentry** — MCP tool requires re-auth. Go to claude.ai → Settings → Connectors to reconnect. Sentry error data has been unavailable for this check.
- [ ] **Connect PostHog** — Appointment count still unavailable. Booking funnel visibility is a blind spot for daily health checks.
- [ ] **Address url.parse() DEP0169** — Deprecation warning on `/api/inngest`. Check if an inngest SDK upgrade resolves it; it's chronic noise that masks future real errors.

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
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs merged (security + legal compliance sprint). |
| **2026-08-24** | **HEALTHY** | **3 error events (2 CredentialsSignin, 1 url.parse). 10 prod PRs merged. PWA sprint complete. MongoDB pool fix shipped (#1230).** |

---

_Generated: 2026-08-24 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [Authorize at claude.ai Connectors](https://claude.ai/customize/connectors)_
