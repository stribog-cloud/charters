---
title: "<Project Name> Testing Strategy"
created: 2026-05-04
updated: 2026-05-04
type: project/testing-strategy
status: governing-reference
tags: [charter, governance, security, stribog]
project: <project-id>
version: "1.0.0"
revision: 2
last_updated: YYYY-MM-DD
parent_moc: "[[MOC - Stribog Governance]]"
---


# <Project Name> Testing Strategy

> The testing strategy for <Project Name>. Documents the testing layers, fixture posture, contract strategy, and verification philosophy adopted by this project.

---

> **Template usage.** Replace every `<placeholder>` with project-specific content. Italicized guidance paragraphs are removed from the live document. The testing strategy is required by Engineering Charter §2.1 once a project's testing surface becomes non-trivial; it is updated at every phase boundary and at any material change to the testing approach.

---

## 0. TL;DR

*Two or three paragraphs. What testing approach this project takes, why those choices, and what coverage and quality gates apply. A reader should know within a minute whether this project's testing posture matches what they expected.*

| Property | Value |
|----------|-------|
| Development methodology | Test-Driven Development (per Engineering Charter §4) |
| Coverage floor | 96% (per Engineering Charter §5.4) |
| Project-declared floor | <e.g. 96% / project-specific stricter floor> |
| Per-package floor for critical paths | <e.g. 98% for security-sensitive packages> |
| Primary test framework | <e.g. Go testing package, pytest, vitest> |
| End-to-end test framework | <e.g. Bats with Kind, Playwright, custom> |
| Coverage tool | <e.g. go test -cover, pytest-cov> |
| Static analysis | <e.g. golangci-lint, mypy, eslint --strict> |

## 1. Guiding Principles

*The principles that shape every testing decision in this project. Specific enough to drive choices, not generic enough to be motivational.*

The strategy is rooted in:

1. **The testing pyramid applies.** Heavy unit tests, moderate integration tests, lean end-to-end tests. Optimize for speed and cost-efficiency.
2. **Contract testing is the structural backbone** for any subsystem with multiple implementations, plugins, or registries.
3. **Shift-left everything.** Static analysis, race detection, linting, and coverage tracking run on every commit.
4. **Test infrastructure is a first-class investment.** Fixture loaders, helpers, generators, and test harnesses are foundational code, not afterthoughts.
5. **Maximize what can be tested without external dependencies.** Mock external services, use in-memory implementations, fixture-load complex inputs.
6. **TDD is the development methodology.** Tests precede implementation. The red-green-refactor cycle shapes the codebase.

*Project-specific additions:*

- <Additional principle relevant to this project>

## 2. Test-Driven Development — How Code Gets Written

### 2.1 Why TDD for This Project

*Project-specific rationale for TDD. What property of the project benefits most from test-first development.*

<TDD rationale.>

### 2.2 The TDD Cycle in Practice

The development of each component follows the red-green-refactor pattern:

1. write the failing test
2. observe the failure (the test must actually fail before the implementation makes it pass; this is observable in closeout evidence per AI Agent Execution Standard §3.1 for AI-assisted work)
3. implement the smallest correct change to produce green
4. refactor while preserving green

### 2.3 What TDD Produces

*Architectural consequences of TDD discipline in this project. APIs that are consumer-driven, types that emerged from test ergonomics, contracts that were defined before implementation.*

- <Consequence>
- ...

### 2.4 Bug Fixes

Bug fixes follow the reproduction-first flow per Engineering Charter §4.3: encode the bug in a failing test, fix the code, retain the regression test permanently.

### 2.5 TDD vs BDD

*If BDD-style fixtures or scenarios are used in this project, name them. Otherwise this section states that BDD is not used and the rationale.*

<BDD usage statement.>

## 3. Test Layers

### 3.1 Layer 1: Unit Tests

*The foundation. Roughly 60-70% of test volume. Run in milliseconds. Cover individual functions, methods, types, in isolation.*

**What gets unit tested:**

- <Package> — <what is tested>
- <Package> — <what is tested>

**Key patterns:**

- Table-driven tests with comprehensive case coverage
- <Project-specific pattern>

### 3.2 Layer 2: Integration Tests

*Moderate volume. Test the interaction of multiple components without crossing the project boundary.*

**What gets integration tested:**

- <Workflow or component interaction>
- <Workflow or component interaction>

### 3.3 Layer 3: Contract Tests

*Per Engineering Charter §5.7. Required for any subsystem designed for multiple implementations.*

**Where contract tests apply:**

- <Extension seam — registry, provider, plugin, parser, etc.>
- <Extension seam>

**Pattern:**

The contract test iterates over all registered implementations and verifies that each satisfies the shared contract. <Project-specific pattern detail.>

### 3.4 Layer 4: Golden Tests

*Per Engineering Charter §5.8. Required where output stability matters to downstream users or tooling.*

**Where golden tests apply:**

- <Output format>
- <Output format>

**Update discipline:**

Golden files are updated only when the output change is intentional. The update is a deliberate commit, not a side effect of running tests with an `--update` flag without review.

### 3.5 Layer 5: End-to-End Tests

*Lean volume. Exercise the system across all its layers including external boundaries.*

**Framework:** <e.g. Bats with Kind, Playwright, custom>

**Scenarios covered:**

- <Scenario>
- <Scenario>

**Why this scope:** <Rationale for what is and is not covered at this layer.>

### 3.6 Layer 6: Benchmark and Performance Tests

*Required only where performance materially matters per Engineering Charter §9.1.*

**Approach:**

<If applicable, describe the benchmark approach. If not applicable, state that and link to a follow-up if performance becomes material.>

## 4. Test Infrastructure

*Per Engineering Charter §5.2, test infrastructure is a first-class engineering asset. This section names the infrastructure pieces and the design decisions behind them.*

### 4.1 Fixture System

**Layout:**

```
test/fixtures/
├── <category-1>/
│   ├── passing.<ext>
│   └── failing.<ext>
├── <category-2>/
└── ...
```

**Loaders:**

- `<helper>` — <purpose>
- `<helper>` — <purpose>

### 4.2 Test Helpers

**Generators:**

- `<generator>` — <what it produces>

**Assertions:**

- `<assertion>` — <what it asserts>

**Pattern:** Functional options where appropriate, so tests read as specifications of the resource being created.

### 4.3 Mock Strategy

*What is mocked, what is not. The default Stribog preference is to use real implementations where they are cheap (in-memory databases, embedded indexes) and mock only at trust or external-system boundaries.*

| External dependency | Mock strategy |
|---------------------|---------------|
| <e.g. cloud API> | <e.g. mock transport with recorded responses> |
| ... | |

### 4.4 Test Infrastructure Tests

The test infrastructure is itself subject to TDD per Engineering Charter §5.2 and AI Agent Execution Standard §3.3. Each helper, generator, and fixture loader has its own tests verifying its behavior before it is depended upon.

## 5. Coverage Strategy

### 5.1 Coverage Floor

The project's coverage floor is **96%** per Engineering Charter §5.4. <If the project declares a stricter floor, name it here.>

### 5.2 Measurement Boundary

*Per Engineering Charter §5.5. Declare what is measured and what is excluded.*

**Measured:**

- <package or path>
- <package or path>

**Excluded with rationale:**

- `<path>` — <reason>
- ...

### 5.3 Per-Package Floors

*Per Engineering Charter §5.6. For critical packages where the global floor is insufficient.*

| Package | Floor | Rationale |
|---------|-------|-----------|
| `<critical package>` | <e.g. 98%> | <e.g. security-sensitive code path> |
| ... | | |

### 5.4 Coverage Discipline

- Coverage is measured on every CI run
- A commit that drops coverage below the floor is non-compliant
- Coverage is not satisfied by trivial assertions (per AI Agent Execution Standard §3.4)
- Coverage exclusion is a governance change per Engineering Charter §5.5; it is not adjusted to flatter the percentage

## 6. Shift-Left Quality Enforcement

*Per Engineering Charter §5.3. Catch defects as early as possible.*

| Layer | Tool | Trigger |
|-------|------|---------|
| Format | <e.g. gofmt + goimports> | local edit, pre-commit, CI |
| Lint | <e.g. golangci-lint> | local, CI |
| Static analysis | <e.g. go vet, mypy> | local, CI |
| Race detection | <e.g. go test -race> | local for changed packages, CI for full suite |
| Vulnerability scan | <e.g. govulncheck> | local on demand, CI on every push |
| Secret scan | <e.g. gitleaks> | pre-commit hook, CI over reachable history |
| Coverage | <e.g. go test -coverprofile> | CI, gating merge |

## 7. CI Posture

CI mirrors the local gates per Engineering Charter §7.3. The CI pipeline runs:

1. format check (fail on formatting drift)
2. lint
3. static analysis
4. unit tests with race detection
5. integration tests
6. contract tests
7. golden tests
8. coverage measurement and floor enforcement
9. secrets scan
10. vulnerability scan
11. build

End-to-end tests run on a defined cadence (per push, per merge to primary, scheduled, or per release) named in the Compliance Annex.

## 8. Test Authorship Discipline

### 8.1 For Human Contributors

Tests are written first per Engineering Charter §4. The failing-test observation precedes the implementation; the resulting commit history makes the TDD path legible.

### 8.2 For AI Agents

AI-assisted work follows the same discipline with the same-turn TDD property per AI Agent Execution Standard §3.1: the test is written, run, observed failing, then the implementation is added and the test re-run. Closeout evidence per AI Agent Execution Standard §4 records both observations.

Test quality is verified during the agent self-audit per AI Agent Execution Standard §10 — trivial, vacuous, or tautological tests are not compliant even if they raise the coverage number.

## 9. Maintenance and Drift

Tests are reviewed on the same cadence as the code they cover. Tests that have been disabled or skipped accumulate as a finding at the next phase or audit boundary; the project does not silently carry skipped tests.

Golden files that drift from the actual output of the system are repaired by intentional commit, not by reflexive regeneration. A golden-file change is reviewed for whether the underlying behavior change was intended.

## 10. References

- Universal Stribog Engineering Charter §4 (development method) and §5 (testing, coverage, quality gates)
- Stribog AI Agent Execution Standard §3 (TDD discipline for agents) and §4 (closeout evidence)
- Charter Compliance Annex §1 (toolchain) and §1.4 (test layer assignment)
- <Project-specific references>

## Template Revision History

*This section governs the template itself, not template instances. Instance documents created from this template carry their own §Revision History per Documentation Standard §12.*

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 0.1.0 | 1 | 2026-05-03 | Initial release at `design-reference` grade. Defined the project testing-strategy contract (TDD posture, test layers, test infrastructure, coverage strategy and measurement boundary, contract tests, golden tests, shift-left enforcement, fixture and harness design). |
| 1.0.0 | 2 | 2026-05-03 | Promoted from `design-reference` v0.1.0 to `governing-reference` v1.0.0 during Charter Set Audit Round 4. Adopted Criterion C from R4 Backlog §2: all canon templates at v1.0.0 are `governing-reference` regardless of placeholder content; `design-reference` is reserved for templates still in active drafting. The testing strategy template's content has stabilized; placeholder syntax is the template's defining shape rather than a draftiness signal. Added this Template Revision History to align with the pattern established by ADR, Audit Closeout, Charter Compliance Annex, Critique Persona, Runbook, and Waiver Register templates. Closes Round 4 finding F52 (template status discipline inconsistent across canon). No normative change to the template's content. |

---
