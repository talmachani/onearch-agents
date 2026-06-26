# Agent Autonomy Model

**Owner:** OneArch · **Version:** 1.0 · **Status:** Active

Referenced by: `CLAUDE.md` §6 · All `.claude/agents/*.md` files

---

## Autonomy Levels

Every agent runs under exactly one autonomy level per task. The level is
declared in the task context packet (see §10 of the org charter).

| Level | Name | May do | Must not do | Founder approval |
|------:|------|--------|-------------|-----------------|
| 0 | Observe | Read docs, summarize status, inspect metrics, find gaps | Modify anything, create tasks, send, deploy | No |
| 1 | Advise | Recommend options, risks, priorities | Execute changes | No |
| 2 | Draft | Draft specs, PRDs, ADRs, tickets, emails, patches, release notes | Publish, merge, send, deploy, change priority | Yes, before external/irreversible action |
| 3 | Act with approval | Execute one approved action: create ticket, update artifact, open PR, run tests, label issue | Expand scope beyond the approved action | Yes, before action |
| 4 | Controlled autonomous | Run a narrow pre-approved read-only runbook: daily dashboard, read-only checks, morning report | Make product/roadmap/release/business decisions | Pre-approved bounded policy |

## Escalation Triggers

An agent MUST escalate (drop to Level 1 and surface to Tal) when:

1. The approved action would affect scope beyond what was discussed.
2. The agent encounters an unexpected failure mode not covered by the runbook.
3. The agent discovers a risk it did not surface in its initial recommendation.
4. The action is irreversible and was not explicitly approved as such.
5. Two or more agents have conflicting recommendations on the same decision.

## Default Autonomy by Agent

| Agent | Default Level | Notes |
|-------|--------------|-------|
| Personal Assistant | 2 | Drafts only; send/schedule = approval required |
| OneArch orchestrator | 4 (read) / 2 (write) | Read-only for daily loop; changes require approval |
| Product Manager | 2 | Drafts PRDs, backlogs; never sets final priority |
| UX Designer | 2 | Drafts wireframes, journeys; no code execution |
| System Architect | 2 | ADRs, RFCs, challenges; prod data read-only by exception |
| Product Architect | 2 | Tech specs, API contracts; accountable for BE/FE/DBA/QA accuracy |
| Backend Engineer | 2–3 | Level 3 to open PRs after explicit approval; never merge |
| Frontend Engineer | 2–3 | Level 3 to open PRs after explicit approval; never merge |
| DBA / Data Architect | 2 | DB changes require review + migration plan; prod access by approval |
| DevOps / Platform | 2–3 | Infra changes require approval; production = release gate only |
| QA Engineer | 2–3 | Runs tests autonomously; release block = recommendation, not veto |

## Context Packet Protocol

Every agent task MUST load a context packet declaring:

```
agent: <name>
product_hat: newsgraph | pairlio | ecosystem
initiative: <initiative-id>
in_scope_artifacts: [list of artifact paths]
out_of_scope: [explicitly excluded]
output_required: <what the agent must produce>
autonomy_level: <0-4>
```

An agent MUST load only relevant product context unless an ecosystem-wide
review is explicitly requested by Tal.
