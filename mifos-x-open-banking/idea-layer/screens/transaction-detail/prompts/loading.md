---
ui_yaml_sha: f9e175a0bb9de365db4c0803b856f44cd0182761536411bcd689e30e8f3ab0d5
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 9b5134e3697ff458aecd7f9819b2cc66ccb01eea1b218bba874ba27381d436ea

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: transaction-detail
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# transaction-detail — loading state

> Auto-generated from screens/transaction-detail/ui.yaml @ SHA 01ce909d9dad7671
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the transaction-detail screen for **HSBC Open Banking**, a UK AISP app showing shimmer skeleton placeholders while a single OBTransaction6 record loads from HSBC via the Open Banking API.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, secondary #B7C9D9, outline #8B9198

Archetype: skeleton_screen

**Component 1 - Top App Bar** (56dp h, full 393dp w, bg #101417): shimmer bar 160dp wide 20dp h replacing title text; leading arrow-back icon 24dp #E0E3E8 visible since navigation is always live; top-of-screen anchored.

**Component 2 - Stat Block** (full width, bg #101417, 24dp top padding, 16dp h-padding): centred shimmer pill 140dp x 40dp representing the hero amount region; below it a shimmer bar 220dp x 14dp for the merchant subline; status chip shimmer 80dp x 28dp rounded-full; all shimmer gradient sweeping over #262A2E base; no amount, merchant, or status text rendered.

**Component 3 - Card** (full width minus 32dp, 12dp radius, bg #1C2024): section-header shimmer bar 120dp x 14dp 16dp top-left inset; seven skeleton rows 56dp each with dividers #41474D; each row has shimmer bar 120dp x 12dp left and shimmer bar 160dp x 12dp right; no labels or values rendered.

**Component 4 - Bottom Navigation Bar** (56dp h, bg #1C2024, full width): four nav items at 30% opacity; no active-state highlight applied during loading.

DO NOT render any real amount, merchant name, date, category, or reference during the skeleton state. DO NOT use an em-dash or any visible text label in shimmer bars. DO NOT tint shimmer bars in #FFB4AB or #95CDF7 since those semantic colours apply only to resolved OBTransaction6 data. DO NOT show the error Banner or action Buttons while the transaction record is still being fetched.

Mood: calm and minimal skeleton state; #95CDF7 is fully absent throughout loading, keeping the dark #101417 surface silent until the OBTransaction6 record resolves into the content state.

↑↑↑ MOCKUP PROMPT
