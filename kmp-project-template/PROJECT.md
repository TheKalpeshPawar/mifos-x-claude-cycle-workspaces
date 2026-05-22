# kmp-project-template

> openMF's official Kotlin Multiplatform / Compose Multiplatform starter template — the canonical scaffold that powers Mifos-X consumer apps (Open Banking, Field Officer, Group Banking, Mobile Wallet, …).
> Imported via `/project-import` on 2026-05-22 as a reference exemplar for KMP project structure, build-logic conventions, and the Effect-based MVI pattern.

| Attribute | Value |
|-----------|-------|
| Workspace | `mifos-x` |
| Slug | `mifos-x-kmp-project-template` |
| Type | `kmp` (subtype: `kmp-template`) |
| Status | `planning` — idea-layer drafted, not yet approved |
| Source | `~/OpenSource/Mifos/kmp-project-template` (symlinked) |
| Fork | `TheKalpeshPawar/kmp-project-template` (origin) |
| Upstream | `openMF/kmp-project-template` |
| Branch | `dev` |
| Created | 2026-05-22 |

## Tech Stack

- **Kotlin** 2.3.20 + **Compose Multiplatform** (via build-logic conventions)
- **Architecture**: MVI with `Effect.kt` + `EventsEffect` (standard MBS/Mifos pattern)
- **DI**: Koin 4.1.1 + koin-annotations 2.1.0 + kotlinInject 0.7.2
- **Network**: Ktor 3.3.3 + Ktorfit 2.7.3
- **Database**: Room 3.0.0-alpha03 + sqlite-bundled 2.6.2 (sqlite-web 2.6.2 for browser)
- **Observability**: Firebase BOM 34.7.0 (Crashlytics + Performance plugins)

## Platforms

| Platform | Status |
|----------|--------|
| Android  | ✅ active (`cmp-android` in settings.gradle.kts) |
| Desktop  | ✅ active (`cmp-desktop`) |
| Web      | ✅ active (`cmp-web`) |
| iOS      | ⚠️ scaffolded (`cmp-ios` directory exists but is NOT in `settings.gradle.kts include()` — present for SwiftUI/Xcode integration when consumed) |

## Module Map

| Group | Modules |
|-------|---------|
| **Apps** | `cmp-android`, `cmp-desktop`, `cmp-web` |
| **Shared** | `cmp-shared`, `cmp-navigation` |
| **Core** | `core:analytics`, `core:common`, `core:data`, `core:database`, `core:datastore`, `core:designsystem`, `core:domain`, `core:model`, `core:network`, `core:store`, `core:ui` (11 modules) |
| **Core-base** | `core-base:analytics`, `core-base:common`, `core-base:database`, `core-base:datastore`, `core-base:designsystem`, `core-base:network`, `core-base:platform`, `core-base:security`, `core-base:store`, `core-base:ui` (10 modules) |
| **Feature** | `feature:home`, `feature:profile`, `feature:settings`, `feature:crypto`, `feature:currency-rates`, `feature:emi-calculator` (6 features) |

## Feature Inventory (idea-layer scope)

The template ships with 6 reference features that demonstrate the architecture end-to-end:

1. **home** — landing/dashboard scaffold
2. **profile** — user profile screen
3. **settings** — preferences (theme, language, etc.)
4. **crypto** — cryptocurrency list/detail (demonstrates network + Room offline cache)
5. **currency-rates** — FX rates table (demonstrates Ktorfit consumption)
6. **emi-calculator** — pure-Kotlin compute (demonstrates a no-network feature)

Per-feature screen YAMLs live at `idea-layer/screens/{feature}.yaml` once `/idea-plan --from-source` STEP 2.5 runs.

## Status / Workflow

| Step | Status | Notes |
|------|--------|-------|
| Workspace scaffolded | ✅ | `PROJECT.md`, `PROJECT_CONFIG.yaml`, `source/` symlink, `idea-layer/` skeleton |
| Source symlinked | ✅ | `source/kmp-project-template/ → ~/OpenSource/Mifos/kmp-project-template` |
| `idea-plan.yaml` drafted | ⏳ | Pending STEP 1–2 deep analysis |
| Per-screen YAMLs | ⏳ | Pending STEP 2.5 |
| MATRIX MODE approval | ⏳ | Pending user review of draft sections |
| `/idea sync` enrichment | — | Run after MATRIX approval |
| `/server init` | n/a | Firebase observability-only; no real backend |

## Next

1. Review draft `idea-layer/idea-plan.yaml` (sections all `_status: draft`).
2. Approve sections via MATRIX MODE; bump to `_status: approved` per section.
3. Optional: `/idea-enrich` to deepen screen YAMLs from source.
4. Optional: `/gap-analysis-project` to surface source ↔ idea-layer drift.

## Related

- Sister project (consumer of this template): `mifos-x/mifos-x-open-banking` — same architecture, ships Open Banking flows.
- Framework references: `references/kmp-project-template/` (if registered as a `/ref-add` submodule for cross-project lookup).
