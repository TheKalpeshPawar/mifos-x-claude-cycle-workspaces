---
ui_yaml_sha: 211923c9f8558a327f161786a206bf7a76aa3989313d251dec81b13885e4ee21
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: d4dccd4ebaad5f0817ab9363e12849b886bc97f7db2c0873dea6cb85806f4ab8

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: customer-search
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# customer-search — loading state

> Auto-generated from screens/customer-search/ui.yaml @ SHA 276dd3f09a65794f
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the customer-lookup screen for **Mifos X Open Banking**, a mobile KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, error #FFB4AB, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title shimmer 100dp x 20dp top-left 16dp inset. Background #12140E, shimmer base #1E201A highlight #282A24. skeleton_screen archetype.

**Component 2 — List Row** (full width minus 32dp insets, top margin 16dp): Lookup field shimmer 48dp tall, 24dp radius, #282A24. Below, chip row shimmer: 4 chips 32dp x 56dp each, 8dp gap, shimmer #282A24.

**Component 3 — List Row** (full width minus 32dp insets, top margin 16dp): 3 customer card shimmers. Each shimmer card surface_container #1E201A 12dp radius 72dp tall, 8dp gap: 40dp circle shimmer left, right column 120dp x 15dp shimmer + 80dp x 12dp shimmer + 100dp x 12dp shimmer stacked 4dp gap. All shimmer #282A24, sweep 1200ms.

**Component 4 — Button** (full width minus 32dp insets, top margin 16dp): 2 button shimmers 48dp x full-width, 12dp radius, #282A24, 8dp gap.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Layout on #12140E. Shimmer placeholders #1E201A rest and #282A24 highlight maintain the skeleton_screen calm that matches the professional taste-default banking aesthetic.
↑↑↑ MOCKUP PROMPT
