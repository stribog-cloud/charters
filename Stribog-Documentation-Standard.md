---
title: "Stribog Documentation Standard"
created: 2026-05-04
updated: 2026-05-12
type: stribog/documentation-standard
status: governing-reference
tags: [anthropic, charter, governance, rag, runbook, stribog]
version: "2.1.0"
revision: 9
last_updated: 2026-05-12
parent_moc: "[[MOC - Stribog Governance]]"
owners: [stribog-team]
---


# Stribog Documentation Standard

> The binding documentation standard for Stribog. This is a mandate. It defines how Stribog documents are structured, written, versioned, diagrammed, and maintained — in any language, on any project, by any author.

---

## 0. TL;DR

| Area | Mandate |
|------|---------|
| Front matter | Canonical YAML front matter is required for all governing, reference, plan, audit, and runbook documents. |
| Structure | Documents use deliberate numbered sections beginning with `0. TL;DR`. |
| Tone | Calm, precise, authoritative, technical, non-performative. |
| Depth | Reference-grade documents capture rationale, boundaries, assumptions, risks, and implementation consequences — not just decisions. |
| Diagrams | D2 is the default diagram language. Source artifacts are version-controlled. |
| Status | Documents carry an explicit, machine-readable status from a fixed vocabulary. |
| Versioning | Documents carry a SemVer `version` and a monotonic `revision` integer. The two move independently. |
| Maintenance | A document that drifts materially from implementation is out of compliance. It must be either updated or marked superseded. |
| Templates | Each document family has a canonical template under `templates/`. New documents start from a template. |

This standard is binding on every Stribog document of governing, reference, planning, audit, or runbook grade. It is binding regardless of authorship — human or AI.

## 0.1 Why This Standard Exists

Weak documentation produces two failures.

The first is technical: architecture becomes ambiguous, decisions drift, maintainers begin implementing their own interpretation of the system.

The second is social: a document looks polished enough to discourage questions, but is not precise enough to deserve trust. That second failure is more dangerous than the first because it is invisible. People build on a foundation they believe is firm.

This standard exists to prevent both, and to make the second failure mode harder to produce.

## 0.2 Relationship to the Engineering Charter

The Universal Stribog Engineering Charter defines what a Stribog project must do.

This standard defines how Stribog reference-grade documents express that work.

Where the charter says "documentation is part of the system," this standard makes that operational.

## 1. Design Position

### 1.1 Documentation Is Architecture

For Stribog, high-discipline documentation is not commentary about the system. It is part of the system's control plane.

A reference-grade document must do more than describe what exists. It must:

- establish boundaries
- capture deliberate choices
- identify source-of-truth layers
- expose non-goals
- surface open risks
- translate decisions into implementation consequences

A document that records decisions without rationale, or describes shape without surfacing tradeoffs, is not yet a reference. It is a sketch.

### 1.2 The Reference-Grade Standard

The expected style for serious internal reference work is concrete, grounded, and sufficient to build from. Concretely, this means:

- specific numbers, not adjectives
- named tools or named contracts where the project depends on them
- code samples or schema fragments where they sharpen a design point
- diagrams whose removal would actually break understanding
- acknowledged tradeoffs — what was rejected, deferred, or remains open

A Stribog reference-grade document should be answerable to the question: *"can a strong engineer build or review the system from this alone?"* If no, it is not yet at reference grade.

## 2. Document Families

Stribog documents fall into a small number of families. Each family has a canonical template under `templates/` and a defined audience.

### 2.1 Governing Documents

These set policy or cross-project rules. Authority over execution.

- Universal Stribog Engineering Charter
- Stribog Documentation Standard
- Stribog AI Agent Execution Standard
- Stribog Operational Delivery Standard
- Charter Governance

Governing documents are versioned, reviewed before freeze, and pinned by individual projects through the Charter Compliance Annex.

### 2.2 Reference Documents

These are architecture-bearing documents that define a system or a major subsystem.

- Master reference (project root)
- Architecture supplements (subsystem-level)
- Storage / interface / contract references
- Testing strategy

Canonical template: `templates/Master-Reference-Template.md`.

### 2.3 Delivery Documents

These convert architecture into execution, or certify that execution is acceptable.

- Build plans (`templates/Build-Plan-Template.md`)
- Architecture Decision Records (`templates/ADR-Template.md`)
- Audit and certification notes (`templates/Audit-Closeout-Template.md`)
- Runbooks (`templates/Runbook-Template.md`)

### 2.4 Per-Project Compliance Documents

These specialize the universal charter for a specific project.

- Charter Compliance Annex (`templates/Charter-Compliance-Annex-Template.md`)
- Local agent rules (`CLAUDE.md`, `AGENTS.md`)
- Waiver register

### 2.5 Public Surface Documents

These explain a repository or product to users and contributors.

- README
- Installation, usage, and API guides
- CLI reference
- [[CONTRIBUTING]] guide
- Changelog
- `SECURITY.md`
- License declaration

For public repositories, this surface is part of project trust, not just onboarding convenience. For platforms like GitHub, the public surface also includes governance-adjacent text artifacts such as `CODEOWNERS`, issue templates, and pull request templates. They are part of the repository contract even when they do not live inside the docs tree.

§2.5 names the public surface in broad strokes; §2.6, §2.7, and §2.8 below split that surface into the three binding sub-families covering user-facing documentation, developer-facing documentation, and user-interface surfaces.

### 2.6 User-Facing Documentation

User-facing documentation — the body of documentation a non-implementer reads to use the product — is a binding sub-family of the public surface. Its architecture (the Diátaxis quadrants), audience model, evidence discipline, in-product help governance, lifecycle, and release coupling are defined by the [[Stribog User Documentation Standard]].

The user-doc family covers, at minimum:

- the quickstart and the how-to library
- the user-facing reference (CLI, configuration, error and exit codes from the user point of view)
- conceptual explanations for the user audience
- the troubleshooting and FAQ library
- user-facing release notes
- the support escalation map
- the in-product help surface (tooltips, empty-state copy, error messages, onboarding strings)

A project that ships a human-operable surface but does not maintain a compliant user-doc family is non-compliant under the [[Stribog User Documentation Standard]] §0.2 applicability.

### 2.7 Developer-Facing Documentation

Developer-facing documentation — the body of documentation an engineer reads to read, change, integrate against, embed, or extend the project — is a binding sub-family of the public surface. Its architecture (generated reference, drift gates, code-sample discipline, public surface stability, deprecation contract), audience model, and release coupling are defined by the [[Stribog Developer Documentation Standard]].

The developer-doc family covers, at minimum:

- the repository README
- the contributor onboarding family (CONTRIBUTING, dev-environment bootstrap, architecture for contributors)
- the integrator-, consumer-, and extender-facing guide library
- generated API, SDK, library, and schema reference
- the ADR index
- the public surface map and the deprecation register
- migration documents across major versions

A project that exposes a developer-callable surface but does not maintain a compliant developer-doc family is non-compliant under the [[Stribog Developer Documentation Standard]] §0.2 applicability.

### 2.8 User-Interface Surfaces

User-interface surfaces — the visual, interactive, and accessibility-bearing surfaces of the product — are governed by the [[Stribog UI/UX Standard]]. Documentation that describes those surfaces (design system documentation, component-library reference, accessibility annotations, motion-token catalogue, design-review records) is itself documentation under this standard and inherits §4 (front matter), §5 (tone), §6 (architecture), and §7 (diagrams), with the UI/UX Standard adding the surface-specific contract.

## 3. File Placement and Naming

### 3.1 Placement Rules

Stribog projects separate documentation by trust and audience. The default split is:

- **repository-shipped public docs** — the public surface
- **repository-shipped internal docs** — internal architecture, planning, audit (typically under `docs/internal/`, ignored from public packaging where applicable)
- **private BrainForest** or equivalent — sensitive personal or operational planning material

Private material does not drift into public or repository-shipped surfaces casually. The boundary is enforced by `.gitignore` and the project's Charter Compliance Annex.

### 3.2 Git-Tracked vs Git-Ignored Documentation

Some Stribog projects deliberately maintain an internal documentation layer that is **repository-local but not repository-shipped**. Typical examples include:

- internal feature specifications
- internal prompts and implementation plans
- internal audit notes
- local-only agent workflow instructions

When a repository uses that pattern:

- the distinction between shipped and non-shipped documentation is explicit in the Charter Compliance Annex
- `.gitignore` reinforces that boundary
- the public documentation surface does not depend on git-ignored internal docs for basic usability
- contributors and agents are instructed in `CLAUDE.md` / `AGENTS.md` not to override the boundary casually

### 3.3 Naming Rules

File names for serious reference documents are explicit and durable.

Preferred characteristics:

- descriptive title-case names
- stable names that match the document's responsibility
- no `notes`, `misc`, or `stuff` naming
- no throwaway-seeming names for long-lived references
- no `-final`, `-final-final`, `-v2-final` suffixes

Examples of good names:

- `Email RAG System Reference.md`
- `Attachment-Architecture.md`
- `Universal-Stribog-Engineering-Charter.md`
- `ADR-0007-Switch-Graph-Store-To-Neo4j.md`

Examples of weak names (forbidden in serious work):

- `ideas.md`
- `random-notes.md`
- `new-architecture-v2-final-final.md`

#### Audit-round filename convention

Stribog charter audit-round records use the canonical filename pattern:

`Charter-Set-Audit-Round-N.md`

where `N` is the integer round number. The word `Audit` is always present. The round number is always in the same position. Filenames are stable identifiers: they do not change on supersession; the closure signal lives in front-matter `status: superseded`, not in the filename. Suffixes such as `-Closed`, `-Final`, `-Old`, or parenthetical closure markers in the filename are forbidden — they encode lifecycle state into a stable identifier and create wikilink-maintenance burden every time state changes.

#### Document title-format parity

When a Stribog document is part of a series (audit rounds, ADRs, project phases), titles share parent structure. The series-name and any qualifying suffix attach without disturbing the parent's word grouping or punctuation.

Example — audit rounds and any associated artifacts:

- `Charter Set Audit — Round N` (the audit round itself)
- `Charter Set Audit — Round N <Qualifier>` (any associated artifact, where `<Qualifier>` describes the artifact's role)

The em dash position and word grouping are inherited from the parent. Drift like `Charter Set Audit Round N — Backlog` (em dash moved to a different position, different word grouping) is forbidden because it breaks parity with the parent series.


### 3.4 Diagram Placement

For repository-resident diagrams, D2 source files live under a controlled path:

- `docs/internal/diagrams/src/`
- `docs/internal/<topic>/diagrams/src/`

Rendered artifacts (SVG, PNG) live separately:

- `docs/internal/diagrams/rendered/`
- `docs/internal/<topic>/diagrams/rendered/`

For BrainForest-resident diagrams (such as the charter set itself), inline `d2` blocks inside the Markdown document are explicitly treated as the canonical source artifact. The document must say so, and the embedded block is the artifact under version control.

### 3.5 Cross-Linking Requirement

Reference-grade documents link their important companion artifacts clearly:

- front-matter relationship fields (`supersedes`, `related_docs`)
- explicit body links to companion references
- explicit links to canonical diagram source and rendered artifacts where diagrams matter

A document that is meaningful only in conjunction with another document but does not link to it is structurally underspecified.

## 4. YAML Front Matter Standard

### 4.1 Front Matter Is Required

All governing, reference, plan, audit, and runbook documents begin with YAML front matter. This is a hard requirement unless the document is intentionally ephemeral.

### 4.2 Required Fields

The minimum required field set is:

| Field | Purpose |
|-------|---------|
| `title` | Human-readable canonical title |
| `type` | Document classification (e.g. `stribog/engineering-charter`, `project/master-reference`) |
| `status` | Current document state, from §10 vocabulary |
| `version` | SemVer for the document's normative content (see §11) |
| `revision` | Monotonic integer that increments on every saved change |
| `last_updated` | Date of last substantive update (ISO `YYYY-MM-DD`) |
| `tags` | Discovery and grouping |
| `aliases` | Alternate names where useful |

### 4.3 Common Optional Fields

Useful optional fields, used when they add clarity rather than ritual noise:

- `scope`
- `project`
- `machine`
- `runtimes`
- `owners`
- `related_docs`
- `supersedes`

### 4.4 Ownership Field

Governing documents must include an `owners` field. Reference-grade documents must include one as well unless ownership is unambiguous from a stronger enclosing control system (e.g. a project repository where a single CODEOWNERS entry obviously covers it).

### 4.5 Preferred Field Order

The preferred field order is:

1. `title`
2. `type`
3. `scope` or `project` where relevant
4. `owners` where relevant
5. `status`
6. `version`
7. `revision`
8. `last_updated`
9. `supersedes` where relevant
10. `related_docs` where relevant
11. `tags`
12. `aliases`
13. additional optional fields

This ordering is not sacred, but drift should be deliberate, not accidental.

### 4.6 Example Front Matter

```yaml
---
title: Universal Stribog Engineering Charter
type: stribog/engineering-charter
scope:
  - all Stribog-owned software, infrastructure, and automation projects
owners:
  - Charter Owner
  - Stribog
status: governing-reference
version: "1.0.0"
revision: 1
last_updated: 2026-05-03
related_docs:
  - Stribog-Documentation-Standard
  - Charter-Governance
tags:
  - stribog
  - engineering
  - charter
aliases:
  - Stribog Engineering Charter
---
```

## 5. Tone, Language, and Prose Standard

### 5.1 Tone

The expected tone for serious Stribog reference work is:

- calm
- precise
- authoritative
- technical
- non-performative

It does not sound like:

- casual chat
- marketing copy
- policy theater
- generic AI summary text
- self-praise ("This document is intentionally rigorous", "We are committed to excellence")

A reference document does not need to tell the reader it is serious. The seriousness is demonstrated by the content.

### 5.2 Language Rules

The language is:

- explicit rather than implied
- concrete rather than vague
- architectural rather than motivational
- honest about uncertainty
- appropriately normative where rules exist

Use words like:

- `must`
- `must not`
- `required`
- `forbidden`
- `recommended`
- `deferred`
- `open risk`

Avoid weak or slippery phrases:

- "probably fine"
- "somehow"
- "maybe later" without a phase boundary
- "best practice" without operational meaning
- "we should" — replace with "the project must" or "the agent must"

### 5.3 Depth Standard

Reference-grade documents explain:

- what the system is
- why it is shaped that way
- what alternatives were rejected or deferred
- what the design implies operationally
- where the known risks are

A document that only states decisions without rationale is not yet at reference grade.

### 5.4 Readability Standard

Serious documents may be dense, but they must remain readable.

That means:

- strong section ordering
- clear subsections
- tables where comparison matters
- bullets where enumeration matters
- restrained repetition used only to reinforce a control point

Avoid:

- bullet soup (paragraph-length thoughts fragmented into lists)
- unnecessary chatter
- repeated filler summaries
- giant undifferentiated walls of text
- meta-commentary that explains the document to itself

### 5.5 Public README and Badge Discipline

For public repositories, the README is a governed trust surface.

It presents a coherent first-contact story that matches actual repository reality:

- what the project is
- how it is installed
- how it is verified
- where the docs live
- what release channel exists
- what the license posture is, where relevant
- where security issues are reported
- which versions or support windows are current, where that matters

Badge usage is allowed and often desirable, but every badge must represent a real, maintained signal — not decoration.

Typical good badge categories:

- CI status
- coverage
- release version
- runtime or language version
- license
- downloads or adoption signals where meaningful

Dynamic badges are wired to real automation outputs.

If a README advertises installation surfaces — package managers, install scripts, release archives, containers, plugin registries — those surfaces correspond to real maintained release pathways, not aspirational placeholders. If public installation guidance offers direct downloads or installer scripts, the surrounding documentation makes artifact verification or provenance expectations legible rather than treating trust as implicit.

### 5.6 Public Repository Governance Documents

For public or shared repositories, governance-adjacent text files are part of the documentation system even when they live under `.github/` or repository root. Examples:

- `SECURITY.md`
- `CODEOWNERS`
- issue templates or forms
- pull request templates
- contributor guides

Issue templates gather reproducible context. Pull request templates reinforce real checklist items: tests, documentation, breaking-change disclosure, and the absence of secrets, PII, or machine-local residue in the diff.

A `SECURITY.md` makes the reporting path, support posture, and disclosure expectations explicit.

These documents reflect the real process. Stale governance surfaces that imply review, disclosure, ownership, or contribution flows that do not actually exist are non-compliant.

## 6. Document Architecture Standard

### 6.1 Numbered Structure

Reference-grade documents use numbered sections.

The pattern:

- `0. TL;DR`
- `0.1`, `0.2`, `0.3` for immediate framing sections
- `1.`, `2.`, `3.` onward for major sections

This pattern makes long documents skimmable without making them feel like legal codes. Short documents (under ~200 lines) may use a simpler structure if they remain readable; everything above that length is numbered.

### 6.2 Canonical High-Level Flow

For master references, the usual flow is:

1. TL;DR
2. current state or bootstrap reality
3. design position or staff-engineer revisions
4. system architecture
5. detailed subsystems
6. operational concerns
7. phased build plan
8. pitfalls and what not to build yet
9. references and tooling

The exact section names may vary; the logical control flow remains deliberate. The canonical skeleton is in `templates/Master-Reference-Template.md`.

### 6.3 Required Content Types for Serious References

Most reference-grade documents explicitly include the relevant subset of:

- scope
- current state
- design position
- architecture
- source-of-truth statements
- assumptions
- non-goals
- open risks
- phased sequencing
- operational implications

### 6.4 Document-Family Templates

Each document family has a canonical template under `templates/`. New documents start from the template, not from a blank file.

| Family | Template |
|--------|----------|
| Master reference | `templates/Master-Reference-Template.md` |
| Architecture Decision Record | `templates/ADR-Template.md` |
| Build plan | `templates/Build-Plan-Template.md` |
| Testing strategy | `templates/Testing-Strategy-Template.md` |
| Audit / certification note | `templates/Audit-Closeout-Template.md` |
| Runbook | `templates/Runbook-Template.md` |
| Waiver register | `templates/Waiver-Register-Template.md` |
| Critique persona | `templates/Critique-Persona-Template.md` |
| Charter Compliance Annex | `templates/Charter-Compliance-Annex-Template.md` |

Template content is normative for shape — sections may be extended, but the canonical sections defined in the template must appear, even if a section's content is "Not applicable to this project" with a one-line reason.

## 7. Diagram Standard

### 7.1 D2 Is the Default

For non-trivial architecture and workflow diagrams, **D2 is the default diagram language**.

It is the preferred baseline because it is:

- text-based
- versionable
- reviewable in Git
- easy to keep close to the source document

### 7.2 Source Control Requirements

Diagram source files are version-controlled. "The rendered PNG exists somewhere" is not sufficient.

If a document embeds D2 directly for readability, the repository still maintains a canonical `.d2` source file for that diagram when the diagram is part of a long-lived governing or reference document. The embedded block is not the canonical artifact unless the document explicitly says so.

For BrainForest-resident charter and standards documents, the embedded `d2` blocks are explicitly treated as the canonical working-source-side source. That declaration is part of the document.

### 7.3 Rendered Artifacts

For canonical or long-lived repository-resident documents, both SVG and PNG must be produced so the diagram remains useful in both rich and plain viewing contexts. For BrainForest-resident documents that rely on the D2 Obsidian plugin for inline rendering, rendered artifacts are not required.

### 7.4 Styling Expectations

D2 diagrams are:

- deliberate
- readable
- color-controlled
- structurally simple enough to review as code

Avoid:

- default-looking diagrams with no visual hierarchy
- excessive line crossing
- unexplained abbreviations
- diagrams that are more decorative than explanatory

A diagram earns its place when its removal would degrade the document's understanding. A diagram that merely repeats the prose is decorative and should be cut.

### 7.5 When a Diagram Is Required

A diagram is strongly recommended when a document explains:

- multi-stage pipelines
- layered control models
- storage or trust boundaries
- state machines
- non-trivial fan-out / fan-in flows
- interaction between public, internal, and private surfaces

## 8. Tables, Code Blocks, and Callouts

### 8.1 Tables

Use tables when comparing:

- alternative choices
- quality gates
- document classes
- phase boundaries
- required artifacts
- mandates by area

Do not use tables to force structure where a short paragraph is clearer.

### 8.2 Code Blocks

Use fenced blocks with explicit language tags:

- `d2`
- `yaml`
- `json`
- `bash`
- `fish`
- `go`
- `python`
- `sql`
- `cypher`

The Charter Compliance Annex names the languages used by the project so style discipline (highlighting, lint behavior in docs) is consistent.

### 8.3 Callout Discipline

Short blockquotes or emphasis lines are acceptable for positioning statements, used sparingly. The prose carries the document; callout styling does not.

## 9. Change Triggers and Review Cadence

### 9.1 Update Triggers

Reference-grade documents are updated when any of the following occurs:

- a material architecture change
- a changed source-of-truth boundary
- a new phase begins or a phase closes
- an interface or schema contract changes
- a safety posture changes
- released behavior changes in a way the document claims to describe
- a dependency that materially shapes the document is replaced or upgraded
- a clause of the parent governing document changes in a way that affects this document

Trigger detection is part of the engineer's and the agent's responsibility. A Stribog project is not "done with a change" until governing documents are updated where they apply.

### 9.2 Freeze Review

Before a document moves to `frozen-reference` or `governing-reference`, it is reviewed for:

- structural completeness
- language precision
- alignment with implementation reality
- status correctness
- diagram-source consistency where diagrams exist
- front-matter accuracy

A freeze without a review is not a freeze; it is a guess.

## 10. Status Vocabulary and Lifecycle

### 10.1 Status Vocabulary

The Stribog status vocabulary is fixed. New documents pick from this list:

| Status | Meaning |
|--------|---------|
| `draft-scaffold` | Skeleton or placeholder. Not yet usable as a basis for anything. |
| `review-draft` | Substantively written; under active review and expected to change. |
| `design-reference` | Usable as a design basis, but not yet frozen. May still change with notice. |
| `governing-reference` | Authoritative baseline. Changes require deliberate revision under §11. |
| `frozen-reference` | Locked. Changes require a new revision and explicit unfreezing review. |
| `superseded` | Replaced by another document. Retained for history. |
| `archived` | No longer active; retained only for historical reference. |

Projects may not invent additional statuses. A project that needs a finer state distinction adds the distinction in its Charter Compliance Annex by specializing one of the values above.

### 10.2 Status Must Mean Something

Status values are not decorative metadata. They correspond to how the document should be treated by readers and contributors. A document tagged `governing-reference` cannot be edited as freely as a `review-draft`; a document tagged `frozen-reference` requires explicit unfreeze before modification.

The distinction between `governing-reference` and `frozen-reference` is operational:

- `governing-reference` — authoritative; updates flow through normal §11 revision discipline
- `frozen-reference` — explicitly locked because external systems pin to it; updates require unfreeze + new revision

Projects that do not need the frozen distinction simply do not use it.

## 11. Versioning and Revision Semantics

### 11.1 Two Independent Counters

Every governing or reference document carries two counters in front matter:

- `version` — `MAJOR.MINOR` for the document's normative content (a `.0` patch component is retained for SemVer compatibility but is not used to track changes)
- `revision` — a monotonic integer that increments on every saved substantive change

The two counters serve different purposes and move on different triggers. `version` answers "what compliance contract does this document offer?" and changes only on normative shifts. `revision` answers "what state of the document was in force at a given moment?" and changes on every substantive save, normative or editorial.

### 11.2 Version Semantics for Documents

Stribog documents use a deliberately reduced SemVer: only `MAJOR` and `MINOR` are used to track meaning. Patch-grade editorial changes flow through `revision` and do not bump `version`.

| Bump | Trigger |
|------|---------|
| `MAJOR` | Breaking change — a clause that may put a previously-compliant project out of compliance. Requires deliberate migration. |
| `MINOR` | New non-breaking section, new optional field, additional rule that does not invalidate any prior compliant project. |
| (no PATCH for documents) | Editorial fixes, typos, formatting, clarifications that do not change meaning are tracked through `revision` only. The `version` field stays unchanged. |

This deliberately departs from SemVer-for-software, where PATCH would bump the third version component on bug fixes. Documents are not software; their consumers (projects pinning to a charter version) only care about whether the compliance contract has changed. Editorial cleanups do not change the contract, so they do not change the version. They are still tracked — through `revision` and the document's §Revision History — so the audit trail remains complete.

Projects pin to a specific `MAJOR.MINOR` of governing documents in their Charter Compliance Annex. They do not float against `MAJOR`. A project moving from `MAJOR=N` to `MAJOR=N+1` is a deliberate migration.

The `.0` patch component on every published `MAJOR.MINOR.0` exists for SemVer parsing compatibility (toolchains that expect three-component versions). It is never incremented above zero by Stribog convention.

### 11.3 Revision Discipline

`revision` is a write-counter for the document. It does not skip. It does not reset on `version` bumps. It increments on every saved change that is more than whitespace.

`revision` is the field used by waivers, audit notes, and compliance declarations to identify exactly which version of a document was in force at the time. A waiver that says "valid against revision 11" is unambiguous; "valid against the latest version" is not.

### 11.4 Freeze Rule

When a document becomes the basis for implementation, phase planning, or release review, it moves toward a frozen or governing status. Endless silent edits to a document that people are building against are dangerous.

A document at `governing-reference` or `frozen-reference` accumulates revisions but does so deliberately. A revision that bumps `MAJOR` of a frozen document requires unfreeze, review, and re-freeze under the Charter Governance lifecycle.

## 12. Documentation Definition of Done

A Stribog document is done when:

- front matter is complete and conforms to §4
- title and type are explicit
- status is accurate and from the §10 vocabulary
- `version` and `revision` are correct
- a §Revision History section is present and current (required for every governing or reference-grade document)
- section ordering is deliberate and follows §6
- rationale is present where the document captures decisions
- boundaries are explicit
- diagrams exist where they materially help, with sources tracked per §7, and reflect current canon (a stale diagram is non-compliant)
- risks and non-goals are named
- the language is precise per §5
- the document does not contradict implementation reality
- the document does not contradict its own front matter or its own earlier sections
- companion documents are linked per §3.5

This applies equally to documents written directly by a maintainer and to documents generated or revised by an AI agent. AI-authored documents follow the same standard; agent-side discipline is governed by the Stribog AI Agent Execution Standard.

## 13. Anti-Patterns

The following are documentation anti-patterns under this standard and are forbidden in serious work:

- architecture hidden across chat transcripts instead of captured in a reference
- "final" documents with throwaway naming and no version/status discipline
- giant notes with no section architecture
- vague inspirational language with no implementation consequence
- diagrams with no source file
- stale docs left unmarked
- public docs that accidentally leak private or sensitive material
- README badge rows disconnected from actual automation or repository state
- public governance files that imply workflows or review controls the repository does not truly enforce
- documents that describe themselves rather than the system they govern
- documents whose body contradicts their own front matter
- copy-paste from another project's reference without adapting source-of-truth claims

## 14. Practical Authoring Rule

When drafting a serious Stribog document, the author asks:

1. can a strong engineer build or review the system from this?
2. are the boundaries, risks, and rationale explicit?
3. does this read like a governing reference, or like a cleaned-up conversation?
4. if this document drifts, will someone notice?
5. does this document name the things it depends on, or hand-wave around them?

If the answer to any of those is no, the document is not yet complete.

---

## 15. Revision History

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 2.1.0 | 6 | 2026-05-12 | MINOR bump applied during Charter Set Audit Round 6 closeout. §2 Document Families expanded: §2.5 retained as the broad public-surface catalogue; §2.6 added to name the User-Facing Documentation sub-family under the [[Stribog User Documentation Standard]]; §2.7 added to name the Developer-Facing Documentation sub-family under the [[Stribog Developer Documentation Standard]]; §2.8 added to point user-interface surfaces at the [[Stribog UI/UX Standard]]. Closes Round 6 finding F62 (User-facing documentation, Developer-facing documentation, and UI/UX surfaces absent from the charter set). No clause was weakened; no previously-compliant project becomes non-compliant under v2.1.0 — the three new standards bind per their own §0.2 applicability clauses, and projects whose surfaces predate v2.1.0 declare their compliance posture in the next Charter Compliance Annex review per Charter Governance §6.1. |

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 0.11.0 | — | 2026-05-03 | Final review-draft prior to v1.0.0 promotion. Superseded by v1.0.0. |
| 1.0.0 | 1 | 2026-05-03 | Initial governing-reference release. Defined required front matter, structure, tone, depth, diagram discipline, status vocabulary, version/revision semantics, document families, and templates set (six families). |
| 1.1.0 | 2 | 2026-05-03 | MINOR bump applied during Charter Set Audit Round 3. Expanded §6.4 Document-Family Templates from six to nine entries to match the actual canon: added **Testing strategy**, **Waiver register**, and **Critique persona** template families. Updated `related_docs` to reference all nine templates. Added this §15 Revision History section. No clause was weakened. The earlier v1.0.0 published a stale §6.4 because the canon expanded between Round 2 and Round 3 without a corresponding §6.4 update; Round 3 closes this drift. |
| 1.2.0 | 3 | 2026-05-03 | MINOR bump applied during Charter Set Audit Round 3 closeout. Reconciled §11 versioning semantics: §11.1 and §11.2 of v1.1.0 contradicted each other (§11.1 said editorial cleanups bump revision only; §11.2 SemVer table said PATCH covers editorial fixes — i.e. version bumps). Resolved by deleting PATCH from the document SemVer model: documents use only `MAJOR` and `MINOR`; editorial changes flow through `revision` only. The published `.0` patch component is retained for SemVer-parser compatibility but is never incremented. Expanded §12 Definition of Done to require a §Revision History section, to require diagrams to reflect current canon, and to forbid documents that contradict their own front matter or own earlier sections (§12 anti-pattern). Closes Round 3 finding F33 (SemVer ambiguity), F40 (some governing docs lacked Revision History), F41 (audit doc lacked Revision History), F42 (Definition of Done did not require Revision History). |
| 1.3.0 | 4 | 2026-05-03 | MINOR bump applied during Charter Set Audit Round 4. Added `working-document` to §10.1 status vocabulary (between `frozen-reference` and `superseded`) to canonize the between-rounds-backlog pattern that emerged after R3 sign-off. Added §10.3 Working-Document Discipline defining the four properties (non-authoritative, operational, finite-lived, history-bearing), the example artifact list, and the four forbidden behaviors. Closes Round 4 finding F55 (`working-document` status was used in `Charter-Set-Round-4-Backlog.md` outside the §10.1 fixed vocabulary; the canon now ratifies the value rather than treating it as an invention). No clause was weakened. The previous fixed-vocabulary mandate is preserved: the vocabulary remains fixed at seven values; F55's defect was using an invented value, not the addition of a needed value through the proper change cycle. |
| 2.0.0 | 5 | 2026-05-03 | **MAJOR bump** applied during Charter Set Audit Round 5. **§10.3 Working-Document Discipline deleted entirely.** `working-document` value removed from §10.1 status vocabulary (vocabulary returned to seven values: `draft-scaffold`, `review-draft`, `design-reference`, `governing-reference`, `frozen-reference`, `superseded`, `archived`). Rationale: the working-document pattern was introduced at v1.3.0 to canonize between-rounds-backlog files. In the half-day after v1.3.0 ratification, the pattern produced five findings (F55 invention, F57 closure-marker confusion, F58 filename-convention drift, F59 preservation-on-supersession wrongness, F60 title-parity drift). Audit Round 1 — the model — was filed cleanly without a backlog file at all; between-rounds findings live in beads (the durable issue tracker) until the next round opens. The simpler answer was overlooked at v1.3.0; v2.0.0 retracts the over-engineering. Closes Round 5 finding F61. **§3.3 expanded** with two new sub-clauses: audit-round filename convention (`Charter-Set-Audit-Round-N.md`, stable identifiers, no `-Closed` suffix) and document title-format parity (series-name with consistent em-dash position and word grouping). Closes Round 5 findings F58 (filename convention) and F60 (title-format parity). MAJOR bump because removing a §10.1 vocabulary value could put a previously-compliant artifact out of compliance, even though no such artifact exists at v1.3.0 close (the only working-document, the R5 Backlog, is being deleted as part of R5 closeout per the F61 deletion mandate). MAJOR on principle, not on practice. The Documentation Standard's structural cleanup is the single largest finding-closure of any audit-round to date. |

---
