---
ui_yaml_sha: 516c2b85d35f0d9def8fe28aea29060f67cb264db1e67fc0370922dde9b3af78
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 9be08623dd74db7a4e0c408f59ee87d672fb2d9700c2ea33bf2d6dcacf672713

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: terms-of-service
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# terms-of-service — loading state

> Auto-generated from screens/terms-of-service/ui.yaml @ SHA ce42b0ec4f511500
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the terms-of-service screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317.

**Component 1 — App Bar Shimmer** (64dp tall, full width): Center shimmer rectangle 120dp wide x 20dp tall. Shimmer base #1E201A, highlight #282A24, 1200ms sweep. Background #12140E. skeleton_screen archetype.

**Component 2 — Card Shimmer 1** (full width minus 32dp insets, top margin 16dp, 12dp corner radius, 80dp tall, background #1E201A): Header shimmer 120dp wide x 16dp tall, two body-line shimmers 280dp x 12dp and 200dp x 12dp with 6dp gap. All shimmer same spec.

**Component 3 — Card Shimmer 2** (full width minus 32dp insets, top margin 8dp, 80dp tall, same spec): Header 80dp, two body lines.

**Component 4 — Card Shimmer 3** (full width minus 32dp insets, top margin 8dp, 80dp tall): Same proportions.

**Component 5 — Card Shimmer 4** (full width minus 32dp insets, top margin 8dp, 80dp tall): Same proportions.

**Component 6 — Card Shimmer 5** (full width minus 32dp insets, top margin 8dp, 80dp tall): Same proportions.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full vertically scrollable layout on pure #12140E. Shimmer placeholders use surface_container #1E201A as rest tone with #282A24 as highlight pulse, keeping the loading state calm and professionally composed, calibrated to the regulated open banking aesthetic.
↑↑↑ MOCKUP PROMPT
