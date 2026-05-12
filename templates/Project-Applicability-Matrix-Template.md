---
title: "<Project Name> — Project Applicability Matrix"
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
type: stribog/applicability-matrix
status: <draft | governing-reference>
tags: [stribog, compliance, applicability]
version: "0.1.0"
revision: 1
project: "<project name>"
owners: [<compliance-owner>]
---

# <Project Name> — Project Applicability Matrix

Maps each Stribog governing standard to its applicability for this project. Derived from the project profile declared in Compliance Annex §0 (Engineering Charter §0.4) and the compliance tier (Engineering Charter §0.6).

**Project profile (Charter §0.4):** `<local-only application | public library / package | hosted service | regulated / high-risk decision-support tool>`

**Compliance tier (Charter §0.6):** `<Foundation | Working | Reference>`

Review this matrix at every charter version bump. A change to any row is a Compliance-Annex change governed by Charter Governance §6.

---

## Applicability Matrix

| Standard | Applicability | Rationale |
|---|---|---|
| Universal Stribog Engineering Charter | `bound` | Binds every Stribog project per §0.2. |
| Stribog Documentation Standard | `bound` | Binds every Stribog document of governing/reference/plan/audit/runbook grade per §0.2. |
| Stribog AI Agent Execution Standard | `<bound \| not applicable>` | `<e.g. "bound — AI-assisted contribution is permitted" or "not applicable — no AI-assisted contribution">` |
| Stribog Operational Delivery Standard | `<bound \| not applicable \| waivered>` | `<e.g. "not applicable — no managed-service or rolling-deployment scope" or "bound — project operates a hosted service">` |
| Stribog Security Posture Standard | `<bound \| not applicable \| waivered>` | `<per its §0.2: e.g. "bound — project handles untrusted input and production secrets" or "not applicable — local-only, no network surface">` |
| Stribog Data and Privacy Standard | `<bound \| not applicable \| waivered>` | `<per its §0.2: e.g. "not applicable — project handles no personal or customer data" or "bound — project processes PII">` |
| Stribog User Documentation Standard | `<bound \| not applicable \| waivered>` | `<per its §0.2: e.g. "bound — project ships a CLI consumed by non-engineer operators" or "not applicable — developer-only surface">` |
| Stribog Developer Documentation Standard | `<bound \| not applicable \| waivered>` | `<per its §0.2: e.g. "bound — project exposes a public Go module API" or "not applicable — no developer-callable public surface">` |
| Stribog UI/UX Standard | `<bound \| not applicable \| waivered>` | `<per its §0.2: e.g. "bound — project ships a web UI" or "not applicable — line-oriented CLI only">` |

**Applicability values:**
- `bound` — standard applies in full per its own §0.2 criteria; compliance posture declared in the Charter Compliance Annex.
- `not applicable` — standard's §0.2 criteria are not met for this project; rationale is required.
- `waivered` — standard applies but a specific clause is waivered; waiver recorded in the Waiver Register.

---

## Active Waivers

> List any `waivered` rows from the matrix above, with waiver register references.

| Standard | Waivered clause | Waiver register entry |
|---|---|---|
| `<Standard>` | `<§X.Y — brief clause name>` | `<Waiver Register entry ID or path>` |

*If no waivers: "No active waivers."*

---

## Review History

| Version | Revision | Date | Reviewer | Change |
|---------|----------|------|----------|--------|
| 0.1.0 | 1 | <YYYY-MM-DD> | <name> | Initial matrix filed from template. |
