# Agent Tool Permission Matrix

**Owner:** OneArch · **Version:** 1.0 · **Status:** Active

Referenced by: All `.claude/agents/*.md` `tools:` frontmatter

Y = allowed · Draft = Level-2 draft only (must present to Tal before executing)
Approval = Level-3, explicit per-action approval required · No = denied

---

## Matrix

| Tool / Action | PM | UX | Arch | BE | FE | DBA | DevOps | QA | PA | OneArch |
|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Read artifacts (Git, Jira, docs) | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y |
| Write/update artifacts (draft) | Draft | Draft | Draft | Draft | Draft | Draft | Draft | Draft | Draft | Draft |
| Create backlog item (Jira) | Draft | No | Draft (tech) | Draft | Draft | Draft | Draft | Draft (QA) | No | Draft |
| Change final priority | No | No | No | No | No | No | No | No | No | No |
| Create PR | No | No | No | Approval | Approval | Approval | Approval | No | No | No |
| Merge PR | No | No | No | Explicit only | Explicit only | Explicit only | Explicit only | No | No | No |
| Run tests (CI / local) | No | No | No | Y | Y | Y | Y | Y | No | Y |
| Deploy staging | No | No | No | Approval | Approval | Approval | Approval | No | No | Approval |
| Deploy production | No | No | No | No | No | No | Release gate | No | No | No |
| Send external email | No | No | No | No | No | No | No | No | Approval | No |
| Modify calendar | No | No | No | No | No | No | No | No | Approval | No |
| Access prod data | No | No | RO exception | No | No | Approval | Approval | No | No | No |
| Access secrets | No | No | No | No | No | No | Approval only | No | No | No |
| Read monitoring (Grafana/Prometheus) | No | No | No | No | No | No | Y | No | No | Y |

## Enforcement

The `tools:` list in each `.claude/agents/<agent>.md` frontmatter is the
**hard enforcement** of this matrix. Claude Code denies any tool not listed.

Example enforcement (Backend Engineer):
```yaml
tools: Read, Edit, Bash, Grep, Glob, mcp__github__create_pr, mcp__neo4j__read-cypher, mcp__postgres__query
```
Note: `mcp__github__merge_pr` is deliberately absent.

## Non-Negotiable Rules

- Agents MUST NOT grant themselves permissions not in their `tools:` list.
- Agents MUST NOT silently expand scope beyond the approved action.
- Agents MUST NOT approve their own high-risk actions.
- Production deploy MUST route through the DevOps release gate only.
- Secrets access MUST be pre-approved for each specific secret, not blanket access.
