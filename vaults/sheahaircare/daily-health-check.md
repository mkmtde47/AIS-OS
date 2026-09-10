# Sheahaircare Daily Health — 2026-09-10

**Status:** HEALTHY
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 0
**Uptime:** 100% (10/10 deploys READY in 24h; 20/20 overall)
**Top Issue:** Domain redirect inverted — `www → 307 → apex`. Should be `apex → 308 → www`. 307 breaks POST webhooks (Paystack).
**Recommendation:** Fix domain redirect in Vercel dashboard before next billing cycle or any Paystack webhook test. Connect PostHog to unblock appointment visibility.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1292 `chore/verify-kit-retrofit-v2` — READY. 10 deploys in 24h, all READY. 20/20 overall. 0 runtime errors. |
| MongoDB | HEALTHY | 0 Sentry DB errors. generateStaticParams guard (PR #1285) holding — no build-time Atlas failures. |
| Sentry | HEALTHY | 0 error events in 24h. 0 open unresolved issues. Clean. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still blind. |

---

## Runtime Errors

**0 errors** in last 24h.

No Vercel runtime errors. No Sentry events. App is clean.

---

## Today's Shipping Activity (24h)

10 deploys — 5 to production, 5 preview. All READY.

| PR | Title | Type | Status |
|---|---|---|---|
| #1292 | chore: retrofit verify-kit (v2 — rebuilt on clean kit) | Prod | READY |
| #1291 | chore(ci): retire typecheck.yml, superseded by verify.yml | Prod | READY |
| #1289 | test(conventions): ratchet four prose-only rules + close open endpoint | Prod | READY |
| #1288 | docs: handoff — security-remediation + www TLS outage session | Prod | READY |
| #1287 | fix(security): authorize subscription-cleanup actions; write README | Prod | READY |
| #1292 | chore: retrofit verify-kit (v2) | Preview | READY |
| #1291 | chore(ci): retire typecheck.yml | Preview | READY |
| #1290 | chore: retrofit verify-kit (original, red CI) | Preview | READY |
| #1289 | test(conventions): ratchet four prose-only rules | Preview | READY |
| #1288 | docs: handoff 2026-09-07 | Preview | READY |

**Notable:** PR #1287 patched a security gap — `auditSubscriptions()` and `fixSubscriptions()` were "use server" exports with zero auth. An unauthenticated POST could mass-disable paid Paystack subscriptions. Now guarded with `requireAdminSection("revenue")`. Critical fix.

**Also notable:** verify-kit is now wired in. Suite grew from 3,640 → 3,684 tests across 390 → 398 files. Harness now asserts file count, so a glob that silently matches nothing no longer exits 0.

---

## Open Issues

- [ ] **Fix domain redirect** — `www → 307 → apex` is inverted. Should be `apex → 308 → www` since all env vars and Paystack callbacks point to www. A 307 breaks POST webhooks. Fix in Vercel Domains settings.
- [ ] **DAST gate is static-only** — The `gate: pass` on record from the 2026-08-25/26 security sprint is static analysis only. Dynamic probes all failed during the www TLS outage. Do not use it to gate hard launch. Re-run DAST when the domain redirect is fixed.
- [ ] **Connect PostHog** — Appointment count still unavailable. Booking funnel is a blind spot.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-15 | HEALTHY | Subscription billing fully resolved. 4 PRs shipped. |
| 2026-07-16 | HEALTHY | 0 errors. 9 prod deploys. Security fix (#864) shipped. |
| 2026-07-17 | HEALTHY | 0 errors. 0 new deploys. App stable after billing sprint. |
| 2026-07-18 | HEALTHY | 0 errors. 9 prod deploys. Paystack billing sprint complete. |
| 2026-07-19 | WARNING | 1 Sentry error — /consumer render fail 23:41 UTC. SHEAHAIRCARE-5 recurring. |
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs merged (security + legal compliance sprint). |
| 2026-08-25/26 | WARNING | www TLS outage voided DAST run. Redirect now inverted (www→apex). |
| **2026-09-10** | **HEALTHY** | **0 errors. 5 prod deploys (security auth fix + CI overhaul). Domain redirect open.** |

---

_Generated: 2026-09-10 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=level%3Aerror&field=count%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
