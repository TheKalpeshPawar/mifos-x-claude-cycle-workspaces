---
ui_yaml_sha: f40389aebb44c1ab7cf7d41e2c7831d6dfd06eb9cf01fcd11f6806ecc71dc804
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 76e2bf44c79a08bcb983f5e5432b91dda88adc38150c048645842fcd034708ee

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: send-money
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# send-money — content state

> Auto-generated from screens/send-money/ui.yaml @ SHA fa7b9cc8d23a162d
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the content state of the send money screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title "Send Money" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow icon 24dp tinted #B2D188. Zero elevation, background #12140E.

**Component 2 — Text Field** (full width minus 32dp insets, top margin 24dp): Outlined text field 56dp tall, 12dp corner radius, label "From Account" Outfit Regular 12sp #8F9285, value "Primary Checking — £4,250.00 available" Outfit Regular 16sp #E3E3D8, outline 1dp #44483D, focused outline 1dp #B2D188.

**Component 3 — Text Field** (full width minus 32dp insets, top margin 12dp): Outlined text field 56dp tall, same shape. Label "Amount" Outfit Regular 12sp #8F9285. Empty value field. Leading currency prefix "£" Outfit Regular 16sp #C5C8BA.

**Component 4 — Text Field** (full width minus 32dp insets, top margin 12dp): Outlined text field 56dp tall. Label "Currency" Outfit Regular 12sp #8F9285, value "GBP" Outfit Regular 16sp #E3E3D8, trailing dropdown arrow 20dp #C5C8BA.

**Component 5 — Text Field** (full width minus 32dp insets, top margin 12dp): Outlined text field 56dp tall. Label "To" Outfit Regular 12sp #8F9285. Leading magnifier icon 20dp #8F9285.

**Component 6 — Chip Row** (full width minus 32dp insets, top margin 16dp, horizontally scrollable): Section label "Recent Beneficiaries" Outfit Medium 14sp #C5C8BA. Two avatar chips 40dp height, 20dp corner radius, background #1E201A, border 1dp #44483D. First chip: initials "JS" in 32dp circle background #354E16 #B2D188 text, label "John Smith" Outfit Regular 13sp #E3E3D8. Second chip: initials "SW" in 32dp circle, label "Sarah Williams" Outfit Regular 13sp #E3E3D8.

**Component 7 — Text Field** (full width minus 32dp insets, top margin 16dp): Outlined text field 56dp tall. Label "Reference" Outfit Regular 12sp #8F9285. Helper text "Optional payment reference" Outfit Regular 11sp #8F9285 below field.

**Component 8 — Card** (full width minus 32dp insets, top margin 16dp, 12dp corner radius, background #1E201A): Section header "Payment Type" Outfit Medium 14sp #C5C8BA with 16dp padding. Three List Row items 48dp tall each, 1dp divider #44483D between rows. Row 1: radio button selected #B2D188, label "SEPA" Outfit Regular 14sp #E3E3D8, trailing "Free" badge Outfit Medium 11sp #B2D188. Row 2: radio button unselected outline #8F9285, label "Domestic" Outfit Regular 14sp #E3E3D8. Row 3: radio button unselected, label "International" Outfit Regular 14sp #E3E3D8.

**Component 9 — Card** (full width minus 32dp insets, top margin 12dp, 12dp corner radius, background #354E16): Body text "Estimated fee: Free (SEPA)" Outfit Regular 14sp #CDEDA3, 16dp padding. Leading info icon 18dp #B2D188.

**Component 10 — Button** (full width minus 32dp insets, top margin 24dp, bottom 32dp): Filled pill button 52dp tall, 999dp corner radius, background #B2D188, label "Continue" Outfit SemiBold 16sp #1F3701 centered.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. The earthy green accent #B2D188 on the continue button, selected radio, and focused field outlines keeps the layout calm and balanced, refined for this regulated open banking context.
↑↑↑ MOCKUP PROMPT
