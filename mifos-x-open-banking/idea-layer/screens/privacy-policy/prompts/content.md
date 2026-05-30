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

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# privacy-policy — content state

> Auto-generated from screens/privacy-policy/ui.yaml @ SHA 5e848da04d355a86
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the Privacy Policy screen for **mifos-x-open-banking**, a professional open banking KMP super-app serving retail banking consumers and field officers.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, error #FFB4AB, outline #8F9285.

**Component 1 — Banner** (full width, 32dp inset): Outfit 14sp, on_surface_variant #C5C8BA on surface_container #1E201A, 8dp radius. Text: "This policy complies with UK GDPR, the Data Protection Act 2018, and EU GDPR."

**Component 2 — Card** (full width minus 32dp inset, 12dp radius, surface_container #1E201A): settings section "Data We Collect." Header — Outfit 16sp bold, on_surface #E3E3D8. Body — Outfit 14sp, on_surface_variant #C5C8BA: "We collect identity data (name, date of birth, national ID), contact data (email, phone), financial data (account numbers, balances, transaction history), and device/usage data. (Remaining categories follow same pattern.)"

**Component 3 — Card** (full width minus 32dp inset, 12dp radius): "Lawful Basis for Processing." Header as above. Body: "Processing grounds include contractual necessity (account services), legal obligation (AML compliance), and legitimate interests (fraud prevention). (Additional bases follow same pattern.)"

**Component 4 — Card** (full width minus 32dp inset, 12dp radius): "How We Use Your Data." Body: "Data is used to display account balances, process payments, perform KYC identity verification, and detect fraud. No data is used for advertising."

**Component 5 — Card** (full width minus 32dp inset, 12dp radius): "Third-Party Data Sharing." Body: "Data is shared with GDPR-compliant processors: Open Bank Project Limited (API services), regulated payment networks, and mandatory regulatory bodies only."

**Component 6 — Card** (full width minus 32dp inset, 12dp radius): "Data Retention." Body: "Transaction records: 7 years (UK Money Laundering Regulations). Account data: duration of relationship plus 6 years post-closure."

**Component 7 — Card** (full width minus 32dp inset, 12dp radius): "Your Rights Under GDPR." Body: "Rights include access, rectification, erasure, restriction, portability, and objection. Contact privacy@mifos.org to exercise any right."

**Component 8 — Card** (full width minus 32dp inset, 12dp radius): "Data Controller and DPO Contact." Body: "Controller: Mifos Initiative, 1 World Trade Center, New York, NY 10007. Processor: Open Bank Project Limited, 11 Leadenhall Street, London. DPO: privacy@mifos.org."

**Component 9 — Text** (full width, 32dp inset, Outfit 12sp, on_surface_variant #C5C8BA): "Last updated: 28 May 2026 -- Version 1.0."

Do not use em-dash anywhere in text. Do not make any headline longer than 3 lines or any subtitle longer than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The earth-green accent #4C662B anchors every interactive element, projecting financial stability and trust. Flat-card depth on a near-black #12140E canvas keeps the settings archetype minimal and regulation-ready.

↑↑↑ MOCKUP PROMPT
