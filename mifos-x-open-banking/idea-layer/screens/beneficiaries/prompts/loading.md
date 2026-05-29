---
ui_yaml_sha: a37ab086ed21a953df7bf0a7272221f8d846dd091086643f77aeaf43d90882ef
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 50f04c2c22d3b19553531501673534e29cf5efcd8edf502464b8bd17740e6925

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: beneficiaries
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# beneficiaries — loading state

> Auto-generated from screens/beneficiaries/ui.yaml @ SHA 7c34bc96f845e53a
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the Beneficiaries screen for **Mifos X Open Banking**, a open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB.

**Component 1 — App Bar Shimmer** (64dp tall, full width): Shimmer rectangle 120dp wide by 24dp tall, centered. Base #1E201A, highlight #282A24, 1200ms horizontal sweep. Background #12140E. skeleton_screen archetype.

**Component 2 — Text Field Shimmer** (full width minus 32dp insets, top margin 16dp): Rectangular shimmer 48dp tall, 24dp corner radius pill. Same sweep.

**Component 3 — Section Header Shimmer** (full width minus 32dp insets, top margin 16dp): Single shimmer rectangle 100dp wide by 14dp tall.

**Component 4 — List Row Shimmer** (full width minus 32dp insets, top margin 8dp, 72dp tall): Leading 40dp circular shimmer avatar. Title shimmer 160dp by 16dp, subtitle shimmer 80dp by 12dp stacked on right, trailing shimmer 60dp by 12dp.

**Component 5 — List Row Shimmer** (full width minus 32dp insets, top margin 4dp, 72dp tall): Same row shimmer shape.

**Component 6 — List Row Shimmer** (full width minus 32dp insets, top margin 4dp, 72dp tall): Same row shimmer shape.

**Component 7 — Section Header Shimmer** (full width minus 32dp insets, top margin 16dp): Single shimmer 120dp by 14dp.

**Component 8 — Card Shimmer** (full width minus 32dp insets, top margin 8dp, 80dp tall): Leading 32dp square shimmer. Two text-line shimmers 180dp and 120dp, trailing 60dp by 12dp.

**Component 9 — Card Shimmer** (full width minus 32dp insets, top margin 8dp, bottom 24dp): Same shape, 80dp tall.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full scrollable layout on #12140E. Shimmer placeholders use surfaceContainer #1E201A rest with #282A24 sweep, keeping the loading state calm and restrained, anchored by the #B2D188 primary token for a minimal, balanced banking experience.
↑↑↑ MOCKUP PROMPT
