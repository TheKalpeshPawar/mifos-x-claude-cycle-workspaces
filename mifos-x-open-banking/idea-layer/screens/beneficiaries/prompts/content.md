---
ui_yaml_sha: d9ae9d4b46f8c880e1bdab3fb08cc6bf8df99140964c3c5557cba8f389363eda
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: d00cdb1f6e53d2e00cfdf9e1fc35a9ceae03f56f9eaf20e3d977935cfc1d9e65

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: beneficiaries
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# beneficiaries — content state

> Auto-generated from screens/beneficiaries/ui.yaml @ SHA dccdec7bdb028e17
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the Beneficiaries screen for **HSBC Open Banking**, a UK Open Banking AISP app that surfaces five read-only saved creditor records retrieved via OBReadBeneficiary5 from the HSBC sandbox.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, surfaceContainer #1C2024, outline #8B9198, error #FFB4AB, secondary #B7C9D9, surfaceContainerHigh #262A2E

**Component 1 - Top App Bar** (56dp x 393dp): back-arrow icon in #95CDF7 at leading edge, title "Beneficiaries" Outfit Medium 22sp #E0E3E8, container #101417, no elevation, detail_screen archetype.

**Component 2 - Banner** (56dp, 361dp wide with 16dp insets): search input field, hint text "Search payees" Outfit Regular 16sp #C1C7CE, pill container #1C2024 radius 28dp, 1dp border #8B9198, leading search icon #C1C7CE 20dp.

**Component 3 - List** (scrollable, remaining height, 361dp wide): five rows on surface #101417, each 80dp tall, 1dp dividers #41474D. Row 1: person icon 32dp #95CDF7, headline "Jameson Lettings" Outfit Medium 16sp #E0E3E8, supporting "40-12-09 65872310 · Ref RENT-FLAT12" Outfit Regular 14sp #C1C7CE, trailing scheme label "SortCode" in #1C2024 Outfit 12sp #8B9198. Row 2: headline "John Sharma" #E0E3E8, supporting "23-05-80 11223344 · Ref FAMILY" #C1C7CE. Row 3: headline "EDF Energy" #E0E3E8, supporting "60-00-01 99887766 · Ref ELEC-8841" #C1C7CE. Row 4: headline "Hargreaves Lansdown" #E0E3E8, supporting "11-22-33 44556677 · Ref ISA-TOPUP" #C1C7CE. Row 5: headline "Priya Rajan N26 GmbH" #E0E3E8, supporting "DE89370400440532013000 · Ref TRAVEL-EUR" #C1C7CE, trailing IBAN badge background #004B6F label "IBAN" #95CDF7 12sp to distinguish international scheme.

**Component 4 - Bottom Navigation Bar** (80dp, 393dp wide): Accounts, Transactions, Beneficiaries, Settings tabs; Beneficiaries active icon and label in #95CDF7, inactive tab icons and labels in #8B9198, container #1C2024.

Do not use em-dash anywhere in text labels or supporting copy. Do not render a Pay, Send, or payment-initiation button on this read-only AISP screen. Do not break the dark #101417 surface with any light or white card panel. Do not place dark text on a dark button container or light text on a light button container.

The Beneficiaries roster reads as calm: five real payee rows in restrained Trust Blue anchored by #95CDF7 icons against the near-black surface, data-legible at a glance.

↑↑↑ MOCKUP PROMPT
