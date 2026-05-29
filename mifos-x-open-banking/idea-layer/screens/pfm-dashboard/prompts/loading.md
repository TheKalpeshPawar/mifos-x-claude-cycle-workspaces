---
ui_yaml_sha: 0bdbdfde5fd7ed1e026905eb4d108b80cd86d133a71869b65d6b021e69bfe215
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 098fa1d041a18cee38889bff802b5c7474e47fbb87155d3a10c17119e71ad7b8

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: pfm-dashboard
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# pfm-dashboard — loading state

> Auto-generated from screens/pfm-dashboard/ui.yaml @ SHA a02b882805629056
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.
> Composition split across section files (Stitch composes them by name).

## Archetype: screen

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## State-specific behavior
- Show shimmer/skeleton loaders matching the content layout block-for-block — no real text, no images. Initial state.

## Composition (top → bottom) — split into 2 sections
1. **section-1** — see screens/pfm-dashboard/prompts/loading.section-1.md
2. **section-2** — see screens/pfm-dashboard/prompts/loading.section-2.md

## Content source manifest
- (none)

↓↓↓ MOCKUP PROMPT

Design the loading state of the pfm-dashboard screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar Shimmer** (64dp tall, full width): Title placeholder 120dp wide, 20dp tall shimmer left-aligned 16dp. Shimmer base #1E201A, highlight #282A24, 1200ms sweep. Background #12140E. skeleton_screen archetype.

**Component 2 — Chip Row Shimmer** (full width minus 32dp insets, top margin 16dp): 4 pill shimmers 80dp wide, 32dp tall, 16dp radius, 8dp gap.

**Component 3 — Summary Card Shimmer** (full width minus 32dp insets, top margin 16dp, 100dp tall, 12dp radius): Three column shimmers — each 60dp wide, two stacked lines 48dp + 32dp tall, base #1E201A.

**Component 4 — Budget Card Shimmer** (full width minus 32dp insets, top margin 12dp, 80dp tall, 12dp radius): Title shimmer 100dp, amounts shimmer 160dp, progress track shimmer 6dp tall full width.

**Component 5 — Section Header Shimmer** (full width minus 32dp insets, top margin 20dp): 140dp wide, 18dp tall shimmer block.

**Component 6 — Category Rows Shimmer** (full width minus 32dp insets, top margin 8dp, surface #1E201A, 12dp radius): 5 rows 48dp each, each with 12dp dot shimmer left, 100dp text shimmer center, 60dp amount shimmer right.

**Component 7 — Budget Cards Shimmer** (full width minus 32dp insets, top margin 8dp): 5 cards 72dp tall, 12dp radius each, category name shimmer + progress bar shimmer 4dp.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The #1E201A to #282A24 shimmer sweep across card-shaped skeleton_screen blocks keeps the loading experience calm and structured, each pulse hinting at the financial clarity about to arrive.

↑↑↑ MOCKUP PROMPT
