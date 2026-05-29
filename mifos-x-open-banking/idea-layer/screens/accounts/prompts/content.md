---
ui_yaml_sha: 06a74a064d747a5df855d29ceca0a54efe2937d3362989fcd2a1e8391bb18936
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 861ca1ef064cf21802182527411b928c266b9e38e67da72ad635ac12829e1575

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: index_list

feature: accounts
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# accounts — content state

> Auto-generated from screens/accounts/ui.yaml @ SHA 086088701e3ba2a6
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the content state of the accounts screen for **Mifos X Open Banking**, a professional open banking KMP super-app serving consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, tertiary #A0CFCB, on_tertiary #003735, error #FFB4AB, on_error #690005, error_container #93000A, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16, scrim #000000.

**Component 1 — App Bar** (64dp tall, full width): Title "My Accounts" Outfit SemiBold 22sp #E3E3D8 left-aligned 16dp padding. Trailing help-outline icon 24dp #8F9285. Background #12140E, zero elevation, 1dp bottom divider #44483D.

**Component 2 — Chip Row** (full width minus 32dp insets, top margin 12dp, 8dp gap, horizontally scrollable): Four filter chips 32dp tall, 16dp corner radius. "ALL" filled #354E16 Outfit Medium 12sp #CDEDA3. "CHECKING" outlined 1dp #44483D Outfit Regular 12sp #C5C8BA. "SAVINGS" outlined 1dp #44483D. "BUSINESS" outlined 1dp #44483D. index_list archetype.

**Component 3 — Card** (full width minus 32dp insets, 16dp corner radius, top margin 16dp, background #1E201A, 16dp padding): Header row: "Primary Checking" Outfit SemiBold 16sp #E3E3D8 on left. Badge "CHECKING" 20dp tall, 4dp corner radius, background #1F4E4B, Outfit Medium 11sp #BCEBE7 on right. Balance "£4,250.00" Outfit SemiBold 28sp #B2D188 top margin 8dp. IBAN row top margin 8dp: account-box icon 16dp #8F9285 + "DE89 3704 0044 0532 0130 00" Outfit Regular 12sp #C5C8BA.

**Component 4 — Card** (full width minus 32dp insets, 16dp corner radius, top margin 12dp, background #1E201A, 16dp padding): Header: "Holiday Savings" Outfit SemiBold 16sp #E3E3D8, badge "SAVINGS" #1F4E4B Outfit Medium 11sp #BCEBE7. Balance "£6,180.50" Outfit SemiBold 28sp #B2D188 top margin 8dp. IBAN: "DE89 3704 0044 0532 0131 00" Outfit Regular 12sp #C5C8BA with account-box icon.

**Component 5 — Card** (full width minus 32dp insets, 16dp corner radius, top margin 12dp, background #1E201A, 16dp padding): Header: "Business Current" Outfit SemiBold 16sp #E3E3D8, badge "BUSINESS" #1F4E4B Outfit Medium 11sp #BCEBE7. Balance "£2,050.00" Outfit SemiBold 28sp #B2D188 top margin 8dp. IBAN: "DE89 3704 0044 0532 0132 00" Outfit Regular 12sp #C5C8BA with account-box icon.

**Component 6 — List Row** (full width minus 32dp insets, top margin 16dp): 1dp divider #44483D. Footer row 56dp tall: "Total across 3 accounts" Outfit Regular 13sp #C5C8BA on left, "£12,480.50" Outfit SemiBold 18sp #B2D188 on right.

**Component 7 — FAB** (56dp diameter, anchored bottom-right 16dp): Filled FAB background #B2D188, plus icon 24dp #1F3701. Bottom Nav 64dp full width background #1E201A, 1dp top divider #44483D.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The earth-green #B2D188 used on balance amounts and the FAB across the deep #12140E canvas creates a calm, balanced index_list, with teal secondary containers lending depth and hierarchy to account type badges.
↑↑↑ MOCKUP PROMPT
