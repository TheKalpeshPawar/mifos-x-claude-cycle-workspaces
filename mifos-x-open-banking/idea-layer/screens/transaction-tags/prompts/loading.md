---
ui_yaml_sha: sha256:transaction-tags-ui-2026-06-02
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
content_hash: transaction-tags-loading-2026-06-02

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: transaction-tags
state: loading
state_visibility: loading
viewmodel: TransactionTagsViewModel

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: /idea export
prompt_template_version: stitch-per-state-v3.0.0
generated_at: "2026-06-02"
---

# transaction-tags — loading state

> Auto-generated from screens/transaction-tags/ui.yaml @ SHA 9b0d54a233059df6
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the transaction-tags screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317.

**Component 1 — App Bar Shimmer** (64dp tall, full width): Center shimmer rectangle 120dp wide x 20dp tall. Shimmer base #1E201A, highlight #282A24, 1200ms sweep. Background #12140E. skeleton_screen archetype.

**Component 2 — Card Shimmer** (full width minus 32dp insets, top margin 16dp, 12dp corner radius, 72dp tall, background #1E201A): Merchant shimmer 200dp x 18dp, amount shimmer 80dp x 22dp right-aligned, date shimmer 140dp x 12dp top margin 8dp.

**Component 3 — Section Shimmer** (full width minus 32dp insets, top margin 20dp): Title shimmer 40dp x 14dp, hint shimmer 120dp x 12dp top margin 6dp.

**Component 4 — Chip Row Shimmer** (full width minus 32dp insets, top margin 8dp, horizontally scrollable): 5 chip shimmers each 80dp wide x 32dp tall, 16dp corner radius, 8dp gap. Same shimmer spec.

**Component 5 — Text Field Shimmer** (full width minus 32dp insets, top margin 12dp, 56dp tall, 12dp corner radius): Outlined shimmer placeholder matching input shape.

**Component 6 — Text Field Shimmer** (full width minus 32dp insets, top margin 12dp, 80dp tall): Notes area shimmer.

**Component 7 — List Row Shimmer** (full width minus 32dp insets, top margin 8dp, 56dp tall): Leading icon circle shimmer 24dp, title shimmer 120dp x 14dp, subtitle shimmer 160dp x 12dp.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full vertically scrollable layout on pure #12140E. Shimmer placeholders use surface_container #1E201A as rest tone with #282A24 as highlight pulse, keeping the loading state calm and structured, calibrated to the trustworthy open banking aesthetic.
↑↑↑ MOCKUP PROMPT
