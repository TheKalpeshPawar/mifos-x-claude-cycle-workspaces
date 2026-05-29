---
ui_yaml_sha: 8fde56d823f64b22e73128c521f3d219cbfb577b1e9cfd8a956cf1e623771788
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 9e83a246428aad974345483a8d8e6e928e0132789b6808bd1518014226c48dfc

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: standing-order-edit
state: error
state_visibility: error

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# standing-order-edit — error state

> Auto-generated from screens/standing-order-edit/ui.yaml @ SHA 274924aa33d0f019
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the error state of the standing order edit screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title "Edit Standing Order" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow 24dp #B2D188. Background #12140E, zero elevation.

**Component 2 — Hero** (centered, top margin 64dp): 160dp x 160dp illustration of a broken pencil or save-failed icon rendered in neutral charcoal tones #44483D / #8F9285 on #12140E. Conveys save failure without alarming visuals. error_state archetype.

**Component 3 — Text** (centered, top margin 24dp, horizontal padding 32dp): "Changes could not be saved" Outfit SemiBold 22sp #E3E3D8 centered, max 2 lines.

**Component 4 — Text** (centered, top margin 8dp, horizontal padding 48dp): "Couldn't save your changes. Check the amount and try again." Outfit Regular 14sp #8F9285 centered, line-height 20sp, max 25 words.

**Component 5 — Button** (full width minus 64dp insets, top margin 32dp): Filled pill button 48dp tall, 999dp corner radius, background #B2D188, leading refresh icon 20dp #1F3701, label "Retry" Outfit SemiBold 16sp #1F3701 centered.

**Component 6 — Button** (centered, top margin 16dp, bottom 48dp): Text button "Cancel" Outfit Medium 14sp #8F9285, no background, 48dp tap target.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Centered layout on #12140E with generous breathing room. The earthy green #B2D188 on the retry button provides a calm and trustworthy recovery action, keeping the error state composed rather than alarming within the regulated open banking aesthetic.
↑↑↑ MOCKUP PROMPT
