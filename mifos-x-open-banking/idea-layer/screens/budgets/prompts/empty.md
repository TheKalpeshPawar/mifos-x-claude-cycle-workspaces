---
ui_yaml_sha: a08e052152877d4ac6b23ae4ddc9eec203447ec8d53b663f8b21b2e9fc9957ad
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: f4924e61020491582fc9a721fcb50d6943c240042297cbf4569f360a3f713c63

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: budgets
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# budgets — empty state

> Auto-generated from screens/budgets/ui.yaml @ SHA 966398224a1dc68c
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the budgets screen for **HSBC Open Banking**, a UK Open Banking AISP letting HSBC account holders set and track monthly spending limits by category.

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F, outline #8B9198

**Component 1 - Top App Bar** (full width 393dp, height 64dp): Outfit medium 22sp title "Budgets" in #E0E3E8 on #101417. No elevation.

**Component 2 - Card** (full width minus 32dp insets, 12dp radius, background #1C2024, 16dp padding): Section label "Set a Budget" Outfit medium 12sp #95CDF7 tracked uppercase, 8dp bottom margin. Outlined field 48dp tall border #41474D label "Category" #C1C7CE. Outlined field 48dp tall border #41474D label "Monthly limit" #C1C7CE. Filled Button: background #95CDF7, label "Save Budget" in #00344E Outfit medium 14sp, 48dp height, radius 9999dp, full width. The Set Budget card is the primary action surface and always visible. Archetype: empty_state.

**Component 3 - Empty State** (centered in scroll area below Set Budget card, 32dp horizontal insets, 48dp top spacing): Icon savings 64dp in #C1C7CE centered. 16dp gap. Outfit medium 20sp heading "No budgets set" in #E0E3E8 center-aligned. 8dp gap. Outfit regular 14sp "Use the form above to create your first monthly spending limit. Limits are tracked against your HSBC transactions." in #C1C7CE center-aligned, max 3 lines. No additional button below (the Set Budget card above is the action).

**Component 4 - Bottom Navigation Bar** (full width, height 80dp, background #1C2024): Active "Budgets": savings icon and label #95CDF7. Inactive "Overview", "Spending", "Subscriptions": icon and label #8B9198.

Do not use an em-dash anywhere in this design. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark surface theme between the Set Budget card and the empty-state guidance below it. Do not place dark labels on dark card backgrounds or light labels on the filled primary button in a colour other than #00344E.

The Set Budget card with its trust-blue #95CDF7 save button dominates the upper half as the natural entry point, while the savings icon and guidance below confirm no budgets exist yet. minimal.

↑↑↑ MOCKUP PROMPT
