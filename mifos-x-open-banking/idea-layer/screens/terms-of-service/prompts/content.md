---
ui_yaml_sha: 516c2b85d35f0d9def8fe28aea29060f67cb264db1e67fc0370922dde9b3af78
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 19c8fdad9f90a00260b60b5889f91a46bcad204312ba667ce3dadf89c09fd70c

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: settings

feature: terms-of-service
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# terms-of-service — content state

> Auto-generated from screens/terms-of-service/ui.yaml @ SHA df10651bc8b83369
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the content state of the terms-of-service screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Terms of Service" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow icon 24dp #B2D188. Zero elevation, background #12140E.

**Component 2 — Card** (full width minus 32dp insets, top margin 16dp, 12dp corner radius, background #1E201A): Header "Agreement Overview" Outfit SemiBold 15sp #E3E3D8 top padding 16dp. Body "These Terms of Service govern your use of Mifos X Open Banking, provided by the Mifos Initiative." Outfit Regular 14sp #C5C8BA top margin 8dp. settings archetype.

**Component 3 — Card** (full width minus 32dp insets, top margin 8dp, same spec): Header "Account Usage" Outfit SemiBold 15sp #E3E3D8. Body "You are responsible for maintaining the confidentiality of your DirectLogin credentials. Report unauthorized access immediately." Outfit Regular 14sp #C5C8BA.

**Component 4 — Card** (full width minus 32dp insets, top margin 8dp): Header "Acceptance of Terms" Outfit SemiBold 15sp #E3E3D8. Body "By creating an account or continuing to use Mifos X Open Banking after changes take effect, you accept these terms." Outfit Regular 14sp #C5C8BA.

**Component 5 — Card** (full width minus 32dp insets, top margin 8dp): Header "Data Handling via Open Bank Project API" Outfit SemiBold 15sp #E3E3D8. Body "This application connects to banking services via the Open Bank Project (OBP) REST API. Data is processed per applicable PSD2 and regional open banking regulations." Outfit Regular 14sp #C5C8BA.

**Component 6 — Card** (full width minus 32dp insets, top margin 8dp): Header "Prohibited Uses" Outfit SemiBold 15sp #E3E3D8. Body "You must not use this application to initiate fraudulent or unauthorised transactions, reverse-engineer the OBP integration, or share access credentials." Outfit Regular 14sp #C5C8BA.

**Component 7 — Card** (full width minus 32dp insets, top margin 8dp): Header "Limitation of Liability" Outfit SemiBold 15sp #E3E3D8. Body "To the maximum extent permitted by law, the Mifos Initiative shall not be liable for indirect or consequential damages arising from service interruptions." Outfit Regular 14sp #C5C8BA.

**Component 8 — Card** (full width minus 32dp insets, top margin 8dp): Header "Dispute Resolution" Outfit SemiBold 15sp #E3E3D8. Body "Contact us at legal@mifos.org before initiating any formal dispute proceedings. We aim to resolve all issues within 30 business days." Outfit Regular 14sp #C5C8BA.

**Component 9 — Card** (full width minus 32dp insets, top margin 8dp, bottom margin 16dp): Header "Governing Law" Outfit SemiBold 15sp #E3E3D8. Body "These Terms of Service are governed by and construed in accordance with the laws of the applicable jurisdiction." Outfit Regular 14sp #C5C8BA.

**Component 10 — Text** (centered, top margin 16dp, bottom padding 32dp): "Last updated: 28 May 2026. Version 1.0" Outfit Regular 12sp #8F9285 centered.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. The earth-green accent #B2D188 on the back-arrow provides a calm navigation anchor; card borders in #44483D keep each legal section restrained and refined for this regulated open banking context.
↑↑↑ MOCKUP PROMPT
