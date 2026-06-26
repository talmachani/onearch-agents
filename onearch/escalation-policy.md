# Escalation Policy

**Owner:** OneArch · **Version:** 1.0 · **Status:** Active

---

## When Agents MUST Escalate to Tal

1. **Scope expansion detected** — the approved action would affect more than what was discussed.
2. **Unexpected failure mode** — not covered by the current runbook or context.
3. **New risk discovered** — a risk not surfaced in the initial recommendation.
4. **Irreversible action** — the action cannot be undone and was not explicitly approved as such.
5. **Agent conflict** — two agents have conflicting recommendations on the same decision.
6. **Security guardrail triggered** — any of the 8 guardrails in `agent-security-guardrails.md`.
7. **Blocked >24h** — a task is blocked on external input for more than one day.
8. **Stale decision** — a decision is needed but no DACI record exists and work cannot proceed.

## Escalation Format

Escalations MUST be concise, decision-oriented, and bundled. Format:

```
## Escalation: [Brief Title]

**Priority:** P0 (immediate) / P1 (today) / P2 (this week)
**From Agent:** [name]
**Trigger:** [which condition from the list above]

**Situation:** [2–3 sentences — what happened]
**Risk if not addressed:** [specific consequence]
**Options:**
  A. [Option A] — Risk: [level]
  B. [Option B] — Risk: [level]
**Recommendation:** [A or B, with reason]
**Founder Decision Required:** [the exact question Tal needs to answer]
```

## Bundling Rule

Agents MUST NOT send individual escalations per issue. Non-urgent escalations
(P2) are bundled into the morning status. P1 escalations are sent at end of day.
P0 escalations are sent immediately.

OneArch is responsible for deduplicating and formatting the escalation bundle.

## What Is NOT an Escalation

- Routine status updates → morning status
- Questions with an obvious answer in the governance docs → read the doc first
- Requests for permission to do something already authorized in the autonomy model
- Progress reports → Jira task updates

## After Escalation

OneArch logs every escalation in `founder/decision-log.md` as a DACI record
(Status: Pending). After Tal decides, OneArch:
1. Updates the DACI record (Status: Decided).
2. Notifies all Informed agents.
3. Unblocks the task.
