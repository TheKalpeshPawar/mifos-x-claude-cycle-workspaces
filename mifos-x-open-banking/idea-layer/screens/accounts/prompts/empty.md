---
ui_yaml_sha: 06a74a064d747a5df855d29ceca0a54efe2937d3362989fcd2a1e8391bb18936
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: b7693abe0c1007a36c9dbca3f0289821468806d4d6ae913edd15a83f2be0481a

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: accounts
state: empty
state_visibility: empty

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# accounts — empty state

> Auto-generated from screens/accounts/ui.yaml @ SHA d9feb696ad11a5eb
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the empty state of the accounts screen for **Mifos X Open Banking**, a professional open banking KMP super-app serving consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, tertiary #A0CFCB, on_tertiary #003735, error #FFB4AB, on_error #690005, error_container #93000A, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16, scrim #000000.

**Component 1 — App Bar** (64dp tall, full width): Title "My Accounts" Outfit SemiBold 22sp #E3E3D8 left-aligned 16dp. Trailing help icon 24dp #8F9285. Background #12140E, 1dp bottom divider #44483D.

**Component 2 — Chip Row** (full width minus 32dp insets, top margin 12dp, 8dp gap): Four chips all outlined 1dp #44483D, 32dp tall, 16dp corner radius. "ALL" Outfit Regular 12sp #C5C8BA. "CHECKING". "SAVINGS". "BUSINESS". empty_state archetype.

**Component 3 — Hero** (centered, top margin 80dp, horizontal padding 48dp): 96dp wide x 96dp tall illustration of a bank building or empty wallet rendered in #44483D and #8F9285 tones. Centered on #12140E.

**Component 4 — App Bar** (centered, top margin 24dp, horizontal padding 32dp): "No accounts linked yet" Outfit SemiBold 20sp #E3E3D8 centered, max 2 lines.

**Component 5 — List Row** (centered, top margin 8dp, horizontal padding 40dp): "Connect your bank accounts through Open Banking to get started." Outfit Regular 14sp #C5C8BA centered, line-height 20sp, max 25 words.

**Component 6 — Button** (full width minus 64dp insets, 48dp tall, 24dp corner radius, top margin 32dp): Filled button background #354E16, label "Add Account" Outfit SemiBold 14sp #CDEDA3 centered.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The forest-green primary container #354E16 on the call-to-action communicates growth potential, turning the empty_state into a calm, balanced invitation rather than a dead end, refined for the financial aesthetic.
↑↑↑ MOCKUP PROMPT
