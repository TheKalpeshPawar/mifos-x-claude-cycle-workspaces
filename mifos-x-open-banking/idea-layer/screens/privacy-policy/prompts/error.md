---
ui_yaml_sha: 0a37b7fd9f646c61727fc05be65e3aeffc9773a1b4f8cf66f1064cde39077166
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 1e101d3e0fb7d073a1ca8f00d8949dd3d8f664062095dd05d1d0de1f77250014

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: privacy-policy
state: error
state_visibility: error

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# privacy-policy — error state

> Auto-generated from screens/privacy-policy/ui.yaml @ SHA 10b53bf0f01737d3
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the privacy-policy screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Privacy Policy" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow 24dp #B2D188. Background #12140E, 1dp bottom divider #44483D. error_state archetype.

**Component 2 — Error Illustration** (centered, top margin 64dp, 160dp wide, 160dp tall): Broken document or disconnected shield icon in #44483D / #8F9285 on #12140E. No red. Calm, neutral tone appropriate for a policy document failure.

**Component 3 — Error Title** (centered, top margin 24dp, horizontal padding 32dp): "Unable to load Privacy Policy" Outfit SemiBold 22sp #E3E3D8, centered, max 2 lines.

**Component 4 — Error Subtext** (centered, top margin 8dp, horizontal padding 48dp): "Please check your connection and try again." Outfit Regular 14sp #8F9285, line-height 20sp, centered.

**Component 5 — Button** (full width minus 64dp insets, top margin 32dp): Filled pill Button 48dp tall, corner radius 999dp, background #B2D188, leading refresh icon 20dp #1F3701, label "Retry" Outfit SemiBold 16sp #1F3701.

**Component 6 — Secondary Action** (centered, top margin 16dp): Text Button "Go back" Outfit Medium 14sp #8F9285.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The #B2D188 Retry button in this error_state keeps the experience calm and balanced, ensuring users in a regulated-industry context feel composed rather than alarmed when a policy document fails to load.

↑↑↑ MOCKUP PROMPT
