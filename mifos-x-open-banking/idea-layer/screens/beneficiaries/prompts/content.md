---
ui_yaml_sha: a37ab086ed21a953df7bf0a7272221f8d846dd091086643f77aeaf43d90882ef
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: e97f6122a8f2576f1c7f27128cb98f5511b5b2a355f2e74067555d69d89c239a

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: beneficiaries
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# beneficiaries — content state

> Auto-generated from screens/beneficiaries/ui.yaml @ SHA 9ede893bad343e00
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the content state of the Beneficiaries screen for **Mifos X Open Banking**, a open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB.

**Component 1 — App Bar** (64dp tall, full width): Title "Beneficiaries" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow icon 24dp tinted #B2D188. Zero elevation, background #12140E.

**Component 2 — Text Field** (full width minus 32dp insets, top margin 16dp): Outlined lookup field 48dp tall, 24dp corner radius pill shape, label "Search" Outfit Regular 14sp #8F9285, leading lookup icon 20dp #C5C8BA, outline 1dp #44483D.

**Component 3 — List Row** (full width minus 32dp insets, top margin 16dp): Section label "Recently Used" Outfit SemiBold 13sp #8F9285 uppercase.

**Component 4 — List Row** (full width minus 32dp insets, top margin 8dp, 72dp tall): Leading 40dp circular avatar background #354E16, initials "JS" Outfit SemiBold 16sp #CDEDA3. Title "John Smith" Outfit SemiBold 15sp #E3E3D8. Subtitle "Barclays UK" Outfit Regular 13sp #C5C8BA. Trailing metadata "500 GBP, 2 days ago" Outfit Regular 12sp #8F9285.

**Component 5 — List Row** (full width minus 32dp insets, top margin 4dp, 72dp tall): Leading 40dp circular avatar #1F4E4B, initials "SW" Outfit SemiBold 16sp #BCEBE7. Title "Sarah Williams" Outfit SemiBold 15sp #E3E3D8. Subtitle "HSBC UK" Outfit Regular 13sp #C5C8BA. Trailing "1200 GBP, 5 days ago" Outfit Regular 12sp #8F9285.

**Component 6 — List Row** (full width minus 32dp insets, top margin 4dp, 72dp tall): Leading 40dp circular avatar #44483D, initials "MC" Outfit SemiBold 16sp #C5C8BA. Title "Michael Chen" Outfit SemiBold 15sp #E3E3D8. Subtitle "Lloyds Bank" Outfit Regular 13sp #C5C8BA.

**Component 7 — List Row** (full width minus 32dp insets, top margin 16dp): Row with label "All Beneficiaries" Outfit SemiBold 15sp #E3E3D8 left-aligned, sort icon 20dp #C5C8BA right-aligned.

**Component 8 — Card** (full width minus 32dp insets, top margin 8dp): surfaceContainer #1E201A background, 12dp corner radius, 16dp padding. Leading NatWest bank logo 32dp rounded square. Title "James Anderson" Outfit SemiBold 15sp #E3E3D8. Subtitle "GB29 NWBK 8819" Outfit Regular 13sp #C5C8BA. Footer "Last payment: 12 May 2026" Outfit Regular 12sp #8F9285.

**Component 9 — Card** (full width minus 32dp insets, top margin 8dp, bottom 80dp): Same shape. Leading Santander logo. Title "Priya Patel" Outfit SemiBold 15sp #E3E3D8. Subtitle "GB72 ABBY 4421" Outfit Regular 13sp #C5C8BA.

**Component 10 — FAB** (56dp diameter, anchored bottom-right 16dp from edges): Circular FAB background #B2D188, plus icon 24dp #1F3701.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full scrollable layout on #12140E. Anchored by the earth-green accent #B2D188 on the FAB and avatar highlights, the layout stays calm, balanced, and refined throughout the regulated-industry banking experience.
↑↑↑ MOCKUP PROMPT
