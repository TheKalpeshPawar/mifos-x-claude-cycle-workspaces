---
ui_yaml_sha: 06a74a064d747a5df855d29ceca0a54efe2937d3362989fcd2a1e8391bb18936
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 208d90938e49fd45e9340cdfa7dd4892e432c543c660b87287a89d93af7e15ad

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: accounts
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# accounts — loading state

> Auto-generated from screens/accounts/ui.yaml @ SHA 631de78b3db00775
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the accounts screen for **Mifos X Open Banking**, a professional open banking KMP super-app serving consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, tertiary #A0CFCB, on_tertiary #003735, error #FFB4AB, on_error #690005, error_container #93000A, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16, scrim #000000.

**Component 1 — App Bar** (64dp tall, full width): Title shimmer 140dp wide x 22dp, left-aligned 16dp. Trailing circle shimmer 24dp. Base #1E201A, highlight #282A24, 1200ms sweep. Background #12140E. skeleton_screen archetype.

**Component 2 — Chip Row** (full width minus 32dp insets, top margin 12dp, 8dp gap): Four chip shimmer rectangles each 72dp wide x 32dp tall, 16dp corner radius. Base #1E201A highlight #282A24, same 1200ms cadence.

**Component 3 — Card** (full width minus 32dp insets, 16dp corner radius, top margin 16dp, background #1E201A, 16dp padding): Header row: shimmer 120dp x 16dp on left, shimmer badge 60dp x 20dp on right. Balance shimmer 100dp x 28dp top margin 10dp. IBAN row top margin 10dp: shimmer 16dp circle + shimmer 200dp x 12dp.

**Component 4 — Card** (full width minus 32dp insets, 16dp corner radius, top margin 12dp, background #1E201A, 16dp padding): Header: shimmer 130dp x 16dp on left, shimmer badge 60dp x 20dp on right. Balance shimmer 110dp x 28dp top margin 10dp. IBAN: shimmer circle 16dp + shimmer 200dp x 12dp top margin 10dp.

**Component 5 — Card** (full width minus 32dp insets, 16dp corner radius, top margin 12dp, background #1E201A, 16dp padding): Same 3-row shimmer pattern: header row, balance row, IBAN row. All shimmer base #1E201A highlight #282A24.

**Component 6 — List Row** (full width minus 32dp insets, top margin 16dp): 1dp divider shimmer #282A24. Footer row 56dp tall: shimmer 140dp x 13dp on left, shimmer 90dp x 18dp on right.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Shimmer placeholders use surface_container #1E201A as rest tone with surface_container_high #282A24 as highlight pulse, keeping the skeleton_screen calm and structured against deep #12140E.
↑↑↑ MOCKUP PROMPT
