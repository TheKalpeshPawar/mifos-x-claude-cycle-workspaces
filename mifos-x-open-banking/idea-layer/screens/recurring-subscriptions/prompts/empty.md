---
ui_yaml_sha: 23ce864f95d53e84e96f1b0c3f59d4d67febe5921e8eb4e697b2ff798f694ce8
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: dbc35cb0ad0773bcc1d11a92b03230ab055e3cd6aafac692678b5af25a177a58

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: recurring-subscriptions
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# recurring-subscriptions — empty state

> Auto-generated from screens/recurring-subscriptions/ui.yaml @ SHA 7d4c6fd9b716dd1c
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the recurring-subscriptions screen for **HSBC Open Banking**, a UK Open Banking AISP that automatically detects recurring payments from HSBC transaction history.

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F, outline #8B9198

**Component 1 - Top App Bar** (full width 393dp, height 64dp): Outfit medium 22sp title "Recurring Payments" in #E0E3E8 on #101417. No elevation.

**Component 2 - Banner** (full width minus 32dp insets, 12dp radius, background #004B6F, 12dp vertical padding, 16dp horizontal padding): Icon info_outline 20dp in #95CDF7 left. Beside it: Outfit regular 13sp "Recurring payments are detected automatically once enough transaction history is available." in #C9E6FF. Archetype: empty_state.

**Component 3 - Empty State** (centered in scroll area below banner, 32dp horizontal insets, 64dp top spacing): Icon autorenew 72dp in #C1C7CE centered. 16dp gap. Outfit medium 20sp heading "No recurring payments found" in #E0E3E8 center-aligned. 8dp gap. Outfit regular 14sp "Connect your HSBC account and allow a few days for patterns to appear in your transaction history." in #C1C7CE center-aligned, max 3 lines. 24dp gap. Button: filled pill background #95CDF7, label "Connect Account" in #00344E Outfit medium 14sp, 48dp height, 200dp min-width, radius 9999dp. All elements horizontally centered.

**Component 4 - Bottom Navigation Bar** (full width, height 80dp, background #1C2024): Active "Subscriptions": autorenew icon and label #95CDF7. Inactive "Overview", "Spending", "Budgets": icon and label #8B9198.

Do not use an em-dash anywhere in this design. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark surface between the informational banner and the empty state with any lighter panel or gradient. Do not place dark text on the filled CTA button or light text on the dark banner without the palette-defined contrast.

The detection banner explains how patterns are found, while the centred empty state guides gently towards account connection, trust-blue #95CDF7 reserved for the single call-to-action and the active nav icon. minimal.

↑↑↑ MOCKUP PROMPT
