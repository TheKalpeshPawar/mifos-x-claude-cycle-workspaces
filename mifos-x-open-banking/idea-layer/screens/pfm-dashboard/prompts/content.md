---
ui_yaml_sha: 0bdbdfde5fd7ed1e026905eb4d108b80cd86d133a71869b65d6b021e69bfe215
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 035cd25e1b1ee44d9564df2fca69d83135ff881cebbc9b815353362b05fa4d09

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: pfm-dashboard
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# pfm-dashboard — content state

> Auto-generated from screens/pfm-dashboard/ui.yaml @ SHA aef534c365877d82
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.
> Composition split across section files (Stitch composes them by name).

## Archetype: screen

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## State-specific behavior
- Fully populated with the real demo content listed below.

## Composition (top → bottom) — split into 2 sections
1. **section-1** — see screens/pfm-dashboard/prompts/content.section-1.md
2. **section-2** — see screens/pfm-dashboard/prompts/content.section-2.md

## Content source manifest
- (none)

↓↓↓ MOCKUP PROMPT

Design the content state of the pfm-dashboard screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Money Overview" Outfit Medium 18sp #E3E3D8 left-aligned 16dp. Background #12140E, 1dp bottom divider #44483D.

**Component 2 — Chip Row** (full width minus 32dp insets, top margin 12dp, horizontally scrollable): 4 filter chips, 32dp tall, 16dp corner radius, 8dp gap. "This Month" filled #354E16 label #CDEDA3 Outfit Medium 13sp. "Last Month", "Last 3 Months", "Custom" outlined 1dp #44483D label #C5C8BA Outfit Regular 13sp.

**Component 3 — Summary Card** (full width minus 32dp insets, top margin 16dp, 100dp tall, 12dp radius): Surface #1E201A, 16dp padding. Three columns: "Spent" label Outfit Regular 12sp #8F9285 + "£1,847.32" Outfit SemiBold 20sp #E3E3D8. "Received" label + "£3,200.00" #B2D188. "Net" label + "+£1,352.68" #B2D188.

**Component 4 — Budget Progress Card** (full width minus 32dp insets, top margin 12dp, 12dp radius): Surface #1E201A, 16dp padding. Header row: "Overall Budget" Outfit Medium 14sp #E3E3D8 left, "73%" Outfit SemiBold 14sp #B2D188 right. Amounts row: "£1,847 spent" left #C5C8BA, "£683 remaining" right #8F9285. Progress track 6dp tall, 8dp radius, base #44483D, fill 73% width #B2D188. Footnote "of £2,530 monthly budget" Outfit Regular 11sp #8F9285.

**Component 5 — Category Section Header** (full width minus 32dp insets, top margin 20dp): "Spending by Category" Outfit SemiBold 14sp #E3E3D8.

**Component 6 — Category List** (full width minus 32dp insets, top margin 8dp, surface #1E201A, 12dp radius): 5 List Row rows 48dp each, 1dp dividers #44483D. Food & Dining: dot #B2D188, "£624.18" trailing. Transport: dot #A0CFCB, "£287.50". Shopping: dot #CDEDA3, "£531.90". Bills: dot #8F9285, "£245.00". Entertainment: dot #44483D, "£158.74".

**Component 7 — Budgets Section Header** (full width minus 32dp insets, top margin 20dp): "Budget Breakdown" Outfit SemiBold 14sp #E3E3D8. "Manage" text Button Outfit Medium 13sp #B2D188 trailing.

**Component 8 — Budget Cards** (full width minus 32dp insets, top margin 8dp): 5 Cards, each 80dp tall, 12dp radius, surface #1E201A. Each shows category name Outfit Medium 14sp + "£X spent / £Y budget" Outfit Regular 12sp #8F9285 + progress bar 4dp fill: Food #B2D188, Transport #A0CFCB, Shopping #CDEDA3, Bills #8F9285, Entertainment #44483D.

**Component 9 — Top Merchants Header** (full width minus 32dp insets, top margin 20dp): "Top Merchants" Outfit SemiBold 14sp #E3E3D8.

**Component 10 — Merchants List** (full width minus 32dp insets, top margin 8dp, surface #1E201A, 12dp radius): 4 List Rows. Tesco, Netflix, Spotify, TfL — each row shows merchant name Outfit Medium 14sp #E3E3D8, category Outfit Regular 12sp #8F9285, amount Outfit SemiBold 14sp #E3E3D8 trailing.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The sage-green #B2D188 progress fills and budget percentages keep financial oversight calm and balanced, reinforcing a restrained, purposeful approach to personal money management.

↑↑↑ MOCKUP PROMPT
