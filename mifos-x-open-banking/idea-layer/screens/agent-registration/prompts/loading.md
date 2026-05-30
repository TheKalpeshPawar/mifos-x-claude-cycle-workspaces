---
ui_yaml_sha: a468125e1106b883f7fa067dc586fd6b137420230253c4e395c0ea724594b5e7
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 01bf09d2ddc01b3c491adda295650d0fef74c6d7017fb19d8b750df8bf3f7fae

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: agent-registration
state: loading
state_visibility: loading

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# agent-registration — loading state

> Auto-generated from screens/agent-registration/ui.yaml @ SHA f52f9cfe602060bd
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the agent registration screen for **Mifos Open Banking**, a Kotlin Multiplatform open-banking super-app for consumer retail banking and field officer agent banking.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB, pending #E8A317, on_surface_variant #C5C8BA.

**Component 1 — App Bar Shimmer** (64dp tall, full width): Shimmer rectangle 160dp wide x 22dp tall, left-aligned 16dp inset. Shimmer base #1E201A, highlight #282A24, sweep 1200ms. Background #12140E. skeleton_screen archetype.

**Component 2 — Title Block Shimmer** (full width minus 32dp insets, top margin 24dp): Two stacked shimmer bars: 220dp wide x 20dp tall (title), then 300dp wide x 14dp tall (subtitle), 8dp gap. Same shimmer cadence.

**Component 3 — Progress Indicator** (centered, top margin 32dp): Circular indeterminate spinner 40dp diameter, stroke color #B2D188, stroke 3dp. Below it, shimmer text bar 180dp wide x 14dp tall, top margin 12dp, #1E201A base.

**Component 4 — Form Card Shimmer** (full width minus 32dp insets, top margin 24dp, 12dp corner radius, background #1E201A): 4 stacked field shimmers: each 56dp tall, full width, 8dp corner radius, 12dp gap. Shimmer sweep identical cadence. (Repeat pattern for remaining 4 fields.)

**Component 5 — Button Shimmer** (full width minus 32dp insets, top margin 24dp): Pill shimmer 48dp tall, corner radius 999, background #282A24.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Vertically scrollable layout on #12140E. The sage green #B2D188 spinner stroke conveys calm forward progress, keeping this loading state composed and financially trustworthy rather than anxious.

↑↑↑ MOCKUP PROMPT
