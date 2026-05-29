---
ui_yaml_sha: 0bdbdfde5fd7ed1e026905eb4d108b80cd86d133a71869b65d6b021e69bfe215
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 823b51c41d473e7aaa34136d4b428488f9b2c6719159886d63c0e993be4b3740

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: pfm-dashboard
state: error
state_visibility: error

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# pfm-dashboard — error state

> Auto-generated from screens/pfm-dashboard/ui.yaml @ SHA 5eab2f2bb3a57e8a
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.
> Composition split across section files (Stitch composes them by name).

## Archetype: screen

## Layout
- type: scrollable_column
- padding: default
- alignment: start

## State-specific behavior
- Show an error illustration, a short message, and a single Retry action. No content rails visible.

## Composition (top → bottom) — split into 2 sections
1. **section-1** — see screens/pfm-dashboard/prompts/error.section-1.md
2. **section-2** — see screens/pfm-dashboard/prompts/error.section-2.md

## Content source manifest
- (none)

↓↓↓ MOCKUP PROMPT

Design the error state of the pfm-dashboard screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Money Overview" Outfit Medium 18sp #E3E3D8 left-aligned 16dp. Background #12140E, 1dp bottom divider #44483D. error_state archetype.

**Component 2 — Period Chip Row** (full width minus 32dp insets, top margin 16dp, scrollable): 4 chips outlined #44483D, labels #C5C8BA Outfit Regular 13sp. Chips are visible but disabled appearance.

**Component 3 — Error Illustration** (centered, top margin 64dp, 160dp wide, 160dp tall): Broken chart outline or disconnected graph in #44483D / #8F9285 on #12140E. No red. Calm financial error visual.

**Component 4 — Error Title** (centered, top margin 24dp, horizontal padding 32dp): "Couldn't load your finances" Outfit SemiBold 22sp #E3E3D8, centered, max 2 lines.

**Component 5 — Error Subtext** (centered, top margin 8dp, horizontal padding 48dp): "Check your connection and try again. Your spending data will be available once you reconnect." Outfit Regular 14sp #8F9285, centered.

**Component 6 — Button** (full width minus 64dp insets, top margin 32dp): Filled pill Button 48dp tall, corner radius 999dp, background #B2D188, leading refresh icon 20dp #1F3701, label "Retry" Outfit SemiBold 16sp #1F3701.

**Component 7 — Secondary Action** (centered, top margin 16dp): Text Button "Go back" Outfit Medium 14sp #8F9285.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The #B2D188 Retry button maintains the calm, professional tone of the error_state, signaling that recovery is one tap away without heightening financial anxiety.

↑↑↑ MOCKUP PROMPT
