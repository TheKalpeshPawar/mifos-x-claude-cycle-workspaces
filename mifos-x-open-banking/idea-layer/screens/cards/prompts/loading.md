---
ui_yaml_sha: sha256:cards-ui-2026-06-02
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
content_hash: cards-loading-2026-06-02

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: cards
state: loading
state_visibility: loading
viewmodel: CardsViewModel

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: /idea export
prompt_template_version: stitch-per-state-v3.0.0
generated_at: "2026-06-02"
---

# cards — loading state

> Auto-generated from screens/cards/ui.yaml @ SHA 00da625d1df59494
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the Cards screen for **Mifos X Open Banking**, a open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB.

**Component 1 — App Bar Shimmer** (64dp tall, full width): Shimmer rectangle 80dp by 24dp left-aligned 16dp. Base #1E201A, highlight #282A24, 1200ms sweep. Background #12140E. skeleton_screen archetype.

**Component 2 — Card Shimmer** (full width minus 32dp insets, top margin 24dp, 192dp tall): Large card shimmer 16dp corner radius. Three shimmer lines at bottom (pan, name, expiry). Top-right spot shimmer. Same 1200ms sweep.

**Component 3 — Chip Row Shimmer** (full width minus 32dp insets, top margin 16dp): 4 shimmer chips each 80dp wide by 40dp tall, 20dp corner radius, 8dp gap.

**Component 4 — Section Header Shimmer** (full width minus 32dp insets, top margin 24dp): Row shimmer 140dp by 16dp left, 60dp by 14dp right.

**Component 5 — List Row Shimmer** (full width minus 32dp insets, top margin 8dp, 64dp tall): Leading 32dp square shimmer. Title 180dp by 16dp, subtitle 80dp by 12dp stacked right. Trailing 60dp by 16dp.

**Component 6 — List Row Shimmer** (full width minus 32dp insets, top margin 4dp, 64dp tall): Same shape.

**Component 7 — List Row Shimmer** (full width minus 32dp insets, top margin 4dp, 64dp tall): Same shape.

**Component 8 — List Row Shimmer** (full width minus 32dp insets, top margin 4dp, 64dp tall): Same shape.

**Component 9 — List Row Shimmer** (full width minus 32dp insets, top margin 4dp, bottom 24dp, 64dp tall): Same shape.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full scrollable layout on #12140E. Shimmer uses surfaceContainer #1E201A rest with #282A24 sweep, producing a calm, predictable loading state that mirrors the content layout precisely, calibrated to the trust-first banking aesthetic.

↑↑↑ MOCKUP PROMPT
