---
ui_yaml_sha: a08e052152877d4ac6b23ae4ddc9eec203447ec8d53b663f8b21b2e9fc9957ad
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 16c28734282d5b46110a05488c43d0a0576ec64cca9e9c0d3c0c52265f19b0df

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: budgets
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# budgets — content state

> Auto-generated from screens/budgets/ui.yaml @ SHA 4f573b9b17eb5d0d
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the budgets screen for **HSBC Open Banking**, a UK Open Banking AISP letting HSBC account holders set and track monthly spending limits by category.

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F, outline #8B9198

**Component 1 - Top App Bar** (full width 393dp, height 64dp): Outfit medium 22sp title "Budgets" in #E0E3E8 left-aligned on #101417. No elevation.

**Component 2 - Card** (full width minus 32dp insets, 12dp radius, background #1C2024, 16dp padding): Section label "Set a Budget" Outfit medium 12sp #95CDF7 tracked uppercase, 8dp bottom margin. Outlined field row 48dp tall, border #41474D, label "Category" #C1C7CE Outfit regular 14sp, trailing chevron icon #8B9198 - acts as dropdown selector with options Groceries, Dining, Transport, Bills, Shopping, Subscriptions. Outlined text field 48dp tall below, border #41474D, label "Monthly limit" #C1C7CE Outfit regular 14sp, currency keyboard. Filled Button below: full-width, background #95CDF7, label "Save Budget" in #00344E Outfit medium 14sp, 48dp height, radius 9999dp. 8dp gap between each field. Archetype: screen.

**Component 3 - List** (full width minus 32dp insets, scrollable, 12dp gap between cards): Section label "June 2025" Outfit medium 12sp #C1C7CE tracked uppercase 8dp above first card. Six budget Cards, each: 12dp radius, background #1C2024, 16dp padding. Inside each card: header row with Outfit medium 16sp category name #E0E3E8 left, trailing Outfit 12sp "spent / limit" in #C1C7CE right. Progress Bar below header: full width, 6dp height, 4dp radius. Under-budget fill #95CDF7, over-budget fill #FFB4AB. Status line below bar: under-budget "£XX.XX remaining" in #C1C7CE Outfit 12sp, over-budget "£XX.XX over limit" in #FFB4AB Outfit 12sp. All amounts in monospace. Cards: Groceries £312.40/£350 under 89% bar #95CDF7 "£37.60 remaining", Dining £231.80/£200 over 116% bar #FFB4AB "£31.80 over limit", Transport £98.20/£150 under 65% bar #95CDF7 "£51.80 remaining", Bills £784.50/£800 under 98% bar #95CDF7 "£15.50 remaining", Shopping £156.90/£120 over 131% bar #FFB4AB "£36.90 over limit", Subscriptions £42.98/£50 under 86% bar #95CDF7 "£7.02 remaining".

**Component 4 - Bottom Navigation Bar** (full width, height 80dp, background #1C2024): Active "Budgets": icon savings filled, icon and label #95CDF7 Outfit 12sp. Inactive "Overview", "Spending", "Subscriptions": icon and label #8B9198.

Do not use an em-dash anywhere in this design. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark surface theme between the Set Budget card and the budget list. Do not place dark text on dark-filled buttons or use green/red semantics outside the defined palette.

Progress bars rendered in two precise tones: trust-blue #95CDF7 for headroom, error-rose #FFB4AB for overspend, keeping regulatory calm while making over-budget rows immediately legible. restrained.

↑↑↑ MOCKUP PROMPT
