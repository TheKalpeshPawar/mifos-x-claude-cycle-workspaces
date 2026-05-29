---
ui_yaml_sha: 7077f6e070d0a7f1125c62a5ea1cc4d67d31364ecad1feced39956a7353733f4
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 7e3f6e29e35f164b616641dd803745ad262c93104c223eab5d7086b52f772803

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: settings
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# settings — loading state

> Auto-generated from screens/settings/ui.yaml @ SHA 83b470d9156355e0
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the settings screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar Shimmer** (64dp tall, full width): Shimmer rectangle 100dp wide x 20dp tall, centered. Shimmer base #1E201A, highlight #282A24, 1200ms sweep. Background #12140E. skeleton_screen archetype.

**Component 2 — Card Shimmer** (full width minus 32dp insets, top margin 24dp, 12dp corner radius, background #1E201A): Section header shimmer 60dp wide x 10dp tall at top. Two list row shimmers 56dp tall each with 1dp divider #282A24. Each row: left icon shimmer 20dp circle, two text shimmers (120dp x 14dp title, 180dp x 12dp subtitle) + right toggle shimmer 42dp x 24dp pill.

**Component 3 — Card Shimmer** (full width minus 32dp insets, top margin 16dp, 12dp corner radius, background #1E201A): Section header shimmer. Three list row shimmers 56dp tall each with 1dp dividers. Same row anatomy as Component 2.

**Component 4 — Card Shimmer** (full width minus 32dp insets, top margin 16dp, 12dp corner radius, background #1E201A): Section header shimmer. Three list row shimmers. Rows 1 toggle, Rows 2-3 chevron shimmer 16dp x 16dp square on trailing side instead of toggle.

**Component 5 — Card Shimmer** (full width minus 32dp insets, top margin 16dp, 12dp corner radius, background #1E201A): Section header shimmer. Four list row shimmers 52dp tall each, each trailing chevron shimmer 16dp x 16dp.

**Component 6 — Row Shimmer** (full width minus 32dp insets, top margin 12dp, bottom 32dp): Two inline text shimmers — 72dp x 12dp on left, 40dp x 12dp on right. No card background, plain layout.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Vertically scrollable layout on #12140E. Shimmer placeholders use #1E201A rest tone with #282A24 highlight at 1200ms, creating a calm structured skeleton that mirrors the four grouped card sections of the content state, calibrated to the professional open banking aesthetic.
↑↑↑ MOCKUP PROMPT
