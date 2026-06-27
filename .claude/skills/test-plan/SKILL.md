---
name: test-plan
description: Write a structured test plan for an initiative or feature. Covers unit, integration, API, and E2E test scope derived from PRD acceptance criteria. Output is a draft test plan for PM and Tal review. Used by QA Engineer before implementation begins.
---

# Test Plan Skill

## When to Use

Invoke when:
- A new initiative enters the Implementation phase (after tech spec is approved)
- Asked to write a test plan for a feature or initiative
- Implementing `onearch/operating-cadence.md` Per Initiative step 5 (QA phase)

## Steps

1. **Read the PRD acceptance criteria.** For every user story in the PRD, extract:
   - The testable condition (what must be true)
   - The actor (who does the action)
   - The observable outcome (what the system must show or do)

   If any acceptance criterion is not testable as written, flag it to the Product Manager before writing the test plan.

2. **Classify tests by layer.** For each acceptance criterion, determine which test layer covers it:

   | Layer | Tool | Coverage focus |
   |-------|------|----------------|
   | Unit | pytest | Single function/class, mocked dependencies |
   | Integration | pytest | Service + real DB (no mocks) |
   | API | Hurl | HTTP contract, request/response, status codes |
   | E2E | Playwright | User journey in a real browser |
   | Regression | (existing suite) | No existing test must break |

3. **Write the test plan** using this exact format:

```markdown
# Test Plan: [Initiative Name]

**Version:** 1.0 · **Status:** Draft · **Owner:** QA Engineer · **Approver:** Product Manager + Tal
**PRD:** [link to PRD in Git]
**Tech Spec:** [link to tech spec in Git]
**Initiative:** [INIT-KEY]

## Scope

**In scope:** [What this test plan covers — feature or initiative name, specific user stories]
**Out of scope:** [Explicitly excluded — prevents test creep]

## Acceptance Criteria Coverage

| US-ID | Acceptance Criterion | Test Layer | Test ID | Status |
|-------|---------------------|------------|---------|--------|
| US-001 | [criterion text] | Unit / Integration / API / E2E | TC-001 | Not started |

## Test Cases

### TC-001: [Test Case Title]

**User Story:** US-001
**Layer:** Unit / Integration / API / E2E
**Priority:** Critical / High / Medium / Low

**Preconditions:**
- [What must be true before this test runs]

**Steps:**
1. [Action]
2. [Action]

**Expected Result:** [What the system must do or show]

**Test command:**
```bash
# Unit/Integration
uv run pytest tests/path/test_file.py::test_function -v

# API (Hurl)
hurl tests/api/endpoint.hurl --variable base_url=http://localhost:8000

# E2E (Playwright)
npx playwright test tests/e2e/feature.spec.ts --headed
```

---

## Regression Scope

[List the existing test files that must continue passing after this change:]
- `tests/unit/test_<related_module>.py`
- `tests/e2e/<related_feature>.spec.ts`

## Risk Areas

[Areas where test coverage is thin or the feature touches complex logic:]
- [Risk 1: description — mitigation: what extra testing we do]

## Exit Criteria

All of the following must be true before QA signs off on the release:
- [ ] All Critical and High priority test cases: PASS
- [ ] Backend coverage ≥ 80%
- [ ] Zero open Critical or High severity bugs
- [ ] Regression suite: no new failures
- [ ] Release-risk contract produced and presented to Tal
```

4. **Flag any untestable acceptance criteria.** If any user story criterion cannot be mapped to a concrete test case, stop and surface it to the Product Manager before proceeding:
   > "Acceptance criterion [US-00N: criterion text] is not testable as written. Surfacing to PM for clarification before test plan is complete."

5. **Present to PM and Tal** with:
   > "Test plan draft complete. PM approval required before QA execution begins."

## Rules

- Every acceptance criterion from the PRD must map to at least one test case — no orphan criteria.
- Critical and High priority test cases must have explicit test commands.
- Never skip the regression scope — existing passing tests must not regress.
- A test plan with untestable acceptance criteria is incomplete — surface to PM before proceeding.
- The exit criteria section must be present and specific — "all tests pass" is not specific enough.
