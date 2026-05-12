---
title: "Charter Governance"
created: 2026-05-04
updated: 2026-05-12
type: stribog/charter-governance
status: governing-reference
tags: [borg-backup, charter, governance, runbook, stribog]
version: "1.4.0"
revision: 1
last_updated: 2026-05-12
parent_moc: "[[MOC - Stribog Governance]]"
owners: [stribog-team]
---


# Charter Governance

> The binding document that governs the Stribog charter set itself. This is the meta-charter: it defines where the charter set lives, how it is versioned, how projects declare compliance against it, how it changes, how it is audited, and how it eventually sunsets.

---

## 0. TL;DR

| Area | Mandate |
|------|---------|
| Canon | The Stribog charter set is the eleven governing documents listed in §2.1 plus the templates set under `templates/`. Nothing else is governing. |
| Physical location | The canonical working source is the Stribog BrainForest charter directory. The promoted distribution source is a Stribog-controlled Git repository. |
| Versioning | Each governing document carries an independent SemVer `version` and a monotonic `revision`. Projects pin to specific `MAJOR.MINOR` versions, never to `latest`. |
| Compliance declaration | Every Stribog project declares which versions of the governing documents it is bound by, in its Charter Compliance Annex. |
| Change process | Charter changes follow a defined cycle: proposal → review-draft → ratification → governing-reference. Bypassing the cycle is forbidden. |
| Audit cadence | The charter set is audited at a defined cadence and on triggering events. Audit findings produce ratified changes or recorded waivers. |
| Sunset | Charter clauses are sunset deliberately, not by neglect. A clause that no longer applies is removed through ratified change, not by ignoring it. |

This document is binding. The other governing documents in the charter set govern the projects; this document governs the other governing documents.

## 0.1 Why This Document Exists

A charter set without a meta-charter has three predictable failure modes.

The first is **drift**. A document that lives in one place gets edited in another place and the two copies disagree. Projects pinning to "the latest version" eventually pin to whichever version they happened to read on the day they were initialized.

The second is **theatrical compliance**. Without an explicit declaration of which charter version a project is bound by, "compliance" becomes whatever the operator believes the charter currently says — which is often a reasonable approximation, but is not auditable.

The third is **silent obsolescence**. Charter clauses written for one phase of the organization continue to apply to all projects long after the underlying reality has changed. Without a sunset mechanism, charters either calcify or are quietly ignored, and quiet ignoring is the more dangerous option because it spreads.

This document exists to prevent all three. The charter set is a control system. Like any control system, it requires its own governance.

## 1. Scope

This document governs:

- the structure of the Stribog charter set
- where the charter set lives physically
- how each governing document is versioned and revised
- how projects pin to and declare compliance against the charter set
- how charter changes are proposed, reviewed, and ratified
- when and how the charter set is audited
- how charter clauses are sunset or replaced
- the roles involved in charter governance

This document does not govern projects directly. Projects are governed by the documents whose lifecycle this document defines.

## 2. Charter Set Canon

The Stribog charter set is the following governing documents and templates. Nothing else is governing.

### 2.1 Governing Documents

| Document | Role |
|----------|------|
| Universal Stribog Engineering Charter | The binding baseline for engineering discipline across all Stribog projects. |
| Stribog Documentation Standard | The form, shape, and maintenance rules for Stribog documents. |
| Stribog AI Agent Execution Standard | The binding rules for AI agents operating on Stribog projects. |
| Stribog Operational Delivery Standard | The binding rules for managed-service, infrastructure, and rolling-deployment work. |
| Stribog Security Posture Standard | The binding rules for security discipline; binds projects meeting its §0.2 applicability criteria. |
| Stribog Data and Privacy Standard | The binding rules for data classification, lifecycle, residency, and privacy; binds projects meeting its §0.2 applicability criteria. |
| Stribog User Documentation Standard | The binding rules for user-facing documentation — Diátaxis content architecture, audience model, evidence discipline, in-product help governance, doc-to-release sync; binds projects meeting its §0.2 applicability criteria. |
| Stribog Developer Documentation Standard | The binding rules for developer-facing documentation — generated reference contract, drift gate, code-sample discipline, public surface map, deprecation contract; binds projects meeting its §0.2 applicability criteria. |
| Stribog UI/UX Standard | The binding rules for user-interface surfaces — design tokens, component state contract, WCAG 2.2 AA accessibility floor, microcopy, i18n, design review gate, frontend performance budgets, consent-first telemetry; binds projects meeting its §0.2 applicability criteria. |
| Stribog Glossary | Authoritative definitions for cross-document terms. Binding for term meaning. |
| Charter Governance | This document. The lifecycle of the charter set itself. |

The Engineering Charter, Documentation Standard, AI Agent Execution Standard, Operational Delivery Standard, Glossary, and Charter Governance bind every Stribog project per their own §0.2 clauses. The Security Posture Standard, Data and Privacy Standard, User Documentation Standard, Developer Documentation Standard, and UI/UX Standard bind only projects that satisfy their respective applicability criteria; the project's Charter Compliance Annex declares whether each applies.

### 2.2 Templates

| Template | Purpose |
|----------|---------|
| `templates/Master-Reference-Template.md` | Skeleton for project master references. |
| `templates/ADR-Template.md` | Skeleton for Architecture Decision Records. |
| `templates/Build-Plan-Template.md` | Skeleton for phased build plans. |
| `templates/Audit-Closeout-Template.md` | Skeleton for audit and certification notes. |
| `templates/Runbook-Template.md` | Skeleton for operational runbooks. |
| `templates/Testing-Strategy-Template.md` | Skeleton for the project testing strategy artifact required by Engineering Charter §2.1 once the testing surface becomes non-trivial. |
| `templates/Critique-Persona-Template.md` | Skeleton for defining critique personas used in the audit, review, and self-audit workflows referenced by the AI Agent Execution Standard and Charter Governance §10. |
| `templates/Charter-Compliance-Annex-Template.md` | Skeleton for per-project Charter Compliance Annexes. |

Templates are normative for shape. Their content is illustrative.

### 2.3 Working Documents

The charter set is accompanied by working documents that are not themselves governing:

- audit-round records (e.g. `Charter-Set-Audit-Round-N.md`)
- the directory `README.md` as a navigation index

Working documents are advisory. They record decisions but do not bind.

## 3. Physical Location and Distribution

### 3.1 Canonical Working Source

The canonical working source for the charter set is a directory in the Stribog BrainForest vault. Its exact local-filesystem location is operator-specific and not declared in the public distribution. The Charter Owner maintains the canonical working source; all other locations (including this public distribution) are derived projections.

This is the single authoritative location for in-progress charter work. Edits to charter documents happen here, not in derived copies.

### 3.2 Promoted Distribution Source

For projects that cannot reach the BrainForest working source — public repositories, multi-operator projects, automated agents running outside the operator's machine — the charter set is promoted to a Stribog-controlled Git repository. The promotion is performed at every charter version bump.

The Compliance Annex of any project that cannot reach BrainForest names the promoted location. Projects that can reach BrainForest reference the BrainForest path directly.

### 3.3 Promotion Discipline

Promotion is one-way. The Git repository is a derived projection of the BrainForest source, not an independent copy. Edits made to the Git repository directly are not authoritative; they must be backported to BrainForest or treated as waiver-tracked deviations.

### 3.4 Working-Source-Side Diagram Source

For BrainForest-resident charter documents, the embedded `d2` blocks inside the Markdown documents are explicitly the canonical diagram source. This is declared in the documents themselves. The Stribog Documentation Standard §7.2 governs the broader rule.

When the charter set is promoted to the Git repository, rendered SVG and PNG artifacts are produced and versioned alongside the Markdown.

### 3.5 Backups

The charter set is backed up under the same backup posture as the rest of BrainForest. A charter set that exists only on a single disk is a fragile control system.

### 3.6 Public Release Profile

Every Stribog project that maintains a public derived projection (a one-way mirror to a public Git repository, a published documentation site, a public artifact registry, etc.) declares a **public release profile** in its Compliance Annex.

The public release profile names two sets:
- **Included** — files, directories, sections, or generated artifacts that ARE part of the public derived projection.
- **Excluded** — files and directories that are NOT part of the public derived projection (typically: internal operational artifacts, audit-round records, draft scratch, vault-local diagrams, confidential annexes).

Two binding rules follow:

1. **No clause may reference an excluded artifact from an included artifact.** A governing clause that requires reading or citing a file outside the public release profile breaks the public projection. If such a reference is necessary, the referenced material moves into the included set, or the citing clause is reframed.

2. **Gates that bind a project apply to the included set.** A gate may, in addition, apply to the canonical working source. It must not apply only to excluded artifacts — that breaks the audit trail in the public projection.

The public release profile is declared once in the Annex and reviewed at every charter version bump. A change to the profile is itself a Compliance-Annex change governed by §6 of this document.

For the Stribog Charter Set's own public release profile, see the `.gitignore` and `README.md` of the promoted distribution repository.

## 4. Charter Versioning Semantics

### 4.1 Two Independent Counters

Every governing document carries two front-matter fields:

- `version` — SemVer (`MAJOR.MINOR.PATCH`) for the document's normative content
- `revision` — a monotonic integer that increments on every saved substantive change

They move independently. Editorial cleanups bump `revision` without touching `version`. Normative changes bump `version` and `revision` together.

### 4.2 SemVer Semantics

| Bump | Trigger |
|------|---------|
| `PATCH` | Editorial fix, typo, formatting, clarification that does not change meaning. |
| `MINOR` | New non-breaking section, new optional field, additional rule that does not invalidate any prior compliant project. |
| `MAJOR` | Breaking change — a clause that may put a previously-compliant project out of compliance. |

This is the Stribog Documentation Standard §11.2 rule, restated here because it is the operational basis for charter versioning.

### 4.3 Documents Move Independently

Each governing document carries its own version counter. The Universal Engineering Charter at `1.2.0` does not imply the Documentation Standard is at `1.2.0`. Lockstep versioning across the charter set is misleading and is forbidden.

The exception is a coordinated charter-set release where multiple documents are bumped together in a single ratification cycle. In that case, the audit-round record names the documents and versions involved.

### 4.4 No Floating Pins

Projects pin to specific `MAJOR.MINOR` versions of governing documents in their Charter Compliance Annex. Pinning to "latest", "main", or an unversioned reference is forbidden.

### 4.5 Compatibility Promise

When a governing document moves from `MAJOR=N` to `MAJOR=N+1`, projects pinned to `MAJOR=N` are not retroactively non-compliant. They remain governed by their pinned version until a deliberate migration is performed.

The Compliance Annex of each project records the migration cadence — when the project intends to move to the next major. A project that pins indefinitely to an aging major is acceptable only if the Compliance Annex acknowledges the pin and names the rationale.

### 4.6 Deprecation

When a clause is replaced or removed across a major boundary, the prior major is marked deprecated in its `status` and a successor reference is added. Deprecated documents remain readable; they do not bind new projects.

## 5. Charter Compliance Annex Contract

### 5.1 The Annex Is Mandatory

Every Stribog project has a Charter Compliance Annex. The Annex is the project's authoritative declaration of what charter version it is bound by, what tooling implements the charter's gates, and any project-specific specializations. A Stribog project without a Compliance Annex is operating outside the governance system.

### 5.2 Required Annex Content

The Charter Compliance Annex captures, at minimum:

- the pinned version of each governing document
- the project's language and runtime stack
- the concrete tooling implementing each charter gate (formatter, linter, static analyzer, test runner, coverage tool, secrets scanner, vulnerability scanner)
- the named entrypoint for the repository command surface (e.g. `Makefile`, `justfile`)
- the project's testing-strategy reference
- the project's attribution convention for AI-assisted commits
- the location of the project's waiver register
- the location of closeout evidence (commit messages, PR descriptions, beads issues, etc.)
- the project's secret store
- any clause-level specializations or stricter rules
- any active waivers (which themselves live in the waiver register, but are summarized here)

The canonical template is `templates/Charter-Compliance-Annex-Template.md`.

### 5.3 The Annex Is Reviewed

The Compliance Annex is reviewed on a defined cadence — at minimum at every major version bump of any pinned governing document, and at every project phase transition. Stale Annexes are out of compliance even if the project's behavior is otherwise compliant, because they undermine the auditability of the charter system.

## 6. Per-Project Compliance Declaration

### 6.1 Compliance Is Declared, Not Assumed

A project is compliant against a specific named version of the charter set, not against an abstract idea of compliance. The declaration is in the Compliance Annex.

### 6.2 Compliance Audit

Compliance is audited:

- at project inception (initial compliance against the pinned version)
- at every phase boundary
- at every charter major-version migration
- on triggering events (incident response that surfaces charter gap, customer audit, governance review)

Audit findings produce one of:

- a ratified charter change (if the gap reflects a defect in the charter)
- a project change to close the gap (if the gap reflects a project defect)
- a recorded waiver (if the gap is intentional and accepted)

### 6.3 Compliance Is Not Binary

A project may be compliant against most clauses and waiver-tracked against others. The waiver register is the authoritative record of partial compliance. A project with a disciplined waiver register is more compliant than a project that claims full compliance and quietly ignores rules.

## 7. Charter Change Process

### 7.1 The Change Cycle

Changes to governing documents follow a defined cycle:

1. **Proposal** — a change is drafted, with rationale, in a working document or a draft branch
2. **Review-draft** — the change is applied to the governing document and its `status` is set to `review-draft` if it represents a significant rework, or kept at `governing-reference` with the version pre-bumped if it is incremental
3. **Review** — the change is reviewed against the audit checklist (§9.2) and against existing project pins
4. **Ratification** — the change is finalized; `version` and `revision` are bumped per §4.2
5. **Distribution** — the change is reflected in the promoted Git repository (if applicable); projects pinning to prior versions remain on those versions until they migrate

### 7.2 Bypassing the Cycle Is Forbidden

A governing document is not edited in place outside this cycle. "Quick fixes" to a `governing-reference` document bypass the audit trail and are forbidden. Editorial cleanups (PATCH bumps) follow a compressed cycle but still pass through ratification.

### 7.3 Multi-Document Coordinated Changes

When a change spans multiple governing documents, the cycle is coordinated:

- the proposal names every affected document
- review covers cross-document consistency
- ratification bumps each affected document's version atomically
- the audit-round record names the coordinated change

### 7.4 Emergency Changes

If a charter defect is discovered during incident response or active engagement, the change may be applied immediately under an emergency waiver. The post-incident review (§12 of the Operational Delivery Standard, or equivalent) ratifies the change retroactively or replaces the emergency change with a properly cycled alternative.

Emergency charter changes are rare and visible. Routine emergencies indicate a poorly designed charter, not a permissive emergency policy.

## 8. Audit Cadence

### 8.1 Scheduled Audits

The charter set is audited on a scheduled cadence:

- at minimum once per year (full audit-round)
- on every major version bump of any governing document
- when a new governing document is added to the canon
- when the operating reality of Stribog changes materially (new revenue line, new technology stack, new compliance regime)
- on **fresh-reader observation** — when a reader who reads the canon cold (without the in-context history of a prior round) surfaces a defect, the next audit-round opens with that defect as a seed finding. This trigger has the same authority as the four scheduled triggers above; a fresh-reader observation does not wait for the annual cadence. Demonstrated by R4: F53/F54/F55 were caught by user observation immediately after R3 sign-off, when the in-round reviewer had missed them. Demonstrated again by R5: F59/F60/F61 were caught the same way after R4 sign-off.

The audit produces an audit-round record (e.g. `Charter-Set-Audit-Round-N.md`) following `templates/Audit-Closeout-Template.md`.

### 8.2 Audit Criteria

Each audit-round verifies:

- governing strength (do the documents actually constrain behavior?)
- internal consistency (do the documents agree with each other?)
- operational fit (do the documents reflect how Stribog actually operates?)
- project alignment (do the documents reflect the practices of the reference projects?)
- diagram and source-artifact integrity
- template currency
- compliance-declaration coverage (do active projects have current Annexes?)

### 8.3 Audit Findings

Audit findings are tracked to closure. A finding produces one of:

- a ratified change to a governing document
- a templated change to one or more templates
- an updated working document
- a recorded waiver against the affected clause for the projects where the finding applies

Findings that produce no action are explicitly closed with a one-line rationale. Open findings without action carrying forward across audit-rounds is forbidden.

## 9. Charter Sunset and Replacement

### 9.1 Clause Sunset

A charter clause is sunset when:

- the operating reality the clause governs no longer exists at Stribog
- the clause has been replaced by a more general or more specific clause
- the clause has been superseded by a new governing document

Sunset is a deliberate ratified change. A clause is not sunset by quietly ignoring it; that is non-compliance, not sunset.

### 9.2 Document Replacement

A governing document may be replaced by a successor. The replacement follows the change cycle; the replaced document's `status` becomes `superseded` and its front matter records the successor.

### 9.3 Charter-Set Rewrites

A full charter-set rewrite (e.g. moving from charter set v1 to v2) follows an extended change cycle:

1. proposal of the new charter set
2. review-draft phase during which both the old and new charter sets coexist
3. migration plan for projects pinned to the old charter set
4. ratification of the new charter set as governing
5. sunset of the old charter set after the last project has migrated or recorded a long-term pin

Rewrites are rare and consequential. They are not undertaken to address ordinary defects, which are resolved through the ordinary change cycle.

## 10. Roles

### 10.1 Charter Owner

The Charter Owner is the role responsible for the integrity of the charter set. The Owner:

- approves ratified changes
- approves emergency changes
- approves audit-round closure
- is named in the front matter of every governing document under `owners`

For Stribog as currently constituted, the Charter Owner is a designated Stribog team member. The role does not change identity casually.

### 10.2 Charter Reviewers

Charter Reviewers are entities — human or AI — whose role is to apply audit and review judgment to charter changes. Reviewers do not approve; they advise. The Charter Owner retains the approval authority.

In Stribog's current operating model, the Reviewer role is filled by:

- the operator (acting in a review-mode persona, distinct from the editing role)
- AI agents in critique-class personas (Devil's Advocate, Editor, Pre-Mortem, etc.)
- selected senior reviewers external to Stribog when consulted

The Compliance Annex of charter-set changes records who reviewed.

### 10.3 Project Compliance Owner

Each Stribog project has a Project Compliance Owner — typically the project's primary maintainer. The Compliance Owner:

- maintains the Compliance Annex
- maintains the waiver register
- attests at phase and release boundaries that the project remains in compliance
- raises charter-defect findings to the Charter Owner

In Stribog's current operating model, the Project Compliance Owner is a team member wearing a distinct hat from any other Stribog role they hold.

## 11. Compliance Across Roles

### 11.1 Distinct Hats Are Real Distinct Hats

In Stribog's small-team model a team member may play multiple roles, but the discipline depends on those roles being treated as distinct. The team member wearing the Charter Owner hat does not approve a change because the team member wearing the Editor hat wrote it; the Owner-hat team member reviews against audit criteria as if the change came from elsewhere.

This is the fundamental discipline that prevents charter capture. A control system whose checks are all performed by the same person at the same time is not really a control system.

### 11.2 AI Agents in Governance Roles

AI agents may serve in governance support roles (Reviewer, draft author, audit assistant). They may not serve as Charter Owner or Project Compliance Owner. Final approval and attestation are retained by the human operator.

The Stribog AI Agent Execution Standard governs how agents participate in governance work. In short: agents may draft, critique, and audit; they may not ratify.

## 12. Anti-Patterns

The following are explicitly outside the Stribog charter governance posture and are forbidden:

- editing a governing document outside the change cycle
- pinning projects to "latest" or to an unversioned reference
- treating the same charter-set version number as bound to multiple documents (lockstep versioning across the canon)
- claiming compliance without a Charter Compliance Annex
- claiming compliance with a stale Compliance Annex
- silent obsolescence (clauses that no longer apply but have not been sunset)
- silent override (operating in violation of a clause without a recorded waiver)
- audit findings that carry forward across rounds without action or rationale
- charter changes ratified by the same hat that authored them, without a review pass in another hat
- charter rewrites motivated by ordinary defects rather than fundamental shifts
- charter set living only on a single machine without backup
- charter changes made directly in the promoted Git repository without backporting to the BrainForest canonical source

This list is not exhaustive. It is illustrative of the failure modes this governance document is built to prevent.

---

## 13. Revision History

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 1.0.0 | 1 | 2026-05-03 | Initial governing-reference release. Defined canon, physical location, charter versioning semantics, Compliance Annex contract, change cycle, audit cadence, sunset, roles. |
| 1.1.0 | 2 | 2026-05-03 | Canon expansion: added Stribog Security Posture Standard, Stribog Data and Privacy Standard, and Stribog Glossary to §2.1; added [[Testing-Strategy-Template]] and [[Critique-Persona-Template]] to §2.2. Clarified that Security Posture and Data and Privacy bind only projects meeting their respective applicability criteria. No clause was weakened; no previously-compliant project becomes non-compliant under v1.1.0, so this is a MINOR bump per Documentation Standard §11.2. |
| 1.1.0 | 3 | 2026-05-03 | Editorial revision applied during Charter Set Audit Round 3 closeout. §0 TL;DR Canon row corrected from "five governing documents" to "eight governing documents" to match §2.1. The earlier rev 2 expanded §2.1 to eight without [[UPDATING]] the TL;DR row, leaving the document self-contradictory for one revision. Closes Round 3 finding F31 (TL;DR vs §2.1 contradiction). No normative change. |
| 1.2.0 | 4 | 2026-05-03 | MINOR bump applied during Charter Set Audit Round 5 closeout. §8.1 Scheduled Audits expanded from four opening triggers to five: added **fresh-reader observation** as a fifth trigger with the same authority as the four scheduled ones. R4 demonstrated the trigger's value (F53/F54/F55 caught by user observation immediately after R3 sign-off when the in-round reviewer had missed them); R5 confirmed it (F59/F60/F61 caught the same way after R4 sign-off). Closes Round 5 finding F56. No clause was weakened; this is an additive trigger that codifies a high-value observation pattern that had been operating informally. |
| 1.3.0 | 5 | 2026-05-12 | MINOR bump applied during Charter Set Audit Round 6 closeout. §0 TL;DR Canon row updated from "eight governing documents" to "eleven governing documents" to match the post-R6 §2.1 row count. §2.1 Governing Documents extended from eight rows to eleven: added [[Stribog User Documentation Standard]], [[Stribog Developer Documentation Standard]], and [[Stribog UI/UX Standard]], each binding per its own §0.2 applicability. §2.1 closing paragraph updated to name the three new standards alongside Security Posture and Data and Privacy as applicability-bounded governing documents. Closes Round 6 finding F62 (user-facing documentation, developer-facing documentation, and UI/UX surfaces absent from the charter set) and Round 6 finding F63 (TL;DR canon-count drift, caught by self-audit before sign-off; same drift class as Round 3 F31 closure). The trigger for Round 6 was fresh-reader observation per §8.1, exercising the §8.1 bullet added in v1.2.0. No clause was weakened; the three new standards do not invalidate any prior compliant project — projects within their applicability declare their compliance posture at the next Charter Compliance Annex review per §6.1. |
| 1.3.0 | 6 | 2026-05-12 | PATCH revision applied during Charter Set Audit Round 7 closeout. Revision history extended to record that Round 7 closed the [[Stribog UI/UX Standard]] v1.0.0 → v1.1.0 interaction-surfaces and polish-craft expansion. The trigger for Round 7 was the second exercise of the §8.1 fresh-reader observation trigger — same trigger that opened Round 6. No structural change to Charter Governance itself in Round 7; this revision records that R7 ran under the governance framework already in place at v1.3.0 (rev 5). |
| 1.4.0 | 1 | 2026-05-12 | MINOR bump. Added §3.6 *Public Release Profile* — every project with a public derived projection declares included and excluded sets in its Compliance Annex; two binding rules enforce that no included artifact references an excluded artifact and that gates apply to the included set. Prompted by external feedback on profile/tier distinction and the need to make public-projection boundaries explicit. |
| 1.3.0 | 7 | 2026-05-12 | PATCH revision applied during Charter Set Audit Round 9 closeout. Revision history extended to record that Round 8 closed operational-follow-through items (Annex reference-fill refresh + R2-backlog re-audit, no governing-document clause changes) and Round 9 closed three charter-clarification items: F79 (browser-only local-first project shape — Annex §C reference fill added), F80 (provider-neutral AI attribution — AI Agent Execution Standard §5.1 example expansion + Engineering Charter §7.7 cross-link refresh), F81 (single-file distributable artifact treatment — Engineering Charter §5.5 + §7.4 clarifications). R9 opened on the deferred-finding trigger of §8.1 (after R8) plus a fresh-reader observation that surfaced three concrete clarifications from cross-project experience. No structural change to Charter Governance itself in Rounds 8 or 9; this revision records the rounds ran under the governance framework already in place. |

---
