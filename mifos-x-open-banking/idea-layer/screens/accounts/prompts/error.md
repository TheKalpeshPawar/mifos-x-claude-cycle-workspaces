---
ui_yaml_sha: 06a74a064d747a5df855d29ceca0a54efe2937d3362989fcd2a1e8391bb18936
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 1941e8e541eb121901ee130fd0d3fd6a5e00cbba0524cf0e6c723b5ffdfe0e86

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: accounts
state: error
state_visibility: error

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# accounts — error state

> Auto-generated from screens/accounts/ui.yaml @ SHA 5b1292d8bc6c7dd0
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the error state of the accounts screen for **Mifos X Open Banking**, a professional open banking KMP super-app serving consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, tertiary #A0CFCB, on_tertiary #003735, error #FFB4AB, on_error #690005, error_container #93000A, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16, scrim #000000.

**Component 1 — App Bar** (64dp tall, full width): Title "My Accounts" Outfit SemiBold 22sp #E3E3D8 left-aligned 16dp. Trailing help icon 24dp #8F9285. Background #12140E, 1dp bottom divider #44483D.

**Component 2 — Hero** (centered, top margin 64dp): 160dp wide x 140dp tall illustration of a disconnected bank link or broken chain rendered in neutral tones #44483D and #8F9285 on #12140E background. error_state archetype with generous vertical breathing room.

**Component 3 — App Bar** (centered, top margin 24dp, horizontal padding 32dp): "Could not load accounts" Outfit SemiBold 22sp #E3E3D8 centered, max 2 lines.

**Component 4 — List Row** (centered, top margin 8dp, horizontal padding 48dp): "Check your internet connection and try again. Your account data is secure." Outfit Regular 14sp #C5C8BA centered, line-height 20sp, max 25 words.

**Component 5 — Button** (full width minus 64dp insets, 48dp tall, 24dp corner radius, top margin 32dp): Filled pill button background #B2D188, leading refresh icon 20dp #1F3701, label "Retry" Outfit SemiBold 16sp #1F3701.

**Component 6 — Button** (centered, top margin 16dp): Text button "Go back" Outfit Medium 14sp #8F9285, no background, no icon.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The warm earth-green #B2D188 retry button provides a non-alarming primary action on the deep #12140E canvas, reinforcing financial security and calm recovery in the error_state.
↑↑↑ MOCKUP PROMPT
