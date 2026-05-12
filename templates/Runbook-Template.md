---
title: "<Operation Name> Runbook"
created: 2026-05-04
updated: 2026-05-12
type: project/runbook
status: governing-reference
tags: [borg-backup, charter, governance, incident, runbook, stribog]
project: <project-id>
service: <affected service or system>
version: "1.0.0"
revision: 4
last_updated: 2026-05-03
runbook_class: <recurring / risky / time-sensitive / knowledge-bearing>
last_executed: <YYYY-MM-DD or never>
last_drilled: <YYYY-MM-DD or never>
estimated_duration: <e.g. 30 minutes>
blast_radius: <e.g. single VM / single cluster / customer environment / fleet-wide>
parent_moc: "[[MOC - Stribog Governance]]"
has_todos: true
---


# <Operation Name> Runbook

> One-sentence description of what this runbook does and when to use it.

---

> **Template usage.** Replace every `<placeholder>`. Italicized guidance paragraphs are removed from the live document. A runbook is binding once published — operators are expected to follow it as written, or to update it if reality has diverged. A runbook that has never been executed end-to-end is marked `status: design-reference` until first successful execution, after which it advances to `governing-reference`.

---

## 0. Trigger

*When does this runbook apply? Specific, observable conditions. Avoid "when needed" or "occasionally."*

This runbook is executed when:

- <Trigger condition>
- <Trigger condition>

This runbook is **not** the right runbook when:

- <Counter-condition that points to a different runbook>

## 0.1 Class and Cadence

| Field | Value |
|-------|-------|
| Class | <recurring / risky / time-sensitive / knowledge-bearing> |
| Expected cadence | <e.g. quarterly, on incident, on demand> |
| Estimated duration | <e.g. 30 minutes> |
| Blast radius | <e.g. single VM, customer environment, fleet-wide> |
| Reversibility | <fully reversible / partially reversible / irreversible (with notes)> |

## 1. Prerequisites

*What must be true before the operator begins. Each prerequisite is verifiable. The runbook does not start until every prerequisite is verified.*

- [ ] <Prerequisite> — verify by `<command or observation>`
- [ ] <Prerequisite> — verify by `<command or observation>`
- [ ] Operator has the rollback plan (§6) readable before starting
- [ ] Monitoring dashboards relevant to this operation are open
- [ ] Change record is filed in the project's durable system
- [ ] Customer notification, if required, has been sent

## 2. Safety Notes

*Warnings about the operation. What can go wrong. What is irreversible. What edge cases historically caused problems. Operators read this before §3.*

- <Warning>
- <Warning>

### 2.1 Irreversible Steps

*Steps that cannot be undone, named explicitly. The operator stops and confirms before each.*

- <Irreversible step>
- ...

### 2.2 Common Mistakes

*Mistakes seen in prior executions of this runbook. "Last time, X was forgotten and Y broke."*

- <Mistake>
- ...

## 3. Steps

*Concrete commands, in order. Each step states what is being done, the command, and the expected output or observable signal. Steps are numbered so the operator can record progress mid-execution.*

### Step 1 — <Action>

**Purpose:** <one-line purpose>

**Command:**

```<shell or language>
<command>
```

**Expected output:**

```
<expected output or signal>
```

**Verification:**

<How to confirm this step succeeded before proceeding.>

**On failure:**

<What to do if this step fails. Often: stop and execute rollback (§6).>

### Step 2 — <Action>

*Repeat the Step 1 pattern.*

### Step N — <Action>

<...>

## 4. Verification

*Post-operation verification. Distinct from per-step verification. The operation is not complete until these checks pass.*

- [ ] <Verification> — `<command or observation>`
- [ ] <Verification> — `<command or observation>`
- [ ] No new alerts have fired in the verification window
- [ ] Customer-facing behavior matches expectation
- [ ] Monitoring shows no anomalies in the relevant signals

### 4.1 Verification Window

*The window during which the verification is monitored. Short for routine changes; extends for delayed-blast-radius operations.*

Window: <e.g. 30 minutes after final step>

## 5. Post-Conditions

*The state that should exist after a successful execution. A reader inheriting the system after this runbook ran should be able to confirm post-conditions independently of the operator's account.*

- <Post-condition>
- <Post-condition>

## 6. Rollback

*The path back to the pre-operation state. Distinct from "fix forward." Rollback is the default response to verification failure.*

### 6.1 Rollback Trigger

This runbook is rolled back when:

- verification (§4) fails after the operation completes
- a step in §3 fails in a way that leaves the system in an inconsistent state
- monitoring fires alerts attributable to the operation
- operator judgment that something looks wrong

### 6.2 Rollback Steps

*Concrete rollback commands, in order. Same level of specificity as §3.*

#### Rollback Step 1 — <Action>

**Command:**

```<shell or language>
<rollback command>
```

**Verification:**

<How to confirm rollback succeeded.>

#### Rollback Step N — <Action>

<...>

### 6.3 Irreversible Components

*If parts of the operation cannot be rolled back, name them and the compensating action. "The data migration cannot be undone; if rollback is required, restore from <backup location> per <Disaster Recovery Runbook>."*

- <Irreversible component> — <compensating action>

## 7. Escalation

*Who to contact, in what order, if the operation fails or rollback also fails. For small-team engagements, this is typically the team's own escalation discipline (vendor support, customer's on-call, external advisor).*

| Failure mode | Contact | Channel |
|--------------|---------|---------|
| <e.g. provider issue> | <e.g. infrastructure-provider support> | <e.g. ticket portal> |
| <e.g. customer-affecting> | <e.g. customer on-call> | <e.g. agreed escalation path> |

## 8. Change Record

*The change record this runbook execution is associated with. The runbook does not run without a change record open.*

| Field | Value |
|-------|-------|
| Change ID | <to be filled by operator at execution time> |
| Operator | <who is executing> |
| Approver (if required) | <who approved> |
| Started at | <UTC timestamp> |
| Completed at | <UTC timestamp> |
| Outcome | <success / rolled back / partial> |

## 9. Drill Log

*Record of test executions of this runbook against non-production targets. The first entry is dated when the runbook was first drilled; subsequent entries record drift discovered during drills and the corresponding runbook updates.*

| Date | Target | Outcome | Notes |
|------|--------|---------|-------|
| YYYY-MM-DD | <e.g. dev cluster> | <pass / partial / fail> | <observations, runbook updates> |
| ... | | | |

## 10. Revision Notes

*Why the most recent revision changed. Each revision should leave a one-line note here, even if the revision was editorial.*

- **rev N (YYYY-MM-DD):** <what changed and why>
- **rev N-1 (YYYY-MM-DD):** ...

---

## Template Revision History

*This section governs the template itself, not runbook instances. Instance runbooks use §10 above.*

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 1.0.0 | 1 | 2026-05-03 | Initial release. Defined the runbook contract (trigger, prerequisites, safety notes, steps, verification, post-conditions, rollback, escalation, change record, drill log). |
| 1.0.0 | 2 | 2026-05-03 | Editorial revision applied during Charter Set Audit Round 3 closeout. Front-matter `status` corrected from `design-reference` to `governing-reference` to match the template's actual canon role at v1.0.0 (consistency with ADR, Audit Closeout, Charter Compliance Annex, Waiver Register, Critique Persona). Added this Template Revision History section distinct from §10 instance-revision notes. Closes Round 3 finding F39 (template status inconsistent with v1.0.0 canon role). No normative change.

---
