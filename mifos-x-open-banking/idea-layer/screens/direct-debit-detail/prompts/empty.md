---
ui_yaml_sha: 43bf8e879b37ae93b3ce62dd72bfb9fee6978b31c734296cf84770dbd633d439
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 066fbeb4541de04d0e1adb6a986682abacb8caecfc38d1457fdb2f2921ec61db

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: direct-debit-detail
state: empty
state_visibility: empty

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# direct-debit-detail — empty state

> Auto-generated from screens/direct-debit-detail/ui.yaml @ SHA 6df574d89e5ec37c
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the empty state of the direct-debit-detail screen for **Mifos X Open Banking**, a mobile KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, error #FFB4AB, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title "Direct Debit" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow 24dp #B2D188. Background #12140E. empty_state page header.

**Component 2 — Hero** (centered, top margin 96dp): Illustration 140dp x 140dp, empty mandate folder icon in #44483D on #12140E. empty_state centered layout.

**Component 3 — App Bar** (centered, top margin 24dp, horizontal padding 48dp): "No mandate details" Outfit SemiBold 22sp #E3E3D8, centered.

**Component 4 — List Row** (centered, top margin 8dp, horizontal padding 48dp): "This direct debit has no data available. Please go back and try again." Outfit Regular 14sp #8F9285, max 25 words, centered.

**Component 5 — Button** (full width minus 64dp insets, top margin 40dp): Filled pill 48dp, 999dp radius, #B2D188, label "Go Back" Outfit SemiBold 14sp #1F3701.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Centered layout on #12140E. The earth-green #B2D188 back action in the empty_state keeps the user journey calm and balanced, aligned with the restrained taste-default banking aesthetic.
↑↑↑ MOCKUP PROMPT
