---
ui_yaml_sha: cef07cfa2ad24b80737c28638685e2e4d53b2eb4711914b0fcd2363e8d0b95e7
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 099cf5f279d8242764b6f95913a10aa601fe6a6e1a8fcf4a03fed32d2d8b9881

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: about
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# about — loading state

> Auto-generated from screens/about/ui.yaml @ SHA c20e6fa56222dd56
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the about screen for **Mifos X Open Banking**, a professional open banking KMP super-app serving consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, tertiary #A0CFCB, on_tertiary #003735, error #FFB4AB, on_error #690005, error_container #93000A, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16, scrim #000000.

**Component 1 — App Bar** (64dp tall, full width): Shimmer placeholder rectangle 120dp wide x 20dp tall, centered. Shimmer base #1E201A, highlight sweep #282A24, animation 1200ms horizontal sweep. Background #12140E. skeleton_screen archetype.

**Component 2 — Card** (full width minus 32dp insets, 12dp corner radius, top margin 24dp, background #1E201A): Circular shimmer placeholder 72dp diameter centered with 16dp top padding. Below: rectangle shimmers 160dp wide x 20dp tall top margin 12dp, and 120dp wide x 14dp tall top margin 6dp. Card bottom padding 16dp. Same 1200ms shimmer cadence.

**Component 3 — Card** (full width minus 32dp insets, 12dp corner radius, top margin 16dp, background #1E201A): Two row shimmers each 56dp tall separated by 1dp #282A24 divider. Each row: left rectangle 60dp wide x 14dp, right rectangle 80dp wide x 14dp, shimmer base #1E201A highlight #282A24.

**Component 4 — Card** (full width minus 32dp insets, 12dp corner radius, top margin 16dp, background #1E201A): Header shimmer 100dp wide x 12dp with 16dp horizontal padding, 40dp tall container. Three list row shimmers each 56dp tall separated by 1dp #282A24 dividers. Each: 140dp wide x 14dp shimmer with 18dp trailing circle shimmer.

**Component 5 — Button** (full width minus 64dp insets, 48dp tall, 24dp corner radius, top margin 24dp): Shimmer rectangle same shape as button, base #1E201A highlight #282A24, 1200ms sweep.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Shimmer placeholders use surface_container #1E201A as rest tone with surface_container_high #282A24 as highlight pulse, keeping the skeleton_screen calm and warm against the deep #12140E background.
↑↑↑ MOCKUP PROMPT
