---
ui_yaml_sha: 54715b757e955ff2e6c72f10c6c28f5c78b17caa1809704e7301772f4059f0b1
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: fa671b892d0e3908cf9d671a4bd6cf289d0b7a1400fd65050cf8179889850711

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: spending-by-category
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# spending-by-category — loading state

> Auto-generated from screens/spending-by-category/ui.yaml @ SHA b3d500d065b6975b
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the spending-by-category screen for **HSBC Open Banking**, a UK Open Banking AISP delivering client-side personal finance management computed from HSBC transaction history.

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F, outline #8B9198

**Component 1 - Top App Bar** (full width 393dp, height 64dp): Outfit medium 22sp title "Spending by Category" in #E0E3E8 left-aligned on #101417. No elevation. Title is visible and real during loading.

**Component 2 - Chip Row** (full width minus 32dp insets, height 48dp, 8dp gap): Three ghost chip placeholders in a horizontal row. Each: rounded rectangle 80x32dp, fill #262A2E, shimmer sweep left-to-right with #313539 highlight band. No text rendered on chips. Archetype: skeleton_screen.

**Component 3 - Stat Block** (full width minus 32dp insets, 12dp radius, background #1C2024, 16dp padding): Three stacked shimmer bars. Top: 80x12dp #262A2E shimmer. Middle: 140x28dp #262A2E shimmer. Bottom: 100x12dp #262A2E shimmer. 8dp vertical gap between bars. Shimmer sweep uniform, left-to-right.

**Component 4 - Bar Chart** (full width minus 32dp insets, height 200dp, background #1C2024, 12dp radius, 16dp padding): Single full-width 20dp tall rectangle in #262A2E shimmer representing the loading bar. Below: two-column legend area showing six 120x12dp shimmer bars in #262A2E with 8dp gaps. No colour segments visible.

**Component 5 - List** (full width minus 32dp insets): Six skeleton rows each 64dp tall, 1dp divider #41474D. Each row: left 8x8dp circle #262A2E shimmer, centre 120x16dp shimmer above 60x12dp shimmer, trailing 60x16dp shimmer above 40x12dp shimmer. Shimmer pulse consistent and in-phase across all rows.

**Component 6 - Bottom Navigation Bar** (full width, height 80dp, background #1C2024): All four tabs rendered at full opacity during loading. Active "Spending": pie_chart icon and label #95CDF7. Inactive "Overview", "Budgets", "Subscriptions": icon and label #8B9198. Nav bar is stable and not shimmer-animated.

Do not use an em-dash anywhere in this design. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the near-black surface theme with lighter shimmer base colours or with any panel that steps outside the palette. Do not place any readable text on skeleton bars.

Skeleton blocks pulse in #262A2E against the #101417 surface, the layout silhouette legible before any data arrives, trust-blue #95CDF7 visible only in the stable nav tab below. calm.

↑↑↑ MOCKUP PROMPT
