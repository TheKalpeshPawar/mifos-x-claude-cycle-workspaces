---
ui_yaml_sha: 64d1e77304b15bebcf5570a91036dd5267b8a38e827f5a966cb61dd278263d6b
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: db27e00242689ca89b064917d92095eb819722a861003bcb0ad7f408bbf2103c

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: application-detail
state: rejected
state_visibility: rejected

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# application-detail — rejected state

> Auto-generated from screens/application-detail/ui.yaml @ SHA 90a5acb3509fce7d
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the rejected state of the application-detail screen for **Mifos X Open Banking**, a professional open banking KMP super-app serving consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, tertiary #A0CFCB, on_tertiary #003735, error #FFB4AB, on_error #690005, error_container #93000A, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16, scrim #000000.

**Component 1 — App Bar** (64dp tall, full width): Leading back-arrow 24dp #B2D188. Title "Application #OBP-2026-00234" Outfit Medium 16sp #E3E3D8 centered. Status chip "Rejected" 24dp tall, 12dp corner radius, background #93000A, label Outfit Medium 12sp #FFB4AB. "Submitted: 20 May 2026" Outfit Regular 12sp #8F9285. Background #12140E, 1dp bottom divider #44483D.

**Component 2 — Card** (full width minus 32dp insets, 12dp corner radius, top margin 16dp, background #1E201A, 16dp padding): Header "Customer" Outfit Medium 12sp #B2D188. Row 56dp: "John Kamau Mwangi" Outfit SemiBold 16sp #E3E3D8 on left, link "View Profile" Outfit Medium 14sp #A0CFCB on right.

**Component 3 — Card** (full width minus 32dp insets, 12dp corner radius, top margin 12dp, background #1E201A, 16dp padding): Header "Application Details" Outfit Medium 12sp #B2D188. Three List Row items 56dp each. "Account Type" / "KCB Savings Account". "Requested Limit" / "KES 500,000" #C5C8BA. "Purpose" / "Personal savings and salary credit".

**Component 4 — Card** (full width minus 32dp insets, 12dp corner radius, top margin 16dp, background #1E201A, 16dp padding): Header "Rejection Reason" Outfit Medium 12sp #FFB4AB. Row 72dp: "Insufficient documentation. Please upload Proof of Address and resubmit." Outfit Regular 14sp #C5C8BA line-height 20sp.

**Component 5 — Button** (full width minus 32dp insets, 48dp tall, 24dp corner radius, top margin 16dp): Filled button background #354E16, label "Submit New Application" Outfit SemiBold 14sp #CDEDA3.

**Component 6 — Button** (full width minus 32dp insets, 48dp tall, 24dp corner radius, top margin 8dp, bottom 32dp): Text button "Contact support" Outfit Medium 14sp #8F9285.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The error container #93000A status chip provides a clear but restrained rejection signal on the deep #12140E surface, while the earth-green #354E16 resubmit button keeps the layout constructive and forward-looking.
↑↑↑ MOCKUP PROMPT
