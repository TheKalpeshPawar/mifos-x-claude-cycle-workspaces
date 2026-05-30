---
ui_yaml_sha: b89d839e6c9e3be9d2a9ef40cf53bd6b62a21124885037343b404ee39dd8d76d
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 5fb79b99aeb3ce0764bce161561fba90cf8634b3fc56a7c8969b258e46bb1d9e

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: home
state: loading
state_visibility: loading

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# home — loading state

> Auto-generated from screens/home/ui.yaml @ SHA 041f8010d0411280
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the home screen for **mifos-x-open-banking**, a Kotlin Multiplatform open-banking super-app for consumer retail banking and field officer agent banking.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (full width, 56dp tall): Outfit medium 20sp, on_surface #E3E3D8; shimmer rectangle matching greeting text and date lines, background #12140E.

**Component 2 — Balance Card** (full width minus 32dp insets, 140dp tall): skeleton_screen shimmer block, surface_container #1E201A fill, radius 16dp; three stacked shimmer bars representing label, balance amount, and masked IBAN; Chip Row of 3 shimmer pill buttons (Send Money, Beneficiaries, View Cards) at bottom, height 36dp each.

**Component 3 — Chip Row** (full width minus 32dp insets, 40dp): single shimmer bar spanning width, background surface_variant #44483D, radius 999dp; represents total-balance aggregate row.

**Component 4 — Card** (full width minus 32dp insets, 56dp each, repeat for 3 transaction rows): each Card is a shimmer skeleton_screen row with icon circle 40dp, two shimmer text bars (merchant name 140dp wide, date/category 100dp wide), and amount + badge shimmer on trailing edge; surface_container_high #282A24 fill.

**Component 5 — Grid** (full width minus 32dp insets, 3 columns, 80dp tall): three shimmer tiles for Standing Orders, ATM and Branches, FX Rates; icon circle 32dp, label bar 48dp wide below each; surface_container #1E201A fill, radius 12dp.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The earth-green accent #4C662B saturates this skeleton_screen with calm assurance, each shimmer pulse a quiet promise that financial data loads with care and precision.

↑↑↑ MOCKUP PROMPT
