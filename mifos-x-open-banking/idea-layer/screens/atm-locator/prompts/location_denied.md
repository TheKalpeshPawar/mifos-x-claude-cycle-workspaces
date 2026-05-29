---
ui_yaml_sha: c8c8040af254236430df923e229edc7208f4a0e351a42c63baa151d487b8456e
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: c02e144e5287723fc018f57716b83caf16717c4e694dc04a2ccdee15676a3f73

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: atm-locator
state: location_denied
state_visibility: location_denied

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# atm-locator — location_denied state

> Auto-generated from screens/atm-locator/ui.yaml @ SHA be270b3eee731d07
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the location_denied state of the ATM Locator screen for **Mifos X Open Banking**, a open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB.

**Component 1 — App Bar** (64dp tall, full width): Title "ATM & Branches" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow icon 24dp tinted #B2D188. Zero elevation, background #12140E.

**Component 2 — Text Field** (full width minus 32dp insets, top margin 16dp): Outlined lookup field 56dp tall, 12dp corner radius, label "Find location" Outfit Regular 14sp #8F9285, outline 1dp #44483D. Disabled, non-interactive in this state.

**Component 3 — Card** (full width minus 32dp insets, top margin 16dp): surfaceContainerHigh #282A24 background, 12dp corner radius, 16dp padding. Left border accent 4dp #FFB4AB. Leading lock-location icon 24dp #FFB4AB. Content: "Location access denied" Outfit SemiBold 15sp #E3E3D8. Subtext: "Mifos X needs location permission to find ATMs near you." Outfit Regular 13sp #C5C8BA.

**Component 4 — Button** (full width minus 32dp insets, top margin 16dp): Filled button 48dp tall, 12dp corner radius, background #354E16, label "Open Preferences" Outfit SemiBold 15sp #CDEDA3, leading preferences icon 20dp #CDEDA3.

**Component 5 — List Row** (full width minus 32dp insets, top margin 24dp): Section header "Search by Address" Outfit SemiBold 13sp #8F9285 uppercase.

**Component 6 — Text Field** (full width minus 32dp insets, top margin 8dp): Active outlined lookup field 56dp tall, 12dp corner radius, label "Enter city, postcode or address" Outfit Regular 14sp #8F9285, focused outline 1dp #B2D188, leading find icon 20dp #B2D188.

**Component 7 — Button** (full width minus 32dp insets, top margin 12dp, bottom 32dp): Outlined button 48dp tall, 12dp corner radius, outline 1dp #B2D188, label "Find ATMs" Outfit Medium 15sp #B2D188.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full layout on #12140E. The earth-green accent #B2D188 on the manual lookup field and button redirects user focus toward a viable action, keeping the experience calm and balanced rather than blocking.
↑↑↑ MOCKUP PROMPT
