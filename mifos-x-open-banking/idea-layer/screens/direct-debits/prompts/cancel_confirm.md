---
ui_yaml_sha: 311b028229aca9607374f911558008041fe6e2b5143fc5015fb945c2ad077cdc
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: e9ad9f68abd54e803bddbec5a9a66b38d84d92b90987d404f5c5a3dd587cbfde

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: direct-debits
state: cancel_confirm
state_visibility: cancel_confirm

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# direct-debits — cancel_confirm state

> Auto-generated from screens/direct-debits/ui.yaml @ SHA 01c0a12f8998f99d
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the cancel_confirm state of the direct-debits screen for **Mifos X Open Banking**, a mobile KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, error #FFB4AB, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title "Direct Debits" Outfit Medium 18sp #E3E3D8 left 16dp. Background #12140E at 60% opacity (scrim behind dialog). Confirmation dialog overlay.

**Component 2 — Card** (full width minus 48dp insets, centered vertically on screen): Dialog card surface_container_high #282A24, 24dp radius, shadow 8dp. Padding 24dp.

**Component 3 — App Bar** (inside dialog): "Cancel Direct Debit?" Outfit SemiBold 20sp #E3E3D8, centered.

**Component 4 — List Row** (inside dialog, top margin 12dp): "Netflix (DD-NF-20240301) will stop collecting payments. This cannot be undone." Outfit Regular 14sp #C5C8BA, line-height 20sp, max 25 words.

**Component 5 — Button** (inside dialog, top margin 24dp, full width): Filled button 48dp, 12dp radius, background #93000A, label "Yes, Cancel Mandate" Outfit SemiBold 14sp #FFDAD6 centered.

**Component 6 — Button** (inside dialog, top margin 8dp, full width): Filled button 48dp, 12dp radius, background #354E16, label "Keep Mandate" Outfit SemiBold 14sp #CDEDA3 centered.

**Component 7 — FAB** (56dp, bottom-right behind dialog, dimmed): Background #354E16 at 40% opacity.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrim overlay on #12140E with dialog centered. The destructive confirm action uses #93000A to signal irreversibility, while the Keep Mandate escape in #354E16 stays calm and balanced, offering a clear recovery path in the restrained taste-default regulated-industry aesthetic.
↑↑↑ MOCKUP PROMPT
