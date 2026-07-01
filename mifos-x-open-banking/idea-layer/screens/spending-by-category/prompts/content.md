---
ui_yaml_sha: 54715b757e955ff2e6c72f10c6c28f5c78b17caa1809704e7301772f4059f0b1
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 1fb966ca2aeca1e7a37b69ebc4bbcad08b76b3fa531f837b632ae5578d53a116

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: spending-by-category
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# spending-by-category — content state

> Auto-generated from screens/spending-by-category/ui.yaml @ SHA 29670d726d84dd94
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the spending-by-category screen for **HSBC Open Banking**, a UK Open Banking AISP delivering client-side personal finance management computed from HSBC transaction history.

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F, outline #8B9198

**Component 1 - Top App Bar** (full width 393dp, height 64dp, top status bar inset): Outfit medium 22sp title "Spending by Category" in #E0E3E8 left-aligned on #101417 surface. No elevation, no shadow, no scrim.

**Component 2 - Chip Row** (full width minus 32dp insets, height 48dp, 8dp gap between chips): Three filter chips in a horizontal row. "This Month" selected: filled background #004B6F, label #95CDF7, Outfit medium 14sp, radius 9999dp, 32dp height. "Last Month" unselected: outlined border #41474D, label #C1C7CE, Outfit regular 14sp. "3 Months" unselected: outlined border #41474D, label #C1C7CE. All chips 48dp touch target. Archetype: detail_screen.

**Component 3 - Stat Block** (full width minus 32dp insets, 12dp radius, background #1C2024, 16dp padding): Outfit regular 12sp label "Total spent" in #C1C7CE tracked uppercase. Below: monospace bold 28sp "£1,847.32" in #E0E3E8. Supporting line Outfit regular 12sp "June 2025" in #8B9198. 24dp vertical internal padding.

**Component 4 - Bar Chart** (full width minus 32dp insets, height 200dp, background #1C2024, 12dp radius, 16dp padding): Horizontal proportional bar 20dp tall, 4dp radius. Six adjacent segments left to right: Groceries 32% filled #95CDF7, Transport 18% filled #B7C9D9, Dining 15% filled #CFC0E8, Bills 14% filled #384956, Subscriptions 12% filled #004B6F, Shopping 9% filled #41474D. Below bar 12dp gap, two-column legend grid: 6dp filled circle in segment colour beside Outfit 12sp category name #C1C7CE, Outfit 12sp percentage #8B9198.

**Component 5 - List** (full width minus 32dp insets, scrollable below chart, 0dp additional margin): Six rows each 64dp tall, 1dp divider #41474D. Each row: left 8x8dp filled circle in category colour, centre Outfit medium 16sp category name #E0E3E8, trailing column right-aligned with monospace Outfit 16sp amount in #FFB4AB above Outfit 12sp percentage in #C1C7CE. Rows in order: Groceries £583.20 32%, Transport £336.40 18%, Dining £275.10 15%, Bills £262.60 14%, Subscriptions £221.68 12%, Shopping £168.34 9%.

**Component 6 - Bottom Navigation Bar** (full width, height 80dp, background #1C2024, bottom inset): Four tabs. Active "Spending": icon pie_chart filled, icon and label #95CDF7 Outfit 12sp. Inactive "Overview" icon home, "Budgets" icon savings, "Subscriptions" icon autorenew: icon and label #8B9198. 48dp icon touch area each.

Do not use an em-dash anywhere in this design. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark surface theme between sections with lighter panel backgrounds or decorative dividers. Do not place dark text on dark-filled buttons or light text on light chip labels.

Six spending categories rendered in measured grid-aligned rows against the near-black surface, trust-blue accent #95CDF7 reserved solely for the active period chip and the selected nav icon. calm.

↑↑↑ MOCKUP PROMPT
