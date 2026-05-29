---
ui_yaml_sha: c8c8040af254236430df923e229edc7208f4a0e351a42c63baa151d487b8456e
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 118d354d74dd92c895273a9e81e26fb1ccce01d815765302da73cb5728afacdb

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: atm-locator
state: empty
state_visibility: empty

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# atm-locator — empty state

> Auto-generated from screens/atm-locator/ui.yaml @ SHA c55708b8ad836480
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the empty state of the ATM Locator screen for **Mifos X Open Banking**, a open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB.

**Component 1 — App Bar** (64dp tall, full width): Title "ATM & Branches" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow icon 24dp tinted #B2D188. Zero elevation, background #12140E.

**Component 2 — Text Field** (full width minus 32dp insets, top margin 16dp): Outlined search field 56dp tall, 12dp corner radius, label "Search location" Outfit Regular 14sp #8F9285, leading search icon 20dp #C5C8BA, outline 1dp #44483D.

**Component 3 — Card** (centered, top margin 64dp, width 280dp): surfaceContainer #1E201A background, 16dp corner radius, 32dp padding, centered. 80dp circular illustration of a map-pin with dashed outline rendered in #44483D on #12140E. empty_state archetype.

**Component 4 — Hero** (centered, top margin 24dp, horizontal padding 32dp): Title "No ATMs or Branches Found" Outfit SemiBold 22sp #E3E3D8 centered, max 2 lines.

**Component 5 — List Row** (centered, top margin 8dp, horizontal padding 48dp): Subtext "Try searching a different address or enable location access to find nearby ATMs." Outfit Regular 14sp #8F9285 centered, line-height 20sp.

**Component 6 — Button** (full width minus 64dp insets, top margin 32dp): Filled pill button 48dp tall, 999dp corner radius, background #B2D188, leading location-dot icon 20dp #1F3701, label "Enable Location" Outfit SemiBold 16sp #1F3701 centered.

**Component 7 — Button** (centered, top margin 16dp, bottom 32dp): Text button label "Search Manually" Outfit Medium 14sp #8F9285, no background, no icon.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Centered layout on #12140E with generous vertical breathing room. The earth-green accent #B2D188 on the primary enable-location button provides a calm, accessible call-to-action calibrated to the trust-first regulated-industry aesthetic.
↑↑↑ MOCKUP PROMPT
