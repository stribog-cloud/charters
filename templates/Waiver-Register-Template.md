---
title: "<Project Name> Waiver Register"
created: 2026-05-04
updated: 2026-05-04
type: project/waiver-register
status: governing-reference
tags: [charter, governance, stribog]
project: <project-id>
version: "1.0.0"
revision: 1
last_updated: YYYY-MM-DD
parent_moc: "[[MOC - Stribog Governance]]"
---


# <Project Name> — Waiver Register

> The authoritative record of every active and historical waiver against the Stribog charter set for this project.

---

> **Template usage.** Replace every `<placeholder>`. Italicized guidance paragraphs are removed from the live document. The waiver register is append-only: closed waivers are not deleted, they are marked `closed` and retained for audit history.
>
> The Compliance Annex §7 holds the at-a-glance summary of currently active waivers. This document holds the full per-waiver record. The two are kept consistent at every Compliance Annex review.

---

## 0. TL;DR

*A reader auditing this project should know within 30 seconds how many active waivers exist, against what clauses, and when each is scheduled to close.*

| Status | Count |
|--------|-------|
| Active | <N> |
| Active and overdue (past expiry) | <N> |
| Closed in the last audit cycle | <N> |
| Total recorded since project inception | <N> |

If empty: *No waivers have been filed against this project as of revision N.*

## 0.1 What a Waiver Is

A waiver is a written, scoped, owned, dated record that a specific clause of a Stribog governing document does not apply (or applies in a modified form) to a specific scope within this project. A waiver does not weaken the charter; it records a known, time-bound exception that the project's Charter Owner has approved.

The full definition lives in the Stribog Glossary under `Waiver`, and the discipline is in Engineering Charter §13 and Charter Governance §6.3.

## 0.2 What a Waiver Is Not

A waiver is not:

- a way to permanently lower a charter floor (it must have an expiry or review date)
- a substitute for fixing the underlying issue (it tracks the issue toward closure)
- something that can exist only in chat or memory (it must be in this register)
- something an agent can grant itself (it must be approved by the Charter Owner)
- something that excuses a clause for the entire project (it has explicit scope)

## 1. Active Waivers

*Each active waiver gets its own §1.N record. A waiver record includes every field defined in §3 below.*

### 1.1 W-NNNN — <Short title>

| Field | Value |
|-------|-------|
| Waiver ID | W-NNNN |
| Status | active |
| Filed | YYYY-MM-DD |
| Filed by | <Charter Owner / Project Compliance Owner> |
| Approved by | <Charter Owner> |
| Approved on | YYYY-MM-DD |

**Clause being waived:**

<Document name and section number, e.g. "Universal Stribog Engineering Charter §5.4 — Coverage Mandate (96% floor)".>

**Scope:**

<Exactly what is waived and what is not. Repository paths, subsystems, time windows, customer environments. Do not waive more than is necessary.>

**Reason:**

<Why this waiver was filed. Concrete; not "convenience.">

**Compensating Controls:**

*The substitute discipline that protects the project while the underlying clause is waived.*

- <Compensating control>
- <Compensating control>

**Expiry / Review Date:**

YYYY-MM-DD

**[[remediation]] Plan:**

<The path to closure. What must happen for this waiver to no longer be needed.>

**Tracking:**

<Beads issue, ticket, or other durable work item tracking the remediation.>

**Review Notes:**

*Each Compliance Annex review touches this waiver and records a one-line note.*

- YYYY-MM-DD: <reviewer note>
- ...

### 1.2 W-NNNN — <Short title>

*Repeat the §1.1 pattern for each active waiver.*

## 2. Closed Waivers

*Closed waivers are retained for audit history. A closed waiver records its closure reason and the date.*

### 2.1 W-NNNN — <Short title> [closed]

| Field | Value |
|-------|-------|
| Waiver ID | W-NNNN |
| Status | closed |
| Filed | YYYY-MM-DD |
| Closed | YYYY-MM-DD |
| Closure reason | <fixed / superseded by clause change / scope expired / waiver no longer needed> |

**Clause that was waived:**

<Document name and section number.>

**Scope:**

<As filed.>

**Reason it was filed:**

<As filed.>

**Resolution:**

<How the underlying issue was resolved. References to the closing change (commit, PR, beads issue, audit-round record).>

### 2.2 W-NNNN — <Short title> [closed]

*Repeat the §2.1 pattern for each closed waiver.*

## 3. Required Waiver Fields

*Reference for §1 and §2 entries. Every waiver record must include every field below. Missing fields are not permitted.*

| Field | Required | Notes |
|-------|----------|-------|
| Waiver ID | yes | Project-scoped, monotonic. Convention: `W-NNNN`. |
| Status | yes | One of: `active`, `closed`. |
| Filed (date) | yes | When the waiver was filed. |
| Filed by | yes | Operator or role that filed the waiver. |
| Approved by | yes | Charter Owner. |
| Approved on (date) | yes | When the Charter Owner approved. |
| Clause being waived | yes | Explicit document and section number. |
| Scope | yes | What is waived; what is not. |
| Reason | yes | Why this waiver was filed. |
| Compensating controls | yes | What protects the project while the clause is waived. |
| Expiry or review date | yes | Every waiver has one. Indefinite waivers are forbidden. |
| Remediation plan | yes | The path to closure. |
| Tracking | yes | Durable work item tracking remediation. |
| Review notes | yes | Updated at every Compliance Annex review. |
| Closed (date) | when closed | Date of closure. |
| Closure reason | when closed | One of: `fixed`, `superseded by clause change`, `scope expired`, `waiver no longer needed`. |
| Resolution | when closed | How the issue was resolved. |

## 4. Review Cadence

The waiver register is reviewed:

- at every Compliance Annex review (per Charter Governance §5.3)
- before every charter audit-round
- when any active waiver reaches its expiry or review date
- when the underlying clause changes through the charter change cycle

A waiver past its expiry date without review is itself non-compliant. Stale waivers either close, renew with a new review date, or escalate as audit findings.

## 5. Anti-Patterns

The following waiver-register anti-patterns are forbidden:

- waivers without an expiry or review date
- waivers whose scope is "the whole project"
- waivers without compensating controls
- waivers that are filed to avoid fixing an issue that could be fixed
- waivers that exist only in the Compliance Annex §7 summary but not in this full register
- waivers that exist only in this register but are not surfaced in the Compliance Annex §7 summary
- waivers approved by anyone other than the Charter Owner
- waivers whose remediation plan is "we'll see"
- closed waivers that are deleted instead of marked `closed`
- waivers that are renewed silently (renewal is a deliberate review event with notes)

---

## 6. Revision History

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 1.0.0 | 1 | YYYY-MM-DD | Initial register for `<project>`. |
| ... | | | |

---
