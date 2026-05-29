---
ui_yaml_sha: 43bf8e879b37ae93b3ce62dd72bfb9fee6978b31c734296cf84770dbd633d439
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 77fc9497f7116cd102d4eee4a7d163d70b806802a5d71331a88f4c3026570e3c

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: detail_screen

feature: direct-debit-detail
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# direct-debit-detail — content state

> Auto-generated from screens/direct-debit-detail/ui.yaml @ SHA 57543724e56ae1f6
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the content state of the direct-debit-detail screen for **Mifos X Open Banking**, a mobile KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, error #FFB4AB, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title "Direct Debit" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow 24dp #B2D188. Trailing more-vertical icon 24dp #8F9285. Background #12140E. detail_screen layout.

**Component 2 — Hero** (centered, top margin 24dp): Merchant logo 64dp x 64dp circle, #1E201A background with letter "N" Outfit Bold 28sp #E3E3D8 (Netflix). Merchant name "Netflix Entertainment" Outfit SemiBold 20sp #E3E3D8 centered, top margin 12dp. "Active" badge 28dp tall, 999dp radius, background #354E16, label Outfit Medium 12sp #CDEDA3 centered, top margin 8dp.

**Component 3 — App Bar** (centered, top margin 16dp): Amount "£15.99" Outfit Bold 32sp #E3E3D8 centered. Frequency "Monthly" Outfit Regular 14sp #8F9285 centered, top margin 4dp.

**Component 4 — Card** (full width minus 32dp insets, top margin 24dp): surface_container #1E201A, 12dp radius. Header "Mandate Details" Outfit SemiBold 15sp #B2D188, 16dp padding. Divider rows: "Next Payment" / "15 Jun 2026", "Account" / "Current Account ****4521", "Mandate Ref" / "MDT-2024-00947", "Start Date" / "12 Jan 2024". Each row: label Outfit Regular 13sp #8F9285 left, value Outfit Medium 14sp #E3E3D8 right, 52dp tall, 1dp #44483D divider.

**Component 5 — Card** (full width minus 32dp insets, top margin 16dp): surface_container #1E201A, 12dp radius. Header row: "Recent Payments" Outfit SemiBold 15sp #B2D188 left, "View all" Outfit Medium 13sp #A0CFCB right, 16dp padding. History rows: Row 1: date "15 May 2026" Outfit Regular 13sp #C5C8BA, status "Collected" badge #354E16/#CDEDA3, amount "-£15.99" Outfit SemiBold 14sp #E3E3D8 right. Row 2: "15 Apr 2026" / "Collected" / "-£15.99". Row 3: "15 Mar 2026" / "Failed" badge #93000A/#FFB4AB / "-£15.99" #FFB4AB. 1dp #44483D dividers.

**Component 6 — Button** (full width minus 32dp insets, top margin 24dp, bottom 32dp): Outlined button 48dp, 12dp radius, outline 1dp #93000A, label "Cancel Mandate" Outfit SemiBold 14sp #FFB4AB. Below: Filled button same dims, background #B2D188, label "Edit Mandate" Outfit SemiBold 14sp #1F3701. 8dp gap.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. Anchored by the earth-green #B2D188 on section headings and the Edit action, the layout stays calm and refined, while the subtle error-toned Cancel uses #FFB4AB to signal irreversibility without alarming the user.
↑↑↑ MOCKUP PROMPT
