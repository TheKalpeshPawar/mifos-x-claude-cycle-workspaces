---
ui_yaml_sha: 4af6ba2fca8822ef1afa49c6800612d2eccac67ae5dd199e1c88a785018712c8
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 4a54745da3e4f02e35d46fff2654283a5f447733df75536bb24eecaff72d037d

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: fo-dashboard
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# fo-dashboard — content state

> Auto-generated from screens/fo-dashboard/ui.yaml @ SHA 6c4746ffe43f9f0d
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the fo-dashboard screen for **Mifos X Open Banking**, a Open Banking KMP super-app for consumer retail banking and field officer agent banking in emerging markets.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (full width, 64dp tall): Title "Good morning, Priya" Outfit Medium 18sp #E3E3D8 left-aligned with 16dp padding. Trailing profile icon 24dp #A0CFCB and gear icon 24dp #8F9285. Background #12140E. Subtitle "Monday, 25 May 2026 · Mifos Nairobi Branch" Outfit Regular 12sp #C5C8BA below title.

**Component 2 — Grid** (full width minus 32dp insets, top margin 20dp, 2-column grid with 12dp gap): 4 stat cards each 80dp tall, 12dp corner radius, background #1E201A. Card 1: value "124" Outfit SemiBold 22sp #B2D188, label "Active Customers" Outfit Regular 12sp #C5C8BA. Card 2: value "5" Outfit SemiBold 22sp #E8A317, label "Pending Applications" Outfit Regular 12sp #C5C8BA. Card 3: value "3" Outfit SemiBold 22sp #E8A317, label "KYC Pending" Outfit Regular 12sp #C5C8BA. Card 4: value "2" Outfit SemiBold 22sp #B2D188, label "Meetings Today" Outfit Regular 12sp #C5C8BA.

**Component 3 — List Row** (full width minus 32dp insets, top margin 24dp): Section header "Action Needed" Outfit SemiBold 14sp #E3E3D8. Three Card items below with background #1E201A, 12dp corner radius, 12dp gap. Card A: text "John Mwangi - KYC expires in 3 days" Outfit Regular 14sp #C5C8BA, Button "Review KYC" 36dp tall filled #354E16 label Outfit Medium 13sp #CDEDA3. Card B: text "Sarah Odhiambo - Application pending 7 days" Outfit Regular 14sp #C5C8BA, Button "View Application" same style. Card C: text "New lead: Peter Kamau - Retail account request" Outfit Regular 14sp #C5C8BA, Button "Start Onboarding" same style.

**Component 4 — Card** (full width minus 32dp insets, top margin 12dp, 12dp corner radius, background #1E201A): Row for "Acme Trading Ltd - New business account inquiry" with Button "Start Corporate Onboarding" Outfit Medium 13sp #1F3701 filled #B2D188 36dp tall. Below it another Card row: "Complete Agent Registration" with Button "Register" same style.

**Component 5 — List Row** (full width minus 32dp insets, top margin 24dp, bottom 32dp): Section header "Today's Schedule" Outfit SemiBold 14sp #E3E3D8. Two rows each 56dp tall, 1dp divider #44483D. Row 1: time "10:00 AM" Outfit Medium 14sp #B2D188 left, details "Mary Wanjiku · Loan Review" Outfit Regular 14sp #E3E3D8 right. Row 2: time "2:30 PM" Outfit Medium 14sp #B2D188, details "James Otieno · New Account Discussion" Outfit Regular 14sp #E3E3D8.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full scrollable layout on #12140E. The soft earth-green accent #B2D188 on stat values, action buttons, and schedule times signals growth and financial stability in a calm, balanced banking presentation.

↑↑↑ MOCKUP PROMPT
