---
ui_yaml_sha: 23ce864f95d53e84e96f1b0c3f59d4d67febe5921e8eb4e697b2ff798f694ce8
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 1af1e007d34e1be41b1624e6ca5b2edb07f37e7c0a2f593988ab3f0d932ee0f4

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: recurring-subscriptions
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# recurring-subscriptions — loading state

> Auto-generated from screens/recurring-subscriptions/ui.yaml @ SHA 881f830a7fa6e61f
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the recurring-subscriptions screen for **HSBC Open Banking**, a UK Open Banking AISP that automatically detects recurring payments from HSBC transaction history.

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F, outline #8B9198

**Component 1 - Top App Bar** (full width 393dp, height 64dp): Outfit medium 22sp title "Recurring Payments" in #E0E3E8 on #101417. Visible and real during loading. No elevation.

**Component 2 - Banner** (full width minus 32dp insets, 12dp radius, background #004B6F, 12dp vertical padding): Info icon placeholder circle 20dp in #41474D left. Beside it: full-width shimmer bar 200x13dp #41474D representing the detection notice text. Banner shape and background remain visible to preserve layout structure. Archetype: skeleton_screen.

**Component 3 - Stat Block** (full width minus 32dp insets, 12dp radius, background #1C2024, 16dp padding): Three stacked shimmer bars: 80x12dp #262A2E, 120x28dp #262A2E, 160x12dp #262A2E. 8dp vertical gap between each. Shimmer sweep left-to-right.

**Component 4 - List** (full width minus 32dp insets, 1dp dividers #41474D): Six skeleton rows each 72dp tall. Each: left 40x40dp circle #262A2E shimmer. Centre column: 120x16dp shimmer above 80x13dp shimmer. Trailing column: 60x16dp shimmer above 56x12dp shimmer. Shimmer pulse uniform and in-phase across all six rows.

**Component 5 - Bottom Navigation Bar** (full width, height 80dp, background #1C2024): Stable during loading. Active "Subscriptions": autorenew icon and label #95CDF7. Inactive "Overview", "Spending", "Budgets": icon and label #8B9198. Nav never shimmer-animated.

Do not use an em-dash anywhere in this design. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark surface by introducing shimmer base colours lighter than #262A2E or outside the palette. Do not render any merchant names, amounts, or dates in skeleton rows.

Six subscription-row silhouettes pulse in #262A2E shimmer against the #101417 surface, preserving spatial expectation before detection resolves, trust-blue #95CDF7 the only live colour in the stable nav tab. calm.

↑↑↑ MOCKUP PROMPT
