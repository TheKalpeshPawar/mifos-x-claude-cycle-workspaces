# IDEA — kmp-project-template

> Production-ready Kotlin Multiplatform template — pre-wired MVI + offline-first Store + Compose UI across Android, Desktop, and Web (iOS scaffolded).

| Attribute | Value |
|-----------|-------|
| Slug | `mifos-x-kmp-project-template` |
| Type | KMP starter template (`kmp` / subtype `kmp-template`) |
| Source | `~/OpenSource/Mifos/kmp-project-template` (symlinked from `openMF/kmp-project-template` fork) |
| Status | `planning` — idea-layer drafted, all sections `_status: draft` pending MATRIX approval |
| Created | 2026-05-22 |

## Problem

Bootstrapping a cross-platform KMP app from scratch costs weeks of work: build-logic conventions, dependency injection, MVI plumbing, design system, multi-platform CI/CD, signing, release pipelines. Each new openMF / Mifos-X consumer app (Open Banking, Group Banking, Field Officer, Mobile Wallet, …) was re-solving the same problems.

## Solution

A consumable starter template that encodes 5+ years of openMF KMP architecture patterns:

- **15 Gradle convention plugins** (Android, Compose, Firebase, KMP-library, Koin, Room, Detekt, Spotless, Ktlint, Kover, GitHooks, …)
- **MVI architecture** via `BaseViewModel<LocalState, Event, Action>` + `Effect.kt` + `EventsEffect`
- **Offline-first Store framework** with declarative `ScreenContent` (Loading / Content / Empty / Error) + `PagingScreenStream<T>`
- **Material 3 design system** with custom Mifos palette (#1800B1 primary) + Outfit font family + adaptive layouts (List-Detail, Navigable, Sidebar, SplitPane, Masonry, FlowRow, Grid)
- **Real demo features** that hit live public APIs (CoinGecko, Frankfurter) — not toy hello-world examples
- **9 GitHub Actions workflows** wired to Fastlane + Play Store + TestFlight + Firebase App Distribution + GitHub Pages
- **lib-integrate machinery** for workspace-local dependency swapping (skip-worktree `lib-integrate.properties`)
- **Customizer script** (`customizer.sh`) to rewrite package namespace + app name for new forks

## Target Users

### Persona 1 — Priya, KMP Team Lead, Mifos-X consumer app
Spinning up a new Mifos-X app (group banking, field officer, …) with the same architecture as the rest of the suite. **Pain:** Before this template — ad-hoc module layout per project, inconsistent MVI patterns, manual CI wiring each time.

### Persona 2 — Daniel, Senior Engineer at a fintech evaluating CMP
Validating CMP feasibility for shipping Android + Desktop + Web from a single codebase, with a realistic example that already wires network, Room, DI, Theme, Navigation. **Pain:** Existing CMP samples are toy apps — no production CI, no offline-first patterns, no real APIs.

### Persona 3 — Mara, Open-source contributor learning Mifos architecture
Understanding the `BaseViewModel` + `Effect.kt` + Store pattern by reading 6 well-organized demo features. **Pain:** Mifos production apps (Mobile, Mobile-Wallet) are too large to learn from cold; this template is the minimum viable example.

## Demo Features (Architecture Showcase)

| Feature | Demonstrates |
|---------|---------------|
| **home** | Stateless navigation hub — 4 feature cards. |
| **profile** | Stub feature pattern (placeholder slot for fork customization). |
| **settings** | DataStore-backed preferences via `UserDataRepository`; standard ViewModel (not BaseViewModel) — shows both patterns coexisting. |
| **crypto** | Network-backed paging via `PagingScreenStream<CoinMarket>` + CoinGecko `/api/v3/coins/markets`. Pull-to-refresh, infinite scroll, detail drilldown. |
| **currency-rates** | Live network table via Frankfurter `/v1/latest` (USD base). Live search filter, empty state, history drilldown. |
| **emi-calculator** | Pure-Kotlin compute (no network) — `BaseViewModel<EmiState, Nothing, EmiAction>` with form inputs and reactive results. |

## Technical Stack

| Layer | Choice |
|-------|--------|
| Language | Kotlin **2.3.20** |
| UI | Compose Multiplatform |
| Architecture | MVI (`BaseViewModel` + `Effect.kt` + `EventsEffect`) |
| DI | Koin **4.1.1** + koin-annotations 2.1.0 + kotlinInject 0.7.2 |
| Network | Ktor **3.3.3** + Ktorfit **2.7.3** |
| Database | Room **3.0.0-alpha03** + sqlite-bundled 2.6.2 (+ sqlite-web 2.6.2) |
| DataStore | multiplatform-settings 1.3.0 + AndroidX DataStore |
| Image | Coil 3.3.0 |
| Navigation | Compose Navigation 2.9.1 (Jetbrains CMP) |
| Observability | Firebase BOM **34.7.0** (Crashlytics + Performance) |
| Versioning | Gradle Reckon (semantic) + monthly calendar (YYYY.MM.0) |

## Platforms

| Platform | Status | Artifact |
|----------|--------|----------|
| Android | ✅ active | APK + AAB → Play Store + Firebase App Distribution |
| Desktop | ✅ active | EXE / MSI / DMG / DEB → GitHub Releases |
| Web | ✅ active | Browser bundle → GitHub Pages |
| iOS | ⚠️ scaffolded | `cmp-ios` directory exists; not in `settings.gradle.kts` `include()`. Forks opt in. |

## Module Topology

- **Apps** (3): `cmp-android`, `cmp-desktop`, `cmp-web`
- **Shared** (2): `cmp-shared`, `cmp-navigation`
- **Core** (11): `core:{analytics, common, data, database, datastore, designsystem, domain, model, network, store, ui}`
- **Core-base** (10): `core-base:{analytics, common, database, datastore, designsystem, network, platform, security, store, ui}`
- **Features** (6): `feature:{home, profile, settings, crypto, currency-rates, emi-calculator}`

## Why This Template Wins (Differentiator)

1. **Real APIs, not mocks** — CoinGecko + Frankfurter integrations prove the network stack works end-to-end.
2. **Comprehensive build-logic** — 15 convention plugins vs. typical CMP samples that ship 1-3.
3. **Production CI** — 9 workflows covering PR gate, multi-platform build, weekly + monthly versioning, coverage gate, docs site.
4. **Multi-target distribution** — Play Store internal/beta/prod, TestFlight, App Store, Firebase App Distribution, GitHub Pages, GitHub Releases.
5. **Workspace integration** — lib-integrate machinery means forks can swap Maven artifacts for local source dirs without modifying gradle files.

## Next Steps

1. Review draft sections in `idea-plan.yaml` and approve via MATRIX MODE.
2. (Optional) Run `/idea-enrich` to deepen per-screen YAMLs.
3. (Optional) Run `/gap-analysis-project` to detect drift between source and idea-layer.
4. (Optional) Add this project to `references/` (via `/ref-add`) so it's queryable from `/ref-lookup` across other projects.
