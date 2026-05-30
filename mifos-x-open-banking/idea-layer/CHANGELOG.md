# mifos-x-open-banking — Changelog

All notable changes to the idea-layer are documented here. Format inspired by [Keep a Changelog](https://keepachangelog.com/).

### 2026-05-30 — removed consumer-home

Removed orphan duplicate screen consumer-home (zero inbound navigation, not in IDEA_MATRIX; canonical consumer dashboard `home` retained). Scrubbed catalog refs; repaired flood corruption in dtos/_index.yaml + server/api_manifest.yaml.

## [Unreleased]

### Exported (design)
- [idea-export] 2026-05-29 — Generated design exports for all 45 features (135 artifacts: 45× SPEC.md + API.md + MOCKUP.md). 6 features exported for the first time (consumer-home, licenses, privacy-policy, standing-order-detail, standing-order-edit, terms-of-service); 39 re-exported from current source YAML (stale brand tokens corrected to v3.0.0 `#4C662B`/Outfit). 2 features transitioned `enriched → designed` (consumer-home, standing-order-edit); 43 already-approved left unchanged. EXPORT_MATRIX.yaml rebuilt: 45 rows, spec/api/mockup all current. Zero placeholders. Roundtrip: 45/45 pass.

### Added
- **consumer-home** — new consumer-persona home dashboard screen (FR-019): balance card, income/spend summary, quick actions (Send/Accounts/Standing Orders/Cards), recent transactions list, 4 states (loading/content/error/empty). Scaffolded: `docs.yaml`, `ui.yaml`, `api.yaml`, `flow.yaml`, `tests.yaml`.
- **standing-order-edit** — scaffolded missing siblings for existing draft screen (FR-006): `ui.yaml` (edit form: amount, currency, frequency, start/end date), `api.yaml` (PUT endpoint), `flow.yaml`, `tests.yaml`.

### Changed (design-system)
- [design-system] v3.0.0 force-regenerate (2026-05-29): Clean schema v3.0 regeneration from scratch — same Figma-sourced palette `#4C662B` + Outfit typeface, no content change. Versioned snapshot `design-tokens.v3.0.0.yaml` created. WCAG AA: 12 pairs, 0 failures. DESIGN.md coherence: PASS (all 5 checks).
- [design-system] v2.0.0 → v3.0.0 (2026-05-28): Schema bump to v3.0 — fixes RULE-DS-TOKEN-VALIDATE-001 DST3 (added top-level `metadata` + `touchTargets` blocks) and DST4 (renamed `color:` → `colors:` plural). Added dark scheme (29 roles), 4 mood gradients (growth_dawn, financial_stability, field_dusk, trust_horizon), M3 emphasized easing curves. DESIGN.md + COMPONENTS.md refreshed to v3.0.0. WCAG AA: 12 pairs, 0 failures. Backup: `design-tokens.v2.0.0.yaml.bak-20260528T155300Z`.
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
- [design-system-stitch] 2026-05-29 — DESIGN.md uploaded to Stitch (asset_id=2005644667042354169, design_md_sha=71b53c295bf8)
