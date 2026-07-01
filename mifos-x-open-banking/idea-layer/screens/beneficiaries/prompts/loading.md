---
ui_yaml_sha: d9ae9d4b46f8c880e1bdab3fb08cc6bf8df99140964c3c5557cba8f389363eda
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: bee973ab89d569264a244e6913655eaf3e3e4688dd16dc40c2b96901c6528e01

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: beneficiaries
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# beneficiaries — loading state

> Auto-generated from screens/beneficiaries/ui.yaml @ SHA c2150d34dc225f1e
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the Beneficiaries screen for **HSBC Open Banking**, a UK Open Banking AISP app while the OBReadBeneficiary5 response is in-flight from the HSBC sandbox API.

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, surfaceContainerHighest #313539, outline #8B9198, onSurfaceVariant #C1C7CE, surfaceVariant #41474D

**Component 1 - Top App Bar** (56dp, 393dp wide): title shimmer bar 120dp x 20dp #262A2E, back-arrow placeholder shimmer 24dp x 24dp #262A2E, container #101417, skeleton_screen archetype.

**Component 2 - Banner** (56dp, 361dp wide): search pill shimmer 361dp x 40dp #262A2E radius 28dp, sweep animates from #262A2E to #313539 to #262A2E over 1400ms ease-in-out, no text visible.

**Component 3 - List** (remaining height, 393dp wide): five shimmer row placeholders on surface #101417, each 80dp tall, 1dp divider #41474D. Each row: leading circle shimmer 40dp x 40dp #262A2E, center primary-text shimmer 160dp x 16dp #262A2E, secondary-text shimmer below it 120dp x 12dp #262A2E, trailing label shimmer 60dp x 20dp #262A2E. All shimmer blocks animate with sweep from #262A2E to #313539 over 1400ms, ease-in-out, no bounce, low-motion compliant.

**Component 4 - Bottom Navigation Bar** (80dp, 393dp wide): container #1C2024, all tab icons and labels in #8B9198; navigation remains functional so the user can leave the screen during loading.

Do not use em-dash in any visible element. Do not reveal any real payee name, account number, or reference during this skeleton state. Do not animate with spring, bounce, or high-velocity easing; honor the low-motion dial of the minimalist-ui design system. Do not collapse or hide the Top App Bar during loading.

Five shimmer rows animate in a calm rhythm in #262A2E on the #101417 surface, Trust Blue #95CDF7 standing by for active icons once payee data resolves.

↑↑↑ MOCKUP PROMPT
