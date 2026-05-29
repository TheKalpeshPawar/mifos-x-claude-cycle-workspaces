---
ui_yaml_sha: de0c641bb5454eb6bb91af4ba18a416b141b46ce0b2cad2598e56a2732ce7577
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 44e6af76b68914c893997b8482c2c2f8bc146f7f4cb152ace7d94e15b0efee28

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: profile
state: empty
state_visibility: empty

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# profile — empty state

> Auto-generated from screens/profile/ui.yaml @ SHA c36aa948bd4811db
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the profile screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "My Profile" Outfit Medium 18sp #E3E3D8 centered. Background #12140E, 1dp bottom divider #44483D. empty_state archetype.

**Component 2 — Avatar Placeholder** (centered, top margin 64dp): 96dp circle #282A24, person outline icon 48dp #44483D centered inside.

**Component 3 — Empty Title** (centered, top margin 24dp, horizontal padding 32dp): "Profile not loaded" Outfit SemiBold 22sp #E3E3D8.

**Component 4 — Empty Subtext** (centered, top margin 8dp, horizontal padding 48dp): "Sign in to view and manage your profile details and account settings." Outfit Regular 14sp #8F9285, line-height 20sp.

**Component 5 — Button** (full width minus 64dp insets, top margin 32dp): Filled pill Button 48dp tall, background #B2D188, label "Sign In" Outfit SemiBold 16sp #1F3701.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The #B2D188 Sign In button in this empty_state provides a calm, minimal re-entry path into the user's banking identity, keeping the experience balanced and restrained.

↑↑↑ MOCKUP PROMPT
