---
ui_yaml_sha: 311407aa8bae098b271a0fcb7b6d0f6b1a2c6f6f1041ffea618960562714bf2e
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: bb5ec88893e767b694a1b664c53d67d4093ad9710a52159b08e347e80fc5a83a

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: account-applications
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# account-applications — loading state

> Auto-generated from screens/account-applications/ui.yaml @ SHA 554d2ba04a4e5093
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the account-applications screen for **Mifos X Open Banking**, a professional open banking KMP super-app serving consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, tertiary #A0CFCB, on_tertiary #003735, error #FFB4AB, on_error #690005, error_container #93000A, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16, scrim #000000.

**Component 1 — App Bar** (64dp tall, full width): Shimmer rectangle 180dp wide x 20dp tall, left-aligned 16dp horizontal padding. Shimmer base #1E201A, highlight #282A24, 1200ms horizontal sweep. Background #12140E. skeleton_screen archetype.

**Component 2 — Chip Row** (full width minus 32dp insets, top margin 12dp, 8dp gap): Four chip-shaped shimmer placeholders each 72dp wide x 32dp tall, 16dp corner radius. Same 1200ms shimmer cadence, base #1E201A highlight #282A24.

**Component 3 — Card** (full width minus 32dp insets, 12dp corner radius, top margin 16dp, background #1E201A, 16dp padding): Header row: shimmer rectangle 120dp wide x 16dp on left, shimmer chip 80dp wide x 24dp on right. Below: shimmer 160dp wide x 14dp top margin 8dp. Footer row top margin 16dp: shimmer 120dp wide x 12dp on left, shimmer button 64dp wide x 32dp on right. Same 1200ms cadence.

**Component 4 — Card** (full width minus 32dp insets, 12dp corner radius, top margin 12dp, background #1E201A, 16dp padding): Header: shimmer 140dp x 16dp on left, shimmer chip 80dp x 24dp on right. Middle: shimmer 180dp x 14dp top margin 8dp. Bottom: shimmer 120dp x 12dp top margin 12dp.

**Component 5 — Card** (full width minus 32dp insets, 12dp corner radius, top margin 12dp, background #1E201A, 16dp padding): Header: shimmer 100dp x 16dp on left, shimmer chip 80dp x 24dp on right. Middle: shimmer 160dp x 14dp top margin 8dp. Footer: shimmer 100dp x 12dp on left, shimmer link 80dp x 12dp on right, top margin 12dp.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Shimmer placeholders use surface_container #1E201A as rest tone with surface_container_high #282A24 as highlight, keeping the skeleton_screen calm and structured against the deep #12140E background.
↑↑↑ MOCKUP PROMPT
