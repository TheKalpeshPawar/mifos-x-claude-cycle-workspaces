---
ui_yaml_sha: 8fde56d823f64b22e73128c521f3d219cbfb577b1e9cfd8a956cf1e623771788
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 403f410033c1678df20c9daebf649e2a26da2ffc88dde8a553508085040fb18f

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: standing-order-edit
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# standing-order-edit — loading state

> Auto-generated from screens/standing-order-edit/ui.yaml @ SHA c0506b2778c41868
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the standing order edit screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar Shimmer** (64dp tall, full width): Shimmer rectangle 160dp wide x 20dp tall, centered. Shimmer base #1E201A, highlight #282A24, 1200ms sweep. Background #12140E. skeleton_screen archetype.

**Component 2 — Card Shimmer** (full width minus 32dp insets, top margin 24dp, 12dp corner radius, background #1E201A): Beneficiary section placeholder. Header shimmer 60dp wide x 10dp. Row shimmer 56dp tall: left circle icon 40dp, two text lines (120dp x 14dp title, 200dp x 12dp subtitle) right-side.

**Component 3 — Text Field Shimmer** (full width minus 32dp insets, top margin 16dp): Rectangular shimmer block 56dp tall, 12dp corner radius. Same 1200ms sweep.

**Component 4 — Text Field Shimmer** (full width minus 32dp insets, top margin 12dp): Rectangular shimmer block 56dp tall, 12dp corner radius. 100ms phase offset.

**Component 5 — Text Field Shimmer** (full width minus 32dp insets, top margin 12dp): Rectangular shimmer block 56dp tall, 12dp corner radius. 200ms phase offset.

**Component 6 — Text Field Shimmer** (full width minus 32dp insets, top margin 12dp): Rectangular shimmer block 56dp tall, 12dp corner radius. 300ms phase offset.

**Component 7 — Text Field Shimmer** (full width minus 32dp insets, top margin 12dp): Rectangular shimmer block 56dp tall, 12dp corner radius. 400ms phase offset.

**Component 8 — Button Shimmer** (full width minus 32dp insets, top margin 24dp): Pill shimmer 52dp tall, 999dp corner radius, background #354E16.

**Component 9 — Button Shimmer** (full width minus 32dp insets, top margin 12dp, bottom 32dp): Pill shimmer 52dp tall, 999dp corner radius, background #1E201A, border 1dp #44483D.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Vertically scrollable layout on #12140E. Shimmer placeholders use #1E201A rest tone with #282A24 highlight at 1200ms cadence with staggered phase offsets per field, creating a calm structured skeleton_screen matching the input field layout of the content state, restrained and refined for this regulated open banking aesthetic.
↑↑↑ MOCKUP PROMPT
