---
ui_yaml_sha: 1983cf22e27c82c37217e6ab750b592b1c3060b8a44f50772fe8f978542b961c
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: ad80393b9bd6e1acafcec1dbc38c9632c2a558c53cc46e19e1f20816edfc6ba5

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: customer-messages
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# customer-messages — loading state

> Auto-generated from screens/customer-messages/ui.yaml @ SHA 04332e5d080770ce
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the customer messages screen for **Mifos X Open Banking**, a professional open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, secondary #A0CFCB, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317.

**Component 1 — App Bar Shimmer** (64dp tall, full width, background #12140E): Title shimmer 100dp wide 20dp, badge shimmer 50dp wide 20dp right. Shimmer base #1E201A highlight #282A24 1200ms.

**Component 2 — Search Bar Shimmer** (full width minus 32dp insets, 48dp tall, 24dp corner radius, top margin 8dp, background #1E201A).

**Component 3 — List Row Shimmer** x4 (72dp tall each, full width, bottom divider 1dp #282A24): Each row: circle shimmer 40dp left, two stacked rects 160dp and 220dp wide right. skeleton_screen archetype.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. Shimmer base #1E201A and highlight #282A24 create a calm pulsing rhythm that signals loading without anxiety, matching the measured motion dial of the professional banking interface.

↑↑↑ MOCKUP PROMPT
