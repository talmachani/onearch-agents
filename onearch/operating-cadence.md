# Operating Cadence

**Owner:** OneArch · **Version:** 1.0 · **Status:** Active

---

## Cadence Overview

| Cadence | Loop | Output |
|---------|------|--------|
| Daily | OneArch Morning Status | Status, decisions needed, work queue, monitoring summary |
| Weekly | Planning + backlog refinement | Prioritized work, updated initiatives |
| Per initiative | Discovery → RFC → decision → spec → implementation → release | Initiative artifacts |
| Per release | Release readiness review | Release packet + founder approval |
| Per incident | Incident command + postmortem | Incident report + corrective work |
| Continuous | Monitoring + SLO/error-budget tracking | Alerts, runbooks, founder escalations |

---

## Daily: Morning Status

**Trigger:** Daily (OneArch, Level 4 controlled autonomous, read-only)
**Output:** Morning status report to Tal

Structure:
```
# OneArch Morning Status — YYYY-MM-DD

## 1. Open Founder Decisions (action required)
[List of DACI decisions awaiting Tal's input, oldest first]

## 2. Work Queue (today's priority)
[Top 3–5 tasks across active initiatives, by P0→P1→P2 priority]

## 3. Monitoring Summary
[Key SLO/error-budget status, any alerts from last 24h]

## 4. Blocked Items
[Tasks blocked on external input or founder decision]

## 5. Completed Since Last Status
[Tasks/artifacts completed in the last 24h]
```

---

## Weekly: Planning + Backlog Refinement

**Trigger:** Weekly (Friday or Monday, Tal-driven)
**Agents:** OneArch (facilitates) · Product Manager · System Architect
**Output:** Updated prioritized backlog + any new DACI records

Steps:
1. OneArch generates a prioritization recommendation (1–5 scoring model).
2. Product Manager reviews backlog against current PRDs.
3. System Architect flags technical debt or architecture risks.
4. Tal makes final priority decisions.
5. OneArch updates the work queue and notifies relevant agents.

---

## Per Initiative: Discovery → Release

1. **Discovery** — PM generates discovery brief; Tal approves initiative.
2. **RFC** — System/Product Architect writes RFC; agents review; Tal approves key decisions.
3. **Spec** — Product Architect writes tech spec; BE/FE/DBA/DevOps/QA review.
4. **Implementation** — Agents execute in tasks; engineers open PRs; Tal approves merges.
5. **QA** — QA runs test plan; generates release-risk contract.
6. **Release** — OneArch assembles release packet; Tal approves; DevOps deploys via gate.

---

## Per Incident

**Severity levels:**
- **S1 (Critical):** Production down or data loss. Page Tal immediately.
- **S2 (High):** Major feature broken, degraded service. Alert Tal within 1 hour.
- **S3 (Medium):** Non-critical feature broken. Alert Tal in morning status.
- **S4 (Low):** Minor issue, workaround available. Track in backlog.

**Incident roles:**
- **Incident Commander:** DevOps (for infra) or Backend (for app)
- **Communications:** OneArch (to Tal)
- **Root cause:** System Architect
- **Postmortem:** System Architect + DevOps
