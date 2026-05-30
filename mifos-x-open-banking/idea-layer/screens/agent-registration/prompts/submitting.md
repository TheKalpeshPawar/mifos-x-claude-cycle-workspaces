---
ui_yaml_sha: a468125e1106b883f7fa067dc586fd6b137420230253c4e395c0ea724594b5e7
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 136b7c897023b4b94edc7079004e21b9d8abb013fb6fc0254c166c3771302774

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form

feature: agent-registration
state: submitting
state_visibility: submitting

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# agent-registration — submitting state

> Auto-generated from screens/agent-registration/ui.yaml @ SHA b83b4bffa0528796
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the submitting state of the agent registration screen for **Mifos Open Banking**, a Kotlin Multiplatform open-banking super-app for consumer retail banking and field officer agent banking.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB, pending #E8A317, on_surface_variant #C5C8BA.

**Component 1 — App Bar** (64dp tall, full width): Title "Agent Registration" Outfit Medium 18sp #E3E3D8 centered. Background #12140E, zero elevation.

**Component 2 — Header Block** (full width minus 32dp insets, top margin 24dp): Title "Agent Registration" Outfit SemiBold 22sp #E3E3D8. Subtitle "Register to become an authorised OBP field agent with your bank" Outfit Regular 14sp #C5C8BA, top margin 8dp. form archetype.

**Component 3 — Text Field Group** (full width minus 32dp insets, top margin 24dp): Outlined Text Fields 56dp tall, 12dp corner radius, outline #8F9285, background #1E201A, opacity 0.5 (disabled). Fields: "Legal Name", "Mobile Phone Number" with prefix "+254", "Agent Number", "Operating Currency". Label 12sp #8F9285, value 16sp #E3E3D8 dimmed. (Repeat pattern for remaining field.) Gap 12dp.

**Component 4 — Progress Indicator** (centered, top margin 24dp): Circular indeterminate spinner 32dp diameter, stroke #B2D188. Below it, label "Submitting your application..." Outfit Regular 14sp #C5C8BA, top margin 8dp, centered.

**Component 5 — Button** (full width minus 32dp insets, top margin 24dp): Filled pill Button 48dp tall, corner radius 999, background #354E16 (disabled tint), label "Register as Agent" Outfit SemiBold 16sp #CDEDA3, centered. Non-interactive.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E, form fields dimmed to signal non-interactivity. The #B2D188 spinner communicates active network progress without alarm, keeping the financial submission moment calm and trustworthy.

↑↑↑ MOCKUP PROMPT
