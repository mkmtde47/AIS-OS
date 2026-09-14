# Sheahaircare Daily Health — 2026-09-14

**Status:** WARNING
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 0
**Uptime:** 100% (10/10 deploys READY in 24h)
**Top Issue:** www → 307 → apex redirect inverted since 2026-08-26 TLS outage. Paystack POST webhooks are unreachable. 19 days unresolved.
**Recommendation:** Fix Vercel domain routing — restore apex → 308 → www. All env vars and third-party callbacks expect www.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | 10/10 deploys READY in 24h. 5 prod merges. Latest: PR #1291 `chore(ci): retire typecheck.yml`. |
| MongoDB | HEALTHY | 0 Sentry errors. No DB errors surfaced. |
| Sentry | HEALTHY | 0 error events in 24h. 0 unresolved issues. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors

**0 errors** in last 24h. Clean.

---

## Today's Shipping Activity (2026-09-14)

5 PRs merged to production. All READY.

| PR | Title | Status |
|---|---|---|
| #1292 | chore: retrofit verify-kit | Prod READY |
| #1291 | chore(ci): retire typecheck.yml, superseded by verify.yml | Prod READY |
| #1289 | test(conventions): ratchet four prose rules + close open endpoint | Prod READY |
| #1288 | docs: handoff for security-remediation + www TLS outage session | Prod READY |
| #1287 | fix(security): authorize subscription-cleanup actions; write a real README | Prod READY |

Also active today: 5 preview builds for PRs #1290, #1289, #1288, #1287 (branch builds). All READY.

---

## Outstanding Issue — www Redirect Inversion (CRITICAL PATH)

**Since:** 2026-08-26 (TLS outage during security audit)
**Duration unresolved:** 19 days

The domain re-add after the TLS incident left the redirect inverted:
- **Current:** `www.sheahaircare.com → 307 → sheahaircare.com`
- **Expected:** `sheahaircare.com → 308 → www.sheahaircare.com`

Every env var, OAuth callback, and Paystack webhook is registered to `www`. A 307 redirect strips the POST body — Paystack payment events are silently dropped. Revenue-critical.

**Fix:** In Vercel project settings → Domains, remove and re-add domains with `www` as primary and apex as redirect (308). Verify with a test webhook POST after the change.

---

## Security Sprint Summary (carried forward)

The 2026-08-25/26 security audit closed **7 Critical, 31 High** findings → 0C/0H. Key fixes landed:
- Mongoose prototype pollution (GHSA-664h-wqgq-64gw) — bumped to 9.9.4
- JWT session maxAge — pinned to 7-day rolling (was 30-day implicit)
- subscription-cleanup server actions — authorization guard added
- Hard launch gate passes **static analysis only** — dynamic probes failed during the TLS outage. Gate is not fully cleared.

---

## Action Items

- [ ] **FIX www redirect (URGENT)** — Paystack webhooks broken 19 days. Revenue impact unquantifiable without PostHog. Fix Vercel domain routing.
- [ ] **Rerun DAST security scan** — The 2026-08-25 scan's dynamic phases all failed during the TLS outage. Hard launch gate shows `pass` but is static-only. Need a clean dynamic pass before hard launch.
- [ ] **Connect PostHog** — Appointment count still unavailable. No visibility into booking funnel.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-15 | HEALTHY | Subscription billing resolved. 4 PRs. |
| 2026-07-16 | HEALTHY | 0 errors. 9 prod deploys. Security fix shipped. |
| 2026-07-17 | HEALTHY | 0 errors. App stable after billing sprint. |
| 2026-07-18 | HEALTHY | 0 errors. 9 prod deploys. Paystack billing sprint done. |
| 2026-07-19 | WARNING | 1 Sentry error. SHEAHAIRCARE-5 recurring. 4 PRs. |
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs (security + legal compliance sprint). |
| 2026-08-25/26 | WARNING | TLS outage voided DAST scan. www redirect inverted. 7C/31H sec audit → 0C/0H. |
| 2026-09-07 | WARNING | www redirect still inverted. Handoff recorded. |
| **2026-09-14** | **WARNING** | **0 errors. 5 PRs shipped (CI + conventions + security). www redirect unresolved day 19.** |

---

_Generated: 2026-09-14 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=level%3Aerror&field=count%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
