---
title: "<Project Name> Master Reference"
created: 2026-05-04
updated: 2026-05-04
type: project/master-reference
status: governing-reference
tags: [borg-backup, charter, cheatsheet, claude-stack, governance, llm, runbook, stribog]
project: <project-id>
version: "1.0.0"
revision: 3
last_updated: YYYY-MM-DD
parent_moc: "[[MOC - Stribog Governance]]"
---


# <Project Name> — Master Reference

> One-sentence description of what this project is and why it exists.

---

> **Template usage.** Replace every `<placeholder>` with project-specific content. Italicized guidance paragraphs are removed from the live document. Sections may be extended; the canonical sections below must appear, even if a section's content is one line of "Not applicable to this project, because <reason>."

---

## 0. TL;DR

*A reader should know within 60 seconds whether this project concerns them. Use a concrete summary table, then 1-3 paragraphs of architectural framing. Specific numbers, not adjectives.*

| Property | Value |
|----------|-------|
| Primary problem | <what this exists to solve> |
| Architectural posture | <e.g. CLI tool, managed service, library, platform> |
| Source of truth | <what is authoritative; what is derived> |
| Implementation language | <pinned version> |
| Delivery model | <versioned releases, rolling deployment, managed service> |
| Current phase | <Phase N — short description> |
| Pinned charter version | <e.g. [[Universal-Stribog-Engineering-Charter]] 1.0.0> |

<TL;DR prose here. Three paragraphs maximum. Lead with the design position, name the contested choices, end with the current state.>

## 0.1 Current State

*The bootstrap section. What exists today, with actual numbers. Deployed components, working surfaces, established baselines, current corpus or fleet sizes, real latencies. A future reader should be able to distinguish what is real from what is planned without ambiguity.*

<Current state details.>

## 0.2 Staff-Engineer Revisions

*Deliberate design choices, especially the contested ones. "We chose X over Y because Z." Single most important rationale capture in the document. Future maintainers and AI agents read this section to understand why the system is shaped the way it is.*

- <Choice 1>: chose `<chosen option>` over `<rejected option>` because <rationale>.
- <Choice 2>: chose `<chosen option>` over `<rejected option>` because <rationale>.
- <Choice N>: ...

## 0.3 Charter Compliance

*This project's authoritative compliance posture lives in the Charter Compliance Annex. This section is a pointer, not a duplicate.*

| Property | Value |
|----------|-------|
| Charter Compliance Annex | `<path/to/Charter-Compliance-Annex.md>` |
| Pinned charter version | <e.g. Universal-Stribog-Engineering-Charter 1.1.0 (revision 3)> |
| Compliance tier | <Foundation / Working / Reference — must match the Annex> |
| Waiver register | `<path/to/WAIVERS.md>` |

For the binding list of governing documents this project pins to, the toolchain that implements the gates, and any active waivers, see the Charter Compliance Annex. This master reference must not contradict the Annex; if drift is detected, the Annex is authoritative for compliance and this document is updated.

## 1. Environment Reality

*Hardware, runtime, dependencies, scale. Concrete numbers, not adjectives. Tables comparing capacity to need, with explicit headroom statements. Cross-reference the Charter Compliance Annex for the authoritative toolchain pin; this section captures what the system runs on, not what governs the build.*

| Resource | Available | Workload need | Headroom |
|----------|-----------|---------------|----------|
| <e.g. RAM> | <amount> | <amount> | <ratio or note> |
| ... | | | |

## 2. System Architecture

*High-level system shape. D2 diagrams for non-trivial structure. Inline `d2` blocks for BrainForest-resident references; `.d2` source files under `docs/internal/diagrams/src/` for repository-resident references, with rendered SVG and PNG alongside. Each diagram is information-bearing: removing it should remove understanding, not just visual scaffolding.*

> Diagrams are written in [D2](https://d2lang.com).

```d2
direction: right

classes: {
  source:  { shape: page;     style: { fill: "#fef3c7"; stroke: "#b45309"; stroke-width: 2 } }
  process: { shape: rectangle; style: { fill: "#dbeafe"; stroke: "#1d4ed8"; stroke-width: 2 } }
  storage: { shape: cylinder;  style: { fill: "#fce7f3"; stroke: "#9f1239"; stroke-width: 2 } }
  output:  { shape: oval;      style: { fill: "#d1fae5"; stroke: "#065f46"; stroke-width: 2 } }
}

# Replace with the actual architecture for this project.
input: "Input" { class: source }
work: "Processing" { class: process }
store: "Persistence" { class: storage }
out: "Output" { class: output }

input -> work -> store -> out
```

*Color legend or structural commentary as needed. Resist diagrams that merely repeat the prose.*

## 3. <Subsystem 1>

*Architectural deep dive on the first major subsystem. Include schema fragments, code samples, and explicit invariants. Name what is authoritative and what is derived. State assumptions and non-goals for this subsystem specifically.*

### 3.1 Why this subsystem

<Design rationale for the subsystem's existence and shape.>

### 3.2 Schema or interface

```<language>
<schema or interface fragment>
```

### 3.3 Invariants and source-of-truth

<What invariants must hold. What is authoritative. What is a derived projection of what.>

## 4. <Subsystem 2>

*Repeat the §3 pattern for each major subsystem. Architecture supplements live in their own files when a subsystem's depth exceeds what this reference can cleanly hold.*

## 5. Interfaces

*External interfaces — CLI, API, MCP, UI, scheduled jobs. Per the [[Universal Stribog Engineering Charter]] §3.3, interfaces are thin layers over a shared core. Document each interface, its data contract, the binding surface-specific standard, and its relationship to the core.*

| Interface | Audience tier | Data contract | Surface-specific standard | Notes |
|-----------|---------------|---------------|---------------------------|-------|
| <e.g. CLI> | <end-user / operator> | <e.g. exit codes 0/1/2; structured logs to stderr> | [[Stribog User Documentation Standard]] for in-product help and reference | |
| <e.g. HTTP API> | <integrator> | <e.g. OpenAPI surface at /openapi.json> | [[Stribog Developer Documentation Standard]] §3.4 / §4 (drift gate, public surface map) | |
| <e.g. Web UI> | <end-user / administrator> | <e.g. routes, auth, server-rendered + SPA> | [[Stribog UI/UX Standard]] (tokens, state contract, WCAG 2.2 AA, performance budget) | |
| <e.g. MCP> | <agent / integrator> | <e.g. tool catalogue, JSON-Schema inputs> | [[Stribog Developer Documentation Standard]] §3.6 schema reference | |
| <e.g. Plugin / hook> | <extender> | <e.g. contract test fixture path> | [[Stribog Developer Documentation Standard]] §6 stability + §3.10 surface map | |
| ... | | | | |

*For each row, link the matching annex declaration in §1–§5 of the Charter Compliance Annex (toolchain, surface owners, accessibility test command, performance budget, locale set, telemetry registry).*

## 6. Phased Build Plan Summary

*The build plan is its own document under the Build-Plan template. This section summarizes the phase shape and links to the plan.*

| Phase | Goal | Status |
|-------|------|--------|
| Phase 1 | <e.g. core CLI + N checkers> | <complete / in-progress / planned> |
| Phase 2 | <e.g. expanded coverage + output formats> | |
| Phase N | ... | |

Build plan: `<path/to/Build-Plan.md>`.

## 7. Operational Concerns

*Privacy, backups, incremental updates, model or dependency upgrades, rebuild budgets, disaster-recovery posture. For projects with material operational character, cross-reference the Stribog Operational Delivery Standard.*

### 7.1 Privacy and isolation

<What sensitivity tier this system operates at. What controls protect that tier.>

### 7.2 Backup strategy

<What is backed up, where, on what cadence, and how restoration is tested.>

### 7.3 Incremental updates

<How the system stays current. Schedules, automation, manual checkpoints.>

### 7.4 Upgrade discipline

<How model, dependency, schema, or contract upgrades are handled.>

## 8. Common Pitfalls

*Failure modes that have either occurred or are highly likely. Concrete, named, actionable. "Skipping X causes Y" rather than "be careful about X." Group by class: data discipline, build sequencing, operational discipline, etc.*

### 8.1 Data discipline

1. <Pitfall>. <Why it matters. What to do instead.>
2. ...

### 8.2 Build sequencing

1. ...

### 8.3 Operational discipline

1. ...

## 9. Tooling Reference

*Languages, frameworks, libraries, services. Specific versions where they materially matter. Server endpoints. Health-check commands. The Charter Compliance Annex carries the authoritative toolchain pin; this section is the practical reference for someone actively using the system.*

### 9.1 Dependencies

```<language>
<dependency manifest fragment>
```

### 9.2 Server endpoints

| Endpoint | Purpose | Health check |
|----------|---------|--------------|
| <e.g. localhost:1234> | <e.g. LLM serving> | <e.g. curl -sf .../v1/models> |
| ... | | |

## 10. References and Further Reading

*External resources, related Stribog projects, RFCs, papers, prior art. Brief annotations explain why each link is included.*

- **<Source>** — <why it matters here>
- ...

## 11. What Not to Build (Yet)

*Explicitly deferred scope. Items considered and rejected for the current phase. This section prevents future contributors and AI agents from silently re-introducing scope that was deliberately set aside.*

- <Deferred item> — <reason for deferral; conditions under which it would become in-scope>
- ...

## Template Revision History

*This section governs the template itself, not template instances. Instance documents created from this template carry their own §Revision History per Documentation Standard §12.*

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 0.1.0 | 1 | 2026-05-03 | Initial release at `design-reference` grade. Defined the project master-reference contract (TL;DR, current state, staff-engineer revisions, environment reality, system architecture, subsystems, interfaces, phased plan summary, operational concerns, common pitfalls, tooling reference, references, what-not-to-build-yet). |
| 1.0.0 | 2 | 2026-05-03 | Promoted from `design-reference` v0.1.0 to `governing-reference` v1.0.0 during Charter Set Audit Round 4. Adopted Criterion C from R4 Backlog §2: all canon templates at v1.0.0 are `governing-reference` regardless of placeholder content; `design-reference` is reserved for templates still in active drafting. The master reference template's content has stabilized; placeholder syntax is the template's defining shape rather than a draftiness signal. Added this Template Revision History to align with the pattern established by ADR, Audit Closeout, Charter Compliance Annex, Critique Persona, Runbook, and Waiver Register templates. Closes Round 4 finding F52 (template status discipline inconsistent across canon). No normative change to the template's content. |
| 1.0.0 | 3 | 2026-05-12 | PATCH revision applied during Charter Set Audit Round 6 closeout. §5 Interfaces table extended: added a *Surface-specific standard* column linking each interface row to its binding surface-specific standard ([[Stribog User Documentation Standard]] for user-facing surfaces, [[Stribog Developer Documentation Standard]] for developer-callable surfaces, [[Stribog UI/UX Standard]] for UI surfaces). Example rows refreshed to illustrate CLI, HTTP API, Web UI, MCP, and Plugin / hook surfaces with their bound standards. Closing prose pointer added to the matching Charter Compliance Annex §2.4 / §2.5 / §2.6 declaration blocks. Closes Round 6 finding F62 sub-finding (Master Reference §5 Interfaces did not connect to the three new standards). No normative change to the template's contract. |

---
