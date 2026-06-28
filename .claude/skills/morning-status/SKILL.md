---
name: morning-status
description: Generate the OneArch daily morning status report for Tal. Reads founder/decision-log.md, active Jira work items, monitoring signals, and blocked items. Outputs a structured 5-section briefing.
---

# Morning Status Skill

## When to Use

Invoke when asked for a morning status, daily briefing, "what do I need to know today," or any daily summary of work state.

## Steps

1. Read `founder/decision-log.md` — collect all entries with `**Status:** Pending`, sorted by Date (oldest first).

2. Read `founder/roadmap-decisions.md` — note current focus and priority order (P0/P1/P2 table).

3. Query Jira via Atlassian MCP (`mcp__atlassian__search_issues`):
   - Active tasks: `status != Done AND status != Cancelled ORDER BY priority ASC`
   - Blocked tasks: tasks with no status change in the last 24 hours
   - Completed: `status = Done AND updated >= -1d`
   - If Atlassian MCP unavailable: read `founder/roadmap-decisions.md` and local Git artifacts instead; note the gap in the output.

4. Query monitoring (Grafana/Prometheus MCP if connected):
   - Active alerts
   - SLO status for active user journeys
   - If unavailable: write "Monitoring data unavailable — check Grafana directly."

5. Compose the report using this exact format — do not add or remove sections:

```
# OneArch Morning Status — [DATE]

## 1. Open Founder Decisions (action required)
[For each pending decision: D-ID · Title · Date opened · One-line summary of what decision is needed]
[If none: "No pending decisions."]

## 2. Work Queue (today's priority)
[P0 tasks first, then P1, then P2. Maximum 5 items.
 Format: [TASK-KEY] Title — Assignee — Status]
[If no active tasks: "No active work items."]

## 3. Monitoring Summary
[Each signal on its own line: Metric · Current value · Status (✅ healthy / ⚠️ degraded / 🔴 alert)]
[If unavailable: "Monitoring data unavailable — check Grafana directly."]

## 4. Blocked Items
[Tasks with no progress >24h.
 Format: [TASK-KEY] Title — Blocked since DATE — Blocker description]
[If none: "No blocked items."]

## 5. Completed Since Last Status
[Format: [TASK-KEY] Title — Completed DATE]
[If none: "No completions since last status."]
```

6. End with:
   - A one-line recommended focus for the day
   - Any open founder decisions listed as explicit questions requiring Tal's input

## Rules

- Never invent data. If a source is unavailable, say so in the relevant section.
- Never skip a section. If a section has no content, write the "If none" placeholder.
- Keep each section concise. Tal reads this in under 5 minutes.
- Oldest pending decisions surface first — urgency grows with age.
