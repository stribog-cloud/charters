---
title: "<Project Name> Charter Compliance Annex"
created: 2026-05-04
updated: 2026-05-12
type: project/charter-compliance-annex
status: governing-reference
tags: [anthropic, borg-backup, charter, claude-stack, governance, incident, k8s]
project: <project-id>
version: "1.2.0"
revision: 11
last_updated: 2026-05-12
parent_moc: "[[MOC - Stribog Governance]]"
---


# <Project Name> — Charter Compliance Annex

> The authoritative declaration of which charter versions this project is bound by, what tooling implements the charter's gates, and any project-specific specializations.

---

> **Template usage.** This is the most important per-project document in the Stribog governance system. It is the single document an auditor or AI agent reads to know what governs this project. Every Stribog project has one, and it is kept current at every charter version migration and every project phase boundary.
>
> Replace every `<placeholder>`. Italicized guidance paragraphs are removed from the live document. The two reference fills at the end (§A — Go service, §B — infra-only managed service) are illustrative; they are kept in this template until the project files its own annex, and removed once project-specific content replaces them.

---

## 0. Charter Pins

*The exact versions of the governing documents this project is bound by. Pinning is to `MAJOR.MINOR` per Documentation Standard §11; revision-only editorial updates (`PATCH`-grade changes within the same `MAJOR.MINOR`) flow through automatically without ceremony, and a `MAJOR` migration is a deliberate event recorded under §6. The `Applicability` column declares whether the standard applies to this project per its own §0.2; standards that do not apply are still listed and explicitly marked **N/A** with a one-line rationale, so the absence is recorded rather than implied.*

| Governing Document | Applicability | Pinned Version | Pinned Revision (last reviewed at) |
|--------------------|---------------|----------------|------------------------------------|
| Universal Stribog Engineering Charter | Applies (binds every Stribog project) | <e.g. 1.1> | <e.g. revision 5, 2026-05-03> |
| Stribog Documentation Standard | Applies (binds every Stribog document of governing/reference grade) | <e.g. 2.0> | <e.g. revision 5, 2026-05-03> |
| Stribog AI Agent Execution Standard | Applies if AI-assisted contribution is permitted (§0.1 below) | <e.g. 1.1> | <e.g. revision 4, 2026-05-03> |
| Stribog Operational Delivery Standard | Applies / N/A — <one-line rationale, e.g. "no managed-service or rolling-deployment scope"> | <e.g. 1.0 or N/A> | |
| Stribog Security Posture Standard | Applies / N/A per its §0.2 — <one-line rationale> | <e.g. 1.0 or N/A> | |
| Stribog Data and Privacy Standard | Applies / N/A per its §0.2 — <one-line rationale, e.g. "project handles no personal or customer data"> | <e.g. 1.0 or N/A> | |
| Stribog User Documentation Standard | Applies / N/A per its §0.2 — <one-line rationale, e.g. "project ships a CLI consumed by non-engineer operators"> | <e.g. 1.0 or N/A> | <e.g. revision 1, 2026-05-12> |
| Stribog Developer Documentation Standard | Applies / N/A per its §0.2 — <one-line rationale, e.g. "project exposes a public HTTP API"> | <e.g. 1.0 or N/A> | <e.g. revision 1, 2026-05-12> |
| Stribog UI/UX Standard | Applies / N/A per its §0.2 — <one-line rationale, e.g. "project ships a web UI"> | <e.g. 1.0 or N/A> | <e.g. revision 1, 2026-05-12> |
| Stribog Glossary | Applies (cross-document terminology reference) | <e.g. 1.2> | <e.g. revision 3, 2026-05-12> |
| Charter Governance | Applies (binds every Stribog project's compliance posture) | <e.g. 1.3> | <e.g. revision 5, 2026-05-12> |

## 0.1 Project Posture

| Property | Value |
|----------|-------|
| Project type | <e.g. Go CLI tool / Python library / managed-service engagement / infrastructure-as-code / mixed> |
| Compliance tier (Engineering Charter §0.5) | <Foundation / Working / Reference> |
| Tier rationale | <one-line: why this tier was chosen, especially when not Reference> |
| Promotion criteria (if Working tier) | <conditions under which this project would be promoted to Reference tier> |
| Primary language(s) | <e.g. Go 1.25+, Bash, YAML> |
| Delivery model | <versioned releases / rolling deployment / managed service / one-off project> |
| Public or private | <public / private / mixed> |
| Operational scope | <none / limited / primary> |
| AI-assisted contribution | <yes / no / limited> |
| Security Posture Standard binds | <yes / no — per Stribog Security Posture Standard §0.2> |
| Data and Privacy Standard binds | <yes / no — per Stribog Data and Privacy Standard §0.2> |

## 1. Toolchain

*The concrete tools that implement the charter gates and conventions. The universal charter names principles; this section names the implementations. A change to any of these is a governance change per Charter Governance §7.*

### 1.1 Build, Test, and Quality Gates

| Gate (Charter §5.9) | Tool | Command |
|---------------------|------|---------|
| Format | <e.g. gofmt + goimports> | `make format` |
| Lint | <e.g. golangci-lint> | `make lint` |
| Static analysis | <e.g. go vet> | `make vet` |
| Test | <e.g. go test ./...> | `make test` |
| Coverage | <e.g. go test -coverprofile> | `make coverage` |
| Secrets scan | <e.g. gitleaks> | `make secrets` |
| Vulnerability scan | <e.g. govulncheck> | `make vuln` |
| Build | <e.g. go build> | `make build` |
| All-up | combined | `make all` |

### 1.2 Repository Command Surface

The named entrypoint for this project's command surface is: `<e.g. Makefile / justfile / taskfile>`.

The entrypoint exposes, at minimum: `format`, `lint`, `test`, `coverage`, `build`, `vulnerability`, `all`.

### 1.3 Coverage Boundary

| Property | Value |
|----------|-------|
| Coverage floor (Charter §5.4) | 96% |
| Project-declared floor (≥ 96%) | <e.g. 96% / 94% (waivered)> |
| Per-package floor for critical paths | <e.g. 98% for `internal/security/`> |
| Measurement boundary | <e.g. all `internal/` and `cmd/` packages, excluding generated code under `internal/proto/gen/`> |
| Excluded paths and rationale | <e.g. `internal/proto/gen/` — generated by buf, not hand-maintained> |

### 1.4 Test Layers

| Layer | Tool / Pattern | Notes |
|-------|----------------|-------|
| Unit | <e.g. table-driven Go tests> | |
| Contract | <e.g. test/integration/contract_test.go iterating registered impls> | |
| Golden | <e.g. test/golden/...> | |
| Integration | <e.g. test/integration/...> | |
| End-to-end | <e.g. Bats + Kind cluster> | |
| Benchmark | <e.g. go test -bench / criterion / pytest-benchmark> | |

### 1.5 Local Hooks

| Hook | Implementation | Bootstrap |
|------|----------------|-----------|
| Pre-commit secrets scan | <e.g. .githooks/pre-commit running gitleaks> | `make hooks-install` |
| Pre-push test | <e.g. optional> | |

## 2. Documentation

### 2.1 Document Locations

| Document | Path |
|----------|------|
| Master reference | <e.g. docs/internal/ARCHITECTURE-REFERENCE.md> |
| Architecture supplements | <e.g. docs/internal/architecture/> |
| Build plan | <e.g. docs/internal/BUILD-PLAN.md> |
| ADRs | <e.g. docs/internal/adr/> |
| Audit closeouts | <e.g. docs/internal/audits/> |
| Runbooks | <e.g. docs/internal/runbooks/> |
| Testing strategy | <e.g. docs/internal/testing-strategy.md> |
| Local agent rules | <e.g. CLAUDE.md, AGENTS.md> |
| Waiver register | <e.g. docs/internal/WAIVERS.md> |

### 2.2 Diagram Source

| Property | Value |
|----------|-------|
| Diagram language | D2 |
| D2 source path | <e.g. docs/internal/diagrams/src/> |
| Rendered output path | <e.g. docs/internal/diagrams/rendered/> |
| Rendered formats | <e.g. SVG and PNG> |

### 2.3 Public Trust Surface (if applicable)

| Surface | Status |
|---------|--------|
| README | <e.g. accurate as of revision N> |
| Badges | <e.g. CI, coverage, license, release> |
| LICENSE | <e.g. Apache-2.0> |
| SECURITY.md | <e.g. private disclosure via …> |
| CODEOWNERS | <e.g. present, names current> |
| PR template | <e.g. .github/pull_request_template.md> |
| Issue templates | <e.g. .github/ISSUE_TEMPLATE/> |

### 2.4 User-Facing Documentation (if [[Stribog User Documentation Standard]] applies)

| Property | Value |
|----------|-------|
| User-doc owner | <name or team> |
| Active audience tiers (User-Doc §2) | <e.g. end-user, operator, integrator> |
| Quickstart location | <e.g. docs/user/quickstart.md> |
| How-to library location | <e.g. docs/user/how-to/> |
| User reference location | <e.g. docs/user/reference/> |
| Explanations location | <e.g. docs/user/concepts/> |
| Troubleshooting + FAQ location | <e.g. docs/user/troubleshooting/> |
| User-facing release notes location | <e.g. docs/user/releases/> |
| Support escalation map | <e.g. docs/user/support.md> |
| In-product strings catalogue | <e.g. src/i18n/en/strings.json + tooling to export> |
| Source language | <e.g. en-US> |
| Shipped locales | <e.g. en-US, ja-JP> |
| Maintained locales | <e.g. en-US, ja-JP — declared maintained at translation cadence> |
| Translation pipeline | <e.g. Lokalise → human reviewer → fallback to source on miss> |
| Doc site hosting target | <e.g. docs.example.com> |
| Doc-to-release sync gate command | <e.g. `make doc-gate` (User-Doc §11.1)> |
| Doc accessibility command | <e.g. `make doc-a11y` per User-Doc §8.4> |

### 2.5 Developer-Facing Documentation (if [[Stribog Developer Documentation Standard]] applies)

| Property | Value |
|----------|-------|
| Developer-doc owner | <name or team> |
| Active audience tiers (Dev-Doc §2) | <e.g. contributor, consumer, extender> |
| README path | <e.g. README.md> |
| CONTRIBUTING path | <e.g. CONTRIBUTING.md> |
| Dev-environment bootstrap path | <e.g. docs/dev/bootstrap.md> |
| Onboarding budget (Dev-Doc §3.2) | <e.g. 7 commands to green smoke check> |
| Architecture-for-contributors path | <e.g. docs/dev/architecture.md> |
| ADR index path | <e.g. docs/internal/adr/README.md> |
| Public surface map path | <e.g. docs/dev/public-surface.md> |
| Deprecation register path | <e.g. docs/dev/deprecations.md> |
| Compatibility window | <e.g. one major version + one minor version> |
| API reference generator | <e.g. spectacular for OpenAPI, godoc, typedoc> |
| SDK reference generator(s) per language | <e.g. godoc, rustdoc, typedoc> |
| Schema reference generator | <e.g. buf for Protobuf> |
| Sample-test runner | <e.g. `make doc-samples-test`> |
| Drift-gate command | <e.g. `make doc-drift-gate`> |
| Reference hosting target | <e.g. docs.example.com/api/v1> |
| Deprecation announcement channel | <e.g. release notes + developer mailing list> |
| Migration document path (major versions) | <e.g. docs/dev/migrations/> |

### 2.6 UI/UX Surface (if [[Stribog UI/UX Standard]] applies)

| Property | Value |
|----------|-------|
| Design owner | <name or team> |
| Design system / component library | <e.g. internal @example/ui-kit v3.2 / external Radix UI / Material> |
| Token registry source | <e.g. tokens/tokens.json — Style Dictionary> |
| Token drift-gate command | <e.g. `make ui-token-gate`> |
| Theme set | <e.g. light, dark> |
| Supported viewports | <e.g. 360-1920 width> |
| Supported device classes | <e.g. modern evergreen browsers; iOS 17+; Android 14+> |
| Supported direction set | <e.g. LTR; RTL via ar-SA when locale set extends> |
| Locale set (shipped) | <e.g. en-US> |
| Locale set (maintained) | <e.g. en-US> |
| Voice charter | <path or inline declaration of voice rules per UI/UX §6.1> |
| Accessibility floor | <e.g. WCAG 2.2 AA (UI/UX §4.1); regulated surfaces declare higher floor here> |
| Screen-reader test platform(s) | <e.g. VoiceOver / macOS Safari; NVDA / Windows Firefox> |
| Visual regression toolchain | <e.g. Chromatic, Percy, Playwright snapshots> |
| Automated a11y toolchain | <e.g. axe-core via @axe-core/playwright> |
| Manual a11y pass cadence | <e.g. every release on the journey set in this annex> |
| Performance budget targets (per UI/UX §10) | <e.g. LCP ≤ 2.5s @ p75; CLS ≤ 0.1; INP ≤ 200ms; JS ≤ 250KB gz; CSS ≤ 60KB gz> |
| Performance budget command | <e.g. `make ui-perf-gate`> |
| Continuous-perf measurement source | <e.g. RUM via NetBeacon; CrUX> |
| Telemetry event registry path | <e.g. src/telemetry/registry.yaml> |
| Telemetry pipeline | <e.g. consent-gated dispatch via @example/telemetry-sdk to first-party collector> |
| Third-party scripts declared | <e.g. none / list> |
| Reduced-motion policy | <e.g. honored via `prefers-reduced-motion`; essential motion declared per component> |
| Design review gate convening | <e.g. weekly design review, sign-off recorded in linear issue> |

#### 2.6.1 Token Layering (UI/UX §2.2)

| Property | Value |
|----------|-------|
| Primitive token source | <e.g. tokens/primitive/*.json — DTCG format> |
| Semantic token source | <e.g. tokens/semantic/*.json> |
| Component token source | <e.g. tokens/component/*.json — optional> |
| Cross-layer drift-gate command | <e.g. `make ui-layer-gate` — fails on a screen referencing a primitive> |
| Token build pipeline | <e.g. Style Dictionary → web / iOS / Android outputs> |

#### 2.6.2 Color Palette (UI/UX §2.9)

| Property | Value |
|----------|-------|
| Color space | <e.g. OKLCH / OKLab / LCH> |
| Palette topology | <brand hues, neutral axis, semantic set, accent set, surface axis> |
| Step density per hue | <e.g. 50, 100, 200, ..., 950> |
| Contrast verification command | <e.g. `make ui-contrast-gate`> |
| CVD verification command | <e.g. `make ui-cvd-check`> |
| Color harmony rule | <e.g. analogous + accent triad — declared per brand> |

#### 2.6.3 Spacing and Baseline (UI/UX §2.10)

| Property | Value |
|----------|-------|
| Spacing scale | <e.g. 4 / 8 / 12 / 16 / 24 / 32 / 48 / 64> |
| Baseline grid | <e.g. 4px baseline; line-heights and inter-block spacing are multiples> |
| Density multipliers | <e.g. compact 0.75; comfortable 1.0; spacious 1.25> |

#### 2.6.4 Theme System (UI/UX §2.11)

| Property | Value |
|----------|-------|
| Shipped themes | <e.g. light, dark, high-contrast> |
| OS-following | <e.g. follows `prefers-color-scheme` by default; per-user override> |
| Accent customization | <e.g. tenant accent via bounded semantic-token override + contrast verification> |
| Theme switcher surface | <e.g. user preferences area, keyboard reachable> |

#### 2.6.5 Visual Polish (UI/UX §2.12)

| Property | Value |
|----------|-------|
| Polish-pass checklist path | <e.g. docs/ui/polish-checklist.md> |
| Polish-pass owner | <name or team> |
| Polish-pass cadence | <e.g. per release for changed surfaces> |
| Type-rendering rules | <e.g. variable font axes; tabular figures in tables; no faux bold> |
| Elevation token catalogue | <e.g. e0, e1, e2, e3, e4 — dark-theme overlays declared> |

#### 2.6.6 Information Architecture (UI/UX §8)

| Property | Value |
|----------|-------|
| IA contract path | <e.g. docs/ui/ia-contract.md> |
| Top-level surfaces | <enumerated list> |
| URL design rules | <e.g. mirrors IA; no GUID paths; redirects tracked in dev-doc deprecation register> |
| Navigation pattern(s) | <e.g. top-nav + drawer sub-nav> |
| Sitemap source | <e.g. generated from route table at build> |

#### 2.6.7 Forms Pipeline (UI/UX §9)

| Property | Value |
|----------|-------|
| Form library | <e.g. internal @example/forms; or react-hook-form + Zod> |
| Default validation timing | <e.g. on-blur; live for password strength only> |
| Autosave interval | <e.g. 10s for long-form input; not applied to dialogs> |
| Idempotency-key strategy | <e.g. UUIDv7 per submit, sent as `Idempotency-Key` header> |
| Unsaved-changes prompt | <e.g. browser-native + custom on route change> |

#### 2.6.8 Notifications Surface (UI/UX §10)

| Property | Value |
|----------|-------|
| Notification library | <e.g. internal @example/notify> |
| Live-region scopes | <enumerated list with per-scope purpose> |
| Auto-dismiss duration formula | <e.g. floor 4s + 50ms/word; ceiling 10s> |
| System-notifications permission rationale path | <e.g. docs/ui/notifications-rationale.md> |
| Notification center location | <e.g. top-right header drawer> |

#### 2.6.9 Authentication and Session (UI/UX §11)

| Property | Value |
|----------|-------|
| Idle-timeout duration | <e.g. 30 minutes> |
| Idle-warning lead time | <e.g. 2 minutes before timeout> |
| MFA / passkey set | <e.g. WebAuthn passkey + TOTP fallback> |
| Account-switching surface | <e.g. user-menu top-level> |
| OAuth providers | <e.g. Google, GitHub> |
| Sign-out propagation | <e.g. revokes refresh token + clears local cache> |

#### 2.6.10 Data Presentation Toolchain (UI/UX §12)

| Property | Value |
|----------|-------|
| Table / data-grid library | <e.g. internal @example/grid; or TanStack Table> |
| Virtualization threshold | <e.g. 200 rows> |
| Chart library | <e.g. internal; or D3 / Recharts / Vega — names accessibility plugin> |
| Export formats | <e.g. CSV, JSON, PDF — declared per surface> |

#### 2.6.11 Modality and Direct Manipulation (UI/UX §13)

| Property | Value |
|----------|-------|
| Modal library | <e.g. internal @example/dialog using Radix Dialog primitive> |
| Maximum nested-modal depth | <e.g. 1 (no nested modals)> |
| Drag-and-drop library | <e.g. internal; or @dnd-kit — names keyboard adapter> |

#### 2.6.12 Real-Time and Collaboration (UI/UX §14)

| Property | Value |
|----------|-------|
| Real-time transport | <e.g. websocket via @example/sync; SSE; polling> |
| Presence pipeline | <e.g. presence on shared surfaces only, debounced 10s> |
| Conflict-resolution strategy | <e.g. manual merge UI per §14.4 for declared collaborative surfaces> |

#### 2.6.13 AI Rendering Pipeline (UI/UX §15)

| Property | Value |
|----------|-------|
| Streaming surface | <e.g. /chat — token-by-token via SSE> |
| Live-region announcement scope | <e.g. response-in-progress + final-output only; per-token forbidden> |
| Citation pipeline | <e.g. retrieved chunks → click-through with source path> |
| Refusal taxonomy | <e.g. policy, low-confidence, insufficient-context — each with named rendering> |
| AI-content disclosure | <e.g. visible footer "Generated by Stribog Assistant" + per-message indicator> |
| Tool-use rendering | <e.g. expandable trace of tool invocations + inputs + outputs> |

#### 2.6.14 Offline Strategy (UI/UX §17)

| Property | Value |
|----------|-------|
| Offline detection | <e.g. service-worker fetch failures + navigator.onLine + heartbeat> |
| Write-queue persistence | <e.g. IndexedDB store + outbox table> |
| Replay strategy | <e.g. FIFO with idempotency-key; conflict surfaces UI per §14.4> |
| Sync indicator location | <e.g. surface-header sync status> |
| Service-worker update UX | <e.g. banner "new version available" + reload action> |

#### 2.6.15 Onboarding Sequence (UI/UX §18)

| Property | Value |
|----------|-------|
| Onboarding step count budget | <e.g. ≤ 5 steps to aha moment> |
| Aha moment definition | <project-specific — declared per surface> |
| Sample data set | <e.g. /fixtures/sample-org.json> |
| Reactivation threshold | <e.g. 30 days idle triggers re-onboarding shortcut> |

#### 2.6.16 Embedded and Adjacent Surfaces (UI/UX §19, §20)

| Property | Value |
|----------|-------|
| Embed surfaces (Stribog inside host) | <enumerated> |
| Third-party embeds in Stribog | <e.g. Stripe Elements (payment), Mapbox (map) — each with consent posture + perf budget contribution> |
| iframe sandbox defaults | <e.g. `sandbox="allow-scripts allow-same-origin"` minimum per surface> |
| postMessage origin allowlist | <enumerated> |
| Email template library | <e.g. MJML compiled with @example/email-build> |
| PDF accessibility floor | <e.g. PDF/UA-1> |
| Print stylesheet entry | <e.g. src/styles/print.css> |

#### 2.6.17 UI Security Configuration (UI/UX §21)

| Property | Value |
|----------|-------|
| Content Security Policy | <full policy or path to source of truth> |
| CSP violation collector | <e.g. /csp-report endpoint> |
| Frame-ancestors policy | <e.g. `frame-ancestors 'none'` or named allowlist> |
| Subresource Integrity coverage | <e.g. all external scripts + stylesheets> |
| Browser-storage inventory | <enumerated keys + sensitivity> |
| Masking policy | <e.g. last-four-digits for card; full-mask for SSN> |

#### 2.6.18 Native Platform Conventions (UI/UX §22)

| Property | Value |
|----------|-------|
| Native targets | <e.g. iOS 17+, Android 14+ — or N/A for web-only> |
| HIG-following declarations | <e.g. iOS share sheet, Android back-gesture, macOS menu bar> |
| Cross-platform divergence allowlist | <surface-by-surface — declared> |

#### 2.6.19 Latency Budgets (UI/UX §25.8)

| Class | Budget (declared per project) |
|-------|------------------------------|
| Input-to-paint (button press / key press) | <e.g. ≤ 100ms p95> |
| Hover / pointer-move feedback | <e.g. ≤ 16ms> |
| Drag tracking | <e.g. ≤ 16ms p95> |
| Scroll | <e.g. sustained 60Hz> |
| Page transition | <e.g. ≤ 200ms perceived> |
| Modal open | <e.g. ≤ 100ms> |
| Tooltip / popover open | <e.g. ≤ 50ms after hover-intent threshold> |
| Form-validation feedback | <e.g. ≤ 200ms after debounce> |
| Search-as-you-type response | <e.g. ≤ 150ms for cached results> |

#### 2.6.20 Easing and Motion Curves (UI/UX §27.7)

| Property | Value |
|----------|-------|
| Easing curve catalogue path | <e.g. tokens/motion/easing.json> |
| Hover-intent delay | <e.g. 150ms> |
| Stagger interval | <e.g. 50ms> |
| Haptic event list | <enumerated trigger → haptic mapping for native targets> |

#### 2.6.21 Testing Toolchain (UI/UX §24.11)

| Layer | Tool + invocation |
|-------|-------------------|
| Unit | <e.g. Vitest — `make ui-test-unit`> |
| Integration | <e.g. Testing Library — `make ui-test-integ`> |
| Visual regression | <e.g. Chromatic — `make ui-test-vr`> |
| Automated a11y | <e.g. axe-core in Playwright — `make ui-test-a11y`> |
| End-to-end | <e.g. Playwright — `make ui-test-e2e`> |
| Offline acceptance | <e.g. service-worker harness — `make ui-test-offline`> |
| Real-time conflict | <e.g. multi-client harness — `make ui-test-rt`> |
| Streaming a11y | <e.g. live-region inspector — `make ui-test-stream`> |
| Performance budget | <e.g. Lighthouse CI — `make ui-perf-gate`> |
| Polish pass | <recorded checklist run by named human> |
| Manual design QA | <recorded session log path> |
| Cross-device | <e.g. BrowserStack / device lab> |

## 3. Git, History, and Attribution

| Property | Value |
|----------|-------|
| Primary branch | <main / master> |
| Branch model | <trunk-based, feature branches, squash merge> |
| Branch protection | <enabled / not applicable for single-maintainer repo> |
| Required CI checks | <list> |
| Linear history | <yes / no> |
| Signed commits | <yes / where supported> |
| Git identity | <e.g. 25719166+msambare@users.noreply.github.com> |
| AI attribution convention | <e.g. `Co-authored-by: Claude <noreply@anthropic.com>` trailer on AI-assisted commits> |
| Conventional Commits | <yes — types: feat, fix, docs, chore, ci, test, perf> |

## 4. AI Agent Posture

| Property | Value |
|----------|-------|
| AI-assisted contribution permitted | <yes / no / limited> |
| Permitted agent harnesses | <e.g. Claude Code, Codex, OpenCode, Goose> |
| Default synthesis-tier model | <e.g. Claude Opus class> |
| Default coding-tier model | <e.g. Claude Sonnet class> |
| Default extraction-tier model | <e.g. Qwen3-4B-Instruct (local)> |
| Default critique-tier model | <e.g. Claude Opus / Devil's Advocate persona> |
| Local-first preference | <yes / no — describe routing> |
| Closeout evidence location | <e.g. commit message body, beads issue, PR description> |
| Memory tooling | <e.g. claude-mem, context-mode, beads> |
| Multi-agent orchestration | <e.g. Superset / not used> |

## 5. Operational Posture (if applicable)

*Skip this section if the project has no operational scope. For projects with operational character, this section is binding alongside the Stribog Operational Delivery Standard.*

| Property | Value |
|----------|-------|
| Service tier | <Critical / Standard / Background> |
| Source-of-truth for configuration | <e.g. Ansible repo, Kubernetes manifests, Terraform> |
| Drift detection | <tool, cadence> |
| Secret store | <e.g. 1Password / Bitwarden / Vault> |
| Monitoring stack | <e.g. Wazuh, Prometheus, Grafana, Uptime Kuma> |
| Alert respondent | <named operator + medium> |
| Incident severity vocabulary | <Sev-1 / Sev-2 / Sev-3 / Sev-4 default, or local subdivision> |
| Customer comms policy | <if applicable> |
| Change record system | <e.g. beads / ticket system / change log> |
| Change windows | <if customer-imposed; otherwise none> |
| Backup posture | <what, where, cadence, restoration drill cadence> |
| RPO / RTO per tier | <e.g. RPO 1h / RTO 4h for Critical> |

## 6. Migration and Sunset

### 6.1 Charter Migration History

| Date | From | To | Notes |
|------|------|----|-------|
| YYYY-MM-DD | <prior pin> | <new pin> | <one-line rationale> |

### 6.2 Migration Cadence

*The intended cadence at which this project migrates to newer `MAJOR` charter versions. Some projects move at every `MAJOR`; some pin long-term and migrate only on a schedule.*

<Migration cadence and rationale.>

### 6.3 Sunset

*If this project has a planned end-of-life, name it. Most projects do not, but managed-service engagements typically do.*

<Sunset posture or "no planned sunset.">

## 7. Active Waivers

*Summary of currently active waivers against any charter clause. The full waiver records live in the waiver register (§2.1); this section is the at-a-glance summary.*

| Waiver ID | Clause | Scope | Owner | Expiry |
|-----------|--------|-------|-------|--------|
| W001 | <e.g. Charter §5.4 — coverage floor> | <e.g. cmd/ subpackage> | <owner> | <YYYY-MM-DD> |
| ... | | | | |

If empty: *No active waivers as of revision N.*

## 8. Annex Review Cadence

| Trigger | Action |
|---------|--------|
| MAJOR version bump of any pinned governing document | Review and update §0 pins; consider migration |
| Project phase boundary | Full annex review |
| Charter audit round | Review per Charter Governance §8 |
| Toolchain change | Update §1; bump revision |
| Project posture change | Update §0.1; bump revision |

The annex is reviewed at minimum quarterly even in the absence of triggering events.

---

## §A. Reference Fill — Go Service Project (security-relevant CLI)

*This is an example fill for a Go service project — modeled after a KubeVigil-shaped repository (public Go CLI tool with MCP server, security-relevant scope, not customer-facing infrastructure). It is kept in the template as a worked example until the project's actual annex content replaces it. Pins are to the v1.2.0 canon.*

```yaml
# §0 — Charter Pins
Universal Stribog Engineering Charter: 1.2 (revision 7, 2026-05-12)
Stribog Documentation Standard: 2.1 (revision 6, 2026-05-12)
Stribog AI Agent Execution Standard: 1.1 (revision 4, 2026-05-03)
Stribog Operational Delivery Standard: not applicable (CLI tool, no managed-service component)
Stribog Security Posture Standard: 1.0 (revision 2, 2026-05-03) — APPLIES (security-relevant tool, scans untrusted manifests)
Stribog Data and Privacy Standard: not applicable (no PII processing; manifest scan input is not personal data)
Stribog User Documentation Standard: 1.0 (revision 1, 2026-05-12) — APPLIES (operators consume the CLI and read MCP integration docs)
Stribog Developer Documentation Standard: 1.0 (revision 1, 2026-05-12) — APPLIES (public Go API + MCP surface consumed by external integrators and contributors)
Stribog UI/UX Standard: not applicable (line-oriented CLI per UI/UX §0.2; governed by User Doc §7 and Eng Charter §3.3 instead)
Stribog Glossary: 1.3 (revision 4, 2026-05-12) — authoritative for cross-document terms
Charter Governance: 1.3 (revision 6, 2026-05-12)

# §0.1 — Project Posture
Project type: Go CLI + MCP server, public OSS, security-relevant
Compliance tier: Reference (public, security-sensitive — Engineering Charter §0.5)
Tier rationale: public-facing security tool; customer trust depends on the canon applied in full
Primary language: Go 1.25+
Delivery model: tagged releases via GoReleaser
Public or private: public (Apache-2.0)
Operational scope: none (CLI only — Operational Delivery Standard does not apply)
AI-assisted contribution: yes, with Co-authored-by attribution
```

```makefile
# §1.1 — gate implementations
format:    gofmt -w . && goimports -w .
lint:      golangci-lint run
vet:       go vet ./...
test:      go test -race ./...
coverage:  go test -race -coverprofile=coverage.out ./... && go tool cover -func=coverage.out
secrets:   gitleaks detect --source . --redact
vuln:      govulncheck ./...
build:     go build -o bin/<binary> ./cmd/<binary>
all:       format lint vet test coverage secrets vuln build
```

```yaml
# §1.3 — Coverage Boundary
Coverage floor (charter mandate): 96%
Project-declared floor: 96%
Per-package floor for critical paths: 98% for internal/security/
Measurement boundary: internal/ + cmd/, excluding internal/proto/gen/
Excluded: internal/proto/gen/ (buf-generated, not hand-maintained)
```

```yaml
# §3 — Git, History, Attribution
Primary branch: master
Branch model: trunk-based, squash-merge
Branch protection: enabled (CODEOWNERS + required CI + linear history + signed commits)
Git identity: 25719166+msambare@users.noreply.github.com
AI attribution: Co-authored-by: Claude <noreply@anthropic.com>
Conventional Commits: yes — feat, fix, docs, chore, ci, test, perf
```

```yaml
# §2.4 — User-Facing Documentation
User-doc owner: maintainers (CODEOWNERS @msambare)
Active audience tiers: operator, integrator, evaluator (per User-Doc §2)
Quickstart location: docs/user/quickstart.md
How-to library location: docs/user/how-to/
User reference location: docs/user/reference/ (generated from --help + MCP introspection)
Explanations location: docs/user/concepts/ (e.g. why-checks-not-rules.md)
Troubleshooting + FAQ: docs/user/troubleshooting/
User-facing release notes: docs/user/releases/ (per tag) + GitHub Releases mirror
Support escalation map: docs/user/support.md (GitHub issues → maintainer DM for security)
In-product strings catalogue: internal/i18n/en/strings.go + `make strings-export`
Source language: en-US
Shipped locales: en-US
Maintained locales: en-US (no localization scope declared; project is en-US only)
Doc site hosting target: github.com/<org>/<repo> README + docs/ (no separate site)
Doc-to-release sync gate command: make doc-gate
Doc accessibility command: make doc-a11y (markdown alt-text + heading-structure check)

# §2.5 — Developer-Facing Documentation
Developer-doc owner: maintainers (CODEOWNERS @msambare)
Active audience tiers: contributor, consumer, embedder, extender
README path: README.md
CONTRIBUTING path: CONTRIBUTING.md
Dev-env bootstrap path: docs/dev/bootstrap.md
Onboarding budget: ≤ 6 commands to green smoke check (clone, go version check, make all, make smoke)
Architecture-for-contributors: docs/dev/architecture.md
ADR index path: docs/internal/adr/README.md
Public surface map path: docs/dev/public-surface.md (enumerated symbols + MCP tools + flags)
Deprecation register path: docs/dev/deprecations.md
Compatibility window: one minor version + one patch — declared in SECURITY.md alongside support window
API reference generator: godoc + buf for protobuf MCP surface
SDK reference generator(s): N/A (no SDK ships; the binary is the consumer interface)
Schema reference generator: buf generate → docs/dev/proto.md (Protobuf MCP surface)
Sample-test runner: make doc-samples-test (go test on examples/ — every README snippet runs)
Drift-gate command: make doc-drift-gate (go doc symbol → public-surface.md diff)
Reference hosting target: pkg.go.dev (godoc) + repo docs/
Deprecation announcement channel: release notes + repo Discussions
Migration document path (major versions): docs/dev/migrations/

# §2.6 — UI/UX Surface
Not applicable. Project ships a line-oriented CLI plus an MCP server with JSON tool I/O.
Per UI/UX §0.2 a line-oriented CLI is governed by User-Doc §7 (in-product help) and
Eng Charter §3.3 (thin interface layers), not by UI/UX §3 / §4 / §5 / §25.
The §2.6.1 – §2.6.21 sub-blocks below are omitted with N/A as the declared posture.
```

```yaml
# §7 — Active Waivers (summary; full register at docs/internal/WAIVER-REGISTER.md)
W-0001: Engineering Charter §5.4 (96% coverage) — pre-v1.1.0 codebase at 94%; ratchet plan
        in flight; expiry 2026-08-03; compensating controls: per-package 98% floor for
        security-sensitive packages, contract-test backbone for all 110 checkers.
```

---

## §B. Reference Fill — Infrastructure-Only Managed Service (inherited engagement)

*This is an example fill for an infrastructure-only managed-service engagement: an inherited production fleet, customer-facing, no shipped software product, primary deliverable is operational. Pins are to the v1.2.0 canon.*

```yaml
# §0 — Charter Pins
Universal Stribog Engineering Charter: 1.2 (revision 7, 2026-05-12)
Stribog Documentation Standard: 2.1 (revision 6, 2026-05-12)
Stribog AI Agent Execution Standard: 1.1 (revision 4, 2026-05-03)
Stribog Operational Delivery Standard: 1.1 (revision 4, 2026-05-12)  # PRIMARY for this engagement
Stribog Security Posture Standard: 1.0 (revision 2, 2026-05-03) — APPLIES (production state, customer infrastructure)
Stribog Data and Privacy Standard: 1.0 (revision 3, 2026-05-03) — APPLIES (handles customer operational data; check §0.2 criteria for PII)
Stribog User Documentation Standard: 1.0 (revision 1, 2026-05-12) — APPLIES (customer-facing runbook surface + status page communications)
Stribog Developer Documentation Standard: 1.0 (revision 1, 2026-05-12) — APPLIES (limited; internal contributor surface for configuration-management roles + manifest overlay tool overlays; no public API)
Stribog UI/UX Standard: 1.1 (revision 2, 2026-05-12) — APPLIES (status page + customer portal carry UI surfaces)
Stribog Glossary: 1.3 (revision 4, 2026-05-12)
Charter Governance: 1.3 (revision 6, 2026-05-12)

# §0.1 — Project Posture
Project type: managed infrastructure for <customer>
Compliance tier: Reference (customer-facing, production-stateful — Engineering Charter §0.5)
Tier rationale: customer engagement; production state under management; customer trust requires full canon
Engagement type: INHERITED (Stribog assumed operational responsibility for an existing production fleet, not a greenfield build — Operational Delivery Standard §13.3)
Primary languages: YAML, Bash, Ansible, Helm
Delivery model: rolling deployment, monthly maintenance windows
Public or private: private
Operational scope: PRIMARY (this project IS the operational engagement)
AI-assisted contribution: limited — generation only, never apply to production directly

# §1.1 — gate implementations
format:    yamllint -s + shfmt -d
lint:      ansible-lint, kube-linter, hadolint
test:      infrastructure test harness (Ansible roles); manifest overlay tool build (manifests); kubeconform (manifest schema)
coverage:  N/A — infra repo; manifest validation tracked instead, with KubeVigil scans on every PR
secrets:   gitleaks detect, with .gitleaks.toml allowlisting test fixtures only
vuln:      trivy fs / trivy image (for shipped containers)
build:     N/A — infrastructure-as-code, not built artifacts
all:       combined invocation

# §5 — Operational Posture
Service tier: Critical (customer-facing infrastructure)
Source-of-truth: configuration-management repo + manifest overlay tool overlays in private Git
Drift detection: configuration-drift detection job on schedule, container CLI diff weekly
Secret store: 1Password Business + Kubernetes external-secrets-operator
Monitoring: Wazuh + Uptime Kuma; alerts via PagerDuty to operator
Alert respondent: operator (24x7, phone push)
Incident vocabulary: Sev-1/2/3/4 baseline
Customer comms: status page + email per SLA
Change record system: beads, mirrored to customer ticket
Change windows: Wed 22:00-02:00 <customer-timezone> per customer SLA
Backup: daily Velero + weekly off-site to encrypted S3
RPO / RTO: RPO 24h / RTO 4h for Critical tier
DR drill posture: inherited fleet — first successful drill must occur within the engagement onboarding window per Operational Delivery Standard §13.3; status tracked in waiver register until first drill succeeds
```

```yaml
# §2.4 — User-Facing Documentation
User-doc owner: engagement lead
Active audience tiers: administrator, operator, end-user (status-page consumer)
Quickstart location: N/A — no end-user quickstart (engagement is operational, not a product)
How-to library location: docs/runbooks/customer-self-service/
User reference location: customer portal documentation hub
Explanations location: N/A
Troubleshooting + FAQ: status-page FAQ + customer portal knowledge base
User-facing release notes: status page changelog + monthly customer email
Support escalation map: docs/escalation-map.md (Tier-1 → Tier-2 → engagement lead → on-call)
In-product strings catalogue: status-page i18n/<locale>.json
Source language: en-US
Shipped locales: en-US
Maintained locales: en-US (customer is en-US; localization not in scope)
Doc site hosting target: customer portal subdomain
Doc-to-release sync gate command: pre-deploy-gate (status-page entry must accompany every customer-visible change)
Doc accessibility command: pa11y on status page on schedule

# §2.5 — Developer-Facing Documentation
Developer-doc owner: engagement lead
Active audience tiers: contributor (internal Stribog operators only)
README path: README.md (private repo)
CONTRIBUTING path: CONTRIBUTING.md (internal contributors only)
Dev-env bootstrap path: docs/dev/bootstrap.md (configuration management + container CLI + mesh-VPN auth)
Onboarding budget: ≤ 10 commands to first configuration-drift check (includes vault decrypt)
Architecture-for-contributors: docs/dev/architecture.md (fleet topology + role layout)
ADR index path: docs/adr/README.md
Public surface map path: N/A — no public API surface
Deprecation register path: N/A — no public API surface
Compatibility window: N/A
API reference generator: N/A
SDK reference generator(s): N/A
Schema reference generator: kubeconform schema set declared
Sample-test runner: infrastructure test harness (configuration management) + manifest overlay tool build
Drift-gate command: configuration-drift detection job on schedule (drift to source-of-truth)
Reference hosting target: internal wiki
Deprecation announcement channel: N/A
Migration document path: N/A

# §2.6 — UI/UX Surface
Design owner: engagement lead (works with customer brand team for portal styling)
Design system / component library: customer-owned (Stribog inherits brand assets); status-page UI uses the status-page-vendor's component primitives
Token registry source: status-page vendor token set + Stribog brand overrides at tokens/brand-overrides.json
Token drift-gate command: make ui-token-gate
Theme set: light, dark (follows OS preference; explicit override exposed in portal)
Supported viewports: 360-1920 width; status page primarily mobile-read
Supported device classes: modern evergreen browsers
Supported direction set: LTR
Locale set (shipped): en-US
Locale set (maintained): en-US
Voice charter: docs/ui/voice.md (operations-first register; no marketing voice on operational surfaces)
Accessibility floor: WCAG 2.2 AA
Screen-reader test platform(s): VoiceOver / macOS Safari (status page primary surface)
Visual regression toolchain: Percy on status-page templates
Automated a11y toolchain: pa11y-ci on portal + status page
Manual a11y pass cadence: quarterly + per material UI change
Performance budget targets: status page LCP ≤ 2.0s @ p75; CLS ≤ 0.05; INP ≤ 200ms (status page must be fast under incident traffic)
Performance budget command: make ui-perf-gate
Continuous-perf measurement source: status-page-vendor RUM + Stribog synthetic check every 5min
Telemetry event registry path: docs/ui/telemetry-registry.yaml
Telemetry pipeline: consent-gated dispatch; status-page vendor handles status-page telemetry
Third-party scripts declared: status-page-vendor only
Reduced-motion policy: honored via `prefers-reduced-motion`; status-page animations disabled under reduced motion
Design review gate convening: at incident-comms changes + at customer-portal feature changes

# §2.6.6 — Information Architecture (UI/UX §8)
IA contract path: docs/ui/ia-contract.md
Top-level surfaces: status overview, incident detail, scheduled maintenance, subscribe
URL design rules: stable URLs; incident IDs are slugified-not-GUID; status changes redirect tracked in changelog
Navigation pattern(s): top-nav + incident list

# §2.6.8 — Notifications Surface (UI/UX §10)
Notification library: status-page-vendor templates
Live-region scopes: incident-banner-region only
Auto-dismiss duration formula: N/A (incident banners persist until resolved)
System-notifications permission rationale path: docs/ui/notifications-rationale.md
Notification center location: status page subscribe surface (email, SMS, webhook channels)

# §2.6.17 — UI Security Configuration (UI/UX §21)
Content Security Policy: enforced via status-page vendor; Stribog brand overrides validated for SRI
CSP violation collector: status-page-vendor collector
Frame-ancestors policy: `frame-ancestors 'none'` for portal; allowlist for embedded status snippets on customer site
Subresource Integrity coverage: all customer-portal external scripts + stylesheets
Browser-storage inventory: portal session cookie only (HttpOnly + Secure + SameSite=Strict)
Masking policy: customer-internal infrastructure identifiers masked on status page

# Other §2.6.* sub-blocks (Token Layering, Spacing, Theme System, Visual Polish,
# Forms, Auth/Session, Data Presentation, Modality, Real-Time, AI Rendering,
# Offline, Onboarding, Embedded, Native, Latency, Easing, Testing Toolchain):
# inherit from status-page vendor where the surface is theirs; declared explicitly
# only where Stribog brand or portal contribution diverges.
```

```yaml
# §7 — Active Waivers (summary; full register at WAIVER-REGISTER.md)
W-0001: Operational Delivery Standard §13.3 (first restoration drill before production) —
        inherited fleet was already in production at engagement start; first drill scheduled
        within the 60-day onboarding window; expiry 2026-07-03; compensating controls:
        verified backup restoration on a non-production target, documented restoration
        procedure, customer aware that DR is unverified-by-Stribog until first drill.
```

---

## §C. Reference Fill — Browser-Only Local-First App (client-only, persists Restricted data locally)

*This is an example fill for a browser-only application that persists Restricted-class data on the user's device with no hosted backend — an encrypted local note-taker, a client-side password vault, an on-device medical-record viewer, or an offline-first PWA that uses on-device LLM inference. The product is a single distributable surface (web app or PWA) and the user's device is the only data residency. Pins are to the v1.2.0 canon.*

```yaml
# §0 — Charter Pins
Universal Stribog Engineering Charter: 1.2 (revision 8, 2026-05-12)
Stribog Documentation Standard: 2.1 (revision 6, 2026-05-12)
Stribog AI Agent Execution Standard: 1.1 (revision 5, 2026-05-12)
Stribog Operational Delivery Standard: not applicable (no hosted backend; no managed service)
Stribog Security Posture Standard: 1.0 (revision 2, 2026-05-03) — APPLIES (Restricted data persists on the user's device; client-side crypto is the trust boundary; threat model spans browser sandbox + extension surface + sync layer if any)
Stribog Data and Privacy Standard: 1.0 (revision 3, 2026-05-03) — APPLIES (Restricted-class data persists locally; Stribog is the controller at the point of code authorship and the user is the controller at the point of data entry; the product is the local-processor)
Stribog User Documentation Standard: 1.0 (revision 1, 2026-05-12) — APPLIES (end-user-facing product)
Stribog Developer Documentation Standard: 1.0 (revision 1, 2026-05-12) — APPLIES (public OSS / contributor-facing repository)
Stribog UI/UX Standard: 1.1 (revision 2, 2026-05-12) — APPLIES (full surface; UI/UX is the product's entire externally-observable behavior)
Stribog Glossary: 1.3 (revision 4, 2026-05-12)
Charter Governance: 1.3 (revision 6, 2026-05-12)

# §0.1 — Project Posture
Project type: SPA / PWA, browser-only, no hosted backend
Compliance tier: Reference (handles Restricted user data — Engineering Charter §0.5)
Tier rationale: client-only does not lower the bar; the absence of a server means the client IS the trust boundary
Primary language: TypeScript
Delivery model: tagged releases; single-file or single-bundle artifact served from a static host
Public or private: declared per project (this example: public OSS)
Operational scope: none (no managed service)
Data residency: user's device — IndexedDB / OPFS / localStorage as declared in §0.1-data-storage
Hosted backend: NONE — declared explicitly; any sync feature is end-to-end encrypted with the server as untrusted relay
Telemetry: consent-first per UI/UX §26.1; no PII; on-device aggregation where possible
AI-assisted contribution: yes per agent neutrality (§3 / AI Agent Execution Standard §5)

# §0.1-data-storage — Local Persistence Inventory (security-relevant)
IndexedDB: encrypted at rest using user-derived key; key never persists outside session memory
OPFS (Origin Private File System): used for large attachments; same encryption posture as IndexedDB
localStorage: theme + preferences only; no Restricted data
sessionStorage: ephemeral UI state only
Cookies: none (no server)
Cache API: static assets only; no user data
Sync: optional end-to-end encrypted sync via untrusted relay (when feature is enabled); key never leaves device unencrypted
```

```makefile
# §1.1 — gate implementations
format:    biome format --write . OR prettier --write .
lint:      biome check . OR eslint .
typecheck: tsc --noEmit
test:      vitest run
coverage:  vitest run --coverage
secrets:   gitleaks detect --source . --redact
vuln:      npm audit --omit=dev && socket-cli scan
build:     vite build --mode production
bundle-check: size-limit
sri:       sri-generate dist/  # generate SRI hashes for the shipped artifact
smoke:     playwright test --grep @smoke  # runs the built artifact, not source
all:       format lint typecheck test coverage secrets vuln build bundle-check sri smoke
```

```yaml
# §1.3 — Coverage Boundary
Coverage floor (charter mandate): 96%
Project-declared floor: 96%
Per-package floor for critical paths: 98% for src/crypto/ and src/storage/ (client-side trust boundary)
Measurement boundary: src/ (TypeScript source) — the COVERAGE SUBJECT
Generated artifact NOT measured: dist/ — the artifact IS the product per Eng Charter §5.5 single-file-distributable clause; dist/ is governed by §7.4 release discipline (reproducible build, SRI hash, size budget, smoke test) instead of by coverage and format gates
Excluded from coverage (within src/): src/generated/, src/types/external/
Reason: generated d.ts files and third-party type declarations
```

```yaml
# §2.4 — User-Facing Documentation
User-doc owner: maintainers
Active audience tiers: end-user (primary), administrator (for self-hosted deployments)
Quickstart location: docs/user/quickstart.md
How-to library location: docs/user/how-to/
User reference location: docs/user/reference/
Explanations location: docs/user/concepts/ — especially the on-device-trust model and the key-derivation explanation
Troubleshooting + FAQ: docs/user/troubleshooting/
User-facing release notes: docs/user/releases/
Support escalation map: docs/user/support.md (GitHub issues primary; security via private disclosure)
In-product strings catalogue: src/i18n/<locale>.json
Source language: en-US
Shipped locales: en-US (additional locales declared per release)
Doc site hosting target: GitHub Pages / Cloudflare Pages — single-page static
Doc-to-release sync gate command: make doc-gate

# §2.5 — Developer-Facing Documentation
Developer-doc owner: maintainers
Active audience tiers: contributor, integrator (if extension API ships), evaluator
README path: README.md
CONTRIBUTING path: CONTRIBUTING.md
Dev-env bootstrap path: docs/dev/bootstrap.md (Node version, pnpm, browser test runners)
Onboarding budget: ≤ 5 commands (clone, pnpm install, pnpm dev, pnpm test, pnpm build)
Architecture-for-contributors: docs/dev/architecture.md (client-only architecture, encryption flow, storage layer)
ADR index path: docs/internal/adr/README.md
Public surface map path: docs/dev/public-surface.md (if extension API ships; otherwise N/A)
Deprecation register path: docs/dev/deprecations.md
Compatibility window: per-major; data-format migrations carry test fixtures
API reference generator: typedoc
Sample-test runner: make doc-samples-test
Drift-gate command: make doc-drift-gate
Reference hosting target: same static host as user docs

# §2.6 — UI/UX Surface (full applicability — UI/UX is the entire product)
Design owner: maintainers
Design system / component library: e.g. internal kit on Radix primitives
Token registry source: tokens/tokens.json — DTCG format
Token drift-gate command: make ui-token-gate
Theme set: light, dark, high-contrast
Supported viewports: 320-1920 width (mobile-first; product runs on phones)
Supported device classes: modern evergreen browsers; iOS 17+ Safari; Android 14+ Chrome
Supported direction set: LTR; RTL declared per locale
Locale set (shipped): en-US
Locale set (maintained): en-US
Voice charter: docs/ui/voice.md (neutral register; trust-explaining over selling)
Accessibility floor: WCAG 2.2 AA
Screen-reader test platform(s): VoiceOver / iOS Safari + NVDA / Windows Firefox
Visual regression toolchain: Playwright snapshots
Automated a11y toolchain: axe-core via @axe-core/playwright
Manual a11y pass cadence: every release
Performance budget targets:
  - LCP ≤ 1.5s @ p75 (no server round-trip; should be fast)
  - CLS ≤ 0.1
  - INP ≤ 200ms
  - Total bundle weight ≤ 300KB gzipped (single-file artifact)
  - Time-to-first-decrypt ≤ 500ms after key entry
Performance budget command: make ui-perf-gate
Continuous-perf measurement source: consented opt-in RUM only
Telemetry event registry path: src/telemetry/registry.yaml
Telemetry pipeline: on-device aggregation; emits only after consent; no PII; no device fingerprint
Third-party scripts declared: NONE (zero third-party scripts; CSP enforces)
Reduced-motion policy: honored
Design review gate convening: per material UI change

# §2.6.14 — Offline Strategy (UI/UX §17 — central to design for this class)
Offline detection: service worker + navigator.onLine + heartbeat (heartbeat only if sync feature enabled)
Write-queue persistence: IndexedDB outbox table; encrypted with same key as primary store
Replay strategy: FIFO with idempotency-key on optional sync; conflict-resolution UI per UI/UX §14.4
Sync indicator location: top-right header (when sync feature enabled)
Service-worker update UX: banner "new version available" + reload action; offline writes preserved across update

# §2.6.17 — UI Security Configuration (UI/UX §21 — central to design for this class)
Content Security Policy: strict — `default-src 'self'; script-src 'self'; style-src 'self'; img-src 'self' data:; connect-src 'self' <sync-relay-if-any>; object-src 'none'; frame-ancestors 'none'; upgrade-insecure-requests`
CSP violation collector: declared per project (may be opt-in on-device aggregator only)
Frame-ancestors policy: 'none' — product is not embeddable
Subresource Integrity coverage: all assets (single-bundle artifact; SRI for each cached resource)
Browser-storage inventory: IndexedDB (encrypted), OPFS (encrypted), localStorage (preferences only); cookies forbidden
Masking policy: passwords + recovery codes auto-clear from clipboard per UI/UX §21.6
Copy-to-clipboard auto-clear duration: 30 seconds for sensitive values
Key derivation: Argon2id or scrypt with declared parameters; key never persists outside session memory

# §3 — Git, History, Attribution
Primary branch: main
Branch model: trunk-based
Git identity: <github-noreply-address>
AI attribution convention: provider-neutral Co-authored-by trailer per AI Agent Execution Standard §5.1
Allowed agent trailers: Claude, Codex, Copilot, Gemini, local-llama, and any future harness declared in this annex
Conventional Commits: yes

# §5 — Operational Posture
Not applicable. Project ships no managed service. Engagement-level operational concerns
(monitoring, on-call, incident response, DR) do not apply at the product layer.
Static hosting of the artifact is the only ops-adjacent activity, governed by §7.4
release discipline for the single-file distributable.

# §7 — Active Waivers (summary)
W-0001: Engineering Charter §3.5 Safety by Design — mutation-safety guard pattern
        does not apply because mutations are on the user's own device only; no
        production state to protect. Compensating control: backup-and-restore UI
        affordance gives the user direct rollback capability.
W-0002: Stribog Data and Privacy Standard §11 Privacy Audit — third-party privacy
        audit not yet performed; client-only architecture inherently limits exposure.
        Self-audit recorded; expiry 2026-12-01 by which time external audit completes.
```

---

## Template Revision History

*This section governs the template itself, not Annex instances. Instance Annexes carry their own revision history under §8 (added during instance filing).*

| Version | Revision | Date | Change |
|---------|----------|------|--------|
| 1.0.0 | 1 | 2026-05-03 | Initial governing-reference release. Defined the Charter Compliance Annex contract: charter pins, project posture, toolchain, documentation locations, AI agent posture, operational posture, migration history, active waivers, review cadence. Two reference fills shipped (§A — Go service, §B — infra-only managed service). |
| 1.0.0 | 2 | 2026-05-03 | Editorial revision applied during Charter Set Audit Round 3 closeout. §0 Charter Pins table restructured: split the conflated "Pinned Version" column into separate `Applicability` and `Pinned Version` columns, so standards that do not apply are explicitly recorded as **N/A** with rationale rather than overloaded into a single cell. Updated §0 prose to reflect the post-F33 doc-SemVer model (no `PATCH` for documents; revision-only editorial updates flow through automatically within the same `MAJOR.MINOR`). Front-matter `related_docs` extended with [[Stribog-Security-Posture-Standard]], [[Stribog-Data-and-Privacy-Standard]], and [[Stribog-Glossary]], all of which are referenced from §0 of this template. Added this Template Revision History section. Closes Round 3 findings F43 (Pinned-Version vs Not-applicable conflation in §0) and F44 (Annex template `related_docs` missing Security, Privacy, Glossary). No normative change to the Annex contract.
| 1.0.0 | 3 | 2026-05-03 | Editorial revision applied during Charter Set Audit Round 5 closeout. §0 Charter Pins example version values updated to reflect the v2.0.0 Documentation Standard release: Stribog Documentation Standard `<e.g. 1.2>` → `<e.g. 2.0>` (rev 3 → rev 5); Charter Governance `<e.g. 1.1>` → `<e.g. 1.2>` (rev 3 → rev 4). §A Reference Fill (Go service) and §B Reference Fill (infra-only managed service) updated similarly. No structural change to the Annex contract; only example pin values were stale and have been refreshed. |
| 1.1.0 | 4 | 2026-05-12 | MINOR bump applied during Charter Set Audit Round 6 closeout. (a) §0 Charter Pins table extended with three new rows — Stribog User Documentation Standard, Stribog Developer Documentation Standard, Stribog UI/UX Standard — each carrying an Applicability column per its own §0.2. (b) §0 Charter Pins example version values for Glossary and Charter Governance refreshed to the v1.2.0 (rev 3) and v1.3.0 (rev 5) values produced by Round 6. (c) New §2.4 *User-Facing Documentation* declaration block added: user-doc owner, audience tiers, library locations, locales, translation pipeline, doc-site hosting target, doc-to-release sync gate command, doc-accessibility command. (d) New §2.5 *Developer-Facing Documentation* declaration block added: dev-doc owner, audience tiers, README/CONTRIBUTING/bootstrap paths, onboarding budget, surface map and deprecation register paths, compatibility window, reference generators, sample-test runner, drift-gate command, reference hosting target, deprecation announcement channel, migration document path. (e) New §2.6 *UI/UX Surface* declaration block added: design owner, component library, token registry and drift-gate command, theme set, supported viewports and device classes, direction set, locale set, voice charter, accessibility floor and test platforms, visual regression toolchain, automated and manual a11y toolchains, performance budget targets and command, continuous-perf measurement source, telemetry registry, third-party scripts, reduced-motion policy, design review gate convening. Closes Round 6 finding F62 follow-up: the three new standards introduced per-project declarations that the Annex did not previously gather. No clause was weakened; projects whose surfaces predate v1.1.0 carry **N/A** in the §0 row and omit the corresponding §2.4 / §2.5 / §2.6 block. |
| 1.2.0 | 5 | 2026-05-12 | MINOR bump applied during Charter Set Audit Round 7 closeout. §2.6 *UI/UX Surface* extended with twenty-one new sub-block declaration tables matching the [[Stribog UI/UX Standard]] v1.1.0 expansion: §2.6.1 Token Layering; §2.6.2 Color Palette; §2.6.3 Spacing and Baseline; §2.6.4 Theme System; §2.6.5 Visual Polish; §2.6.6 Information Architecture; §2.6.7 Forms Pipeline; §2.6.8 Notifications Surface; §2.6.9 Authentication and Session; §2.6.10 Data Presentation Toolchain; §2.6.11 Modality and Direct Manipulation; §2.6.12 Real-Time and Collaboration; §2.6.13 AI Rendering Pipeline; §2.6.14 Offline Strategy; §2.6.15 Onboarding Sequence; §2.6.16 Embedded and Adjacent Surfaces; §2.6.17 UI Security Configuration; §2.6.18 Native Platform Conventions; §2.6.19 Latency Budgets; §2.6.20 Easing and Motion Curves; §2.6.21 Testing Toolchain. Each sub-block is keyed to the corresponding section of the UI/UX Standard so an auditor can trace per-project declarations back to the binding clause in one hop. Closes Round 7 finding F74 (per-project declaration surface lagged the UI/UX expansion). No clause was weakened; projects whose UIs do not intersect a given sub-surface omit the corresponding sub-block. |
| 1.2.0 | 6 | 2026-05-12 | PATCH revision applied during Charter Set Audit Round 8 closeout. §A *Reference Fill — Go Service Project* and §B *Reference Fill — Infrastructure-Only Managed Service* refreshed to the v1.2.0 canon: pins advanced to Engineering Charter 1.2 rev 7, Documentation Standard 2.1 rev 6, Operational Delivery 1.1 rev 4, User Doc 1.0 rev 1, Developer Doc 1.0 rev 1, UI/UX 1.1 rev 2, Glossary 1.3 rev 4, Charter Governance 1.3 rev 6. §A extended with worked §2.4 user-doc and §2.5 dev-doc declaration fills (CLI + MCP project), and §2.6 UI/UX declared explicitly as **N/A** with rationale (line-oriented CLI per UI/UX §0.2). §B extended with worked §2.4 user-doc (customer-portal + status-page surface), §2.5 dev-doc (internal contributor surface only), and §2.6 UI/UX fills covering status-page IA, notifications, and UI security configuration. Closes Round 8 finding F77 (Annex reference fills lagged the v1.2.0 canon). No structural change to the Annex contract; example values refreshed and worked examples of the new declaration blocks added. |
| 1.2.0 | 7 | 2026-05-12 | PATCH revision applied during Charter Set Audit Round 9 closeout. New §C *Reference Fill — Browser-Only Local-First App* added covering a project shape the template did not previously demonstrate: a client-only SPA / PWA that persists Restricted-class data on the user's device with no hosted backend (encrypted local note-taker, client-side password vault, on-device medical-record viewer, offline-first PWA with on-device LLM inference). The §C fill covers (a) §0 pins with Op-Delivery N/A and Security / Privacy / User Doc / Dev Doc / UI/UX all applicable, (b) §0.1-data-storage local-persistence inventory (IndexedDB / OPFS / localStorage / sessionStorage / Cache API / sync each declared with classification posture), (c) §1.1 single-file-distributable build pipeline (Vite + bundle-check + SRI generation + Playwright smoke against the built artifact) per Eng Charter §7.4, (d) §1.3 source-vs-artifact coverage boundary per Eng Charter §5.5 single-file clause (src/ is coverage subject; dist/ is governed by release discipline), (e) §2.4 / §2.5 / §2.6 declaration fills with UI/UX fully applicable, (f) §2.6.14 offline strategy and §2.6.17 UI security as central design surfaces for this class, (g) §3 git posture with provider-neutral AI-attribution allowlist, (h) §5 Operational Posture **N/A** with rationale, (i) §7 worked waivers reflecting client-only architecture's distinct risk profile. Closes Round 9 finding F79 (no worked example for browser-only local-Restricted-data class). No structural change to the Annex contract; the template now demonstrates three reference fills (§A Go CLI + MCP, §B infra-managed-service, §C browser-only local-first) covering the three commonest Stribog project shapes. |

---
