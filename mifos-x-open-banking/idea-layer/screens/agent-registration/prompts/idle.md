---
ui_yaml_sha: sha256:agent-registration-ui-2026-06-02
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
content_hash: agent-registration-idle-2026-06-02

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form

feature: agent-registration
state: idle
state_visibility: idle
viewmodel: AgentRegistrationViewModel

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: /idea export
prompt_template_version: stitch-per-state-v3.0.0
generated_at: "2026-06-02"
---

# agent-registration — idle state

> Auto-generated from screens/agent-registration/ui.yaml @ SHA 0636bb42b9aadfab
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the idle state of the agent registration screen for **Mifos Open Banking**, a Kotlin Multiplatform open-banking super-app for consumer retail banking and field officer agent banking.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB, pending #E8A317, on_surface_variant #C5C8BA.

**Component 1 — App Bar** (64dp tall, full width): Title "Agent Registration" Outfit Medium 18sp #E3E3D8 centered. Background #12140E, zero elevation.

**Component 2 — Header Block** (full width minus 32dp insets, top margin 24dp): Title "Agent Registration" Outfit SemiBold 22sp #E3E3D8, top margin 0. Subtitle "Register to become an authorised OBP field agent with your bank" Outfit Regular 14sp #C5C8BA, top margin 8dp. form archetype.

**Component 3 — Text Field Group** (full width minus 32dp insets, top margin 24dp): Outlined Text Field 56dp tall, 12dp corner radius, outline #8F9285, focused outline #B2D188, background #1E201A. Fields in order: "Legal Name" (value empty), "Mobile Phone Number" with prefix box "+254" 48dp wide, "Agent Number", "Operating Currency" (repeat pattern for remaining field). Label 12sp #8F9285, value 16sp #E3E3D8. Gap 12dp between fields.

**Component 4 — Chip Row** (full width minus 32dp insets, top margin 16dp): Label "Supported Services" Outfit Medium 14sp #C5C8BA, top margin 0. Below it, horizontally wrapping Chip Row: chips for "Cash Deposit", "Cash Withdrawal", "Account Opening", "Bill Payment", "Fund Transfer". Chip background #1E201A, outline #8F9285, label 13sp #E3E3D8, 8dp corner radius, 8dp gap.

**Component 5 — Commission Field** (full width minus 32dp insets, top margin 12dp): Outlined Text Field "Commission Rate (%)" same style as Component 3.

**Component 6 — Button** (full width minus 32dp insets, top margin 24dp, bottom margin 32dp): Filled pill Button 48dp tall, corner radius 999, background #B2D188, label "Register as Agent" Outfit SemiBold 16sp #1F3701 centered.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. The sage green #B2D188 on the register button anchors the form with a restrained, trustworthy call to action suited for regulated financial onboarding.

↑↑↑ MOCKUP PROMPT
