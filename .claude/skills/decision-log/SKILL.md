---
name: decision-log
description: Record a new founder decision or resolve a pending one in founder/decision-log.md using the DACI format. Use when Tal makes a decision affecting roadmap, priority, architecture, release, or business direction, or when a new decision needs to be drafted for Tal's review.
---

# Decision Log Skill

## When to Use

Invoke when:
- Tal makes a decision that should be recorded permanently
- A pending decision in `founder/decision-log.md` gets a resolution
- A new decision needs to be drafted for Tal's review

## Decision ID Format

`D-[PRODUCT]-[NNN]` where:
- `NG` = NewsGraph
- `PL` = Pairlio
- `EC` = Ecosystem (cross-product)
- `NNN` = three-digit incrementing number (001, 002, …)

To get the next ID: read `founder/decision-log.md`, find the highest existing number for the product, increment by 1.

## Steps — Add a New Decision

1. Read `founder/decision-log.md` to find the next available ID.

2. Append the new entry to the `## Pending Decisions` section using this exact template:

```markdown
### [D-ID]: [Decision Title]

**Date:** YYYY-MM-DD
**Driver:** [agent name or "Tal"]
**Approver:** Tal
**Contributors:** [comma-separated list of agents]
**Informed:** [comma-separated list of agents and artifacts to update]
**Status:** Pending

#### Context
[2–4 sentences: what situation or question triggered this decision]

#### Options Considered

**Option A: [Name]**
- Pros: [specific advantage]
- Cons: [specific disadvantage]
- Risk: Low / Medium / High

**Option B: [Name]**
- Pros: [specific advantage]
- Cons: [specific disadvantage]
- Risk: Low / Medium / High

#### Recommendation
[One paragraph: agent's recommended option with clear rationale]

#### Decision
[Tal: fill in]

#### Rationale
[Tal: fill in]

#### Consequences
- [What changes as a result of this decision]
- [What artifact updates are required]

#### Review Date
[When this decision should be revisited, if applicable — or "N/A"]
```

3. Commit: `git commit -m "decision: draft [D-ID] — [short title] (pending Tal decision)"`

4. Surface to Tal: present the options and recommendation; ask Tal to confirm or adjust.

## Steps — Resolve a Pending Decision

1. Find the decision entry in `founder/decision-log.md`.

2. Apply exactly these changes:
   - `**Status:** Pending` → `**Status:** Decided`
   - `#### Decision\n[Tal: fill in]` → `#### Decision\n[Tal's chosen option and any notes]`
   - `#### Rationale\n[Tal: fill in]` → `#### Rationale\n[Tal's reasoning]`

3. Commit: `git commit -m "decision: record [D-ID] — [short description of what was decided]"`

4. Identify the Informed list from the decision record. Notify those agents (surface in the next morning status or directly if urgent).

## Rules

- MUST NOT mark Status: Decided without Tal explicitly confirming in the same session.
- MUST increment the ID correctly — never reuse a D-ID.
- MUST commit after every add or resolve action.
- Every decided decision MUST have both `#### Decision` and `#### Rationale` filled in (not `[Tal: fill in]`).
- After resolving a decision, always surface the Informed list so relevant agents can update their context.
