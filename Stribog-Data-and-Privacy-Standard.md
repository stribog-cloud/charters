---
title: "Stribog Data and Privacy Standard"
created: 2026-05-04
updated: 2026-05-12
type: stribog/data-privacy-standard
status: governing-reference
tags: [charter, embeddings, governance, incident, stribog]
version: "1.0.0"
revision: 5
last_updated: 2026-05-12
parent_moc: "[[MOC - Stribog Governance]]"
owners: [stribog-team]
---


# Stribog Data and Privacy Standard

> The binding standard for how Stribog projects handle data — particularly personal, customer, and sensitive data. This is a mandate. It governs data classification, lifecycle, residency, subject rights, cross-border transfer, breach notification, processing agreements, and AI-mediated data handling.

---

## 0. TL;DR

| Area | Mandate |
|------|---------|
| Classification | Every Stribog project that handles data declares the classification of every data category it touches. |
| Lifecycle | Each data category has a declared lifecycle: collection purpose, retention period, deletion guarantee. |
| Residency | Data residency is a deliberate design decision recorded in the master reference, not a side effect of vendor choice. |
| Subject rights | Where DPDPA, GDPR, or comparable regimes apply, data subject rights (access, correction, erasure, portability) are buildable from the system. |
| PII | Personal Identifiable Information is handled with explicit awareness of the regime that protects it. |
| Cross-border | Cross-border data transfers are documented and conform to the applicable regime. |
| Breach | Data breach detection, response, and notification follow the security incident track with privacy-specific obligations. |
| DPA | Stribog as data processor signs Data Processing Agreements that align with this standard; Stribog as data controller publishes equivalent commitments to its own subjects. |
| AI | AI-mediated processing is governed: training data, inference data, retention, model output, and provenance disclosure. |
| Audit | Privacy posture is audited at the same cadence as the security audit, and aligned with applicable regulator inquiry windows. |

This standard is binding alongside the Universal Stribog Engineering Charter for any Stribog project that meets the §0.2 applicability criteria. It refines several charter clauses (§8 secret and PII hygiene, §8.1 secret prevention) for the privacy-discipline context.

## 0.1 Why This Standard Exists

Stribog handles data that is not its own. Customer infrastructure data flows through managed-service engagements. AI-mediated processing — increasingly central to Stribog's work — moves data through model inference paths. Stribog's primary operating jurisdiction has the Digital Personal Data Protection Act 2023 (DPDPA), which imposes specific obligations on entities that process personal data. Stribog has explored IAPP AIGP certification and has clients with data-protection expectations of their own.

A general-purpose engineering charter is not enough for this work. Privacy as a discipline has its own classification framework, its own lifecycle obligations, its own subject-rights mechanics, and its own breach-notification clocks. Treating it as a side concern of general data hygiene produces precisely the failures that regulators sanction — failures that cost client engagements, civil penalties, and in some cases criminal exposure.

This standard exists to convert privacy from an aspirational posture into mechanical, observable, audit-trail-bearing engineering work that aligns with applicable regulatory regimes (notably DPDPA, with structural compatibility for GDPR-grade obligations where customer engagements require them).

## 0.2 Applicability

This standard binds every Stribog project that satisfies one or more of the following:

- the project collects, stores, processes, or transmits personal data of identifiable individuals
- the project handles customer data on behalf of a Stribog client (Stribog acting as a data processor)
- the project handles operator-internal data classified as Confidential or Restricted under §2
- the project's design materially affects how data flows across Stribog systems
- the project is delivered into a regulatory regime (DPDPA, GDPR, sectoral) that imposes data-protection obligations
- the project trains, fine-tunes, or operates AI models on data of any classification above Public

A Stribog project that satisfies none of the above is not bound by this standard, but the burden of proof is on the exemption.

## 0.3 Definitions

This standard relies on the Stribog Glossary for cross-cutting terms. Privacy-specific terms used in this document:

- **Data subject** — the individual to whom personal data relates.
- **Data controller** — the entity that determines the purpose and means of processing personal data.
- **Data processor** — the entity that processes personal data on behalf of a controller.
- **Personal data / PII** — data that identifies or can reasonably be used to identify a living individual.
- **Sensitive personal data** — personal data classes that the applicable regime treats with elevated protection (e.g. financial data under DPDPA significant-data-fiduciary rules, special-category data under GDPR).
- **Data Processing Agreement (DPA)** — a contract between controller and processor that allocates data-protection obligations.
- **Data subject request (DSR)** — a request from an individual to exercise rights over their personal data (access, correction, erasure, portability, objection).

## 1. Core Positions

Stribog's position on data and privacy rests on six points.

1. **Privacy is a design property, not a policy statement.** Privacy postures are designed into the architecture before implementation, not retrofitted before audit.
2. **Data has a lifecycle.** Every data category Stribog handles has a declared lifecycle from collection through deletion. Data without a declared lifecycle is forbidden.
3. **Minimize at every stage.** Data is collected only where necessary, retained only as long as necessary, processed only where authorized, and disclosed only to those who require it.
4. **Subject rights are buildable, not bolt-on.** Where applicable regimes grant subjects rights (access, correction, erasure, portability), those rights must be exercisable from the system without heroic engineering.
5. **Boundaries are recorded.** Every cross-system, cross-regime, or cross-border data flow is documented in the master reference.
6. **AI does not exempt the data.** Data flowing through AI training, fine-tuning, or inference paths remains subject to this standard. AI-mediated processing is a processing path, not a privacy reset.

These positions are the lens through which every clause below is enforced.

## 2. Data Classification

### 2.1 Classification Vocabulary

Stribog uses a four-tier data classification:

| Class | Definition | Examples |
|-------|------------|----------|
| **Public** | Information intended for unrestricted disclosure. Loss has no operational impact. | Published documentation, open-source code, marketing material, public release notes |
| **Internal** | Information for use within Stribog and named partners. Loss causes minor reputational impact. | Internal architecture notes, project plans, internal runbooks |
| **Confidential** | Information whose unauthorized disclosure would cause material harm. Includes most customer operational data and unredacted Stribog operational detail. | Customer infrastructure configuration, customer logs, internal credentials (not the secrets themselves), pricing models |
| **Restricted** | Information whose unauthorized disclosure would cause severe harm. Includes personal data, secrets, financial account material, and data subject to sectoral regulation. | Personal data, secrets, credentials, payment material, health information |

### 2.2 Per-Project Classification

Every Stribog project bound by this standard records, in its master reference or as a linked supplement:

- every category of data it handles
- the classification of each category
- the rationale for the classification

A project that touches multiple classifications applies the discipline of the highest classification its data reaches.

### 2.3 Classification Inheritance

Derived data inherits the classification of the most sensitive source. Aggregations, summaries, embeddings, and indexes derived from Restricted data are themselves Restricted unless a deliberate de-identification process has been performed and recorded.

De-identification is a technical claim that requires evidence; calling something "anonymized" without recorded evidence does not change its classification.

## 3. Data Lifecycle

### 3.1 Collection

Data is collected only where there is a declared purpose. The purpose is recorded for each data category, in the master reference or a linked supplement. The purpose must be:

- specific (not "for system improvement")
- contemporaneous (declared before or at the time of collection, not retroactively)
- proportionate (the data collected is proportionate to the purpose)
- lawful (collection conforms to the applicable regime's legal basis requirements)

### 3.2 Storage

Stored data is:

- located in a system whose classification matches or exceeds the data's classification
- protected by access controls that enforce least privilege per the Stribog Security Posture Standard
- encrypted at rest where the classification requires it (the Charter Compliance Annex names the encryption posture per classification)
- backed up under a posture appropriate to its classification and the project's RPO/RTO

### 3.3 Processing

Data is processed only for declared purposes. New processing purposes require either:

- an extension to the original purpose declaration with a recorded rationale
- fresh consent or other legal basis appropriate to the regime

Processing logs, where required, capture purpose, actor, and outcome at a granularity sufficient to reconstruct the processing in the event of a subject request or regulator inquiry.

### 3.4 Retention

Every data category has a declared retention period. The retention period is:

- bounded (no "indefinite" retention without a recorded rationale)
- aligned with the declared purpose (data is retained only as long as the purpose remains)
- aligned with applicable legal retention requirements (which set both floors and ceilings)
- enforced by automation where the volume justifies it

A retention period that has expired triggers deletion. Data that has outlived its retention is non-compliant and is surfaced as a finding at the next audit.

### 3.5 Deletion

Deletion is a positive guarantee, not an absence-of-keeping.

- **Logical deletion** removes data from active systems and indexes.
- **Physical deletion** removes data from backups, archives, and any derived stores after their respective retention windows expire.

Each data category's deletion guarantee is named in the Compliance Annex. "Best effort" is not a deletion guarantee for Restricted data.

Deletion that cannot be made unconditional (because of legal-hold obligations or backup-retention windows) is recorded as a known constraint, with the operational pathway to eventual deletion documented.

### 3.6 Lifecycle Diagram

For Stribog projects that handle Confidential or Restricted data, the master reference includes (or links to) a lifecycle diagram showing each data category's flow from collection through deletion. The diagram follows the D2 discipline of the Stribog Documentation Standard.

## 4. Data Residency

### 4.1 Declared Residency

Every project bound by this standard records, for each data category, the residency of:

- the primary data store
- backups
- derived projections (search indexes, vector stores, embeddings)
- any transient processing locations
- AI inference paths (where applicable)

Residency is a deliberate design decision. It is not the side effect of selecting a default region in a vendor console.

### 4.2 Residency Compliance

Where the applicable regime imposes residency obligations (e.g. customer engagements that contractually require Indian residency, or sectoral regimes that pin specific data classes to specific jurisdictions), the system architecture demonstrably honors those obligations. Demonstrable here means: a reviewer can trace the data path from collection through deletion and confirm that no stage exceeds the residency constraint.

### 4.3 Residency Drift Detection

For systems where residency is contractually constrained, residency drift (data appearing in a region it should not) is detected, not assumed absent. The Compliance Annex names the detection mechanism.

## 5. Data Subject Rights

### 5.1 Required Rights

Where the applicable regime grants data subjects rights, the system supports the corresponding operations. Under DPDPA the relevant rights include access, correction, erasure, grievance redressal, and nomination. Under GDPR they additionally include portability and objection.

For each applicable right, the system supports the operation:

- **Access** — given a subject identifier, the system can produce the personal data held about that subject across all stores
- **Correction** — the system supports authenticated correction with audit trail
- **Erasure** — the system supports deletion that propagates through derived stores within the regime's response window
- **Portability** — where required, data is exportable in a structured, commonly used, machine-readable format
- **Objection / restriction** — where required, processing can be restricted for a specific subject without breaking system integrity

### 5.2 DSR Response Discipline

Data subject requests have regime-defined response windows. The Compliance Annex names:

- the channel through which subjects submit DSRs
- the verification mechanism that confirms subject identity
- the response window:
  - **GDPR Art. 12.3** — one month from receipt, with conditional two-month extension for complex or numerous requests (extension itself notified to the subject within the initial month)
  - **DPDPA** — the response window prescribed by the DPDPA Rules in force at audit time. As of the Draft DPDPA Rules published in January 2025, the prevailing draft prescribes a response window measured in days from request receipt; the Compliance Annex records the exact current window, the date of the Rules version cited, and the source URL. This citation is refreshed at every charter audit-round and at every Rules-version change.
  - the customer's contracted window where stricter than the regulatory baseline above
- the operator path for fulfillment

The asymmetry between concretely cited GDPR provisions and the parameterized DPDPA window reflects regulatory reality, not Stribog vagueness: GDPR is settled law cited at the Article level; DPDPA implementing-Rules drafting is in progress. A change to the prescribed window is treated as a regulatory-regime change per §0.1, triggers a Compliance Annex update, and is reflected at the next charter audit-round.

DSRs are tracked in the project's durable work system to closure.

### 5.3 Erasure Across Derived Stores

Erasure that does not propagate to derived stores (search indexes, vector embeddings, AI training corpora, backups within their retention window, replicated systems, audit logs subject to legal retention) is incomplete. The Compliance Annex names the propagation mechanism per derived store, and the residual-data posture for stores where propagation is constrained.

## 6. PII Handling

### 6.1 PII Inventory

Every project that handles PII maintains a PII inventory: which fields, in which stores, derived from which sources, retained under which lifecycle. The inventory is the foundation for §3.4 retention, §5 subject rights, and §8 breach notification.

A project handling PII without a PII inventory is non-compliant.

### 6.2 PII Minimization

PII is collected, processed, and stored only where the declared purpose requires it. Where a purpose can be served by an identifier that does not directly identify (a hash, a tokenized reference, an opaque ID), the non-identifying form is preferred.

### 6.3 PII in Logs

PII does not flow into logs, error reports, telemetry, or observability systems unless the destination is itself classified to handle PII and the inclusion is recorded in the PII inventory. Where PII is necessary for diagnostics, it is included via redaction-aware logging configuration, not per-call developer discipline.

### 6.4 PII in Test Fixtures

Production PII is never used as test fixture material. Test fixtures use synthetic PII (clearly fake names, `@example.com` email addresses, RFC 5737 IP addresses, RFC 3849 IPv6 documentation prefixes, and equivalent placeholders for sectoral identifiers). The Charter Compliance Annex names the synthetic-fixture conventions.

## 7. Cross-Border Data Transfer

### 7.1 Cross-Border Transfer Inventory

Every cross-border data transfer in the system is documented. The documentation captures:

- source jurisdiction
- destination jurisdiction
- data categories transferred
- legal basis for the transfer (under each applicable regime)
- operational mechanism (managed service, vendor processing, support access)

### 7.2 DPDPA Cross-Border Posture

Under DPDPA, cross-border transfer to jurisdictions outside the primary operating jurisdiction is permitted unless restricted by notification. Stribog projects monitor the applicable notification regime and respond to changes by adjusting transfer paths or seeking customer-side adjustments to engagement scope.

### 7.3 Customer-Imposed Cross-Border Constraints

Customer engagements that impose cross-border constraints stricter than the applicable regulatory regime are honored at the engagement level. The Compliance Annex of an engagement project records the customer-imposed constraints separately from the regulatory baseline.

## 8. Breach Notification

### 8.1 Breach Detection

Every project bound by this standard has declared mechanisms for detecting personal data breaches (unauthorized access, disclosure, alteration, or loss of personal data). Detection is not assumed; it is engineered.

Detection sources include:

- security monitoring (per the Stribog Security Posture Standard)
- access-anomaly detection
- vulnerability disclosure inbound
- third-party notification (vendor breach affecting Stribog systems)
- internal observation by operators

### 8.2 Breach Response

A confirmed or suspected personal-data breach triggers the security incident response path (Stribog Security Posture Standard §10) with privacy-specific extensions:

- the affected data categories and approximate volumes are determined as early as the [[INVESTIGATION]] supports
- the affected subjects are identified to the extent possible
- the regulatory notification clock starts at the point of confirmation, not at the point of [[remediation]]
- the customer-notification clock under the applicable engagement DPA starts at the corresponding contracted point

### 8.3 Regulatory Notification

Where the applicable regime requires regulator notification, the project is engineered to support that notification within the required window. The Compliance Annex names:

- the regulator(s) the project is accountable to
- the contracted notification window per regulator
- the operator path for filing notifications
- the legal counsel coordination protocol

Concrete windows applicable to common Stribog engagements:

- **GDPR Art. 33** — supervisory-authority notification within 72 hours of awareness, where feasible; reasoned justification required if the 72-hour mark is missed
- **GDPR Art. 34** — notification to affected data subjects without undue delay where the breach is likely to result in a high risk to subject rights and freedoms
- **DPDPA** — notification to the Data Protection Board and to affected subjects within the window prescribed by the DPDPA Rules in force at audit time. As of the Draft DPDPA Rules published in January 2025, the prevailing draft prescribes a notification window measured in hours from breach confirmation; the Compliance Annex records the exact current window, the date of the Rules version cited, and the source URL. This citation is refreshed at every charter audit-round and at every Rules-version change.

The asymmetry between concretely cited GDPR Articles and the parameterized DPDPA window reflects regulatory reality, not Stribog vagueness: GDPR is settled law cited at the Article level; DPDPA implementing-Rules drafting is in progress. The Compliance Annex captures any narrower window imposed by customer DPA terms.

### 8.4 Subject Notification

Where the regime or engagement requires direct notification of affected subjects, the notification:

- describes the nature of the breach in plain language
- describes the categories of personal data affected
- describes the likely consequences
- describes the measures taken or proposed to address the breach
- provides a contact point for further information

Subject notification respects the operational principles of the Stribog Operational Delivery Standard §11.3 (customer comms) while satisfying the privacy-specific obligations of this section.

### 8.5 Customer Notification (Stribog as Processor)

Where Stribog acts as a data processor on behalf of a customer who is the controller, breach notification flows first to the customer per the engagement DPA. The customer's regulatory and subject-notification obligations are theirs to discharge; Stribog's obligation is to provide the customer with what the customer needs to discharge those obligations within the contracted timeline.

## 9. Data Processing Agreements

### 9.1 Stribog as Data Processor

For engagements where Stribog processes customer personal data, a Data Processing Agreement is in place before processing begins. The DPA aligns with this standard and the applicable regime, and explicitly addresses:

- the categories and purposes of processing
- the duration of processing
- the rights and obligations of the controller
- the obligations of the processor (this Stribog discipline)
- sub-processor authorization (where Stribog uses sub-processors)
- security measures (per the Stribog Security Posture Standard)
- breach notification flow (per §8.5)
- subject-rights coordination
- audit and inspection rights
- data return or deletion at engagement end

A processing engagement without a DPA is non-compliant.

### 9.2 Stribog as Data Controller

Where Stribog acts as a data controller (collecting personal data for its own purposes, e.g. customer-relationship management, billing, contractual records), the Stribog privacy notice published to subjects describes:

- the controller identity (Stribog IT Solutions Pvt Ltd / Derbatech Solutions Pvt Ltd, as applicable)
- the categories of personal data collected
- the purposes
- the legal basis under DPDPA (or other applicable regime)
- the retention period
- the recipients of the data
- the rights available to the subject
- the grievance contact

The privacy notice is a public document and is itself governed by the Stribog Documentation Standard.

### 9.3 Sub-Processor Discipline

Sub-processors used in customer engagements (managed-service vendors, infrastructure providers, AI inference providers) are:

- inventoried per engagement
- authorized by the customer DPA
- subject to written terms that flow down the controller's obligations
- reviewed for their own privacy posture before engagement

A sub-processor change requires customer notification under most engagement DPAs; the Compliance Annex names the change-control discipline.

## 10. AI and Data

### 10.1 AI as a Data Processing Path

AI-mediated processing — model training, fine-tuning, retrieval-augmented inference, embedding generation, agent action over data — is a data processing path subject to this standard. Routing personal data through an AI system does not exempt the data from classification, lifecycle, residency, subject rights, or breach obligations.

### 10.2 Training and Fine-Tuning

Personal data is not used for model training or fine-tuning unless:

- the legal basis under the applicable regime supports it
- the data subjects have been informed
- the model output cannot be made to disclose the training data (or the disclosure risk is recorded and accepted)
- the training corpus is documented as a Stribog data category with declared classification, residency, and lifecycle

A common Stribog default is: do not use customer or subject personal data for any training or fine-tuning without explicit per-engagement authorization recorded in the DPA.

### 10.3 Inference

Personal data flowing through AI inference paths is governed by the same residency, retention, and disclosure rules as any other processing path. The Compliance Annex names:

- which inference providers are authorized
- the residency of each provider's processing
- the retention posture of each provider (zero-retention API where available; otherwise the contractual retention window)
- whether inference inputs may be used by the provider for their own model improvement (the default Stribog answer is no, contractually verified)

### 10.4 Local-First Where Privacy Pressure Justifies

Where data classification, residency constraints, or customer DPA terms make cloud-hosted AI inference impractical, Stribog routes processing to local inference (per the AI Agent Execution Standard §7.3). The Compliance Annex names the local-first routing rules per data classification.

### 10.5 AI Output and Provenance

AI output that influences operational or customer-facing decisions is recorded with provenance: which model, which prompt context, which retrieval path, when. This serves both the AI Agent Execution Standard's attribution discipline and this standard's audit requirements.

### 10.6 AI Agent Access to Personal Data

AI agents (per the AI Agent Execution Standard) operating on Stribog projects may access personal data only where:

- the agent's task scope explicitly authorizes it
- the access is logged
- the agent does not export the personal data to an unauthorized destination (including its own training pipeline, where the model provider has not committed to non-use)

The agent's stop-and-ask boundaries (AI Agent Execution Standard §9) explicitly include uncertainty about authorization to access personal data.

## 11. Privacy Audit

### 11.1 Project Privacy Audit

Every Stribog project bound by this standard is privacy-audited:

- at project go-live
- at every major architecture change
- on a defined cadence named in the Compliance Annex (typically annually, aligned with the security audit)
- on triggering events (DSR surge, customer DPA review, regulator inquiry, breach)

### 11.2 Audit Criteria

The privacy audit verifies, at minimum:

- the PII inventory is current
- declared retention periods match operational reality
- subject-rights mechanisms are exercisable end-to-end (test DSRs are run through the system)
- residency constraints are honored
- DPA obligations match operational behavior
- AI processing paths are recorded
- breach detection mechanisms are functional

### 11.3 Regulator and Customer Inquiry Readiness

The system is engineered such that responses to regulator or customer inquiries can be produced within the contracted or regulatory window. "We need a month to compile the answer" is not a defensible response under most applicable regimes.

## 12. Anti-Patterns

The following are explicitly forbidden under this standard:

- handling personal data without a recorded data classification
- collecting personal data for an unstated or post-hoc purpose
- "indefinite" retention without recorded rationale
- deletion that does not propagate to derived stores within the declared window
- using production personal data as test fixture material
- routing personal data through AI inference paths without recording the path in the master reference
- using customer or subject personal data for model training without explicit written authorization
- residency claims that cannot be traced through the architecture
- DSR fulfillment that requires manual data archaeology rather than supported system operations
- breach response that begins the regulatory clock at remediation rather than at confirmation
- DPA obligations honored in contract but not in operational practice
- relying on "anonymization" as a classification reset without recorded de-identification evidence
- privacy notices that describe a process the project does not actually follow (governance theater, per Engineering Charter §15)
- AI agents accessing personal data outside an authorized task scope
- sub-processor changes without customer notification under the applicable DPA
- audit logs containing personal data without inclusion in the PII inventory

This list is not exhaustive. It is illustrative of the failure modes this standard is built to prevent.

## 13. Revision History

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 1.0.0 | 1 | 2026-05-03 | Initial governing-reference release. Defined data classification (Public, Internal, Confidential, Sensitive PII, Regulated), data lifecycle (collection minimization, retention, deletion, archival), data residency (per-customer regime, transfer mechanisms), data subject rights (DSR taxonomy, response discipline, fulfillment record), PII handling (inventory, access controls, logging), cross-border transfer mechanisms, breach notification (regulator, subject, customer pathways under DPDPA, GDPR, contractual regimes), data processing agreements, AI-specific data handling, privacy audit cadence. |
| 1.0.0 | 2 | 2026-05-03 | Editorial revision applied during Charter Set Audit Round 3. §5.2 and §8.3 framing updated to acknowledge that DPDPA implementing-Rules windows have been the subject of evolving regulatory drafting; the project records the *current* understood window in its Compliance Annex with date and source. No normative change. |
| 1.0.0 | 3 | 2026-05-03 | Editorial revision applied during Charter Set Audit Round 3 closeout. §5.2 and §8.3 strengthened: GDPR provisions cited concretely (Art. 12.3 for DSR response, Art. 33 for breach notification) and DPDPA Draft Rules 2025 cited concretely (with explicit "as of <draft date>" qualifier and the existing regulatory-drafting caveat preserved) so the GDPR-vs-DPDPA asymmetry reflects regulatory reality (settled vs draft) rather than Stribog hand-waving. Added this §13 Revision History section to satisfy Documentation Standard §12 Definition of Done (Revision History required for governing-reference documents). Closes Round 3 findings F40 (governing standard lacked Revision History) and F48/F49 (DPDPA-vs-GDPR concreteness asymmetry). No normative change.

---
