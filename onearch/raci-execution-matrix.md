# RACI Execution Matrix

**Owner:** OneArch · **Version:** 1.0 · **Status:** Active

Applies after a decision has been made by Tal. Defines who does what for each
work type.

R = Responsible (does the work)
A = Accountable (owns quality and completeness)
C = Consulted (provides input, reviews)
I = Informed (notified of progress and outcome)

---

## Matrix

| Work type | Responsible | Accountable | Consulted | Informed |
|:----------|:------------|:------------|:----------|:---------|
| Product brief / PRD | Product Manager | Tal | UX, Architect | All |
| UX flow / wireframes | UX Designer | Product Manager | FE, QA | Tal |
| Technical design / spec | Product Architect | System Architect | BE, FE, DBA, DevOps, QA | Tal |
| API implementation | Backend Engineer | Product Architect | FE, QA, DevOps | Tal, Product |
| UI implementation | Frontend Engineer | Product Architect | UX, BE, QA | Tal, Product |
| DB migration | DBA | Product Architect | BE, DevOps, QA | Tal |
| Infra change | DevOps | System Architect | BE, DBA, QA | Tal |
| Test plan | QA Engineer | Product Manager | UX, BE, FE, DBA | Tal |
| Release packet | OneArch | Tal | All | All |
| Incident response | DevOps | System Architect | BE, DBA, QA, PA | Tal |
| Agent provisioning | OneArch | Tal | System Architect, QA | All |

## Handoff Protocol

When work transitions from one agent to another (e.g., Product Architect → Backend):

1. Accountable agent publishes the output artifact to Git.
2. Artifact is linked in the Jira task.
3. Responsible agent (next in chain) @-reads the artifact before starting.
4. If the artifact is incomplete or ambiguous, the Responsible agent raises a
   blocker in Jira and surfaces to Tal — does NOT proceed on assumptions.
