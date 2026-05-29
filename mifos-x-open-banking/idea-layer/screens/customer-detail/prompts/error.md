---
ui_yaml_sha: 446998a2d04bdffe5c3942db1e66ab81cccc8fbd49ed6f0a6c91223077a1b2ce
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 4729ceecc8bd68f7b83aded0691479f614e6a132a3d2867d6076a2136741c4da

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: customer-detail
state: error
state_visibility: error

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# customer-detail — error state

> Auto-generated from screens/customer-detail/ui.yaml @ SHA 7bd205aa0765c808
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the customer detail screen for **Mifos X Open Banking**, a professional open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, secondary #A0CFCB, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Customer Detail" Outfit Medium 18sp #E3E3D8, leading back-arrow 24dp #B2D188, background #12140E.

**Component 2 — Hero** (centered, top margin 64dp): 140dp illustration of a broken data connection in neutral #44483D / #8F9285 on #12140E.

**Component 3 — List Row** (centered, top margin 24dp, horizontal padding 48dp): Title "Could not load customer" Outfit SemiBold 20sp #E3E3D8 centered. Subtitle "Check your connection and try again. Customer data is preserved." Outfit Regular 14sp #C5C8BA centered. error_state archetype.

**Component 4 — Button** (full width minus 64dp insets, top margin 32dp, 48dp tall, 24dp corner radius, background #B2D188, leading refresh icon 20dp #1F3701, label "Retry" Outfit SemiBold 15sp #1F3701).

**Component 5 — Button** (centered, top margin 12dp): Text button "Go back" Outfit Medium 14sp #8F9285.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Centered layout on #12140E. Anchored by #B2D188 on the retry action, the layout stays calm and restrained, preserving composure for field officers in a regulated banking environment.

↑↑↑ MOCKUP PROMPT
