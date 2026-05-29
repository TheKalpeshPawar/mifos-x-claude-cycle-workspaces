---
ui_yaml_sha: 0a37b7fd9f646c61727fc05be65e3aeffc9773a1b4f8cf66f1064cde39077166
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 22fd22f27119a1bd934627028a30c82b46920d255cabe38edd022f346e77d23e

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: settings

feature: privacy-policy
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# privacy-policy — content state

> Auto-generated from screens/privacy-policy/ui.yaml @ SHA 5e848da04d355a86
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the privacy-policy screen for **Mifos X Open Banking**, a professional open banking super-app for consumer retail banking and field officer workflows.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Privacy Policy" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow 24dp #B2D188. Background #12140E, 1dp bottom divider #44483D. settings archetype.

**Component 2 — GDPR Banner** (full width minus 32dp insets, top margin 16dp, 12dp radius, 12dp padding): Surface #282A24, left border 3dp #A0CFCB. Text "This policy complies with UK GDPR, the Data Protection Act 2018, and EU GDPR (Regulation 2016/679)." Outfit Regular 12sp #C5C8BA.

**Component 3 — Card: Data We Collect** (full width minus 32dp insets, top margin 12dp, 12dp radius): Surface #1E201A, 16dp padding. Header "Data We Collect" Outfit SemiBold 14sp #E3E3D8. Body "We collect identity data (name, date of birth, national ID), contact data (email, phone, address), financial data (account balances, transaction history), and device data (IP address, device ID)." Outfit Regular 13sp #C5C8BA, line-height 20sp.

**Component 4 — Card: Lawful Basis** (full width minus 32dp insets, top margin 8dp, 12dp radius): Surface #1E201A, 16dp padding. Header "Lawful Basis for Processing" Outfit SemiBold 14sp #E3E3D8. Body "We process under: (a) Contract performance — account provision and payment services; (b) Legal obligation — UK Money Laundering Regulations 2017; (c) Legitimate interest — fraud prevention." Outfit Regular 13sp #C5C8BA.

**Component 5 — Card: How We Use Your Data** (full width minus 32dp insets, top margin 8dp, 12dp radius): Surface #1E201A, 16dp padding. Header "How We Use Your Data" Outfit SemiBold 14sp #E3E3D8. Body "Your data is used exclusively to: provide account balance and transaction display, process payments and direct debits, comply with KYC / AML obligations, and detect fraud." Outfit Regular 13sp #C5C8BA.

**Component 6 — Card: Third-Party Sharing** (full width minus 32dp insets, top margin 8dp, 12dp radius): Surface #1E201A, 16dp padding. Header "Third-Party Data Sharing" Outfit SemiBold 14sp #E3E3D8. Body "We share data with Open Bank Project Limited under GDPR-compliant Data Processing Agreements. No data is sold to advertisers or marketing platforms." Outfit Regular 13sp #C5C8BA.

**Component 7 — Card: Retention** (full width minus 32dp insets, top margin 8dp, 12dp radius): Surface #1E201A. Header "Data Retention" Outfit SemiBold 14sp #E3E3D8. Body "Transaction records: 7 years (UK Money Laundering Regulations 2017). Identity data: duration of account + 7 years. Device logs: 12 months." Outfit Regular 13sp #C5C8BA.

**Component 8 — Card: Your Rights** (full width minus 32dp insets, top margin 8dp, 12dp radius): Surface #1E201A. Header "Your Rights Under GDPR" Outfit SemiBold 14sp #E3E3D8. Body "Right to: Access, Rectification, Erasure, Restriction of Processing, Data Portability, Object. Exercise via privacy@mifos.org." Outfit Regular 13sp #C5C8BA.

**Component 9 — Card: DPO Contact** (full width minus 32dp insets, top margin 8dp, 12dp radius): Surface #1E201A. Header "Data Controller & DPO Contact" Outfit SemiBold 14sp #E3E3D8. Body "Controller: Mifos Initiative, 1 World Trade Center, New York, NY 10007. Processor: Open Bank Project Limited, 11 Leadenhall Street, London EC3V 4AB. DPO: privacy@mifos.org." Outfit Regular 13sp #C5C8BA.

**Component 10 — Last Updated** (full width minus 32dp insets, top margin 16dp, bottom margin 32dp): "Last updated: 28 May 2026 - Version 1.0" Outfit Regular 11sp #8F9285, centered.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Anchored by #A0CFCB teal on the GDPR compliance banner and #B2D188 on the back-arrow, the layout stays calm and restrained, projecting regulatory transparency and balanced user confidence in data handling.

↑↑↑ MOCKUP PROMPT
