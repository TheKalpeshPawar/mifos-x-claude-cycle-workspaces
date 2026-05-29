---
ui_yaml_sha: de0c641bb5454eb6bb91af4ba18a416b141b46ce0b2cad2598e56a2732ce7577
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 992dad83b0655f65296200a49a8d71e92d10489e229e4ba21f56d1a384ce4098

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: profile
state: error
state_visibility: error

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# profile — error state

> Auto-generated from screens/profile/ui.yaml @ SHA 301ee6d497f75fc4
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the profile screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "My Profile" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow 24dp #B2D188. Background #12140E, 1dp bottom divider #44483D. error_state archetype.

**Component 2 — Error Illustration** (centered, top margin 64dp, 160dp wide, 160dp tall): Broken profile outline or disconnected user icon in #44483D / #8F9285 on #12140E. No red. Neutral, calm tone.

**Component 3 — Error Title** (centered, top margin 24dp, horizontal padding 32dp): "Couldn't load your profile" Outfit SemiBold 22sp #E3E3D8, centered, max 2 lines.

**Component 4 — Error Subtext** (centered, top margin 8dp, horizontal padding 48dp): "Check your connection and try again. We will sync your data the moment you're back online." Outfit Regular 14sp #8F9285, line-height 20sp.

**Component 5 — Button** (full width minus 64dp insets, top margin 32dp): Filled pill Button 48dp tall, corner radius 999dp, background #B2D188, leading refresh icon 20dp #1F3701, label "Retry" Outfit SemiBold 16sp #1F3701.

**Component 6 — Secondary Action** (centered, top margin 16dp): Text Button "Go back" Outfit Medium 14sp #8F9285.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The amber-calm #B2D188 Retry button in this error_state provides a warm, non-alarming primary action calibrated to the profile archetype, avoiding jarring the user who is trying to access their account identity.

↑↑↑ MOCKUP PROMPT
