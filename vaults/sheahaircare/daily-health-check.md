# Sheahaircare Daily Health — 2026-07-29

**Status:** HEALTHY
**Appointments (24h):** UNAVAILABLE (PostHog not connected)
**Errors (24h):** 2
**Uptime:** 100%
**Top Issue:** `NotFoundError: removeChild` — DOM node removed before unmount (SHEAHAIRCARE-14, 2 occurrences, below alert threshold)
**Recommendation:** ALL CLEAR — monitor SHEAHAIRCARE-14 for recurrence; wire PostHog MCP for appointment tracking

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | HEALTHY | Latest prod: `dpl_7jwo8F` on `main` — READY. 0 runtime errors. All 20 recent deploys READY. |
| Sentry | HEALTHY | 2 errors in 24h (below >5 alert threshold). 1 issue group: SHEAHAIRCARE-14. |
| MongoDB | ASSUMED HEALTHY | App serving normally — no API errors in Sentry. No direct MCP check available. |
| PostHog | NOT CONNECTED | Appointment count unavailable. Booking funnel still a blind spot. |

---

## Runtime Errors

**2 errors** in last 24h.

| Issue | Title | Count | Last Seen |
|---|---|---|---|
| SHEAHAIRCARE-14 | `NotFoundError: removeChild on Node` | 2 | 2026-07-28 06:33 UTC |

**SHEAHAIRCARE-14** — `NotFoundError: Failed to execute 'removeChild' on 'Node': The node to be removed is not a child of this node.`
Browser-side DOM error, likely a React hydration or unmount race condition. 2 occurrences, not spiking. Monitor for increase.

---

## Today's Shipping Activity

Recent production deploys on `main`:

| Deploy | Commit | Status |
|---|---|---|
| `dpl_7jwo8F` | fix(consumer): session with no user redirects to sign-in (not consent wall) | READY |
| `dpl_HgUPEv` | fix(home): stop MarketplaceRows emitting a second category rail | READY |
| `dpl_CrRXV2` | feat(home): four self-care doors as swipeable row | READY |

Feature branches in preview (not yet on `main`):
- `feat/share-studio` — PR #1071: pre-made social assets, captions, tracked links (Share Studio)
- `fix/reland-house-doors-scroll-row` — PR #1070: re-land swipeable doors fix

---

## Action Items

- [ ] **Watch SHEAHAIRCARE-14** — 2 DOM removeChild errors, last seen yesterday. Low severity now, but if it spikes after the Share Studio merge, it may be tied to new SSR/hydration paths.
- [ ] **Merge PR #1070 / #1071** — Both preview deploys are READY. Share Studio is the priority feature.
- [ ] **Connect PostHog** — Appointment count still a blind spot. Cannot track booking conversion without it.
- [ ] **Add `/api/health` endpoint** — Ping MongoDB and surface status here automatically each morning.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-10 | HEALTHY | 0 unresolved issues. Hydration error resolved. 7 PRs shipped. |
| 2026-07-11 | WARNING | SHEAHAIRCARE-Y (hooks violation, signin). 1 build failure. 8 PRs shipped. |
| 2026-07-12 | WARNING | MongoNetworkTimeoutError on marketplace (4 events). |
| 2026-07-14 | WARNING | Vault 401 — Inngest marketing sync broken. |
| 2026-07-15 | HEALTHY | Subscription billing resolved. 4 PRs shipped. |
| 2026-07-16 | HEALTHY | 0 errors. 9 prod deploys. Security fix (#864) shipped. |
| 2026-07-17 | HEALTHY | 0 errors. App stable after billing sprint. |
| 2026-07-18 | HEALTHY | 0 errors. 9 prod deploys. Paystack billing sprint complete. |
| 2026-07-19 | WARNING | 1 Sentry error — /consumer render fail. SHEAHAIRCARE-5 recurring. |
| 2026-07-20 | HEALTHY | 0 errors. 7 PRs merged (security + legal compliance sprint). |
| **2026-07-29** | **HEALTHY** | **2 errors (DOM removeChild, below threshold). All deploys READY. Share Studio in preview.** |

---

_Generated: 2026-07-29 08:00 SAST_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
_Sentry: [View errors](https://fl4ll.sentry.io/explore/discover/homepage/?dataset=errors&queryDataset=error-events&query=&project=4511344680304640&field=issue&field=title&field=count%28%29&field=last_seen%28%29&sort=-count%28%29&statsPeriod=24h&mode=aggregate&yAxis=count%28%29)_
