# Artifact Lifecycle Policy

**Owner:** OneArch · **Version:** 1.0 · **Status:** Active

---

## Artifact Types

| Type | Format | Location | Loaded by |
|------|--------|----------|-----------|
| Subagent | Markdown + YAML frontmatter | `.claude/agents/` | Claude Code (auto-delegated) |
| Agent Skill | `SKILL.md` + optional resources | `.claude/skills/<name>/` | Claude Code (on trigger) |
| MCP server | Server process/URL + auth | `.claude/.mcp.json` | Claude Code (on session start) |
| Org charter | Markdown | `CLAUDE.md` at root | Claude Code (always in context) |
| Governance doc | Markdown | `onearch/` | @-referenced by agents |
| Initiative README | Markdown | Git (per initiative path) | @-referenced by Jira link |
| PRD | Markdown | `products/<product>/` | @-referenced by agents |
| ADR | Markdown | `ecosystem/adr/` | @-referenced by agents |
| RFC | Markdown | `ecosystem/` | @-referenced by agents |
| Decision record | Markdown | `founder/decision-log.md` | Always @-referenced for decisions |

## Linking Rules (Non-Negotiable)

- Every artifact MUST link to exactly one primary initiative.
- Every task SHOULD produce or update ≥1 artifact.
- Every commit/PR MUST reference the Jira task key in the commit message.
- A PR description MUST reference both the task key and the initiative key.

Commit message format:
```
[TASK-KEY] Short description of change

Initiative: [INIT-KEY]
Artifact: path/to/artifact.md
```

## Initiative Closure Checklist

An initiative MUST NOT be closed until ALL of the following are true:
- [ ] All challenges marked Done, Cancelled, or explicitly waived by Tal
- [ ] All tasks marked Done, Cancelled, or explicitly waived by Tal
- [ ] All required artifacts are published to Git and linked in Jira
- [ ] QA release-risk review complete and attached to release packet
- [ ] Release packet approved by Tal
- [ ] OneArch morning status reflects the closed initiative

## Artifact Ownership

| Artifact | Created by | Reviewed by | Approved by |
|----------|-----------|-------------|------------|
| PRD | Product Manager | System Architect, UX | Tal |
| ADR | System Architect or Product Architect | Relevant engineers | Tal (for breaking decisions) |
| RFC | Any agent | System Architect | Tal |
| Tech spec | Product Architect | BE/FE/DBA/DevOps/QA | Tal |
| Migration plan | DBA | BE, DevOps | Tal |
| Release packet | OneArch | QA, DevOps | Tal |
| Decision record | Driver agent | Relevant contributors | Tal |

## Artifact Freshness

OneArch MUST flag artifacts as stale if:
- A governance doc has not been reviewed in >90 days.
- An initiative artifact references a closed Jira task as "open."
- A decision record references an artifact that has since changed substantially.
