# Sheahaircare Daily Health — 2026-07-11

**Status:** WARNING
**Appointments (24h):** N/A — PostHog not connected
**Errors (24h):** 4 events, 1 unresolved issue
**Uptime:** 100% — prod READY (1 build failure auto-recovered)
**Top Issue:** SHEAHAIRCARE-Y — hooks violation on `/consumer/signin` (2 users affected)
**Recommendation:** Investigate SHEAHAIRCARE-Y. PR #789 build failure was a one-off; prod recovered via #790.

---

## System Status

| System | Status | Notes |
|---|---|---|
| Vercel | WARNING | Prod READY (PR #790). 1 build ERROR on PR #789 (auto-recovered). 8 PRs shipped today. |
| Sentry | WARNING | 4 error events, 1 unresolved issue (SHEAHAIRCARE-Y — new, affects signin). |
| PostHog | NOT CONNECTED | Appointment count unavailable. |
| MongoDB | HEALTHY | No DB errors in Sentry. No timeout events. |

---

## Sentry Issues (Open)

### SHEAHAIRCARE-Y — NEW
- **Error:** `Rendered more hooks than during the previous render.`
- **Culprit:** `/consumer/signin`
- **Events:** 2 | **Users:** 2
- **First seen:** ~10h ago (2026-07-10 ~22:00 SAST)
- **Status:** Unresolved

> Hooks-order violation on the consumer signin page. Likely introduced by recent auth refactor work (PRs #787–#790). Needs investigation.

---

## Sentry Error Events (24h) — 4 total

| Issue | Title | Events | Status |
|---|---|---|---|
| SHEAHAIRCARE-Y | Rendered more hooks than during previous render | 2 | **UNRESOLVED** |
| SHEAHAIRCARE-5 | Server Components render error (digest omitted in prod) | 1 | — |
| SHEAHAIRCARE-Z | UnrecognizedActionError: Server Action not found | 1 | Fixed by PR #785 (residual) |

Error threshold (>5): **NOT triggered** — 4 events in 24h.

---

## Vercel — Current Production

| Deployment | Status | PR | Description |
|---|---|---|---|
| dpl_6tNv8pZeWqcxenAESQuz1X5q7h9t | **READY (PROD)** | #790 | feat(billing): cancel membership → free at period end (PR2/3) |
| dpl_8iPJGE2DSuXECasRwrMUH89BSWbq | **ERROR** | #789 | copy: get-featured speaks as 'we' — BUILD FAILED, superseded |
| dpl_JB47NKTKYjtHoAfViC4mP9b8JDEW | READY (rollback) | #788 | feat(billing): customer billing page — view plan + upgrade (PR1/3) |

---

## Today's Shipping Activity (PRs Deployed)

| PR | Change | Status |
|---|---|---|
| #790 | feat(billing): cancel membership → free at period end (PR2/3) | ✅ PROD |
| **#789** | copy: get-featured speaks as 'we', not 'I' | ❌ BUILD ERROR (auto-recovered) |
| #788 | feat(billing): customer billing page — view plan + upgrade (PR1/3) | ✅ PROD |
| #787 | fix(auth): wait for session cookie before post-sign-in redirect | ✅ PROD |
| #786 | feat: reinforce founding offer on signup form | ✅ PROD |
| #785 | fix(consumer): recover from UnrecognizedActionError (SHEAHAIRCARE-Z) | ✅ PROD |
| #784 | fix: recruit door sends cold traffic to create-account | ✅ PROD |
| #783 | feat(portal): scroll-reveal the lower sections | ✅ PROD |

8 PRs shipped. Heavy build day.

---

## Trend

| Date | Status | Top Issue |
|---|---|---|
| 2026-07-07 | HEALTHY | 0 Sentry errors. Active build week. |
| 2026-07-08 | WARNING | MongoNetworkTimeoutError + 12 auth errors. |
| 2026-07-09 | WARNING | Hydration error on appointments page. PR #728 in progress. |
| 2026-07-10 | HEALTHY | 0 unresolved issues. Hydration error resolved. 7 PRs shipped. |
| **2026-07-11** | **WARNING** | **SHEAHAIRCARE-Y (hooks violation, signin). 1 build failure auto-recovered. 8 PRs shipped.** |

---

## Open Action Items

- [ ] **Fix SHEAHAIRCARE-Y** — hooks violation on `/consumer/signin`. Likely introduced by auth refactor (PRs #787–#790). Investigate hook call order in that flow.
- [ ] **Verify SHEAHAIRCARE-Z closed** — 1 residual event after PR #785 fix. Monitor for recurrence.
- [ ] **Add PostHog token** — appointment tracking still unavailable. 5 min task.
- [ ] **Investigate PR #789 build failure** — why did the copy-only change break the build? May indicate fragile build config.

---

_Generated: 2026-07-11 08:00 SAST_
_Sentry: fl4ll org. [View dashboard](https://fl4ll.sentry.io/issues/)_
_Vercel: [View project](https://vercel.com/mkmmogano-7968s-projects/sheahaircare)_
