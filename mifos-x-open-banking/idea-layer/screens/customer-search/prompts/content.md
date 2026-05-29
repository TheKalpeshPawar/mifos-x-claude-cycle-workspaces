---
ui_yaml_sha: 211923c9f8558a327f161786a206bf7a76aa3989313d251dec81b13885e4ee21
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: ceeb090029c5c8a8f324d9c236c572f0544112f0aa214d7ff4fbc1cbdfd6222e

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: customer-search
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# customer-search — content state

> Auto-generated from screens/customer-search/ui.yaml @ SHA 962d9d15eb5c7dce
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the content state of the customer-lookup screen for **Mifos X Open Banking**, a mobile KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, error #FFB4AB, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title "Find Customer" Outfit Medium 18sp #E3E3D8 left-aligned 16dp inset. Background #12140E, zero elevation.

**Component 2 — Text Field** (full width minus 32dp insets, top margin 16dp): Filled lookup field 48dp tall, 24dp corner radius, background #1E201A. Leading magnifier icon 20dp #8F9285, placeholder "Find customers" Outfit Regular 14sp #8F9285. Focus ring #B2D188.

**Component 3 — Chip Row** (full width minus 32dp insets, top margin 12dp, horizontally scrollable): 4 filter chips 32dp tall, 16dp corner radius, 8dp gap. "All" chip filled background #354E16, label Outfit Medium 13sp #CDEDA3 (selected). "Active", "Prospect", "Dormant" chips outlined 1dp #44483D, labels Outfit Regular 13sp #C5C8BA.

**Component 4 — Button** (full width minus 32dp insets, top margin 12dp): Outlined button 40dp tall, 20dp corner radius, outline 1dp #44483D, leading QR icon 18dp #B2D188, label "Scan Customer ID" Outfit Medium 13sp #B2D188.

**Component 5 — List Row** (full width minus 32dp insets, top margin 16dp): 3 customer result cards, each surface_container #1E201A, 12dp radius, 12dp gap. Card 1: Avatar circle 40dp "JM" Outfit SemiBold 16sp #CDEDA3 on #354E16 bg, right column: "John Mwangi" Outfit SemiBold 15sp #E3E3D8, "KYC Verified" chip #CDEDA3 on #354E16, "Checking Account - KES 45,200" Outfit Regular 13sp #C5C8BA, "3 days ago" Outfit Regular 12sp #8F9285 trailing. Card 2: Avatar "SO" on #1F4E4B, "Sarah Odhiambo", "KYC Pending" chip #E8A317 background 12dp, "Application in Review" #C5C8BA, "7 days ago" #8F9285. Card 3: Avatar "PK" on #282A24, "Peter Kamau", "New Prospect" chip outlined #44483D, "No account yet" #C5C8BA.

**Component 6 — Button** (full width minus 32dp insets, top margin 16dp): Filled button 48dp tall, 12dp radius, background #B2D188, label "Onboard New Customer" Outfit SemiBold 14sp #1F3701. Below it, outlined button same dims, outline 1dp #44483D, label "Onboard Business Customer" Outfit Medium 14sp #E3E3D8. 8dp gap between.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. Anchored by the earth-green #B2D188 on the selected filter chip and primary enrollment action, the layout stays calm, balanced, and refined within the taste-default financial aesthetic.
↑↑↑ MOCKUP PROMPT
