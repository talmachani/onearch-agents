# Founder-Led DACI Decision Framework

**Owner:** OneArch · **Version:** 1.0 · **Status:** Active

Used for every decision that affects roadmap, priority, architecture, release,
or business direction. Tal is the Approver for all such decisions.

---

## DACI Roles

| Role | Who | Responsibility |
|------|-----|---------------|
| Driver | The agent preparing the brief | Gather analysis, write the decision record, surface options |
| Approver | Tal (always, for roadmap/priority/release/architecture/business) | Final decision |
| Contributors | Agents supplying analysis, risk, estimates, impact | Provide structured input |
| Informed | Agents who must update their work after the decision | Acknowledge and update artifacts |

## Decision Record Template

File each decision as `founder/decision-log.md` entry using this format:

```markdown
### [D-ID]: [Decision Title]

**Date:** YYYY-MM-DD
**Driver:** [agent or Tal]
**Approver:** Tal
**Contributors:** [list of agents]
**Informed:** [list of agents/artifacts to update]
**Status:** Pending | Decided | Superseded

#### Context
[What situation or question triggered this decision]

#### Options Considered

**Option A: [Name]**
- Pros: ...
- Cons: ...
- Risk: Low / Medium / High

**Option B: [Name]**
- Pros: ...
- Cons: ...
- Risk: Low / Medium / High

#### Recommendation
[Agent's recommended option with rationale]

#### Decision
[Tal's decision — filled in by Tal or OneArch after Tal confirms]

#### Rationale
[Why this option was chosen]

#### Consequences
- [What changes as a result]
- [What artifact updates are required]

#### Review Date
[When this decision should be revisited, if applicable]
```

## Mandatory Decision Categories

These categories ALWAYS require a DACI record:

| Category | Example | Approver |
|----------|---------|---------|
| Roadmap | "Build NewsGraph ingestion before Pairlio MVP" | Tal |
| Priority change | "Move P0 from X to Y" | Tal |
| Architecture | "Use Neo4j vs Postgres-only for graph storage" | Tal |
| Scope | "Cut feature X from MVP" | Tal |
| Release | "Approve v0.1.0 for production" | Tal |
| Agent provisioning | "Promote agent from Sandbox to Active" | Tal |
| Business trade-off | "Partner with X vs build internally" | Tal |

## Pending Decisions to Create (from spec §31)

These decisions MUST be created as the first real DACI records:

- **D-NG-001:** NewsGraph MVP sequence — pipeline-first vs UI-first
- **D-NG-002:** Graph-writer pattern vs direct Neo4j writes
- **D-PL-001:** Pairlio MVP timing vs NewsGraph-first focus
