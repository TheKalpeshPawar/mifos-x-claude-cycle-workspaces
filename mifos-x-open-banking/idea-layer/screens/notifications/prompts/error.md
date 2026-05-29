---
ui_yaml_sha: 3fd23727025f84161f07e7aec5d0eac94651cf54a8c6617a21f7b92e54ebab5a
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: fa40bb1a242d3424da32e0734ce2660d7db8755fe917974e36d102b68504ecb2

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: notifications
state: error
state_visibility: error

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# notifications — error state

> Auto-generated from screens/notifications/ui.yaml @ SHA c17a28e9c48c1430
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the notifications screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Notifications" Outfit Medium 18sp #E3E3D8 left-aligned 16dp padding. Background #12140E, zero elevation, 1dp bottom divider #44483D. error_state archetype.

**Component 2 — Error Illustration** (centered, top margin 64dp, 160dp wide, 160dp tall): Disconnected signal or broken chain icon rendered in neutral tones #44483D / #8F9285 on #12140E. No harsh red. Conveys connectivity failure without alarm.

**Component 3 — Error Title** (centered, top margin 24dp, horizontal padding 32dp): "Couldn't load notifications" Outfit SemiBold 22sp #E3E3D8, centered, max 2 lines.

**Component 4 — Error Subtext** (centered, top margin 8dp, horizontal padding 48dp): "Check your connection and try again. Your notification history will load when you are back online." Outfit Regular 14sp #8F9285, line-height 20sp, centered.

**Component 5 — Button** (full width minus 64dp insets, top margin 32dp): Filled pill Button 48dp tall, corner radius 999dp, background #B2D188, leading refresh icon 20dp #1F3701, label "Retry" Outfit SemiBold 16sp #1F3701.

**Component 6 — Secondary Action** (centered, top margin 16dp): Text Button label "Go back" Outfit Medium 14sp #8F9285, no background, no icon.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The sage-green #B2D188 Retry button provides a calm, non-alarming recovery action, keeping the error_state feeling stable rather than urgent, consistent with the regulated-industry aesthetic.

↑↑↑ MOCKUP PROMPT
