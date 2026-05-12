---
title: "Stribog Charter Set Index"
created: 2026-05-04
updated: 2026-05-12
type: stribog/charter-index
status: governing-reference
tags: [charter, governance, rag, runbook, stribog]
project: Stribog - Common
version: "1.2.0"
revision: 10
last_updated: 2026-05-12
parent_moc: "[[MOC - Stribog Governance]]"
owners: [stribog-team]
---


# Stribog Charter Set Index

> Navigation index for the Stribog charter set. The canonical working source for every Stribog governing document.

---

## 0. TL;DR

This directory holds the binding governance canon for every Stribog project. The canon consists of **eleven governing documents** and **nine templates**. Nothing else here is governing.

The canon as a whole sits at `1.2.0` (universally bumped from `1.1.0` on 2026-05-12 to add three new governing documents — User Documentation, Developer Documentation, UI/UX — covering the user-facing and contributor-facing surfaces previously absent from the canon). Individual documents version independently per Charter Governance §4.3; the table in §1.1 below names each document's current version.

Projects pin to specific versions in their Charter Compliance Annex; they do not float against `latest`.

## 1. The Canon

### 1.1 Governing Documents

These eleven documents are binding. Each has its own §0.2 applicability clause. Several apply universally; six (Operational Delivery, Security Posture, Data and Privacy, User Documentation, Developer Documentation, UI/UX) apply only to projects meeting their specific criteria, declared in the Charter Compliance Annex.

| Document | Current Version | Applicability | Read order |
|----------|-----------------|---------------|------------|
| [[Universal-Stribog-Engineering-Charter]] | `1.2.0` (rev 8) | Universal — every Stribog project | 1 |
| [[Stribog-Documentation-Standard]] | `2.1.0` (rev 6) | Universal — every Stribog document of governing/reference/plan/audit/runbook grade | 2 |
| [[Stribog-AI-Agent-Execution-Standard]] | `1.1.0` (rev 5) | Universal — every Stribog project that accepts AI-assisted contribution | 3 |
| [[Stribog-Operational-Delivery-Standard]] | `1.1.0` (rev 4) | Projects with managed-service, infrastructure, or rolling-deployment scope | 4 |
| [[Stribog-Security-Posture-Standard]] | `1.0.0` (rev 2) | Projects meeting its §0.2 criteria (security tools, untrusted input, secrets, production state) | 5 |
| [[Stribog-Data-and-Privacy-Standard]] | `1.0.0` (rev 3) | Projects meeting its §0.2 criteria (PII, customer data, regulated regimes) | 6 |
| [[Stribog-User-Documentation-Standard]] | `1.0.0` (rev 1) | Projects meeting its §0.2 criteria (any project shipping a human-operable surface — UI, CLI for non-engineers, API for integrators, managed service) | 7 |
| [[Stribog-Developer-Documentation-Standard]] | `1.0.0` (rev 1) | Projects meeting its §0.2 criteria (any project exposing a developer-callable surface — public API, SDK, plugin seam, contributor-facing codebase) | 8 |
| [[Stribog-UI-UX-Standard]] | `1.1.0` (rev 2) | Projects meeting its §0.2 criteria (any project shipping a user interface — web, mobile, desktop, dashboard, TUI, embedded) | 9 |
| [[Stribog-Glossary]] | `1.3.0` (rev 4) | Universal — authoritative for cross-document term meaning | 10 |
| [[Charter-Governance]] | `1.3.0` (rev 6) | Universal — governs the charter set itself | 11 |

The Engineering Charter §0.5 defines three **compliance tiers** (Foundation, Working, Reference) that graduate the discipline applied based on project risk while keeping the universal canon binding on every Stribog project. Every project declares its tier in its Charter Compliance Annex.

### 1.2 Templates

Every Stribog document family has a canonical template under `templates/`. New documents start from a template, not from a blank file.

| Template | For | Current Version |
|----------|-----|-----------------|
| `templates/Master-Reference-Template.md` | Project master references — Email RAG-style skeleton with §0.3 Compliance Annex pointer | `0.1.0` (rev 1) |
| `templates/ADR-Template.md` | Architecture Decision Records — Nygard-style with Stribog status mapping | `1.0.0` (rev 2) |
| `templates/Build-Plan-Template.md` | Phased build plans — phases, gates, acceptance, cross-phase concerns | `0.1.0` (rev 1) |
| `templates/Audit-Closeout-Template.md` | Audit and certification notes — verdict, criteria, findings, residual risk, advisory-vs-binding signoff | `1.0.0` (rev 2) |
| `templates/Runbook-Template.md` | Operational runbooks — trigger, prereqs, steps, verification, rollback, drill log | `1.0.0` (rev 2) |
| `templates/Testing-Strategy-Template.md` | Project testing strategy artifact — TDD posture, layers, infrastructure, coverage strategy, shift-left | `0.1.0` (rev 1) |
| `templates/Critique-Persona-Template.md` | Defining critique personas for review and self-audit workflows | `1.0.0` (rev 2) |
| `templates/Waiver-Register-Template.md` | Per-project waiver register | `1.0.0` (rev 1) |
| `templates/Charter-Compliance-Annex-Template.md` | Per-project compliance declaration — most important per-project doc | `1.0.0` (rev 2) |

### 1.3 Other Canon Members

These documents are part of the canon but are not themselves governing standards. Each carries its own `status` per Documentation Standard §10.1.

| Document | Status | Role |
|----------|--------|------|
| `README.md` (this index) | `governing-reference` | The canonical navigation index for the charter set. Authoritative for what *is* in the canon and at what version. |

Between-rounds findings (defects discovered after a round closes but before the next opens) live in beads (the durable issue tracker) tagged `charter-audit`. The next audit round seeds its findings from those beads issues. The previous between-rounds-backlog file pattern was retracted at Documentation Standard v2.0.0 (R5 closeout) — see Doc Standard §15 v2.0.0 history entry and Charter Set Audit Round 5 §3 finding F61.

## 2. Where to Start

| If you are… | Read first |
|-------------|-----------|
| New to the canon | This README, then the Engineering Charter, then the Documentation Standard, then the Glossary |
| Starting a new Stribog project | Charter Governance §5, then `templates/Charter-Compliance-Annex-Template.md`, then the Engineering Charter (especially §0.3 and §0.5) |
| Auditing a project | The project's Charter Compliance Annex, then the governing documents pinned in that Annex in Read-Order order |
| An AI agent on first contact with a project | The project's Charter Compliance Annex, then the AI Agent Execution Standard, then the project's master reference and local agent rules |
| Building a security tool or handling untrusted input | Engineering Charter, then Security Posture Standard, then the project's master reference |
| Handling customer or personal data | Engineering Charter, then Data and Privacy Standard, then the project's master reference |
| Operating production infrastructure | Engineering Charter, then Operational Delivery Standard, then the relevant runbooks |
| Migrating a project to a newer charter version | Charter Governance §4 and §5, then the Compliance Annex of the project, then the Revision History of any document whose major version changed |
| Drafting a charter change | Charter Governance §7, then the Engineering Charter §15 anti-patterns to make sure the change does not introduce one |

## 3. Versioning

Each governing document carries an independent SemVer `version` and a monotonic `revision`. They move independently per Charter Governance §4.3. The table in §1.1 names current values.

The 1.0.0 → 1.1.0 canon expansion on 2026-05-03 affected four documents (Engineering Charter, AI Agent Execution Standard, Charter Governance, this README) and added three new governing documents (Security Posture, Data and Privacy, Glossary) and two new templates (Testing Strategy, Critique Persona). No previously-compliant project becomes non-compliant under v1.1.0. Each affected document's §Revision History records the specific change.

The 1.1.0 → 1.2.0 canon expansion on 2026-05-12 (Round 6) added three new governing documents — [[Stribog-User-Documentation-Standard]], [[Stribog-Developer-Documentation-Standard]], [[Stribog-UI-UX-Standard]] — covering the user-facing and contributor-facing surfaces previously absent from the canon. Round 6 opened on fresh-reader observation (the §8.1 trigger added in Charter Governance v1.2.0, exercised for the first time at the next major audit-round). The expansion also produced coordinated MINOR or PATCH bumps in: Engineering Charter (1.1.0 → 1.2.0, §3.3 + §5.9 + §14 cross-references), Documentation Standard (2.0.0 → 2.1.0, §2 family expansion to §2.6 / §2.7 / §2.8), Operational Delivery Standard (1.0.0 → 1.1.0, §11.3 + §15.2 user-facing-doc coupling), Charter Governance (1.2.0 → 1.3.0, §2.1 canon row expansion), Glossary (1.1.0 → 1.2.0, new §6 User-Facing Surface Terms group with twenty-one new terms), Charter Compliance Annex template (1.0.0 → 1.1.0, §0 pins extended + new §2.4 / §2.5 / §2.6 declaration blocks), Master Reference template (rev bump, §5 Interfaces table extended). No previously-compliant project becomes non-compliant under v1.2.0; the three new standards bind per their own §0.2 applicability, and projects whose surfaces predate v1.2.0 declare their compliance posture at the next Annex review per Charter Governance §6.1.

Projects pin to specific `MAJOR.MINOR` versions. They do not float against `latest`.

## 4. Physical Location

Per Charter Governance §3:

- **Canonical working source:** this BrainForest directory (`~/Documents/BrainForest/10 - Work/Stribog - Common/charters/`). All in-progress charter work happens here.
- **Promoted distribution source:** a Stribog-controlled Git repository under `github.com/stribog-cloud/`, named in the Compliance Annex of any project that cannot reach BrainForest. The Git repository is a one-way derived projection of this BrainForest source. Establishment of this repository is tracked under R2 audit finding F19.
- **Diagram source:** for documents in this BrainForest location, embedded `d2` blocks are the canonical diagram source. Each document declares this explicitly.

## 5. Change Process

Charter changes follow Charter Governance §7. Briefly:

1. Proposal — drafted in a working document or draft branch
2. Review-draft — applied with version pre-bumped
3. Review — against audit checklist and existing project pins, with Reviewer role per Charter Governance §10.2 (advisory) and Charter Owner approval (binding)
4. Ratification — `version` and `revision` bumped per Documentation Standard §11.2; Revision History section updated
5. Distribution — reflected in the promoted Git repository

Changes outside this cycle are forbidden. "Quick fixes" to a `governing-reference` document bypass the audit trail. Each document carries a §Revision History recording what changed at each version.

## 6. Audit Cadence

The charter set is audited on the cadence defined in Charter Governance §8:

- annually at minimum (full audit-round)
- on every major version bump of any governing document
- when a new governing document is added (the v1.1.0 canon expansion triggered Round 2 amendment and Round 3 closure on 2026-05-03)
- when Stribog's operating reality changes materially

Audit-round records are maintained internally as operational artifacts and are not part of this public distribution. Closure outcomes are reflected in the revision-history sections of each governing document affected by the round.

## 7. Anti-Patterns

The following are forbidden under this canon. The full lists live in the governing documents; this is the at-a-glance summary:

- editing a governing document outside the change cycle (Charter Governance §7)
- bumping a governing document's version without recording the change in its Revision History
- pinning projects to "latest" or to an unversioned reference (Charter Governance §4.4)
- claiming compliance without a Charter Compliance Annex (Charter Governance §5)
- governance theater — files that imply processes the project does not enforce (Engineering Charter §15, Documentation Standard §13)
- silent waivers — rules ignored without record (Engineering Charter §13)
- AI-assisted commits without disclosed provenance (AI Agent Execution Standard §5)
- confabulating evidence — claiming command output, file content, or test results that were not actually observed (AI Agent Execution Standard §4.4)
- production change without a record (Operational Delivery Standard §16)
- runbooks that have never been executed end-to-end (Operational Delivery Standard §7.3)
- canon drift — documents at different versions but cross-referenced as if synchronized

## License

The Stribog Charter Set is licensed under the Creative Commons Attribution 4.0
International License (CC BY 4.0). See [LICENSE](LICENSE) for the full text.

You are free to share and adapt these documents for any purpose, including
commercially, provided you give appropriate credit to Stribog and indicate
if changes were made.

## 8. Revision History

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 1.0.0 | 1 | 2026-05-03 | Initial governing-reference release. Navigation index for the v1.0.0 canon: five governing documents (Universal Stribog Engineering Charter, Stribog Documentation Standard, Stribog AI Agent Execution Standard, Stribog Operational Delivery Standard, Charter Governance) and six templates (Master Reference, ADR, Build Plan, Audit Closeout, Runbook, Charter Compliance Annex). |
| 1.1.0 | 2 | 2026-05-03 | MINOR bump applied during the v1.0.0 → v1.1.0 canon expansion. Concrete changes: (a) §1.1 Governing Documents table extended to list eight documents — three new governing documents added to the canon (Stribog Security Posture Standard, Stribog Data and Privacy Standard, Stribog Glossary); (b) §1.2 Templates table extended to list eight templates — two new templates added (Testing Strategy, Critique Persona); (c) §1.1 and §1.2 tables gained `Current Version` columns reflecting Charter Governance §4.3 independent versioning; (d) §3 Versioning rewritten to record the v1.1.0 canon-expansion event and reference each document's own §Revision History as the authoritative per-document change log; (e) front-matter `related_docs` extended to list the eight governing documents in canon order; (f) front-matter `supersedes` records the in-place rewrite from v1.0.0; (g) §7 Anti-Patterns extended to include "bumping a governing document's version without recording the change in its Revision History" and "canon drift — documents at different versions but cross-referenced as if synchronized." No previously-compliant project becomes non-compliant under v1.1.0; the new standards (Security Posture, Data and Privacy) bind only projects that meet their own §0.2 applicability criteria. |
| 1.1.0 | 3 | 2026-05-03 | PATCH revision applied during Charter Set Audit Round 3 closeout. Added this §8 Revision History section. The README at v1.1.0 rev 2 had been bumped to reflect the canon expansion but lacked the corresponding history entry — a violation of the README's own §7 anti-pattern ("bumping a governing document's version without recording the change in its Revision History"). This revision closes Round 3 finding F30 ("README §Revision History missing"). No normative change. |
| 1.1.0 | 4 | 2026-05-03 | PATCH revision applied at Charter Set Audit Round 3 sign-off. §6 Audit Cadence updated: forward-looking statement "Round 2.5 / Round 3 planning" replaced with the realized outcome "Round 2 amendment and Round 3 closure on 2026-05-03"; "most recent audit-round record" pointer advanced from `Charter-Set-Audit-Round-2.md` to `Charter-Set-Audit-Round-3.md`, with R2 retained as the prior record. No normative change. |
| 1.1.0 | 5 | 2026-05-03 | PATCH revision applied during Charter Set Audit Round 4. Three concrete drifts corrected: (a) §0 TL;DR template-count corrected from "eight templates" to "nine templates" — [[Waiver-Register-Template]] was added during R3 alongside Testing Strategy and Critique Persona, but the §0 TL;DR claim was never updated past 8 even though §1.2 and Documentation Standard §6.4 both already listed all nine; (b) §1.2 Audit Closeout Template version refreshed from `1.0.0 (rev 1)` to `1.0.0 (rev 2)` to reflect the F51 closure that promoted the template's revision counter; (c) §1.3 retitled from "Working Documents" to "Other Canon Members" — the previous title and table mis-classified the README itself as a working-document, contradicting the README's own `status: governing-reference` front-matter; the new §1.3 declares each non-standard canon member's `status` per Documentation Standard §10.1, distinguishing `governing-reference` (README, audit-rounds) from `working-document` (between-rounds backlogs), the latter ratified at Doc Standard v1.3.0 per F55 closure. Closes Round 4 findings F53 (template-count drift), F54 (README self-classification inconsistency). No normative change. |
| 1.1.0 | 6 | 2026-05-03 | PATCH revision applied during Charter Set Audit Round 5 closeout. Reflects the v2.0.0 Documentation Standard release: (a) §1.1 governing-document table updated — Stribog Documentation Standard advanced from `1.2.0 (rev 3)` to `2.0.0 (rev 5)` (MAJOR bump for §10.3 deletion and `working-document` removal from §10.1 vocabulary; §3.3 expansion with audit-round naming and title-format conventions); Charter Governance advanced from `1.1.0 (rev 3)` to `1.2.0 (rev 4)` (fresh-reader observation added as fifth §8.1 trigger). (b) §1.3 row for `Charter-Set-Round-N-Backlog.md` removed — the working-document pattern is retracted at Doc Standard v2.0.0; between-rounds findings now live in beads. §1.3 narrative updated to point readers at the canonical successor location. No normative change to README's own role; only mirrors changes ratified elsewhere in the canon. |
| 1.2.0 | 7 | 2026-05-12 | MINOR bump applied during Charter Set Audit Round 6 closeout. Concrete changes: (a) §0 TL;DR canon count corrected from "eight governing documents" to "eleven governing documents" to reflect the three new standards (User Documentation, Developer Documentation, UI/UX); (b) §1.1 governing-document table extended to list eleven documents, with the three new rows added at read-order positions 7, 8, 9 alongside their `1.0.0 (rev 1)` initial values, and current-version values refreshed for every document that bumped under Round 6 (Engineering Charter `1.1.0 (rev 5)` → `1.2.0 (rev 6)`, Documentation Standard `2.0.0 (rev 5)` → `2.1.0 (rev 6)`, Operational Delivery Standard `1.0.0 (rev 3)` → `1.1.0 (rev 4)`, Glossary `1.1.0 (rev 2)` → `1.2.0 (rev 3)`, Charter Governance `1.2.0 (rev 4)` → `1.3.0 (rev 5)`); (c) §1.1 applicability prose updated from "two (Security Posture, Data and Privacy) apply only to projects meeting their specific criteria" to the new applicability-bounded set of five standards; (d) §3 Versioning extended with a paragraph recording the 1.1.0 → 1.2.0 canon-expansion event, naming each downstream document's bump and rationale, and citing the fresh-reader trigger; (e) §6 Audit Cadence pointer advanced to `Charter-Set-Audit-Round-6.md`. Closes Round 6 finding F62. No clause was weakened. |
| 1.2.0 | 8 | 2026-05-12 | PATCH revision applied during Charter Set Audit Round 7 closeout. §1.1 governing-document table refreshed to reflect Round 7 bumps: Engineering Charter `1.2.0 (rev 6)` → `1.2.0 (rev 7)`, UI/UX Standard `1.0.0 (rev 1)` → `1.1.0 (rev 2)`, Glossary `1.2.0 (rev 3)` → `1.3.0 (rev 4)`, Charter Governance `1.3.0 (rev 5)` → `1.3.0 (rev 6)`. §6 Audit Cadence pointer advanced from `Charter-Set-Audit-Round-6.md` to `Charter-Set-Audit-Round-7.md`. Closes Round 7 finding F76 (README canon-table drift after UI/UX v1.1.0 expansion). No clause was weakened; the README mirrors changes ratified in the bumped documents. |
| 1.2.0 | 9 | 2026-05-12 | PATCH revision applied during Charter Set Audit Round 9 closeout. §1.1 governing-document table refreshed for Round 9 bumps: Engineering Charter `1.2.0 (rev 7)` → `1.2.0 (rev 8)`, AI Agent Execution Standard `1.1.0 (rev 4)` → `1.1.0 (rev 5)`. §6 Audit Cadence pointer advanced from R7 to R9 (skipping R8 in the pointer since R8 was an operational-followthrough round that produced no governing-document bump; R8 record remains canonical for backlog state). No clause was weakened. |

---
