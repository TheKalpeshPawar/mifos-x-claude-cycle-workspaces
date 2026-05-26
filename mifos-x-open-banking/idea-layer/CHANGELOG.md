# mifos-x-open-banking — Changelog

All notable changes to the idea-layer are documented here. Format inspired by [Keep a Changelog](https://keepachangelog.com/).

## [Unreleased]

### Changed (design-system)
- [design-system] v1.0.0 → v2.0.0: Full regeneration from Figma source (file tEEJwW4HkUR75fKhDq73Jz). Primary color `#1800B1` → `#4C662B`, font Inter/Space Grotesk → Outfit, background `#FCF8FF` → `#F9FAEF`. 14 component specs (12 universal + 2 banking). WCAG AA validated (12 pairs, 0 failures). App-shell colors updated.

### Changed
- IDEA.md + FEATURES.md repositioned as **empty-slate scaffold** (2026-05-22) — was previously describing TaskMinder (template reference), then briefly redescribed as "financial utilities showcase" reflecting template feature modules. Both narratives were wrong; the actual product scope is undefined and to be set by `/idea-plan`.
- PROJECT_CONFIG.yaml `architecture: mvi` → `architecture: stream-first`.
- PROJECT_CONFIG.yaml `modules.feature` extended to reflect actual source state (6 modules) — note: crypto/currency-rates/emi-calculator scheduled for removal.

### Added
- IDEA.md (empty-slate version) — brand + architecture only, no fake product narrative.
- FEATURES.md (empty-slate) — only home/profile/settings; template features marked for removal.
- REQUIREMENTS.md — scaffolding FRs (FR-001…FR-005) + universal NFRs (NFR-001…NFR-016).
- ROADMAP.md — v0.1 (Empty-slate Scaffold) → v0.2 (Product Scope Definition).
- LAYER_STATUS.md — per-layer enabled/active table.
- CAPABILITY_STATE.yaml — backfill scaffold for 4 retained features + `pending_removal` block.
- TAG_REGISTRY.yaml — feature + priority + maturity + architecture + platform + concerns tag taxonomy.
- APP_FLOW.mmd — navigation graph reflecting only scaffolding screens.
- idea-layer/flows/app-main.yaml — main app flow (scaffolding only).
- idea-layer/design-system/design-tokens.yaml — Material 3 token system from brand `#1800B1`.
- idea-layer/design-system/DESIGN.md — design principles + color/type/spacing/motion specs.
- idea-layer/design-system/COMPONENTS.md — M3 component inventory + project-specific wrappers.
- idea-layer/design-system/app-shell.yaml — app-shell defaults (top app bar, bottom nav, snackbar host).
- 6 layer-status doc pairs in workspace (server/client/feature/infrastructure/platform/testing).

### Removed
- 3 stub ui.yaml directories: `screens/crypto/`, `screens/currency-rates/`, `screens/emi-calculator/` — created in error during initial sync attempt; removed once empty-slate direction confirmed.

## [0.1-bootstrap] — 2026-05-20

Initial post-import idea-layer scaffold after `/project-import`.

### Added
- IDEA.md (auto-generated from template assumptions — replaced 2026-05-22).
- FEATURES.md (template reference — replaced 2026-05-22).
- 4 feature screen directories (home, profile, settings, splash) with ui.yaml stubs.
- PROJECT.md, PROJECT_CONFIG.yaml.
- idea-plan.yaml (output of `/idea-plan --from-source` 4-agent deep import).
