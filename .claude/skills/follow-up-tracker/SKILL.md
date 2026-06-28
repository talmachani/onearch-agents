---
name: follow-up-tracker
description: Extract, log, and track action items and follow-ups from conversations. Use when Tal mentions a commitment, task, or action item that should be tracked, or when asked to check what follow-ups are open or overdue.
---

# Follow-up Tracker Skill

## When to Use

Invoke when:
- Tal mentions a commitment ("I'll follow up with X", "we need to check Y by Friday")
- A conversation produces action items that should be tracked
- Asked to check what follow-ups are open, due today, or overdue

## Follow-up Log

Follow-ups are tracked in `founder/follow-up-log.md`.

ID format: `FU-[NNN]` where NNN increments from the last ID in the log.

Table format:
```
| ID | Owner | Item | Due | Context | Status |
|----|-------|------|-----|---------|--------|
| FU-001 | Tal | Email John re: contract clause 4.2 | 2026-06-28 | Contract review meeting 2026-06-26 | Open |
```

Status values: `Open` · `Done` · `Cancelled`

## Steps — Add a Follow-up

1. Read `founder/follow-up-log.md` to find the next available ID.

2. Extract from the conversation:
   - **Owner**: Tal / [agent name] / [external party name]
   - **Item**: specific and concrete. Not "follow up on contract" — instead "email John Smith re: indemnification clause 4.2 before Friday's signing." One action per row.
   - **Due**: use explicit date if stated. If implied (e.g., "before Thursday's meeting"), convert to the specific date. If unclear, ask Tal before logging.
   - **Context**: one sentence explaining what triggered this follow-up.

3. Append the row to the table in `founder/follow-up-log.md`.

4. Commit: `git commit -m "track: add follow-up FU-[NNN] — [item summary]"`

5. Confirm to Tal: "Logged FU-[NNN]: [item] — due [date]."

## Steps — Check Open Follow-ups

1. Read `founder/follow-up-log.md`.

2. Filter rows where Status = `Open`.

3. Classify:
   - **Overdue**: Due < today
   - **Due today**: Due = today
   - **Upcoming**: Due > today

4. Report in this order: Overdue (🔴) → Due today (🟡) → Upcoming (⚪).

5. For each item: `FU-ID: [Item] — Owner: [name] — Due: [date] [🔴 OVERDUE / 🟡 TODAY]`

## Steps — Close a Follow-up

1. Find the row in `founder/follow-up-log.md`.

2. Change Status from `Open` to `Done` (or `Cancelled` if abandoned).

3. Commit: `git commit -m "track: close follow-up FU-[NNN] — [item summary]"`

## Rules

- One action per row. If a conversation produces 5 items, log 5 rows with 5 IDs.
- Never invent due dates without basis. If unclear, ask Tal.
- Never log vague items. If the action isn't specific enough to execute, ask Tal to clarify before logging.
- Never mark Done without Tal confirming the action was completed.
