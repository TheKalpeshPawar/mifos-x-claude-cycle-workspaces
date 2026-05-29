---
ui_yaml_sha: de0c641bb5454eb6bb91af4ba18a416b141b46ce0b2cad2598e56a2732ce7577
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: cc7c099f9dcaa63395fd277175f680849a4a4a3c11b3b18deff98709e68bda9b

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: profile

feature: profile
state: saved
state_visibility: saved

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# profile — saved state

> Auto-generated from screens/profile/ui.yaml @ SHA b19f8f98fbaf0875
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the saved state of the profile screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "My Profile" Outfit Medium 18sp #E3E3D8 centered. Trailing preferences icon 24dp #8F9285. Background #12140E, 1dp bottom divider #44483D.

**Component 2 — Success Banner** (full width minus 32dp insets, top margin 16dp, 56dp tall, 12dp radius): Surface #354E16. Leading check-circle icon 20dp #B2D188. "Your profile has been updated successfully." Outfit Medium 14sp #CDEDA3. Banner slides in from top.

**Component 3 — Avatar Section** (centered, top margin 16dp): 96dp circular avatar photo. Display name "Maria Santos" Outfit SemiBold 20sp #E3E3D8 below. Email "maria.santos@email.com" Outfit Regular 13sp #8F9285.

**Component 4 — Input Fields** (full width minus 32dp insets, top margin 24dp): Three outlined Text Fields (Full Name "Maria Santos", Email "maria.santos@email.com" with lock, Phone "+44 7700 900123") in read-mode, outlined #44483D.

**Component 5 — Button Save** (full width minus 32dp insets, top margin 24dp, 48dp tall, pill): Filled #B2D188, label "Save Changes" Outfit SemiBold 16sp #1F3701 — visually active but non-interactive.

**Component 6 — Button Change Password** (full width minus 32dp insets, top margin 8dp, 48dp tall, pill): Outlined #44483D, label "Change Password" Outfit Medium 16sp #E3E3D8.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The #354E16 success banner with #B2D188 check icon communicates a successful save with calm confidence, keeping the overall experience balanced and restrained without over-celebrating.

↑↑↑ MOCKUP PROMPT
