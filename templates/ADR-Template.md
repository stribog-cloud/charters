---
title: "ADR-NNNN: <Decision Title>"
created: 2026-05-04
updated: 2026-05-04
type: project/adr
status: governing-reference
tags: [charter, governance, stribog]
project: <project-id>
adr_status: proposed
version: "1.0.0"
revision: 2
last_updated: 2026-05-03
parent_moc: "[[MOC - Stribog Governance]]"
---


# ADR-NNNN: <Decision Title>

> One-sentence summary of the decision in plain language.

---

> **Template usage.** Replace every `<placeholder>`. Italicized guidance paragraphs are removed from the live document. ADRs are immutable once accepted: corrections produce a new ADR that supersedes the prior one.

---

## 0. Status

*ADRs carry **two** status fields. Front-matter `status` is the document-grade status from the Stribog vocabulary in Documentation Standard §10.1 (typically `governing-reference` for an accepted ADR, `review-draft` for a proposed one, `superseded` once another ADR replaces it, `archived` if rejected). Front-matter `adr_status` is the ADR-instance lifecycle value: one of `proposed`, `accepted`, `rejected`, `deprecated`, `superseded`. The two fields move together but live separately: `status` answers "how should readers treat this document?" and `adr_status` answers "what is the lifecycle state of the decision it records?" They map as follows: `proposed → review-draft`, `accepted → governing-reference`, `rejected → archived`, `deprecated → superseded`, `superseded → superseded`. Status changes are themselves recorded events with dates.*

| Field | Value |
|-------|-------|
| `status` (front matter) | One of: review-draft / governing-reference / archived / superseded |
| `adr_status` (front matter) | One of: proposed / accepted / rejected / deprecated / superseded |
| Decided on | YYYY-MM-DD |
| Decided by | <Charter Owner or designated approver> |
| Supersedes | <ADR-XXXX, if applicable> |
| Superseded by | <ADR-YYYY, if applicable> |

## 1. Context

*What forced this decision. The problem, the constraints, the operating reality at the time. Three or four paragraphs at most. A reader two years from now must understand why the decision had to be made, even if the surrounding system has changed since.*

<Context.>

### 1.1 Forces

*The competing concerns the decision must reconcile. Concrete tensions: speed vs. correctness, generality vs. simplicity, cost vs. capability. Name them explicitly.*

- **<Force A>**: <description>
- **<Force B>**: <description>
- **<Force N>**: ...

### 1.2 Assumptions

*What this ADR assumes to be true. If any assumption later proves false, this ADR is a candidate for supersession.*

1. <Assumption>
2. ...

## 2. Decision

*The decision itself. Stated in normative voice ("we will use X"), not as a discussion. The decision is what is recorded; the reasoning lives in §3.*

<Decision statement.>

## 3. Consequences

*What follows from the decision, both intended and accepted-as-cost. ADRs that list only positive consequences are not honest enough to act as governance.*

### 3.1 Positive

- <Consequence>
- ...

### 3.2 Negative

- <Consequence>
- ...

### 3.3 Risks and Open Questions

- <Risk or open question>
- ...

## 4. Alternatives Considered

*Every meaningfully evaluated alternative, with a one-paragraph reason for rejection. "We considered X but rejected it because Y." A future reader needs to understand which paths were explored and why each was set aside, so the same paths are not silently reopened.*

### 4.1 <Alternative A>

<Description and reason for rejection.>

### 4.2 <Alternative B>

<Description and reason for rejection.>

### 4.3 Do nothing

*Always evaluate the do-nothing option explicitly, even if it is obviously wrong. Naming it forces the decision to actually carry weight.*

<Why doing nothing was insufficient.>

## 5. Implementation Notes

*Practical guidance for implementing the decision. Not a design document — a pointer to the design document or to the affected components, with any concrete operational notes that should travel with the decision.*

- <Implementation note>
- ...

## 6. Verification

*How will the project know the decision was correctly implemented? What test, observation, or audit confirms compliance with this ADR?*

- <Verification mechanism>
- ...

## 7. Related ADRs and References

- <ADR-XXXX>: <relationship>
- <External reference>: <why it informed this decision>

## 8. Revision History

*Each ADR carries its own revision history. The first row is `1.0.0 / 1` for the initial proposal; status transitions (proposed → accepted, accepted → deprecated, etc.) are revision-bump events with dated rows.*

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 1.0.0 | 1 | YYYY-MM-DD | Initial proposal. |

---

## Template Revision History

*This section governs the template itself, not ADR instances. Instance ADRs use §8 above.*

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 1.0.0 | 1 | 2026-05-03 | Initial governing-reference release. |
| 1.0.0 | 2 | 2026-05-03 | Editorial revision applied during Charter Set Audit Round 3 closeout. Front-matter `status` corrected from `proposed` (an ADR-instance value not in Documentation Standard §10.1 vocabulary) to `governing-reference` (the template's true document-grade status). Introduced `adr_status` as a separate front-matter field for ADR-instance lifecycle. §0 prose rewritten to distinguish document-grade `status` from ADR-instance `adr_status`. Added Stribog Documentation Standard to `related_docs`. Added §8 Revision History scaffold for ADR instances and this Template Revision History for the template itself. Closes Round 3 finding F38 (template front-matter status not in §10.1 vocabulary). No normative change to ADR semantics.

---
