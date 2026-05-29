---
ui_yaml_sha: 886497acc937d3f77eee431d1ffe01ed5447c84b05aaf98a8bff4c5dc9157014
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 8a5c8199c7c455d840a272424967a247adc1defcb1fe3bad42267023324ef519

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: card-detail
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# card-detail — content state

> Auto-generated from screens/card-detail/ui.yaml @ SHA 9bd5650486b22725
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the content state of the Card Detail screen for **Mifos X Open Banking**, a open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB.

**Component 1 — App Bar** (64dp tall, full width): Title "Card Details" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow icon 24dp tinted #B2D188. Zero elevation, background #12140E.

**Component 2 — Card** (full width minus 32dp insets, top margin 24dp, 192dp tall): Rounded card visual 16dp corner radius, background linear gradient from #354E16 to #1E201A. Top row: Mifos X wordmark Outfit Bold 14sp #CDEDA3 left, Visa logo right #E3E3D8. Middle: masked PAN "4521" Outfit Medium 20sp letter-spacing 2sp #E3E3D8. Bottom left: cardholder name "ALEX JOHNSON" Outfit Medium 13sp #C5C8BA. Bottom right: expiry "09/29" Outfit Regular 13sp #C5C8BA. Trailing "Show card details" text link 12sp #B2D188 below the card.

**Component 3 — Card** (full width minus 32dp insets, top margin 16dp): surfaceContainer #1E201A, 12dp corner radius, 16dp padding. Row with "Card Active" Outfit SemiBold 15sp #E3E3D8 left, active toggle switch right with track #354E16 and thumb #B2D188.

**Component 4 — Card** (full width minus 32dp insets, top margin 12dp): surfaceContainer #1E201A, 12dp corner radius, 16dp padding. Header "Spending Limits" Outfit SemiBold 15sp #E3E3D8. Row 1: "Daily limit" Outfit Regular 14sp #C5C8BA, "2500 GBP" Outfit SemiBold 14sp #E3E3D8, edit pencil icon 18dp #B2D188. Divider 1dp #44483D. Row 2: "Monthly limit" Outfit Regular 14sp #C5C8BA, "10000 GBP" Outfit SemiBold 14sp #E3E3D8, edit pencil icon 18dp #B2D188.

**Component 5 — Button** (full width minus 32dp insets, top margin 16dp): Outlined button 48dp tall, 12dp corner radius, outline 1dp #44483D, leading snowflake icon 20dp #A0CFCB, label "Freeze Card" Outfit Medium 15sp #E3E3D8.

**Component 6 — Button** (full width minus 32dp insets, top margin 8dp): Outlined button 48dp tall, 12dp corner radius, outline 1dp #93000A, leading warning icon 20dp #FFB4AB, label "Report Lost/Stolen" Outfit Medium 15sp #FFB4AB.

**Component 7 — Button** (full width minus 32dp insets, top margin 8dp, bottom 32dp): Filled button 48dp tall, 12dp corner radius, background #354E16, leading list icon 20dp #CDEDA3, label "View Transactions" Outfit Medium 15sp #CDEDA3.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full scrollable layout on #12140E. The earth-green accent #B2D188 on the active toggle, edit controls, and primary action creates a confident atmosphere — calm, balanced, and refined for the regulated-industry banking context.
↑↑↑ MOCKUP PROMPT
