---
ui_yaml_sha: f40389aebb44c1ab7cf7d41e2c7831d6dfd06eb9cf01fcd11f6806ecc71dc804
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: c6b2145e55a87fdc3607f7de02fbe2b85a0cc0fc7fb48adebbb9b7f1cefc3e91

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: send-money
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# send-money — loading state

> Auto-generated from screens/send-money/ui.yaml @ SHA e9e5b51eb19f391d
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the send money screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar Shimmer** (64dp tall, full width): Shimmer placeholder rectangle 120dp wide x 20dp tall, centered horizontally with 16dp top/bottom padding. Shimmer base #1E201A, highlight #282A24, animation duration 1200ms horizontal sweep. Background #12140E, zero elevation. skeleton_screen archetype.

**Component 2 — Text Field Shimmer** (full width minus 32dp insets, top margin 24dp): Rectangular shimmer block 56dp tall, 12dp corner radius. Same shimmer animation at 1200ms cadence.

**Component 3 — Text Field Shimmer** (full width minus 32dp insets, top margin 12dp): Rectangular shimmer block 56dp tall, 12dp corner radius. Same shimmer animation, 100ms phase offset.

**Component 4 — Text Field Shimmer** (full width minus 32dp insets, top margin 12dp): Rectangular shimmer block 56dp tall, 12dp corner radius. 200ms phase offset.

**Component 5 — Text Field Shimmer** (full width minus 32dp insets, top margin 12dp): Rectangular shimmer block 56dp tall, 12dp corner radius. 300ms phase offset.

**Component 6 — Chip Row Shimmer** (full width minus 32dp insets, top margin 16dp): Section label shimmer 80dp wide x 14dp tall. Below: two horizontally arranged chip shimmers, each 100dp wide x 40dp tall, 20dp corner radius, 8dp gap between chips.

**Component 7 — Text Field Shimmer** (full width minus 32dp insets, top margin 16dp): Rectangular shimmer block 56dp tall, 12dp corner radius.

**Component 8 — Card Shimmer** (full width minus 32dp insets, top margin 16dp, 12dp corner radius): Card placeholder 140dp tall. Section header shimmer 80dp wide x 14dp at 16dp from top. Three row shimmers 48dp tall each, separated by 1dp dividers #282A24.

**Component 9 — Card Shimmer** (full width minus 32dp insets, top margin 12dp, 12dp corner radius): Rectangular shimmer block 48dp tall. Background #1E201A.

**Component 10 — Button Shimmer** (full width minus 32dp insets, top margin 24dp, bottom 32dp): Pill shimmer 52dp tall, 999dp corner radius, background #1E201A with shimmer sweep.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full vertically scrollable layout on #12140E. Shimmer placeholders use #1E201A as the rest tone with #282A24 as the highlight pulse at 1200ms, keeping the loading state calm and steady rather than flickery, calibrated to the professional open banking aesthetic.
↑↑↑ MOCKUP PROMPT
