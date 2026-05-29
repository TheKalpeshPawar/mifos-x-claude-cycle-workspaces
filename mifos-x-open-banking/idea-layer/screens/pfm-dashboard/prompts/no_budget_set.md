---
ui_yaml_sha: 0bdbdfde5fd7ed1e026905eb4d108b80cd86d133a71869b65d6b021e69bfe215
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 71affc6aed65da6431786eab63159bb10311afe8956f14a01007937fdefcd2d3

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: pfm-dashboard
state: no_budget_set
state_visibility: no_budget_set

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# pfm-dashboard — no_budget_set state

> Auto-generated from screens/pfm-dashboard/ui.yaml @ SHA a44f82301b8ca71c
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.
> Composition split across section files (Stitch composes them by name).

## Archetype: screen

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## State-specific behavior
- Custom state "No Budget Set".

## Composition (top → bottom) — split into 2 sections
1. **section-1** — see screens/pfm-dashboard/prompts/no_budget_set.section-1.md
2. **section-2** — see screens/pfm-dashboard/prompts/no_budget_set.section-2.md

## Content source manifest
- (none)

↓↓↓ MOCKUP PROMPT

Design the no_budget_set state of the pfm-dashboard screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Money Overview" Outfit Medium 18sp #E3E3D8 left-aligned 16dp. Background #12140E, 1dp bottom divider #44483D.

**Component 2 — Period Chip Row** (full width minus 32dp insets, top margin 16dp, scrollable): "This Month" filled #354E16 #CDEDA3, others outlined #44483D #C5C8BA. 32dp tall, 16dp radius.

**Component 3 — Summary Card** (full width minus 32dp insets, top margin 16dp, 100dp tall, 12dp radius): Surface #1E201A. Three columns Spent / Received / Net with real values. Spent "£1,847.32" #E3E3D8, Received "£3,200.00" #B2D188, Net "+£1,352.68" #B2D188.

**Component 4 — No Budget Banner** (full width minus 32dp insets, top margin 16dp, 12dp radius, 16dp padding): Surface #282A24, left border 3dp #B2D188. Title "No budget set" Outfit SemiBold 14sp #E3E3D8. Body "Set monthly limits to track your spending by category and stay on target." Outfit Regular 13sp #C5C8BA, max 2 lines. Button "Set Up Budget" filled #B2D188 label #1F3701 Outfit SemiBold 14sp, 40dp tall, pill shape.

**Component 5 — Category Section** (full width minus 32dp insets, top margin 20dp): Header "Spending by Category" Outfit SemiBold 14sp #E3E3D8. Category list surface #1E201A, 5 rows: Food £624.18, Transport £287.50, Shopping £531.90, Bills £245.00, Entertainment £158.74 with color dots.

**Component 6 — Merchants Section** (full width minus 32dp insets, top margin 20dp): Header "Top Merchants" Outfit SemiBold 14sp #E3E3D8. 4 List Rows: Tesco, Netflix, Spotify, TfL with amounts.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The #B2D188 left border on the No Budget Banner and its matching CTA create a calm, balanced call-to-action signal, guiding users toward budget setup with minimal visual friction.

↑↑↑ MOCKUP PROMPT
