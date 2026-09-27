# Sheahaircare Daily Health — 2026-09-27

**Status:** WARNING
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 2
**Uptime:** ~99% (9/10 prod deploys READY, 1 CANCELED by superseding push)
**Top Issue:** SHEAHAIRCARE-1S — Downtime detected on `https://www.sheahaircare.com/api/health` (~18h ago)
**Recommendation:** Verify `/api/health` is currently responding. Investigate N+1 query on homepage prerender.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: PR #1296 `fix(scripts): drop emailVerified from the purge safety gate` — READY. 9/10 recent deploys READY. 1 CANCELED (normal — superseded). |
| MongoDB | HEALTHY (implied) | 0 Sentry errors targeting MongoDB in 24h. No DB connection failures seen. |
| Sentry | WARNING | 2 error events in 24h. 3 unresolved issues with activity in last 24h — see below. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Active Issues (Last 24h)

### SHEAHAIRCARE-1S — Downtime detected for `/api/health` ⚠️
- **Category:** outage
- **Events:** 1 (18h ago)
- **Users affected:** 0
- **Action needed:** Check if `/api/health` is currently returning 200. If not, this is a live incident. If it recovered, determine root cause and duration.

### SHEAHAIRCARE-1P — N+1 Query
- **Category:** db_query
- **Culprit:** `prerender route (app) /`
- **Events:** 1 (19h ago)
- **Users affected:** 0
- **Action needed:** Review homepage prerender query pattern. N+1 on the root route will hurt cold-start performance at scale.

### SHEAHAIRCARE-1J — CSP violation: perplexity CDN font blocked
- **Category:** CSP report
- **Events:** 2 (22h ago)
- **Action needed:** Low priority. If Perplexity fonts are intentional (AI widget), add `https://frontend-cdn.perplexity.ai` to `font-src` CSP directive.

---

## Shipping Activity (Today)

3 PRs merged in rapid succession — security/spam remediation sprint:

| PR | Title | Status |
|---|---|---|
| #1296 | fix(scripts): drop emailVerified from the purge safety gate | Prod READY |
| #1295 | chore(scripts): purge tool for the 2026-09-16 signup-spam accounts | Prod READY |
| #1294 | fix(security): gate provider signup behind BotID, cap welcome-email flood | Prod READY |
| #1293 | fix(proxy): forward x-pathname on the request (CANCELED — superseded) | CANCELED |

**Note:** PR #1293 cancel is normal — a faster push superseded it before the build finished.

---

## Action Items

- [ ] **Investigate SHEAHAIRCARE-1S** — Confirm `/api/health` is currently live. If it recovered, check logs for the 18h-ago window. If still down, escalate immediately.
- [ ] **Fix SHEAHAIRCARE-1P** — N+1 on homepage prerender. Profile the root route's DB calls and add `include` or batching.
- [ ] **Fix SHEAHAIRCARE-1J (low priority)** — Add `https://frontend-cdn.perplexity.ai` to `font-src` CSP, or remove the Perplexity widget if it's not intentional.
- [ ] **Connect PostHog** — Appointment count has been unavailable for 2+ months. Booking funnel is a blind spot.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-15 | HEALTHY | Subscription billing resolved. |
| 2026-07-16 | HEALTHY | 0 errors. Security fix (#864) shipped. |
| 2026-07-17 | HEALTHY | 0 errors. App stable after billing sprint. |
| 2026-07-18 | HEALTHY | 0 errors. Paystack billing sprint complete. |
| 2026-07-19 | WARNING | 1 Sentry error — /consumer render fail. SHEAHAIRCARE-5 recurring. |
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs merged (security + legal compliance sprint). |
| 2026-07-21–09-26 | — | No check run (68-day gap). |
| **2026-09-27** | **WARNING** | **2 errors. /api/health downtime detected (SHEAHAIRCARE-1S). Spam-purge sprint (3 PRs). PostHog still not connected.** |

---

_Generated: 2026-09-27 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=&field=count%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
_Sentry issues: [View unresolved](https://fl4ll.sentry.io/issues/?query=is%3Aunresolved+lastSeen%3A-24h)_
