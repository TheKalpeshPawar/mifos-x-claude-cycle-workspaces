---
ui_yaml_sha: b89d839e6c9e3be9d2a9ef40cf53bd6b62a21124885037343b404ee39dd8d76d
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 82418c61623a94e83e07736e5b8b71c568501b572e100b802a8d4624be8bc455

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: dashboard

feature: home
state: content
state_visibility: content

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# home — content state

> Auto-generated from screens/home/ui.yaml @ SHA 39c82f1bfadd4407
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the home screen for **mifos-x-open-banking**, a Kotlin Multiplatform open-banking super-app for consumer retail banking and field officer agent banking.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (full width, 56dp tall): Outfit medium 22sp "Good morning, Alex" in on_surface #E3E3D8; subtitle Outfit regular 14sp "Monday, 25 May 2026" in on_surface_variant #C5C8BA; background surface #12140E.

**Component 2 — Balance Card** (full width minus 32dp insets, radius 16dp): dashboard card on surface_container #1E201A; Outfit medium 14sp "Primary Checking" in on_surface_variant; Outfit bold 28sp "£4,250.00" in primary #B2D188; Outfit regular 14sp ".... .... .... 0130" in on_surface_variant. Chip Row of 3 filled buttons (Send Money, Beneficiaries, View Cards), background primary_container #354E16, label on_primary_container #CDEDA3, height 36dp, spacing 8dp.

**Component 3 — Chip Row** (full width minus 32dp insets, 40dp, radius 999dp): wallet icon + Outfit regular 14sp "Total across 3 accounts: £12,480.50" in on_surface #E3E3D8; background surface_variant #44483D.

**Component 4 — Card** (full width minus 32dp insets, 64dp each): 3 transaction Cards on surface_container_high #282A24. Row: icon circle 40dp outline #8F9285; leading stack with merchant name Outfit medium 16sp on_surface + category/date Outfit regular 12sp on_surface_variant; trailing amount Outfit medium 16sp (debit on_surface, credit primary #B2D188) + badge chip. Txn1: Tesco Supermarket, 23 May 2026, Groceries, -£42.50 DEBIT. Txn2: Salary Payment, 22 May 2026, Income, +£3,200.00 CREDIT. Txn3: EDF Energy, 20 May 2026, Utilities, -£94.20 DEBIT.

**Component 5 — Grid** (full width minus 32dp insets, 3 columns, 88dp tall): icon tile cards on surface_container #1E201A, radius 12dp. Standing Orders (repeat icon), ATM and Branches (location_on), FX Rates (currency_exchange). Icon 24dp on_primary_container #CDEDA3, label Outfit regular 12sp on_surface below.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The earth-green accent #4C662B grounds this dashboard in financial stability, its warm and balanced presence across cards and action chips conveying reliable growth for every retail banking consumer.

↑↑↑ MOCKUP PROMPT
