---
ui_yaml_sha: a468125e1106b883f7fa067dc586fd6b137420230253c4e395c0ea724594b5e7
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 0e3647e3f25ab1dec6a23082fa251256c51ead7dcd6f2fa992293bf2122a273a

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form

feature: agent-registration
state: validation_error
state_visibility: validation_error

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# agent-registration — validation_error state

> Auto-generated from screens/agent-registration/ui.yaml @ SHA 62cece5dac2243d8
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the validation_error state of the agent registration screen for **Mifos Open Banking**, a Kotlin Multiplatform open-banking super-app for consumer retail banking and field officer agent banking.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB, pending #E8A317, on_surface_variant #C5C8BA.

**Component 1 — App Bar** (64dp tall, full width): Title "Agent Registration" Outfit Medium 18sp #E3E3D8 centered. Background #12140E, zero elevation.

**Component 2 — Header Block** (full width minus 32dp insets, top margin 24dp): Title "Agent Registration" Outfit SemiBold 22sp #E3E3D8. Subtitle "Register to become an authorised OBP field agent with your bank" Outfit Regular 14sp #C5C8BA, top margin 8dp. form archetype.

**Component 3 — Text Field Group with Errors** (full width minus 32dp insets, top margin 24dp): Outlined Text Fields 56dp tall, 12dp corner radius. Error fields: outline 1dp #FFB4AB. "Legal Name" field outline #FFB4AB, error caption "Legal name is required" Outfit Regular 12sp #FFB4AB below. "Mobile Phone Number" with prefix "+254", field outline #FFB4AB, error caption "Enter a valid 9-digit phone number" 12sp #FFB4AB. "Agent Number" field outline #FFB4AB, error "Agent number is required" 12sp #FFB4AB. "Operating Currency" outline #8F9285 (valid). Gap 12dp between fields.

**Component 4 — Error Banner** (full width minus 32dp insets, top margin 16dp, background #93000A, 12dp corner radius, 16dp padding): Error icon 20dp #FFB4AB leading. Message "Registration failed. Please check your details and try again." Outfit Regular 14sp #FFDAD6. Row layout, 8dp gap.

**Component 5 — Button** (full width minus 32dp insets, top margin 24dp): Filled pill Button 48dp tall, corner radius 999, background #B2D188, label "Register as Agent" Outfit SemiBold 16sp #1F3701.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. The #FFB4AB error outlines and banner signal field-level issues without dominating the screen; the #B2D188 submit button remains visually primary, guiding resubmission with balanced confidence.

↑↑↑ MOCKUP PROMPT
