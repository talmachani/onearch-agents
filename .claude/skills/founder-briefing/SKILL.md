---
name: founder-briefing
description: Compile a concise, decision-oriented briefing for Tal covering open decisions, active work, flagged items, and follow-ups due. Use before meetings, at the start of the day, or when Tal needs a current-state snapshot. Maximum 1 page.
---

# Founder Briefing Skill

## When to Use

Invoke when:
- Tal asks for a briefing, summary, or "what do I need to know"
- Preparing for a meeting or review session
- Starting the workday (pairs with `morning-status` for full daily picture — morning-status covers work queue and monitoring; this covers decisions and follow-ups)
- Tal needs context on a specific topic before a conversation

## Steps

1. Read `founder/decision-log.md` — collect Status: Pending entries. Note Date for urgency ranking.

2. Read `founder/roadmap-decisions.md` — note current P0/P1/P2 focus.

3. Read `founder/follow-up-log.md` — collect Status: Open entries. Flag any where Due < today as overdue.

4. Read `founder/vision.md` — keep product direction in mind for the "Recommended Focus."

5. Query Jira via Atlassian MCP if available — active work items and any blockers >24h. If unavailable, note the gap.

6. Compose the briefing using this exact format — do not add or remove sections. Keep each section to 3–5 lines maximum:

```
# Founder Briefing — [DATE] [Morning / Pre-[Meeting name] / Ad-hoc]

## Must Decide Today
[D-ID: Title — one-sentence summary of what decision is needed, ranked by urgency (oldest first)]
[If none: "No pending decisions."]

## In Progress
[[INIT-KEY or short label] Initiative name — current status, next milestone or blocker]
[If none: "No active initiatives."]

## Flagged for Attention
[One line each: blocked items >24h, open risks, anything unusual]
[If none: "Nothing flagged."]

## Follow-ups Due
[FU-ID: Item — Owner: Name — Due: DATE [🔴 OVERDUE if past due]]
[If none: "No follow-ups due today."]

## Recommended Focus
[One sentence: where Tal should spend time today, given the above.]
[If none: "Continue monitoring existing decisions and follow-ups."]
```

7. If this is a pre-meeting briefing, append one additional section:

```
## Context for [Meeting Name / Topic]
[Relevant decisions (from decision-log.md), artifacts (file paths), and background that Tal needs for this specific meeting. Max 5 bullet points.]
```

## Rules

- Maximum 1 page. If more content exists, summarize and offer "Want more detail on X?"
- Never skip sections. If a section has no content, write the "If none" placeholder.
- Briefings are for Tal's decision-making, not status reports for others. Tight, actionable, decision-oriented.
- "Recommended Focus" is always a suggestion — frame it as "I'd suggest focusing on…" not "You should…"
- Never invent data. If a source is unavailable, say so in the relevant section.
