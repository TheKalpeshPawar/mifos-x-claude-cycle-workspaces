---
ui_yaml_sha: d9ae9d4b46f8c880e1bdab3fb08cc6bf8df99140964c3c5557cba8f389363eda
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: fb94fbedc4463f38b31e4bec7ad3a4e933c91c634acbdc5a96c5d25ecd69fa65

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: beneficiaries
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# beneficiaries — empty state

> Auto-generated from screens/beneficiaries/ui.yaml @ SHA 84762f88527a3beb
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the Beneficiaries screen for **HSBC Open Banking**, a UK Open Banking AISP app where OBReadBeneficiary5 returns no saved payee records for the selected account.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, surfaceContainer #1C2024, outline #8B9198, primaryContainer #004B6F, secondary #B7C9D9, surfaceVariant #41474D

**Component 1 - Top App Bar** (56dp, 393dp wide): back-arrow icon in #95CDF7, title "Beneficiaries" Outfit Medium 22sp #E0E3E8, container #101417, empty_state archetype.

**Component 2 - Banner** (56dp, 361dp wide): search input visible but inactive, hint text "Search payees" Outfit Regular 16sp #8B9198, pill container #1C2024 radius 28dp, 1dp border #41474D to signal disabled state.

**Component 3 - Empty State** (centered vertically in remaining 640dp, 361dp wide): illustration icon "people_outline" 64dp #C1C7CE centered, headline "No saved payees" Outfit Medium 20sp #E0E3E8 centered, body text "Payees added to your HSBC account will appear here once available" Outfit Regular 14sp #C1C7CE centered, 24dp gap between illustration, headline and body, generous vertical breathing room above and below.

**Component 4 - Bottom Navigation Bar** (80dp, 393dp wide): container #1C2024, Beneficiaries tab active icon and label in #95CDF7, inactive tab icons in #8B9198.

Do not use em-dash in the headline or body copy. Do not render skeleton rows or phantom list items in the empty state. Do not add an "Add payee" or "Set up" action button; this AISP screen has no payment-initiation capability. Do not break the dark surface with a bright or white illustration panel.

The empty screen reads as calm: the "people_outline" illustration in #C1C7CE and the Trust Blue #95CDF7 back arrow communicate clearly that no payees are registered, without alarm.

↑↑↑ MOCKUP PROMPT
