---
ui_yaml_sha: 43bf8e879b37ae93b3ce62dd72bfb9fee6978b31c734296cf84770dbd633d439
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: ab89b65c0d68b3299f6b92324ab85575fe12ab0f04d3e4b4bc89c6348aa3daac

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: direct-debit-detail
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# direct-debit-detail — loading state

> Auto-generated from screens/direct-debit-detail/ui.yaml @ SHA e393789eddb3ffce
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the direct-debit-detail screen for **Mifos X Open Banking**, a mobile KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, error #FFB4AB, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title shimmer 100dp x 20dp centered. Background #12140E, shimmer base #1E201A highlight #282A24. skeleton_screen shimmer layout.

**Component 2 — Hero** (centered, top margin 24dp): 64dp circle shimmer #282A24. Below: 160dp x 20dp text shimmer centered + 80dp x 14dp text shimmer centered top 8dp + 60dp x 24dp badge shimmer top 8dp. All shimmer 1200ms sweep.

**Component 3 — App Bar** (centered, top margin 16dp): 80dp x 32dp amount shimmer + 60dp x 14dp frequency shimmer stacked.

**Component 4 — Card** (full width minus 32dp insets, top margin 24dp): surface_container #1E201A 12dp radius. Header shimmer 120dp x 15dp. 4 list rows each 52dp tall: label shimmer 80dp x 12dp left, value shimmer 120dp x 14dp right, 1dp #44483D dividers. All #282A24.

**Component 5 — Card** (full width minus 32dp insets, top margin 16dp): surface_container #1E201A 12dp radius. Header row: 120dp shimmer left + 50dp shimmer right. 3 history rows each 56dp tall: date shimmer 70dp + status shimmer 60dp + amount shimmer 50dp right. Dividers #44483D.

**Component 6 — Button** (full width minus 32dp insets, top margin 24dp): 2 button shimmers 48dp, 12dp radius, #282A24, 8dp gap.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. The skeleton_screen shimmer rests on #1E201A with #282A24 pulse, maintaining a calm and balanced tone throughout the taste-default banking loading experience.
↑↑↑ MOCKUP PROMPT
