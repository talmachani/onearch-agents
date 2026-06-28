---
name: incident-response
description: Structured incident response runbook for OneArch. Use when a production health check fails, monitoring fires an alert, or Tal reports an outage. Classifies severity (S1-S4), executes the appropriate response, writes the incident log to incidents/, and triggers post-mortem if required.
---

# Incident Response Skill

## When to Use

Invoke when:
- A post-deploy health check fails (DevOps invokes immediately)
- Monitoring fires a production alert
- Tal reports a user-visible outage or data issue
- Asked to "open an incident" or "declare an incident"

## Steps

### 1. Classify severity

Determine the incident level using `onearch/operating-cadence.md` Per Incident criteria:

| Severity | Condition | Tal notification |
|----------|-----------|-----------------|
| S1 Critical | Production down or data loss | Page Tal immediately |
| S2 High | Major feature broken, degraded service | Alert Tal within 1 hour |
| S3 Medium | Non-critical feature broken, workaround exists | Alert Tal in next morning status |
| S4 Low | Minor issue, workaround available | No Tal notification — create Jira bug |

If severity is unclear, default to the higher level (err toward over-escalating to Tal).

### 2. Notify Tal

Per severity:

- **S1:** Stop all other work. Surface immediately to Tal with this message:
  > "S1 INCIDENT DECLARED — [what is down]. Impact: [who/what is affected]. Time of detection: [HH:MM UTC]. I am executing incident response now."

- **S2:** Alert within 1 hour:
  > "S2 incident detected — [what is broken]. Impact: [description]. I am investigating."

- **S3:** Include in next morning status run.

- **S4:** Create a Jira bug ticket; no immediate Tal notification.

### 3. Decide rollback

Ask: "Was this incident triggered by a recent deployment?"

- **Yes (deploy-related):** Execute rollback immediately without waiting for root cause analysis.
  ```bash
  # Revert to previous deployment
  argocd app set [app-name] --revision [previous-tag]
  argocd app sync [app-name]
  # Watch rollout
  kubectl rollout status deployment/[deployment-name] -n [namespace]
  ```
  Then execute migration rollback if migrations were included in the deploy:
  ```bash
  alembic downgrade -1  # repeat once per migration in reverse order
  ```
  After rollback: re-run the post-deploy health checklist. Report result to Tal.

- **No (not deploy-related):** Do NOT rollback (no point). Investigate root cause. Escalate to System Architect for diagnosis. Implement hotfix or mitigation.

### 4. Write the incident log

Create the file `incidents/INC-YYYYMMDD-NNN-[short-name].md` using the format below. Fill in everything you know now; Root Cause and Resolution are updated as investigation progresses.

Determine the sequence number NNN by running:
```bash
ls incidents/ | grep "INC-$(date +%Y%m%d)" | wc -l
```
Increment by 1 (start at 001 if none exist today).

**Incident log template:**

```markdown
# Incident: INC-YYYYMMDD-NNN — [Short Description]

**Severity:** S1 / S2 / S3 / S4
**Status:** Open
**Start:** YYYY-MM-DD HH:MM UTC
**Detected by:** Post-deploy health check / Monitoring alert / Tal report / User report
**Incident Commander:** DevOps (infra) / Backend Engineer (app) — [delete the inapplicable one]

## Impact

[Who and what is affected. Examples: "All users cannot log in", "NewsGraph search returns 500 for queries containing quotes", "~20% of article ingestion jobs failing"]

## Timeline

| Time (UTC) | Event |
|------------|-------|
| HH:MM | [Incident detected — how] |
| HH:MM | [Tal notified] |
| HH:MM | [First action taken] |
| HH:MM | [Rollback executed / Hotfix deployed / Mitigation applied] |
| HH:MM | [Service restored / Incident resolved] |

## Root Cause

[Update as investigation progresses. Leave "Under investigation" until known.]

Under investigation.

## Mitigation

[What stopped the bleeding — rollback, hotfix, feature flag, manual intervention]

## Resolution

[What fully resolved the incident. Leave "Pending" until resolved.]

Pending.

## Post-Mortem

| | |
|-|-|
| **Required** | Yes (S1/S2) / No (S3/S4) |
| **Due** | YYYY-MM-DD (24h after resolution for S1; 72h for S2) |
| **Owner** | System Architect |
| **Status** | Pending |

---
*Incident log maintained by DevOps. Root cause and postmortem owned by System Architect.*
```

### 5. Update the incident log as the incident progresses

As new information becomes available:
- Fill in the Root Cause when known
- Add timeline entries as actions are taken
- Update Status from Open → Mitigated (service restored but investigation ongoing) → Resolved
- Set Resolution when the incident is fully closed

### 6. Trigger post-mortem for S1/S2

After the incident is resolved:
- Update the incident log: Status → Resolved, Resolution → [what fixed it]
- Surface to System Architect: "S1/S2 incident [INC-ID] resolved. Post-mortem required by [due date]. Please schedule and assign."
- Create a Jira ticket for the post-mortem work item

## Rules

- S1 and S2 incidents MUST be surfaced to Tal before anything else — root cause analysis comes second.
- When in doubt about severity, escalate to the higher level. Over-escalation to Tal is safe; under-escalation is not.
- For deploy-related incidents, rollback first — investigate afterward. A rollback takes minutes; an investigation takes hours.
- Never close an incident without a populated Resolution section.
- S1/S2 post-mortems are not optional — they MUST be scheduled and owned by System Architect.
- Incident logs are permanent records — never delete or modify completed incident logs.
