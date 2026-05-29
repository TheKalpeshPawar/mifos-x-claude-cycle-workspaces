---
ui_yaml_sha: 4af6ba2fca8822ef1afa49c6800612d2eccac67ae5dd199e1c88a785018712c8
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: ac22ab906faf68fafe219d0c81a9fa91c8e9f51580cdfffd1416886db4e7e95a

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: fo-dashboard
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# fo-dashboard — loading state

> Auto-generated from screens/fo-dashboard/ui.yaml @ SHA c9a573cd0ef71958
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the fo-dashboard screen for **Mifos X Open Banking**, a Open Banking KMP super-app for consumer retail banking and field officer agent banking in emerging markets.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, outline #8F9285, pending #E8A317.

**Component 1 — App Bar Shimmer** (64dp tall, full width): Shimmer placeholder rectangle 160dp wide x 20dp tall top-left with 16dp padding. Background #12140E. Shimmer base #1E201A, highlight #282A24, animation duration 1200ms horizontal sweep. skeleton_screen archetype.

**Component 2 — Grid Shimmer** (full width minus 32dp insets, top margin 20dp, 2-column grid 12dp gap): 4 shimmer card blocks each 80dp tall, 12dp corner radius, base #1E201A, highlight #282A24. Same 1200ms shimmer cadence.

**Component 3 — List Row Shimmer** (full width minus 32dp insets, top margin 24dp): Section header shimmer 120dp wide x 16dp tall. Below it 3 shimmer card blocks each 72dp tall, 12dp corner radius, 12dp gap. Each card: one text-line shimmer 240dp x 14dp and one button shimmer 100dp x 36dp, 18dp corner radius.

**Component 4 — Card Shimmer** (full width minus 32dp insets, top margin 12dp, 72dp tall, 12dp corner radius): Single shimmer card with text-line shimmer 200dp x 14dp and button shimmer 120dp x 36dp right-aligned.

**Component 5 — List Row Shimmer** (full width minus 32dp insets, top margin 24dp): Section header shimmer 140dp wide x 16dp tall. Below it 2 rows each 56dp tall. Each row: time shimmer 60dp x 14dp left, detail shimmer 180dp x 14dp right, 1dp divider shimmer #282A24.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full scrollable layout on pure #12140E. Shimmer placeholders use surface_container #1E201A as rest tone with #282A24 as the highlight pulse, keeping loading calm and grounded for field officers awaiting data sync.

↑↑↑ MOCKUP PROMPT
