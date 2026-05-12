---
title: "Stribog Operational Delivery Standard"
created: 2026-05-04
updated: 2026-05-12
type: stribog/operational-delivery-standard
status: governing-reference
tags: [borg-backup, charter, docker, governance, incident, investigation, k8s]
version: "1.1.0"
revision: 9
last_updated: 2026-05-12
parent_moc: "[[MOC - Stribog Governance]]"
owners: [stribog-team]
---


# Stribog Operational Delivery Standard

> The binding standard for Stribog operational work. This is a mandate. It governs managed services, infrastructure as code, rolling deployments, production change, incident response, and post-mortem discipline.

---

## 0. TL;DR

| Area | Mandate |
|------|---------|
| Change discipline | Every operational change has a change record. Ad-hoc, untracked production change is forbidden. |
| Pre-deploy | Known target state, verified prerequisites, declared rollback plan. |
| Deployment | Dry-run or staging first where feasible. Staged rollout. Canary where blast radius justifies. |
| Post-deploy | Verification probes succeed before a deployment is declared complete. Rollback remains ready until success is verified. |
| Runbooks | Every recurring or risky operation has a runbook. Runbooks are tested before they are needed. |
| Configuration | Source of truth declared. Drift detected and remediated. Manual production tweaks are temporary by definition. |
| Secrets | Never in repos. Rotated per policy. Scoped to least privilege. |
| Monitoring | Every service tier has a declared observability baseline. Alerts route to a real respondent. |
| Incidents | Severity-classified. Customer-facing communication follows the project's policy. |
| Post-mortems | Required for sev-1 and sev-2 incidents. Blameless. Action items tracked to closure. |
| DR | Restoration is tested, not theoretical. RPO and RTO are declared per service tier. |
| Lifecycle | Every operational asset has an owner, a renewal cadence, and a sunset path. |

This standard is binding alongside the Universal Stribog Engineering Charter for any Stribog project whose primary deliverable is operational. It refines several charter clauses (notably §7.4 release discipline and §9 reliability) for the operational context.

## 0.1 Why This Standard Exists

A meaningful share of Stribog work is operational rather than software-shipping. The fleet spans hypervisors, container runtimes, Kubernetes clusters, and managed services; the operator team is small, and Stribog delivers to customer engagements. That combination produces specific failure modes:

- a single unrecorded change can compromise reproducibility for an entire engagement
- a rollback plan that exists only as a thought is not a rollback plan
- runbooks written after an incident describe a recovery that no one practiced
- monitoring that exists but routes to no respondent is decoration
- post-mortems performed informally are post-mortems that produce no organizational learning
- configuration drift that accumulates silently is a multi-year credit card debt

A larger organization absorbs these failure modes through layered ownership. A small organization absorbs them in customer outages, billing disputes, and personal time. This standard exists to convert them into work that surfaces early, audibly, and recoverably.

It also exists because the Universal Stribog Engineering Charter assumes a software-shipping cadence (versioned releases, changelogs, tag-driven publication) that fits poorly when the deliverable is "the cluster keeps running." The shape of operational discipline is genuinely different, and it deserves its own document.

## 0.2 Applicability

This standard binds every Stribog project whose primary or significant deliverable is operational, including:

- managed-service engagements where Stribog operates the customer's infrastructure
- infrastructure-as-code repositories that produce production change
- ongoing operation of Stribog-owned production systems
- platform services consumed by other Stribog projects
- shared infrastructure (Kubernetes clusters, hypervisors, mesh networks, identity systems, monitoring backbones)

It applies in full unless one of the following holds:

- a written waiver exists in the project's waiver register
- a customer engagement contractually overrides a clause (in which case the waiver records the override)
- a more local Stribog standard refines this standard without weakening it

For projects that are primarily software-shipping but have an operational tail (e.g. KubeVigil's release surface), only the clauses that apply to the operational tail bind that project. Software-shipping concerns remain governed by the engineering charter.

## 0.3 What Counts as an Operational Change

For the purposes of this standard, an **operational change** is any modification to:

- production or production-adjacent infrastructure
- production configuration (Kubernetes manifests, service configuration, network configuration, identity configuration, observability configuration)
- shared platform services
- managed-service customer environments
- production data, schemas, or migrations
- secrets, certificates, or trust roots
- DNS, routing, or perimeter rules
- on-call or incident-response routing

A read-only operation is not an operational change. A dry-run is not an operational change. A change that the change-management system marks as "applied" is.

## 1. Core Positions

Operational work rests on five positions.

1. **Production change is recorded change.** Every operational change is captured in a durable record before it is applied, so a future [[INVESTIGATION]] can answer "what changed, when, by whom, and why."
2. **Reversibility is a design property.** Operational changes are designed to be reversible by default. Irreversibility requires explicit acknowledgment.
3. **Verification is part of the change.** A change is not complete when the apply succeeds; it is complete when the post-apply verification succeeds.
4. **Runbooks are practiced, not authored.** A runbook that has never been executed end-to-end is fiction.
5. **Operational state has owners.** Every operational asset — every cluster, every service, every secret, every certificate, every customer environment — has a named owner, a renewal cadence, and a sunset path.

These positions are the lens through which every clause below is enforced.

## 2. Change Management

### 2.1 Change Records

Every operational change has a change record before it is applied. The record captures:

- the change ID
- the target system, environment, or customer
- the rationale
- the planned start and end window
- the rollback plan
- the affected blast radius (services, customers, dependencies)
- the verification plan
- the operator(s) executing the change
- the approver(s), where the change requires approval
- a link to the runbook or procedure being followed

The Charter Compliance Annex names where change records live (typically a project-local issue tracker, a customer-engagement ticket system, or a shared changelog). Chat logs and verbal agreement are not change records.

### 2.2 Change Classes

Operational changes fall into three classes.

| Class | Definition | Discipline |
|-------|------------|------------|
| Standard | Pre-approved, well-understood, low blast radius (e.g. routine package updates within a tested patch window) | Recorded, executed, verified. No additional approval. |
| Normal | Material but not urgent. Reviewable in advance. | Recorded with full pre-deploy discipline (§3). Approval per project policy. Verified per §5. |
| Emergency | Time-critical, often during incident response. | Recorded as soon as the emergency is contained. Post-incident review per §12. Compensating controls per §13. |

Every operational change is one of these three. A change that does not fit any class is presumed Normal.

### 2.3 Change Windows

Where a customer or project requires change windows, those windows are explicit, documented in the runbook, and respected. Change outside an agreed window requires either a waiver or escalation to Emergency class.

### 2.4 Forbidden Patterns

The following are forbidden:

- production change with no record
- production change with a record fabricated after the fact to look like prior planning
- production change executed by an operator who has not read the runbook
- production change whose rollback plan is "fix it forward"
- multi-target production change where blast radius is "all customers" without explicit approval

## 3. Pre-Deploy Discipline

### 3.1 Known Target State

Before any non-trivial deployment, the target state is known. That means:

- the desired configuration is captured in source control or a declarative tool (Ansible, Kubernetes manifests, Terraform-equivalent, configuration management)
- the diff between current state and target state has been reviewed
- the diff is the diff that will be applied — no last-minute "while I'm here" additions

If the apply tool does not produce a reviewable plan or diff, the apply tool is wrapped in one that does, or the change runs through a staging environment first.

### 3.2 Verified Prerequisites

Before apply, prerequisites are verified:

- backups are current and restorable
- snapshots have been taken where the change permits them
- dependent services are healthy
- maintenance windows are confirmed (where applicable)
- monitoring is functioning end-to-end (the worst time to discover broken monitoring is during a failed deployment)

A "should be fine" prerequisite is not verified.

### 3.3 Declared Rollback Plan

Every Normal-class change has an explicit rollback plan recorded in the change record. The plan answers:

- what command, action, or sequence reverts the change
- who is authorized to execute the rollback
- what observable signal triggers rollback
- what the rollback's own blast radius is
- what is irreversible (data migrations, secret rotations, customer-visible state) and what is not

A change whose rollback plan is "redeploy from backup" is acceptable only if backup restoration has been recently tested. A change whose rollback plan is "we'll figure it out" is non-compliant.

### 3.4 Dry-Run or Staging First

Where feasible, a change is dry-run, staged, or applied to a non-production environment first. The list of cases where this is genuinely infeasible is small; most claims of "we have to apply directly to prod" do not survive examination.

The Charter Compliance Annex names the project's staging strategy (a dev cluster, a staging customer, a personal VPS, a Kind/k3d ephemeral cluster).

## 4. Deployment Discipline

### 4.1 Apply Posture

The apply posture for any operational change is:

- the operator has the change record open
- the operator has the runbook open
- the operator has the rollback plan readable in the same context
- monitoring dashboards relevant to the change are open
- the apply command is run, with output captured to a durable medium
- output is observed; the operator does not walk away mid-apply

For automated apply pipelines, the equivalent is: the pipeline produces capturable logs, the change record links to the pipeline run, and an alerting hook fires on apply failure.

### 4.2 Staged Rollout

For changes affecting multiple targets (multiple machines, multiple customers, multiple cluster nodes), the change rolls out in stages:

- single-target first, verified
- small subset next, verified
- broader rollout, verified at each step
- final batch only after the prior batches have been observed to remain healthy

The gating between stages is explicit. A staged rollout that batches without verification between batches is not staged; it is theatrical.

### 4.3 Canary Where Blast Radius Justifies

Where the blast radius of a change is large (a Kubernetes upgrade, a network configuration change, a shared identity-provider change), canary the change against a representative subset before broad rollout. Canary criteria, observation window, and abort thresholds are defined in the runbook before the change begins.

### 4.4 Apply Halts

The apply halts on:

- prerequisite verification failure
- intermediate verification failure during staged rollout
- monitoring alarm during the apply window
- operator judgment that something looks wrong

A halted apply is not a failed change. It is a successfully deferred change. The change record captures the halt, the cause, and the next step (resume after fix, retry on schedule, abandon).

## 5. Post-Deploy Verification

### 5.1 Verification Is Part of the Change

A change is not complete when the apply succeeds. It is complete when the post-apply verification succeeds. Verification is named in the change record and executed before the change is closed.

Verification covers:

- the change took effect (configuration is what was declared, services are running, network paths are healthy)
- dependent services remain healthy
- customer-facing behavior matches expectations
- no new alerts have fired since apply
- monitoring shows no anomalies in the relevant signals during the verification window

### 5.2 Verification Window

The verification window is explicit. For routine changes it is short (minutes). For changes with delayed blast radius (cron-driven jobs, scheduled rotations, slow-propagating configurations), the window extends to cover the next firing of the affected behavior. The runbook names the window.

### 5.3 Failed Verification Triggers Rollback

If verification fails, the rollback plan from §3.3 executes. Rollback is the default; "fix forward" is a deliberate, recorded escalation rather than a default mode.

## 6. Rollback Posture

### 6.1 Rollback Is Designed In

Every change is designed to be reversible by default. Where reversibility is impossible (data migrations, deletion, irrevocable secret rotation, customer-visible state mutation), the change record explicitly acknowledges the irreversibility and names compensating controls (extended verification window, paired sign-off, staged data migration with reversibility checkpoints).

### 6.2 Rollback Is Tested

For changes that recur (deploy patterns, rotation procedures, recovery flows), the rollback path is exercised on a non-production system or against a synthetic target on a defined cadence. The first execution of a rollback should never happen during a real incident.

### 6.3 Rollback Is Rehearsed Mentally Before Apply

Before apply, the operator can answer:

- what command will I run if this fails?
- where will I observe whether it worked?
- what time budget do I have before the customer-visible impact becomes material?
- who do I notify if the rollback also fails?

If the operator cannot answer these, the change is not ready to apply.

## 7. Runbook Discipline

### 7.1 When a Runbook Is Required

A runbook is required for any operational task that is:

- recurring (deployments, rotations, backups, certificate renewals, OS patching)
- risky (data migrations, identity changes, network reconfiguration)
- time-sensitive in execution (incident-response procedures, failover, restore-from-backup)
- knowledge-bearing (procedures that exist only in operator memory)

A task that does not fit those categories does not require a runbook, but the operator should ask whether it should — most "one-off" operational tasks become recurring within a year.

### 7.2 Runbook Structure

Runbooks follow the canonical Stribog runbook template (`templates/Runbook-Template.md`). The structure ensures every runbook captures:

- trigger (when does this runbook apply)
- prerequisites (what must be true before starting)
- safety notes (what can go wrong, what is irreversible)
- steps (concrete commands, expected output)
- verification (how to know it worked)
- rollback (how to undo)
- post-conditions (what state should exist after)
- escalation (who to call if it fails)

A runbook missing any of these sections is incomplete.

### 7.3 Runbooks Are Tested

A runbook is tested before it is needed. Test execution may be:

- a dry-run against a non-production system
- an exercised live execution during a planned change window
- a tabletop walkthrough where the steps are read aloud against a real environment without applying

A runbook that has never been executed end-to-end is, for practical purposes, a hypothesis. It is marked as such until tested.

### 7.4 Runbook Maintenance

Runbooks drift. They are reviewed:

- after every incident in which they were executed
- on a defined cadence named in the Charter Compliance Annex (typically quarterly for active runbooks, annually for dormant ones)
- whenever a system the runbook touches changes materially

Stale runbooks are worse than absent runbooks because operators trust them.

## 8. Configuration Management

### 8.1 Source of Truth

Every production system has a declared configuration source of truth. The source of truth is a Git-tracked declarative artifact wherever feasible. The Compliance Annex names the source of truth per system tier:

- infrastructure: typically Terraform/OpenTofu, Ansible, or equivalent
- Kubernetes workloads: typically Helm charts, Kustomize overlays, or Argo/Flux-managed manifests
- service configuration: typically a config-management repository or environment-shaped configuration
- secrets: a dedicated secret store (not Git)

### 8.2 Drift Detection

Configuration drift is detected, not assumed absent. The detection mechanism is named in the Compliance Annex. Drift detection runs on a defined cadence and surfaces deviations to the operator.

When drift is detected, the operator does one of:

- reconcile the system back to source of truth
- update source of truth to reflect the intentional drift, with a change record explaining the update
- record the drift in the waiver register if it is intentional but cannot yet be reconciled

Drift left undetected and unaddressed is a slow-motion outage.

### 8.3 Manual Production Tweaks

Manual production tweaks happen — under incident pressure, during exploratory diagnosis, or when the source-of-truth tooling is itself unavailable. Manual tweaks are temporary by definition. After the immediate need is resolved, the tweak is either:

- promoted to source of truth (with a change record)
- reverted

A manual tweak that quietly persists is configuration drift.

### 8.4 Environment Parity

Where the project maintains multiple environments (dev, staging, production), drift between environments is treated with the same seriousness as drift within an environment. Lack of parity is the most common reason "it worked in staging" fails to predict production behavior.

## 9. Secrets Management

### 9.1 Never in Repositories

Secrets are never in repositories — not in source files, not in configuration files, not in test fixtures (except synthetic test secrets explicitly allowlisted), not in documentation, not in commit history. Secret prevention follows the engineering charter §8.1; this section adds the operational-specific clauses.

### 9.2 Secret Store

Every project that uses secrets has a declared secret store. The Compliance Annex names the store and the access pattern. Operators retrieve secrets from the store at use time; they do not cache secrets in shell history, scrollback, or local files.

### 9.3 Rotation

Every secret has a declared rotation cadence. The cadence is enforced through a calendar reminder, automation, or both. Secrets that have outlived their rotation window are surfaced as compliance issues, not as administrative annoyances.

### 9.4 Scope and Least Privilege

Secrets are scoped to the smallest set of actors and systems that genuinely require them. A secret that is "shared across all environments" is rotated and re-scoped. A secret that nobody can identify a current consumer for is rotated and revoked.

### 9.5 Compromise Posture

Every project declares a secret-compromise posture: what counts as compromise, how compromise is detected, and what the immediate response sequence is. Discovering a leaked secret without a pre-existing response plan is the wrong time to start designing one.

## 10. Monitoring and Observability

### 10.1 Tiered Observability Baseline

Every service has a declared observability tier in the Compliance Annex. The tier determines the baseline:

| Tier | Baseline |
|------|----------|
| Critical | Logs, metrics, traces (where applicable), uptime probes, alerting routed to a real respondent, on-call rotation if more than one operator |
| Standard | Logs, metrics, uptime probes, alerting on threshold breaches |
| Background | Logs sufficient for postmortem reconstruction; alerting may be deferred to scheduled review |

A service with no declared tier is presumed Standard.

### 10.2 Alert Routing

Alerts route to a real respondent. Alerts that route to an unmonitored mailbox, a never-checked dashboard, or a Slack channel that nobody watches are not alerts; they are decoration. The respondent is named in the Compliance Annex; for small-team engagements, the respondent is named in the Compliance Annex and the alerting medium reaches them on their actual on-call posture (phone push, SMS, or equivalent).

### 10.3 Alert Hygiene

Alerts are tuned. An alert that fires routinely without action — for any reason, even a "good" reason — desensitizes the operator and degrades the entire alerting surface. Routine-fire alerts are either fixed, suppressed under a documented condition, or removed.

The Compliance Annex names a review cadence for alert hygiene (typically monthly).

### 10.4 Dashboards

For services where active investigation is expected, dashboards exist and are kept current. A dashboard that displays a metric the underlying system no longer emits is misleading and is removed.

### 10.5 Logging Standards

Logs are structured where the runtime supports it. The Compliance Annex names the project's logging conventions (format, level vocabulary, sensitive-field redaction). PII or secret material does not flow into logs.

## 11. Incident Response

### 11.1 Severity Classification

Every incident is classified by severity. The default operational vocabulary is:

| Severity | Definition |
|----------|------------|
| Sev-1 | Customer-impacting outage or security incident with material exposure |
| Sev-2 | Significant degradation, partial outage, or near-miss with customer visibility |
| Sev-3 | Internal degradation or asymptomatic anomaly that warrants response |
| Sev-4 | Maintenance-grade event tracked for completeness |

A project may add finer subdivisions in its Compliance Annex, but the four-tier baseline must remain mappable.

For incidents whose primary character is security rather than availability or performance — confirmed compromise, suspected compromise, vulnerability discovery, supply-chain anomaly — the parallel **Sec-1 / Sec-2 / Sec-3 / Sec-4** vocabulary defined in Stribog Security Posture Standard §10.2 applies. Sec-* and Sev-* may coexist for the same event (a confirmed customer-data compromise is both a Sec-1 and a Sev-1); the most severe applicable classification governs response, and the incident timeline records both classifications. The Compliance Annex names how the project routes Sec-* notifications to its security-incident response path versus its operational-incident response path; the two paths may share infrastructure but the classification distinction is preserved.


### 11.2 Incident Roles

Even in a small-team engagement, incident response has explicit roles played by the same team member at different points if necessary:

- Incident Commander: decides what happens next
- Operator: executes
- Communicator: handles customer and stakeholder updates
- Recorder: captures the timeline

A team member may play multiple roles. The discipline is that the team member switches role consciously and acts according to the role they are currently in.

### 11.3 Customer Communication

For sev-1 and sev-2 incidents that are customer-visible, the project's customer-communication policy applies. The policy is declared in the Compliance Annex and addresses:

- when the customer is notified
- through what channel
- what initial information is provided
- what update cadence is committed to during the incident
- when "all clear" is communicated

Silence during a customer-visible outage is one of the most expensive failure modes in a managed-service engagement.

Incident communications that reach end-users carry the same microcopy and voice discipline as the rest of the user-facing surface. The error-message standard of the [[Stribog UI/UX Standard]] §6.2 and the user-facing release-note rules of the [[Stribog User Documentation Standard]] §4.6 apply: internal exception classes, internal hostnames, and engineer-grade stack traces do not appear in customer-visible incident messaging.

### 11.4 Incident Timeline

Every sev-1 and sev-2 incident has a timeline recorded as the incident unfolds, not reconstructed afterward. The timeline captures:

- when each signal arrived
- when each decision was made and by whom
- when each action was taken and what its effect was
- when the customer was notified, and what they were told
- when the incident was declared resolved

The timeline is the input to the post-mortem.

### 11.5 Stabilization vs Resolution

Incident response separates stabilization (customer-visible impact ends) from resolution ([[ROOT CAUSE]] is addressed). Stabilization is the urgent goal; resolution may take longer and may produce additional change records. The incident is not closed until both are complete or the resolution is explicitly tracked as a follow-up commitment.

## 12. Post-Mortems

### 12.1 When Required

Post-mortems are required for:

- every sev-1 incident
- every sev-2 incident
- any sev-3 incident the operator judges to carry organizational learning
- any near-miss whose investigation would inform future design

A project may set a stricter rule. It may not set a looser one.

### 12.2 Post-Mortem Discipline

Post-mortems are blameless. They focus on the system, the process, and the design — not on individual fault. They produce:

- a factual timeline of what happened
- a root-cause analysis (technical and process-level)
- a list of contributing factors
- action items with owners and due dates
- lessons applicable beyond the immediate incident

### 12.3 Action Items Tracked to Closure

Action items from post-mortems are tracked in the project's durable work system to closure. A post-mortem that produces action items that quietly disappear is a post-mortem that produced nothing.

The Compliance Annex names the cadence at which open post-mortem actions are reviewed (typically at every retrospective or monthly review).

### 12.4 Post-Mortems Are Read

Post-mortems are accessible to every team member who might encounter a similar situation. For small-team projects, that means an indexed, searchable post-mortem record. Post-mortems written and never re-read are the most expensive kind of writing.

## 13. Disaster Recovery

### 13.1 Tested, Not Theoretical

Every project that holds production state has a tested disaster recovery posture. "We have backups" is not a DR posture. A tested restoration on a defined cadence is.

### 13.2 RPO and RTO

Each production service tier declares:

- **Recovery Point Objective** — the maximum acceptable data loss measured in time
- **Recovery Time Objective** — the maximum acceptable downtime during recovery

The values are committed to in writing in the Compliance Annex and, where applicable, in customer engagements. Backup cadence and DR rehearsal cadence are derived from these targets, not the other way around.

### 13.3 Restoration Drills

Restoration drills are performed on a defined cadence. For greenfield projects, the first drill must succeed before the project enters production. For **inherited engagements** — where Stribog assumes operational responsibility for an existing production fleet that was not built by Stribog — the first drill must succeed within the engagement's defined onboarding window, and operating the inherited fleet without a successful drill in that window is itself a recorded risk in the engagement's waiver register.

Subsequent drills surface drift between the documented restoration procedure and the current state of the systems.

A drill that has never succeeded is an unverified hypothesis. A project relying on an unverified DR hypothesis — greenfield or inherited — is operating with an unrecorded waiver.

### 13.4 Off-Site and Off-Trust

Backups are stored at sufficient logical and physical distance from the primary system that a single failure cannot destroy both. The Compliance Annex names the off-site storage strategy and the trust boundary between primary and backup systems (a backup that lives behind the same compromised credential as the primary is not a backup).

## 14. Capacity, Cost, and Lifecycle

### 14.1 Capacity Planning

Production systems have declared capacity headroom. When utilization approaches the headroom threshold, the project either expands capacity, shifts load, or accepts the headroom reduction with a recorded decision. Surprise capacity exhaustion is forbidden by this charter; "surprise" implies the headroom was not being watched.

### 14.2 Cost Posture

Every project that consumes paid infrastructure tracks cost against an expected baseline. Material variance from baseline triggers investigation and either [[remediation]] or a recorded explanation. The Compliance Annex names the cost-tracking cadence.

### 14.3 Lifecycle and Sunset

Every operational asset has:

- a named owner
- a renewal or review cadence
- a sunset path

That includes machines, certificates, DNS records, customer environments, monitoring rules, runbook documents, and credentials. Assets without owners drift to neglect; assets without sunset paths accumulate indefinitely. The Compliance Annex names the inventory mechanism.

## 15. Operational Definition of Done

### 15.1 Change-Level Done

An operational change is done when:

- the change record is complete and accurate
- the apply succeeded
- post-deploy verification succeeded
- no follow-up alerts are firing
- the change record is closed in the durable system
- customer communication, where applicable, has been delivered

### 15.2 Deployment-Level Done

A deployment (multi-change rollout) is done when:

- every change in the rollout is at change-level done
- the staged rollout completed without halt
- the rollback path was not invoked, or if it was, the resulting state is recorded
- any incidents triggered by the deployment are at incident-resolution
- every user-observable behavior change in the rollout carries a published or embargoed user-facing release note per the [[Stribog User Documentation Standard]] §4.6, and the doc-to-release sync gate of that standard's §11 held green

### 15.3 Engagement-Level Done

A customer engagement is at operational compliance when:

- the engagement has a declared service-tier per system
- monitoring and alerting are functional and routed
- runbooks for the recurring operations exist and are tested
- DR posture is declared and tested
- the waiver register reflects every active deviation from this standard
- the renewal/sunset posture for every asset under management is current

## 16. Anti-Patterns

The following anti-patterns are forbidden under this standard:

- production change without a record
- "I'll write the runbook after I do this once"
- rollback plans that are "fix it forward"
- customer-visible outages with no customer communication
- incidents that produce no post-mortem
- post-mortems whose action items disappear
- monitoring whose alerts route nowhere
- DR backups whose restoration has never been verified
- secrets stored in repositories under any rationalization
- configuration drift treated as background noise
- "we'll figure out the rotation later" for a secret in production
- production systems with no declared owner
- staged rollouts that don't actually verify between stages
- alerts that fire routinely and are routinely ignored
- incident timelines reconstructed from memory
- runbooks that exist but have never been executed
- silent manual production tweaks that persist
- environment-parity drift treated as inevitable

This list is not exhaustive. It is illustrative of the failure modes this standard is built to prevent.

---

## 17. Revision History

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 1.0.0 | 1 | 2026-05-03 | Initial governing-reference release. Defined operational change management, pre-deploy and apply discipline, post-deploy verification, rollback posture, runbook discipline, configuration management, secrets management, observability tiers, severity-classified incident response, blameless post-mortem discipline, RPO/RTO declaration, DR drill cadence, capacity/cost/lifecycle posture, and operational definition of done. |
| 1.0.0 | 2 | 2026-05-03 | PATCH revision applied during Charter Set Audit Round 3. §13.3 Restoration Drills clarified to handle **inherited engagements** — where Stribog assumes operational responsibility for an existing production fleet that was not built by Stribog (e.g. the managed-service engagement). The first-drill rule remains; the timing is bounded by the engagement's onboarding window rather than by greenfield project entry into production. Added this §17 Revision History section. No clause was weakened. |
| 1.0.0 | 3 | 2026-05-03 | Editorial revision applied during Charter Set Audit Round 3 closeout. §11.1 Severity Classification extended with a paragraph cross-referencing Stribog Security Posture Standard §10.2 Sec-* vocabulary, making explicit that Sec-* and Sev-* may coexist for the same event and that the Compliance Annex names how routing distinguishes the two response paths. Front-matter `related_docs` extended with [[Stribog-Security-Posture-Standard]], Stribog-Data-and-Privacy-Standard, and [[Stribog-Glossary]]. Closes Round 3 finding F37 (one-way link between operational severity and security severity vocabularies). No normative change. |
| 1.1.0 | 4 | 2026-05-12 | MINOR bump applied during Charter Set Audit Round 6 closeout. §11.3 Customer Communication extended with a paragraph binding incident communications that reach end-users to the [[Stribog UI/UX Standard]] §6.2 error-message standard and the [[Stribog User Documentation Standard]] §4.6 release-note discipline. §15.2 Deployment-Level Done extended with a clause requiring that every user-observable behavior change in a rollout carries a published or embargoed user-facing release note and that the doc-to-release sync gate held. Closes Round 6 finding F62 (operational delivery surfaces did not couple to user-facing documentation). No clause was weakened; the new requirements bind only where the underlying standards' §0.2 applicability holds. |

---
