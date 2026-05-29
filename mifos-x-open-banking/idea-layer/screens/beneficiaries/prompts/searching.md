---
ui_yaml_sha: a37ab086ed21a953df7bf0a7272221f8d846dd091086643f77aeaf43d90882ef
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 9220a08c0c74c7d45cb84882c1a06122bf26231d5fe8bf9d8bc5ca797677e7e2

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: beneficiaries
state: searching
state_visibility: searching

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# beneficiaries — searching state

> Auto-generated from screens/beneficiaries/ui.yaml @ SHA 9686e8b05de5cc77
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the searching state of the Beneficiaries screen for **Mifos X Open Banking**, a open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB.

**Component 1 — App Bar** (64dp tall, full width): Title "Beneficiaries" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow icon 24dp tinted #B2D188. Zero elevation, background #12140E.

**Component 2 — Text Field** (full width minus 32dp insets, top margin 16dp): Active outlined lookup field 48dp tall, 24dp corner radius, value "Patel" Outfit Regular 14sp #E3E3D8, focused outline 1dp #B2D188, leading lookup icon 20dp #B2D188, trailing clear-X icon 20dp #C5C8BA.

**Component 3 — List Row** (full width minus 32dp insets, top margin 16dp): Section label "Search Results" Outfit SemiBold 13sp #8F9285 uppercase, right-aligned count "1 result" Outfit Regular 12sp #8F9285.

**Component 4 — Card** (full width minus 32dp insets, top margin 8dp): surfaceContainer #1E201A background, 12dp corner radius, 16dp padding. Leading Santander logo 32dp rounded square. Title "Priya Patel" Outfit SemiBold 15sp #E3E3D8, with "Patel" segment highlighted #B2D188 background #354E16. Subtitle "GB72 ABBY 4421" Outfit Regular 13sp #C5C8BA. Footer "Santander UK, Last payment: 8 May 2026" Outfit Regular 12sp #8F9285.

**Component 5 — Card** (full width minus 32dp insets, top margin 12dp): surfaceContainer #1E201A background, 12dp corner radius, 16dp padding, centered. Icon person-find 32dp #44483D center. Caption "No more results for 'Patel'" Outfit Regular 13sp #8F9285 centered.

**Component 6 — FAB** (56dp diameter, anchored bottom-right 16dp): Circular FAB background #B2D188, plus icon 24dp #1F3701.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full layout on #12140E. The earth-green accent #B2D188 on the active lookup field and highlighted match text gives clear visual feedback — calm, balanced, and refined within the financial-stability banking context.
↑↑↑ MOCKUP PROMPT
