---
ui_yaml_sha: f78a3dba3aff3089e2451e41f32781ab4fe14bcec47d87ec57ad572302aa3a0c
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: b47e33a5ad2f44fef57bb9e914fc54b914aa70a4d658a75852806a65f251aa31

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: standing-orders
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# standing-orders — content state

> Auto-generated from screens/standing-orders/ui.yaml @ SHA d7116c3a65d496b0
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the content state of the standing-orders screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Standing Orders" Outfit Medium 18sp #E3E3D8 centered. Zero elevation, background #12140E.

**Component 2 — Chip Row** (full width minus 32dp insets, top margin 16dp): Single status chip "3 active" 32dp tall, 16dp corner radius, filled background #354E16, label Outfit Medium 13sp #CDEDA3, label anchored left.

**Component 3 — Card** (full width minus 32dp insets, top margin 16dp, 12dp corner radius, background #1E201A): Rent Payment card. Header row: title "Rent Payment" Outfit SemiBold 16sp #E3E3D8 left, badge "Active" Outfit Medium 11sp #CDEDA3 on #354E16 pill right. Beneficiary "To: Landlord Holdings Ltd" Outfit Regular 14sp #C5C8BA top margin 4dp. Amount row: "£1,200 / month" Outfit SemiBold 14sp #B2D188 left, "Next: 1 Jun 2026" Outfit Regular 12sp #8F9285 right. Action row top margin 8dp: edit icon 20dp #8F9285 and delete icon 20dp #FFB4AB, 16dp apart, anchored right, 48dp tap targets.

**Component 4 — Card** (full width minus 32dp insets, top margin 12dp, 12dp corner radius, background #1E201A): Netflix Subscription card. Title "Netflix Subscription" Outfit SemiBold 16sp #E3E3D8, badge "Active" same style as Component 3. Amount "£15.99 / month" Outfit SemiBold 14sp #B2D188, "Next: 7 Jun 2026" Outfit Regular 12sp #8F9285. Edit + delete icons same spec, anchored right.

**Component 5 — Card** (full width minus 32dp insets, top margin 12dp, 12dp corner radius, background #1E201A): Gym Membership card. Title "Gym Membership" Outfit SemiBold 16sp #E3E3D8, badge "Paused" Outfit Medium 11sp #E3E3D8 on #44483D pill right. Amount "£45.00 / month" Outfit SemiBold 14sp #C5C8BA (muted, paused), "Next: 15 Jun 2026 (Paused)" Outfit Regular 12sp #8F9285. Edit + delete icons anchored right.

**Component 6 — FAB** (56dp diameter, anchored bottom-right 16dp insets): Background #B2D188, plus icon 24dp #1F3701, label "Create Standing Order" Outfit Medium 14sp #1F3701 trailing. Corner radius 16dp.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. The earth-green accent #B2D188 on active badges, amounts, and FAB keeps the layout balanced and refined; card borders in #44483D maintain a calm, minimal structure suited to this open banking context.
↑↑↑ MOCKUP PROMPT
