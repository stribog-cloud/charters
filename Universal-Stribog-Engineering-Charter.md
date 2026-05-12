---
title: "Universal Stribog Engineering Charter"
created: 2026-05-04
updated: 2026-05-12
type: stribog/engineering-charter
status: governing-reference
tags: [anthropic, charter, docker, governance, k8s, obsidian, stribog]
version: "1.2.0"
revision: 13
last_updated: 2026-05-12
parent_moc: "[[MOC - Stribog Governance]]"
owners: [stribog-team]
---


# Universal Stribog Engineering Charter

> The governing engineering charter for Stribog. This is a mandate. It binds every Stribog project across every language, runtime, and delivery model.

---

## 0. TL;DR

| Area | Mandate |
|------|---------|
| Architecture | Reference-first and contract-first. Broad implementation does not begin before the governing reference exists and is current. |
| Development method | Test-Driven Development is the default cycle: `red → green → refactor`. Bug fixes start with a failing reproduction. |
| Behavioral validation | BDD-style fixtures and scenarios are encouraged where they sharpen acceptance behavior. They do not displace TDD. |
| Coverage | **96% total line coverage is mandatory** for every Stribog project, measured against the declared production-code boundary. |
| Documentation | Documentation is part of the system. A project that ships behavior with stale references is incomplete. |
| Safety | Mutating workflows must be bounded, previewable, reversible where feasible, and verified after change. |
| Delivery | Trunk-based history, explicit quality gates, reproducible release artifacts, and audit closeout for serious milestones. |
| AI agents | Agents operate against written references, preserve TDD discipline, and surface uncertainty honestly. Their compliance is governed by a dedicated standard. |
| Operations | Managed services, infrastructure, and rolling-deployment work are bound by the Stribog Operational Delivery Standard alongside this charter. |
| Waivers | Every exception is named, scoped, owned, dated, and recorded in the project's waiver register. |

This charter is binding. There is no implicit waiver. A project either complies, holds a written waiver against a named clause, or is out of compliance.

## 0.1 Why This Charter Exists

Stribog presents to clients as an enterprise-shaped delivery organization; a fleet spanning hypervisors, container runtimes, and managed services; and a growing share of the actual engineering work is performed by AI agents executing against written instructions.

This combination is unforgiving. It removes the cushions that protect larger organizations:

- there is no second engineer to catch architectural drift in code review
- there is no separate QA team to compensate for thin test coverage
- there is no operations team to clean up after a fragile release
- there is no senior reviewer in another time zone to question a sloppy decision
- there is no institutional memory other than what is written down

The cost of any one of those cushions failing in a larger organization is absorbed by the organization. The cost of any one of those cushions failing at Stribog is absorbed by the project, the client engagement, or the operator personally.

This charter exists because the only sustainable answer to that asymmetry is engineering discipline made explicit, mechanical, and difficult to bypass. It is the cushion. Every rule below converts a class of failure that would otherwise compound silently into a failure that surfaces early, audibly, and recoverably.

## 0.2 Applicability and Binding Force

This charter binds every Stribog-owned project, including:

- private repositories
- public repositories
- internal automation
- client-facing infrastructure
- experimental or research code expected to outlive a single session
- documentation projects of governing or reference grade

It applies in full unless one of the following holds:

- a written waiver exists in the project's waiver register, citing the specific clause, scope, reason, owner, compensating controls, and expiry
- a more local Stribog standard refines this charter without weakening it (e.g. a per-language Charter Compliance Annex that tightens specific mandates)

The default assumption is that any non-trivial Stribog repository is in scope. The burden of proof rests on any exception, never on the charter.

## 0.3 Definition of a Stribog Project

This charter binds **Stribog projects**. A Stribog project is any work product that satisfies one or more of the following:

1. it has a Stribog-owned Git repository
2. it has a planned working life beyond a single session
3. it is, or will be, customer-facing or billed against a client engagement
4. it manages production state, secrets, or infrastructure
5. it is published publicly under Stribog or a Stribog-controlled organization
6. it is referenced by other Stribog projects as a dependency or contract

Disposable spikes, throwaway scratch work, and one-off scripts that satisfy none of the above are not Stribog projects and are not bound by this charter. They must, however, be deleted or promoted to compliance before being merged into any Stribog project repository.

The promotion rule is absolute: a spike that survives is a Stribog project, and the moment it survives, it is bound by this charter retroactively from that point forward.

## 0.4 Governance Stack

> Diagrams are written in `D2`. Use the D2 Obsidian plugin to render them inline; without it Obsidian shows the D2 source directly. For this BrainForest location, the embedded `d2` block is the canonical diagram source artifact.

```d2
direction: down

classes: {
  governance_group: {
    shape: rectangle
    style: { fill: "#f7f0e6"; stroke: "#8f6a3c"; stroke-width: 2 }
  }
  governance_item: {
    shape: rectangle
    style: { fill: "#fffaf3"; stroke: "#b78b56"; stroke-width: 2 }
  }
  annex_group: {
    shape: rectangle
    style: { fill: "#f4eefb"; stroke: "#7655a8"; stroke-width: 2 }
  }
  annex_item: {
    shape: rectangle
    style: { fill: "#fdfaff"; stroke: "#9270c0"; stroke-width: 2 }
  }
  project_group: {
    shape: rectangle
    style: { fill: "#e8f1ec"; stroke: "#2f6d58"; stroke-width: 2 }
  }
  project_item: {
    shape: rectangle
    style: { fill: "#f7fbf8"; stroke: "#5f8b79"; stroke-width: 2 }
  }
  execution_group: {
    shape: rectangle
    style: { fill: "#eef2fb"; stroke: "#5473a3"; stroke-width: 2 }
  }
  execution_item: {
    shape: rectangle
    style: { fill: "#f8faff"; stroke: "#7f97bc"; stroke-width: 2 }
  }
  assurance_group: {
    shape: rectangle
    style: { fill: "#fbf2e8"; stroke: "#c07628"; stroke-width: 2 }
  }
  assurance_item: {
    shape: rectangle
    style: { fill: "#fffaf4"; stroke: "#d39a5a"; stroke-width: 2 }
  }
}

governance: "Stribog Governance Layer\n(universal, language-agnostic)" { class: governance_group
  charter: "Universal Stribog\nEngineering Charter" { class: governance_item }
  docs: "Stribog\nDocumentation Standard" { class: governance_item }
  agents: "Stribog AI Agent\nExecution Standard" { class: governance_item }
  ops: "Stribog Operational\nDelivery Standard" { class: governance_item }
  security: "Stribog Security\nPosture Standard\n(applies per §0.2)" { class: governance_item }
  privacy: "Stribog Data and\nPrivacy Standard\n(applies per §0.2)" { class: governance_item }
  glossary: "Stribog Glossary\n(authoritative term meaning)" { class: governance_item }
  cgov: "Charter Governance\n(lifecycle · versioning · compliance)" { class: governance_item }
}

annex: "Per-Project Specialization Layer" { class: annex_group
  compliance: "Charter Compliance Annex\nlanguage · stack · tooling" { class: annex_item }
}

project: "Per-Project Control Layer" { class: project_group
  reference: "Master Reference\nsource of truth" { class: project_item }
  supplements: "Architecture Supplements\nADRs · contracts · constraints" { class: project_item }
  plan: "Build Plan\nmilestones · gates · dependencies" { class: project_item }
  local_rules: "Local Agent Rules\nCLAUDE.md · AGENTS.md" { class: project_item }
  waivers: "Waiver Register" { class: project_item }
}

execution: "Execution Layer" { class: execution_group
  tdd: "TDD\nred → green → refactor" { class: execution_item }
  implementation: "Implementation\ncode · tests · fixtures" { class: execution_item }
  docsync: "Documentation Sync\nupdate references with reality" { class: execution_item }
}

assurance: "Assurance Layer" { class: assurance_group
  gates: "Quality Gates\nlint · static · tests\ncoverage 96% · secrets · build" { class: assurance_item }
  audit: "Audit / Certification\nphase closeout · release readiness" { class: assurance_item }
  release: "Release / Operational State\nversioned · documented · reproducible" { class: assurance_item }
}

governance.charter -> annex.compliance: "binds via annex"
governance.docs -> project.reference: "defines form"
governance.agents -> execution.tdd: "binds agents"
governance.ops -> assurance.release: "binds operational delivery"
governance.security -> project.supplements: "threat model · SARs"
governance.privacy -> project.supplements: "classification · lifecycle"
governance.glossary -> project.reference: "authoritative term meaning"
governance.cgov -> annex.compliance: "compliance declaration"

annex.compliance -> project.reference
annex.compliance -> project.local_rules
annex.compliance -> project.waivers

project.reference -> project.supplements
project.reference -> project.plan
project.plan -> execution.tdd
project.local_rules -> execution.tdd
project.supplements -> execution.implementation

execution.tdd -> execution.implementation
execution.implementation -> execution.docsync
execution.docsync -> assurance.gates
assurance.gates -> assurance.audit
assurance.audit -> assurance.release
```

The full canon of Stribog governing documents is:

| Document | Role |
|----------|------|
| Universal Stribog Engineering Charter | This document. The binding baseline for engineering discipline. |
| Stribog Documentation Standard | The form, shape, and maintenance rules for Stribog documents. |
| Stribog AI Agent Execution Standard | The binding rules for AI agents operating on Stribog projects. |
| Stribog Operational Delivery Standard | The binding rules for managed-service, infrastructure, and rolling-deployment work. |
| Stribog Security Posture Standard | The binding rules for threat modeling, security architecture, vulnerability management, and security incident response. |
| Stribog Data and Privacy Standard | The binding rules for data classification, lifecycle, residency, subject rights, and breach notification. |
| Stribog Glossary | The authoritative cross-document terminology reference. |
| Charter Governance | The lifecycle, versioning, and compliance-declaration rules for the charter set itself. |
| Charter Compliance Annex (per project) | The per-language or per-stack specialization that names concrete tooling for a project and pins the charter version it is bound by. |

A Stribog project must declare which version of this charter it is bound by, in its Charter Compliance Annex. Projects do not float against the latest charter; they pin to a version.

## 0.5 Compliance Tiers

Not every Stribog project carries the same operational risk. The charter applies to all of them, but the form in which it applies is graduated through three compliance tiers. Every Stribog project declares its tier in the Charter Compliance Annex.

| Tier | Scope | Discipline |
|------|-------|------------|
| **Foundation** | All Stribog projects (per §0.3). | Universal charter applies in full. Coverage floor 96%. Reference-first. TDD. Full quality-gate set. Documentation, audit, and waiver discipline. |
| **Working** | Working-grade projects: small tools, internal automations, exploratory utilities that are kept beyond a single session but are not yet customer-facing or production-stateful. | Foundation tier with two relaxations: (a) the master reference may be a condensed single-section document rather than the full §2.1 artifact set, until the project is promoted to Reference tier; (b) phased build plan is optional. All other Foundation rules apply. |
| **Reference** | Customer-facing projects, production-stateful systems, public repositories, security-sensitive systems, and any project named in a customer engagement. | Foundation tier in full. Additionally: full §2.1 artifact set is mandatory, security and privacy standards apply where their §0.2 criteria are met, audit-closeout records are mandatory at every phase boundary. |

The Working tier is not a permanent home. A project that becomes customer-facing, holds production state, or grows past exploratory scope is promoted to Reference tier. Promotion is recorded in the Compliance Annex with a Reference-tier compliance audit before the next material change ships.

The Working tier is not a workaround for §0.3. A project that satisfies any of the §0.3 promotion criteria is a Stribog project at Foundation tier minimum, and is bound by this charter. The Working tier is a recognition that the full Reference-tier artifact set is excessive overhead for projects that have not yet earned it; it is not a path to compliance avoidance.

## 0.6 What This Charter Does Not Govern

The negative space matters. This charter explicitly does not govern:

- **Disposable spikes and one-off scratch work** that satisfy none of the §0.3 criteria. These are not Stribog projects.
- **Customer-owned code that Stribog only consults on** without [[CONTRIBUTING]] to the repository. The customer's own engineering practices govern that code; Stribog's engagement [[DELIVERABLES]] (assessments, recommendations, runbooks Stribog produces) are governed by this charter.
- **Sales material, proposals, marketing, and external communications.** These have their own discipline (clarity, accuracy, brand) but are outside the engineering scope of this charter. Where such material asserts technical claims, the underlying engineering work that supports those claims is governed.
- **Statutory and contractual obligations** that arise outside the engineering process (corporate filings, tax compliance, MSA-level contractual terms). Where engineering decisions intersect contracts (data residency, deletion guarantees, SLA commitments), the engineering decisions are governed by this charter and the Stribog Data and Privacy Standard or Operational Delivery Standard as applicable.
- **Personal hobby projects** undertaken outside of any Stribog organizational context. A personal project that is later transferred into a Stribog repository is a Stribog project from the date of transfer.

Projects that fall into these categories may still benefit from the discipline this charter codifies. Voluntary adoption is allowed and encouraged. Mandatory binding is not.

## 1. Core Engineering Positions

Stribog engineering rests on six positions.

1. **Architecture must be written down before it is scaled.** A serious project must have a governing reference before broad implementation begins. The reference is the contract between the engineer's understanding and the system's eventual shape.
2. **Contracts are stronger than convenience.** Interfaces, invariants, schemas, and control surfaces are made explicit before broad feature growth, not after.
3. **Tests shape the system.** Tests are not validation after the fact; they are part of how APIs, behavior, and design boundaries are formed.
4. **Documentation is part of the build.** A project that ships behavior with stale governing documents is unfinished, regardless of how the code looks.
5. **Risky behavior must be bounded.** Systems that mutate user state, infrastructure, or external systems default to safety, clarity, and recoverability.
6. **Quality must be measured.** Coverage, benchmarks, audits, release checks, and verification loops exist because intuition is not a control system.

These positions are not aspirational. They are the lens through which every clause below is enforced.

## 2. Project Governance Model

Every Stribog project must maintain a coherent project control plane.

### 2.1 Required Governing Artifacts

The minimum artifact set for a Stribog project is:

| Artifact | Purpose | Required when |
|----------|---------|---------------|
| Charter Compliance Annex | Names the charter version this project pins to, and specifies language/stack-specific concretizations. | At project inception. Before broad implementation. |
| Master reference | Defines problem, architecture, source-of-truth, boundaries, phases, and deliberate choices. | Before broad implementation. |
| Architecture supplements | Deep dives for subsystems whose precision exceeds what the master reference can cleanly hold. | When the subsystem becomes non-trivial. |
| Testing strategy | Defines testing layers, fixture posture, contract strategy, and verification philosophy. | Once the project's testing surface becomes non-trivial. |
| Build plan | Converts architecture into milestones, acceptance criteria, dependencies, and quality gates. | Before multi-phase implementation. |
| Local agent rules | Project-specific working constraints for AI agents, typically `CLAUDE.md` and `AGENTS.md`. | Early, before sustained AI-assisted contribution. |
| Audit / certification record | Records whether a phase or release is actually ready. | Before phase closeout or any release marked as serious. |
| Changelog or release history | Records externally meaningful change. | Before shipping any meaningful version. |
| Waiver register | Records every active charter waiver, its scope, owner, and expiry. | At project inception. Empty is acceptable; absent is not. |

### 2.2 Source-of-Truth Discipline

Every Stribog project must explicitly state, in its master reference:

- what is authoritative versus advisory
- what is a source of truth versus a derived projection
- what is frozen versus still exploratory
- what is shipped versus internal-only

This rule applies to code, data, configuration, and documentation alike. Ambiguity here is the most expensive ambiguity any system can carry.

### 2.3 Durable Work Tracking

Multi-session, multi-phase, or non-trivial work must be tracked in a durable issue or work system. The mechanism may vary (the Charter Compliance Annex names the chosen system); the requirement does not.

The tracking system must answer, at any point:

- what is currently in flight
- why each item exists
- what has changed
- what remains open
- what was consciously deferred and why

Chat logs, oral memory, and scrollback are not durable. A waiver-tracking system that does not survive a closed terminal does not exist.

### 2.4 Additive Architectural Evolution

Once a project's shape is established, architectures evolve additively unless a deliberate rewrite decision is recorded in an ADR.

That means:

- existing seams are extended, not casually rewritten
- new layers preserve the earlier control model
- materially altering architecture requires an ADR

The burden of proof is on any rewrite. "It felt cleaner" is not a justification.

## 3. Architecture Standard

The architecture baseline is intentionally conservative. Stribog projects optimize for legibility, recoverability, and cross-language portability of patterns over local cleverness.

### 3.1 Reference-First and Contract-First

The expected order of work is:

1. define the problem and its boundaries
2. define the source-of-truth and projection layers
3. define subsystem contracts and invariants
4. define phased implementation and quality gates
5. only then implement broadly

Broad implementation before these artifacts exist is **forbidden** for Stribog projects.

This rule is contested in industry, so it is restated explicitly:

- **Spikes are allowed and encouraged** when the problem domain is genuinely unfamiliar and the cost of designing without empirical contact is too high.
- **The compliant pattern is** `spike → discard → write reference → implement test-first`.
- **The non-compliant pattern is** `spike → keep → grow indefinitely → write reference last (or never)`.
- **Merging a spike into the primary branch without prior promotion through reference-and-test-first discipline is forbidden.** This rule is consistent with §0.3: a spike that has not been deleted or promoted before merge is, by definition, an unsanctioned addition to a Stribog project repository.

A spike branch must be deleted or fully promoted (reference written, tests-first implementation produced) before any of its code lands on the project's primary branch. The spike provides learning; it does not provide architecture, and it does not provide the implementation that ships.

### 3.2 Explicit Boundaries

Every architecture must make the following boundaries explicit:

- **data boundaries** — what state lives where, who owns it
- **trust boundaries** — which surfaces are trusted, which are not
- **interface boundaries** — what crosses each transport
- **failure boundaries** — what fails together, what fails independently
- **safety boundaries** — what is mutating, where the dry-run lives

If a reviewer cannot point to all five in the reference set, the architecture is underspecified.

### 3.3 Thin Interface Layers

External interfaces — CLI, API, MCP, UI, scheduled jobs, automation entrypoints — must be thin layers over a shared core wherever the problem permits.

The default preference is:

- a single shared core of behavior
- thin transport layers above the core
- explicit data contracts at every boundary
- no duplicated business logic across entrypoints

Duplicated business logic across transports is one of the most expensive forms of drift in long-lived systems.

UI surfaces (web, mobile, desktop, dashboard, terminal UI, embedded) are bound by the [[Stribog UI/UX Standard]] for the surface-specific contract — design tokens, component state contract, accessibility, microcopy, internationalization, performance budgets, telemetry consent. Developer-callable surfaces (API, SDK, library, plugin seam) are bound by the [[Stribog Developer Documentation Standard]] for the public surface map, the generated reference contract, the deprecation discipline, and the code-sample test contract. User-operable surfaces (any surface a non-implementer touches) are bound by the [[Stribog User Documentation Standard]] for the Diátaxis content architecture, in-product help governance, evidence discipline, and the doc-to-release sync gate.

### 3.4 Dependency Posture

Stribog projects prefer boring, inspectable, and justified dependencies.

The dependency standard is:

- the standard library of the host language is the first option
- a third-party dependency is added only when it materially earns its place
- core runtime, security, storage, and parsing paths are held to a stricter bar than auxiliary code
- unusual or high-risk dependencies are named and justified in the master reference

The Charter Compliance Annex for each project additionally names a dependency cap, a review cadence, or both, appropriate to that language and runtime.

### 3.5 Safety by Design

If a system mutates files, databases, infrastructure, or any user-controlled state, the architecture must account for:

- preview or dry-run behavior, where the action is meaningfully previewable
- explicit opt-in escalation for higher-risk actions
- post-mutation verification
- backup, snapshot, or recovery posture, where feasible
- partial-failure behavior with clear exit semantics
- end-to-end auditability of what changed

These are not optional. A mutating system that lacks any of them is non-compliant by default.

For systems whose mutations affect production state, customer infrastructure, or shared services, the safety-by-design rule above is the architectural baseline; the operational discipline (change records, dry-run-first, rollback posture, post-mutation verification windows, incident response if mutation surfaces a defect) is governed by the Stribog Operational Delivery Standard §3 through §6 and §11.

## 4. Development Method

### 4.1 TDD Is Mandatory

For Stribog projects, the default development method is Test-Driven Development.

The required cycle is:

1. write the failing test
2. observe the failure
3. implement the smallest correct change that produces a passing test
4. refactor while preserving green

The rule is not "write tests soon." The rule is "write the test first." For AI-assisted work, the agent may produce the failing test and the implementation in the same turn; the test must still fail before the implementation is run, and the failure must be observable in the closeout evidence.

### 4.2 Spike, Discard, Rewrite

A spike is allowed when the problem domain is genuinely unfamiliar. The compliant pattern is:

1. open a spike branch
2. explore, learn, prove or disprove a hypothesis
3. record the lessons in an ADR or a master-reference draft
4. delete the spike branch
5. begin the real work test-first

The non-compliant pattern is to grow a spike into production code and add tests later. That is retrofit validation, not TDD, and it is forbidden except under emergency waiver.

### 4.3 Bug Fixes Begin With Reproduction

A bug fix is not complete engineering unless the bug is first captured in a failing test, fixture, or reproducible scenario. The default flow is:

1. encode the bug as a failing unit, integration, contract, golden, or end-to-end test
2. fix the code
3. retain the regression test permanently unless there is a documented reason not to

### 4.4 Test Infrastructure Is Subject to TDD

Helpers, fixtures, generators, harnesses, mock transports, validation scripts, scenario runners, and shell-test scaffolding are not exempt from TDD. If they are important enough to rely on, they are important enough to validate.

### 4.5 BDD Where It Sharpens Behavior

BDD-style thinking is encouraged when it improves behavioral clarity. Good uses include:

- end-to-end operator workflows
- acceptance scenarios
- recovery and [[remediation]] flows
- CLI behavior
- documented `given / when / then` expectations attached to fixtures

The Charter Compliance Annex for each project names the BDD framework where one is used. BDD complements TDD; it does not replace the requirement to write tests first.

## 5. Testing, Coverage, and Quality Gates

### 5.1 Layered Testing Is Required

Every Stribog project must define its testing layers intentionally. The usual layers are:

- unit tests
- integration tests
- contract tests
- golden tests
- end-to-end tests
- benchmark or performance tests, where performance materially matters

Not every repository needs every layer in equal volume. Every repository must explain which layers it relies on, why, and what each layer is responsible for catching. That explanation lives in the project's testing strategy document.

### 5.2 Test Infrastructure Is First-Class

Fixtures, generators, loaders, scenario harnesses, mocks, validation scripts, and end-to-end orchestration utilities are engineering assets. They must be:

- designed intentionally
- tested
- maintained alongside the project
- structured to reduce friction for future test growth, not to accumulate as ad hoc debris

### 5.3 Shift-Left Quality Enforcement

Stribog projects catch defects as early as possible. The shift-left posture includes:

- static analysis appropriate to the language
- linting
- race detection where the runtime supports it and concurrency is real
- coverage tracking
- dependency or vulnerability scanning
- contract enforcement in CI

Shift-left work is not adjacent to testing; it is part of the testing posture.

### 5.4 Coverage Mandate

**96% total line coverage is mandatory for every Stribog project.**

This is a floor, not a target. A project below the floor is out of compliance and must either rise to it, hold a written waiver against this clause with a defined remediation horizon, or be archived.

A 96% floor is achievable when:

- the codebase is structured for testability from the first commit
- thin layers are exercised through integration tests rather than mocked unit tests
- generated code is excluded explicitly via the coverage boundary, not hidden tacitly
- the test infrastructure is treated as a first-class asset
- contract and golden tests cover the seams that unit tests cannot

Where 96% is genuinely unreachable for a class of code (for example, vendor-shaped boilerplate that the language idiom mandates), the answer is a written waiver against §5.4 with named scope, named compensating controls, and a defined remediation horizon. It is never a quiet drift downward.

### 5.5 Coverage Measurement Boundary

Every Stribog project must declare its coverage measurement boundary explicitly. The default boundary is:

- repository production code, including all primary and supporting modules
- excluding vendored third-party code
- excluding generated artifacts that are not hand-maintained
- excluding test code itself (tests are not measured against tests)

Any exclusion beyond that baseline must be written down and justified in the project's Charter Compliance Annex.

The measurement boundary must not be quietly shifted to make the percentage look better. A boundary change is a governance change and is itself subject to review.

**Single-file and self-contained distributables.** Where the build produces a generated artifact that is itself the user-shipped product — a single-file HTML SPA bundled by Vite or Astro, a single-binary CLI compiled from source, a single `.wasm` module, a bookmarklet, a notebook exported as a self-contained HTML — the generated artifact is *not* the coverage subject. The hand-authored source that produced it is the coverage subject. The same applies to format, lint, and static-analysis gates: they run against source, not against generated bundles. The artifact is governed instead by §7.4 release discipline (reproducibility, integrity, smoke test, size budget) and, where applicable, by the surface-specific standards that bind the artifact's runtime behavior (UI/UX for a single-file SPA, Security Posture for a security-relevant binary). The Charter Compliance Annex names the source / artifact boundary so the gates target the right surface.

### 5.6 Per-Package Blind-Spot Rule

A repository must not hide a weak critical package behind a healthy aggregate number.

If a package, module, or subsystem is materially important to the system's behavior and sits notably below the project floor, that gap must be tracked in the work system and explained in the master reference, even if the aggregate coverage number still passes. A package floor may be set in the Charter Compliance Annex (typically equal to or above the global floor) for critical paths.

### 5.7 Contract Tests for Extension Seams

Any subsystem designed for multiple implementations, plugins, providers, registries, adapters, or transports must have contract tests that enforce the shared rules of the seam. This applies especially to:

- registries
- provider abstractions
- output formats
- protocol adapters
- parser layers
- storage interfaces
- agent or model abstractions

### 5.8 Golden Tests for Stable Outputs

Golden tests must be used where output stability matters to downstream users, machines, or tooling. This commonly applies to:

- report formats
- generated configuration
- CLI output contracts
- rendered artifacts
- serialization layers
- structured log formats consumed by other tools

### 5.9 Quality Gate Set

The minimum local-and-CI gate set for every Stribog project must include:

- formatting
- linting
- static analysis appropriate to the language
- tests
- coverage measurement and floor enforcement
- secrets scanning
- vulnerability or dependency scanning
- build verification

Projects bound by surface-specific standards add the gates declared by those standards. The [[Stribog Developer Documentation Standard]] §4.4 adds the developer-reference drift gate. The [[Stribog UI/UX Standard]] §24 adds the visual-regression, automated-accessibility, offline-acceptance, real-time-conflict, streaming-a11y, cross-browser-fidelity, polish-pass, and manual-design-QA gates; §25 adds the frontend performance-budget gate including the per-class latency budgets of §25.8 and the scroll-and-frame-rate gate of §25.9; §2.3 adds the token-drift gate including the cross-layer-reach gate; §2.9.4 adds the contrast-verification gate at palette construction. The [[Stribog User Documentation Standard]] §11 adds the doc-to-release sync gate. These gates are binding under §5.9 for projects within the applicable standards' §0.2 scope.

The Charter Compliance Annex for each project names the concrete tools that implement each gate. The gates themselves are non-negotiable; the implementation choice is local.

### 5.10 Repository Command Surface

Every Stribog repository must expose an obvious local command surface for its quality gates.

The implementation may vary by language. The requirement does not. The repository must make the standard operations discoverable and repeatable through a single named entrypoint (typically a `Makefile`, `justfile`, `taskfile`, or equivalent named in the Charter Compliance Annex), exposing at minimum:

- `format`
- `lint`
- `test`
- `coverage`
- `build`
- `vulnerability` or dependency scan
- `all` (all-up verification)

"The commands exist somewhere in chat history" is not compliant. "The commands are documented in CONTRIBUTING but the entrypoint does not expose them" is not compliant. The named entrypoint is the contract.

### 5.11 Quality-Gate Configuration as Governed Artifacts

The files that define and enforce the quality posture are themselves governed artifacts. Examples include:

- linter and formatter configuration
- secret-scanning configuration and allowlists
- local hook scripts
- test runner and coverage configuration
- release-pipeline and packaging configuration

These files are versioned, reviewed, and kept aligned with the documented gate model. Quietly weakening a gate by editing its configuration is as real a governance change as weakening the code or the charter text. It requires the same review and the same waiver discipline.

### 5.12 Gate Removal or Weakening

Projects may add stronger gates without ceremony. Removing or weakening any gate listed in §5.9, including by configuration change, requires a waiver.

## 6. Documentation as a System Surface

Documentation is part of the engineering system, not a trailing artifact. The position is:

- architecture is not real until it is written down clearly enough to build against
- design changes are not complete until the governing references reflect them
- release readiness includes documentation readiness

For material work, documentation updates ship in the same branch, pull request, or change set as the implementation change wherever feasible. If documentation is deferred, that deferral is explicit, tracked in the work system, and time-bounded.

The form of Stribog documents — front matter, structure, status vocabulary, diagram discipline, maintenance triggers — is governed by the Stribog Documentation Standard. That standard is a binding companion to this charter, not optional style guidance.

## 7. Git, CI, and Release Discipline

### 7.1 History Discipline

The default delivery model is:

- trunk-based primary branch (`main` or `master`)
- short-lived feature branches
- review through pull request, or equivalent for small-team repositories where a structured self-review record is maintained
- squash merge for clean history, unless a project explicitly chooses another model

The objective is a clean, comprehensible, bisectable primary branch.

### 7.2 Remote Protection

For shared or public remotes, the expected baseline is:

- branch protection on the primary branch
- no force push to the protected branch
- required status checks
- linear history or equivalent cleanliness control
- code ownership or equivalent review-ownership declaration for non-trivial repositories
- review-thread resolution where the platform supports it
- stale-review invalidation or equivalent re-review protection where the platform supports it
- signed commits where platform support makes that practical

### 7.3 CI Mirrors Real Local Gates

CI must enforce the same meaningful gates that contributors are expected to run locally. CI is not a theatrical wrapper over a weaker reality.

If a gate is enforced in CI but contributors cannot easily run it locally, that gate is incomplete. If a gate runs locally but is not enforced in CI, that gate is non-binding.

### 7.4 Release Discipline

Meaningful versions ship with:

- versioned artifacts, reproducible builds, or both
- explicit version semantics appropriate to the project
- a changelog or release notes with meaningful structure
- documentation synchronized to the release
- an explicit release-readiness or certification check for serious milestones

For public or broadly distributed repositories, release automation is explicit and tag-driven where the toolchain supports it. Release publication is reproducible, reviewable, and does not depend on ad hoc local steps.

Where a build produces a distributable artifact, build verification includes a smoke test of the produced artifact, not only a successful compile. Public release surfaces — package managers, install scripts, container images, archives, checksums — are part of the release contract.

Install scripts, binary downloads, and similar direct distribution surfaces verify artifact integrity through checksums, signatures, or an equivalent mechanism wherever the toolchain makes it practical.

For projects whose delivery model is operational rather than versioned (managed services, rolling deployments, infrastructure code), release equivalents are governed by the Stribog Operational Delivery Standard.

**Single-file distributable artifacts.** Where the build artifact is also the user-shipped product (single-file SPA, single-binary CLI, single `.wasm` module, bookmarklet, self-contained notebook export), the release contract is:

- the build is reproducible — the same source plus the declared toolchain produces the same artifact bit-for-bit, or to a declared canonical form when the toolchain emits non-determinism (timestamps, module ordering)
- the artifact carries a verifiable integrity reference (checksum, signature, SRI hash) the consumer can verify before running
- the artifact has a declared size budget appropriate to its delivery channel and the surface-specific standard that binds it (UI/UX §25.1 frontend bundle weight for a single-file SPA; a similar budget for native binaries)
- the artifact is smoke-tested in its shipped form, not only by re-running the source — the smoke test verifies the integrity reference holds, the artifact loads, and one named end-to-end path through it succeeds
- the source / artifact boundary is named in the Charter Compliance Annex so quality gates target the source while release gates target the artifact (see §5.5)

### 7.5 Public Repository Trust Surface

For public repositories, the front door is part of the engineering surface. That includes:

- README accuracy
- badge accuracy
- release visibility
- license clarity
- installation-path accuracy
- documentation discoverability
- security-disclosure visibility
- contributor-workflow visibility

Public quality signals such as badges must correspond to real, maintained automation or real repository state. Decorative theater is non-compliant.

### 7.6 Public Repository Governance Surfaces

For public or shared repositories, the repository contract extends beyond source files and CI. The governed surface includes, where relevant:

- `CODEOWNERS` or equivalent review-ownership declaration
- a pull request template or equivalent review checklist
- issue templates that gather reproducible context
- `SECURITY.md` or equivalent private vulnerability reporting policy
- contributor workflow guidance that matches the actual branch, review, and merge model

These files describe the real process. A repository that publishes governance surfaces implying review, ownership, or disclosure flows that do not actually exist is non-compliant.

### 7.7 Git Identity and AI Attribution

For shared or public Git history, contributors do not casually expose personal email addresses when the hosting platform provides a privacy-preserving identity mechanism (such as a `noreply` address). The Charter Compliance Annex names the identity convention to be used for the project.

Repositories that accept AI-assisted changes must define how authorship and attribution are disclosed in commit or merge history. The convention is provider-neutral — the same trailer shape works across model families and across the harnesses that may run them. The default form is:

```
Co-authored-by: <agent-name> <agent-id-or-noreply-address>
```

The convention is named in the Charter Compliance Annex; humans and agents follow it consistently. The detailed agent-side rules — concrete trailer examples per agent harness (Claude, Codex, Copilot, Gemini, local / self-hosted, cross-vendor), multi-agent attribution, identity-privacy rules — are governed by the [[Stribog AI Agent Execution Standard]] §5.

## 8. Security, Privacy, and Mutating Safety

### 8.1 Secret and PII Hygiene

Repositories, fixtures, examples, tests, and documentation do not casually leak:

- credentials, tokens, or API keys
- private customer or operator data
- personal identifiers
- machine-local paths or environment-specific residue
- internal-only operational detail

Private planning material lives in the correct private context, not inside repository-shipped artifacts.

Secret prevention is layered. Stribog repositories combine:

- a deliberately structured `.gitignore`
- privacy-preserving Git identity for shared or public history
- staged secret scanning via local hooks where the risk justifies it
- pull-request checklist reminders
- CI-side secrets scanning, ideally over reachable history
- protected merge paths so unverified changes cannot land

Secret-scanning allowlists are governance artifacts, not dumping grounds. Any allowlist or suppression file is minimal, explicit, path-scoped or rule-scoped, and limited to intentional fixtures or other tightly controlled cases. Each entry is justified.

### 8.2 Distribution Runtime Hardening

If a project ships container images, packaged services, or other executable distribution surfaces, the runtime posture defaults toward least privilege wherever the platform makes that practical. Typical expectations include:

- minimal runtime images
- non-root execution
- absence of unnecessary tooling in runtime artifacts
- explicit runtime metadata where it materially improves traceability

This is not a demand for one packaging style. It is a demand that distributed runtime artifacts not be casually over-privileged.

### 8.3 `.gitignore` as a Governance Boundary

For Stribog repositories, `.gitignore` is part of the repository's governance boundary, not just clutter control. It is expected to define and protect categories such as:

- build outputs and binaries
- test, coverage, and benchmark artifacts
- local environment files
- secrets and credential-bearing files
- runtime scan output that may contain private or sensitive data
- ephemeral end-to-end runtime artifacts
- local-only issue-tracking state
- local-only AI agent instructions
- internal engineering documentation that is intentionally not part of the public repo surface
- generated analysis artifacts that are reproducible and not committed

### 8.4 Ignore Policy Structure

Stribog repositories structure `.gitignore` deliberately, with grouped sections and comments that make the repository boundary legible to humans. The point is not aesthetic neatness; it is to make obvious which classes of material are shippable, local-only, regenerable, sensitive, or internal-only.

### 8.5 Forbidden Override Pattern

If a path is intentionally ignored because it is local-only, sensitive, internal-only, or regenerable, maintainers and agents must not override that boundary casually with `git add -f` or equivalent force-tracking behavior.

Forcing a governed ignored artifact into a repository requires an explicit decision and a written justification. The default rule is: **if the boundary exists, respect it**.

### 8.6 Mutating Workflow Controls

Any tool or workflow that changes state must be designed so that a reasonable operator can answer:

- what will change
- what did change
- how the risk was bounded
- what to do if something failed

The default posture for any mutating workflow is:

- preview or dry-run first, where meaningful
- explicit opt-in for apply
- clear blast-radius controls
- post-mutation verification
- recoverability where feasible

### 8.7 Failure Honesty

Systems degrade honestly. Partial success, skipped work, unresolved errors, and bounded uncertainty are surfaced explicitly rather than hidden behind a false success state. Exit codes, error reports, and operator-facing messages reflect the actual outcome.

## 9. Performance, Reliability, and Operability

### 9.1 Measure Before Claiming

If performance materially matters, the project establishes benchmark fixtures and profiles real hot paths before claiming any optimization. Performance work must be benchmarked, profiled, verified after change, and documented if it materially changes the design.

### 9.2 Reliability Expectations

Serious systems define:

- expected failure modes
- timeout and retry posture
- concurrency assumptions where relevant
- operator-visible error behavior
- observability hooks proportionate to the system

### 9.3 Operability Baseline

Every operator-facing tool exposes:

- a `--help` or equivalent affordance
- predictable exit semantics (`0` for success, non-zero with stable, documented meanings for failure modes)
- structured logs to a stable stream (default: `stderr`; the project's Charter Compliance Annex may name a different convention)
- a `--dry-run` (or equivalent) for any mutating command, printing the intended actions before they are taken
- actionable failure messages that name the failed step, the cause, and the operator-facing remedy where one exists

These are not stylistic preferences. They are the contract between the tool and the human or system holding it.

For projects whose primary product is operational rather than a tool — managed services, infrastructure, deployments — the broader reliability and operability discipline is governed by the Stribog Operational Delivery Standard.

## 10. AI Agent Execution

AI agents are first-class contributors to Stribog projects. Their behavior is bound by a dedicated standard: the **Stribog AI Agent Execution Standard**.

That standard governs:

- which references an agent must read before broad work
- how TDD discipline is preserved when the agent generates both test and implementation
- what closeout evidence is required for AI-assisted changes
- how multi-agent or multi-session coordination is handled
- how an agent surfaces uncertainty, asks for confirmation, and signals when it should stop
- attribution and provenance disclosure for AI-assisted commits

Every Stribog project that uses AI assistance is bound by that standard, in addition to this charter. Agent compliance is verified as part of phase and release closeout.

## 11. Operational Delivery

A meaningful share of Stribog work is operational: managed services, infrastructure as code, rolling deployments, change windows, incident response. The discipline appropriate to that work — release equivalents, runbook structure, incident response, post-mortems, change management — is governed by the **Stribog Operational Delivery Standard**.

For projects whose primary deliverable is operational, that standard is binding alongside this charter and refines several clauses (notably §7.4 release discipline) for the operational context.

## 12. Definition of Done

"Done" means more than "the code exists."

### 12.1 Task-Level Done

A task is done when:

- the behavior is implemented
- the tests were written first, or a waiver is on file
- the relevant tests pass
- the documentation is updated where the change touches a governed surface
- the local gates relevant to the change are green

### 12.2 Subsystem-Level Done

A subsystem is done when:

- contracts and boundaries are explicit
- tests cover the intended behavior and the intended failure modes
- documentation explains how the subsystem fits the architecture
- integration behavior is validated
- risks and non-goals are recorded

### 12.3 Phase-Level Done

A phase is done when:

- the planned deliverables exist
- the acceptance criteria are met
- the quality gates pass
- coverage remains compliant against the §5.4 floor
- documentation is synchronized
- an audit or closeout review has been performed and recorded

### 12.4 Release-Level Done

A release is done when:

- the build is reproducible
- the version is explicit
- the changelog is updated
- the release-facing documentation matches shipped behavior
- serious blockers are either fixed or consciously deferred with written justification

For operational releases (rolling deployments, infrastructure changes, managed-service updates), the parallel checklist lives in the Stribog Operational Delivery Standard.

## 13. Exceptions and Waivers

Every exception is explicit. A valid waiver records:

- the exact clause being waived (by section number)
- the scope (what code, what subsystem, what timeframe)
- the reason
- the owner
- compensating controls
- the expiry or review date

There are no invisible waivers. There are no implicit waivers. There are no waivers that exist only in chat or oral memory.

### 13.1 Waiver Register

Each Stribog project maintains a waiver register in its repository. The register's exact location is named in the Charter Compliance Annex. A waiver that does not appear in the register does not exist.

### 13.2 Emergency Deviations

If an emergency forces a temporary deviation from this charter, the deviation is documented in the waiver register immediately after stabilization. In particular:

- missing reproduction tests are added as soon as the incident is contained
- any lowered gate or skipped verification is recorded and repaid against a defined horizon
- the system returns to the charter baseline; it does not remain permanently degraded by convenience

## 14. Companion Documents

This charter expects the following companion documents to exist and remain aligned:

- Stribog Documentation Standard
- Stribog AI Agent Execution Standard
- Stribog Operational Delivery Standard
- Stribog Security Posture Standard (binding for projects meeting its §0.2 criteria)
- Stribog Data and Privacy Standard (binding for projects meeting its §0.2 criteria)
- Stribog User Documentation Standard (binding for projects meeting its §0.2 criteria — any project shipping a human-operable surface)
- Stribog Developer Documentation Standard (binding for projects meeting its §0.2 criteria — any project exposing a developer-callable or contributor-facing surface)
- Stribog UI/UX Standard (binding for projects meeting its §0.2 criteria — any project shipping a user interface)
- Stribog Glossary
- Charter Governance
- Charter Compliance Annex (per project)

Each Stribog project additionally maintains its own master reference, build plan, ADRs, audit records, and waiver register, per §2.1.

## 15. Anti-Patterns

The following are explicitly outside the Stribog standard and are forbidden by this charter:

- architecture by improvisation
- code first, tests later
- coverage as a vanity metric rather than a confidence metric
- stale documentation after material design or implementation changes
- mutating behavior without bounded controls
- casual dependency sprawl in critical paths
- pretending uncertainty does not exist
- gate weakening via configuration change without waiver
- governance theater (governance files that imply processes the project does not enforce)
- silent waivers (rules quietly ignored without record)
- AI-assisted code that fails to disclose its provenance per the project's attribution convention
- spike code grown into production without rewrite
- coverage-boundary edits made to flatter the percentage rather than reflect reality
- "we'll document it later" deferred indefinitely

This list is not exhaustive. It is illustrative of the failure modes this charter is built to prevent.

---

## 16. Revision History

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 0.11.0 | — | 2026-05-03 | Final review-draft prior to v1.0.0 promotion. Superseded by v1.0.0. |
| 1.0.0 | 1 | 2026-05-03 | Initial governing-reference release. Defined the binding baseline for engineering discipline: 96% coverage mandate, reference-first architecture, TDD as default, quality gate set, documentation as system surface, security and mutating-safety discipline, AI agent and operational-delivery cross-references, definition of done across task/subsystem/phase/release tiers, waiver discipline, anti-patterns. |
| 1.1.0 | 2 | 2026-05-03 | MINOR bump. Added §0.5 Compliance Tiers (Foundation / Working / Reference) to graduate discipline by project risk while keeping the universal canon binding on every Stribog project. Added §0.6 What This Charter Does Not Govern to make the charter's negative space explicit (customer-owned code that Stribog only consults on; sales material; statutory and contractual obligations outside engineering; personal hobby projects). Expanded §14 Companion Documents to include the Stribog Security Posture Standard, Stribog Data and Privacy Standard, and Stribog Glossary. No clause was weakened; no previously-compliant project becomes non-compliant under v1.1.0. |
| 1.1.0 | 3 | 2026-05-03 | PATCH revision. Added cross-reference at the end of §3.5 Safety by Design pointing to the Stribog Operational Delivery Standard §3–§6 and §11 for systems whose mutations affect production state. Added this §16 Revision History section. No normative change; clarification and structural addition only. |
| 1.1.0 | 4 | 2026-05-03 | PATCH revision applied during Charter Set Audit Round 3. §0.1 fleet description refined for accuracy. §9.3 Operability Baseline named `stderr` as the default structured-log stream, with the Charter Compliance Annex permitted to name a different convention. No normative change; clarification only. |
| 1.1.0 | 5 | 2026-05-03 | Editorial revision applied during Charter Set Audit Round 3 closeout. §0.4 governance-stack D2 diagram updated to include the three nodes added by the v1.1.0 canon expansion (`security`, `privacy`, `glossary`) with edges `security -> project.supplements` (threat model · SARs), `privacy -> project.supplements` (classification · lifecycle), `glossary -> project.reference` (authoritative term meaning). Closes Round 3 finding F32 (stale governance-stack diagram). No normative change. The earlier rev 2 MINOR bump that added the three governing documents to §0.4's prose did not update the §0.4 diagram, leaving the diagram in canon drift for two revisions; this revision closes that drift. |
| 1.2.0 | 6 | 2026-05-12 | MINOR bump applied during Charter Set Audit Round 6 closeout. §14 Companion Documents extended to list the three new governing documents added under Round 6: [[Stribog User Documentation Standard]], [[Stribog Developer Documentation Standard]], and [[Stribog UI/UX Standard]], each binding per its own §0.2 applicability. §3.3 Thin Interface Layers extended with a closing paragraph naming the surface-specific binding standards for UI, developer-callable, and user-operable surfaces. §5.9 Quality Gate Set extended with a paragraph naming the surface-specific gates the three new standards add (developer-reference drift gate, visual-regression and automated-accessibility gates, frontend performance-budget gate, doc-to-release sync gate). Closes Round 6 finding F62. No clause was weakened; the three new standards bind only projects within their applicability and the gates they introduce apply only to those projects. |
| 1.2.0 | 7 | 2026-05-12 | PATCH revision applied during Charter Set Audit Round 7 closeout. §5.9 Quality Gate Set surface-specific-gates paragraph updated to reflect the [[Stribog UI/UX Standard]] v1.1.0 expansion: UI/UX gate references advanced from §9 (visual regression / automated a11y) and §10 (performance budget) to §24 (now also covering offline acceptance, real-time conflict, streaming a11y, cross-browser fidelity, polish pass, manual design QA) and §25 (now also covering per-class latency budgets and scroll-and-frame-rate); added the token-drift / cross-layer-reach gate at §2.3 and the contrast-verification gate at §2.9.4. No clause was weakened; the cited section numbers were stale, and the new gates were already binding under the UI/UX Standard's own clauses. Closes Round 7 finding F75 (Engineering Charter §5.9 cross-reference drift after UI/UX renumbering). |
| 1.2.0 | 8 | 2026-05-12 | PATCH revision applied during Charter Set Audit Round 9 closeout. Two clarifications and one attribution refresh, all additive: (a) §5.5 *Coverage Measurement Boundary* extended with a closing paragraph addressing single-file and self-contained distributables — single-file HTML SPA, single-binary CLI, single `.wasm` module, bookmarklet, self-contained notebook export — making explicit that the *source* carries coverage / format / lint / static-analysis gates while the *generated artifact* carries §7.4 reproducibility, integrity, size, and smoke-test gates. The principle (exclude generated from coverage) was already in §5.5; the clarification names the edge case where the artifact and the product are the same object. (b) §7.4 *Release Discipline* extended with a single-file-distributable release contract — reproducible build, integrity reference, declared size budget, smoke test in the shipped form, source/artifact boundary named in the Annex. (c) §7.7 *Git Identity and AI Attribution* clarified to a provider-neutral trailer shape with the detailed concrete examples per agent harness routed to the [[Stribog AI Agent Execution Standard]] §5. Closes Round 9 findings F80 (Claude-specific attribution example) and F81 (single-file distributable artifact treatment under-specified). No clause was weakened; no previously-compliant project becomes non-compliant under v1.2.0 rev 8. |

---
