---
ui_yaml_sha: 77ef7dbe843044a66b73b3c529d340294fe8b8804fa009b3a4c22aa5f5ddacab
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 4384143762671e7b118d749bc872ea86452982c2c1fb8133b639b0d084b90784

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: consent-manager
state: populated
state_visibility: populated

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-manager — populated state

> Auto-generated from screens/consent-manager/ui.yaml @ SHA 461e90ba4dc00485
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the populated state of the consent manager screen for **Mifos X Open Banking**, a professional open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, secondary #A0CFCB, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Connected Apps" Outfit Medium 18sp #E3E3D8, leading back-arrow 24dp #B2D188, background #12140E.

**Component 2 — Card** (MoneyManager Pro consent card, full width minus 32dp insets, 12dp corner radius, background #1E201A, top margin 24dp): App name "MoneyManager Pro" Outfit SemiBold 15sp #E3E3D8, dates "Granted 1 Mar 2026 - Expires 1 Mar 2027" Outfit Regular 12sp #C5C8BA, "ACTIVE" badge filled #354E16 Outfit Medium 11sp #B2D188. Chip Row: "Read Accounts", "View Transactions", "Check Balances" chips outlined 1dp #44483D Outfit Regular 12sp #C5C8BA. Button "Revoke Access" outlined 1dp #FFB4AB label Outfit Medium 14sp #FFB4AB.

**Component 3 — Card** (TaxHelper consent card, same style, top margin 12dp): "TaxHelper" Outfit SemiBold 15sp, "Granted 15 Jan 2026 - Expires 15 Jan 2027", "ACTIVE" badge. Chip Row: "View Transactions", "Read Accounts". Button "Revoke Access".

**Component 4 — Card** (BudgetWise consent card, top margin 12dp): "BudgetWise" Outfit SemiBold 15sp, "Granted 10 Oct 2025 - Expired 10 Apr 2026", "EXPIRED" badge outlined 1dp #8F9285 label #8F9285. Chip Row: "Check Balances". Button "Remove" outlined 1dp #8F9285.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. The sage-green #B2D188 on active consent badges signals healthy, authorized connections, projecting calm financial oversight suited to the taste-default aesthetic.

↑↑↑ MOCKUP PROMPT
