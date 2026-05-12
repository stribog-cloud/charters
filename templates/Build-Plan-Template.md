---
title: "<Project Name> Build Plan"
created: 2026-05-04
updated: 2026-05-04
type: project/build-plan
status: governing-reference
tags: [charter, cheatsheet, governance, runbook, security, stribog]
project: <project-id>
version: "1.0.0"
revision: 2
last_updated: YYYY-MM-DD
parent_moc: "[[MOC - Stribog Governance]]"
has_todos: true
---


# <Project Name> — Build Plan

> The phased build plan for <Project Name>. Converts the master reference's architecture into milestones, gates, dependencies, and explicit acceptance criteria.

---

> **Template usage.** Replace every `<placeholder>`. Italicized guidance paragraphs are removed from the live document. The build plan is a living document until the project is feature-complete; it must remain synchronized with implementation reality.

---

## 0. TL;DR

*Phase shape and current status in one table. A reader checking on the project should know within seconds what phase is in flight, what was last completed, and what comes next.*

| Phase | Goal | Status | Acceptance |
|-------|------|--------|------------|
| Phase 1 | <Goal> | <complete / in-progress / planned> | <one-line acceptance summary> |
| Phase 2 | <Goal> | | |
| Phase N | ... | | |

## 0.1 Preconditions

*What must be true before Phase 1 can start. Master reference exists, Charter Compliance Annex is filed, toolchain is set up, repository skeleton is created.*

1. Master reference at `design-reference` or stronger
2. Charter Compliance Annex filed with pinned charter version
3. Repository skeleton with quality-gate command surface (Makefile/justfile/equivalent) exposing format, lint, test, coverage, build, vulnerability, all
4. Local hooks bootstrapped per Charter Compliance Annex
5. Waiver register exists (may be empty)
6. CI baseline configured to mirror local gates

## 1. Phase 1 — <Phase Name>

### 1.1 Goal

<One paragraph: what this phase produces and why.>

### 1.2 Scope

*What is in scope for this phase, enumerated. Each item is concrete enough to build against — not "improve X" but "implement Y with property Z."*

- <Scope item>
- <Scope item>
- ...

### 1.3 Out of Scope

*Items deliberately deferred to a later phase or to "what not to build (yet)." This list prevents scope creep during execution.*

- <Out-of-scope item> — <deferred to Phase N or Out>
- ...

### 1.4 Dependencies

*External or cross-phase dependencies. Other Stribog projects, third-party services, infrastructure prerequisites.*

- <Dependency>
- ...

### 1.5 Acceptance Criteria

*Concrete, observable criteria for declaring the phase complete. Each criterion is testable.*

- [ ] <Criterion> — verified by <test or observation>
- [ ] ...

### 1.6 Quality Gates

*Phase-level quality gates beyond the standard charter gates. Coverage targets, performance budgets, latency targets, integration checkpoints.*

| Gate | Threshold | Verification |
|------|-----------|--------------|
| Coverage | ≥ 96% (charter floor) | `<coverage command>` |
| Lint | Zero errors | `<lint command>` |
| <Phase-specific gate> | | |

### 1.7 Risks

- <Risk>: <mitigation>
- ...

### 1.8 Closeout

*The phase is closed when:*

- all acceptance criteria are met
- all quality gates pass
- documentation is synchronized to the master reference
- an audit closeout note has been recorded under `templates/Audit-Closeout-Template.md`
- the next phase's preconditions are verified

## 2. Phase 2 — <Phase Name>

*Repeat the §1 pattern for each phase.*

### 2.1 Goal

<...>

## N. Phase N — <Phase Name>

<...>

## N+1. Cross-Phase Concerns

### N+1.1 Coverage Floor Maintenance

*The 96% coverage floor applies throughout, not only at phase closeout. Any commit that reduces coverage below the floor is non-compliant. Reference the project's measurement boundary as declared in the Charter Compliance Annex.*

### N+1.2 Documentation Synchronization

*Documentation updates ship in the same change set as the implementation that requires them, per Engineering Charter §6. Deferred documentation is tracked in the work system with a defined horizon.*

### N+1.3 Architecture Stability

*Phases extend, they do not rewrite. Any phase that requires materially altering the architecture defined in the master reference must be preceded by an ADR. The burden of proof is on any rewrite.*

### N+1.4 Waiver Discipline

*Phase-specific waivers are filed in the project's waiver register before the phase begins, not retroactively. Emergency waivers issued during the phase are recorded immediately on stabilization.*

## N+2. Build Plan Definition of Done

The build plan itself is done when:

- every planned phase is in `complete` status
- every cross-phase concern has been addressed
- the master reference reflects shipped reality
- the audit-closeout records for each phase are filed
- the waiver register has been reconciled (closed waivers archived, open waivers carry expiry dates)

After build-plan completion, the project transitions to the operational lifecycle governed by the Stribog Operational Delivery Standard, where applicable.

## Template Revision History

*This section governs the template itself, not template instances. Instance documents created from this template carry their own §Revision History per Documentation Standard §12.*

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 0.1.0 | 1 | 2026-05-03 | Initial release at `design-reference` grade. Defined the phased-build-plan contract (TL;DR, preconditions, per-phase: goal, scope, out-of-scope, dependencies, acceptance criteria, quality gates, risks, closeout; cross-phase concerns; build-plan definition of done). |
| 1.0.0 | 2 | 2026-05-03 | Promoted from `design-reference` v0.1.0 to `governing-reference` v1.0.0 during Charter Set Audit Round 4. Adopted Criterion C from R4 Backlog §2: all canon templates at v1.0.0 are `governing-reference` regardless of placeholder content; `design-reference` is reserved for templates still in active drafting. The build plan template's content has stabilized; placeholder syntax is the template's defining shape rather than a draftiness signal. Added this Template Revision History to align with the pattern established by ADR, Audit Closeout, Charter Compliance Annex, Critique Persona, Runbook, and Waiver Register templates. Closes Round 4 finding F52 (template status discipline inconsistent across canon). No normative change to the template's content. |

---
