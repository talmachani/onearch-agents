# Founder Decision Log

**Owner:** Tal (decisions) + OneArch (record-keeping) · **Version:** 1.0

All roadmap, priority, architecture, release, and business decisions
are recorded here using the DACI format from `onearch/founder-led-daci.md`.

---

## Pending Decisions

### D-NG-001: NewsGraph MVP Sequence

**Date:** 2026-06-26
**Driver:** System Architect / Product Manager
**Approver:** Tal
**Contributors:** Product Architect, Backend Engineer
**Informed:** All agents
**Status:** Decided

#### Context
The NewsGraph MVP can be built pipeline-first (ingest, correlate, store — expose via
API only) or UI-first (basic graph browsing UI before the pipeline is complete).
These sequences have different risk and feedback profiles.

#### Options Considered

**Option A: Pipeline-first**
- Build ingestion → correlation → graph-writer → GraphQL API → then UI
- Pros: validates the core technical hypothesis early; API-first means UI can be swapped
- Cons: no user-visible progress for longer; harder to get founder/user feedback early
- Risk: Medium

**Option B: UI-first**
- Build basic browsing UI against a static/seed dataset → then wire live ingestion
- Pros: founder can see and evaluate the UX earlier; easier to course-correct on UX
- Cons: may build UI assumptions that break when real data arrives
- Risk: Medium

**Option C: Parallel (thin slice)**
- Build a vertical slice: one source → minimal ingestion → one graph → one UI view
- Pros: validates end-to-end quickly; real data from day one
- Cons: more coordination; easy to scope-creep
- Risk: Low–Medium

#### Recommendation
Option C (thin vertical slice) — validate the full stack with one source before
scaling either the pipeline or the UI.

#### Decision
Option C — Thin vertical slice.

#### Rationale
Validates the full stack end-to-end with real data from day one. One source, minimal ingestion, one graph, one UI view. Scale both the pipeline and the UI only after the slice is working.

---

### D-NG-002: Graph-Writer Pattern

**Date:** 2026-06-26
**Driver:** Product Architect
**Approver:** Tal
**Contributors:** Backend Engineer, DBA
**Informed:** All agents
**Status:** Decided

#### Context
Should the NewsGraph backend use a dedicated graph-writer service (receives events,
writes to Neo4j idempotently) or write directly from the ingestion pipeline to Neo4j?

#### Options Considered

**Option A: Dedicated graph-writer service**
- Pros: single write path, clear idempotency contract, testable in isolation
- Cons: extra service to maintain
- Risk: Low

**Option B: Direct pipeline writes**
- Pros: simpler initial architecture
- Cons: harder to guarantee idempotency; pipeline changes affect graph writes
- Risk: Medium

#### Recommendation
Option A — graph-writer service with explicit idempotency contract.

#### Decision
Option A — Dedicated graph-writer service.

#### Rationale
Single write path with a clear idempotency contract. Testable in isolation. Keeps ingestion pipeline changes from directly affecting graph writes.

---

### D-PL-001: Pairlio MVP Timing

**Date:** 2026-06-26
**Driver:** Product Manager
**Approver:** Tal
**Contributors:** System Architect
**Informed:** All agents
**Status:** Decided

#### Context
Should Pairlio MVP be built concurrently with NewsGraph, or after NewsGraph reaches
a stable state?

#### Options Considered

**Option A: Concurrent**
- Pros: faster time-to-market for both
- Cons: splits founder attention; shared platform built under pressure
- Risk: High

**Option B: NewsGraph-first**
- Pros: shared platform is validated before Pairlio builds on it
- Cons: Pairlio delayed
- Risk: Low

#### Recommendation
Option B — NewsGraph-first; use the learnings to build Pairlio's platform layer better.

#### Decision
Option B — NewsGraph-first.

#### Rationale
Shared platform gets validated under NewsGraph before Pairlio depends on it. Keeps founder attention focused. Pairlio benefits from learnings on the platform layer.

---

## Decided Decisions

All three founding decisions (D-NG-001, D-NG-002, D-PL-001) are recorded above with Status: Decided.
