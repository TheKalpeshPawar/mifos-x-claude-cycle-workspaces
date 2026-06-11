---
design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form

feature: send-money-amount
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: idea-render-screen (LLM-local) v1.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# send-money-amount — content state

> Auto-generated from screens/send-money-amount/ui.yaml
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the content state of the send money amount-entry screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #4C662B, on_primary #FFFFFF, primary_container #CDEDA3, on_primary_container #102000, secondary #386663, secondary_container #BCEBE7, on_secondary_container #00201E, background #F9FAEF, on_background #1A1C16, surface #FFFFFF, on_surface #1A1C16, surface_variant #E1E4D5, on_surface_variant #44483D, surface_container #F0F1E6, outline #75796C, outline_variant #C5C8BA, error #BA1A1A.

**Component 1 — App Bar** (64dp tall, full width): Title "Send Money" Outfit SemiBold 22sp #1A1C16 left-aligned. Leading back-arrow icon 24dp tinted #44483D. Zero elevation, background #F9FAEF.

**Component 2 — From Account selector** (full width minus 40dp insets, top margin 8dp, 12dp corner radius, surface #FFFFFF, 1dp outline #C5C8BA): Leading 44dp rounded square #CDEDA3 with account_balance icon 24dp #102000. Two-line body: label "From Account" Outfit Regular 12sp #44483D, value "Primary Checking — €4,820.00" Outfit SemiBold 15sp #1A1C16. Trailing expand_more chevron 24dp #44483D. Tappable to switch account.

**Component 3 — Amount field** (full width minus 40dp insets, top margin 18dp): Outlined text field 56dp tall, 12dp corner radius, focused outline 1dp #4C662B. Label "Amount" Outfit Regular 12sp #44483D above. Leading currency prefix "€" 18sp SemiBold #44483D. Entered value "250.00" Outfit SemiBold 22sp #1A1C16.

**Component 4 — Section label "To"** Outfit Medium 12sp #44483D uppercase, top margin 20dp.

**Component 5 — Beneficiary search field** (full width minus 40dp insets): Outlined text field 56dp tall, 12dp radius, leading search icon 20dp #44483D, placeholder "Search beneficiary..." Outfit Regular 16sp #75796C.

**Component 6 — Selected beneficiary row** (full width minus 40dp insets, top margin 0, 12dp radius, surface #FFFFFF, 1dp #C5C8BA): 40dp circle avatar #BCEBE7 initials "LW" #00201E SemiBold. Name "Liam Walker" Outfit SemiBold 14sp #1A1C16, subtitle "SEPA · IBAN DE89 ••3000" Outfit Regular 12sp #44483D. Trailing check_circle 24dp #4C662B. Never render an OBP login username — show the resolved beneficiary name only.

**Component 7 — Reference field** (full width minus 40dp insets, top margin 14dp): Outlined text field 56dp tall, placeholder "Payment for invoice #1234" #75796C. Helper text "Max 35 characters" Outfit Regular 11sp #44483D below.

**Component 8 — Payment Type chip group** (top margin 20dp): Section label "Payment Type" Outfit Medium 12sp #44483D uppercase. Filter chip row, 34dp tall, 8dp radius: chip "SEPA" SELECTED background #BCEBE7 #00201E with leading check 16dp; chip "Domestic" unselected 1dp #75796C #44483D; chip "International" DISABLED dashed outline 0.45 opacity. Below row: reason text "International unavailable — no BIC on file for this beneficiary" Outfit Regular 13sp #44483D.

**Component 9 — Fee banner** (full width minus 40dp insets, top margin 8dp, 8dp radius, background #CDEDA3): Leading info icon 20dp #102000, text "Estimated fee: Free (SEPA)" Outfit Medium 14sp #102000, 16dp/12dp padding.

**Component 10 — Continue button** (full width minus 40dp insets, pinned to a bottom action bar with 1dp top divider #C5C8BA on #F9FAEF): Filled button 52dp tall, 12dp corner radius, background #4C662B, label "Continue" Outfit SemiBold 15sp #FFFFFF centered. Navigates to send-money-confirm.

Do not use em-dash anywhere in text. Do not render any OBP login username as a counterparty name. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable form on #F9FAEF with a pinned bottom Continue bar. The earthy green accent #4C662B on the Continue button, selected chip, and focused field outline keeps the layout calm and balanced, refined for this regulated open banking context.
↑↑↑ MOCKUP PROMPT
