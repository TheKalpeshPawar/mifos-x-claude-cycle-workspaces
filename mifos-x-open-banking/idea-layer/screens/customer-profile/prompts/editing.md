---
ui_yaml_sha: ed2405e9b0ab40e84eddfcb7e669dd5d6df03b6a59f4997cb41c63dd2313c905
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 5c2263c39e2dbdacede5a726421bac37c04b979b417a3251b9774e8a81be3f7d

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: customer-profile
state: editing
state_visibility: editing

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# customer-profile — editing state

> Auto-generated from screens/customer-profile/ui.yaml @ SHA 4b5b04fd93890081
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the editing state of the customer-profile screen for **Mifos X Open Banking**, a professional open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, error #FFB4AB, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title "Edit Profile" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow icon 24dp #B2D188. Trailing "Save" text button Outfit SemiBold 14sp #B2D188. Background #12140E, zero elevation.

**Component 2 — Text Field** (full width minus 32dp insets, top margin 24dp): Section label "Personal Information" Outfit SemiBold 14sp #B2D188. Outlined text field 56dp tall, 12dp corner radius, outline 1dp #44483D focused to #B2D188. Field 1: label "Full Name" Outfit Regular 12sp #8F9285, value "John Kamau Mwangi" Outfit Regular 16sp #E3E3D8, cursor #B2D188. Field 2: label "Phone" #8F9285, value "+254 722 123 456" #E3E3D8. Field 3: label "Email" #8F9285, value "john.mwangi@gmail.com" #E3E3D8. 12dp gap between fields.

**Component 3 — Text Field** (full width minus 32dp insets, top margin 16dp): Section label "Address" Outfit SemiBold 14sp #B2D188. Field 1: label "Street" #8F9285, value "123 Moi Avenue, Nairobi" #E3E3D8. Field 2: label "County" #8F9285, value "Nairobi County, Kenya" #E3E3D8. Field 3: label "Postcode" #8F9285, value "00100" #E3E3D8. Focused field outline #B2D188, unfocused #44483D.

**Component 4 — Text Field** (full width minus 32dp insets, top margin 16dp): Section label "Employment" Outfit SemiBold 14sp #B2D188. Field 1: label "Employer" #8F9285, value "Safaricom PLC" #E3E3D8. Field 2: label "Monthly Income" #8F9285, value "KES 85,000" #E3E3D8. Field 3: label "Employment Type" #8F9285, value "Permanent" #E3E3D8.

**Component 5 — Button** (full width minus 32dp insets, top margin 32dp, bottom 32dp): Filled button 48dp tall, 12dp corner radius, background #B2D188, label "Save Changes" Outfit SemiBold 15sp #1F3701 centered. Below it, text button "Discard Changes" Outfit Medium 14sp #8F9285 centered, top margin 12dp.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable input view on #12140E. Anchored by #B2D188 on focused field outlines and the Save action, the layout stays calm and refined, keeping the editing experience precise and financially grounded.
↑↑↑ MOCKUP PROMPT
