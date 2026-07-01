---
ui_yaml_sha: 8f627a0862016e34b232d8c97c47bf23a2cebbe6255b04b8f9e6429b85a1f5c9
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 34f97a03f569c03ddca362b9e8303897c9f87e5aff16fbf1e2d8ec292341601f

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: direct-debits
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# direct-debits — loading state

> Auto-generated from screens/direct-debits/ui.yaml @ SHA f032d896b251263c
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the Direct Debits screen for **HSBC Open Banking**, a UK Open Banking AISP app while the OBReadDirectDebit2 response is in-flight from the HSBC sandbox API.

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, surfaceContainerHighest #313539, outline #8B9198, onSurfaceVariant #C1C7CE, surfaceVariant #41474D

**Component 1 - Top App Bar** (56dp, 393dp wide): title shimmer bar 120dp x 20dp #262A2E, back-arrow shimmer placeholder 24dp x 24dp #262A2E, container #101417, skeleton_screen archetype.

**Component 2 - Chip Row** (48dp, 361dp wide): two shimmer chip placeholders each 80dp x 32dp #262A2E radius 8dp, 8dp gap, representing Active and Inactive mandate count chips.

**Component 3 - List** (remaining height, 393dp wide): four shimmer Card placeholders container #1C2024 radius 12dp, 12dp vertical gap, 16dp horizontal insets. Each card 88dp tall: status-badge shimmer 60dp x 20dp #262A2E top-left, headline shimmer 120dp x 16dp #262A2E, amount-subline shimmer 180dp x 14dp #262A2E, mandate-ref shimmer 100dp x 12dp #262A2E. Shimmer sweep from #262A2E to #313539 to #262A2E over 1400ms ease-in-out, no bounce.

**Component 4 - Bottom Navigation Bar** (80dp, 393dp wide): container #1C2024, all tab icons #8B9198; navigation remains accessible while mandate data loads.

Do not use em-dash in any element. Do not reveal originator names, debit amounts, or mandate references during the skeleton state. Do not animate with spring or bounce easing; honor the low-motion dial 2 of the minimalist-ui design system. Do not hide or collapse the Top App Bar or Bottom Navigation Bar during the loading phase.

Four mandate card skeletons pulse in a restrained shimmer, #262A2E on #101417, Trust Blue #95CDF7 ready to illuminate Active badges as soon as mandate data arrives from OBReadDirectDebit2.

↑↑↑ MOCKUP PROMPT
