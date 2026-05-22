# mifos-x-open-banking

> Production-ready Kotlin Multiplatform starter from the Mifos Initiative — Android, iOS, Desktop, Web, all from one codebase.

| Attribute | Value |
|-----------|-------|
| **Slug** | `mifos-x-open-banking` |
| **Workspace** | `mifos-x` |
| **Type** | KMP (Compose Multiplatform) |
| **Platforms** | Android · iOS · Desktop · Web |
| **Architecture** | Stream-First (BaseViewModel + ScreenDataStream + Store5) · Koin DI · Ktor/Ktorfit · Room KMP |
| **Backend** | Firebase (Crashlytics + Performance) |
| **Status** | `initialized` — adopted via `/project-import` on 2026-05-20 |
| **Source** | [github.com/openMF/mifos-x-open-banking](https://github.com/openMF/mifos-x-open-banking) |
| **Fork** | [TheKalpeshPawar/mifos-x-open-banking](https://github.com/TheKalpeshPawar/mifos-x-open-banking) (`dev` branch) |
| **Local clone** | `workspaces/mifos-x/mifos-x-open-banking/source/mifos-x-open-banking/` → symlink to `/home/kalpesh/OpenSource/Mifos/mifos-x-open-banking/` (full git history, user-managed) |
| **Current branch** | `feat/sync-workspace-with-template-post-sync` (feature branch; upstream default is `dev`) |

## Module Map

```
cmp-android    cmp-desktop    cmp-ios    cmp-web       ← platform entry points
        ╲          │           │         ╱
              cmp-shared · cmp-navigation                ← composition root
                        │
        ┌──────────────┼──────────────┐
   core/*         core-base/*      feature/*
   (data, db,    (analytics,    (home, profile,
    domain,       common,        settings, crypto,
    network,…)    network,…)     currency-rates,
                                 emi-calculator)
```

## Layer Status

All 8 layers enabled. Idea-layer is being bootstrapped from source via 4 parallel Explore agents (see `idea-layer/idea-plan.yaml` for live state).

## Next Steps

1. Complete `/idea-plan --from-source` deep analysis (4 agents in parallel).
2. Review draft sections in `idea-layer/idea-plan.yaml`, mark approved.
3. Run `/idea sync` to enrich generated screen YAMLs.
4. `/gap-analysis-project` to surface mismatches between source and idea-layer.
5. `/kmp-implement {feature}` for new work going forward.

## Configuration

Machine-readable: `PROJECT_CONFIG.yaml`. Edit via `/project-add --verify` or directly.
