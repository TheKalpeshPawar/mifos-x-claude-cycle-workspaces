---
ui_yaml_sha: a08e052152877d4ac6b23ae4ddc9eec203447ec8d53b663f8b21b2e9fc9957ad
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 03d225f6fb6ad9e1c52833a9735f78b032eb25894f544898e33ceb2c3e72bcf9

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: budgets
state: error
state_visibility: error

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# budgets — error state

> Auto-generated from screens/budgets/ui.yaml @ SHA f7b88c61ea486251
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the budgets screen for **HSBC Open Banking**, a UK Open Banking AISP letting HSBC account holders set and track monthly spending limits by category.

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F, outline #8B9198

**Component 1 - Top App Bar** (full width 393dp, height 64dp): Outfit medium 22sp title "Budgets" in #E0E3E8 on #101417. No elevation.

**Component 2 - Error State** (centered in full scroll area, 32dp horizontal insets, 80dp top spacing from app bar): Icon warning_amber 72dp in #FFB4AB centered. 16dp gap. Outfit medium 20sp heading "Couldn't load budgets" in #E0E3E8 center-aligned. 8dp gap. Outfit regular 14sp body "Your transaction data is temporarily unavailable. Pull down to refresh or tap retry." in #C1C7CE center-aligned, max 3 lines. 24dp gap. Button: filled pill background #95CDF7, label "Retry" in #00344E Outfit medium 14sp, 48dp height, 160dp min-width, radius 9999dp. All elements horizontally centered. No budget list or Set Budget form visible. Archetype: error_state.

**Component 3 - Bottom Navigation Bar** (full width, height 80dp, background #1C2024): Active "Budgets": savings icon and label #95CDF7. Inactive "Overview", "Spending", "Subscriptions": icon and label #8B9198.

Do not use an em-dash anywhere in this design. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark surface by placing the Error State on a visually distinct lighter panel or error-coloured background. Do not place dark text on dark-filled buttons.

A pared-back error surface with a single centred action: warning-amber #FFB4AB signals the problem, trust-blue #95CDF7 on the retry button immediately restores agency, dark #101417 keeping the regulated-fintech register. restrained.

↑↑↑ MOCKUP PROMPT
