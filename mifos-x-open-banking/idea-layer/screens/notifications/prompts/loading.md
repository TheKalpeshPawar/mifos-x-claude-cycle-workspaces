---
ui_yaml_sha: 3fd23727025f84161f07e7aec5d0eac94651cf54a8c6617a21f7b92e54ebab5a
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 1c9a3cd8755933fc3538b4e3e88a8292c4cd8d2d993d9427662a01881c96c828

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: notifications
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# notifications — loading state

> Auto-generated from screens/notifications/ui.yaml @ SHA d569e442092a2399
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the notifications screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar Shimmer** (64dp tall, full width): Title placeholder shimmer rectangle 120dp wide, 20dp tall, left-aligned 16dp padding. Shimmer base #1E201A, highlight sweep #282A24, 1200ms horizontal animation. Background #12140E. skeleton_screen archetype.

**Component 2 — Section Header Shimmer** (full width minus 32dp insets, top margin 16dp): One shimmer rectangle 80dp wide, 16dp tall, simulating "Today" section label.

**Component 3 — List Row Shimmer 1** (full width minus 32dp insets, top margin 12dp, 72dp tall): Circular shimmer 40dp left for icon background, two stacked text-line shimmers 180dp + 120dp on right, timestamp shimmer 48dp bottom-right. Corner radius 12dp.

**Component 4 — List Row Shimmer 2** (full width minus 32dp insets, top margin 8dp, 72dp tall): Same structure as Component 3 — icon circle + two text lines + timestamp, shimmer base #1E201A.

**Component 5 — Section Header Shimmer 2** (full width minus 32dp insets, top margin 24dp): One shimmer rectangle 72dp wide, 16dp tall, simulating "Earlier" label.

**Component 6 — List Row Shimmer 3** (full width minus 32dp insets, top margin 12dp, 72dp tall): Same layout, two text-line shimmers 200dp + 140dp.

**Component 7 — List Row Shimmer 4** (full width minus 32dp insets, top margin 8dp, 72dp tall): Same structure, 160dp + 100dp text shimmers. No real labels.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The shimmer palette of #1E201A base with #282A24 highlight keeps the skeleton_screen calm and warm rather than anxious, with each sweep suggesting imminent arrival of notification data.

↑↑↑ MOCKUP PROMPT
