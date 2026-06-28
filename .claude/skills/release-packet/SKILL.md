---
name: release-packet
description: Assemble the release packet for a OneArch initiative. Bundles QA sign-off, migration runbook, rollback plan, and post-deploy checklist into a Tal approval request. Output is a draft in this response — the main session saves it to releases/. Required before any production deploy.
---

# Release Packet Skill

## When to Use

Invoke when:
- An initiative has completed QA phase and the release-risk contract is ready
- Asked to "assemble the release packet" or "prepare for release"
- Implementing `onearch/operating-cadence.md` Per Initiative step 6

## Steps

1. **Gather inputs.** Collect the following before drafting:

   | Input | Where to find it |
   |-------|-----------------|
   | Initiative key + name | Jira epic or PRD frontmatter |
   | PRD link | Git path in the relevant product repo |
   | Tech spec link | Git path in the relevant product repo |
   | QA release-risk contract | Jira attachment or Git path — produced by qa-engineer |
   | Migration files (if any) | `migrations/versions/YYYYMMDD_NNN_*.py` in product repo |
   | Current deployment tag | `git describe --tags --abbrev=0` in product repo |

   If any input is missing, stop and request it:
   > "Cannot assemble release packet — missing: [item]. Please provide before proceeding."

2. **Classify QA risk.** Read the release-risk contract and extract:
   - Overall risk level: Low / Medium / High / Critical
   - QA recommendation: Release / Release with conditions / Hold
   - Known failures count and highest severity
   - Test coverage %

   If QA recommendation is "Hold", stop:
   > "QA recommends holding this release (risk level: [X]). Release packet cannot be assembled until QA signs off. Escalate to Tal if you want to override QA's recommendation — that is a Founder Decision."

3. **Classify migrations.** For each migration file:
   - Extract the name, purpose (from the docstring), and estimated run time (from the migration plan doc)
   - Flag any migration with Table-level lock risk (requires maintenance window)
   - If any migration has a table-level lock and no maintenance window is scheduled, flag to Tal in the release packet

4. **Draft the release packet.** Output the complete release packet in this response using the format below. Do not write it to a file — OneArch does not have a Write tool. The main session will save it.

   ```markdown
   # Release Packet: [Product] — [Release Name]

   **Date:** YYYY-MM-DD
   **Assembled by:** OneArch
   **Initiative:** [INIT-KEY] — [Initiative Name]
   **Status:** Draft — Pending Tal Approval

   ---

   ## What's Shipping

   [Bulleted list of user-facing changes from the PRD — what Tal will see and approve]

   - [Change 1: brief description for a non-technical reader]
   - [Change 2: ...]

   ## References

   | Artifact | Link |
   |----------|------|
   | PRD | [Git path] |
   | Tech Spec | [Git path] |
   | QA Release-Risk Contract | [Jira/Git link] |

   ---

   ## QA Sign-off

   | | |
   |-|-|
   | **Risk Level** | Low / Medium / High |
   | **QA Recommendation** | Release / Release with conditions / Hold |
   | **Test Results** | N passed, N failed (N skipped) |
   | **Coverage** | X% |
   | **Known Failures** | None / [list: severity — description — owner] |

   ---

   ## Migration Runbook

   [If no migrations: "No database migrations in this release."]

   | Migration | Purpose | Est. time | Lock risk | Rollback |
   |-----------|---------|-----------|-----------|---------|
   | YYYYMMDD_NNN_name | [one-line purpose] | < 1s / 1–10s / >10s | None / Row / Table | `alembic downgrade -1` |

   **Migration execution order:** Run in ascending order (oldest first).

   **Pre-migration:** Take a database backup before running any migration in production.

   ---

   ## Rollback Plan

   If anything goes wrong after deploy, execute in this order:

   1. **Revert deployment:**
      ```bash
      # ArgoCD sync to previous tag
      argocd app set [app-name] --revision [previous-tag]
      argocd app sync [app-name]
      ```

   2. **Roll back migrations (if any, reverse order):**
      ```bash
      alembic downgrade -1  # repeat once per migration, in reverse order
      ```

   3. **Verify rollback:**
      ```bash
      kubectl get pods -n [namespace]  # all pods Running
      # Check error rate in Grafana: [dashboard name]
      ```

   4. **Estimated rollback time:** [N minutes]

   5. **Data loss on rollback:** Yes / No — [if yes, describe what data is affected]

   ---

   ## Post-Deploy Checklist

   DevOps executes this immediately after production deploy. All items must be green within 10 minutes.

   - [ ] All pods healthy: `kubectl get pods -n [namespace]` — all Running
   - [ ] API error rate < 1% for 10 consecutive minutes (Grafana)
   - [ ] P95 API latency < 500ms for 10 consecutive minutes (Grafana)
   - [ ] Key user journey functional: [describe the one thing to manually verify]
   - [ ] No migration errors in database logs
   - [ ] No new alert firing in monitoring

   **If any checklist item fails:** Stop. Execute rollback. Escalate to Tal + System Architect immediately.

   ---

   ## Tal Approval

   - [ ] I (Tal) have reviewed this release packet and approve production deployment.

   **To approve:** Check the box above and reply "approved" or "go ahead" in this session. DevOps will not deploy without this.

   ---

   *Assembled by OneArch. Authorized by CLAUDE.md §10: "Production deploys MUST have a release packet approved by Tal."*
   *Save this packet to `releases/YYYY-MM-DD-[product]-[release-name].md` before seeking Tal's approval.*
   ```

5. **Present to Tal** with:
   > "Release packet draft complete for [INIT-KEY]. This must be saved to `releases/YYYY-MM-DD-[product]-[release-name].md` and approved by Tal before DevOps proceeds. QA risk level: [X]. Migration count: [N]."

## Rules

- Never assemble a release packet when QA recommendation is "Hold" — escalate to Tal instead.
- Never omit the Rollback Plan — a release without a pre-written rollback is not shippable.
- Never omit the Post-Deploy Checklist — DevOps uses it immediately after deploy.
- Always note data loss risk on rollback explicitly — "None" is a valid and required answer.
- Always flag Table-level lock migrations — they require a maintenance window or zero-downtime migration strategy.
