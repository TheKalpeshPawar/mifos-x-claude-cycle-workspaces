---
ui_yaml_sha: a1448cadef7246768dbb0cfbf2db2a732fde45be45f4f072a644677b222e1f9f
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 4349e0a8c6137c24d3c497f064198859cd9ce440b5117b39a4c4447676447836

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: standing-order-detail
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# standing-order-detail — loading state

> Auto-generated from screens/standing-order-detail/ui.yaml @ SHA 03b35bac920f8225
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the standing order detail screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar Shimmer** (64dp tall, full width): Shimmer rectangle 160dp wide x 20dp tall, centered. Shimmer base #1E201A, highlight #282A24, 1200ms sweep. Background #12140E. skeleton_screen archetype.

**Component 2 — Card Shimmer** (full width minus 32dp insets, top margin 24dp, 16dp corner radius, background #1E201A): Header card placeholder. Title shimmer 120dp wide x 22dp tall centered. Badge shimmer 60dp wide x 24dp tall below, 12dp corner radius. Total height approx 80dp.

**Component 3 — Card Shimmer** (full width minus 32dp insets, top margin 12dp, 16dp corner radius, background #1E201A): Beneficiary section. Header shimmer 72dp wide x 12dp tall. Three row shimmers 44dp tall each with 1dp divider #282A24 between. Each row: left label shimmer 60dp wide x 12dp, right value shimmer 120dp wide x 14dp.

**Component 4 — Card Shimmer** (full width minus 32dp insets, top margin 12dp, 16dp corner radius, background #1E201A): Schedule section. Header shimmer 56dp wide x 12dp tall. Four row shimmers 44dp tall with dividers. Same row anatomy.

**Component 5 — Card Shimmer** (full width minus 32dp insets, top margin 12dp, 16dp corner radius, background #1E201A): Amount section. Header shimmer. Amount row: large value shimmer 100dp wide x 28dp tall + small badge shimmer 40dp wide x 20dp.

**Component 6 — Card Shimmer** (full width minus 32dp insets, top margin 12dp, 16dp corner radius, background #1E201A): History section. Header shimmer. Five row shimmers 44dp tall each with dividers. Each row: date shimmer 80dp left, status shimmer 80dp center, amount shimmer 64dp right.

**Component 7 — Button Row Shimmer** (full width minus 32dp insets, top margin 16dp, bottom 32dp): Two pill shimmers 48dp tall each, 999dp corner radius, first 60% width background #354E16, second 60% width background #1E201A, 12dp gap between.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. Shimmer placeholders use #1E201A rest tone with #282A24 highlight at 1200ms cadence, creating a calm structured skeleton_screen matching the five grouped card sections of the content state, balanced and restrained for this regulated open banking aesthetic.

↑↑↑ MOCKUP PROMPT
