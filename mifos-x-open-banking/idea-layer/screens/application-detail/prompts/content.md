---
ui_yaml_sha: 64d1e77304b15bebcf5570a91036dd5267b8a38e827f5a966cb61dd278263d6b
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 168003045bb0afca0d65cef148e0e06ca44000a85cff0c461bc694f8b1731230

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: application-detail
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# application-detail — content state

> Auto-generated from screens/application-detail/ui.yaml @ SHA e9bc0313cc9777de
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the content state of the application-detail screen for **Mifos X Open Banking**, a professional open banking KMP super-app serving consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, tertiary #A0CFCB, on_tertiary #003735, error #FFB4AB, on_error #690005, error_container #93000A, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16, scrim #000000.

**Component 1 — App Bar** (64dp, full width, background #12140E, 1dp bottom divider #44483D): Back-arrow 24dp #B2D188 leading. Title "Application #OBP-2026-00234" Outfit Medium 16sp #E3E3D8 centered. Below: chip "Pending Review" 24dp, 12dp radius, #1E201A fill, Outfit Medium 12sp #E8A317. "Submitted: 20 May 2026" Outfit Regular 12sp #8F9285.

**Component 2 — Card** (full width, 32dp insets, 12dp radius, 16dp margin top, #1E201A, 16dp padding): Header "Customer" Outfit Medium 12sp #B2D188. Row 56dp: "John Kamau Mwangi" Outfit SemiBold 16sp #E3E3D8 left; "View Profile" Outfit Medium 14sp #A0CFCB right.

**Component 3 — Card** (full width, 32dp insets, 12dp radius, 12dp margin top, #1E201A, 16dp padding): Header "Application Details" Outfit Medium 12sp #B2D188. Three rows 56dp each, 1dp dividers #44483D. Row 1: "Account Type" #C5C8BA / "KCB Savings Account" #E3E3D8. Row 2: "Requested Limit" #C5C8BA / "KES 500,000" #B2D188. Row 3: "Purpose" #C5C8BA / "Personal savings and salary credit" #E3E3D8.

**Component 4 — List Row** (full width, 32dp insets, 12dp margin top, 48dp, #1E201A, 12dp radius, 16dp padding): Verified-user icon 20dp #B2D188 left. "KYC Status: Verified" Outfit Medium 14sp #E3E3D8. Checkmark 16dp #B2D188 right.

**Component 5 — Card** (full width, 32dp insets, 12dp radius, 16dp margin top, #1E201A, 16dp padding): Header "Supporting Documents" Outfit Medium 12sp #B2D188. Two rows 64dp, 1dp divider. Doc 1: icon 40dp #1F4E4B fill 8dp radius, "National ID" Outfit Medium 14sp #E3E3D8 + "Verified" 12sp #B2D188; "View" link #A0CFCB right. Doc 2: icon 40dp #44483D fill, "Proof of Address" + "Pending Upload" 12sp #8F9285; "Upload" button 32dp 8dp radius #354E16 right.

**Component 6 — Text Field** (full width, 32dp insets, 16dp margin top, 96dp, 12dp radius, outlined 1dp #44483D): Label "Review Notes" Outfit Regular 12sp #8F9285. Focused outline on edit.

**Component 7 — Button** (full width, 32dp insets, 48dp, 24dp radius, 16dp margin top): Filled #B2D188, label "Approve Application" Outfit SemiBold 14sp #1F3701.

**Component 8 — Button** (full width, 32dp insets, 48dp, 24dp radius, 8dp margin top): Outlined 1dp #FFB4AB, label "Reject Application" Outfit Medium 14sp #FFB4AB.

**Component 9 — Button** (full width, 32dp insets, 48dp, 24dp radius, 8dp margin top, 32dp bottom): Outlined 1dp #44483D, label "Request Information" Outfit Medium 14sp #C5C8BA.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Anchored by the earth-green #B2D188 approve button and teal secondary tones, the layout stays calm and balanced, with error rose #FFB4AB reject button providing unambiguous semantic separation for a regulated financial workflow.
↑↑↑ MOCKUP PROMPT
