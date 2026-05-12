---
title: "Stribog Glossary"
created: 2026-05-04
updated: 2026-05-12
type: stribog/glossary
status: governing-reference
tags: [borg-backup, charter, governance, kubevigil, rag, runbook, security, stribog]
version: "1.3.0"
revision: 5
last_updated: 2026-05-12
parent_moc: "[[MOC - Stribog Governance]]"
owners: [stribog-team]
---


# Stribog Glossary

> Authoritative definitions for terms that appear across multiple Stribog governing documents. When the charter set says "audit record" in one place and "audit closeout" in another, this is the document that disambiguates.

---

## 0. TL;DR

Several terms in the Stribog canon are similar enough to be confused but distinct enough that confusion is a real failure mode. This glossary defines each term in one place, names the canonical source clause, and makes adjacent terms explicit so a reader does not conflate them.

This glossary is binding: where another governing document is ambiguous, this glossary is authoritative for term meaning.

## 1. Process and Evidence Terms

### Audit Record / Audit Closeout

**Definition.** A document that captures the verdict, criteria, findings, remediations, deferred items, and residual risks of an audit performed against a project, phase, release, or the charter set itself.

**Canonical source.** Engineering Charter §2.1 (required artifact); `templates/Audit-Closeout-Template.md` (canonical structure); Charter Governance §8 (audit cadence for charter audits).

**Distinct from.** Closeout evidence (which is per-task) and change record (which is per-operational-change).

**Example.** `Charter-Set-Audit-Round-2.md`. KubeVigil's `GO-LIVE-CERTIFICATION.md`.

### Closeout Evidence

**Definition.** The explicit, machine-readable artifacts an AI agent (or human contributor) provides at task completion to demonstrate that TDD, gates, and documentation discipline were honored. Includes failing-test observation, passing-test observation, gate run results, documentation diff, and any waivers invoked.

**Canonical source.** AI Agent Execution Standard §4.

**Distinct from.** An audit record (which assesses a larger unit of work) and a change record (which is for operational changes).

**Lives in.** Commit message bodies, pull-request descriptions, beads issues, or the location named in the project's Charter Compliance Annex.

### Change Record

**Definition.** A pre-apply document that captures the rationale, target, blast radius, rollback plan, verification plan, and operator(s) for an operational change before it is applied.

**Canonical source.** Operational Delivery Standard §2.1.

**Distinct from.** Closeout evidence (post-task; software work) and audit records (assessment-grade artifacts). A change record is an *intent* artifact filed before action; closeout evidence is a *result* artifact filed after action.

**Lives in.** A durable issue or change-management system named in the Compliance Annex.

### Charter Compliance Annex

**Definition.** The per-project document that pins which versions of the governing documents the project is bound by, and names the concrete tooling that implements each charter gate. It is the project's authoritative declaration of what governs it.

**Canonical source.** Charter Governance §5; `templates/Charter-Compliance-Annex-Template.md`.

**Distinct from.** A waiver register (which records exceptions to the charter) and a master reference (which describes the project's architecture). The Annex points to both.

### Master Reference

**Definition.** The architecture-bearing document that defines a project's problem, source of truth, boundaries, phases, and deliberate design choices. The single document a strong engineer reads to understand the system.

**Canonical source.** Engineering Charter §2.1; `templates/Master-Reference-Template.md`.

**Distinct from.** Architecture supplements (which deepen specific subsystems) and build plans (which sequence the implementation).

**Reference example.** [[Email RAG System Reference]] (`~/Documents/BrainForest/30 - HomeLab/Email RAG System Reference.md`) is the canonical Stribog house-style example for this document family.

### Architecture Decision Record (ADR)

**Definition.** A short, immutable-once-accepted document that captures a single architectural decision, the context that forced it, the alternatives considered, and the consequences accepted. Numbered sequentially per project (`ADR-0001-…`).

**Canonical source.** Engineering Charter §2.4; `templates/ADR-Template.md`.

**Distinct from.** A master reference (which is the *system* description) and a build plan (which is the *implementation* sequence). An ADR is a *decision* artifact.

### Build Plan

**Definition.** The phased implementation plan for a project. Converts the master reference's architecture into milestones, dependencies, acceptance criteria, and quality gates.

**Canonical source.** Engineering Charter §2.1; `templates/Build-Plan-Template.md`.

### Runbook

**Definition.** A binding operational procedure for a recurring, risky, time-sensitive, or knowledge-bearing operation. Captures trigger conditions, prerequisites, safety notes, steps, verification, rollback, post-conditions, and escalation paths.

**Canonical source.** Operational Delivery Standard §7; `templates/Runbook-Template.md`.

### Drill (Runbook Drill)

**Definition.** A test execution of a runbook against a non-production target, performed before the runbook is needed. The first drill must succeed before a runbook advances from `design-reference` to `governing-reference`.

**Canonical source.** Operational Delivery Standard §7.3, §13.3 (DR drills); Runbook template §9 (drill log).

**Distinct from.** A live execution (which has real customer or production impact). A drill executes the same procedure against a sacrificial target.

### Waiver

**Definition.** A written, scoped, owned, dated record that a specific clause of a governing document does not apply (or applies in a modified form) to a specific scope. Every waiver records: clause, scope, reason, owner, compensating controls, expiry.

**Canonical source.** Engineering Charter §13; Charter Governance §6.3.

**Distinct from.** A *deferred finding* in an audit record (which tracks an unmet criterion to closure) and a *change in the charter itself* (which goes through the change cycle in Charter Governance §7). A waiver does not modify the charter; it records a known, time-bound exception.

### Waiver Register

**Definition.** The durable, repository-resident document where all active waivers for a project are recorded. Named in the project's Charter Compliance Annex.

**Canonical source.** Engineering Charter §13.1; Charter Compliance Annex Template §7.

## 2. Versioning and Status Terms

### Version (Document)

**Definition.** A SemVer (`MAJOR.MINOR.PATCH`) string in a document's front matter that records the semantics of normative content changes. PATCH = editorial; MINOR = additive; MAJOR = breaking.

**Canonical source.** Documentation Standard §11; Charter Governance §4.

**Distinct from.** `revision` (a monotonic write-counter) and `status` (a lifecycle state).

### Revision (Document)

**Definition.** A monotonic integer in a document's front matter that increments on every saved substantive change. Used by waivers, audits, and compliance declarations to identify exactly which document state was in force at the time.

**Canonical source.** Documentation Standard §11.3.

**Distinct from.** `version` (which changes only on normative shifts) and `last_updated` (which is the calendar date).

### Status (Document)

**Definition.** A fixed-vocabulary lifecycle state in a document's front matter. The seven canonical values are: `draft-scaffold`, `review-draft`, `design-reference`, `governing-reference`, `frozen-reference`, `superseded`, `archived`. Some document families (notably ADRs) use a sub-vocabulary defined in their template.

**Canonical source.** Documentation Standard §10.1.

### Pin (Charter Pin)

**Definition.** A declaration in a project's Charter Compliance Annex that the project is bound by a specific `MAJOR.MINOR` version of a governing document. Projects do not float against `latest`; they pin.

**Canonical source.** Charter Governance §4.4; Charter Compliance Annex Template §0.

## 3. Engineering Discipline Terms

### Spike

**Definition.** An exploratory branch of code or research used to learn an unfamiliar problem domain before committing to architecture. Spikes are allowed and encouraged; spikes that survive merge are forbidden.

**Canonical source.** Engineering Charter §3.1, §4.2.

**Compliant pattern.** `spike → discard → write reference → implement test-first`.

**Non-compliant pattern.** `spike → grow into production → write reference last (or never)`.

### Reference-First / Contract-First

**Definition.** The Stribog architectural posture that requires the master reference and subsystem contracts to exist before broad implementation begins. Implementation is downstream of reference.

**Canonical source.** Engineering Charter §3.1.

### Source of Truth

**Definition.** The authoritative artifact for a piece of state. All other representations of that state are derived projections. Every Stribog project must declare its sources of truth explicitly.

**Canonical source.** Engineering Charter §2.2.

### Coverage Floor

**Definition.** The minimum acceptable percentage of total line coverage for a Stribog project. The universal floor is **96%**. A project whose coverage falls below the floor is out of compliance and must rise, file a waiver, or be archived.

**Canonical source.** Engineering Charter §5.4.

**Boundary.** The coverage measurement boundary (what is counted) is declared in the Compliance Annex per §5.5.

### Quality Gate

**Definition.** An automated check that must pass before code can advance through the development pipeline. The minimum Stribog gate set is named in Engineering Charter §5.9 (format, lint, static, test, coverage, secrets, vulnerability, build).

**Canonical source.** Engineering Charter §5.9–§5.12.

## 4. Operational Terms

### Service Tier

**Definition.** A declared classification of a service that determines its operational discipline (monitoring baseline, RPO/RTO targets, backup cadence, alert routing). Default vocabulary: Critical, Standard, Background.

**Canonical source.** Operational Delivery Standard §10.1, §13.2.

### RPO / RTO

**Definition.**
- **Recovery Point Objective (RPO):** the maximum acceptable data loss measured in time
- **Recovery Time Objective (RTO):** the maximum acceptable downtime during recovery

Both are declared per service tier and recorded in the Compliance Annex.

**Canonical source.** Operational Delivery Standard §13.2.

### Severity (Incident)

**Definition.** A classification of an incident's customer or operational impact. Default Stribog vocabulary:
- **Sev-1:** customer-impacting outage or material security incident
- **Sev-2:** significant degradation, partial outage, near-miss with customer visibility
- **Sev-3:** internal degradation or asymptomatic anomaly
- **Sev-4:** maintenance-grade event

**Canonical source.** Operational Delivery Standard §11.1.

### Stabilization vs Resolution

**Definition.** Two distinct phases of incident response:
- **Stabilization:** customer-visible impact ends
- **Resolution:** [[ROOT CAUSE]] is addressed

An incident is not closed until both are complete or the resolution is tracked as a follow-up commitment.

**Canonical source.** Operational Delivery Standard §11.5.

### Configuration Drift

**Definition.** Divergence between a system's running configuration and its declared source of truth. Drift is detected (not assumed absent) on a defined cadence and is either reconciled, promoted to source of truth, or recorded in the waiver register.

**Canonical source.** Operational Delivery Standard §8.2.

## 5. AI Agent Terms

### Agent

**Definition.** An AI system performing engineering work on a Stribog project, including but not limited to: Claude Code, Codex CLI, OpenCode, Goose, custom harnesses. Bound by the AI Agent Execution Standard regardless of harness or model.

**Canonical source.** AI Agent Execution Standard §0.2.

### Confabulation

**Definition.** An agent's production of plausible-sounding but unverified or invented claims — file paths that don't exist, command output that wasn't observed, file contents that weren't read, attributions that didn't happen. Identified as the dominant agent failure mode and forbidden under §11.

**Canonical source.** AI Agent Execution Standard §1 (core position 4); §11 (forbidden behaviors).

### Required Reading

**Definition.** The reading sequence an agent must complete before broad work on a project: pinned charter version, companion governing standards, project's Charter Compliance Annex, master reference, architecture supplements, testing strategy, local agent rules, waiver register.

**Canonical source.** AI Agent Execution Standard §2.

### Self-Audit (Agent)

**Definition.** A mandatory pre-completion review by the agent against a fixed checklist (architectural alignment, TDD evidence, coverage impact, test quality, documentation drift, safety regressions, attribution, waivers, confabulation). Output appears in closeout evidence.

**Canonical source.** AI Agent Execution Standard §10.

### Critique Persona

**Definition.** A structured prompt-and-task pattern that turns an agent into a critic of its own (or another agent's) output. Common Stribog personas: Devil's Advocate, Editor, Pre-Mortem, The Critic. Used for high-stakes work that benefits from a separate-pass review.

**Canonical source.** `templates/Critique-Persona-Template.md`; AI Agent Execution Standard §10 (high-stakes critique requirement).

### Model Tier

**Definition.** A classification of model capability used to match models to task complexity. Stribog default tiers: Synthesis, Coding, Extraction, Critique. Project-specific defaults named in the Compliance Annex §4.

**Canonical source.** AI Agent Execution Standard §7.

## 6. User-Facing Surface Terms

Terms used across the User Documentation Standard, Developer Documentation Standard, and UI/UX Standard. These terms govern the surfaces a non-implementer encounters.

### Diátaxis Quadrant

**Definition.** One of the four orthogonal content modes — *tutorial*, *how-to guide*, *reference*, *explanation* — that together form a complete user-documentation surface. The quadrants are defined by two axes: the reader is *acquiring* versus *applying* skill, and the content is *practical* versus *theoretical*. A document occupies exactly one quadrant; mixed-quadrant pages are non-compliant.

**Canonical source.** Stribog User Documentation Standard §3.

### Audience Tier

**Definition.** A declared category of reader for whom a user-facing or developer-facing document is primarily written. The user-doc audience tiers are *end-user*, *operator*, *administrator*, *integrator*, *evaluator*. The developer-doc audience tiers are *contributor*, *consumer*, *embedder*, *extender*, *operator-developer*. A document declares its tier(s) in front matter and in its opening paragraph.

**Canonical source.** Stribog User Documentation Standard §2; Stribog Developer Documentation Standard §2.

### User-Facing Release Note

**Definition.** A release note written for the audience that uses the software, in plain language, naming the user-visible changes by audience tier, any required action, any deprecation status, and links to the matching documentation pages. Distinct from a producer-side changelog; a changelog does not satisfy the user-facing release-note requirement.

**Canonical source.** Stribog User Documentation Standard §4.6.

### In-Product Help

**Definition.** Documentation that travels inside the running product — tooltip text, empty-state copy, error messages, inline hints, contextual help drawers, onboarding microcopy. Governed by the same tone, evidence, and review discipline as standalone documentation, reviewable as a body of text in bulk.

**Canonical source.** Stribog User Documentation Standard §7; Stribog UI/UX Standard §6.

### Microcopy

**Definition.** The visible text on user-interface controls, labels, hints, errors, empty states, confirmations, and onboarding strings. Governed by the project's *voice charter*. Distinct from prose documentation: microcopy is bound by space and context.

**Canonical source.** Stribog UI/UX Standard §6; Stribog User Documentation Standard §7.

### Voice Charter

**Definition.** A written, per-project declaration of UI voice — register (formal, neutral, casual), person and tense, preferred constructions, forbidden constructions, locale-specific notes. UI microcopy is reviewed against the voice charter; violations are non-compliant.

**Canonical source.** Stribog UI/UX Standard §6.1.

### Support Escalation Map

**Definition.** The published, dated document that names the path a user follows when self-service documentation does not resolve their problem — channels, expected response posture, the boundary between self-service and assisted support. An undefined or stale escalation map is non-compliant.

**Canonical source.** Stribog User Documentation Standard §4.7.

### Doc-to-Release Sync

**Definition.** The discipline that a documentation update for a behavior change lands on or before the release that ships the behavior. Enforced by the release-blocking doc gate of the User Documentation Standard.

**Canonical source.** Stribog User Documentation Standard §11.

### Public Surface

**Definition.** The set of symbols, endpoints, schemas, flags, environment variables, and behaviors a Stribog project promises to keep stable within its declared compatibility window. The public surface is enumerated in the *public surface map*; an element absent from the map is, by default, internal and not protected by the stability contract.

**Canonical source.** Stribog Developer Documentation Standard §0.3, §3.10, §6.

### Generated Reference

**Definition.** Developer reference content produced mechanically from project source — OpenAPI, gRPC reflection, GraphQL SDL, godoc, rustdoc, typedoc, sphinx autodoc, or equivalent — by a tool whose output is the canonical artifact. Hand-typed developer reference is non-compliant where generation is feasible.

**Canonical source.** Stribog Developer Documentation Standard §4.

### Drift Gate

**Definition.** A quality gate that fails the build when the generated reference disagrees with the project source, when a public surface symbol is undocumented, or when a documented symbol no longer exists. Binding under the Engineering Charter §5.9 quality gate set for projects within the Developer Documentation Standard's applicability.

**Canonical source.** Stribog Developer Documentation Standard §4.4.

### Code Sample

**Definition.** A snippet of code, embedded in or referenced from developer documentation, that demonstrates a real call against the public surface. Code samples are first-class testable artifacts — versioned, owned, and run against the real surface (or a contract test fixture) on every release.

**Canonical source.** Stribog Developer Documentation Standard §5.

### Deprecation Notice

**Definition.** A dated, owned, written record that a public surface element will be removed at or after a stated future date, with a stated migration path. Carries: deprecated element by fully-qualified name, announcement date, intended removal date, migration path, owner, release in which announced, and runtime signal information.

**Canonical source.** Stribog Developer Documentation Standard §6.2.

### Compatibility Window

**Definition.** The period during which the public surface honors its stability contract for a given stability posture. Declared per project in the Charter Compliance Annex. Distinct from the support window for end-users — a surface element may be stable but unsupported, or supported but not yet stable.

**Canonical source.** Stribog Developer Documentation Standard §0.3, §6.3.

### Design Token

**Definition.** A named, machine-readable value representing a single visual primitive — a color, a typographic step, a spacing unit, a radius, an elevation, a duration, a breakpoint, a z-index, an opacity, a border style. Tokens are the source of truth; component code consumes tokens by name and does not hard-code visual values.

**Canonical source.** Stribog UI/UX Standard §2.1.

### Component State Contract

**Definition.** The declared set of visual and behavioral states every interactive component supports — `default`, `hover`, `focus`, `focus-visible`, `active`, `disabled`, `read-only`, `loading`, `empty`, `partial`, `error`, `success`, and where applicable `selected`/`checked` and `expanded`/`collapsed`. Every state is visually and programmatically distinguishable.

**Canonical source.** Stribog UI/UX Standard §3.

### WCAG 2.2 AA

**Definition.** The World Wide Web Consortium's Web Content Accessibility Guidelines, version 2.2, conformance level AA. The minimum accessibility floor for every UI surface bound by the UI/UX Standard. Surfaces in regulated or accessibility-critical contexts declare a higher floor in the Charter Compliance Annex.

**Canonical source.** Stribog UI/UX Standard §4.1.

### ARIA

**Definition.** Accessible Rich Internet Applications — the W3C specification of roles, states, and properties that bridge gaps between native semantics and assistive technology. Used to augment, not replace, native semantic elements. ARIA misuse — incorrect roles, conflicting roles, redundant roles — is forbidden.

**Canonical source.** Stribog UI/UX Standard §4.4.

### Focus Trap

**Definition.** A deliberate restriction of keyboard focus to a bounded region of the UI — typically a modal dialog — with a documented escape that restores focus to the originating control. Focus traps are scoped, intentional, and reversible; an unintentional focus trap is a defect.

**Canonical source.** Stribog UI/UX Standard §4.2, §4.3.

### Reduced-Motion Preference

**Definition.** The user setting (`prefers-reduced-motion` in CSS, the equivalent platform setting elsewhere) that the UI honors by replacing non-essential animation with non-animated equivalents. A surface that ignores the preference is non-compliant.

**Canonical source.** Stribog UI/UX Standard §4.6, §12.4.

### Performance Budget

**Definition.** A numeric ceiling on a measurable frontend signal — Largest Contentful Paint, Cumulative Layout Shift, Interaction to Next Paint, Time to First Byte, bundle weight, asset weight — that a release must not exceed. A release that exceeds any declared budget is held. For non-web surfaces, analogous budgets (cold-start latency, first-frame time, binary size) apply.

**Canonical source.** Stribog UI/UX Standard §10.

### Consent-First Telemetry

**Definition.** The discipline that no UI telemetry leaves the user's runtime until the user has affirmatively consented under the disclosures of the Data and Privacy Standard. Pre-consent telemetry, including via third-party scripts, is non-compliant.

**Canonical source.** Stribog UI/UX Standard §11.1.

### Design Review Gate

**Definition.** A release-blocking review at which a design change of declared significance — new screen, new flow, new or changed token, new or changed component, high-traffic microcopy, public marketing surface — is signed off by the named design owner. Sign-off is recorded.

**Canonical source.** Stribog UI/UX Standard §8.

### Information Architecture (IA)

**Definition.** The organization of a product's surfaces into a navigable structure of routes, groupings, labels, and hierarchy that maps to the user's mental model. The IA is a designed surface, not an emergent property.

**Canonical source.** Stribog UI/UX Standard §8.

### Deep-Link

**Definition.** A URL or platform-equivalent addressable identifier that resolves a user directly to a specific surface state — including filters, selection, and expanded disclosures — without requiring navigation from a root surface.

**Canonical source.** Stribog UI/UX Standard §8.4.

### Scroll Restoration

**Definition.** The discipline of preserving a surface's scroll position across navigation, returning the user to where they were rather than to the top, when the navigation pattern is *resume* rather than *reset*.

**Canonical source.** Stribog UI/UX Standard §8.5.

### Validation Timing

**Definition.** The declared moment at which form-field validation runs — *on submit*, *on blur*, or *live* — chosen per field based on the cognitive cost and stakes of premature feedback.

**Canonical source.** Stribog UI/UX Standard §9.2.

### Dirty State

**Definition.** A form-field or form-aggregate state indicating that the current value differs from the last-saved value. Distinct from *invalid*. The dirty / clean distinction drives unsaved-changes protection and autosave.

**Canonical source.** Stribog UI/UX Standard §9.7.

### IME Composition

**Definition.** The intermediate state of input from an Input Method Editor — used in CJK and other complex-script entry — during which a sequence of keystrokes is being composed into a final character. Validation and submission wait for composition to commit.

**Canonical source.** Stribog UI/UX Standard §9.6.

### Live Region

**Definition.** A region of the UI that programmatically announces dynamic updates to assistive technology via the platform's live-region facility (`aria-live`, `UIAccessibilityAnnouncementNotification`, equivalent). Scoped to the announcements it must carry; over-scoped live regions pollute screen-reader output.

**Canonical source.** Stribog UI/UX Standard §4.4, §10.5.

### Idle Timeout

**Definition.** The session policy under which a user with no recent interaction is signed out after a declared duration. Stribog idle-timeout discipline requires a warning before the timeout, an extend affordance, and recovery of pending work after re-authentication.

**Canonical source.** Stribog UI/UX Standard §11.3.

### Optimistic UI

**Definition.** The discipline of rendering the assumed outcome of a user action immediately and reconciling against the real outcome when the server responds, including a declared rollback path on failure.

**Canonical source.** Stribog UI/UX Standard §16.2.

### Skeleton

**Definition.** A placeholder rendering that preserves the future layout of a surface while real content loads. Distinct from a spinner; chosen above a declared latency threshold per project.

**Canonical source.** Stribog UI/UX Standard §16.1.

### Stale-While-Revalidate

**Definition.** A caching and rendering discipline that renders the last known value immediately and replaces it once a fresh value arrives, with a visible indicator (the `stale` state) while the revalidation is in flight.

**Canonical source.** Stribog UI/UX Standard §16.3.

### Write Queue

**Definition.** An offline-aware, locally persisted buffer of pending user mutations, applied to the server once connectivity returns. Each queued mutation carries an idempotency key; replay handles conflict resolution per §14.4.

**Canonical source.** Stribog UI/UX Standard §17.3.

### Conflict Resolution

**Definition.** The UI contract that presents two conflicting versions of a record — typically the user's local version and an authoritative server version — and asks the user to choose, merge, or override. Silent last-write-wins is non-compliant for surfaces declared collaborative.

**Canonical source.** Stribog UI/UX Standard §14.4.

### Presence Indicator

**Definition.** A UI signal that another user is currently viewing or editing a shared surface. Scoped to the shared surface; presence telemetry follows consent.

**Canonical source.** Stribog UI/UX Standard §14.3.

### Streaming UI

**Definition.** A UI surface whose content arrives incrementally — token-by-token model output, server-sent events, websocket chunks — and is rendered as it arrives. Live-region announcements are scoped per §15.2 to avoid per-chunk chatter.

**Canonical source.** Stribog UI/UX Standard §15.2.

### Generative UI

**Definition.** A UI surface whose structure, not only content, is generated at runtime by a model or a server-side template engine. Generative surfaces bind to the UI/UX Standard despite their generation.

**Canonical source.** Stribog UI/UX Standard §15.

### Modality

**Definition.** The property of a surface that captures or restricts user attention. Stribog modality taxonomy: dialog, sheet, popover, drawer, sidebar, inline disclosure, full-page takeover. Distinct from disclosure (expand / collapse).

**Canonical source.** Stribog UI/UX Standard §13.

### Drop Target

**Definition.** A region declared eligible to receive a drag operation, with declared accept criteria and a visible state contract (`drop-eligible` / `drop-forbidden`). Every drag-and-drop surface has a keyboard-only alternative.

**Canonical source.** Stribog UI/UX Standard §13.7, §13.8.

### Forced-Colors Mode

**Definition.** The OS-level high-contrast mode under which the user agent overrides author colors with a system palette (`forced-colors: active`, Windows High Contrast, equivalent). UI must remain usable; tested on every release.

**Canonical source.** Stribog UI/UX Standard §4.10.

### Token Layer (Primitive / Semantic / Component)

**Definition.** The layered organization of the design-token registry. *Primitive* tokens hold raw values; *semantic* tokens hold intent and theme-switch through semantic aliases; *component* tokens hold per-component bindings. Component code consumes the highest applicable layer.

**Canonical source.** Stribog UI/UX Standard §2.2.

### Perceptual Color Space

**Definition.** A color space — OKLCH, OKLab, LCH — in which equal numeric steps in lightness correspond to equal visual steps. Stribog color palettes are constructed in a perceptual color space; sRGB-only construction produces visually uneven ramps and is non-compliant.

**Canonical source.** Stribog UI/UX Standard §2.9.1.

### Baseline Grid

**Definition.** The vertical rhythm to which type and inter-block spacing align. Stribog spacing scales are constructed as multiples of a baseline; off-baseline drift is a polish defect.

**Canonical source.** Stribog UI/UX Standard §2.10.2.

### Easing Curve

**Definition.** The mathematical curve a motion duration is shaped by — entrance / exit / in-out / spring / step. Stribog motion uses declared easing curves from a project-owned catalogue, not the platform default.

**Canonical source.** Stribog UI/UX Standard §27.7.

### Micro-Interaction

**Definition.** A small motion and feedback detail — button hover lift, toggle transition, checkbox check-mark draw-on, focus-ring fade-in, copy-to-clipboard confirmation flash — that distinguishes a finished UI from a working one. Every micro-interaction is implemented through the motion token set and honors the reduced-motion preference.

**Canonical source.** Stribog UI/UX Standard §27.8.

### Haptic Feedback

**Definition.** Tactile vibration cues delivered on platforms that support them, used surgically on declared trigger events and consistent across the surface. Governed by the user's system-level haptics preference.

**Canonical source.** Stribog UI/UX Standard §27.9.

### Frame Budget

**Definition.** The per-frame time allowance for the surface to remain at the display's refresh rate — 16ms at 60Hz, 8ms at 120Hz. Pointer-move, scroll, drag, and animation work that exceeds the frame budget produces jank and is a §29.20 defect.

**Canonical source.** Stribog UI/UX Standard §25.8, §25.9.

### Hover-Intent

**Definition.** The discipline of delaying a hover-triggered surface (tooltip, dropdown, popover) by a declared interval so that incidental cursor motion does not fire the surface. The delay is part of the motion token set.

**Canonical source.** Stribog UI/UX Standard §27.8.1.

### SSR / Hydration Posture

**Definition.** A web project's declared rendering posture — SPA, SSR, SSG, hybrid, streaming — chosen with reasoning against §25.1 LCP and the §25.6 hydration budget. JS-disabled fallback is declared per project.

**Canonical source.** Stribog UI/UX Standard §25.6.

### Theme Parity

**Definition.** The requirement that every product surface renders correctly in every shipped theme. Visual regression captures every component in every theme; per-theme defects are non-compliant.

**Canonical source.** Stribog UI/UX Standard §2.11.4.

### Polish Pass

**Definition.** A human-performed review against the §2.12 polish checklist — alignment, type rendering, shadow consistency, edge treatment, icon-text optical alignment, illustration consistency, edge-state styling — required before sign-off at the design review gate.

**Canonical source.** Stribog UI/UX Standard §2.12.10, §24.8.

## 7. Governance Terms

### Charter Owner

**Definition.** The role responsible for the integrity of the charter set. Approves ratified changes, emergency changes, and audit-round closure. Named in the `owners` field of every governing document.

**Canonical source.** Charter Governance §10.1.

### Charter Reviewer

**Definition.** A role — human or AI — that applies audit and review judgment to charter changes. Reviewers do not approve; they advise. Final approval is retained by the Charter Owner.

**Canonical source.** Charter Governance §10.2.

### Project Compliance Owner

**Definition.** The per-project role responsible for maintaining the Charter Compliance Annex, the waiver register, and attesting to compliance at phase and release boundaries.

**Canonical source.** Charter Governance §10.3.

### Distinct Hats

**Definition.** The discipline that requires small-team Stribog roles (Charter Owner, Project Compliance Owner, Editor) to be treated as distinct even when the same team member plays them. Prevents charter capture: the Owner does not approve the Editor's draft without a separate review pass.

**Canonical source.** Charter Governance §11.1.

### Compliance Tier

**Definition.** The classification of a Stribog project that determines the form in which the charter applies. Three tiers: **Foundation** (universal — every Stribog project), **Working** (small tools, internal automations, exploratory utilities not yet customer-facing or production-stateful — Foundation with two relaxations: condensed master reference and optional phased build plan), **Reference** (customer-facing, production-stateful, public, or security-sensitive — Foundation in full plus mandatory §2.1 artifact set, applicable security/privacy standards, and audit closeouts at every phase boundary).

**Canonical source.** Engineering Charter §0.5.

**Distinct from.** *Service Tier* (operational classification, governs monitoring/RPO/RTO; defined in Operational Delivery Standard §10.1) and *Model Tier* (AI capability classification; defined in AI Agent Execution Standard §7). The three tier vocabularies are independent: a project at Compliance Tier `Reference` may run a service at Service Tier `Standard` and call a model at Model Tier `Synthesis`. The terms share the word *tier*; they share nothing else.

**Distinct from.** A *reference document* (a document family — master references, architecture supplements — defined in Documentation Standard §2.2). The Compliance Tier name `Reference` and the document family `reference` are different concepts that happen to share an English word; do not conflate.

## 8. Reading This Glossary

When two terms in different documents appear to mean the same thing, consult this glossary. The term defined here is authoritative.

When a term used in a Stribog document is not defined here, raise it as a finding in the next charter audit-round. New cross-cutting terms are added to this glossary; project-local terms remain in their project's master reference.

---

## 9. Revision History

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 1.0.0 | 1 | 2026-05-03 | Initial governing-reference release. Defined cross-document terms across Process and Evidence, Versioning and Status, Engineering Discipline, Operational, AI Agent, and Governance categories. |
| 1.1.0 | 2 | 2026-05-03 | MINOR bump applied during Charter Set Audit Round 3. Added **Compliance Tier** term to §6 Governance Terms, with explicit disambiguation against *Service Tier* (operational), *Model Tier* (AI), and the *reference document* family. Closes a terminology gap identified in Round 3 self-critique: the canon used "Reference" for both a Compliance Tier and a document family, and the Glossary previously did not authoritatively distinguish them. Added this §8 Revision History section. |
| 1.2.0 | 3 | 2026-05-12 | MINOR bump applied during Charter Set Audit Round 6 closeout. New §6 *User-Facing Surface Terms* inserted between §5 AI Agent Terms and the prior §6 Governance Terms (now renumbered §7), with the Reading section renumbered §8 and Revision History renumbered §9. The new §6 group adds twenty-three cross-document terms required by the three new standards: Diátaxis Quadrant, Audience Tier, User-Facing Release Note, In-Product Help, Microcopy, Voice Charter, Support Escalation Map, Doc-to-Release Sync, Public Surface, Generated Reference, Drift Gate, Code Sample, Deprecation Notice, Compatibility Window, Design Token, Component State Contract, WCAG 2.2 AA, ARIA, Focus Trap, Reduced-Motion Preference, Performance Budget, Consent-First Telemetry, Design Review Gate. Each term names the canonical source standard. Closes Round 6 finding F62 follow-up: the three new standards introduced cross-document vocabulary that needed an authoritative single-source definition before they could bind. No prior term meaning changed; this is purely additive. |
| 1.3.0 | 4 | 2026-05-12 | MINOR bump applied during Charter Set Audit Round 7 closeout. §6 *User-Facing Surface Terms* extended with thirty additional cross-document terms required by the [[Stribog UI/UX Standard]] v1.1.0 expansion: Information Architecture, Deep-Link, Scroll Restoration, Validation Timing, Dirty State, IME Composition, Live Region, Idle Timeout, Optimistic UI, Skeleton, Stale-While-Revalidate, Write Queue, Conflict Resolution, Presence Indicator, Streaming UI, Generative UI, Modality, Drop Target, Forced-Colors Mode, Token Layer (Primitive / Semantic / Component), Perceptual Color Space, Baseline Grid, Easing Curve, Micro-Interaction, Haptic Feedback, Frame Budget, Hover-Intent, SSR / Hydration Posture, Theme Parity, Polish Pass. Closes Round 7 finding F73 (vocabulary drift behind UI/UX v1.1.0 expansion). No prior term meaning changed; this is additive. The §6 group now holds fifty-three cross-document terms covering the user-facing-surface canon. |

---
