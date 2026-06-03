---
ui_yaml_sha: sha256:cards-ui-2026-06-02
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
content_hash: cards-error-2026-06-02

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: cards
state: error
state_visibility: error
viewmodel: CardsViewModel

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: /idea export
prompt_template_version: stitch-per-state-v3.0.0
generated_at: "2026-06-02"
---

# cards — error state

> Auto-generated from screens/cards/ui.yaml @ SHA 14e5d1ca015dc543
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the error state of the Cards screen for **Mifos X Open Banking**, a open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB.

**Component 1 — App Bar** (64dp tall, full width): Title "My Cards" Outfit SemiBold 20sp #E3E3D8 left-aligned 16dp. Zero elevation, background #12140E. error_state archetype.

**Component 2 — Hero** (centered, top margin 64dp): 160dp wide by 160dp tall illustration of a card with an X or disconnected plug, rendered in neutral tones #44483D and #8F9285 on #12140E.

**Component 3 — Hero** (centered, top margin 24dp, horizontal padding 32dp): "Could not load your cards" Outfit SemiBold 22sp #E3E3D8 centered, max 2 lines.

**Component 4 — List Row** (centered, top margin 8dp, horizontal padding 48dp): "Check your connection and try again. Your cards and limits are safe." Outfit Regular 14sp #8F9285 centered, max 25 words.

**Component 5 — Button** (full width minus 64dp insets, top margin 32dp): Filled pill button 48dp tall, 999dp corner radius, background #B2D188, leading refresh icon 20dp #1F3701, label "Retry" Outfit SemiBold 16sp #1F3701 centered.

**Component 6 — Button** (centered, top margin 16dp, bottom 32dp): Text button "Go back" Outfit Medium 14sp #8F9285.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Centered layout on #12140E. The earth-green accent #B2D188 on the retry button reassures the user that their financial data is secure while offering a calm recovery path.

↑↑↑ MOCKUP PROMPT
