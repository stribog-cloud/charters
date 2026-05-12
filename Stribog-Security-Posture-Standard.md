---
title: "Stribog Security Posture Standard"
created: 2026-05-04
updated: 2026-05-12
type: stribog/security-posture-standard
status: governing-reference
tags: [charter, governance, hardening, incident, kubevigil, security, stribog]
version: "1.0.0"
revision: 6
last_updated: 2026-05-12
parent_moc: "[[MOC - Stribog Governance]]"
owners: [stribog-team]
---


# Stribog Security Posture Standard

> The binding standard for how Stribog projects address security as a discipline distinct from general engineering. This is a mandate. It governs threat modeling, security architecture review, secure coding, security testing, vulnerability management, supply chain, identity, cryptography, and security incident response.

---

## 0. TL;DR

| Area | Mandate |
|------|---------|
| Threat modeling | Every Stribog project performs and records a threat model before broad implementation. The threat model is a living artifact. |
| Security architecture review | Architectural changes that touch trust boundaries require a security architecture review recorded in an ADR. |
| Secure coding | Security-sensitive paths follow language-specific secure-coding practices named in the Charter Compliance Annex. |
| Security testing | Every project that handles untrusted input has explicit security tests beyond the general test suite. |
| Vulnerability management | Dependency, base-image, and code vulnerabilities are scanned in CI and tracked to closure with severity-bound horizons. |
| Supply chain | Build provenance, dependency pinning, and artifact integrity are part of the release contract. |
| Identity & access | Authentication, authorization, and audit logging are designed in, not bolted on. Least privilege is the default. |
| Cryptography | Cryptographic choices follow current public guidance. Custom cryptography is forbidden. |
| Security incident response | Security incidents are a distinct severity track from operational incidents, with separate disclosure and customer communication discipline. |
| Security audit | Every Stribog project that holds production state or handles untrusted input is security-audited on a defined cadence. |

This standard is binding alongside the Universal Stribog Engineering Charter for any Stribog project that meets the §0.2 applicability criteria. It refines several charter clauses (§3.5 safety by design, §8 security and mutating safety) for the security-discipline context.

## 0.1 Why This Standard Exists

Stribog's work routinely intersects security in ways that cannot be safely treated as ordinary engineering:

- KubeVigil is a security tool. Its own security posture is the product itself.
- Managed-service engagements include pentest readiness, security-control hardening, and vulnerability [[remediation]] as routine [[DELIVERABLES]].
- Stribog operates production infrastructure that holds customer state, secrets, and trust roots.
- Stribog has explored security-adjacent compliance regimes (DPDPA, AIGP) where security posture is a formal requirement.

A general-purpose engineering charter is not enough for this work. Security as a discipline has its own threat model, its own failure modes, its own review cadence, and its own incident response. Treating it as a side concern of general quality assurance produces precisely the failures that pentests catch — failures that cost client engagements, reputation, and in some cases legal exposure.

This standard exists to convert security from a vague aspiration into mechanical, observable, audit-trail-bearing engineering work.

## 0.2 Applicability

This standard binds every Stribog project that satisfies one or more of the following:

- the project is itself a security tool, framework, or assessment artifact (e.g. KubeVigil)
- the project handles untrusted input from external sources (network, API, file upload, user-supplied data)
- the project manages secrets, credentials, certificates, or trust roots
- the project operates production infrastructure
- the project is delivered to a customer with a security expectation in the engagement
- the project handles data classified as Confidential or Restricted under the Stribog Data and Privacy Standard

A Stribog project that satisfies none of the above (a pure utility, an internal automation that processes only Stribog-owned trusted data) is not bound by this standard, but the burden of proof is on the exemption.

## 0.3 Definitions

This standard relies on the Stribog Glossary for cross-cutting terms. Security-specific terms used in this document:

- **Threat model:** a structured analysis of the assets a system protects, the actors who might threaten them, the attack vectors available to those actors, and the controls that mitigate the risk.
- **Trust boundary:** a point in the system architecture where data, control, or identity crosses from one trust domain to another.
- **Security control:** a technical, procedural, or governance measure that mitigates a threat.
- **Security incident:** an event, suspected or confirmed, that compromises the confidentiality, integrity, or availability of Stribog or customer assets, or violates a Stribog security policy.

## 1. Core Positions

Stribog's position on security rests on six points.

1. **Security is a design property, not a polish step.** Security postures are designed into the architecture before implementation, not retrofitted before audit.
2. **Threat models precede implementation.** Every applicable Stribog project has a recorded threat model before broad implementation begins. The threat model is updated when the system's trust boundaries change.
3. **The trust boundary is the smallest unit of security review.** Security is reviewed at boundaries, not within trusted regions.
4. **Least privilege is the default.** Every actor — human, service, agent, automation — has the minimum permissions required to perform its declared role.
5. **Failure honesty applies to security.** Detected vulnerabilities, observed compromises, and suspected indicators are surfaced explicitly, not buried.
6. **Custom cryptography is forbidden.** Cryptographic primitives, protocols, and constructions follow current public guidance and well-reviewed implementations.

These positions are the lens through which every clause below is enforced.

## 2. Threat Modeling

### 2.1 Required Threat Model

Every Stribog project bound by this standard records a threat model. The threat model is part of the project's master reference or lives as an architecture supplement linked from the master reference.

The threat model captures, at minimum:

- **Assets** — what is being protected (data, systems, identity, availability, brand)
- **Actors** — who might threaten those assets (external attacker, malicious insider, compromised dependency, mistaken operator, abusive user)
- **Trust boundaries** — where data, control, or identity crosses trust domains
- **Attack surfaces** — the externally reachable interfaces of the system
- **Threats** — concrete attack scenarios mapped to assets and actors
- **Controls** — the technical, procedural, or governance measures that mitigate each threat
- **Residual risks** — risks that remain after controls are applied
- **Open items** — threats that are known but not yet adequately mitigated

### 2.2 Threat Modeling Methodology

Stribog projects choose a threat modeling methodology appropriate to the project. Acceptable methodologies include:

- **STRIDE** (Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Elevation of privilege) — preferred for general systems
- **PASTA** (Process for Attack Simulation and Threat Analysis) — for higher-stakes systems where attacker simulation is valuable
- **Attack trees** — for analyzing specific high-value attack paths
- **LINDDUN** (Linkability, Identifiability, Non-repudiation, Detectability, Disclosure, Unawareness, Non-compliance) — preferred where privacy threats dominate

The Charter Compliance Annex names the project's chosen methodology. Mixing methodologies within one project is allowed if the rationale is recorded.

### 2.3 Threat Model Maintenance

The threat model is updated when:

- a new trust boundary is added to the system
- an existing trust boundary changes posture
- a new attack surface is exposed
- a new class of actor enters scope
- a security incident reveals a threat the model did not capture
- a major architectural change is made (in lockstep with the corresponding ADR)

A threat model that is materially out of date is out of compliance.

### 2.4 Threat Model Review

The threat model is reviewed at every phase boundary and at every charter audit-round. Review verifies that the model still reflects the system, that controls are still effective, and that residual risks are still acceptable.

## 3. Security Architecture Review

### 3.1 When a Security Architecture Review Is Required

A security architecture review (SAR) is performed and recorded as an ADR when any of the following occurs:

- a new trust boundary is introduced
- the authentication, authorization, or audit-logging architecture changes
- a new external integration crosses a trust boundary
- a cryptographic primitive, protocol, or key-management approach changes
- a new third-party dependency enters a security-sensitive path
- the data classification of state managed by the system changes (per the Stribog Data and Privacy Standard)
- the project takes on a new compliance obligation that has security implications

A SAR is not required for purely additive changes that do not cross trust boundaries.

### 3.2 SAR Discipline

A SAR is documented in an ADR following `templates/ADR-Template.md`. The ADR's Context, Decision, Consequences, and Alternatives sections explicitly address the security implications of the change. The Verification section names how the security posture will be tested or observed.

### 3.3 Reviewer

A SAR is reviewed by at least one Charter Reviewer applying security-specific judgment. For small-team Stribog, this is a team member wearing a critique-class hat (per Charter Governance §11.1) supported by AI agents in critique personas (per `templates/Critique-Persona-Template.md`). For high-stakes engagements, an external security reviewer is consulted.

## 4. Secure Coding Practices

### 4.1 Language-Specific Practices

Secure-coding practices are language-specific. The Charter Compliance Annex for each project names:

- the secure-coding guideline followed (e.g. CERT, OWASP language guides, Go secure-coding patterns)
- the static analysis tools enforcing it
- the code-review checklist that includes security review for security-sensitive paths

### 4.2 Universal Patterns

Across languages, the following are mandated:

- **Input validation at trust boundaries.** Untrusted input is validated for type, length, range, and allowed character set before use. Validation occurs at the boundary, not deep in the call stack.
- **Output encoding contextual to the destination.** Data emitted into HTML, SQL, shell, log, or other contexts is encoded for that context. Concatenated string queries are forbidden where parameterized alternatives exist.
- **Error handling that does not leak.** Errors surfaced to external actors do not include stack traces, internal paths, secret values, or other internal-only information.
- **Secrets-in-code prevention.** Secrets, credentials, tokens, and keys are never in source code, configuration, or test fixtures (except synthetic fixtures explicitly allowlisted per Engineering Charter §8.1).
- **Logging that excludes sensitive material.** Structured logs explicitly redact PII, secrets, and credentials. Redaction is enforced by logging-library configuration, not by per-call discipline.
- **Bounded resource consumption.** Inputs that drive resource consumption (memory, CPU, connections, file handles) are bounded explicitly to prevent resource-exhaustion denial of service.

### 4.3 Code Review for Security-Sensitive Paths

Code that touches security-sensitive paths receives explicit security review. The Charter Compliance Annex names which paths are security-sensitive (typically: authentication, authorization, cryptography, secret handling, input parsing of untrusted data, audit logging).

For small-team Stribog, security review is performed by a team member wearing a critique-class hat, supported by AI agents in critique personas, with attention to the OWASP Top 10 and CWE-25 most-dangerous-weakness patterns relevant to the language.

## 5. Security Testing

### 5.1 Required Security Test Layers

Every Stribog project bound by this standard has explicit security tests beyond general functional testing. The required layers are:

- **Input-validation tests** — boundary, malformed, oversized, malicious, and edge-case inputs at every trust boundary
- **Authentication and authorization tests** — every protected operation rejects unauthenticated access, rejects unauthorized access, and enforces declared least-privilege boundaries
- **Injection tests** — SQL, command, path traversal, log injection, deserialization, where the language and runtime allow them
- **Crypto-misuse tests** — verifying cryptographic operations follow guidance (e.g. random IVs, constant-time comparisons for secrets, key separation)
- **Output-leakage tests** — error responses, logs, and externally visible state do not leak internal-only information
- **Authorization-bypass tests** — direct object reference, missing function-level checks, privilege escalation attempts

### 5.2 Fuzz Testing Where Applicable

Projects that parse untrusted structured input (file formats, network protocols, configuration files, message formats) have fuzz tests against their parsers. The Charter Compliance Annex names the fuzzing tool and runtime.

### 5.3 Pentest Readiness for Customer-Facing Surfaces

Projects with customer-facing surfaces maintain pentest readiness as a continuous discipline, not a one-shot pre-engagement push. The readiness baseline is:

- a current threat model (per §2)
- current security tests passing in CI (per §5.1)
- vulnerability scan results triaged to closure (per §6)
- an inventory of known accepted risks recorded in the waiver register
- a runbook for pentest support (information gathering, scope confirmation, finding triage)

## 6. Vulnerability Management

### 6.1 Continuous Vulnerability Scanning

Every Stribog project bound by this standard runs vulnerability scans in CI, at minimum on every primary-branch commit. The Charter Compliance Annex names the tools per scan class:

- **Dependency vulnerability scanning** — for the project's third-party dependencies
- **Base-image scanning** — for container images (operating-system packages, embedded runtimes)
- **Secret scanning** — over reachable Git history (per Engineering Charter §8.1)
- **Static security analysis** — code-level pattern matching for known weakness classes
- **Infrastructure-as-code scanning** — for Terraform, Helm, Kubernetes manifests, where applicable

### 6.2 Triage Discipline

Every detected vulnerability is triaged within a horizon defined by severity:

| Severity | Triage horizon | Remediation horizon |
|----------|----------------|---------------------|
| Critical | 24 hours | 7 days |
| High | 72 hours | 30 days |
| Medium | 7 days | 90 days |
| Low | 30 days | next routine cycle |

Triage produces one of:

- a remediation work item (patch, version bump, configuration change)
- a risk acceptance recorded in the waiver register with compensating controls
- a determination that the vulnerability does not apply to this project's actual usage

The triage outcome is recorded; "we'll look at it later" is not a triage outcome.

### 6.3 Embargoed Vulnerabilities

For embargoed vulnerabilities (CVEs disclosed under coordinated disclosure), Stribog projects respect embargo until public disclosure. The compliance-relevant point is that the project's vulnerability response process must be capable of handling pre-disclosure information without leaking it.

### 6.4 Vulnerability Disclosure for Stribog Projects

For Stribog projects that distribute software (KubeVigil and similar), the project publishes a `SECURITY.md` declaring:

- the private reporting channel for security issues
- the supported-version posture
- the disclosure timeline (typically 90 days from report or coordinated public disclosure, whichever is sooner)
- credit and acknowledgment posture

`SECURITY.md` reflects the real process. Governance theater is forbidden per Engineering Charter §15.

## 7. Supply Chain Security

### 7.1 Build Provenance

Release artifacts produced by Stribog projects carry verifiable provenance. The Charter Compliance Annex names the provenance mechanism: signed tags, signed releases, SLSA-level attestations, container image signing (cosign), or equivalent.

### 7.2 Dependency Pinning

Direct dependencies are pinned to specific versions, not floating against major or minor ranges. The pin file (`go.mod`, `package-lock.json`, `requirements.txt`, `Cargo.lock`, etc.) is committed and is part of the build contract.

### 7.3 Dependency Review

New dependencies entering security-sensitive paths receive explicit review covering:

- maintainer reputation and project health
- license compatibility
- transitive dependency footprint
- vulnerability history
- alternative options considered

The review is recorded in an ADR for non-trivial dependency additions to security-sensitive paths.

### 7.4 Artifact Integrity

Release artifacts published to public surfaces (package managers, install scripts, container registries, GitHub Releases) are accompanied by integrity material — checksums, signatures, or both — sufficient for a downstream user to verify they obtained an authentic artifact.

Install scripts that download and execute material from the network verify integrity before execution.

## 8. Identity, Authentication, and Authorization

### 8.1 Identity Discipline

Every Stribog system that authenticates actors has a declared identity model:

- what counts as an identity (human user, service, agent, automation)
- where identities are issued, rotated, and revoked
- how identities are bound to authentication credentials

The identity model is named in the master reference and reflected in the Compliance Annex.

### 8.2 Authentication Posture

Authentication mechanisms follow current public guidance. The Charter Compliance Annex names:

- the authentication primitives used (password + MFA, SSO/OAuth/OIDC, passwordless, mTLS, API keys)
- the credential storage approach (where applicable)
- the session model (token format, expiry, refresh discipline)
- the rate-limit and lockout posture against brute-force and credential-stuffing attacks

Custom authentication primitives are forbidden. Use well-reviewed implementations.

### 8.3 Authorization as Least Privilege

Every protected operation requires a positive authorization decision. The default is deny. Authorization is enforced at the boundary closest to the operation, not only at the front door.

The authorization model is documented at the master-reference level (RBAC, ABAC, capability-based, or hybrid) and the per-operation enforcement is verifiable through the §5 test layers.

### 8.4 Audit Logging

Every privileged operation, every authentication event, and every authorization-decision boundary produces an audit log entry containing, at minimum:

- the actor identity (or "unauthenticated")
- the operation requested
- the decision (allowed / denied / error)
- a timestamp
- a correlation identifier sufficient to reconstruct the request flow

Audit logs are protected per the Stribog Data and Privacy Standard and are not subject to operator-side mutability without governance trail.

## 9. Cryptography

### 9.1 Algorithm Choices

Cryptographic algorithm choices follow current public guidance (NIST, IETF, current OWASP). The Charter Compliance Annex names:

- the symmetric-encryption suite (e.g. AES-GCM with declared key length)
- the asymmetric and key-exchange primitives
- the hash functions (e.g. SHA-256 family, BLAKE3) and their use contexts
- the password-hashing function (e.g. argon2id, scrypt, bcrypt) with declared parameters
- the random-number source (cryptographic RNG provided by the platform)

### 9.2 Key Management

Cryptographic keys are:

- generated using a cryptographic RNG
- stored in a dedicated key-management system or secret store named in the Compliance Annex
- scoped to the smallest set of consumers
- rotated on a defined cadence
- never in source code, configuration files, logs, or test fixtures (except synthetic test material per Engineering Charter §8.1)

Key compromise has a declared response sequence in the Compliance Annex.

### 9.3 Forbidden Patterns

The following are forbidden under this standard:

- custom cryptographic primitives or constructions
- cryptographic operations using deprecated algorithms (MD5, SHA-1 for security-relevant use, DES, RC4, ECB-mode block ciphers)
- non-constant-time comparisons for secret material
- predictable IVs or nonces in modes that require unpredictable ones
- shared keys across environments (production keys are never the same as staging or development keys)
- bundling private keys in distributed artifacts

## 10. Security Incident Response

### 10.1 Distinct from Operational Incident Response

Security incident response is a distinct discipline from operational incident response (governed by Operational Delivery Standard §11–§12). The disciplines overlap (a security incident often produces customer-visible operational impact) but the response paths differ in three key respects:

- **Disclosure constraints** — security incidents may have legal, contractual, or coordinated-disclosure obligations that shape what is communicated, when, and to whom
- **Forensic preservation** — security incidents may require state preservation that conflicts with normal stabilize-and-restore operational pressure
- **Customer communication** — security incidents have customer-communication obligations distinct from outage communication, including under DPDPA (per the Stribog Data and Privacy Standard)

### 10.2 Security Incident Severity

Stribog uses a parallel severity vocabulary for security incidents:

| Security Severity | Definition |
|-------------------|------------|
| Sec-1 | Confirmed compromise of customer data, credentials, or production systems with material exposure |
| Sec-2 | Strong indicator of compromise, or confirmed compromise with limited exposure |
| Sec-3 | Suspicious indicator that warrants [[INVESTIGATION]] |
| Sec-4 | Vulnerability discovery or near-miss without active exploitation |

Sec-* and Sev-* may coexist for the same event. The most severe applicable classification governs response.

### 10.3 Initial Response

On detection of a Sec-1 or Sec-2 incident:

1. **Preserve.** State that may be forensically relevant is preserved before remediation begins.
2. **Contain.** Compromise is contained — affected credentials revoked, affected systems isolated, attacker access removed.
3. **Notify (internal).** The Charter Owner / Project Compliance Owner is notified immediately.
4. **Notify (customer).** Per the customer's contracted notification timeline and the Stribog Data and Privacy Standard.
5. **Notify (regulator).** Per applicable regulatory regime (DPDPA reporting timelines where relevant).
6. **Investigate.** [[ROOT CAUSE]] and scope are determined.
7. **Remediate.** Affected systems are restored, controls are strengthened.
8. **Post-mortem.** Per Operational Delivery Standard §12, plus the security-specific concerns in §10.4.

### 10.4 Security Post-Mortem Discipline

Security post-mortems extend the operational post-mortem template (`templates/Audit-Closeout-Template.md` adapted) with:

- **Indicator timeline** — when each indicator of compromise was first observed and whether it was acted on
- **Detection-gap analysis** — why the compromise was not detected earlier
- **Control-gap analysis** — which controls failed, which were missing
- **Customer-impact assessment** — confirmed and possible exposure
- **Disclosure record** — to whom, when, what was disclosed
- **Lessons applied to the threat model** — explicit updates to §2 artifacts

Security post-mortems may be subject to legal hold or counsel-driven scope; the operator coordinates with counsel where engagement contracts or regulation require it.

## 11. Security Audit Cadence

### 11.1 Project Security Audit

Every Stribog project bound by this standard receives a security audit:

- at project go-live (initial production exposure)
- at every major architecture change
- on a defined cadence named in the Compliance Annex (typically annually)
- on triggering events (incident, customer audit, regulatory inquiry)

Audits are recorded under `templates/Audit-Closeout-Template.md` with security-specific findings classified by severity.

### 11.2 External Security Assessment

For projects with material customer-facing surfaces, external assessment (third-party pentest, code review, audit) is performed on a cadence appropriate to the engagement risk. The Charter Compliance Annex names the cadence and the assessor selection criteria.

External findings are tracked to closure in the same waiver-or-remediation discipline as internal findings.

### 11.3 Charter-Set Security Review

The Stribog charter set itself is reviewed for security implications at every charter audit-round (per Charter Governance §8). Security review verifies that:

- the canon's clauses do not implicitly require unsafe practices
- new clauses do not create exfiltration or compromise vectors
- clauses dependent on third-party tools account for tool compromise

## 12. Anti-Patterns

The following are explicitly forbidden under this standard:

- shipping a security-relevant project without a recorded threat model
- treating security as a final-polish step before release
- implementing custom cryptographic primitives or protocols
- using deprecated cryptographic algorithms in security-relevant paths
- shared keys or credentials across environments
- security incidents handled through the general operational-incident path without distinct disclosure consideration
- vulnerability scan results that accumulate without triage
- "security review" performed by the same hat that wrote the code without a separate critique-class pass
- pentest readiness treated as pre-engagement scrambling rather than continuous discipline
- secrets stored in source code, configuration files, test fixtures (except synthetic), or logs
- audit logs subject to silent operator mutation
- governance theater (a `SECURITY.md` that does not describe the real disclosure process)
- threat models that have not been updated since the system's trust boundaries last changed
- new security-sensitive dependencies added without ADR-grade review

This list is not exhaustive. It is illustrative of the failure modes this standard is built to prevent.

---

## 13. Revision History

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 1.0.0 | 1 | 2026-05-03 | Initial governing-reference release. Defined required threat modeling, security architecture review, secure coding practices, security testing layers, vulnerability management with severity-bound triage and remediation horizons, supply chain (provenance, dependency pinning, dependency review, artifact integrity), identity and access (least privilege default, audit logging), cryptographic posture (custom cryptography forbidden), security incident response distinct from operational incident response, and security audit cadence. |
| 1.0.0 | 2 | 2026-05-03 | Editorial revision applied during Charter Set Audit Round 3 closeout. Added this §13 Revision History section to satisfy Documentation Standard §12 Definition of Done (Revision History required for governing-reference documents). Closes Round 3 finding F40 (governing standard lacked Revision History). No normative change. |

---
