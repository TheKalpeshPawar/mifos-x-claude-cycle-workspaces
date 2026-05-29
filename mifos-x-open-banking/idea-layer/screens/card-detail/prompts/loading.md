---
ui_yaml_sha: 886497acc937d3f77eee431d1ffe01ed5447c84b05aaf98a8bff4c5dc9157014
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: fc67e06edda7a5e1410f611b29ee72b98aed2772634dad7fd2ca80caefea180b

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: card-detail
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# card-detail — loading state

> Auto-generated from screens/card-detail/ui.yaml @ SHA 7a62a1d97c0c3090
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the Card Detail screen for **Mifos X Open Banking**, a open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB.

**Component 1 — App Bar Shimmer** (64dp tall, full width): Centered shimmer rectangle 120dp by 24dp. Base #1E201A, highlight #282A24, 1200ms sweep. Background #12140E. skeleton_screen archetype.

**Component 2 — Card Shimmer** (full width minus 32dp insets, top margin 24dp, 192dp tall): Large rectangular shimmer 16dp corner radius, same sweep animation. Two thin shimmer lines at bottom (pan, cardholder), one top-right shimmer spot.

**Component 3 — Card Shimmer** (full width minus 32dp insets, top margin 16dp, 56dp tall): surfaceContainer #1E201A, 12dp corner radius. Row with 180dp shimmer label left, 40dp toggle-shape shimmer right.

**Component 4 — Card Shimmer** (full width minus 32dp insets, top margin 12dp, 112dp tall): surfaceContainer #1E201A, 12dp corner radius. Header shimmer 120dp, two rows each with 100dp + 80dp shimmers.

**Component 5 — Button Shimmer** (full width minus 32dp insets, top margin 16dp, 48dp tall): Outlined shimmer rectangle 12dp corner radius, base #1E201A.

**Component 6 — Button Shimmer** (full width minus 32dp insets, top margin 8dp, 48dp tall): Same shape.

**Component 7 — Button Shimmer** (full width minus 32dp insets, top margin 8dp, bottom 32dp, 48dp tall): Filled shimmer #282A24 corner radius 12dp.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full scrollable layout on #12140E. Shimmer uses surfaceContainer #1E201A rest with #282A24 sweep, producing a calm, professional loading state that matches the financial app trust profile.
↑↑↑ MOCKUP PROMPT
