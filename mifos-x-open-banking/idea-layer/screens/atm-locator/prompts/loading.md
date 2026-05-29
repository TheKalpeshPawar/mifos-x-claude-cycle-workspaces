---
ui_yaml_sha: c8c8040af254236430df923e229edc7208f4a0e351a42c63baa151d487b8456e
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: d66c9e0a570c1a9b0ba82bd436bb59bd39ccac2aa158b8a904f854bdcad02432

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: atm-locator
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# atm-locator — loading state

> Auto-generated from screens/atm-locator/ui.yaml @ SHA 6273d53d435827f0
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the ATM Locator screen for **Mifos X Open Banking**, a open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB.

**Component 1 — App Bar Shimmer** (64dp tall, full width): Shimmer placeholder rectangle 120dp wide by 24dp tall, centered with 16dp horizontal padding. Shimmer base #1E201A, highlight #282A24, animation duration 1200ms horizontal sweep. Background #12140E, zero elevation. skeleton_screen archetype.

**Component 2 — Text Field Shimmer** (full width minus 32dp insets, top margin 16dp): Rectangular shimmer block 56dp tall, 12dp corner radius, same shimmer animation cadence.

**Component 3 — Card Shimmer** (full width minus 32dp insets, top margin 12dp): Rectangular shimmer block 56dp tall, 12dp corner radius, surfaceContainer #1E201A rest with #282A24 sweep.

**Component 4 — Chip Row Shimmer** (full width minus 32dp insets, top margin 16dp, horizontally scrollable): 4 chip-shaped shimmer placeholders, each 80dp wide by 32dp tall, 16dp corner radius, 8dp gap. Same sweep cadence.

**Component 5 — Section Header Shimmer** (full width minus 32dp insets, top margin 16dp): Single shimmer rectangle 160dp wide by 16dp tall.

**Component 6 — Card Shimmer** (full width minus 32dp insets, top margin 8dp): Rectangular shimmer block 112dp tall, 12dp corner radius. Contains an icon placeholder 20dp by 20dp on left, two text line shimmers 180dp and 120dp stacked on right, and one 80dp by 16dp shimmer line at bottom.

**Component 7 — Card Shimmer** (full width minus 32dp insets, top margin 8dp): Same shape as Component 6, 96dp tall.

**Component 8 — Card Shimmer** (full width minus 32dp insets, top margin 8dp, bottom 24dp): Same shimmer card 128dp tall with three text lines.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full scrollable layout on #12140E. Shimmer placeholders use surfaceContainer #1E201A as rest tone with #282A24 as the highlight pulse, keeping the loading state calm and restrained throughout.
↑↑↑ MOCKUP PROMPT
