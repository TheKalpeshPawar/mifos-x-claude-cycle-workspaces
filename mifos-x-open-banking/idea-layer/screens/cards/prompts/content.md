---
ui_yaml_sha: sha256:cards-ui-2026-06-02
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
content_hash: cards-content-2026-06-02

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: index_list

feature: cards
state: content
state_visibility: content
viewmodel: CardsViewModel

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: /idea export
prompt_template_version: stitch-per-state-v3.0.0
generated_at: "2026-06-02"
---

# cards — content state

> Auto-generated from screens/cards/ui.yaml @ SHA 96bd91327a92849f
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the content state of the Cards screen for **Mifos X Open Banking**, a open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB.

**Component 1 — App Bar** (64dp tall, full width): Title "My Cards" Outfit SemiBold 20sp #E3E3D8 left-aligned with 16dp inset. Zero elevation, background #12140E.

**Component 2 — Card** (full width minus 32dp insets, top margin 24dp, 192dp tall): Mifos Debit Visa card, gradient #354E16 to #1E201A, 16dp corner radius. PAN "4521" Outfit Medium 20sp letter-spacing 2sp #E3E3D8. Name "Alex Johnson" Outfit Medium 13sp #C5C8BA. Visa logo right. "Active" chip top-right: background #354E16, label Outfit SemiBold 11sp #CDEDA3. Dot-indicator below: two dots, first filled #B2D188 (selected), second #44483D.

**Component 3 — Chip Row** (full width minus 32dp insets, top margin 16dp): 4 quick-action chips horizontal row, 40dp tall, 20dp corner radius, 8dp gap. "Freeze" outline #44483D icon snowflake 16dp. "Set Limit" outline #44483D icon dial 16dp. "View PIN" outline #44483D icon eye 16dp. "Report Lost" outline #93000A icon warning 16dp #FFB4AB label Outfit Regular 13sp #FFB4AB.

**Component 4 — List Row** (full width minus 32dp insets, top margin 24dp): Section header row "Card Transactions" Outfit SemiBold 15sp #E3E3D8 left, "See all" link Outfit Regular 13sp #B2D188 right.

**Component 5 — List Row** (full width minus 32dp insets, top margin 8dp, 64dp tall): Leading Netflix logo 32dp rounded. "Netflix" Outfit SemiBold 14sp #E3E3D8. "20 May 2026" Outfit Regular 12sp #8F9285 below. Trailing "-15.99 GBP" Outfit SemiBold 14sp #FFB4AB right.

**Component 6 — List Row** (full width minus 32dp insets, top margin 4dp, 64dp tall): "Tesco Express" Outfit SemiBold 14sp #E3E3D8. Trailing "-34.56 GBP" Outfit SemiBold 14sp #E3E3D8.

**Component 7 — List Row** (full width minus 32dp insets, top margin 4dp, 64dp tall): "Uber" Outfit SemiBold 14sp #E3E3D8. Trailing "-12.40 GBP" Outfit SemiBold 14sp #E3E3D8.

**Component 8 — List Row** (full width minus 32dp insets, top margin 4dp, 64dp tall): "Amazon.co.uk" Outfit SemiBold 14sp #E3E3D8. Trailing "-67.99 GBP" Outfit SemiBold 14sp #E3E3D8.

**Component 9 — List Row** (full width minus 32dp insets, top margin 4dp, 64dp tall): "Starbucks" Outfit SemiBold 14sp #E3E3D8. Trailing "-5.85 GBP" Outfit SemiBold 14sp #E3E3D8.

**Component 10 — Button** (full width minus 32dp insets, top margin 16dp, bottom 32dp): Outlined button 48dp tall, 12dp corner radius, outline 1dp #B2D188, label "Order New Card" Outfit Medium 15sp #B2D188.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full scrollable layout on #12140E. The earth-green accent #B2D188 on card selection indicator, order-card button, and see-all link creates confident card-management UX — calm, balanced, and refined for the regulated-industry banking context.

↑↑↑ MOCKUP PROMPT
