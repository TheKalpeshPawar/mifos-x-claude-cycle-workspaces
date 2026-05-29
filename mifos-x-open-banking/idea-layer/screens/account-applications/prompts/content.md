---
ui_yaml_sha: 311407aa8bae098b271a0fcb7b6d0f6b1a2c6f6f1041ffea618960562714bf2e
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: c2a48baa7eef15f7aa431274845d37dae8b0c49acb12be9836aee628e91e89bd

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: account-applications
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# account-applications — content state

> Auto-generated from screens/account-applications/ui.yaml @ SHA 2e57ccd0c0cac5ca
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the content state of the account-applications screen for **Mifos X Open Banking**, a professional open banking KMP super-app serving consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, tertiary #A0CFCB, on_tertiary #003735, error #FFB4AB, on_error #690005, error_container #93000A, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16, scrim #000000.

**Component 1 — App Bar** (64dp tall, full width): Title "Account Applications" Outfit Medium 18sp #E3E3D8 left-aligned with 16dp leading padding. Background #12140E, zero elevation, 1dp bottom divider #44483D.

**Component 2 — Chip Row** (full width minus 32dp insets, top margin 12dp, 8dp gap, horizontally scrollable): Four filter chips 32dp tall, 16dp corner radius. "All (8)" chip filled #354E16 label Outfit Medium 13sp #CDEDA3 selected. "Pending (3)" chip outlined 1dp #44483D label Outfit Regular 13sp #C5C8BA. "Approved (3)" chip outlined 1dp #44483D label Outfit Regular 13sp #C5C8BA. "Rejected (2)" chip outlined 1dp #44483D label Outfit Regular 13sp #C5C8BA.

**Component 3 — Card** (full width minus 32dp insets, 12dp corner radius, top margin 16dp, background #1E201A, 16dp padding): Header row: "John Mwangi" Outfit SemiBold 16sp #E3E3D8 on left. Status chip "Pending Review" 24dp tall, 12dp corner radius, background #E8A317 with 8% opacity (#1E201A tinted), label Outfit Medium 12sp #E8A317. "KCB Savings Account" Outfit Regular 14sp #C5C8BA top margin 4dp. Footer row top margin 12dp: "Submitted: 20 May 2026" Outfit Regular 12sp #8F9285 on left. Button "Review" 32dp tall, 8dp corner radius, background #354E16, Outfit Medium 12sp #CDEDA3 on right.

**Component 4 — Card** (full width minus 32dp insets, 12dp corner radius, top margin 12dp, background #1E201A, 16dp padding): Header row: "Sarah Odhiambo" Outfit SemiBold 16sp #E3E3D8 on left. Status chip "Approved" 24dp tall, background #354E16, Outfit Medium 12sp #B2D188 on right. "M-Shwari Checking Account" Outfit Regular 14sp #C5C8BA top margin 4dp. "Submitted: 18 May 2026" Outfit Regular 12sp #8F9285 top margin 12dp.

**Component 5 — Card** (full width minus 32dp insets, 12dp corner radius, top margin 12dp, background #1E201A, 16dp padding): Header row: "Peter Kamau" Outfit SemiBold 16sp #E3E3D8 on left. Status chip "Rejected" 24dp tall, background #93000A, Outfit Medium 12sp #FFB4AB on right. "Business Current Account" Outfit Regular 14sp #C5C8BA top margin 4dp. Footer row top margin 12dp: "Submitted: 12 May 2026" Outfit Regular 12sp #8F9285 on left. Link "View Reason" Outfit Medium 12sp #B2D188 on right.

**Component 6 — FAB** (56dp diameter, anchored bottom-right 16dp insets): Filled FAB background #B2D188, plus icon 24dp #1F3701, label absent. Bottom Nav 64dp tall full width background #1E201A, 1dp top divider #44483D.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Anchored by the earth-green #B2D188 FAB and selected chip on deep #12140E canvas, the layout stays calm and balanced, with semantic pending amber #E8A317 and error rose #FFB4AB keeping status badges immediately legible.
↑↑↑ MOCKUP PROMPT
