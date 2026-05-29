---
ui_yaml_sha: f78a3dba3aff3089e2451e41f32781ab4fe14bcec47d87ec57ad572302aa3a0c
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 0dbca2ebdc57199dab82138b2f30b510ce88502897229716f5a30b8be1615426

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: standing-orders
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# standing-orders — loading state

> Auto-generated from screens/standing-orders/ui.yaml @ SHA 8d34ee1e147e827e
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the standing-orders screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317.

**Component 1 — App Bar Shimmer** (64dp tall, full width): Shimmer rectangle 120dp wide x 20dp tall top-center at 16dp vertical inset. Shimmer base #1E201A, highlight #282A24, horizontal sweep 1200ms. Background #12140E, zero elevation. skeleton_screen archetype.

**Component 2 — Header Row Shimmer** (full width minus 32dp insets, top margin 16dp): Shimmer rectangle 160dp wide x 24dp tall (title placeholder) left-aligned, and 64dp wide x 24dp tall (chip placeholder) with 12dp corner radius right-aligned. Same shimmer animation.

**Component 3 — Card Shimmer 1** (full width minus 32dp insets, top margin 16dp, 12dp corner radius, 80dp tall, background #1E201A): Row: 200dp x 18dp title shimmer left, 48dp x 18dp badge shimmer right. Below: 160dp x 14dp beneficiary shimmer top margin 8dp. Bottom row: 100dp x 14dp amount shimmer, 80dp x 14dp date shimmer.

**Component 4 — Card Shimmer 2** (full width minus 32dp insets, top margin 12dp, same spec as Component 3): Shimmer blocks at same proportions.

**Component 5 — Card Shimmer 3** (full width minus 32dp insets, top margin 12dp, same spec as Component 3): Shimmer blocks at same proportions.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full vertically scrollable layout on pure #12140E. Shimmer placeholders use surface_container #1E201A as rest tone with #282A24 as highlight pulse, keeping the loading state calm and financially composed rather than nervous, calibrated to the trustworthy open banking aesthetic.
↑↑↑ MOCKUP PROMPT
