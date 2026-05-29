---
ui_yaml_sha: 446998a2d04bdffe5c3942db1e66ab81cccc8fbd49ed6f0a6c91223077a1b2ce
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 86ca3583de5deb958474de13e6178ebd61e24f2d738875d6e6ff3d07e2b7efd6

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: customer-detail
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# customer-detail — content state

> Auto-generated from screens/customer-detail/ui.yaml @ SHA 1d83aeb650b81c24
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the customer detail screen for **Mifos X Open Banking**, a professional open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, secondary #A0CFCB, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Customer Detail" Outfit Medium 18sp #E3E3D8, leading back-arrow 24dp #B2D188, trailing "Send Message" text button Outfit Medium 14sp #B2D188. Background #12140E.

**Component 2 — Hero** (full width, background #1E201A, 24dp padding): Avatar circle 64dp initials "JM" Outfit Bold 22sp #1F3701 background #B2D188, centered. "John Mwangi" Outfit SemiBold 20sp #E3E3D8 top margin 12dp centered. "Customer since Jan 2024" Outfit Regular 13sp #C5C8BA. "KYC Verified" chip 28dp tall filled #354E16 Outfit Medium 11sp #B2D188 top margin 8dp.

**Component 3 — Chip Row** (stats, full width minus 32dp insets, top margin 16dp): "2 Accounts", "KES 145,200", "3 days ago" each chip 32dp tall background #1E201A outline 1dp #44483D Outfit Regular 12sp #C5C8BA, 8dp gap.

**Component 4 — Card** (personal info, full width minus 32dp insets, 12dp corner radius background #1E201A, top margin 16dp): Header "Personal Information" Outfit SemiBold 14sp #C5C8BA. Rows: "John Kamau Mwangi", "DOB: 14 Mar 1985", "National ID: KE12345678", "Phone: +254 722 123 456", "Email: john.mwangi@gmail.com" each Outfit Regular 14sp #E3E3D8 56dp tall, dividers 1dp #44483D between rows. "View Full Profile" text link Outfit Medium 13sp #B2D188 bottom 12dp.

**Component 5 — Card** (address, same style, top margin 8dp): Header "Address". Row "123 Moi Avenue, Nairobi, Kenya" Outfit Regular 14sp #E3E3D8.

**Component 6 — Card** (relationship manager, same style, top margin 8dp): "Assigned to: Priya Sharma" Outfit Regular 14sp #E3E3D8, "Reassign" text link Outfit Medium 13sp #B2D188 right.

**Component 7 — FAB** (bottom right, 56dp diameter, background #B2D188, + icon 24dp #1F3701, label "Create Application" Outfit Medium 13sp #1F3701).

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. Anchored by the accent #B2D188 on the KYC badge and FAB, the composition stays calm and refined, projecting credibility for the field officer workflow.

↑↑↑ MOCKUP PROMPT
