---
ui_yaml_sha: 54715b757e955ff2e6c72f10c6c28f5c78b17caa1809704e7301772f4059f0b1
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 332c53199a98657e3a77eba3e0382cfef6efcd4c373ec04da89f8e14b81b8ad8

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: spending-by-category
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# spending-by-category — empty state

> Auto-generated from screens/spending-by-category/ui.yaml @ SHA 6293c9ef354cea79
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the spending-by-category screen for **HSBC Open Banking**, a UK Open Banking AISP delivering client-side personal finance management computed from HSBC transaction history.

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F, outline #8B9198

**Component 1 - Top App Bar** (full width 393dp, height 64dp): Outfit medium 22sp title "Spending by Category" in #E0E3E8 left-aligned on #101417. No elevation.

**Component 2 - Chip Row** (full width minus 32dp insets, height 48dp, 8dp gap): Three chips. "This Month" selected: filled #004B6F, label #95CDF7, Outfit medium 14sp, radius 9999dp, 32dp height. "Last Month" unselected: outlined #41474D, label #C1C7CE. "3 Months" unselected: outlined #41474D, label #C1C7CE. Period selector stays active even when no data exists for the period. Archetype: empty_state.

**Component 3 - Empty State** (centered in scroll area below chip row, 32dp horizontal insets, 64dp top spacing): Outline icon pie_chart 72dp in #C1C7CE centered. 16dp gap. Outfit medium 20sp heading "No spending data" in #E0E3E8 center-aligned. 8dp gap. Outfit regular 14sp body "No transactions found for this period. Try a different date range or connect your HSBC account to get started." in #C1C7CE center-aligned, max 3 lines. 24dp gap. Button: filled pill, background #95CDF7, label "Explore Accounts" in #00344E Outfit medium 14sp, 48dp height, 200dp min-width, radius 9999dp. All elements horizontally centered.

**Component 4 - Bottom Navigation Bar** (full width, height 80dp, background #1C2024): Active "Spending": icon pie_chart filled, icon and label #95CDF7. Inactive "Overview", "Budgets", "Subscriptions": icon and label #8B9198. Outfit 12sp labels.

Do not use an em-dash anywhere in this design. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark surface theme with any lighter background behind the Empty State component. Do not place dark text on dark-filled CTA buttons.

An uncluttered dark canvas centred on a single well-composed empty state above the nav bar, trust-blue #95CDF7 reserved for the period chip and the single call-to-action, everything else stepping back. minimal.

↑↑↑ MOCKUP PROMPT
