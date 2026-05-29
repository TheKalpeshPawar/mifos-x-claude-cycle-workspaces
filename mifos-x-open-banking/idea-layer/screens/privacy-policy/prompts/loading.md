---
ui_yaml_sha: 0a37b7fd9f646c61727fc05be65e3aeffc9773a1b4f8cf66f1064cde39077166
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 98aae628db67e1d5293bf2828a0771f1fd1b579e9a90ae7cf03364f57af474cc

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: privacy-policy
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# privacy-policy — loading state

> Auto-generated from screens/privacy-policy/ui.yaml @ SHA b430a63027f14933
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the privacy-policy screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar Shimmer** (64dp tall, full width): Title placeholder shimmer 120dp wide, 20dp tall, centered. Back-arrow shimmer 24dp left. Shimmer base #1E201A, highlight #282A24, 1200ms. Background #12140E. skeleton_screen archetype.

**Component 2 — GDPR Banner Shimmer** (full width minus 32dp insets, top margin 16dp, 48dp tall, 12dp radius): Surface #282A24, two text-line shimmers 240dp + 180dp.

**Component 3 — Card Shimmer 1** (full width minus 32dp insets, top margin 12dp, 96dp tall, 12dp radius): Surface #1E201A. Section header shimmer 100dp. Three text-line shimmers 260dp / 220dp / 180dp.

**Component 4 — Card Shimmer 2** (full width minus 32dp insets, top margin 8dp, 96dp tall, 12dp radius): Same structure as Component 3.

**Component 5 — Card Shimmer 3** (full width minus 32dp insets, top margin 8dp, 80dp tall, 12dp radius): Surface #1E201A. Header shimmer 120dp. Two text-line shimmers 240dp / 200dp.

**Component 6 — Card Shimmer 4** (full width minus 32dp insets, top margin 8dp, 80dp tall, 12dp radius): Same structure.

**Component 7 — Card Shimmer 5** (full width minus 32dp insets, top margin 8dp, 64dp tall, 12dp radius): Header shimmer + one text-line shimmer.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The card-shaped skeleton_screen shimmers in #1E201A with #282A24 highlights mirror the policy content structure, keeping the loading state minimal and restrained, coherent with the overall screen layout.

↑↑↑ MOCKUP PROMPT
