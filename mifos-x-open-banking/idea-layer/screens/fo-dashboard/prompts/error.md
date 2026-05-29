---
ui_yaml_sha: 4af6ba2fca8822ef1afa49c6800612d2eccac67ae5dd199e1c88a785018712c8
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: c77274afa7cde4f0d98c85807a69c794e27a965c7c2732208107770895fe072f

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: fo-dashboard
state: error
state_visibility: error

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# fo-dashboard — error state

> Auto-generated from screens/fo-dashboard/ui.yaml @ SHA 4f9c5551bb47c98e
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the fo-dashboard screen for **Mifos X Open Banking**, a Open Banking KMP super-app for consumer retail banking and field officer agent banking in emerging markets.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (full width, 64dp tall): Title "Dashboard" Outfit Medium 18sp #E3E3D8 centered. Trailing settings icon 24dp #8F9285. Background #12140E. Zero elevation.

**Component 2 — Hero** (centered, top margin 64dp): 160dp x 160dp illustration of a broken connection or disconnected network node rendered in #1E201A and #8F9285 tones on #12140E background. Conveys "something went wrong" without alarming red visuals. error_state archetype.

**Component 3 — App Bar** (centered, top margin 24dp, horizontal padding 32dp): Title "Couldn't load your dashboard" Outfit SemiBold 22sp #E3E3D8 centered, max 2 lines.

**Component 4 — List Row** (centered, top margin 8dp, horizontal padding 48dp): Subtext "Check your connection and try again. Your data will sync automatically once you are back online." Outfit Regular 14sp #C5C8BA line-height 20sp centered, max 25 words.

**Component 5 — Button** (full width minus 64dp insets, top margin 32dp): Filled pill button 48dp tall, 999dp corner radius, background #B2D188, leading refresh icon 20dp #1F3701, label "Retry" Outfit SemiBold 16sp #1F3701.

**Component 6 — Button** (centered, top margin 16dp): Text button "Go back" Outfit Medium 14sp #8F9285, no background, no icon.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Centered layout on #12140E with generous vertical breathing room. The earth-green #B2D188 retry button provides a calm, non-alarming recovery action calibrated to regulated financial contexts where trust must never erode.

↑↑↑ MOCKUP PROMPT
