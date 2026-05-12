---
title: "<Project Name> — Developer Documentation"
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
type: stribog/developer-documentation
status: <draft | governing-reference>
tags: [stribog, developer-documentation]
version: "0.1.0"
revision: 1
audience: <e.g. contributors, integrators, SDK consumers>
parent_moc: "<[[MOC - Project Name]]>"
owners: [<doc-owner>]
---

# <Project Name> — Developer Documentation

> <One-sentence description of the public surface this project exposes to developers.>

Per [[Stribog Developer Documentation Standard]].

---

## README Skeleton

> The README is the canonical entry point for any developer discovering this project.

### What this is

<One paragraph: what the project does, what problem it solves, and who should use it.>

### Install

```<language>
<install command or dependency declaration>
```

### Minimal example

```<language>
<smallest useful code snippet that demonstrates the core callable>
```

### Further reading

- [Quickstart](#dev-environment-bootstrap)
- [Public Surface Map](#public-surface-map)
- [CONTRIBUTING](#contributing)

---

## CONTRIBUTING Skeleton

> Defines the contributor workflow. Keep it short — point to full standards rather than duplicating them.

### Prerequisites

- <tool 1> `<minimum version>`
- <tool 2> `<minimum version>`

### Dev-environment bootstrap

See [Dev-Environment Bootstrap](#dev-environment-bootstrap) below.

### Workflow

1. Fork or branch from `main`.
2. Run `make all` (or `<equivalent>`) before submitting — all gates must pass.
3. Write tests first (TDD per Engineering Charter §4).
4. Open a pull request against `main`. Title format: `<type>: <short description>`.

### Commit and attribution

<reference to Engineering Charter §7.7 for AI-attribution trailer format>

---

## Architecture for Contributors

> Explains the internal structure to the level a new contributor needs to make a change.

### Repository layout

| Directory / File | Purpose |
|---|---|
| `<path>` | <purpose> |
| `<path>` | <purpose> |

### Key design decisions

- <ADR pointer or inline rationale for most important structural decision>
- <ADR pointer or inline rationale for second decision>

### How a request / invocation flows

<Short prose or ordered list tracing a typical call through the system.>

---

## Public Surface Map

> Required by [[Stribog Developer Documentation Standard]]. Lists every callable, endpoint, flag, config key, exit code, and schema field that is part of the public contract. Stability column governs the deprecation window.

| Callable / Endpoint / Flag / Config key / Exit code / Schema field | Type | Stability | Description |
|---|---|---|---|
| `<name>` | <function \| HTTP endpoint \| CLI flag \| env var \| exit code \| schema field> | <stable \| beta \| experimental \| deprecated> | <one-line description> |

**Stability definitions:**
- `stable` — governed by compatibility window; breaking changes require a deprecation notice and migration guide.
- `beta` — may change in minor releases with notice.
- `experimental` — may change or be removed at any time; no deprecation guarantee.
- `deprecated` — still present; removal scheduled per the Deprecation Notice register below.

---

## Generated Reference Pipeline

> Declares how API / config / schema reference is generated. Required when the project has a generated reference surface.

| Surface | Generator tool | Source | Output path | Drift-gate command |
|---|---|---|---|---|
| <e.g. Go pkg docs> | <e.g. godoc / pkgsite> | <e.g. `internal/`> | <e.g. `docs/reference/`> | `make drift-gate` |

---

## Deprecation Notice Register

> Every deprecated surface has an entry here. Required by [[Stribog Developer Documentation Standard]].

| Surface | Deprecated since | Removal target | Replacement | Migration guide |
|---|---|---|---|---|
| `<name>` | `<version>` | `<version or date>` | `<replacement>` | `<path or URL>` |

---

## Dev-Environment Bootstrap

**Minimum time to first green test:** `<e.g. under 5 minutes>`

```bash
# 1. Clone
git clone <repo-url>
cd <repo-name>

# 2. Install dependencies
<install command>

# 3. Run all gates
make all

# 4. Verify
make test
```

**Common issues:** <link to troubleshooting section or issue tracker>

---

## Document Revision History

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 0.1.0 | 1 | <YYYY-MM-DD> | Initial skeleton filed from template. |
