---
ui_yaml_sha: 77ef7dbe843044a66b73b3c529d340294fe8b8804fa009b3a4c22aa5f5ddacab
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: d36e1e91a8a05677ec1c17aff8c18db3912132e72de3490d22a06981792354c6

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: consent-manager
state: revoke_confirm
state_visibility: revoke_confirm

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-manager — revoke_confirm state

> Auto-generated from screens/consent-manager/ui.yaml @ SHA 66a01a0a7ad03066
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the revoke_confirm state of the consent manager screen for **Mifos X Open Banking**, a professional open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, secondary #A0CFCB, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Connected Apps" Outfit Medium 18sp #E3E3D8, leading back-arrow 24dp #B2D188, background #12140E, scrim overlay #000000 at 40% opacity on screen content behind dialog.

**Component 2 — Card** (dialog surface, full width minus 32dp insets, centered vertically, 16dp corner radius, background #1E201A, elevation shadow): Title "Revoke access?" Outfit SemiBold 18sp #E3E3D8. Body "This will immediately remove this app's access to your account data. You can reconnect at any time." Outfit Regular 14sp #C5C8BA top margin 8dp.

**Component 3 — Button** (Cancel action, full width minus 16dp insets inside dialog, 44dp tall, top margin 24dp): Outlined button 8dp corner radius outline 1dp #44483D, label "Cancel" Outfit Medium 15sp #E3E3D8.

**Component 4 — Button** (Revoke action, same width, top margin 8dp): Filled button 44dp tall 8dp corner radius background #FFB4AB, label "Revoke" Outfit SemiBold 15sp #690005.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Dialog on scrimmed #12140E. The warm coral #FFB4AB on the destructive Revoke button clearly signals irreversibility while remaining within the trusted earth-tone palette, calibrated to the taste-default aesthetic.

↑↑↑ MOCKUP PROMPT
