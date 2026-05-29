---
ui_yaml_sha: de0c641bb5454eb6bb91af4ba18a416b141b46ce0b2cad2598e56a2732ce7577
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 5385b7822074df6cee3b51f48fb5c305fc5a92c9761a23cbb610c3dd10c50c9a

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: profile

feature: profile
state: saving
state_visibility: saving

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# profile — saving state

> Auto-generated from screens/profile/ui.yaml @ SHA 1b88633d054bd26c
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the saving state of the profile screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "My Profile" Outfit Medium 18sp #E3E3D8 centered. Background #12140E, 1dp bottom divider #44483D. profile archetype.

**Component 2 — Avatar Section** (centered, top padding 24dp): 96dp circular avatar photo. "Maria Santos" Outfit SemiBold 20sp #E3E3D8 below.

**Component 3 — Form Fields Disabled** (full width minus 32dp insets, top margin 24dp): Three Text Fields in disabled state — Full Name "Maria Santos", Email "maria.santos@email.com", Phone "+44 7700 900123". Outlined #282A24 (muted). Labels and values #8F9285.

**Component 4 — Button Save (loading)** (full width minus 32dp insets, top margin 24dp, 48dp tall, pill): Filled #354E16 (muted active), circular progress indicator 20dp #B2D188 centered. Label hidden. Disabled tap response.

**Component 5 — Button Change Password (disabled)** (full width minus 32dp insets, top margin 8dp, 48dp tall, pill): Outlined #282A24, label "Change Password" Outfit Medium 16sp #44483D.

**Component 6 — Progress Bar** (full width, top 0dp): Indeterminate linear progress bar 4dp tall at screen top, color #B2D188, animated left-to-right sweep.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The #B2D188 indeterminate progress bar and spinner communicate active data submission with restrained, balanced motion, keeping the saving state calm and composed throughout.

↑↑↑ MOCKUP PROMPT
