---
ui_yaml_sha: b176ea2d469f885b24e961885ac2755e38a0e1865e6d2f063caf8d6eec8ce214
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: f724ee4892d96aeec3c7cfcec1ac4341c3412fe9927d43e36922d3d7db091df2

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: scheduled-payments
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# scheduled-payments — loading state

> Auto-generated from screens/scheduled-payments/ui.yaml @ SHA b3be4d8f02ac3258
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the scheduled-payments screen for **HSBC Open Banking**, a UK AISP reference app fetching future-dated payment data via OBReadScheduledPayment3 from HSBC, within the Trust Blue minimalist Material 3 dark system on a 393x852dp Pixel 5.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, surfaceContainerHighest #313539, onSurfaceVariant #C1C7CE, outline #8B9198, primaryContainer #004B6F

**Component 1 - Top App Bar** (full width, 64dp, bg #101417): back-arrow icon #C1C7CE left; shimmer bar 120x18dp at title position in #262A2E with left-to-right #313539 highlight sweep; no real text shown.

**Component 2 - List** (361dp wide, bg #101417): 4 skeleton Card rows, 8dp gap, 16dp horizontal padding; skeleton_screen archetype.

**Component 3 - Card** (361x96dp, r=12dp, bg #1C2024): shimmer bar 160x16dp top-left #262A2E for payee name; shimmer bar 80x16dp top-right #262A2E for amount; shimmer bar 120x14dp center-left #262A2E for execution date; shimmer bar 100x12dp bottom-left #262A2E for reference; all bars animate with synchronized #313539 sweep.

**Component 4 - Card** (361x96dp, r=12dp, bg #1C2024): identical 4-bar shimmer pattern to Component 3.

**Component 5 - Card** (361x96dp, r=12dp, bg #1C2024): identical 4-bar shimmer pattern.

**Component 6 - Card** (361x96dp, r=12dp, bg #1C2024): identical 4-bar shimmer pattern; no text visible anywhere in the List.

**Component 7 - Bottom Navigation Bar** (full width, 80dp, bg #1C2024): items "Home", "Accounts", "Payments", "More" in static #C1C7CE; navigation is not shimmered; "Payments" icon slightly elevated brightness.

Do not reveal any real payee names, amounts, dates, or references; all data positions hold shimmer bars exclusively. Do not overlay a circular spinner on top of the skeleton Cards; shimmer sweep within each Card is the only loading indicator. Do not reduce Card height during loading; skeleton Cards maintain the 361x96dp footprint matching the content state exactly. Do not show an Empty State or Error State component in the loading view.

Patient anticipation. Layout mirrors content geometry precisely. No data revealed prematurely. Tone: restrained, #95CDF7 minimal.

↑↑↑ MOCKUP PROMPT
