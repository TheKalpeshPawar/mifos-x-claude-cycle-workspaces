---
ui_yaml_sha: 993761900d60ef7be1f81c63930e46c519c3c997ab0e078c4e378490b32f227c
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 4e55aecd3342cf5f7407985ea6017c2d3a032a1ce0b8266fbb42598a353f8977

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: standing-orders
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# standing-orders — loading state

> Auto-generated from screens/standing-orders/ui.yaml @ SHA 97039a7a784d252c
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the Standing Orders screen for **HSBC Open Banking**, a UK Open Banking AISP app while the OBReadStandingOrder6 response is in-flight from the HSBC sandbox.

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, surfaceContainerHighest #313539, outline #8B9198, onSurfaceVariant #C1C7CE, surfaceVariant #41474D

**Component 1 - Top App Bar** (56dp, 393dp wide): title shimmer bar 160dp x 20dp #262A2E, back-arrow shimmer 24dp x 24dp #262A2E, container #101417, skeleton_screen archetype.

**Component 2 - Stat Block** (40dp, 361dp wide): single shimmer bar 120dp x 14dp #262A2E representing the Active / Inactive summary line.

**Component 3 - List** (remaining height, 393dp wide): five shimmer Card placeholders container #1C2024 radius 12dp, 12dp vertical gap, 16dp insets. Each card 96dp tall: status-badge shimmer 60dp x 20dp #262A2E top-left, headline shimmer 140dp x 16dp #262A2E, amount shimmer 80dp x 14dp #262A2E, frequency shimmer 200dp x 12dp #262A2E, footer shimmer 160dp x 12dp #262A2E. Shimmer sweep #262A2E to #313539 to #262A2E over 1400ms ease-in-out, no bounce, low-motion compliant.

**Component 4 - Bottom Navigation Bar** (80dp, 393dp wide): container #1C2024, all tab icons #8B9198; navigation remains accessible while standing-order data loads.

Do not use em-dash in any element. Do not reveal any payee name, amount, or frequency during this skeleton state. Do not animate with spring or high-velocity easing; adhere to the low-motion dial 2 of the minimalist-ui system. Do not collapse or hide the Top App Bar or Bottom Navigation Bar during loading.

Five mandate card skeletons animate in a calm pulse in #262A2E on the #101417 surface, Trust Blue #95CDF7 standing by for Active badges once standing-order data resolves.

↑↑↑ MOCKUP PROMPT
