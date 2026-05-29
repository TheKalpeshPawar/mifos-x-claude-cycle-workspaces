---
ui_yaml_sha: de0c641bb5454eb6bb91af4ba18a416b141b46ce0b2cad2598e56a2732ce7577
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 041fc3e4bba604c3e223aebb9cf6f418047fe751bc04b0e5150aa3d471454202

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: profile
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# profile — loading state

> Auto-generated from screens/profile/ui.yaml @ SHA bd8d743dbb80567d
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the profile screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar Shimmer** (64dp tall, full width): Title placeholder 120dp wide, 20dp tall, centered shimmer. Shimmer base #1E201A, highlight #282A24, 1200ms. Background #12140E. skeleton_screen archetype.

**Component 2 — Avatar Shimmer** (centered, top margin 24dp): 96dp circular shimmer base #282A24. Below it two stacked text-line shimmers: 120dp wide (name) + 160dp wide (email).

**Component 3 — Section Header Shimmer** (full width minus 32dp insets, top margin 24dp): 140dp wide, 14dp tall shimmer.

**Component 4 — Text Field Shimmer 1** (full width minus 32dp insets, top margin 8dp, 56dp tall, 12dp radius): Outlined shimmer #44483D, inner shimmer block 80% width, 20dp tall.

**Component 5 — Text Field Shimmer 2** (full width minus 32dp insets, top margin 12dp): Same as Component 4.

**Component 6 — Text Field Shimmer 3** (full width minus 32dp insets, top margin 12dp): Same.

**Component 7 — Button Shimmer 1** (full width minus 32dp insets, top margin 24dp, 48dp tall, pill radius): Shimmer base #354E16.

**Component 8 — Button Shimmer 2** (full width minus 32dp insets, top margin 8dp, 48dp tall, pill radius): Shimmer base #282A24.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The avatar circle shimmer and field-shaped skeleton_screen placeholders match the layout precisely, making the #1E201A to #282A24 pulse feel calm and restrained, signaling imminent data arrival.

↑↑↑ MOCKUP PROMPT
