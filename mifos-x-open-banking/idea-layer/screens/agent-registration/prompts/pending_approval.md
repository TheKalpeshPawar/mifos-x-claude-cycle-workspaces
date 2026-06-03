---
ui_yaml_sha: sha256:agent-registration-ui-2026-06-02
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
content_hash: agent-registration-pending-2026-06-02

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form

feature: agent-registration
state: pending_approval
state_visibility: pending_approval
viewmodel: AgentRegistrationViewModel

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: /idea export
prompt_template_version: stitch-per-state-v3.0.0
generated_at: "2026-06-02"
---

# agent-registration — pending_approval state

> Auto-generated from screens/agent-registration/ui.yaml @ SHA c759c832fbdabee6
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the pending_approval state of the agent registration screen for **Mifos Open Banking**, a Kotlin Multiplatform open-banking super-app for consumer retail banking and field officer agent banking.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB, pending #E8A317, on_surface_variant #C5C8BA.

**Component 1 — App Bar** (64dp tall, full width): Title "Agent Registration" Outfit Medium 18sp #E3E3D8 centered. Background #12140E, zero elevation.

**Component 2 — Header Block** (full width minus 32dp insets, top margin 24dp): Title "Agent Registration" Outfit SemiBold 22sp #E3E3D8. Subtitle "Register to become an authorised OBP field agent with your bank" Outfit Regular 14sp #C5C8BA, top margin 8dp.

**Component 3 — Pending Status Banner** (full width minus 32dp insets, top margin 24dp, background #1E201A, 12dp corner radius, 16dp padding): Card with Row layout. Leading hourglass icon 24dp #E8A317. Right column: title "Pending Approval" Outfit SemiBold 16sp #E3E3D8, body "Your agent application is under review. You will be notified once your bank confirms your status." Outfit Regular 14sp #C5C8BA, top margin 4dp. form archetype.

**Component 4 — Form Summary Card** (full width minus 32dp insets, top margin 16dp, background #1E201A, 12dp corner radius, 16dp padding): Read-only field rows for "Legal Name", "Mobile Phone Number", "Agent Number", "Operating Currency" each 48dp tall, divider #44483D between rows. Label 12sp #8F9285, value 14sp #E3E3D8. (Repeat pattern for remaining fields.)

**Component 5 — Button** (full width minus 32dp insets, top margin 24dp): Filled pill Button 48dp tall, corner radius 999, background #354E16, label "Go to Dashboard" Outfit SemiBold 16sp #CDEDA3 centered.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Layout on #12140E. The amber #E8A317 pending icon anchors the status banner with calm authority, signaling review in progress without alarming the field officer awaiting bank confirmation.

↑↑↑ MOCKUP PROMPT
