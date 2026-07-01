---
ui_yaml_sha: a08e052152877d4ac6b23ae4ddc9eec203447ec8d53b663f8b21b2e9fc9957ad
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 1813e37beb80ece366a08af41dbf15566285f27e5c4c83d29b12c9fd878eb22d

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: budgets
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# budgets — loading state

> Auto-generated from screens/budgets/ui.yaml @ SHA 315b112554b49dff
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the budgets screen for **HSBC Open Banking**, a UK Open Banking AISP letting HSBC account holders set and track monthly spending limits by category.

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F, outline #8B9198

**Component 1 - Top App Bar** (full width 393dp, height 64dp): Outfit medium 22sp title "Budgets" in #E0E3E8 on #101417. Visible and real during loading. No elevation.

**Component 2 - Card** (full width minus 32dp insets, 12dp radius, background #1C2024, 16dp padding): "Set a Budget" section label shimmer bar 100x12dp #262A2E. Below: two full-width shimmer bars each 48dp tall #262A2E representing the category dropdown and amount field, 8dp gap between. Full-width 48dp shimmer bar for the Save Budget button placeholder. Shimmer sweep left-to-right. Archetype: skeleton_screen.

**Component 3 - List** (full width minus 32dp insets, 12dp gap between cards): Section label shimmer 80x12dp #262A2E. Six skeleton budget Cards below, each: 12dp radius, #1C2024 background, 16dp padding. Inside each: header row shimmer 120x16dp #262A2E left, 80x12dp #262A2E right. Progress bar placeholder: full-width 6dp tall #262A2E shimmer. Status line placeholder: 100x12dp #262A2E shimmer. Shimmer sweep uniform across all six cards, in-phase.

**Component 4 - Bottom Navigation Bar** (full width, height 80dp, background #1C2024): All tabs visible and stable during loading. Active "Budgets": savings icon and label #95CDF7. Inactive "Overview", "Spending", "Subscriptions": icon and label #8B9198. Nav bar never shimmer-animated.

Do not use an em-dash anywhere in this design. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the near-black surface theme with lighter shimmer base colours outside the palette. Do not render any readable text or numeric content inside skeleton placeholders.

Six skeleton budget cards pulse in #262A2E shimmer, spatial placeholders confirming the data shape before transaction records resolve, trust-blue #95CDF7 alive only in the stable nav tab. calm.

↑↑↑ MOCKUP PROMPT
