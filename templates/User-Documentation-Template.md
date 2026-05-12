---
title: "<Project Name> — User Documentation"
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
type: stribog/user-documentation
status: <draft | governing-reference>
tags: [stribog, user-documentation]
version: "0.1.0"
revision: 1
audience: <e.g. end-users, non-engineer operators, integrators>
parent_moc: "<[[MOC - Project Name]]>"
owners: [<doc-owner>]
---

# <Project Name> — User Documentation

> <One-sentence description of what this project does and who it serves.>

Per [[Stribog User Documentation Standard]]. Structured on the Diátaxis framework: Quickstart, Tutorials, How-to Guides, Reference, and Explanation are distinct quadrants serving distinct reader needs.

---

## Quickstart

> Goal: reader achieves a working outcome in under five minutes.

**Prerequisites**

- <prerequisite 1>
- <prerequisite 2>

**Steps**

1. <Step 1 — install or obtain the project>
2. <Step 2 — minimal configuration>
3. <Step 3 — run the first command or action>

**Expected outcome:** <what the reader sees when it works>

---

## Tutorials

> Goal: learning-oriented. Each tutorial guides the reader through a complete end-to-end task, building competence.

### Tutorial 1: <Name of first tutorial>

**What you will learn:** <one sentence>

**Duration:** <estimated time>

**Prerequisites:** <list or "none beyond Quickstart">

**Steps**

1. <Step 1>
2. <Step 2>
3. <Step 3>

**Verification:** <how the reader confirms success>

---

## How-to Guides

> Goal: task-oriented. Each guide answers "how do I accomplish X?" for readers who already understand the basics.

### How to <task 1>

**When to use this:** <brief context>

1. <Step 1>
2. <Step 2>

### How to <task 2>

**When to use this:** <brief context>

1. <Step 1>
2. <Step 2>

---

## Reference

> Goal: information-oriented. Complete, accurate, and scannable. Written to be consulted, not read linearly.

### <API / CLI / Configuration reference title>

| <Parameter / Flag / Field> | Type | Default | Description |
|---|---|---|---|
| `<name>` | `<type>` | `<default>` | <description> |

### Exit Codes (if applicable)

| Code | Meaning |
|---|---|
| `0` | Success |
| `<N>` | <meaning> |

---

## Explanation

> Goal: understanding-oriented. Explains concepts, design decisions, and background needed to use the project effectively.

### <Concept or design topic 1>

<Explanation of the concept and why it matters to the user.>

### <Concept or design topic 2>

<Explanation of the concept and why it matters to the user.>

---

## Release Notes

> Point to the project's canonical release notes location rather than duplicating them here.

Release notes for this project are maintained at: `<path or URL to CHANGELOG / release notes>`

See the release notes before upgrading across major versions.

---

## In-Product Help Mapping

> Maps UI entry points or CLI help flags to the documentation sections they link to. Required by [[Stribog User Documentation Standard]].

| UI entry point / CLI flag | Links to section | Notes |
|---|---|---|
| `--help` / `-h` | Reference | Generated from code; keep in sync with this Reference section |
| <UI tooltip or modal> | <Section> | <any localization or versioning notes> |

---

## Document Revision History

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 0.1.0 | 1 | <YYYY-MM-DD> | Initial skeleton filed from template. |
