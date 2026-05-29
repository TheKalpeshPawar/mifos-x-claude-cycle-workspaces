---
ui_yaml_sha: f40389aebb44c1ab7cf7d41e2c7831d6dfd06eb9cf01fcd11f6806ecc71dc804
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: fb3559ddaf25f0b086c398e07a6c77a7e5d9222f98904d3e36d638539ab88e50

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: send-money
state: validating
state_visibility: validating

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# send-money — validating state

> Auto-generated from screens/send-money/ui.yaml @ SHA 2890ef1b7ab04b86
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the validating state of the send money screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title "Send Money" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow 24dp tinted #B2D188 (disabled, 40% opacity). Background #12140E, zero elevation.

**Component 2 — Text Field** (full width minus 32dp insets, top margin 24dp, disabled overlay 60% opacity): Outlined text field 56dp tall, 12dp corner radius, label "From Account" Outfit Regular 12sp #8F9285, value "Primary Checking — £4,250.00 available" Outfit Regular 16sp #C5C8BA, outline 1dp #44483D.

**Component 3 — Text Field** (full width minus 32dp insets, top margin 12dp, disabled): Outlined text field 56dp tall. Label "Amount" Outfit Regular 12sp #8F9285. Value "£150.00" Outfit Regular 16sp #C5C8BA, outline 1dp #44483D.

**Component 4 — Text Field** (full width minus 32dp insets, top margin 12dp, disabled): Outlined text field 56dp tall. Label "Currency" Outfit Regular 12sp #8F9285, value "GBP" Outfit Regular 16sp #C5C8BA, trailing chevron 20dp #44483D.

**Component 5 — Text Field** (full width minus 32dp insets, top margin 12dp, disabled): Outlined text field 56dp tall. Label "To" Outfit Regular 12sp #8F9285. Value "John Smith" Outfit Regular 16sp #C5C8BA.

**Component 6 — Card** (full width minus 32dp insets, top margin 16dp, 12dp corner radius, background #1E201A): Horizontal center row. Circular progress indicator 24dp tinted #E8A317 (pending color, animated). Text "Validating payment details..." Outfit Regular 14sp #C5C8BA with 12dp left gap.

**Component 7 — Card** (full width minus 32dp insets, top margin 12dp, background #354E16): "SEPA transfer via OBP API v7 — validating beneficiary IBAN" Outfit Regular 13sp #CDEDA3, leading clock icon 16dp #B2D188, 16dp padding.

**Component 8 — Button** (full width minus 32dp insets, top margin 24dp, bottom 32dp, disabled): Filled pill 52dp tall, 999dp corner radius, background #282A24, label "Validating..." Outfit SemiBold 16sp #8F9285 centered. No tap action.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full layout on #12140E with fields rendered at reduced opacity to signal non-interactive state. The amber #E8A317 on the progress spinner signals in-progress validation, keeping the screen restrained and calm while the user waits for this regulated open banking check to complete.
↑↑↑ MOCKUP PROMPT
