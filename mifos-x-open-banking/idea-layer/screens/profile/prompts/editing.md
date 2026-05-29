---
ui_yaml_sha: de0c641bb5454eb6bb91af4ba18a416b141b46ce0b2cad2598e56a2732ce7577
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: d4b3834f8ecb174621c50c2447fb76befda75a3d1e019fb399498f575a607045

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: profile

feature: profile
state: editing
state_visibility: editing

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# profile — editing state

> Auto-generated from screens/profile/ui.yaml @ SHA 2ebd3615fa7d6db8
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the editing state of the profile screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Edit Profile" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow 24dp #B2D188. Trailing "Save" text Button Outfit Medium 14sp #B2D188. Background #12140E, 1dp bottom divider #44483D.

**Component 2 — Avatar Picker** (centered, top padding 24dp): 96dp diameter circular avatar with photo. Bottom-right edit badge 32dp circle #B2D188, pencil icon 18dp #1F3701.

**Component 3 — Text Field Full Name** (full width minus 32dp insets, top margin 24dp, 56dp tall, 12dp radius): Outlined Text Field, focused outline 1dp #B2D188, label "Full Name" Outfit Regular 12sp #B2D188, value "Maria Santos" Outfit Regular 16sp #E3E3D8.

**Component 4 — Text Field Email** (full width minus 32dp insets, top margin 12dp): Outlined, label "Email Address", value "maria.santos@email.com". Trailing lock icon 16dp #8F9285 (read-only, outlined #44483D not focused).

**Component 5 — Text Field Phone** (full width minus 32dp insets, top margin 12dp): Outlined #44483D, label "Phone Number", value "+44 7700 900123".

**Component 6 — Text Field Bio** (full width minus 32dp insets, top margin 12dp, 96dp tall, multiline): Outlined #44483D, label "Short Bio", value "Banking officer at Mifos Initiative. Open finance advocate.", character counter "62 / 160" Outfit Regular 11sp #8F9285 bottom-right.

**Component 7 — Divider** (full width, top margin 24dp): 1dp horizontal rule #44483D.

**Component 8 — Button Delete** (full width minus 32dp insets, top margin 24dp, bottom 32dp, 48dp tall, pill): Outlined 1dp #FFB4AB, label "Delete account" Outfit Medium 14sp #FFB4AB centered.

## State-specific behavior
- Custom state "Editing" — all text fields are editable, focused field shows #B2D188 outline.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The #B2D188 focused field outline and "Save" trailing button create a cohesive edit mode signal, guiding the user through input field completion with a calm, refined green accent.

↑↑↑ MOCKUP PROMPT
