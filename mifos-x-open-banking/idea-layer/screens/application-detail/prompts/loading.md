---
ui_yaml_sha: 64d1e77304b15bebcf5570a91036dd5267b8a38e827f5a966cb61dd278263d6b
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 7ccc8a5efbd550d8aaa0f03d4fa79f62a29891aaa05e501a7051874aaa0d7332

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: application-detail
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# application-detail — loading state

> Auto-generated from screens/application-detail/ui.yaml @ SHA 85a744be8f3af52f
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the application-detail screen for **Mifos X Open Banking**, a professional open banking KMP super-app serving consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, tertiary #A0CFCB, on_tertiary #003735, error #FFB4AB, on_error #690005, error_container #93000A, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16, scrim #000000.

**Component 1 — App Bar** (64dp tall, full width): Back-arrow 24dp shimmer circle. Title shimmer 180dp x 18dp centered. Shimmer base #1E201A highlight #282A24, 1200ms sweep. Background #12140E. skeleton_screen archetype.

**Component 2 — Card** (full width minus 32dp insets, 12dp corner radius, top margin 16dp, background #1E201A, 16dp padding): Header shimmer 80dp x 12dp. Below row 56dp: shimmer 140dp x 16dp on left, shimmer link 80dp x 14dp on right. Same 1200ms cadence.

**Component 3 — Card** (full width minus 32dp insets, 12dp corner radius, top margin 12dp, background #1E201A, 16dp padding): Header shimmer 120dp x 12dp. Three row shimmers each 56dp tall with 1dp #282A24 dividers. Row 1: shimmer 80dp x 14dp + shimmer 140dp x 14dp. Row 2: shimmer 80dp x 14dp + shimmer 100dp x 14dp. Row 3: shimmer 60dp x 14dp + shimmer 180dp x 14dp.

**Component 4 — List Row** (full width minus 32dp insets, top margin 12dp, 48dp tall, background #1E201A, 12dp corner radius, 16dp padding): Circle shimmer 20dp + shimmer 160dp x 14dp. Same cadence.

**Component 5 — Card** (full width minus 32dp insets, 12dp corner radius, top margin 16dp, background #1E201A, 16dp padding): Header shimmer 140dp x 12dp. Two document row shimmers each 64dp tall with 1dp divider. Each: square shimmer 40dp + two text shimmers stacked + trailing shimmer 48dp x 32dp.

**Component 6 — Text Field shimmer** (full width minus 32dp insets, top margin 16dp, 96dp tall, 12dp corner radius, shimmer #1E201A highlight #282A24).

**Component 7 — Button shimmer** (full width minus 32dp insets, 48dp tall, 24dp corner radius, top margin 16dp, shimmer base #1E201A highlight #282A24).

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Shimmer placeholders use surface_container #1E201A as rest tone with surface_container_high #282A24 as highlight pulse, keeping the skeleton_screen calm and structured against deep #12140E, matched block-for-block to the content layout.
↑↑↑ MOCKUP PROMPT
