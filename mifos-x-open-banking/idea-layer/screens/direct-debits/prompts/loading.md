---
ui_yaml_sha: 311b028229aca9607374f911558008041fe6e2b5143fc5015fb945c2ad077cdc
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 041b06d1d7258e52f30d6102bc5e8944f92a6b97ef82350c8378cdb4b034cfa0

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: direct-debits
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# direct-debits — loading state

> Auto-generated from screens/direct-debits/ui.yaml @ SHA 904c39372c30f849
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the direct-debits screen for **Mifos X Open Banking**, a Open Banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, error #FFB4AB, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title shimmer 100dp x 20dp left 16dp. Shimmer base #1E201A highlight #282A24. Background #12140E. skeleton_screen archetype.

**Component 2 — Card** (full width minus 32dp insets, top margin 20dp): surface_container #1E201A 12dp radius shimmer card 96dp tall. Header row: name shimmer 80dp x 16dp left, badge shimmer 48dp x 22dp right. Amount shimmer 100dp x 18dp below header. Date shimmer 120dp x 12dp below amount. Ref shimmer 140dp x 12dp below date. All #282A24, sweep 1200ms.

**Component 3 — Card** (full width minus 32dp insets, top margin 12dp): Same shimmer card layout, 96dp tall, all #282A24.

**Component 4 — Card** (full width minus 32dp insets, top margin 12dp): Same shimmer card layout, 96dp tall, all #282A24 at 60% opacity.

**Component 5 — FAB** (56dp circle, bottom-right, 16dp margin): Shimmer circle #282A24.

**Component 6 — Bottom Nav** (64dp tall, full width): Icon shimmers 24dp + label shimmers 40dp x 10dp per tab. Background #1E201A, top 1dp #44483D. All #282A24.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. Shimmer rest #1E201A with highlight #282A24 keeps the skeleton_screen restrained and calm, anchored by the surface accent #B2D188 awaiting reveal.
↑↑↑ MOCKUP PROMPT
