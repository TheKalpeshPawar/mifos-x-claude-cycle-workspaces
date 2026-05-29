---
ui_yaml_sha: 3fd23727025f84161f07e7aec5d0eac94651cf54a8c6617a21f7b92e54ebab5a
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 33292e8411e30fade04a63596cea52c31e84c133903038226f9252d8356835ac

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: notifications
state: empty
state_visibility: empty

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# notifications — empty state

> Auto-generated from screens/notifications/ui.yaml @ SHA 4174e21eaecb2eb8
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the notifications screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Notifications" Outfit Medium 18sp #E3E3D8 left-aligned with 16dp horizontal padding. Background #12140E, zero elevation, 1dp bottom divider #44483D. empty_state archetype.

**Component 2 — Hero Illustration Zone** (centered, top margin 80dp, 160dp tall): Muted illustration of an empty bell outline rendered in #44483D on #12140E. No red alarm tones. Conveys calm absence of activity.

**Component 3 — Empty Title** (centered, top margin 24dp, horizontal padding 32dp): "No notifications yet" Outfit SemiBold 22sp #E3E3D8, centered, max 2 lines.

**Component 4 — Empty Subtext** (centered, top margin 8dp, horizontal padding 48dp): "Activity updates for payments, KYC approvals, and direct debits will appear here." Outfit Regular 14sp #8F9285, line-height 20sp, centered.

**Component 5 — Button** (full width minus 64dp insets, top margin 32dp): Filled pill Button 48dp tall, corner radius 999dp, background #B2D188, label "Explore Accounts" Outfit SemiBold 16sp #1F3701.

**Component 6 — Bottom Nav** (64dp tall, full width, anchored bottom): 4 tabs Home, Payments, Notifications (selected with #B2D188 icon + label), Profile. Background #1E201A, top 1dp divider #44483D. Inactive icons #8F9285 20dp.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The soft sage-green #B2D188 on the primary Button creates a calm, balanced call-to-action that feels restrained and purposeful, calibrated to the professional banking aesthetic.

↑↑↑ MOCKUP PROMPT
