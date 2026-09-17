# Sheahaircare Daily Health — 2026-09-17

**Status:** WARNING
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 0
**Uptime:** 100% (20/20 READY across all tracked deploys)
**Top Issue:** www→apex redirect is a 307 (should be 308 apex→www) — breaks POST webhooks. Paystack payment callbacks at risk. Flagged Sept 7, unresolved 10 days.
**Recommendation:** Verify Vercel domain redirect config. Fix www↔apex inversion before any payment-flow testing or user acquisition.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | All 20 tracked deploys READY. Latest prod: PR #1292 `chore/verify-kit-retrofit-v2` (~Sept 9). No deploys in last 24h — app stable. |
| MongoDB | HEALTHY | 0 Sentry DB errors. SHEAHAIRCARE-5 (idle-pool race) silent for 59+ days. Likely resolved. |
| Sentry | HEALTHY | 0 error events in last 24h. No unresolved issues. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still blind. |

---

## Runtime Errors

**0 errors** in last 24h.

Sentry is clean. No crashes, no DB timeouts, no auth failures.

---

## Recent Shipping Activity

No production deploys in the last 24h. Last prod merge was Sept 9:

| PR | Title | Type |
|---|---|---|
| #1292 | chore: retrofit verify-kit (v2) | CI tooling |
| #1291 | chore(ci): retire typecheck.yml, superseded by verify.yml | CI tooling |
| #1289 | test(conventions): ratchet four prose rules + close open endpoint | Security/ratchets |
| #1288 | docs: handoff — security-remediation + www TLS outage session | Docs |
| #1287 | fix(security): authorize subscription-cleanup actions | Security fix |
| #1286 | perf(inngest): stop OFF-feature crons burning free-tier executions | Perf |
| #1285 | fix(build): fail soft when generateStaticParams can't reach DB | Reliability |
| #1283 | fix(security): bump mongoose 9.9.4 (GHSA-664h-wqgq-64gw) | Security fix |
| #1284 | fix(auth): pin JWT session lifetime, 7-day rolling | Security fix |

App has been quiet for 8 days post security sprint. No new features shipped.

---

## Open Issues

- [ ] **www→apex redirect inverted** — Vercel domain config shows `www -> 307 -> apex`. Should be `apex -> 308 -> www`. A 307 drops the POST body on redirect, which breaks Paystack webhook callbacks. Every env var and third-party OAuth callback is registered against `www`. Flagged in PR #1288 handoff (Sept 7). Fix in Vercel dashboard: set apex (sheahaircare.com) to redirect → www.sheahaircare.com with a 308. Verify Paystack webhook URL is pointed at www.
- [ ] **Connect PostHog** — Appointment count has been blind since Day 1. No visibility into booking funnel, drop-off, or conversion.
- [ ] **DAST gate incomplete** — PR #1288 notes the last security audit gate is STATIC-ONLY. Dynamic probes failed during the Sept 8 www TLS outage. A hard_launch_gate: enforce on static-only is unsafe. Run a fresh dynamic scan before launch.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-10 | HEALTHY | 0 unresolved. Hydration error resolved. 7 PRs. |
| 2026-07-11 | WARNING | SHEAHAIRCARE-Y hooks violation (signin). 1 build failure. |
| 2026-07-12 | WARNING | MongoNetworkTimeoutError on marketplace (4 events). Sentry offline. |
| 2026-07-13 | — | No check run. |
| 2026-07-14 | WARNING | Vault 401 — Inngest marketing sync broken. DYNAMIC_SERVER_USAGE on /find. |
| 2026-07-15 | HEALTHY | Billing resolved. 4 PRs. url.parse() only open issue. |
| 2026-07-16 | HEALTHY | 0 errors. 9 prod deploys. Security fix (#864) shipped. |
| 2026-07-17 | HEALTHY | 0 errors. 0 new deploys. App stable post-billing sprint. |
| 2026-07-18 | HEALTHY | 0 errors. 9 prod deploys. Billing sprint complete. |
| 2026-07-19 | WARNING | 1 error — /consumer render fail 23:41 UTC. SHEAHAIRCARE-5 recurring. |
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs merged (security + legal compliance). 2 PRs in preview. |
| 2026-09-17 | **WARNING** | **0 errors. App stable. www→apex 307 redirect open 10 days. DAST gate incomplete. No PostHog.** |

---

## Action Items for Today

1. **Fix the domain redirect** — Vercel dashboard → sheahaircare → Domains. Set apex to redirect to www with 308. Takes 5 min. Paystack webhooks at risk until this is done.
2. **Schedule DAST re-run** — Security gate is static-only. Run dynamic scan before any launch push.
3. **Connect PostHog** — Wire the SDK token. Will unblock booking funnel visibility.

---

_Generated: 2026-09-17 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=level%3Aerror&field=count%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
