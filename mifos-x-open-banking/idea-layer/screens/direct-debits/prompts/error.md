---
ui_yaml_sha: 311b028229aca9607374f911558008041fe6e2b5143fc5015fb945c2ad077cdc
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: ca80e82d17816d5b8275d9818a1100895156ebdb7f7eeb637d62c65ffe07a736

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: direct-debits
state: error
state_visibility: error

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# direct-debits — error state

> Auto-generated from screens/direct-debits/ui.yaml @ SHA a091dc9241bec836
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the error state of the direct-debits screen for **Mifos X Open Banking**, a mobile KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, error #FFB4AB, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title "Direct Debits" Outfit Medium 18sp #E3E3D8 left 16dp. Background #12140E. error_state page header.

**Component 2 — Hero** (centered, top margin 80dp): Illustration 140dp x 140dp, broken subscription or disconnected server in #44483D on #12140E. error_state illustration.

**Component 3 — App Bar** (centered, top margin 24dp, horizontal padding 32dp): "Couldn't load direct debits" Outfit SemiBold 22sp #E3E3D8 centered, max 2 lines.

**Component 4 — List Row** (centered, top margin 8dp, horizontal padding 48dp): "Please check your connection and try again." Outfit Regular 14sp #8F9285, max 25 words, centered.

**Component 5 — Button** (full width minus 64dp insets, top margin 32dp): Filled pill 48dp, 999dp radius, #B2D188, leading refresh icon 20dp #1F3701, label "Retry" Outfit SemiBold 14sp #1F3701.

**Component 6 — Bottom Nav** (64dp tall, full width): Payments selected #354E16/#B2D188. Others #8F9285. Background #1E201A, top 1dp #44483D.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Centered layout on #12140E. The earth-green #B2D188 retry keeps the error_state calm and balanced, consistent with the restrained taste-default banking aesthetic.
↑↑↑ MOCKUP PROMPT
