---
name: product-discovery
description: Write a structured product discovery brief for a new initiative or feature. Covers problem statement, target user, solution hypothesis, risks, success metrics, and open questions. Output is a draft artifact for Tal approval — never published directly.
---

# Product Discovery Skill

## When to Use

Invoke when:
- Starting a new initiative (per `onearch/operating-cadence.md` Per Initiative step 1)
- Tal asks "what problem does X solve?" or "should we build Y?"
- A user story has been proposed but the underlying problem isn't validated
- A discovery brief is needed before PRD writing begins

## Steps

1. **Clarify scope.** Before writing, confirm with Tal (or from context):
   - Which product: NewsGraph or Pairlio
   - The initiative or feature name
   - Any constraints already decided (check `founder/decision-log.md` and `founder/roadmap-decisions.md`)

2. **Gather context.** Read:
   - `founder/vision.md` — product vision and direction
   - `founder/roadmap-decisions.md` — current priority order and non-goals
   - `founder/decision-log.md` — relevant decided decisions that constrain scope
   - Any existing PRDs in `products/<product>/` for context on prior scoping

3. **Write the discovery brief** using this exact format:

```markdown
# Discovery Brief: [Initiative Name]

**Version:** 1.0 · **Status:** Draft · **Owner:** Product Manager · **Approver:** Tal
**Product:** NewsGraph / Pairlio / Ecosystem
**Date:** YYYY-MM-DD

## Problem Statement

[2–4 sentences answering: What problem exists? Who has it? What is the evidence this is a real problem? What happens if we don't solve it?]

## Target User

**Role:** [specific role — e.g., "investigative journalist at a mid-sized outlet"]
**Context:** [when they encounter this problem, what tools they currently use]
**Pain Point:** [specific friction — concrete, not generic]

## Solution Hypothesis

[1–2 sentences: "We believe that [building X] for [target user] will [achieve Y] because [reason Z]."]

This is a hypothesis, not a commitment. It should be falsifiable.

## What Success Looks Like

| Metric | Target | Measurement Method |
|--------|--------|--------------------|
| [metric] | [value] | [how we will measure] |

## What We Are Not Solving (Non-Goals)

- [Explicitly out of scope — prevents scope creep]

## Risks

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| [risk] | Low/Med/High | Low/Med/High | [approach] |

## Open Questions

- [Q: question that must be answered before we can write the PRD — owner: Name — due: DATE]

## Dependencies

- [Dependency: what it is, who owns it, what we need from them, current status]

## Recommendation

[1 paragraph: should we proceed? If yes, what is the proposed initiative scope? If no, why not and what instead?]
```

4. **Present to Tal.** End every discovery brief with:
   > "This is a draft discovery brief. Founder approval required before PRD writing begins."
   >
   > **Founder Decision Required:** YES — approve this discovery brief and authorize PRD phase, or redirect scope.

## Rules

- Never write a PRD or user stories during the discovery phase — discovery comes first, PRD comes second.
- Never invent user research. If evidence is unavailable, say "Assumption — no data yet" and flag it as a risk.
- Every non-goal must be explicit. Implicit non-goals become scope creep.
- Every open question must have an owner and a due date.
- Always check `founder/decision-log.md` before proposing anything that touches an already-decided architecture decision.
