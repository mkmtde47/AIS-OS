# Sheahaircare Vault — Agent Operations Manual

## What This Is

A comprehensive **operations manual** that teaches an AI agent to diagnose and fix Sheahaircare issues without human judgment calls. The vault is your **durable operating system** for the product.

**Location:** `/Users/mkmtde/Workspace/vaults/Sheahaircare/`

## How It Works

### Agent Entry Point

1. Load `🤖 Agent/AGENT_BRIEFING.md` (2-min orientation)
2. Load `🤖 Agent/AGENT_MANIFEST.md` (what healthy looks like)
3. Load `🤖 Agent/AGENT_MEMORY.md` (facts & thresholds)
4. Load `🤖 Agent/AGENT_CHECKLIST.md` (run health checks)
5. If something fails → load matching `RUNBOOK_*.md`
6. Report in `🤖 Agent/Ops Logs/` (durable record)

### Running a Health Check

```bash
# Execute MongoDB health check
mongo sheahaircare < vaults/Sheahaircare/tools/health-checks/mongodb-health-check.mongodb.js

# Save result
Create file in: vaults/Sheahaircare/🤖 Agent/Ops Logs/Health Report - [DATE].md
```

### System Invariants

Five critical invariants — if any are violated, stop and investigate:

1. **MongoDB is the source of truth** — App reads from DB, not Paystack
2. **One active subscription per stylist** — Never 2+ simultaneously
3. **paystackCustomerId is unique** — No cross-customer contamination
4. **paystackSubscriptionCode is unique** — Prevents webhook misrouting
5. **Confirmed appointments have paystackReference** — No payment = no confirmation

## Access Required

### Read-Only (For Health Checks)

| System | Need | Setup |
|--------|------|-------|
| MongoDB | Read-only user | Create in Atlas; add to `.env` |
| Paystack | API read access | Get from dashboard; add to `.env` |
| Vercel logs | Viewer access | Already configured |

### With Approval (For Fixes)

| Action | Approval | Log |
|--------|----------|-----|
| Update DB records | MKM approval | Incident report |
| Refund payment | MKM approval | Paystack reference |
| Deploy | MKM approval | Deployment note |

## Critical Thresholds

**When to escalate:**

| Signal | Action |
|--------|--------|
| Webhook success rate < 95% | CRITICAL — Alert MKM |
| Orphaned appointments > 5 | CRITICAL — Alert MKM |
| Stuck pending subscriptions > 2 | HIGH — Investigate |
| Cross-customer data visible | CRITICAL — Isolate & alert |

## Runbooks Available

- `RUNBOOK_AUTH.md` — Login/OAuth failures
- `RUNBOOK_PAYSTACK.md` — Payment processing issues
- `RUNBOOK_SUBSCRIPTIONS.md` — Plan upgrades/downgrades
- `RUNBOOK_BOOKINGS.md` — Appointment issues
- `RUNBOOK_EMAIL.md` — Email delivery failures
- `RUNBOOK_DATABASE.md` — Connection/performance issues
- `RUNBOOK_WEBHOOKS.md` — Webhook delivery problems
- `RUNBOOK_DATA_CONSISTENCY.md` — Data integrity violations

## Quick Start Scenario

**"Stylist says they upgraded to Pro but features aren't unlocking"**

1. Load BRIEFING → routes to RUNBOOK_SUBSCRIPTIONS ✓
2. Load MANIFEST → understand upgrade flow ✓
3. Load AGENT_MEMORY → check INV-002 (one active sub) ✓
4. Run health check: Query 3 in AGENT_CHECKLIST ✓
5. Follow decision tree in RUNBOOK_SUBSCRIPTIONS ✓
6. Execute fix with MKM approval ✓
7. Log result in Ops Logs ✓

## Links

- [Vault Dashboard](file:///Users/mkmtde/Workspace/vaults/Sheahaircare/)
- [Agent Briefing](file:///Users/mkmtde/Workspace/vaults/Sheahaircare/🤖%20Agent/AGENT_BRIEFING.md)
- [Operations Logs](file:///Users/mkmtde/Workspace/vaults/Sheahaircare/🤖%20Agent/Ops%20Logs/)
- [Health Check Scripts](file:///Users/mkmtde/Workspace/vaults/Sheahaircare/🤖%20Agent/tools/health-checks/)

## Next: Credential Setup

To run live diagnostics, add to `.env`:

```
MONGODB_READONLY_URI=[connection string with read-only user]
PAYSTACK_API_KEY=[read-only key from dashboard]
```

Once set, the agent can run health checks autonomously.
