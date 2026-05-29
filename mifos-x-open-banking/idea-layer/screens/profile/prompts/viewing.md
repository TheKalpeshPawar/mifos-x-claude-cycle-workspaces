---
ui_yaml_sha: de0c641bb5454eb6bb91af4ba18a416b141b46ce0b2cad2598e56a2732ce7577
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 81c038c7a8a47343c57baad8a4e5fba58a6f5a2789ae3779dada6719b0c1736c

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: profile

feature: profile
state: viewing
state_visibility: viewing

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# profile — viewing state

> Auto-generated from screens/profile/ui.yaml @ SHA ab920b2a103528c9
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the viewing state of the profile screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "My Profile" Outfit Medium 18sp #E3E3D8 centered. Trailing edit icon 24dp #B2D188. Background #12140E, 1dp bottom divider #44483D. profile archetype.

**Component 2 — Avatar Section** (centered, top padding 32dp): 96dp circular avatar photo "Maria Santos". Display name "Maria Santos" Outfit SemiBold 20sp #E3E3D8, top margin 12dp. "Field Officer, Mifos Initiative" Outfit Regular 13sp #A0CFCB below name.

**Component 3 — Info Card** (full width minus 32dp insets, top margin 24dp, 12dp radius): Surface #1E201A, 16dp padding. Section "Personal Information" Outfit SemiBold 12sp #8F9285 uppercase. List Rows 48dp: Full Name "Maria Santos" Outfit Regular 14sp #E3E3D8, Email "maria.santos@email.com" Outfit Regular 14sp #C5C8BA, Phone "+44 7700 900123" Outfit Regular 14sp #C5C8BA. 1dp row dividers #44483D.

**Component 4 — Button Edit Profile** (full width minus 32dp insets, top margin 24dp, 48dp tall, pill): Filled #B2D188, label "Edit Profile" Outfit SemiBold 16sp #1F3701.

**Component 5 — Button Change Password** (full width minus 32dp insets, top margin 8dp, 48dp tall, pill): Outlined 1dp #44483D, label "Change Password" Outfit Medium 16sp #E3E3D8.

**Component 6 — Button Log Out** (full width minus 32dp insets, top margin 24dp, bottom 32dp, 48dp tall): Outlined 1dp #FFB4AB, label "Log Out" Outfit Medium 16sp #FFB4AB.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The #A0CFCB teal job-title label and #B2D188 Edit Profile button convey both professional identity and easy access to editing, keeping the experience calm, balanced, and refined.

↑↑↑ MOCKUP PROMPT
