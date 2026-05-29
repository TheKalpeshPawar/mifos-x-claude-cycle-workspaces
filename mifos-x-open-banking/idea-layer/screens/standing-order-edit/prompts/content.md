---
ui_yaml_sha: 8fde56d823f64b22e73128c521f3d219cbfb577b1e9cfd8a956cf1e623771788
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 76f22476e1447e1f02e8baa609f38e922f04a572dc3fa83418add01853898932

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form

feature: standing-order-edit
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# standing-order-edit — content state

> Auto-generated from screens/standing-order-edit/ui.yaml @ SHA 548c6c8fe1379c5f
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the content state of the standing order edit screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title "Edit Standing Order" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow 24dp #B2D188. Trailing "Save" text button Outfit Medium 14sp #B2D188. Background #12140E, zero elevation.

**Component 2 — Card** (full width minus 32dp insets, top margin 24dp, 12dp corner radius, background #1E201A): Section header "Paying To" Outfit Medium 12sp #8F9285 uppercase with 16dp padding. Row: leading bank icon 24dp #A0CFCB in 40dp circle background #44483D, title "Landlord Holdings Ltd" Outfit Medium 14sp #E3E3D8, subtitle "GB29 NWBK 6016 1331 9268 19, NatWest Bank" Outfit Regular 12sp #8F9285. form archetype.

**Component 3 — Text Field** (full width minus 32dp insets, top margin 16dp): Outlined text field 56dp tall, 12dp corner radius, label "Amount" Outfit Regular 12sp #8F9285, value "1200.00" Outfit Regular 16sp #E3E3D8, leading "£" prefix #C5C8BA, outline 1dp #B2D188 (focused).

**Component 4 — Text Field** (full width minus 32dp insets, top margin 12dp): Outlined text field 56dp tall. Label "Currency" Outfit Regular 12sp #8F9285, value "GBP — British Pound" Outfit Regular 16sp #E3E3D8, trailing chevron 20dp #C5C8BA.

**Component 5 — Text Field** (full width minus 32dp insets, top margin 12dp): Outlined text field 56dp tall. Label "Frequency" Outfit Regular 12sp #8F9285, value "Monthly" Outfit Regular 16sp #E3E3D8, trailing chevron 20dp #C5C8BA.

**Component 6 — Text Field** (full width minus 32dp insets, top margin 12dp): Outlined text field 56dp tall. Label "Start Date" Outfit Regular 12sp #8F9285, value "1 Jan 2026" Outfit Regular 16sp #E3E3D8, trailing calendar icon 20dp #C5C8BA.

**Component 7 — Text Field** (full width minus 32dp insets, top margin 12dp): Outlined text field 56dp tall. Label "End Date (optional)" Outfit Regular 12sp #8F9285, value "Ongoing, no end date" Outfit Regular 16sp #8F9285 (placeholder style), trailing calendar icon 20dp #44483D.

**Component 8 — Button** (full width minus 32dp insets, top margin 24dp): Filled pill 52dp tall, 999dp corner radius, background #B2D188, label "Save Changes" Outfit SemiBold 16sp #1F3701 centered.

**Component 9 — Button** (full width minus 32dp insets, top margin 12dp, bottom 32dp): Outlined pill 52dp tall, 999dp corner radius, border 1dp #44483D, label "Cancel" Outfit Medium 16sp #C5C8BA centered.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. The earth-green accent #B2D188 on the active amount field outline and save button communicates clear primary action hierarchy, keeping the layout restrained and refined for this regulated financial editing context.
↑↑↑ MOCKUP PROMPT
