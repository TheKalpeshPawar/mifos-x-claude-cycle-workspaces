---
ui_yaml_sha: ed2405e9b0ab40e84eddfcb7e669dd5d6df03b6a59f4997cb41c63dd2313c905
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: b0876a5326c463503f77f325c8d8fa87cecf53ef5623f39a4a48eaae85d6e0de

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: customer-profile
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# customer-profile — loading state

> Auto-generated from screens/customer-profile/ui.yaml @ SHA 61afecff225dc63c
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the customer-profile screen for **Mifos X Open Banking**, a professional open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, error #FFB4AB, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Shimmer rectangle 120dp x 24dp, top-left with 16dp inset. Shimmer base #1E201A, highlight sweep #282A24, animation 1200ms horizontal. Background #12140E. skeleton_screen archetype.

**Component 2 — List Row** (full width minus 32dp insets, top margin 24dp): Section heading shimmer 100dp x 14dp, #282A24. Below it, surface_container #1E201A card 12dp radius. 6 shimmer rows each 56dp tall: each row has a 60dp x 12dp label shimmer left, 140dp x 15dp value shimmer right, 1dp #44483D bottom divider. Shimmer sweep animation shared 1200ms cadence.

**Component 3 — List Row** (full width minus 32dp insets, top margin 16dp): Section heading shimmer 60dp x 14dp #282A24. surface_container card. 3 rows each 56dp tall, shimmer pairs label/value same dimensions, dividers #44483D.

**Component 4 — List Row** (full width minus 32dp insets, top margin 16dp): Section heading shimmer 80dp x 14dp. surface_container card. 3 rows, shimmer pairs, dividers.

**Component 5 — Button** (full width minus 32dp insets, top margin 24dp, bottom 32dp): Shimmer rectangle 48dp tall, 12dp radius, #282A24 background.

**Component 6 — Bottom Nav** (64dp tall, full width, anchored bottom): 4 tab icon shimmers 24dp each, label shimmers 32dp x 10dp. Background #1E201A, top 1dp #44483D. All shimmer #282A24.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full scrollable layout on #12140E. Shimmer rest tone #1E201A with highlight pulse #282A24 keeps the skeleton_screen state calm and minimal, conveying the professional stability of the banking aesthetic.
↑↑↑ MOCKUP PROMPT
