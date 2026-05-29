---
ui_yaml_sha: 43bf8e879b37ae93b3ce62dd72bfb9fee6978b31c734296cf84770dbd633d439
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 0d58866900a766f55482e4c998abb7f5a26b1b27c0fb28ea12e47119388af107

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: direct-debit-detail
state: error
state_visibility: error

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# direct-debit-detail — error state

> Auto-generated from screens/direct-debit-detail/ui.yaml @ SHA 2b162b864315da3b
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the error state of the direct-debit-detail screen for **Mifos X Open Banking**, a mobile KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, error #FFB4AB, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title "Direct Debit" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow 24dp #B2D188. Background #12140E. error_state page header.

**Component 2 — Hero** (centered, top margin 80dp): Illustration 140dp x 140dp, broken document or disconnected cloud icon in #44483D/#8F9285 on #12140E. error_state illustration centered.

**Component 3 — App Bar** (centered, top margin 24dp, horizontal padding 32dp): "Couldn't load mandate details" Outfit SemiBold 22sp #E3E3D8, centered, max 2 lines.

**Component 4 — List Row** (centered, top margin 8dp, horizontal padding 48dp): "Please try again. Your mandate data is safe." Outfit Regular 14sp #8F9285, max 25 words, centered.

**Component 5 — Button** (full width minus 64dp insets, top margin 32dp): Filled pill 48dp, 999dp radius, #B2D188, leading refresh icon 20dp #1F3701, label "Try Again" Outfit SemiBold 14sp #1F3701.

**Component 6 — Button** (centered, top margin 12dp): Text button "Go back" Outfit Medium 14sp #8F9285, no background.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Centered layout on #12140E. The earth-green #B2D188 retry action keeps the error_state calm and balanced, consistent with the restrained taste-default banking aesthetic.
↑↑↑ MOCKUP PROMPT
