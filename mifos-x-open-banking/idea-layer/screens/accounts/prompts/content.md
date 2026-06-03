---
ui_yaml_sha: 32104a29c04c671ed5b57d3bf8d3f614dc3c4a3c7f3991600922913889eb8f9c
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 0d8c9ff7a940e9df82e21d33cdadf771d5ed36f1e3c2137673b93fac7fd2cf27

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: index_list

feature: accounts
state: content
state_visibility: content

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# accounts — content state

> Auto-generated from screens/accounts/ui.yaml @ SHA 783643b36492e304
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the My Accounts screen for **mifos-x-open-banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: background #12140E, surface #1E201A, surfaceHigh #282A24, onSurface #E3E3D8, primary #B2D188, onPrimary #1F3701, primaryContainer #354E16, onPrimaryContainer #CDEDA3, secondary #A0CFCB, onSecondary #003735, outline #8F9285, outlineVariant #44483D, onSurfaceVariant #C5C8BA, pending #E8A317, error #FFB4AB.

**Component 1 — Top App Bar** (56dp tall, full width): Title "My Accounts" Outfit SemiBold 20sp #E3E3D8, left-aligned 16dp inset. Trailing help icon 24dp tinted #C5C8BA. Background #12140E, zero elevation.

**Component 2 — Search Bar** (full width, 48dp tall, 16dp horizontal inset, top margin 12dp): Outlined pill field, corner radius 999dp, stroke 1dp #8F9285. Leading search icon 20dp #C5C8BA. Placeholder "Search by name, number or label" Outfit Regular 16sp #8F9285. Background #1E201A. No filter tabs, no chips.

**Component 3 — Bank Group Header: Mifos Bank UK** (full width, 16dp insets, top margin 20dp): Row — bank icon 20dp #B2D188, column: "Mifos Bank UK" Outfit Medium 14sp #E3E3D8, "2 accounts" Outfit Regular 12sp #C5C8BA. Subtotal "£10,430.50" Outfit SemiBold 16sp #B2D188 right-aligned. 12dp vertical padding.

**Component 4 — Account Card: Primary Checking** (80dp min-height, 12dp radius, margin-top 8dp): Background #282A24. Header row: "Primary Checking" Outfit Medium 16sp #E3E3D8 left; badge "CHECKING" 11sp #CDEDA3 on #354E16 pill right. Balance "£4,250.00" Outfit SemiBold 22sp #B2D188. IBAN row: account_box icon 16dp #8F9285, "DE89 3704 0044 0532 0130 00" 12sp #C5C8BA. 16dp padding. index_list archetype card.

**Component 5 — Account Card: Holiday Savings** (80dp min-height, 12dp radius, margin-top 8dp): Background #282A24. Header row: "Holiday Savings" Outfit Medium 16sp #E3E3D8 left; badge "SAVINGS" 11sp #CDEDA3 on #354E16 pill right. Balance "£6,180.50" Outfit SemiBold 22sp #B2D188. IBAN row: account_box icon 16dp #8F9285, "DE89 3704 0044 0532 0131 00" 12sp #C5C8BA. 16dp padding.

**Component 6 — Bank Group Header: Mifos Business UK** (full width, 16dp insets, margin-top 20dp): Row — bank icon 20dp #B2D188, column: "Mifos Business UK" Outfit Medium 14sp #E3E3D8, "1 account" 12sp #C5C8BA. Subtotal "£2,050.00" Outfit SemiBold 16sp #B2D188 right-aligned. 12dp vertical padding.

**Component 7 — Account Card: Business Current** (80dp min-height, 12dp radius, margin-top 8dp): Background #282A24. Header row: "Business Current" Outfit Medium 16sp #E3E3D8 left; badge "BUSINESS" 11sp #CDEDA3 on #354E16 pill right. Balance "£2,050.00" Outfit SemiBold 22sp #B2D188. IBAN row: account_box icon 16dp #8F9285, "DE89 3704 0044 0532 0132 00" 12sp #C5C8BA. 16dp padding.

**Component 8 — Divider** (margin-top 20dp): 1dp horizontal rule #44483D, 16dp insets.

**Component 9 — Total Balance Footer** (56dp tall): Row — "Total across 3 accounts" Outfit Regular 14sp #C5C8BA left, "£12,480.50" Outfit Bold 18sp #E3E3D8 right. Background transparent.

**Component 10 — FAB: Add Account** (56dp circle, bottom-right 16dp inset): Background #B2D188, add icon 24dp #1F3701. Elevation shadow.

DO NOT use em-dash anywhere in text. DO NOT make any headline more than 3 lines or any subtitle more than 25 words. DO NOT break the page theme between sections. DO NOT place light text on light buttons or dark text on dark buttons.

Scrollable dark surface #12140E with a calm, refined feel. Earth-green primary #B2D188 on balances, subtotals, FAB, and IBAN icons signals financial stability; card lift from #12140E to #282A24 creates depth consistent with the taste-default dials.

↑↑↑ MOCKUP PROMPT
