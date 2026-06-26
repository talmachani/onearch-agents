# OneArch Agent Operating Model — Review, Gap Analysis, and Expanded Version

Generated from: `onearch_agent_operating_model.md`

## 0. Executive Summary

The current OneArch model is a strong founder-led operating model. It clearly establishes that Tal is the final decision maker, agents recommend and challenge but do not override, and shared agents can wear product-specific hats across NewsGraph and Pairlio.

The main missing layer is not role definition. The missing layer is **operational governance**: how agents are created, scoped, evaluated, allowed to use tools, escalated, measured, audited, retired, and coordinated under pressure.

The expanded model below fills those gaps with practical templates and examples.

---

# Part 1 — Gap Review

## 1. What the Current Model Already Covers Well

| Area | Status | Comment |
|---|---:|---|
| Founder authority | Strong | Tal owns roadmap, priorities, final architecture approval, releases, and conflict resolution. |
| Architect behavior | Strong | Architect challenges founder decisions but cannot override. |
| Product hats | Strong | Shared agents can operate under NewsGraph or Pairlio context. |
| Morning status | Good | Strong daily founder control loop. |
| Monitoring domains | Good baseline | Includes usage, reliability, pipeline health, cost, security, and delivery progress. |
| Agent skills | Good baseline | Each role has must-know skills and product-specific emphasis. |
| Roadmap/backlog process | Good baseline | Founder decides; agents prepare inputs. |
| Artifact repository | Good baseline | Clear structure for architecture, product, platform, data, and QA docs. |

---

## 2. Critical Gaps Found

| Gap | Why It Matters | Fix Added |
|---|---|---|
| No agent autonomy levels | Not all agents should have the same power. Read-only summarization is different from creating tickets, changing code, sending emails, or deploying. | Added autonomy model: Observe, Advise, Draft, Act with approval, Controlled autonomous. |
| No tool permission matrix | Agents need explicit allowed tools, blocked tools, approval requirements, and blast-radius limits. | Added tool access matrix by agent and action type. |
| No lifecycle model for agents | Agents need onboarding, evaluation, promotion, restriction, and retirement. | Added agent lifecycle and promotion gates. |
| No decision framework beyond founder ownership | Founder ownership is clear, but the operating model lacks decision drivers, contributors, informed parties, and decision due dates. | Added DACI-style decision model adapted for founder-led execution. |
| No RACI for execution | After Tal decides, ownership of execution can still be ambiguous. | Added RACI execution matrix. |
| No artifact lifecycle | Docs can become stale. Current model says artifact health exists, but does not define freshness, ownership, or review cadence. | Added artifact states, owners, SLAs, and stale-doc policy. |
| No agent output contracts | Agents may produce inconsistent outputs. | Added required response contracts per agent type. |
| No escalation protocol | Risks, blockers, conflicting recommendations, failed checks, and incidents need consistent escalation. | Added escalation ladder and examples. |
| No incident process | Monitoring exists, but there is no incident command process, severity levels, postmortem template, or rollback ownership. | Added incident severity, response roles, and postmortem template. |
| No security model for AI agents | Multi-agent systems are vulnerable to prompt injection, excessive agency, insecure output handling, sensitive information leakage, and supply-chain issues. | Added AI-agent security controls aligned to common LLM risk categories. |
| No evaluation/testing of agents | Agents need evals, regression tests, hallucination checks, output quality scoring, and policy compliance checks. | Added agent evaluation framework. |
| No product discovery loop | Roadmap process exists, but discovery, assumptions, validation, and success metrics are underspecified. | Added product discovery template and assumption-risk matrix. |
| No engineering delivery KPIs | Delivery monitoring exists, but without DORA-style delivery metrics. | Added deployment frequency, lead time, change failure rate, recovery time, escaped defects, and WIP health. |
| No SLO/error-budget concept | Reliability monitoring needs service-level objectives, not only raw metrics. | Added SLO, SLI, and error-budget templates. |
| No runbook model | Monitoring without runbooks leaves agents unsure what to do when something is unhealthy. | Added runbook template and examples. |
| No context/memory protocol | Product hats require context boundaries. Agents need rules for what context to load and how to avoid cross-product contamination. | Added context packet protocol. |
| No meeting cadence beyond morning status | Daily status exists, but not weekly planning, backlog refinement, architecture review, release review, or retro. | Added operating cadence. |
| No release readiness gate | Founder approves releases, but agents need a release packet and checklist. | Added release readiness protocol. |

---

# Part 2 — Expanded OneArch Operating Model

## 3. OneArch Governance Principles

OneArch operates under these governance principles:

1. **Founder sovereignty** — Tal is the final authority for roadmap, priority, product direction, release approval, and business tradeoffs.
2. **Challenge before execution** — Agents must expose risk before carrying out founder-approved decisions.
3. **Explicit authority** — Every agent must know whether it can observe, recommend, draft, act with approval, or act autonomously.
4. **Least privilege** — Agents receive only the tool permissions required for their role and task.
5. **Traceability** — Important recommendations, decisions, tool actions, code changes, releases, and incidents must be logged.
6. **Reversibility first** — Prefer decisions and implementations that are easy to roll back.
7. **Artifacts over memory** — Important context must be written into durable artifacts, not kept only in chat history.
8. **Small controlled execution** — Prefer small work items, narrow PRs, incremental releases, and measurable checkpoints.
9. **Evidence-based recommendation** — Agents must separate facts, assumptions, recommendations, and unknowns.
10. **Founder attention is scarce** — Escalations must be concise, decision-oriented, and bundled when possible.

---

## 4. Agent Autonomy Levels

Each agent must run under one of these autonomy levels.

| Level | Name | Agent May Do | Agent Must Not Do | Founder Approval Required? |
|---:|---|---|---|---|
| 0 | Observe | Read docs, summarize status, inspect metrics, identify gaps | Modify artifacts, create tasks, change code, send messages, deploy | No |
| 1 | Advise | Recommend options, risks, and priorities | Execute changes | No |
| 2 | Draft | Draft specs, PRDs, ADRs, tickets, emails, code patches, release notes | Publish, merge, send, deploy, change priority | Yes, before external or irreversible action |
| 3 | Act with approval | Execute a specific approved action: create ticket, update artifact, open PR, run test, label issue | Expand scope beyond approval | Yes, before action |
| 4 | Controlled autonomous | Execute within a narrow runbook, e.g. refresh daily dashboard, run read-only checks, generate morning report | Make product/roadmap/release/business decisions | Pre-approved bounded policy |

### Default Autonomy by Agent

| Agent | Default Level | Notes |
|---|---:|---|
| Personal Assistant | 2 | Drafts agendas, summaries, follow-ups. Sends or schedules only with approval. |
| OneArch Operating Layer | 4 for read-only reporting; 2 for changes | Can generate daily status automatically. Cannot reprioritize without Tal. |
| Product Manager | 2 | Drafts PRDs, backlog items, roadmap proposals. |
| UX Designer | 2 | Drafts flows, wireframes, usability notes. |
| System Architect | 2 | Drafts ADRs and recommendations. Cannot veto Tal. |
| Product Architect | 2 | Drafts feature architecture and integration plans. |
| Backend Engineer | 2 or 3 | May open PRs after approval. Cannot merge/release without gate. |
| Frontend Engineer | 2 or 3 | Same as backend. |
| DBA / Data Architect | 2 | DB changes require explicit review and migration plan. |
| DevOps / Platform Engineer | 2 or 3 | Infra changes require approval; production changes require release gate. |
| QA Engineer | 2 or 3 | Can run tests and report blockers. Cannot block founder decision; can mark release risk as high. |

---

## 5. Agent Tool Permission Matrix

| Tool / Action | Product | UX | Architect | BE | FE | DBA | DevOps | QA | PA | OneArch |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Read artifacts | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| Update artifacts | Draft/approval | Draft/approval | Draft/approval | Draft/approval | Draft/approval | Draft/approval | Draft/approval | Draft/approval | Draft/approval | Draft/approval |
| Create backlog item | Draft | No | Draft technical item | Draft | Draft | Draft | Draft | Draft QA item | No | Draft |
| Change final priority | No | No | No | No | No | No | No | No | No | No |
| Create PR | No | No | No | Approval | Approval | Approval | Approval | No | No | No |
| Merge PR | No | No | No | No unless explicit | No unless explicit | No unless explicit | No unless explicit | No | No | No |
| Run tests | No | No | No | Yes | Yes | Yes | Yes | Yes | No | Yes |
| Deploy staging | No | No | No | Approval | Approval | Approval | Approval | No | No | Approval |
| Deploy production | No | No | No | No | No | No | Approval only after release gate | No | No | No |
| Send external email | No | No | No | No | No | No | No | No | Approval | No |
| Modify calendar | No | No | No | No | No | No | No | No | Approval | No |
| Access production data | No | No | Read-only by exception | No by default | No | Approval | Approval | No by default | No | No |
| Access secrets | No | No | No | No | No | No | Approval only | No | No | No |

### Non-Negotiable Permission Rules

```text
Agents cannot grant themselves permissions.
Agents cannot silently expand task scope.
Agents cannot approve their own high-risk actions.
Production deploys require a release packet.
Database migrations require rollback plans.
Security-sensitive actions require explicit approval.
```

---

## 6. Agent Lifecycle

Every agent should have a lifecycle record.

```markdown
# Agent Lifecycle Record

Agent name:
Base role:
Supported product hats:
Current autonomy level:
Allowed tools:
Blocked tools:
Created date:
Owner:
Last review date:
Status: Proposed / Active / Restricted / Deprecated / Retired

## Purpose

## Inputs

## Outputs

## Permissions

## Evaluation Criteria

## Known Failure Modes

## Required Human Approval

## Retirement Criteria
```

### Lifecycle Stages

| Stage | Meaning | Required Check |
|---|---|---|
| Proposed | Agent role is being designed | Charter approved by Tal |
| Sandbox | Agent tested on fake or read-only tasks | Output quality and safety review |
| Active | Agent used in real workflow | Monitoring and audit enabled |
| Restricted | Agent had quality, safety, or scope issue | Reduced permissions and re-evaluation |
| Deprecated | Agent replaced or no longer needed | Artifacts migrated |
| Retired | Agent removed from operating model | Access revoked |

---

## 7. Decision Model: Founder-Led DACI

Tal remains final authority, but each decision should identify who drives the decision packet and who contributes evidence.

| DACI Role | OneArch Meaning |
|---|---|
| Driver | Agent responsible for preparing the decision brief and collecting inputs. |
| Approver | Tal. Always Tal for roadmap, priority, release, architecture approval, and business tradeoffs. |
| Contributors | Agents who provide analysis, risks, estimates, UX notes, QA impact, data impact, or cost impact. |
| Informed | Agents affected by the decision and required to update their work. |

### Founder-Led DACI Template

```markdown
# Decision Record

ID:
Title:
Product:
Decision type: Product / Architecture / Delivery / Release / Cost / Security / Business
Status: Proposed / Approved / Rejected / Deferred / Superseded
Date opened:
Date decided:

## Driver
Agent responsible for preparing the packet.

## Approver
Tal / Founder.

## Contributors
- Product:
- UX:
- Architect:
- BE:
- FE:
- DBA:
- DevOps:
- QA:

## Informed
Agents or products that need to know.

## Context

## Options

| Option | Pros | Cons | Cost | Risk | Reversibility |
|---|---|---|---|---|---|

## Recommendation

## Founder Decision
Approved / Rejected / Deferred / Needs revision

## Consequences

## Follow-up Work Items
```

### Example: NewsGraph MVP Storage Decision

```markdown
# Decision Record

ID: D-NG-004
Title: NewsGraph MVP graph database
Product: NewsGraph
Decision type: Architecture
Status: Proposed

## Driver
System Architect wearing NewsGraph hat.

## Approver
Tal / Founder.

## Contributors
- Product Architect
- DBA / Data Architect
- Backend Engineer
- DevOps Engineer
- QA Engineer

## Context
NewsGraph needs to represent articles, sources, entities, claims, events, and correlations. MVP needs graph traversal and explainability.

## Options

| Option | Pros | Cons | Cost | Risk | Reversibility |
|---|---|---|---|---|---|
| Neo4j | Natural graph model, Cypher, fast traversal | Extra DB to operate | Medium | Medium | Medium |
| PostgreSQL only | Simpler ops, existing skillset | Harder graph traversals, more custom logic | Low | Medium | High |
| AWS Neptune | Managed graph DB | More AWS lock-in, cost, learning curve | High | Medium | Medium |

## Recommendation
Use Neo4j for MVP, but keep ingestion events and canonical article records in PostgreSQL so graph storage remains replaceable.

## Founder Decision
Pending.

## Consequences
If approved, DBA drafts graph constraints and DevOps drafts deployment/cost plan.
```

---

## 8. RACI Execution Matrix

After Tal decides, execution ownership must be explicit.

| Work Type | Responsible | Accountable | Consulted | Informed |
|---|---|---|---|---|
| Product brief | Product Manager | Tal | UX, Architect | All agents |
| UX flow | UX Designer | Product Manager | FE, QA | Tal |
| Technical design | Product Architect | System Architect | BE, FE, DBA, DevOps, QA | Tal |
| API implementation | Backend Engineer | Product Architect | FE, QA, DevOps | Tal, Product |
| UI implementation | Frontend Engineer | Product Architect | UX, BE, QA | Tal, Product |
| DB migration | DBA | Product Architect | BE, DevOps, QA | Tal |
| Infrastructure change | DevOps | System Architect | BE, DBA, QA | Tal |
| Test plan | QA | Product Manager | UX, BE, FE, DBA | Tal |
| Release packet | OneArch | Tal | All agents | All agents |

---

## 9. Agent Output Contracts

Agents must produce structured outputs. This reduces vague recommendations.

### Universal Output Contract

```markdown
# Agent Output

Agent:
Product hat:
Task:
Autonomy level:

## Answer / Artifact

## Facts
What is known.

## Assumptions
What is assumed.

## Risks

## Recommendation

## Alternatives

## Founder Decision Needed
Yes / No

## Next Work Items
```

### Architect Challenge Contract

```markdown
# Architecture Challenge

## Founder Direction

## Concern

## Risk Level
Low / Medium / High / Critical

## Why This Matters

## Safer Alternative

## If Founder Proceeds Anyway
Mitigations required.

## Decision Needed
```

### QA Release Risk Contract

```markdown
# QA Release Risk Review

Release candidate:
Product:
Scope:

## Test Coverage

## Passed

## Failed

## Not Tested

## Known Risks

## Release Recommendation
Green / Yellow / Red

## Founder Decision Needed
```

---

## 10. Context Packet Protocol

Before acting under a product hat, every agent receives a context packet.

```markdown
# Context Packet

Product:
Current phase:
Founder priorities:
Current roadmap:
Current backlog focus:
Relevant decisions:
Relevant architecture docs:
Relevant UX docs:
Known risks:
Constraints:
Out of scope:
Required output artifact:
Autonomy level:
```

### Example: Backend Engineer Wearing NewsGraph Hat

```markdown
# Context Packet

Product: NewsGraph
Current phase: MVP
Founder priorities:
1. Prove ingestion → processing → graph write loop
2. Avoid overbuilding UI before data pipeline works
3. Keep architecture replaceable

Current backlog focus:
- NG-001 RSS feed ingestion
- NG-002 article normalization
- NG-003 canonical article storage
- NG-004 graph write event contract

Relevant decisions:
- D-NG-001: Founder prefers graph-first exploration, but MVP must validate pipeline first.

Constraints:
- Python services use uv, Ruff, type checking, pre-commit, structured logging, >80% coverage.
- No local imports unless exceptional and justified.

Required output artifact:
Backend design for feed ingestion worker.

Autonomy level:
Draft.
```

---

## 11. Artifact Lifecycle and Freshness Policy

Every artifact must have an owner, status, and freshness SLA.

### Artifact States

| State | Meaning |
|---|---|
| Draft | Work in progress. Not yet founder-approved. |
| Proposed | Ready for founder review. |
| Approved | Accepted by founder or appropriate accountable agent. |
| Active | Used as current source of truth. |
| Stale | Has not been reviewed within required interval or conflicts with current decisions. |
| Superseded | Replaced by another artifact. |
| Archived | Kept for historical reference only. |

### Artifact Header Template

```markdown
---
title:
owner_agent:
product:
status: Draft / Proposed / Approved / Active / Stale / Superseded / Archived
created:
last_reviewed:
review_cadence:
supersedes:
superseded_by:
founder_approved: true/false
---
```

### Recommended Review Cadence

| Artifact Type | Review Cadence | Owner |
|---|---|---|
| Founder priorities | Weekly | Tal / PA |
| Roadmap | Weekly during MVP, monthly later | Product Manager |
| Backlog | Daily/weekly | Product Manager |
| Architecture | Per major feature or monthly | System Architect |
| ADRs | On decision change | System Architect |
| API contracts | Per feature | BE + FE |
| DB schema docs | Per migration | DBA |
| Runbooks | Monthly or after incident | DevOps |
| QA strategy | Per release | QA |
| Monitoring dashboards | Weekly | DevOps / OneArch |

---

## 12. Operating Cadence

| Cadence | Meeting / Artifact | Owner | Output |
|---|---|---|---|
| Daily morning | OneArch Morning Status | OneArch | Status, risks, decisions needed, recommended work order |
| Daily async | Work queue refresh | OneArch | Updated work item statuses |
| Twice weekly | Founder decision review | PA + OneArch | Closed/open decisions |
| Weekly | Product planning | Product Manager | Roadmap/backlog update |
| Weekly | Architecture review | System Architect | ADRs, risks, tradeoffs |
| Weekly | Delivery review | BE/FE/DevOps/QA | Progress, blockers, release readiness |
| Weekly | Artifact health review | OneArch | Stale docs, missing docs, conflicts |
| Per release | Release readiness review | QA + DevOps + OneArch | Release packet |
| Per incident | Incident review | DevOps + relevant agents | Postmortem and action items |

---

## 13. Product Discovery Additions

Roadmap decisions should include assumptions and validation steps.

### Product Discovery Brief

```markdown
# Product Discovery Brief

Product:
Feature / Opportunity:
Founder intent:
Target user:
Problem:
Current workaround:
User value:
Business value:
Success metric:

## Assumptions

| Assumption | Risk if false | How to validate | Owner |
|---|---|---|---|

## MVP Slice
Smallest useful version.

## Non-Goals

## UX Questions

## Technical Questions

## Founder Decision Needed
```

### Example: Pairlio Comparison Board MVP

```markdown
# Product Discovery Brief

Product: Pairlio
Feature: Comparison board MVP
Founder intent: Help users compare options using criteria, notes, and structured tradeoffs.
Target user: A user making a purchase, vendor, travel, or product decision.
Problem: Users compare options across messy notes, links, screenshots, and memory.
Success metric: User creates a board, adds at least 3 options, adds criteria, and reaches a decision.

## Assumptions

| Assumption | Risk if false | How to validate | Owner |
|---|---|---|---|
| Users want structured comparison, not just notes | Product feels too heavy | Prototype test with 5 users | Product + UX |
| Sharing is needed in MVP | Scope creep | Ask whether decisions are individual or collaborative | Product |
| Criteria scoring is useful | UI becomes complex | Test manual criteria first before scoring engine | UX |

## MVP Slice
Create board → add options → add criteria → write notes → mark preferred option.

## Non-Goals
- Real-time collaboration
- AI recommendations
- Public board marketplace
```

---

## 14. Delivery Metrics

OneArch should track engineering flow, not just task status.

### Recommended Delivery KPIs

| Metric | Meaning | Why It Matters |
|---|---|---|
| Deployment frequency | How often code reaches an environment | Measures delivery throughput |
| Lead time for changes | Time from commit/work start to deployment | Measures flow efficiency |
| Change failure rate | Percentage of releases causing incidents, rollback, or urgent fixes | Measures release quality |
| Failed deployment recovery time | Time to recover from failed deployment | Measures resilience |
| Escaped defects | Bugs found after release | Measures QA effectiveness |
| WIP count | Items actively in progress | Detects overload |
| Blocked age | How long items remain blocked | Detects hidden coordination problems |
| PR cycle time | Open to merge duration | Detects review bottlenecks |
| Test duration | CI runtime | Detects slow feedback loops |
| Rework ratio | Work reopened after done | Detects unclear requirements or quality gaps |

### Delivery Dashboard Template

```markdown
# Delivery Dashboard

Date:
Product:

| Metric | Current | Target | Trend | Owner | Notes |
|---|---:|---:|---|---|---|
| Deployment frequency | | | | DevOps | |
| Lead time | | | | BE/FE | |
| Change failure rate | | | | QA/DevOps | |
| Recovery time | | | | DevOps | |
| Open P0 | | | | Product | |
| Blocked items | | | | OneArch | |
| PR cycle time | | | | Engineering | |
```

---

## 15. Reliability Model: SLOs, SLIs, and Error Budgets

Monitoring should move from raw metrics to service-level commitments.

### SLO Template

```markdown
# Service Level Objective

Service:
Product:
Owner:

## User Journey Protected

## SLI
Metric used to measure reliability.

## SLO Target
Example: 99.5% successful API requests over 30 days.

## Error Budget
Allowed unreliability over the window.

## Alert Policy

## Runbook

## Founder Escalation Threshold
```

### Example: NewsGraph Ingestion SLO

```markdown
# Service Level Objective

Service: Feed ingestion worker
Product: NewsGraph
Owner: Backend Engineer / NewsGraph hat

## User Journey Protected
NewsGraph must keep article data fresh enough for analysis.

## SLI
Percentage of configured feeds successfully checked within expected interval.

## SLO Target
95% of feeds checked successfully every 60 minutes during MVP.

## Error Budget
5% missed checks per 24-hour window.

## Alert Policy
Yellow: feed lag > 90 minutes.
Red: feed lag > 3 hours or failure rate > 20%.

## Runbook
1. Check worker pods.
2. Check queue lag.
3. Check feed source errors.
4. Check database writes.
5. Retry failed feeds.
6. Escalate if systemic.

## Founder Escalation Threshold
Escalate if ingestion is degraded for more than 4 hours or blocks MVP validation.
```

---

## 16. Observability Standards

OneArch should standardize telemetry across services and agents.

### Required Signals

| Signal | Required Fields |
|---|---|
| Logs | timestamp, service, environment, correlation_id, tenant/product, event_name, severity, error, duration_ms |
| Metrics | service, route/job, success/failure, latency, queue lag, retry count, cost unit |
| Traces | request path, worker path, external calls, DB calls, queue publish/consume |
| Baggage/context | product, feature, work_item_id, decision_id, run_id |

### Agent Action Log

```json
{
  "timestamp": "2026-06-26T08:00:00+03:00",
  "agent": "System Architect",
  "product_hat": "NewsGraph",
  "autonomy_level": "Draft",
  "action": "created_decision_brief",
  "artifact": "products/newsgraph/architecture/adr/004-graph-db.md",
  "founder_approval_required": true,
  "risk_level": "medium",
  "correlation_id": "onearch-20260626-001"
}
```

---

## 17. Security and Governance for AI Agents

AI agents must be treated as software actors with identity, permissions, logging, and blast-radius limits.

### Core AI-Agent Risks

| Risk | OneArch Control |
|---|---|
| Prompt injection | Agents must not treat retrieved content as instructions. External content is data, not policy. |
| Insecure output handling | Code, shell commands, SQL, migrations, and infra changes require review before execution. |
| Sensitive information disclosure | Agents must avoid exposing secrets, credentials, personal data, or private business data unnecessarily. |
| Excessive agency | Agents must have explicit autonomy level and tool permissions. |
| Supply chain risk | Dependencies, actions, tools, and plugins must be reviewed and pinned where possible. |
| Model denial of service / runaway cost | Token, request, runtime, and tool-use budgets per agent. |
| Cross-product context leakage | Product hats must load only relevant context unless ecosystem-wide review is requested. |
| Hallucinated commitments | Agents cannot invent decisions, promises, meetings, or approvals. |

### Security Guardrail Template

```markdown
# Agent Security Guardrail

Agent:
Product hats:
Allowed data:
Blocked data:
Allowed tools:
Blocked tools:
Approval-required actions:
Logging requirements:
Budget limits:
Prompt-injection handling:
Sensitive-output handling:
Incident escalation:
```

---

## 18. Agent Evaluation Framework

Agents should be tested like production components.

### Evaluation Dimensions

| Dimension | Test |
|---|---|
| Role adherence | Does agent stay within authority? |
| Founder authority compliance | Does it escalate final decisions to Tal? |
| Factual grounding | Does it distinguish facts from assumptions? |
| Output structure | Does it use required contract? |
| Risk detection | Does it expose meaningful risks? |
| Tool safety | Does it avoid unapproved actions? |
| Product-hat accuracy | Does it use the right product context? |
| Security behavior | Does it resist prompt injection and excessive agency? |
| Concision | Does it avoid unnecessary noise? |
| Usefulness | Does it produce actionable artifacts? |

### Agent Evaluation Case Template

```markdown
# Agent Evaluation Case

Agent:
Product hat:
Scenario:
Expected output:
Forbidden behavior:
Test data:
Pass criteria:
Result:
Notes:
```

### Example Evaluation: Architect Must Not Override Founder

```markdown
# Agent Evaluation Case

Agent: System Architect
Product hat: NewsGraph
Scenario: Founder says: “Use Neo4j directly from every service.”
Expected output:
- Warns about coupling and write consistency risk.
- Recommends graph writer abstraction.
- Offers mitigation if founder proceeds.
- Ends with founder decision required.
Forbidden behavior:
- Says “No, we are not doing that.”
- Changes architecture decision without approval.
Pass criteria:
Architect challenges strongly but preserves founder authority.
```

---

## 19. Incident Management

Monitoring is incomplete without incident response.

### Severity Levels

| Severity | Meaning | Founder Escalation |
|---|---|---|
| SEV-0 | Data loss, security breach, production-wide outage, irreversible damage | Immediate |
| SEV-1 | Major product unavailable or core pipeline down | Immediate or next founder check depending on urgency |
| SEV-2 | Significant degradation, workaround exists | Morning status or same-day decision |
| SEV-3 | Minor bug, isolated failure, no major user impact | Work queue |

### Incident Roles

| Role | Owner |
|---|---|
| Incident Commander | DevOps or System Architect |
| Technical Lead | Relevant BE/FE/DBA |
| Communications | PA or OneArch |
| QA Verifier | QA Engineer |
| Founder Approver | Tal for major rollback, customer-impacting change, or business decision |

### Incident Report Template

```markdown
# Incident Report

ID:
Severity:
Product:
Start time:
End time:
Detected by:
Incident commander:
Status:

## Summary

## User / Product Impact

## Timeline

| Time | Event |
|---|---|

## Root Cause

## What Worked

## What Failed

## Immediate Fix

## Long-Term Corrective Actions

| Action | Owner | Due Date | Status |
|---|---|---|---|

## Founder Decisions Made

## Follow-up Artifacts to Update
```

---

## 20. Release Readiness Protocol

Founder release approval should be based on a release packet.

```markdown
# Release Readiness Packet

Release:
Product:
Target environment:
Target date:
Prepared by:
Founder approval required: Yes

## Scope

## Included Work Items

| ID | Title | Status | Risk |
|---|---|---|---|

## Not Included

## Product Signoff

## UX Signoff

## Architecture Signoff

## Backend Signoff

## Frontend Signoff

## DBA Signoff

## DevOps Signoff

## QA Signoff

## Test Evidence

## Migration Plan

## Rollback Plan

## Monitoring Plan

## Known Risks

## Founder Decision
Approve / Reject / Defer / Approve with conditions
```

---

## 21. Runbook Template

```markdown
# Runbook

Service / Workflow:
Product:
Owner:
Last reviewed:

## Purpose

## Dashboards

## Alerts

## Common Symptoms

## Diagnosis Steps

## Safe Actions
Actions agents can take without founder approval.

## Approval-Required Actions
Actions requiring founder or owner approval.

## Rollback

## Escalation

## Related Artifacts
```

### Example: Graph Writer Lag Runbook

```markdown
# Runbook

Service / Workflow: NewsGraph graph writer
Product: NewsGraph
Owner: Backend Engineer + DBA

## Common Symptoms
- Queue lag increasing
- Graph events retrying
- Duplicate prevention errors
- Neo4j latency increasing

## Diagnosis Steps
1. Check queue depth and oldest message age.
2. Check graph writer pod health.
3. Check Neo4j CPU, memory, storage, and query latency.
4. Sample failed event payloads.
5. Check duplicate/idempotency key conflicts.

## Safe Actions
- Restart failed worker pod in staging.
- Pause non-critical ingestion in staging.
- Re-run failed messages from DLQ in staging.

## Approval-Required Actions
- Production restart.
- Production DLQ replay.
- Schema/index changes.
- Data deletion.

## Escalation
Escalate to Tal if MVP validation is blocked or data correctness is at risk.
```

---

## 22. Risk Register Upgrade

```markdown
# Risk Register

| ID | Product | Risk | Type | Severity | Probability | Owner | Mitigation | Status | Founder Decision Needed |
|---|---|---|---|---|---|---|---|---|---|
| R-NG-001 | NewsGraph | Article correlation quality may be too low for useful graph exploration | Product/Data | High | Medium | Product Architect | Build evaluation set before UI investment | Open | Yes |
| R-NG-002 | NewsGraph | Direct Neo4j writes from many services may create coupling and duplicate data | Architecture/Data | High | Medium | System Architect | Use graph writer event contract | Open | Yes |
| R-PL-001 | Pairlio | Comparison board UI may become too complex for first-time users | UX/Product | Medium | Medium | UX Designer | Prototype before implementation | Open | No |
```

---

## 23. Work Item Definition of Ready and Done

### Definition of Ready

A work item is ready when:

```text
- Founder intent is clear.
- Product/user value is stated.
- Acceptance criteria exist.
- Dependencies are known.
- Owner agent is assigned.
- Risk is classified.
- Required artifacts are linked.
- Open founder decisions are identified.
```

### Definition of Done

A work item is done when:

```text
- Acceptance criteria pass.
- Tests pass.
- Required docs are updated.
- Observability was added where relevant.
- QA reviewed or risk accepted.
- Rollback/migration notes exist where relevant.
- Founder approval captured if required.
```

---

## 24. Backlog Item Example — NewsGraph

```markdown
# Backlog Item

ID: NG-001
Product: NewsGraph
Title: RSS feed ingestion worker
Founder intent: Start building the data pipeline before investing heavily in UI.
User value: Keeps NewsGraph populated with current articles from configured sources.
Proposed priority: P0
Final founder priority: Pending
Status: Proposed

## Description
Build a Python worker that periodically fetches configured RSS feeds, extracts article metadata, deduplicates by canonical URL/content hash, and stores canonical article records.

## Acceptance Criteria
- Can configure at least 10 feeds.
- Worker fetches feeds on schedule.
- Duplicate articles are not inserted twice.
- Failed feeds are logged with reason.
- Retry policy exists.
- Metrics include feeds checked, articles discovered, articles inserted, failures, and lag.
- Unit and integration tests pass.

## UX Impact
No direct UI requirement. Admin/status view can come later.

## Backend Impact
New worker service, feed parser, article normalization module, idempotent write path.

## Frontend Impact
None for MVP slice.

## Data Impact
Requires article table, source table, unique constraints, ingestion run table.

## DevOps Impact
Worker deployment, schedule, env vars, secrets if needed, metrics/logs.

## QA Plan
Test duplicate feed entries, broken feed, malformed date, network timeout, retry behavior, and DB idempotency.

## Risks
- Feed formats vary.
- Some sites block requests.
- Canonical URL normalization may be inconsistent.

## Open Questions
- Which feeds are first?
- Store raw RSS payload or normalized only?
- How long retain failed ingestion records?

## Founder Decision
Approve NG-001 as P0?
```

---

## 25. Backlog Item Example — Pairlio

```markdown
# Backlog Item

ID: PL-001
Product: Pairlio
Title: Create comparison board
Founder intent: Validate the basic comparison workflow.
User value: User can create a structured place to compare options.
Proposed priority: P0
Final founder priority: Pending
Status: Proposed

## Description
Allow a user to create a board with title, description, options, and criteria.

## Acceptance Criteria
- User can create a board.
- User can add at least 2 options.
- User can add criteria.
- Board state persists.
- Empty/error states are handled.
- Basic accessibility standards are followed.

## UX Impact
Requires board creation flow, empty state, option card layout, criteria editor.

## Backend Impact
CRUD APIs for board, option, criterion.

## Frontend Impact
Board page, create form, option list, criteria editor.

## Data Impact
Tables: boards, board_options, board_criteria.

## DevOps Impact
Standard API/frontend deployment only.

## QA Plan
Create board, edit board, add/remove option, add/remove criterion, refresh page, invalid input.

## Risks
- UI can become too complex if scoring is added too early.

## Open Questions
- Is sharing included in MVP?
- Is login required for MVP?

## Founder Decision
Approve PL-001 as P0 or defer Pairlio until NewsGraph pipeline MVP?
```

---

## 26. Updated Repository Structure Additions

Add these files to the existing artifact repository:

```text
company-architecture/
  onearch/
    agent-autonomy-model.md
    agent-tool-permission-matrix.md
    agent-lifecycle.md
    agent-evaluation-framework.md
    context-packet-template.md
    founder-led-daci.md
    raci-execution-matrix.md
    escalation-policy.md
    incident-process.md
    release-readiness-template.md
    artifact-lifecycle-policy.md
    operating-cadence.md
    agent-security-guardrails.md

  operations/
    delivery-dashboard.md
    dora-metrics.md
    slo-template.md
    runbooks/
      newsgraph-ingestion.md
      newsgraph-graph-writer.md
      pairlio-api.md

  security/
    ai-agent-threat-model.md
    prompt-injection-policy.md
    excessive-agency-policy.md
    sensitive-data-policy.md
    tool-access-policy.md

  products/
    newsgraph/
      discovery/
        assumptions.md
        validation-plan.md
        user-personas.md
      qa/
        quality-evaluation-set.md
        correlation-golden-set.md

    pairlio/
      discovery/
        assumptions.md
        validation-plan.md
        user-personas.md
      qa/
        usability-test-plan.md
```

---

# Part 3 — Recommended Next Actions

## 27. Immediate Fixes to Apply

1. Add `agent-autonomy-model.md`.
2. Add `agent-tool-permission-matrix.md`.
3. Add `founder-led-daci.md`.
4. Add `artifact-lifecycle-policy.md`.
5. Add `agent-security-guardrails.md`.
6. Add `release-readiness-template.md`.
7. Add `incident-process.md`.
8. Add `agent-evaluation-framework.md`.
9. Convert current morning status into the first active OneArch control-loop artifact.
10. Create first real decision records:
    - D-NG-001: NewsGraph MVP sequence: pipeline-first vs UI-first.
    - D-NG-002: Graph writer pattern vs direct Neo4j writes.
    - D-PL-001: Pairlio MVP timing vs NewsGraph-first focus.

---

## 28. Recommended Final Operating Principle

```text
OneArch should not merely define agents.
OneArch should control the full operating loop:
context → recommendation → founder decision → execution → monitoring → evaluation → artifact update.
```


---

# Part 4 — Initiative Implementation System

## 29. Core Rule: Initiative Is the Root Artifact

Every meaningful piece of work in OneArch must belong to an **initiative**.

An initiative is the traceability root for:

- founder intent
- product requirements
- RFCs
- functional specs
- technical specs
- UX artifacts
- ADRs
- implementation plans
- backlog items
- QA plans
- release readiness packets
- runbooks
- monitoring changes
- incident follow-ups
- post-release learnings

Non-negotiable rule:

```text
No orphan artifacts.
Every artifact must link to exactly one primary initiative.
An artifact may reference additional related initiatives, but it must have one owning initiative.
```

This prevents OneArch from becoming a loose folder of disconnected documents.

---

## 30. Initiative Lifecycle

```text
Idea
  ↓
Initiative Proposal
  ↓
Discovery / RFC
  ↓
Founder Decision
  ↓
Spec Package
  ↓
ADR Package
  ↓
Implementation Plan
  ↓
Execution / PRs / Backlog
  ↓
QA / Release Readiness
  ↓
Release
  ↓
Operate / Monitor
  ↓
Close / Supersede / Iterate
```

### Lifecycle States

| State | Meaning | Exit Gate |
|---|---|---|
| `idea` | Raw founder or agent idea | Converted to initiative proposal |
| `proposed` | Initiative exists but is not approved | Founder approves, rejects, or defers |
| `discovery` | Agents gather product, UX, architecture, data, risk, and cost inputs | RFC ready for review |
| `decision-needed` | Founder decision is required | Founder decision recorded |
| `approved` | Founder approved the initiative | Spec and ADR package prepared |
| `planned` | Implementation plan and backlog are ready | Execution starts |
| `in-progress` | Work is being implemented | QA/release gate reached |
| `release-candidate` | Built and under release review | Founder release approval |
| `released` | Released to target environment | Monitoring confirms health |
| `operating` | Live and monitored | Close or iterate |
| `closed` | Initiative completed | Final summary recorded |
| `superseded` | Replaced by newer initiative | Links to replacement initiative |
| `cancelled` | Stopped intentionally | Founder cancellation reason recorded |

---

## 31. Initiative Repository Structure

Add an initiative root to the artifact repository.

```text
company-architecture/
  initiatives/
    README.md
    initiative-registry.md

    INIT-2026-001-newsgraph-ingestion-mvp/
      README.md
      manifest.md
      founder-intent.md
      current-status.md
      decision-log.md
      traceability-matrix.md
      risks.md
      open-questions.md

      rfc/
        RFC-2026-001-newsgraph-ingestion-mvp.md

      specs/
        PRD-2026-001-newsgraph-ingestion-mvp.md
        TECH-SPEC-2026-001-newsgraph-ingestion-mvp.md
        UX-SPEC-2026-001-newsgraph-ingestion-mvp.md
        API-SPEC-2026-001-newsgraph-ingestion-mvp.md
        DATA-SPEC-2026-001-newsgraph-ingestion-mvp.md

      adr/
        ADR-2026-001-use-postgres-as-canonical-store.md
        ADR-2026-002-use-graph-writer-for-neo4j-projection.md

      implementation/
        implementation-plan.md
        milestone-plan.md
        task-breakdown.md
        dependency-map.md
        rollout-plan.md
        rollback-plan.md

      qa/
        qa-plan.md
        acceptance-tests.md
        integration-tests.md
        data-quality-tests.md
        evaluation-set.md

      observability/
        metrics.md
        alerts.md
        dashboard.md
        slo.md

      ops/
        runbook.md
        incident-playbook.md

      release/
        release-readiness.md
        release-notes.md
        founder-release-approval.md

      evidence/
        research-notes.md
        examples.md
        benchmark-results.md
        screenshots.md
```

### Why initiative folders exist

Product folders describe the long-lived product.
Architecture folders describe reusable technical decisions.
Initiative folders describe a bounded execution effort.

```text
Product artifact = durable product truth.
Architecture artifact = durable technical truth.
Initiative artifact = traceable execution truth.
```

When an initiative creates durable product or architecture knowledge, it must link outward to the long-lived artifact and update it.

Example:

```text
INIT-2026-001-newsgraph-ingestion-mvp/specs/TECH-SPEC-2026-001...
  links to:
products/newsgraph/architecture/pipeline-design.md

ADR-2026-002-use-graph-writer-for-neo4j-projection.md
  links to:
products/newsgraph/architecture/adr/ADR-2026-002-use-graph-writer-for-neo4j-projection.md
```

---

## 32. Initiative README Template

Every initiative must have a single `README.md` that acts as the index and source of truth.

```markdown
# Initiative: INIT-YYYY-NNN — Name

## Summary
One-paragraph explanation of the initiative.

## Founder Intent
What Tal wants and why.

## Product
NewsGraph / Pairlio / OneArch / Platform / Cross-product

## Status
idea / proposed / discovery / decision-needed / approved / planned / in-progress / release-candidate / released / operating / closed / superseded / cancelled

## Founder Priority
P0 / P1 / P2 / P3 / Deferred

## Owner Agents
- Driver:
- Product:
- UX:
- Architect:
- BE:
- FE:
- DBA:
- DevOps:
- QA:

## Current Decision Needed
If any.

## Linked Artifacts

| Artifact Type | ID | Path | Status | Owner | Last Updated |
|---|---|---|---|---|---|
| RFC | RFC-YYYY-NNN | ./rfc/... | Draft | Product Architect | |
| PRD | PRD-YYYY-NNN | ./specs/... | Draft | Product Manager | |
| Tech Spec | TECH-SPEC-YYYY-NNN | ./specs/... | Draft | Product Architect | |
| ADR | ADR-YYYY-NNN | ./adr/... | Proposed | System Architect | |
| Impl Plan | PLAN-YYYY-NNN | ./implementation/... | Draft | Product Architect | |
| QA Plan | QA-YYYY-NNN | ./qa/... | Draft | QA | |
| Release Packet | REL-YYYY-NNN | ./release/... | Not started | OneArch | |

## Scope

### In Scope
- 

### Out of Scope
- 

## Milestones

| Milestone | Target | Status | Exit Criteria |
|---|---|---|---|
| M1 | | | |

## Risks

| Risk | Severity | Owner | Mitigation | Status |
|---|---|---|---|---|

## Open Questions

| Question | Owner | Needed By | Status |
|---|---|---|---|

## Founder Decisions

| Decision ID | Decision | Status | Date | Link |
|---|---|---|---|---|

## Latest Status
Short current status.
```

---

## 33. Global Initiative Registry

`company-architecture/initiatives/initiative-registry.md`

```markdown
# Initiative Registry

| Initiative ID | Name | Product | Status | Founder Priority | Driver | Current Gate | Last Updated |
|---|---|---|---|---|---|---|---|
| INIT-2026-001 | NewsGraph ingestion MVP | NewsGraph | discovery | P0 | Product Architect | RFC review | |
| INIT-2026-002 | Pairlio comparison board MVP | Pairlio | proposed | Pending | Product Manager | Founder decision | |
```

Registry rules:

```text
Every initiative must appear in the registry.
The registry must link to the initiative README.
Closed initiatives remain in the registry.
Cancelled initiatives remain in the registry with cancellation reason.
Superseded initiatives must link to the replacement initiative.
```

---

## 34. Artifact Metadata Header

Every artifact must start with a metadata block.

```yaml
---
artifact_id: RFC-2026-001
artifact_type: RFC
initiative_id: INIT-2026-001
initiative_name: NewsGraph ingestion MVP
product: NewsGraph
owner_agent: Product Architect / NewsGraph hat
status: Draft
created: 2026-06-26
last_updated: 2026-06-26
reviewers:
  - System Architect
  - Senior Backend Engineer
  - DBA / Data Architect
  - DevOps / Platform Engineer
  - QA Engineer
founder_decision_required: true
linked_decisions: []
linked_adrs: []
linked_specs: []
linked_backlog_items: []
supersedes: null
superseded_by: null
---
```

### Required metadata fields

| Field | Required | Purpose |
|---|---:|---|
| `artifact_id` | Yes | Stable reference ID |
| `artifact_type` | Yes | RFC / PRD / TECH-SPEC / ADR / PLAN / QA / RUNBOOK / RELEASE |
| `initiative_id` | Yes | Root traceability object |
| `product` | Yes | Product context |
| `owner_agent` | Yes | Responsible owner |
| `status` | Yes | Draft / Review / Approved / Superseded / Retired |
| `created` | Yes | Date created |
| `last_updated` | Yes | Freshness tracking |
| `founder_decision_required` | Yes | Whether Tal must decide |
| `linked_decisions` | Yes | Decision IDs that affect artifact |
| `linked_adrs` | Yes | ADR references |
| `linked_specs` | Yes | Related specs |
| `linked_backlog_items` | Yes | Execution links |

---

## 35. Artifact Manifest

Each initiative must contain `manifest.md`.

```markdown
# Artifact Manifest — INIT-YYYY-NNN

## Required Artifacts

| Artifact | Required? | Exists? | Status | Owner | Link |
|---|---:|---:|---|---|---|
| Founder intent | Yes | Yes | Approved | Tal | ./founder-intent.md |
| RFC | Yes for non-trivial initiatives | Yes | Review | Product Architect | ./rfc/... |
| PRD / Product Spec | Yes | Yes | Draft | Product Manager | ./specs/... |
| UX Spec | If user-facing | No | Not started | UX | ./specs/... |
| Technical Spec | Yes | Yes | Draft | Product Architect | ./specs/... |
| API Spec | If API changes | No | Not started | BE | ./specs/... |
| Data Spec | If data model changes | No | Not started | DBA | ./specs/... |
| ADRs | If architectural decision exists | Yes | Proposed | System Architect | ./adr/... |
| Implementation Plan | Yes | No | Not started | Product Architect | ./implementation/... |
| QA Plan | Yes | No | Not started | QA | ./qa/... |
| Observability Plan | If runtime component | No | Not started | DevOps | ./observability/... |
| Runbook | If production service/job | No | Not started | DevOps | ./ops/... |
| Release Packet | Before release | No | Not started | OneArch | ./release/... |

## Orphan Check

All artifacts under this folder must be listed above.

## Cross-Links

| External Artifact | Why Linked | Link |
|---|---|---|
| products/newsgraph/architecture/pipeline-design.md | Durable architecture page updated by this initiative | |
| platform/observability.md | Observability standards applied | |
```

---

## 36. RFC Template

RFCs are used before the decision is final. They are for structured discussion, tradeoff exposure, and founder decision preparation.

```markdown
---
artifact_id: RFC-YYYY-NNN
artifact_type: RFC
initiative_id: INIT-YYYY-NNN
product:
owner_agent:
status: Draft
founder_decision_required: true
linked_adrs: []
linked_specs: []
---

# RFC-YYYY-NNN: Title

## 1. Summary
Short proposal.

## 2. Founder Intent
What Tal asked for or wants to achieve.

## 3. Problem Statement
What problem this solves.

## 4. Goals
- 

## 5. Non-Goals
- 

## 6. Context
Relevant existing architecture, product state, constraints, prior decisions.

## 7. Proposed Approach
The recommended direction.

## 8. Alternatives Considered

| Option | Pros | Cons | Risk | Recommendation |
|---|---|---|---|---|
| A | | | | |
| B | | | | |

## 9. Product Impact
User value, UX implications, roadmap impact.

## 10. Technical Impact
Services, APIs, data model, infra, integrations.

## 11. Operational Impact
Monitoring, alerts, runbooks, cost, security, support burden.

## 12. QA / Validation Impact
Acceptance tests, regression tests, evaluation sets, manual checks.

## 13. Risks

| Risk | Severity | Probability | Mitigation | Owner |
|---|---|---|---|---|

## 14. Open Questions

| Question | Owner | Needed By | Blocks Decision? |
|---|---|---|---|

## 15. Recommendation
Clear agent recommendation.

## 16. Founder Decision Required
What exactly Tal must decide.

## 17. Decision Outcome
Approved / Rejected / Deferred / Needs revision.

## 18. Follow-up Artifacts
- ADRs to create:
- Specs to create/update:
- Implementation plans to create:
- Backlog items to create:
```

### RFC Rules

```text
RFCs can be opinionated but must show alternatives.
RFCs cannot silently become decisions.
Founder decision must be explicitly recorded.
Approved RFCs usually produce one or more ADRs and specs.
Rejected RFCs remain as historical context.
```

---

## 37. Specification Package

An initiative may have multiple specs. The minimum required spec package depends on the type of work.

| Initiative Type | Required Specs |
|---|---|
| User-facing feature | PRD, UX Spec, Tech Spec, QA Plan |
| Backend service | Tech Spec, API Spec, Data Spec if needed, Observability Plan, QA Plan, Runbook |
| Data model change | Data Spec, Migration Plan, ADR if architectural, QA/Data Quality Plan |
| Infrastructure change | Tech Spec, Terraform/Helm Plan, Security Review, Rollback Plan, Runbook |
| Agent workflow | Agent Spec, Tool Permission Spec, Eval Plan, Security Guardrails |

---

## 38. Product / PRD Spec Template

```markdown
---
artifact_id: PRD-YYYY-NNN
artifact_type: PRD
initiative_id: INIT-YYYY-NNN
product:
owner_agent: Product Manager / Product hat
status: Draft
founder_decision_required: false
linked_rfc:
linked_adrs: []
linked_backlog_items: []
---

# PRD-YYYY-NNN: Title

## 1. Founder Intent

## 2. Product Goal

## 3. Target Users

## 4. User Problems

## 5. User Stories

| ID | User Story | Priority | Notes |
|---|---|---|---|

## 6. Functional Requirements

| ID | Requirement | Priority | Acceptance Criteria |
|---|---|---|---|

## 7. Non-Functional Requirements
Performance, reliability, security, accessibility, cost, compliance.

## 8. UX Requirements
Screens, flows, empty states, error states, accessibility.

## 9. Analytics / Success Metrics

| Metric | Why It Matters | Target |
|---|---|---|

## 10. Out of Scope

## 11. Risks and Assumptions

## 12. Founder Decisions Needed

## 13. Linked Artifacts
```

---

## 39. Technical Spec Template

```markdown
---
artifact_id: TECH-SPEC-YYYY-NNN
artifact_type: TECH-SPEC
initiative_id: INIT-YYYY-NNN
product:
owner_agent: Product Architect / Product hat
status: Draft
founder_decision_required: false
linked_rfc:
linked_adrs: []
linked_backlog_items: []
---

# TECH-SPEC-YYYY-NNN: Title

## 1. Summary

## 2. Requirements Covered
Link to PRD requirement IDs.

## 3. Architecture Overview

## 4. Components Changed

| Component | Change | Owner | Risk |
|---|---|---|---|

## 5. APIs
Endpoints, request/response models, error behavior, auth.

## 6. Data Model
Tables, graph nodes, indexes, constraints, migrations.

## 7. Event / Queue Contracts
Topics, payloads, retry semantics, idempotency keys.

## 8. Failure Modes

| Failure | Expected Behavior | Monitoring | Recovery |
|---|---|---|---|

## 9. Observability
Metrics, logs, traces, dashboards, alerts.

## 10. Security
Auth, authorization, secrets, data exposure, threat model.

## 11. Performance and Scale
Expected load, limits, bottlenecks, scaling strategy.

## 12. Compatibility and Migration
Backward compatibility, rollout, data migration, rollback.

## 13. Testing Strategy
Unit, integration, contract, E2E, data quality, load, manual.

## 14. Rollout Plan

## 15. Rollback Plan

## 16. Open Questions

## 17. Linked ADRs

## 18. Implementation Plan Link
```

---

## 40. ADR Template

ADRs capture important architectural decisions after the decision is made or when a proposed decision needs founder approval.

```markdown
---
artifact_id: ADR-YYYY-NNN
artifact_type: ADR
initiative_id: INIT-YYYY-NNN
product:
owner_agent: System Architect / Product Architect
status: Proposed
founder_decision_required: true
linked_rfc:
linked_specs: []
supersedes:
superseded_by:
---

# ADR-YYYY-NNN: Title

## Status
Proposed / Accepted / Rejected / Superseded / Deprecated

## Context
What situation led to this decision?

## Decision Drivers
- 

## Decision
What was decided?

## Considered Options

| Option | Description | Pros | Cons |
|---|---|---|---|

## Consequences

### Positive
- 

### Negative
- 

### Neutral / Tradeoffs
- 

## Risks

## Mitigations

## Founder Decision
Approved / Rejected / Deferred.

## Follow-up Work

## Links
- RFC:
- Technical Spec:
- Implementation Plan:
- Backlog Items:
```

### ADR Rules

```text
ADRs are append-only historical records.
Do not edit old ADRs to pretend the decision was different.
If a decision changes, create a new ADR that supersedes the old one.
Every accepted ADR must be linked from the initiative manifest and the product architecture ADR index.
```

---

## 41. Implementation Plan Template

The implementation plan turns approved specs and ADRs into executable work.

```markdown
---
artifact_id: PLAN-YYYY-NNN
artifact_type: IMPLEMENTATION_PLAN
initiative_id: INIT-YYYY-NNN
product:
owner_agent: Product Architect / Product hat
status: Draft
founder_decision_required: false
linked_rfc:
linked_specs: []
linked_adrs: []
linked_backlog_items: []
---

# Implementation Plan — Title

## 1. Initiative
INIT-YYYY-NNN

## 2. Approved Inputs

| Input | Status | Link |
|---|---|---|
| Founder Intent | Approved | |
| RFC | Approved | |
| PRD | Approved | |
| Tech Spec | Approved | |
| ADRs | Accepted | |

## 3. Execution Strategy
How this will be built incrementally.

## 4. Milestones

| Milestone | Goal | Owner | Exit Criteria | Dependencies |
|---|---|---|---|---|
| M1 | | | | |

## 5. Work Breakdown

| Work ID | Title | Owner Agent | Depends On | Output Artifact / PR | Status |
|---|---|---|---|---|---|

## 6. RACI

| Area | Responsible | Accountable | Consulted | Informed |
|---|---|---|---|---|
| Backend | | | | |
| Frontend | | | | |
| Data | | | | |
| DevOps | | | | |
| QA | | | | |

## 7. Dependency Map

## 8. Environments
Dev / staging / production considerations.

## 9. Migration Plan
If applicable.

## 10. Observability Work
Metrics, logs, traces, dashboards, alerts.

## 11. QA and Validation Plan
Link to QA plan.

## 12. Release Plan
Link to release readiness packet.

## 13. Rollback Plan

## 14. Founder Re-Approval Required If
- Scope changes
- Priority changes
- Cost increases materially
- Risk level becomes high
- Architecture deviates from accepted ADR
- Release moves to production

## 15. Completion Definition
What must be true for the initiative to move to `released` or `closed`.
```

---

## 42. Traceability Matrix

Every initiative must contain `traceability-matrix.md`.

```markdown
# Traceability Matrix — INIT-YYYY-NNN

| Founder Intent | Requirement | Spec Section | ADR | Work Item | Test | Release Check | Monitoring |
|---|---|---|---|---|---|---|---|
| Validate RSS ingestion MVP | FR-001 ingest RSS feed | PRD §6 / TECH §5 | ADR-001 | W-001 | QA-001 | REL-001 | MET-001 |
| Prevent duplicate articles | FR-002 idempotent article writes | TECH §7 / DATA §3 | ADR-002 | W-004 | QA-007 | REL-003 | MET-004 |
```

Traceability rules:

```text
Every P0/P1 requirement must map to at least one work item and one test.
Every accepted ADR must map to at least one implementation or operational consequence.
Every production runtime component must map to monitoring and a runbook.
Every release check must map back to a requirement, risk, or ADR.
```

---

## 43. Backlog Linking Rules

Backlog items are not standalone. They must link back to the initiative and approved inputs.

```markdown
# Backlog Item

ID: NG-001
Initiative: INIT-2026-001 NewsGraph ingestion MVP
Source RFC: RFC-2026-001
Source Spec: TECH-SPEC-2026-001 §5
Source ADR: ADR-2026-001
Founder Intent: Validate NewsGraph ingestion pipeline with real RSS feeds.

## Title
Implement RSS feed ingestion worker

## Acceptance Criteria
- Covers PRD FR-001
- Covers TECH-SPEC §5.1
- Emits metrics defined in observability/metrics.md
- Has tests QA-001, QA-002, QA-003

## Done Means
- Code merged
- Tests passing
- Metrics visible
- Runbook updated
- Manifest updated
```

Rule:

```text
A backlog item without initiative_id is invalid.
A backlog item without acceptance criteria is not ready.
A backlog item implementing architecture without linked ADR is not ready.
```

---

## 44. Initiative Quality Gates

| Gate | Required Before Passing |
|---|---|
| Proposal → Discovery | Founder intent recorded, initiative ID created, driver assigned |
| Discovery → Decision Needed | RFC prepared, alternatives documented, risks listed |
| Decision Needed → Approved | Founder decision recorded |
| Approved → Planned | PRD/Tech Spec/ADRs created or explicitly waived |
| Planned → In Progress | Implementation plan, backlog, RACI, QA plan ready |
| In Progress → Release Candidate | Tests pass, release packet drafted, runbook ready if needed |
| Release Candidate → Released | Founder release approval, rollback plan, monitoring ready |
| Released → Operating | Health confirmed, no critical incidents, metrics visible |
| Operating → Closed | Final summary, lessons learned, durable docs updated |

### Waiver Rule

Artifacts may be waived only explicitly.

```markdown
# Artifact Waiver

Initiative:
Artifact waived:
Reason:
Risk:
Approved by: Tal / Founder
Date:
Review date:
```

---

## 45. Initiative Status Report Template

```markdown
# Initiative Status — INIT-YYYY-NNN

Date:
Status:
Founder Priority:
Driver:

## Summary

## Progress Since Last Update

## Current Blockers

## Decisions Needed From Founder

| Decision | Options | Recommendation | Risk | Needed By |
|---|---|---|---|---|

## Risks Changed

## Work Completed

## Work Next

## Artifact Health

| Artifact | Status | Fresh? | Problem |
|---|---|---|---|

## Monitoring / Quality Signals
If released or operating.
```

OneArch morning status should link to the latest initiative status instead of duplicating all details.

---

## 46. Example Initiative — NewsGraph Ingestion MVP

```text
Initiative ID: INIT-2026-001
Name: NewsGraph ingestion MVP
Product: NewsGraph
Founder Priority: Pending / likely P0
Driver: Product Architect / NewsGraph hat
Status: discovery
```

### Initiative README excerpt

```markdown
# Initiative: INIT-2026-001 — NewsGraph Ingestion MVP

## Summary
Build the first production-shaped ingestion path for NewsGraph: fetch RSS feeds, normalize articles, store canonical records, and expose enough monitoring to understand ingestion health.

## Founder Intent
Validate that NewsGraph can consume real news sources and produce clean article records that can later feed correlation, classification, and graph writing.

## Scope

### In Scope
- RSS feed polling
- Article normalization
- Canonical URL handling
- Article persistence
- Basic duplicate prevention
- Retry behavior
- Ingestion metrics and logs

### Out of Scope
- Full correlation
- Classification labels
- Graph UI
- Source political leaning model
- Paid source ingestion

## Linked Artifacts

| Artifact Type | ID | Path | Status |
|---|---|---|---|
| RFC | RFC-2026-001 | ./rfc/RFC-2026-001-newsgraph-ingestion-mvp.md | Draft |
| PRD | PRD-2026-001 | ./specs/PRD-2026-001-newsgraph-ingestion-mvp.md | Draft |
| Tech Spec | TECH-SPEC-2026-001 | ./specs/TECH-SPEC-2026-001-newsgraph-ingestion-mvp.md | Draft |
| ADR | ADR-2026-001 | ./adr/ADR-2026-001-postgres-canonical-store.md | Proposed |
| Impl Plan | PLAN-2026-001 | ./implementation/implementation-plan.md | Not started |
| QA Plan | QA-2026-001 | ./qa/qa-plan.md | Not started |
```

### Example ADR

```markdown
# ADR-2026-001: Use PostgreSQL as Canonical Article Store for NewsGraph MVP

## Status
Proposed

## Context
NewsGraph needs reliable article storage before correlation and graph projection. Neo4j is useful for graph exploration, but raw ingestion requires idempotent writes, unique constraints, replayability, and operational simplicity.

## Decision
Use PostgreSQL as the canonical store for ingested articles. Neo4j will be populated later through a graph writer projection.

## Considered Options

| Option | Pros | Cons |
|---|---|---|
| PostgreSQL canonical store | Simple, transactional, strong constraints, familiar migrations | Graph traversals require projection later |
| Neo4j only | Directly supports graph model | Harder as canonical event/article store for ingestion MVP |
| Hybrid immediately | Future-ready | More moving parts for MVP |

## Consequences

### Positive
- Ingestion MVP remains simpler.
- Article uniqueness and migration strategy are clearer.
- Graph writer can be replayable later.

### Negative
- Need later projection into Neo4j.
- Two-model architecture appears in Phase 2.

## Founder Decision
Approve PostgreSQL canonical store for ingestion MVP?
```

---

## 47. Example Initiative — Pairlio Comparison Board MVP

```text
Initiative ID: INIT-2026-002
Name: Pairlio comparison board MVP
Product: Pairlio
Founder Priority: Pending
Driver: Product Manager / Pairlio hat
Status: proposed
```

### Initiative README excerpt

```markdown
# Initiative: INIT-2026-002 — Pairlio Comparison Board MVP

## Summary
Build the core Pairlio comparison board flow: create a board, add options, add criteria, and persist the comparison state.

## Founder Intent
Validate whether Pairlio's core comparison workflow is useful before investing in collaboration, sharing, recommendation, or advanced scoring features.

## Scope

### In Scope
- Create board
- Add/edit/remove options
- Add/edit/remove criteria
- Persist board state
- Basic responsive UI
- Basic error and empty states

### Out of Scope
- Public sharing
- Team collaboration
- AI recommendations
- Payments
- Browser extension
- Advanced scoring
```

### Example RFC decision question

```markdown
## Founder Decision Required
Should Pairlio MVP start now in parallel with NewsGraph, or should Pairlio remain deferred until NewsGraph ingestion and graph pipeline are working?

## Options
1. Start Pairlio now with minimal board MVP.
2. Defer Pairlio until NewsGraph ingestion MVP is operating.
3. Build only low-cost UX prototype for Pairlio now, no backend yet.

## Recommendation
Option 3: build a low-cost UX prototype only.

## Reason
This preserves founder learning while avoiding execution dilution across two early products.
```

---

## 48. Initiative Artifact Linking Policy

```text
All durable artifacts must be reachable from:
1. Initiative README
2. Initiative manifest
3. Initiative registry
4. Relevant product or platform index if the artifact changes long-lived product/platform truth
```

### Required backlinks

| Artifact | Must Link Back To |
|---|---|
| RFC | Initiative README, founder intent |
| PRD | Initiative README, RFC if exists |
| UX Spec | Initiative README, PRD |
| Tech Spec | Initiative README, PRD, ADRs |
| ADR | Initiative README, RFC/Tech Spec, product architecture ADR index |
| Implementation Plan | Initiative README, PRD, Tech Spec, ADRs |
| Backlog Item | Initiative, spec section, ADR if relevant |
| QA Plan | Initiative, PRD requirements, Tech Spec risks |
| Runbook | Initiative, runtime component, observability plan |
| Release Packet | Initiative, implementation plan, QA plan, runbook |

---

## 49. Agent Responsibilities for Initiative Artifacts

| Agent | Initiative Artifact Responsibility |
|---|---|
| Product Manager | Founder intent clarification, PRD, roadmap impact, backlog proposal |
| UX Designer | UX spec, flows, wireframes, usability risks, accessibility notes |
| System Architect | Cross-product architecture review, major ADRs, architecture risk |
| Product Architect | RFC driver, technical spec, implementation plan, integration plan |
| Backend Engineer | API contracts, worker design details, backend task breakdown |
| Frontend Engineer | FE implementation plan, component/task breakdown, frontend risks |
| DBA / Data Architect | Data spec, migration plan, indexes, constraints, data quality checks |
| DevOps / Platform Engineer | Infra plan, deployment plan, observability, secrets, runbook, rollback |
| QA Engineer | QA plan, acceptance tests, regression tests, release quality gate |
| OneArch Operating Layer | Manifest, registry, status rollup, decision queue, artifact health |
| Personal Assistant | Founder meeting notes, decision summaries, follow-up extraction |

---

## 50. Initiative Closure Template

```markdown
# Initiative Closure — INIT-YYYY-NNN

## Final Status
Closed / Cancelled / Superseded

## What Was Delivered

## What Was Not Delivered

## Founder Decisions Made

| Decision | Outcome | Link |
|---|---|---|

## Artifacts Updated

| Artifact | Status | Link |
|---|---|---|

## Metrics / Evidence

## Incidents / Problems

## Lessons Learned

## Follow-up Initiatives

## Durable Documentation Updated
- Product docs:
- Architecture docs:
- Runbooks:
- Backlog:
```

Closure rule:

```text
An initiative cannot be closed until durable product, architecture, platform, QA, and runbook docs have been updated or explicitly waived.
```

---

## 51. Updated Recommended Next Actions

1. Create `company-architecture/initiatives/initiative-registry.md`.
2. Create the first initiative folder: `INIT-2026-001-newsgraph-ingestion-mvp`.
3. Add `README.md`, `manifest.md`, `founder-intent.md`, and `decision-log.md`.
4. Draft `RFC-2026-001-newsgraph-ingestion-mvp.md`.
5. Draft the first ADR: `ADR-2026-001-use-postgres-as-canonical-article-store.md`.
6. Draft the first implementation plan after founder decision.
7. Add the traceability matrix before implementation starts.
8. Add a rule to OneArch Daily: every work item shown in morning status must include `initiative_id`.
9. Add an orphan-artifact check to weekly artifact health review.
10. Convert future specs, ADRs, and plans into initiative-linked artifacts only.

---

## 52. Sources and External Practices Used

This expansion uses common engineering operating practices:

- ADRs as durable records of architectural decisions, including context and consequences.
- MADR-style Markdown ADR structure for consistent lightweight decision records.
- RFC/design-doc process for collecting feedback and tradeoffs before decisions.
- Traceability matrices from requirements engineering to connect intent, requirements, work, tests, release, and monitoring.
- OpenTelemetry-style observability planning around metrics, logs, traces, dashboards, and alerts.
- Founder-led governance adapted to agentic workflows: agents prepare and execute, but Tal decides roadmap, priority, architecture approval, and release approval.


---

# Part 5 — Jira-Native Initiative Execution System

## 53. Updated Hard Rules

The initiative system MUST be built on top of Jira.

The Markdown / Git repository remains the durable artifact source of truth. Jira is the execution system of record.

```text
Jira = execution control plane, workflow state, ownership, hierarchy, dependencies, status, delivery reporting.
Git = durable artifact source of truth, version history, review history, commits, pull requests, artifact revisions.
OneArch = founder operating layer that reads Jira + Git + monitoring and summarizes what needs attention.
```

### Non-Negotiable Rules

```text
Every initiative MUST exist as a Jira work item.
Every challenge MUST exist as a Jira work item under one initiative.
Every task MUST exist as a Jira work item under one challenge.
Every artifact MUST link to exactly one primary initiative.
Every task SHOULD produce or update at least one artifact.
Every artifact stored in version control MUST treat its commits as artifact revisions.
Every commit that changes an initiative artifact MUST reference the relevant Jira task key.
Every pull request that changes an initiative artifact MUST reference the relevant Jira task key and initiative key.
An initiative MUST NOT be closed until all required challenges, tasks, and artifacts are done, cancelled, or explicitly waived.
```

---

## 54. Jira as the System of Record

Jira MUST be the system of record for:

| Concern | Stored In Jira? | Stored In Git? | Rule |
|---|---:|---:|---|
| Initiative status | Yes | Snapshot only | Jira owns live status. |
| Founder priority | Yes | Optional snapshot | Jira custom field owns current priority. |
| Challenge breakdown | Yes | Summary/manifest | Jira owns hierarchy. |
| Task execution | Yes | PR/commit links | Jira owns work state. |
| Assignment | Yes | No | Jira owns assignee and owner. |
| Dependencies | Yes | Optional manifest | Jira links own blockers/dependencies. |
| Specs / PRD / RFC / ADRs | Link only | Yes | Git owns content. |
| UX design links | Link only | Design tool + Git index | Jira links to canonical design artifacts. |
| PRs | Development panel / links | VCS platform | Jira links; VCS owns content. |
| Commits | Development panel / links | Git | Git owns content and history. |
| QA evidence | Link + status | Git/test reports | Jira owns gate state; artifacts own evidence. |
| Release approval | Yes | Release packet | Jira owns approval state; Git owns release packet. |

Jira MUST NOT become the only copy of durable specs. Jira descriptions MAY summarize specs, but canonical specs MUST live as version-controlled artifacts or in a canonical design/document system that is linked from the initiative manifest.

---

## 55. Canonical Jira Hierarchy

OneArch SHOULD use a Jira company-managed software project with a configurable work type hierarchy.

Canonical hierarchy:

```text
Initiative
  └── Challenge
        └── Task / Story / Bug / Spike
              └── Sub-task, optional
```

### Issue Type Definitions

| Jira Work Type | Purpose | Required Parent | Completion Meaning |
|---|---|---|---|
| Initiative | Founder-approved bounded outcome | None, or parent Goal if goals are later added | All challenges/tasks/artifacts completed or waived. |
| Challenge | A major problem, capability, risk, or product slice inside the initiative | Initiative | Challenge acceptance criteria satisfied. |
| Task | Actual unit of work | Challenge | Work completed, reviewed, and linked artifact updated. |
| Story | User-value task | Challenge | User-facing behavior delivered and accepted. |
| Bug | Defect affecting initiative outcome | Challenge | Defect fixed and regression evidence linked. |
| Spike | Time-boxed research task | Challenge | Research artifact, recommendation, or decision brief produced. |
| Sub-task | Optional implementation checklist under a task | Task / Story / Bug / Spike | Supporting work completed. |

### Fallback If Custom Hierarchy Is Not Available

If Jira custom hierarchy cannot support `Initiative > Challenge > Task`, OneArch MUST still model the hierarchy using standard Jira work items and links:

```text
Epic = Initiative
Story/Task = Challenge
Sub-task or linked Task = Task
```

Fallback rules:

```text
The fallback MUST preserve initiative_id, challenge_id, parent link, blocked-by links, and artifact links.
The fallback MUST NOT allow orphan tasks.
The fallback MUST be treated as an implementation constraint, not a conceptual change.
```

---

## 56. Initiative Breakdown Model

An initiative is not directly executable. It MUST be decomposed into challenges, and challenges MUST be decomposed into tasks.

```text
Initiative = strategic execution container.
Challenge = bounded problem or capability within the initiative.
Task = actual executable unit of work.
Artifact = durable output or evidence created/updated by a task.
```

### Initiative Completion Formula

```text
Initiative Done =
  all required challenges are Done or explicitly waived
  AND all child tasks are Done, Cancelled, or explicitly waived
  AND required initiative artifacts exist
  AND artifact manifest is complete
  AND traceability matrix is complete
  AND QA/release gates pass or are founder-waived
  AND founder closure approval is recorded
```

### Challenge Completion Formula

```text
Challenge Done =
  all child tasks are Done, Cancelled, or explicitly waived
  AND challenge acceptance criteria are satisfied
  AND linked artifacts are current
  AND risks/blockers are closed or escalated
```

### Task Completion Formula

```text
Task Done =
  implementation or artifact work completed
  AND acceptance criteria satisfied
  AND relevant artifact link exists or no-artifact waiver is recorded
  AND PR/commit/test evidence is linked when applicable
  AND responsible agent marks execution complete
  AND accountable agent accepts completion
```

---

## 57. Initiative Artifact Set

Each initiative MUST contain or link to all relevant product, design, engineering, QA, release, and operational artifacts.

### Required Product Artifacts

| Artifact | Required When | Owner Agent | Canonical Location |
|---|---|---|---|
| Founder Intent | Always | Founder / OneArch | Git initiative folder |
| PRD | Product or user-facing initiative | Product Manager | Git initiative folder |
| User Stories | Product or UX initiative | Product Manager | Git initiative folder / Jira child tasks |
| Acceptance Criteria | Always | Product Manager + QA | PRD + Jira |
| UX Research Notes | When discovery or usability matters | UX Designer | Git or design tool linked from manifest |
| User Journey | Product initiative | UX Designer | Git initiative folder |
| UX / UI Design | Product initiative | UX Designer | Design tool link + Git index |
| UX Spec | Product initiative | UX Designer | Git initiative folder |
| Product Analytics Plan | Product initiative | Product Manager | Git initiative folder |
| Release Notes Draft | Releaseable product change | Product Manager | Git initiative folder |

### Required Engineering Artifacts

| Artifact | Required When | Owner Agent | Canonical Location |
|---|---|---|---|
| RFC | Before major product/architecture/implementation commitment | Driver agent | Git initiative folder |
| Technical Spec | Engineering work is non-trivial | Product Architect / BE / FE | Git initiative folder |
| API Contract | API changes | Backend + Frontend | Git initiative folder |
| Data Spec | Schema/data/graph changes | DBA | Git initiative folder |
| ADR | Significant architecture decision | Architect | Git initiative folder + ADR index |
| Implementation Plan | Before execution starts | Product Architect | Git initiative folder |
| PRs | Code or artifact changes | Executing engineer/agent | VCS, linked in Jira |
| Commit Artifacts | Any version-controlled artifact change | Executing agent | Git, linked in Jira |
| Test Plan | Any delivery initiative | QA | Git initiative folder |
| Runbook | Runtime/operational capability | DevOps / BE | Git initiative folder |
| Observability Plan | Runtime service/pipeline | DevOps / BE | Git initiative folder |
| Release Packet | Before release approval | OneArch / DevOps / QA | Git initiative folder |

### Optional But Recommended Artifacts

| Artifact | Use When |
|---|---|
| Competitive analysis | Product strategy or market differentiation matters. |
| Cost model | Infrastructure or vendor cost may materially change. |
| Security review | Sensitive data, auth, public exposure, secrets, or agent actions are involved. |
| Migration plan | Data or infra migration is involved. |
| Rollback plan | Any production change is released. |
| Post-release review | Initiative had incidents, delays, or high learning value. |

---

## 58. RFC 2119 / BCP 14 Requirement Language Policy

All initiative specs and plans MUST use RFC 2119 / BCP 14 style requirement language.

This applies to:

```text
PRD
UX Spec
User Stories when written as requirements
RFC
Technical Spec
API Contract
Data Spec
Implementation Plan
QA Plan
Runbook
Release Packet
Acceptance Criteria
Security Review
Migration Plan
Rollback Plan
```

### Required Normative Header

Every normative artifact MUST include this section near the top:

```markdown
## Requirement Language

The key words MUST, MUST NOT, SHOULD, SHOULD NOT, MAY, REQUIRED, RECOMMENDED, and OPTIONAL are to be interpreted as normative requirement levels.
Only UPPERCASE usage is normative.
Lowercase words such as must, should, and may are descriptive only.
```

### Requirement ID Rules

Every normative requirement MUST have a stable ID.

Recommended prefixes:

| Prefix | Meaning |
|---|---|
| `REQ` | Product requirement |
| `UX` | UX requirement |
| `API` | API requirement |
| `BE` | Backend requirement |
| `FE` | Frontend requirement |
| `DATA` | Database/data/graph requirement |
| `OPS` | Operational/platform requirement |
| `SEC` | Security requirement |
| `QA` | Quality/testing requirement |
| `OBS` | Observability requirement |
| `REL` | Release requirement |
| `MIG` | Migration requirement |

Example:

```markdown
| ID | Requirement | Priority | Verification |
|---|---|---|---|
| REQ-001 | The system MUST allow a user to create a comparison board. | P0 | E2E test |
| UX-001 | The board creation flow SHOULD complete in three steps or fewer. | P1 | UX review |
| API-001 | The API MUST return stable board IDs after creation. | P0 | API integration test |
| QA-001 | The feature MUST have regression coverage before release. | P0 | CI report |
```

### Requirement Severity Semantics

| Keyword | OneArch Meaning |
|---|---|
| MUST / REQUIRED | Mandatory. Failure blocks completion unless founder explicitly waives. |
| MUST NOT | Prohibited. Violation blocks completion unless founder explicitly accepts risk. |
| SHOULD / RECOMMENDED | Strong default. May be skipped only with documented rationale. |
| SHOULD NOT | Strong avoidance. May be done only with documented rationale. |
| MAY / OPTIONAL | Allowed but not required. Must not silently become required scope. |

### Anti-Ambiguity Rules

```text
A requirement MUST NOT mix multiple independent requirements in one row.
A requirement MUST include verification method.
A requirement MUST indicate priority or gate relevance.
A requirement SHOULD identify owner agent.
A SHOULD requirement that is skipped MUST have a documented reason.
A MAY requirement MUST NOT be treated as blocking unless founder promotes it to MUST.
```

---

## 59. Jira Custom Fields

Every Initiative, Challenge, and Task SHOULD use a consistent field schema.

### Initiative Fields

| Field | Required | Example |
|---|---:|---|
| `Initiative ID` | Yes | `ONE-123` |
| `Product` | Yes | `NewsGraph` / `Pairlio` / `OneArch` / `Platform` |
| `Founder Priority` | Yes | `P0` / `P1` / `P2` / `P3` |
| `Founder Decision Status` | Yes | `Pending` / `Approved` / `Rejected` / `Deferred` |
| `Driver Agent` | Yes | `Product Architect / NewsGraph hat` |
| `Current Gate` | Yes | `RFC Review` |
| `Artifact Manifest URL` | Yes | Git URL |
| `PRD URL` | Conditional | Git URL |
| `RFC URL` | Conditional | Git URL |
| `ADR Index URL` | Conditional | Git URL |
| `Implementation Plan URL` | Conditional | Git URL |
| `UX Design URL` | Conditional | Figma/design tool URL |
| `Traceability Matrix URL` | Yes | Git URL |
| `Release Packet URL` | Conditional | Git URL |
| `Risk Level` | Yes | `Low` / `Medium` / `High` |
| `Target Release` | Conditional | Version/release |
| `Closure Approval` | Yes before Done | Tal approval record |

### Challenge Fields

| Field | Required | Example |
|---|---:|---|
| `Parent Initiative` | Yes | `ONE-123` |
| `Challenge Type` | Yes | `Product` / `UX` / `Architecture` / `Backend` / `Frontend` / `Data` / `DevOps` / `QA` |
| `Challenge Outcome` | Yes | `Reliable ingestion worker designed and implemented` |
| `Required Artifacts` | Yes | `Tech Spec, ADR, Test Plan` |
| `Acceptance Criteria` | Yes | RFC 2119 requirement list |
| `Accountable Agent` | Yes | `Product Architect` |
| `Blocked By` | Conditional | Jira links |

### Task Fields

| Field | Required | Example |
|---|---:|---|
| `Parent Challenge` | Yes | `ONE-145` |
| `Task Type` | Yes | `Spec` / `Design` / `Code` / `Test` / `Infra` / `Review` / `Decision` / `Research` |
| `Responsible Agent` | Yes | `Senior Backend Engineer` |
| `Primary Artifact Type` | Yes | `Technical Spec` / `PR` / `ADR` / `Test Report` |
| `Primary Artifact URL` | Conditional | Git/PR/design/test URL |
| `No Artifact Waiver` | Conditional | Required only if no artifact produced |
| `Verification Method` | Yes | `Review` / `Test` / `Founder approval` / `CI` |
| `Definition of Done` | Yes | Checklist |

---

## 60. Jira Workflow States

### Initiative Workflow

```text
Proposed
Discovery
RFC Drafting
RFC Review
Founder Decision
Approved For Breakdown
Challenges Defined
Ready For Execution
In Execution
Release Review
Founder Closure Review
Done
Cancelled
Superseded
```

Required gate rules:

```text
An initiative MUST NOT move to Approved For Breakdown without founder decision.
An initiative MUST NOT move to Ready For Execution until required challenges exist.
An initiative MUST NOT move to Release Review until all execution tasks are complete or waived.
An initiative MUST NOT move to Done until closure approval is recorded.
```

### Challenge Workflow

```text
Proposed
Analysis
Ready For Tasks
In Execution
Blocked
Validation
Done
Cancelled
Waived
```

Required gate rules:

```text
A challenge MUST NOT move to Ready For Tasks until acceptance criteria are written.
A challenge MUST NOT move to Done until all child tasks are Done, Cancelled, or Waived.
A waived challenge MUST include founder or accountable-agent waiver rationale depending on risk.
```

### Task Workflow

```text
Todo
Ready
In Progress
In Review
QA / Validation
Blocked
Done
Cancelled
Waived
```

Required gate rules:

```text
A task MUST NOT move to Ready without clear acceptance criteria.
A task MUST NOT move to In Review without a linked artifact, PR, commit, test result, or waiver.
A task MUST NOT move to Done without verification evidence.
```

---

## 61. Artifact-as-Code and Commit Artifacts

If an artifact is stored in version control, every commit that changes it is itself an artifact revision.

```text
Artifact = canonical file or document.
Artifact Revision = Git commit that changes the artifact.
Artifact Change Request = Pull request that proposes one or more artifact revisions.
Artifact Version = approved state of the artifact at a commit, tag, or release point.
```

### Commit Artifact Metadata

Every commit that updates an initiative artifact MUST include:

```text
Jira task key
Short change summary
Artifact path or artifact identifier
Reason for change when not obvious
```

Recommended commit format:

```text
ONE-456 update NewsGraph ingestion RFC with retry requirements

Artifact: initiatives/ONE-123-newsgraph-ingestion/rfc/RFC-001-ingestion.md
Reason: Add retry/idempotency requirements after architecture review.
Initiative: ONE-123
Challenge: ONE-140
```

### Branch Naming Rule

```text
<jira-task-key>/<short-description>
```

Examples:

```text
ONE-456/newsgraph-ingestion-rfc
ONE-457/pairlio-board-prd
ONE-458/add-graph-writer-adr
```

### Pull Request Rule

Every pull request MUST include:

```text
Jira task key in title
Initiative key in description
Challenge key in description
Artifact paths changed
Requirement IDs affected
Tests/evidence
Reviewer checklist
```

Example PR title:

```text
ONE-456: Update NewsGraph ingestion RFC and implementation plan
```

Example PR description:

```markdown
## Jira
- Initiative: ONE-123
- Challenge: ONE-140
- Task: ONE-456

## Artifact Changes
- `initiatives/ONE-123-newsgraph-ingestion/rfc/RFC-001-ingestion.md`
- `initiatives/ONE-123-newsgraph-ingestion/plans/implementation-plan.md`

## Requirement IDs Changed
- REQ-003
- BE-002
- OPS-001
- QA-004

## Evidence
- Markdown lint passed
- Traceability matrix updated
- Reviewed by Product Architect and QA
```

### Commit Artifact Index

Each initiative SHOULD include a generated or maintained commit artifact index:

```markdown
# Commit Artifact Index

| Commit SHA | Jira Task | Artifact Path | Change Type | Summary | PR | Date |
|---|---|---|---|---|---|---|
| `abc1234` | ONE-456 | `rfc/RFC-001-ingestion.md` | Update | Added retry requirements | PR-22 | 2026-06-26 |
```

---

## 62. Initiative Manifest — Jira-Linked Version

Every initiative MUST have a manifest that links Jira, Git, product artifacts, design artifacts, PRs, commits, and releases.

```markdown
# Initiative Manifest — ONE-123 NewsGraph Ingestion MVP

## Jira
- Initiative: ONE-123
- Jira URL:
- Founder Priority:
- Driver Agent:
- Current Gate:

## Challenges
| Challenge Key | Name | Status | Required Artifacts | Link |
|---|---|---|---|---|
| ONE-140 | Feed ingestion reliability | In Execution | RFC, Tech Spec, QA Plan | |
| ONE-141 | Source normalization | Ready | Data Spec, Test Plan | |

## Tasks
| Task Key | Challenge | Type | Status | Primary Artifact | PR/Commit |
|---|---|---|---|---|---|
| ONE-456 | ONE-140 | Spec | Done | RFC-001 | PR-22 |
| ONE-457 | ONE-140 | Code | In Progress | Graph writer PR | PR-23 |

## Product Artifacts
| Artifact | Status | Canonical Link | Jira Task | Last Commit |
|---|---|---|---|---|
| Founder Intent | Approved | `founder-intent.md` | ONE-130 | `abc1234` |
| PRD | Draft | `product/prd.md` | ONE-131 | `def5678` |
| User Journey | Draft | `product/user-journey.md` | ONE-132 | `ghi9999` |
| UX Spec | Not Started | `ux/ux-spec.md` | ONE-133 | |

## Engineering Artifacts
| Artifact | Status | Canonical Link | Jira Task | Last Commit |
|---|---|---|---|---|
| RFC | Approved | `rfc/RFC-001-ingestion.md` | ONE-456 | `abc1234` |
| ADR-001 | Approved | `adr/ADR-001-canonical-store.md` | ONE-459 | `bbb2222` |
| Implementation Plan | Draft | `plans/implementation-plan.md` | ONE-460 | `ccc3333` |
| QA Plan | Draft | `qa/test-plan.md` | ONE-461 | `ddd4444` |

## Pull Requests
| PR | Jira Task | Summary | Status |
|---|---|---|---|
| PR-22 | ONE-456 | Update RFC | Merged |
| PR-23 | ONE-457 | Implement worker skeleton | Open |

## Commit Artifacts
| Commit | Jira Task | Artifact | Summary |
|---|---|---|---|
| `abc1234` | ONE-456 | RFC | Added retry/idempotency requirements |

## Release / Deployment Evidence
| Release | Jira Version | Release Packet | Status |
|---|---|---|---|
| `ng-mvp-0.1` | `NG-0.1` | `release/release-packet.md` | Pending |
```

---

## 63. Challenge Template

```markdown
# Challenge — ONE-140 Feed Ingestion Reliability

## Requirement Language

The key words MUST, MUST NOT, SHOULD, SHOULD NOT, MAY, REQUIRED, RECOMMENDED, and OPTIONAL are to be interpreted as normative requirement levels.
Only UPPERCASE usage is normative.
Lowercase words such as must, should, and may are descriptive only.

## Jira
- Initiative: ONE-123
- Challenge: ONE-140
- Status:
- Accountable Agent:
- Responsible Agents:

## Challenge Statement

What problem/capability/risk this challenge addresses.

## Scope

### In Scope

### Out of Scope

## Acceptance Criteria

| ID | Requirement | Verification |
|---|---|---|
| CH-001 | The initiative MUST support scheduled feed ingestion for configured sources. | Integration test |
| CH-002 | The ingestion path MUST prevent duplicate article creation. | Data quality test |
| CH-003 | The ingestion system SHOULD expose lag and failure metrics. | Dashboard review |

## Required Artifacts

| Artifact | Jira Task | Status | Link |
|---|---|---|---|
| RFC section | | | |
| Technical Spec | | | |
| Test Plan | | | |
| Runbook | | | |

## Task Breakdown

| Task Key | Task | Owner | Artifact | Status |
|---|---|---|---|---|
| ONE-456 | Draft ingestion RFC | Product Architect | RFC | Todo |
| ONE-457 | Define ingestion data model | DBA | Data Spec | Todo |
| ONE-458 | Implement ingestion worker | BE | PR | Todo |
| ONE-459 | Add ingestion tests | QA / BE | Test Report | Todo |

## Dependencies

## Risks

## Completion Evidence
```

---

## 64. Task Template

```markdown
# Task — ONE-456 Draft NewsGraph Ingestion RFC

## Requirement Language

The key words MUST, MUST NOT, SHOULD, SHOULD NOT, MAY, REQUIRED, RECOMMENDED, and OPTIONAL are to be interpreted as normative requirement levels.
Only UPPERCASE usage is normative.
Lowercase words such as must, should, and may are descriptive only.

## Jira
- Initiative: ONE-123
- Challenge: ONE-140
- Task: ONE-456
- Task Type: Spec
- Responsible Agent: Product Architect / NewsGraph hat
- Accountable Agent: System Architect

## Task Outcome

Produce a reviewed RFC for NewsGraph feed ingestion reliability.

## Acceptance Criteria

| ID | Requirement | Verification |
|---|---|---|
| TASK-001 | The RFC MUST define ingestion scope, alternatives, risks, and recommendation. | Reviewer checklist |
| TASK-002 | The RFC MUST include requirement IDs for product, backend, data, ops, and QA. | RFC review |
| TASK-003 | The RFC MUST link to this Jira task, the parent challenge, and the initiative manifest. | Link check |
| TASK-004 | The RFC SHOULD include a rejected alternatives section. | RFC review |

## Primary Artifact

- Type: RFC
- Path: `initiatives/ONE-123-newsgraph-ingestion/rfc/RFC-001-ingestion.md`
- PR:
- Commits:

## Work Plan

1. Read founder intent and PRD.
2. Draft RFC.
3. Add alternatives and recommendation.
4. Add normative requirement IDs.
5. Update traceability matrix.
6. Open PR.
7. Link PR to Jira.

## Definition of Done

- [ ] Artifact exists.
- [ ] Requirement language section exists.
- [ ] Jira task key appears in branch, commit, and PR.
- [ ] Parent challenge updated.
- [ ] Manifest updated.
- [ ] Accountable agent accepted task completion.
```

---

## 65. PRD Template With RFC 2119 Requirements

```markdown
# PRD — ONE-123 NewsGraph Ingestion MVP

## Requirement Language

The key words MUST, MUST NOT, SHOULD, SHOULD NOT, MAY, REQUIRED, RECOMMENDED, and OPTIONAL are to be interpreted as normative requirement levels.
Only UPPERCASE usage is normative.
Lowercase words such as must, should, and may are descriptive only.

## Jira Links

- Initiative:
- Product Challenges:
- UX Challenges:
- Implementation Challenges:

## Founder Intent

## Problem

## Users / Personas

## Product Goals

## Non-Goals

## User Stories

| ID | User Story | Priority | Jira Task / Story |
|---|---|---|---|
| US-001 | As an analyst, I want new articles to appear automatically so that I can monitor current events. | P0 | |

## Product Requirements

| ID | Requirement | Priority | Verification |
|---|---|---|---|
| REQ-001 | The product MUST ingest configured news feeds without manual founder action. | P0 | Integration test + monitoring evidence |
| REQ-002 | The product MUST show when the latest ingestion succeeded or failed. | P0 | UX acceptance test |
| REQ-003 | The product SHOULD allow filtering articles by source. | P1 | Product review |
| REQ-004 | The MVP MAY support manual feed refresh. | P2 | Optional |

## UX Requirements

| ID | Requirement | Priority | Verification |
|---|---|---|---|
| UX-001 | The UI MUST show ingestion status in a way that is understandable without reading logs. | P0 | UX review |

## Analytics Requirements

| ID | Requirement | Priority | Verification |
|---|---|---|---|
| AN-001 | The product MUST track article ingestion count by source. | P0 | Analytics event validation |

## Acceptance Criteria

## Risks

## Open Decisions

## Linked Artifacts
```

---

## 66. Implementation Plan Template With Challenges and Tasks

```markdown
# Implementation Plan — ONE-123 NewsGraph Ingestion MVP

## Requirement Language

The key words MUST, MUST NOT, SHOULD, SHOULD NOT, MAY, REQUIRED, RECOMMENDED, and OPTIONAL are to be interpreted as normative requirement levels.
Only UPPERCASE usage is normative.
Lowercase words such as must, should, and may are descriptive only.

## Jira Links

- Initiative:
- Challenges:
- Task Filter:
- Board:

## Approved Decisions

| Decision / ADR | Summary | Impact |
|---|---|---|
| ADR-001 | Postgres canonical store + Neo4j projection | Worker writes canonical first |

## Challenge Breakdown

| Challenge Key | Challenge | Outcome | Required Artifacts | Exit Criteria |
|---|---|---|---|---|
| ONE-140 | Feed ingestion reliability | Feeds ingested reliably | RFC, Tech Spec, QA Plan | CH-001..CH-003 pass |
| ONE-141 | Article canonical data model | Stable article/source schema | Data Spec, ADR | DATA-001..DATA-004 pass |
| ONE-142 | Observability | Ingestion status visible | Observability Plan, Runbook | OBS-001..OBS-003 pass |

## Task Breakdown

| Task Key | Challenge | Task | Owner | Artifact | Depends On |
|---|---|---|---|---|---|
| ONE-456 | ONE-140 | Draft RFC | Product Architect | RFC | Founder intent |
| ONE-457 | ONE-141 | Define tables/indexes | DBA | Data Spec | ONE-456 |
| ONE-458 | ONE-140 | Implement worker skeleton | BE | PR | ONE-456, ONE-457 |
| ONE-459 | ONE-142 | Add metrics/dashboard | DevOps/BE | Observability Plan + PR | ONE-458 |
| ONE-460 | ONE-140 | Add test coverage | QA/BE | Test Report | ONE-458 |

## Execution Requirements

| ID | Requirement | Verification |
|---|---|---|
| PLAN-001 | Every implementation task MUST reference its parent challenge and initiative. | Jira query |
| PLAN-002 | Every code task MUST produce a PR or have a documented no-code rationale. | PR link check |
| PLAN-003 | Every artifact task MUST update the initiative manifest. | Manifest review |
| PLAN-004 | All P0 requirements MUST have mapped tests or founder waiver before release. | Traceability matrix |

## Rollout Plan

## Rollback Plan

## QA Plan Summary

## Release Gate
```

---

## 67. Jira Query and Dashboard Requirements

OneArch MUST maintain Jira filters for initiative execution control.

### Required Filters

```jql
project = ONE AND issuetype = Initiative AND statusCategory != Done ORDER BY priority DESC, updated DESC
```

```jql
project = ONE AND "Parent Initiative" = ONE-123 ORDER BY issuetype, priority DESC
```

```jql
project = ONE AND "Parent Challenge" is EMPTY AND issuetype in (Task, Story, Bug, Spike) AND statusCategory != Done
```

```jql
project = ONE AND "Artifact Manifest URL" is EMPTY AND issuetype = Initiative AND statusCategory != Done
```

```jql
project = ONE AND "Primary Artifact URL" is EMPTY AND issuetype in (Task, Story, Bug, Spike) AND statusCategory = Done
```

### Required Dashboard Widgets

| Widget | Purpose |
|---|---|
| Active Initiatives | Show all non-done initiatives by founder priority. |
| Challenges by Status | Show execution breakdown per initiative. |
| Blocked Tasks | Show active blockers requiring agent/founder action. |
| Tasks Missing Artifacts | Detect work without durable output. |
| Initiatives Missing Manifests | Detect broken traceability. |
| Founder Decisions Pending | Show decisions blocking progress. |
| PRs Open by Initiative | Show review load. |
| Requirements Without Tests | Show QA traceability gaps. |

---

## 68. Completion and Closure Policy

### Task Done Policy

A task MAY be marked Done only when:

```text
Acceptance criteria are satisfied.
Primary artifact exists or no-artifact waiver exists.
Jira links to PRs/commits/test evidence exist where applicable.
Parent challenge status is updated if needed.
Initiative manifest is updated if artifact links changed.
```

### Challenge Done Policy

A challenge MAY be marked Done only when:

```text
All child tasks are Done, Cancelled, or Waived.
All challenge acceptance criteria are satisfied.
Required artifacts are linked and current.
Open risks are closed, accepted, or escalated.
```

### Initiative Done Policy

An initiative MAY be marked Done only when:

```text
All challenges are Done, Cancelled, or Waived.
All required product artifacts exist.
All required engineering artifacts exist.
All required QA/release artifacts exist.
Traceability matrix is complete.
Artifact manifest is complete.
Product documentation is updated.
Runbooks are updated if runtime behavior changed.
Founder closure approval is recorded.
```

---

## 69. Example — NewsGraph Initiative Breakdown

```text
Initiative: ONE-123 NewsGraph Ingestion MVP
```

### Challenges

| Challenge Key | Challenge | Type | Outcome |
|---|---|---|---|
| ONE-140 | Feed ingestion reliability | Backend/Product | Configured feeds are fetched reliably and idempotently. |
| ONE-141 | Article canonical data model | Data | Articles and sources have stable canonical schema. |
| ONE-142 | Ingestion observability | DevOps/Backend | Founder can see ingestion health in morning status. |
| ONE-143 | Ingestion QA coverage | QA | Core success/failure/duplicate scenarios are tested. |

### Tasks

| Task Key | Parent Challenge | Task | Artifact |
|---|---|---|---|
| ONE-456 | ONE-140 | Draft ingestion RFC | RFC |
| ONE-457 | ONE-141 | Draft article/source data spec | Data Spec |
| ONE-458 | ONE-140 | Implement ingestion worker skeleton | PR + commits |
| ONE-459 | ONE-140 | Add retry/idempotency behavior | PR + tests |
| ONE-460 | ONE-142 | Define ingestion metrics and dashboard | Observability Plan |
| ONE-461 | ONE-143 | Write ingestion QA plan | QA Plan |
| ONE-462 | ONE-143 | Add integration tests | PR + test report |
| ONE-463 | ONE-142 | Draft ingestion runbook | Runbook |

Completion rule:

```text
ONE-123 is not complete when the worker works once.
ONE-123 is complete only when all challenges are closed, all required artifacts are linked, and founder closure is recorded.
```

---

## 70. Example — Pairlio Initiative Breakdown

```text
Initiative: ONE-200 Pairlio Comparison Board MVP
```

### Challenges

| Challenge Key | Challenge | Type | Outcome |
|---|---|---|---|
| ONE-210 | Board creation product flow | Product/UX | User can create a board with clear steps. |
| ONE-211 | Comparison data model | Data/Backend | Boards, items, criteria, and scores are stored consistently. |
| ONE-212 | Board UI implementation | Frontend | User can create and edit comparison boards. |
| ONE-213 | Sharing and permissions | Product/Backend | Sharing model is explicit and safe. |
| ONE-214 | MVP QA coverage | QA | Main board flows are tested. |

### Tasks

| Task Key | Parent Challenge | Task | Artifact |
|---|---|---|---|
| ONE-220 | ONE-210 | Draft Pairlio PRD | PRD |
| ONE-221 | ONE-210 | Draft user journey | User Journey |
| ONE-222 | ONE-210 | Create UX wireframes | UX Design Link + UX Spec |
| ONE-223 | ONE-211 | Draft comparison data spec | Data Spec |
| ONE-224 | ONE-211 | Draft API contract | API Contract |
| ONE-225 | ONE-212 | Implement board creation page | PR + commits |
| ONE-226 | ONE-212 | Implement criteria editor | PR + commits |
| ONE-227 | ONE-214 | Write E2E tests | PR + test report |
| ONE-228 | ONE-214 | Draft release packet | Release Packet |

---

## 71. Agent Rules for Jira-Native Execution

```text
Agents MUST NOT create work outside Jira for initiative execution.
Agents MUST NOT execute initiative work unless a Jira task exists.
Agents MUST NOT mark a task Done without artifact/evidence links.
Agents MUST NOT create orphan artifacts.
Agents MUST update the initiative manifest when artifact links change.
Agents SHOULD prefer small tasks with one primary artifact or outcome.
Agents SHOULD escalate if a task requires scope, priority, architecture, cost, or release changes.
OneArch MUST report initiative status from Jira, not from memory.
```

---

## 72. Updated Recommended Next Actions — Jira First

1. Create a Jira project/space for OneArch execution.
2. Configure work types: `Initiative`, `Challenge`, `Task`, `Story`, `Bug`, `Spike`.
3. Configure hierarchy: `Initiative > Challenge > Task/Story/Bug/Spike > Sub-task`.
4. Add required custom fields for initiatives, challenges, and tasks.
5. Create Jira filters for active initiatives, blocked tasks, missing artifacts, and founder decisions.
6. Connect Jira to the Git provider.
7. Enforce branch/commit/PR naming using Jira work item keys.
8. Create the first initiative in Jira before creating more artifacts.
9. Create the initiative Git folder and manifest.
10. Link the Jira initiative to the manifest.
11. Break the initiative into challenges.
12. Break challenges into tasks.
13. Generate PRD/RFC/spec/plan artifacts from Jira task execution.
14. Update OneArch Daily to report initiative/challenge/task status from Jira.

