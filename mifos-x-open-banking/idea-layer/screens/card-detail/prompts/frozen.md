---
ui_yaml_sha: 886497acc937d3f77eee431d1ffe01ed5447c84b05aaf98a8bff4c5dc9157014
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 6003480e025cc9cf9d2ef393be3e21ebb1b1a2931b9e9fa582738c80a3bf5dfc

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: card-detail
state: frozen
state_visibility: frozen

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# card-detail — frozen state

> Auto-generated from screens/card-detail/ui.yaml @ SHA 134862b54e04e8ca
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the frozen state of the Card Detail screen for **Mifos X Open Banking**, a open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB.

**Component 1 — App Bar** (64dp tall, full width): Title "Card Details" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow icon 24dp tinted #B2D188. Zero elevation, background #12140E.

**Component 2 — Card** (full width minus 32dp insets, top margin 24dp, 192dp tall): Card visual 16dp corner radius, background gradient #282A24 to #1E201A with subtle frost-grain overlay, desaturated. Top row: Mifos X wordmark Outfit Bold 14sp #8F9285 left, Visa logo #44483D right. PAN "4521" Outfit Medium 20sp letter-spacing 2sp #8F9285. Cardholder "ALEX JOHNSON" Outfit Medium 13sp #44483D. Expiry "09/29" Outfit Regular 13sp #44483D. Overlapping "Frozen" badge center: 32dp rounded rectangle background #A0CFCB, snowflake icon 16dp #003735, label "Frozen" Outfit SemiBold 12sp #003735.

**Component 3 — Card** (full width minus 32dp insets, top margin 16dp): surfaceContainer #1E201A, 12dp corner radius, 16dp padding. Left border accent 4dp #A0CFCB. Row "Card Frozen" Outfit SemiBold 15sp #E3E3D8 left, inactive toggle right with track #44483D and thumb #8F9285.

**Component 4 — Card** (full width minus 32dp insets, top margin 12dp): Same limits section with muted edit icons #44483D. "Daily limit: 2500 GBP", "Monthly limit: 10000 GBP" Outfit Regular 14sp #8F9285 (dimmed).

**Component 5 — Button** (full width minus 32dp insets, top margin 16dp): Filled button 48dp tall, 12dp corner radius, background #A0CFCB, leading snowflake-off icon 20dp #003735, label "Unfreeze Card" Outfit SemiBold 15sp #003735.

**Component 6 — Button** (full width minus 32dp insets, top margin 8dp, bottom 32dp): Outlined button 48dp tall, 12dp corner radius, outline 1dp #44483D, label "View Transactions" Outfit Medium 15sp #C5C8BA.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full layout on #12140E. The secondary teal accent #A0CFCB on frozen status and the unfreeze button creates a calm, informational state that is clearly distinguishable from the active card, maintaining security trust throughout.
↑↑↑ MOCKUP PROMPT
