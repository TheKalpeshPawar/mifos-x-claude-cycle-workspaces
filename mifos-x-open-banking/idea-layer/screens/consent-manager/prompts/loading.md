---
ui_yaml_sha: 77ef7dbe843044a66b73b3c529d340294fe8b8804fa009b3a4c22aa5f5ddacab
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 5ee2d3569e821f6bec288d4a481d14bca9ceee5a4654af3b335558b858a0284c

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: consent-manager
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-manager — loading state

> Auto-generated from screens/consent-manager/ui.yaml @ SHA 064719313fb43dec
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the consent manager screen for **Mifos X Open Banking**, a professional open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, secondary #A0CFCB, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317.

**Component 1 — App Bar Shimmer** (64dp tall, full width): Title shimmer rectangle 120dp wide 20dp tall centered, shimmer base #1E201A highlight #282A24 sweep 1200ms, background #12140E.

**Component 2 — Card Shimmer** (full width minus 32dp insets, 96dp tall, 12dp corner radius, top margin 24dp): Header row shimmer: 40dp circle left, two stacked rectangles 160dp and 100dp wide right. Chip Row shimmer: 3 pill shapes 72dp wide 28dp tall, 8dp gap. Button shimmer rectangle full width 44dp tall. skeleton_screen archetype. All shimmer: base #1E201A, highlight #282A24, 1200ms cadence.

**Component 3 — Card Shimmer** (same dimensions, top margin 12dp): Identical to Component 2, 2 chip shapes.

**Component 4 — Card Shimmer** (same dimensions, top margin 12dp): Identical to Component 2, 1 chip shape.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. Shimmer uses surface_container #1E201A as rest tone and surface_container_high #282A24 as highlight pulse, keeping the loading state calm and unobtrusive within the trusted financial aesthetic.

↑↑↑ MOCKUP PROMPT
