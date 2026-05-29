---
ui_yaml_sha: cef07cfa2ad24b80737c28638685e2e4d53b2eb4711914b0fcd2363e8d0b95e7
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 4d8cf987b2446524eb565c1b7ccdf5aeedbff8e7b1d6f1f0a714cf6775137c1a

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: settings

feature: about
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# about — content state

> Auto-generated from screens/about/ui.yaml @ SHA aa6d8b32b2f7e7ef
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the content state of the about screen for **Mifos X Open Banking**, a professional open banking KMP super-app serving consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, tertiary #A0CFCB, on_tertiary #003735, error #FFB4AB, on_error #690005, error_container #93000A, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16, scrim #000000.

**Component 1 — App Bar** (64dp tall, full width): Title "About" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow icon 24dp tinted #B2D188. Background #12140E, zero elevation, 1dp bottom divider #44483D.

**Component 2 — Card** (full width minus 32dp insets, 12dp corner radius, top margin 24dp, background #1E201A): Logo image centered 72dp diameter with 16dp top padding. Below logo: "Mifos X Open Banking" Outfit SemiBold 20sp #E3E3D8 centered, top margin 12dp. "Open Banking for Everyone" Outfit Regular 13sp #C5C8BA centered, top margin 4dp. settings archetype.

**Component 3 — Card** (full width minus 32dp insets, 12dp corner radius, top margin 16dp, background #1E201A): Two List Row items separated by 1dp divider #44483D. Row 1: "Version" Outfit Regular 14sp #C5C8BA on left, "1.0.0" Outfit Medium 14sp #E3E3D8 on right, 56dp tall. Row 2: "Build" Outfit Regular 14sp #C5C8BA on left, "2026.05.001" Outfit Medium 14sp #E3E3D8 on right, 56dp tall.

**Component 4 — Card** (full width minus 32dp insets, 12dp corner radius, top margin 16dp, background #1E201A): Header "Legal" Outfit Medium 12sp #B2D188 with 16dp horizontal padding, 40dp tall. Three List Row items, each 56dp tall, separated by 1dp dividers #44483D. "Terms of Service" Outfit Regular 14sp #E3E3D8 with trailing open-in-new icon 18dp #8F9285. "Privacy Policy" Outfit Regular 14sp #E3E3D8 with trailing open-in-new icon 18dp #8F9285. "Open Source Licenses" Outfit Regular 14sp #E3E3D8 with trailing chevron-right icon 18dp #8F9285.

**Component 5 — Button** (full width minus 64dp insets, 48dp tall, 24dp corner radius, top margin 24dp, bottom 32dp): Outlined button, outline 1dp #B2D188, label "Rate This App" Outfit Medium 14sp #B2D188 centered.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The earth-green accent #B2D188 on the app bar back arrow, legal section header, and rate button outline creates a calm, growth-oriented feel calibrated to the trust-first financial aesthetic, keeping the dark settings surface professional and unfussy.
↑↑↑ MOCKUP PROMPT
