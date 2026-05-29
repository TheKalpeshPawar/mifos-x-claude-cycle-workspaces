---
ui_yaml_sha: 0d92768a4d5ddf82143347d12811e4d5c43b46201bead5239e2c5443c0a89f3b
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: df13dc3b42ccb4f96c9b975d464c200517da62bc34447b33bbf12ca60f60b0bc

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: consumer-home
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consumer-home — loading state

> Auto-generated from screens/consumer-home/ui.yaml @ SHA ce8b178ee7315e08
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the consumer home screen for **Mifos X Open Banking**, a professional open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, secondary #A0CFCB, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317.

**Component 1 — App Bar Shimmer** (56dp tall, full width, background #12140E): Title shimmer rectangle 140dp wide 20dp tall, notification icon shimmer 24dp circle. Shimmer base #1E201A highlight #282A24 1200ms sweep.

**Component 2 — Card Shimmer** (balance card, full width minus 32dp insets, 120dp tall, 16dp corner radius, top margin 16dp): Label shimmer 80dp wide 14dp. Amount shimmer 180dp wide 36dp top margin 8dp. Sub-row: two columns each 120dp wide with two stacked shimmer rects. skeleton_screen archetype.

**Component 3 — Chip Row Shimmer** (full width minus 32dp insets, top margin 20dp): 4 pill shimmers 80dp wide 36dp tall 8dp gap.

**Component 4 — Section Header Shimmer** (top margin 20dp): Two shimmer rects 160dp and 60dp wide 16dp tall.

**Component 5 — List Row Shimmer** x3 (56dp tall each, 8dp corner radius, full width minus 32dp, 4dp gap): Each row two shimmer rects 160dp and 80dp wide.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. Shimmer uses surface_container #1E201A as rest tone with surface_container_high #282A24 as highlight, keeping the loading state calm and unobtrusive within the trusted open banking aesthetic.

↑↑↑ MOCKUP PROMPT
