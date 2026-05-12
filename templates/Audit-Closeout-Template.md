---
title: "<Subject> Audit Closeout"
created: 2026-05-04
updated: 2026-05-04
type: project/audit-closeout
status: governing-reference
tags: [charter, governance, runbook, stribog]
project: <project-id>
version: "1.0.0"
revision: 2
last_updated: YYYY-MM-DD
audit_subject: <e.g. Phase 3 closeout, v0.5.0 release, Q2-2026 charter audit>
audit_round: <integer or named round>
parent_moc: "[[MOC - Stribog Governance]]"
---


# <Subject> Audit Closeout

> Audit closeout for <subject>. This document records the verdict, the criteria evaluated, the findings, the remediations, and the residual risks at the time the audit closes.

---

> **Template usage.** Replace every `<placeholder>`. Italicized guidance paragraphs are removed from the live document. Audit closeouts are append-only after ratification: subsequent audits produce new closeout documents that supersede or extend prior ones.

---

## 0. Verdict

*The audit's bottom line, stated plainly. One of: `pass`, `pass-with-remediation`, `pass-with-deferred-findings`, `fail`. The verdict is supported by the rest of the document; it is not a placeholder for "we did our best."*

| Field | Value |
|-------|-------|
| Verdict | <pass / pass-with-remediation / pass-with-deferred-findings / fail> |
| Audit subject | <what was audited> |
| Audit round | <round identifier> |
| Audit window | <YYYY-MM-DD to YYYY-MM-DD> |
| Auditor | <Charter Owner or designated auditor> |
| Reviewer | <Reviewer name or role> |

## 0.1 Verdict Summary

*Two or three paragraphs describing the verdict. What was found, what was fixed during the audit, what remains open, and whether the subject is fit for its declared purpose at audit close.*

<Summary.>

## 1. Audit Scope

*What was in scope. Repository paths, document set, system surface, time window, customer engagement. Anything material to the subject must be either explicitly in scope or explicitly noted as out of scope with rationale.*

### 1.1 In Scope

- <Item>
- ...

### 1.2 Out of Scope

- <Item> — <reason for exclusion>
- ...

## 2. Audit Criteria

*The checklist the audit was performed against. Each criterion is concrete and verifiable. Criteria that depend on subjective judgment are explicitly marked.*

| # | Criterion | Source | Pass / Partial / Fail |
|---|-----------|--------|-----------------------|
| C1 | <Criterion> | <e.g. Engineering Charter §5.4> | <result> |
| C2 | <Criterion> | <source> | <result> |
| ... | | | |

## 3. Findings

*Each finding is recorded with a unique identifier, a severity, a description, and a [[remediation]] status. Findings remain in the document even after they are closed, so the audit serves as a durable record.*

### Finding Severity Vocabulary

| Severity | Definition |
|----------|------------|
| Blocker | The subject cannot be declared fit for purpose without resolution. |
| Major | Material defect that should be resolved before next audit. |
| Minor | Defect that should be tracked but does not block fitness. |
| Observation | Note for future consideration; not a defect. |

### Finding Records

#### F1 — <Short title>

| Field | Value |
|-------|-------|
| Severity | <Blocker / Major / Minor / Observation> |
| Source | <which criterion or governing clause this maps to> |
| Status | <Open / In progress / Fixed / Deferred / Closed-no-action> |

**Issue:**

<Description of the finding. What is wrong, where it is wrong, what the impact is.>

**Resolution:**

<What was done. Code change, document change, configuration change, waiver filed. Reference commits, PRs, beads issues, or other durable artifacts.>

**Verification:**

<How the resolution was verified.>

#### F2 — <Short title>

*Repeat the F1 pattern for each finding.*

## 4. Remediations Applied During Audit

*Findings closed during the audit window. Useful as a quick survey for readers who want to know what changed as a result of the audit itself.*

| Finding | Resolution Summary |
|---------|--------------------|
| F1 | <one-line resolution> |
| ... | |

## 5. Deferred Findings

*Findings that are accepted into a tracked-deferral state. Each deferred finding has an owner, a remediation horizon, and either a recorded waiver against the underlying clause or a tracked work item.*

| Finding | Owner | Horizon | Waiver / Work Item |
|---------|-------|---------|--------------------|
| F<N> | <owner> | YYYY-MM-DD | <reference> |
| ... | | | |

## 6. Validation Performed

*The verifications run during the audit. Tool runs, cross-checks, document reviews, dry-runs of critical paths. Specific commands and results, not "we ran the gates."*

| Validation | Outcome |
|------------|---------|
| <e.g. `make all` | <pass / N tests, M coverage> |
| <e.g. cross-check master reference vs implementation | <pass / drift noted under F<N>> |
| ... | |

## 7. Residual Risks

*Risks that remain at audit close, even after the verdict. The audit is honest about what it could not fully assess and where the system retains exposure. A clean audit with unstated residual risk is a less useful audit than a faithful one with named exposure.*

- <Residual risk> — <severity, monitoring posture, owner>
- ...

## 8. Recommendations

*Forward-looking recommendations for the next audit cycle, the next phase, or the project's broader posture. Recommendations are advisory; they do not bind unless ratified into the project's plan or charter.*

- <Recommendation>
- ...

## 9. Closeout Signoff

*Per Charter Governance §10, Reviewer signoff is advisory ("I have read this audit and have no blocking findings to raise"). Approval rests with the Charter Owner or Project Compliance Owner; their signoff is binding. The audit is closed when the binding signoff is recorded.*

| Role | Signoff weight | Name | Date |
|------|----------------|------|------|
| Auditor | Performs the audit | | |
| Reviewer | Advisory; surfaces blocking findings if any | | |
| Charter Owner / Project Compliance Owner | **Binding**; closes the audit-round | | |

## 10. Revision History

*Each audit-round record carries its own revision history. The first row is `1.0.0 / 1` for the initial filing. Subsequent rows record amendments (per the discipline of Charter Set Audit Round 2 §10.3 — amendments are exceptional, not routine). Each row names what changed and which finding it closes.*

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 1.0.0 | 1 | YYYY-MM-DD | Initial filing of <Subject> Audit. Verdict: <verdict>. <One-line summary of findings opened, closed, deferred>. |

---

## Template Revision History

*This section governs the template itself, not audit-round instances. Instance audit-rounds use §10 above to record their own history.*

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 1.0.0 | 1 | 2026-05-03 | Initial governing-reference release. Defined the audit-closeout contract: verdict, scope, criteria, finding records with severity vocabulary, in-round remediations, deferred findings, validation performed, residual risks, recommendations, closeout signoff with binding-vs-advisory weight. |
| 1.0.0 | 2 | 2026-05-03 | Editorial revision applied post Charter Set Audit Round 3 sign-off, surfaced during R3 final state-verification sweep. Added §10 Revision History scaffold (instance-level) so audit-round instances filed from this template carry the §Revision History section that Documentation Standard §12 mandates for governing-reference documents — a section that R2 and R3 instances filed without (resolved separately for those instances). Added this Template Revision History (template-level) to align with the pattern established by ADR, Runbook, Critique Persona, Charter Compliance Annex, and Waiver Register templates. Added `Stribog-Documentation-Standard` to `related_docs`. Closes finding F51 (Audit Closeout Template lacked Revision History — strict-pattern application of the F40 closure rule that resolved the same defect across three governing standards during R3). No normative change to the audit-closeout contract. |

---
