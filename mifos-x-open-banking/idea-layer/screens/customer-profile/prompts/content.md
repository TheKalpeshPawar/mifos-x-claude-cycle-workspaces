---
ui_yaml_sha: ed2405e9b0ab40e84eddfcb7e669dd5d6df03b6a59f4997cb41c63dd2313c905
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: baae64fe444d54817ce90c8a8ae12e262b75efa7153bb97ad7a1b7d5621995e1

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: customer-profile
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# customer-profile — content state

> Auto-generated from screens/customer-profile/ui.yaml @ SHA c37df97789fda1cf
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the content state of the customer-profile screen for **Mifos X Open Banking**, a professional open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, error #FFB4AB, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title "Customer Profile" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow icon 24dp tinted #B2D188. Trailing edit icon 24dp #8F9285. Zero elevation, background #12140E.

**Component 2 — List Row** (full width minus 32dp insets, top margin 24dp): Section heading "Personal Information" Outfit SemiBold 14sp #B2D188, left-aligned, bottom margin 8dp. Label-value rows on surface_container #1E201A, 12dp corner radius. Row 1: label "Full Name" Outfit Regular 12sp #8F9285, value "John Kamau Mwangi" Outfit Medium 15sp #E3E3D8. Row 2: label "Date of Birth" Outfit Regular 12sp #8F9285, value "14 March 1985 (Age: 41)" Outfit Medium 15sp #E3E3D8. Row 3: label "National ID" Outfit Regular 12sp #8F9285, value "KE12345678" Outfit Medium 15sp #E3E3D8. Row 4: label "Tax PIN (KRA)" Outfit Regular 12sp #8F9285, value "A001234567M" Outfit Medium 15sp #E3E3D8. Row 5: label "Phone" Outfit Regular 12sp #8F9285, value "+254 722 123 456" Outfit Medium 15sp #A0CFCB. Row 6: label "Email" Outfit Regular 12sp #8F9285, value "john.mwangi@gmail.com" Outfit Medium 15sp #A0CFCB. Each row 56dp tall, 16dp horizontal padding, 1dp bottom divider #44483D.

**Component 3 — List Row** (full width minus 32dp insets, top margin 16dp): Section heading "Address" Outfit SemiBold 14sp #B2D188. surface_container #1E201A card, 12dp radius. Row 1: "123 Moi Avenue, Nairobi" Outfit Medium 15sp #E3E3D8. Row 2: "Nairobi County, Kenya" Outfit Regular 14sp #C5C8BA. Row 3: "Postcode: 00100" Outfit Regular 14sp #C5C8BA. Rows 56dp tall, 1dp dividers #44483D.

**Component 4 — List Row** (full width minus 32dp insets, top margin 16dp): Section heading "Employment" Outfit SemiBold 14sp #B2D188. surface_container #1E201A card. Row 1: label "Employer" #8F9285, value "Safaricom PLC" #E3E3D8 Outfit Medium 15sp. Row 2: label "Monthly Income" #8F9285, value "KES 85,000" #B2D188 Outfit SemiBold 15sp. Row 3: label "Employment Type" #8F9285, value "Permanent" #E3E3D8 Outfit Medium 15sp. Rows 56dp, dividers #44483D.

**Component 5 — Button** (full width minus 32dp insets, top margin 24dp, bottom 32dp): Filled button 48dp tall, 12dp corner radius, background #B2D188, label "Edit Information" Outfit SemiBold 15sp #1F3701 centered.

**Component 6 — Bottom Nav** (64dp tall, full width, anchored bottom): 4 tabs Home, Payments, **Profile** (selected, indicator #354E16, icon #B2D188 24dp + label Outfit Medium 11sp #B2D188), Settings. Background #1E201A, top 1dp #44483D. Inactive icons 20dp #8F9285 + labels Outfit Regular 11sp #8F9285.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E with 16dp section gaps. Anchored by the accent #B2D188 on section headings, the active nav tab, and the primary action button, the composition stays calm and refined, conveying financial trust.
↑↑↑ MOCKUP PROMPT
