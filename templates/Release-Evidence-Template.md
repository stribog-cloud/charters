---
title: "<Project Name> — Release Evidence"
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
type: stribog/release-evidence
status: governing-reference
tags: [stribog, release, evidence]
release-version: "<e.g. 1.2.0>"
release-date: "<YYYY-MM-DD>"
project: "<project name>"
owners: [<release-owner>]
---

# <Project Name> — Release Evidence

Release `<version>` on `<date>`. Per Engineering Charter §7.4.

---

## Reproducible Build

| Property | Value |
|---|---|
| Build command | `<exact command that produces the release artifact>` |
| Build environment | `<OS, tool version, e.g. "Ubuntu 24.04, Go 1.25.0">` |
| Expected artifact hash (SHA-256) | `<hash>` |
| Observed artifact hash (SHA-256) | `<hash>` |
| Hash match | `<yes / no — MUST be yes to release>` |
| Artifact path(s) | `<path(s) to built artifact(s)>` |

---

## Integrity Reference

| Artifact | SBOM pointer | Signature pointer | Verification command |
|---|---|---|---|
| `<artifact name>` | `<path or URL to SBOM>` | `<path or URL to signature>` | `<e.g. cosign verify ...>` |

---

## Smoke Test Record

> Run against the shipped artifact, not the source tree.

| Test / Command | Expected outcome | Observed outcome | Pass |
|---|---|---|---|
| `<smoke test command 1>` | `<expected>` | `<observed>` | `<yes / no>` |
| `<smoke test command 2>` | `<expected>` | `<observed>` | `<yes / no>` |

**Overall smoke result:** `<PASS / FAIL>`

---

## Size Budget Compliance

| Property | Value |
|---|---|
| Declared size budget | `<e.g. "binary ≤ 20 MB">` (Charter Compliance Annex §1.3) |
| Observed artifact size | `<observed size>` |
| Within budget | `<yes / no>` |
| Notes | `<any relevant context, e.g. "compressed: X MB, uncompressed: Y MB">` |

---

## Source / Artifact Boundary

| Property | Value |
|---|---|
| Source root | `<path — coverage, lint, static analysis apply here>` |
| Generated / excluded paths | `<paths excluded from coverage per Annex §1.3>` |
| Artifact root | `<path — reproducibility, integrity, size, smoke-test discipline applies here>` |
| Boundary declaration location | `<Compliance Annex §1.3 or other governing document>` |

---

## Provenance Trailer

| Property | Value |
|---|---|
| Built by | `<name or role — human or AI agent>` |
| AI-attribution | `<if AI-assisted, provider-neutral trailer per Engineering Charter §7.7>` |
| Build tooling | `<tool name and version>` |
| Build timestamp (UTC) | `<ISO 8601 datetime>` |
| Release commit SHA | `<full git SHA of the tagged commit>` |
| Release tag | `<e.g. v1.2.0>` |
| Signing key / identity | `<key ID or signing identity, if applicable>` |

---

## Release Checklist

- [ ] Hash match verified
- [ ] SBOM present and linked
- [ ] Smoke tests pass against the shipped artifact
- [ ] Size budget met
- [ ] Source/artifact boundary matches Compliance Annex §1.3
- [ ] Release commit tagged and pushed (or equivalent for local-only releases)
- [ ] This evidence record filed to the project's audit trail

---

*Filed by `<name>` on `<date>`. This record is append-only after filing.*
