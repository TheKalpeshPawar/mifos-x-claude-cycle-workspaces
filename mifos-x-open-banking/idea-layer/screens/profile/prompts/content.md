---
ui_yaml_sha: de0c641bb5454eb6bb91af4ba18a416b141b46ce0b2cad2598e56a2732ce7577
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: bc5fb7f937574c7a3593fd9a231aee9a26ed094b7b92d50db08f80160af79ffb

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: profile

feature: profile
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# profile — content state

> Auto-generated from screens/profile/ui.yaml @ SHA ceef31ac688cbbb9
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the profile screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "My Profile" Outfit Medium 18sp #E3E3D8 centered. Trailing preferences icon 24dp #8F9285. Background #12140E, 1dp bottom divider #44483D.

**Component 2 — Avatar Section** (centered, top padding 24dp): 96dp diameter circular avatar with photo. Bottom-right edit badge 32dp circle #B2D188, pencil icon 18dp #1F3701.

**Component 3 — Display Name** (centered, top margin 12dp): "Maria Santos" Outfit SemiBold 20sp #E3E3D8. Below it "maria.santos@email.com" Outfit Regular 13sp #8F9285.

**Component 4 — Section Header** (full width minus 32dp insets, top margin 24dp): "Personal Information" Outfit SemiBold 12sp #8F9285, uppercase letter-spacing 0.5.

**Component 5 — Text Field Full Name** (full width minus 32dp insets, top margin 8dp, 56dp tall, 12dp radius): Outlined Text Field, 1dp outline #44483D, label "Full Name" Outfit Regular 12sp #8F9285, value "Maria Santos" Outfit Regular 16sp #E3E3D8.

**Component 6 — Text Field Email** (full width minus 32dp insets, top margin 8dp): Same shape. Label "Email Address", value "maria.santos@email.com". Trailing lock icon 16dp #8F9285 (read-only).

**Component 7 — Text Field Phone** (full width minus 32dp insets, top margin 8dp): Label "Phone Number", value "+44 7700 900123".

**Component 8 — Button Save** (full width minus 32dp insets, top margin 24dp, 48dp tall, pill): Filled #B2D188, label "Save Changes" Outfit SemiBold 16sp #1F3701.

**Component 9 — Button Change Password** (full width minus 32dp insets, top margin 8dp, 48dp tall, pill): Outlined 1dp #44483D, label "Change Password" Outfit Medium 16sp #E3E3D8.

**Component 10 — Button Log Out** (full width minus 32dp insets, top margin 24dp, 48dp tall): Outlined 1dp #FFB4AB, label "Log Out" Outfit Medium 16sp #FFB4AB.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The #B2D188 Save Changes button and avatar edit badge create a unified green thread, anchoring the user's identity management experience in a calm, balanced, and refined aesthetic.

↑↑↑ MOCKUP PROMPT
