---
ui_yaml_sha: b89d839e6c9e3be9d2a9ef40cf53bd6b62a21124885037343b404ee39dd8d76d
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 3c532ddc96d9a043cd1228cb0c87b5dd693d839e1385de24c41182313e0c5ec1

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: home
state: empty
state_visibility: empty

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# home — empty state

> Auto-generated from screens/home/ui.yaml @ SHA bc24b44103d76175
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the home screen for **mifos-x-open-banking**, a Kotlin Multiplatform open-banking super-app for consumer retail banking and field officer agent banking.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, background #12140E, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, outline #8F9285, pending #E8A317.

**Component 1 — App Bar** (full width, 56dp): Outfit medium 20sp "mifos-x-open-banking" in on_surface #E3E3D8; background surface #12140E.

**Component 2 — Hero** (full width, centered, 220dp vertical space): empty_state illustration centered; account_balance_wallet icon 64dp in on_primary_container #CDEDA3 on primary_container #354E16 circle 96dp; Outfit medium 20sp "No accounts linked yet" in on_surface #E3E3D8 below, 16dp gap; Outfit regular 14sp "Connect your bank to start managing payments, cards and transactions." in on_surface_variant #C5C8BA, max 2 lines, centered; 32dp below illustration.

**Component 3 — FAB** (centered, 48dp height, radius 999dp): primary filled FAB "Link a Bank Account", background primary_container #354E16, label Outfit medium 16sp on_primary_container #CDEDA3; 24dp below Hero text; min touch target 48dp.

**Component 4 — Card** (full width minus 32dp insets, 48dp, radius 12dp): secondary info Card on surface_container #1E201A; Outfit regular 14sp "You can link accounts from any Open Bank Project v7 supported institution." in on_surface_variant #C5C8BA; 24dp top margin; outline border #8F9285 1dp.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The primary green #B2D188 on deep surface #12140E transforms this empty_state into an invitation, the FAB's warm earth-green accent promising accessible growth for first-time banking consumers.

↑↑↑ MOCKUP PROMPT
