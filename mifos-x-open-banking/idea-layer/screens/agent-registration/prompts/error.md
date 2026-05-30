---
ui_yaml_sha: a468125e1106b883f7fa067dc586fd6b137420230253c4e395c0ea724594b5e7
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 6474e8b10fdd4cff6df85fc2e45a97fec49e34162f31cad500b66ec030df9250

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: agent-registration
state: error
state_visibility: error

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# agent-registration — error state

> Auto-generated from screens/agent-registration/ui.yaml @ SHA 71b496c1e03513c9
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the agent registration screen for **Mifos Open Banking**, a Kotlin Multiplatform open-banking super-app for consumer retail banking and field officer agent banking.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB, pending #E8A317, on_surface_variant #C5C8BA.

**Component 1 — App Bar** (64dp tall, full width): Title "Agent Registration" Outfit Medium 18sp #E3E3D8 centered. Background #12140E, zero elevation.

**Component 2 — Error Illustration** (centered, top margin 64dp): 160dp wide x 160dp tall illustration of a disconnected API plug or broken network link in neutral #44483D / #8F9285 tones on #12140E background. Conveys connectivity failure without harsh red tones.

**Component 3 — Error Title** (centered, top margin 24dp, horizontal padding 32dp): "Registration Unavailable" Outfit SemiBold 22sp #E3E3D8 centered, max 2 lines. error_state archetype.

**Component 4 — Error Subtext** (centered, top margin 8dp, horizontal padding 48dp): "Unable to reach the Open Bank Project server. Check your connection and try again." Outfit Regular 14sp #C5C8BA, line-height 20sp, centered, max 25 words.

**Component 5 — Retry Button** (full width minus 64dp insets, top margin 32dp): Filled pill Button 48dp tall, corner radius 999, background #B2D188, leading refresh icon 20dp #1F3701, label "Retry" Outfit SemiBold 16sp #1F3701 centered.

**Component 6 — Secondary Action** (centered, top margin 16dp): Text Button label "Go back" Outfit Medium 14sp #8F9285, no background.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Centered layout on #12140E with generous vertical breathing room. The #B2D188 retry button stays warm and encouraging; error tones remain neutral rather than alarming, preserving trust in a regulated banking context.

↑↑↑ MOCKUP PROMPT
