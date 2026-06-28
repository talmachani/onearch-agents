---
name: architecture-rfc
description: Write a structured architecture RFC (Request for Comments) for a significant technical change. Covers context, problem, proposed solution, alternatives, open questions, and the DACI decision record. Output is a draft for team review and Tal approval — never implemented until approved.
---

# Architecture RFC Skill

## When to Use

Invoke when:
- Proposing a change that affects more than one service or data store
- Proposing a new service, storage technology, or external dependency
- A technical approach has significant tradeoffs that require founder input
- Implementing `onearch/operating-cadence.md` Per Initiative step 2 (RFC phase)
- The System Architect or Product Architect needs to surface a technical decision via DACI

## RFC File Naming

RFCs live in `ecosystem/rfc/` as `RFC-NNN-title-in-kebab-case.md`.

To get the next RFC number: `ls ecosystem/rfc/ | sort | tail -1` and increment.

If `ecosystem/rfc/` doesn't exist yet: `mkdir -p ecosystem/rfc`.

## Steps

1. **Confirm scope.** Before writing, check:
   - `founder/decision-log.md` — is there an existing DACI decision that constrains this RFC?
   - `ecosystem/adr/` — is there an existing ADR that covers this area?
   - `onearch/agent-security-guardrails.md` — does the proposal touch any security guardrail?

2. **Draft the RFC** using this exact template. Output the full draft in your response. A session with file-write access will save it to `ecosystem/rfc/RFC-NNN-<title>.md` and commit it.

```markdown
# RFC-[NNN]: [Title]

**Date:** YYYY-MM-DD
**Author:** System Architect / Product Architect
**Status:** Draft | Under Review | Accepted | Rejected | Superseded by RFC-NNN
**Initiative:** [INIT-KEY or "N/A — cross-cutting"]
**Related ADR:** [NNNN-title or "None yet"]
**Jira:** [EPIC-KEY or "N/A"]

## Summary

[2–3 sentences: what is being proposed and why. This is the TL;DR for Tal.]

## Context and Problem Statement

[What is the current state? What problem or limitation is being addressed? Why now?
Include relevant metrics, incidents, or product requirements that motivate this change.]

## Proposal

[Describe the proposed solution in enough detail that an engineer can implement it without ambiguity.
Include: service names, data flows, API surface changes, data model changes, deployment changes.]

### Architecture Diagram (text)

```
[Service A] --request--> [Service B] --write--> [Store C]
                              |
                         [Queue D]
                              |
                         [Service E] --read--> [Store C]
```

### Key Design Decisions

- **Decision 1:** [What was decided and why — not what was rejected]
- **Decision 2:** [...]

## Alternatives Considered

### Alternative A: [Name]

**What:** [Description]
**Why rejected:** [Specific reason — not vague]

### Alternative B: [Name]

**What:** [Description]
**Why rejected:** [Specific reason]

## Risks and Mitigations

| Risk | Severity | Mitigation |
|------|----------|------------|
| [risk] | Low/Med/High/Critical | [approach] |

## Migration Plan

[How do we get from current state to proposed state? What is the rollback plan if the migration fails?
List steps in order. Flag irreversible steps explicitly.]

**Rollback:** [specific rollback procedure — not "we will roll back"]

## Open Questions

- [Q: question — owner: Name — blocking? yes/no — due: DATE]

## Reviewer Sign-off Required

- [ ] System Architect — architectural correctness
- [ ] Product Architect — product spec alignment
- [ ] Backend Engineer — implementability
- [ ] DBA — data model correctness (if applicable)
- [ ] DevOps — deployment feasibility (if applicable)
- [ ] Tal — final approval (REQUIRED before implementation begins)
```

3. **Open a DACI record** if the RFC introduces a decision that requires Tal's explicit input. Use the `decision-log` skill to draft the record in `founder/decision-log.md`.

4. **Present to Tal.** End every RFC with:
   > "This RFC is a draft. Implementation MUST NOT begin until Tal explicitly approves this RFC."
   >
   > **Founder Decision Required:** YES — approve RFC-[NNN] and authorize implementation, or redirect.

5. **Hand off for commit.** Present the complete RFC draft to Tal. When Tal approves the draft, it will be saved to `ecosystem/rfc/RFC-NNN-<title>.md` and committed with:

```
rfc: draft RFC-NNN — <short title> (pending Tal approval)
```

Note: Architect agents operate at Level 2 (drafts only). File creation and git commit are performed in the main session after Tal reviews the draft.

## Rules

- Never begin implementation of an RFC before Tal explicitly approves it.
- Every RFC that changes service boundaries or adds a new data store MUST also produce an ADR.
- Every risk rated High or Critical requires a mitigation before the RFC is submitted for review.
- Never invent metrics or incident data. If evidence is unavailable, say "Assumption — not yet measured."
- Every open question must have an owner, a blocking flag, and a due date.
- The rollback plan must be specific — "we will roll back" with no procedure is not acceptable.
