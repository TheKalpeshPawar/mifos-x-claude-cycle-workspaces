---
ui_yaml_sha: 873a3d34112d09657c43fb2cbb8ef9113e41cd60883696b1b6463664ce7e9627
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 0168db0a443c31833e3b91ce65026f990a93cf43ce9dfb0cd744f192c8aa2988

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: consent-list
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-list — content state

> Auto-generated from screens/consent-list/ui.yaml @ SHA 0b1bec49311d7fec
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the consent-list screen for **HSBC Open Banking**, a UK AISP app managing active and historical account-access consents under Trust Blue minimalist Material 3 DARK on 393x852dp Pixel 5.

Palette: surface #101417, onSurface #E0E3E8, primary #95CDF7, onPrimary #00344E, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F

**Component 1 - Top App Bar** (full-width, 64dp): Outfit Medium 22sp title "Consents" in #E0E3E8 on #101417 surface; back-arrow icon at leading edge; no trailing actions.

**Component 2 - Banner** (full-width minus 32dp insets, 72dp, #1C2024): warning_amber icon 24dp left; Outfit Regular 14sp "1 consent expires in 14 days. Reconfirm to keep your data access active." #E0E3E8; persistent, no dismiss button.

**Component 3 - List** (full-width minus 32dp, archetype detail_screen): "Active" section label Outfit Medium 12sp #C1C7CE uppercase; Card A (full-width, 112dp, #1C2024 radius 12dp) - HSBC logo 40dp circle leading, Chip "Authorised" filled #004B6F label #95CDF7, body "10 permissions: accounts, balances, transactions, beneficiaries, standing orders, direct debits, scheduled payments, statements, products, party name" Outfit Regular 13sp #C1C7CE, footer "Expires 26 Sep 2026" right-aligned 12sp #C1C7CE; Card B (full-width, 120dp, #1C2024 radius 12dp) - HSBC logo 40dp, Chip "Authorised" filled #004B6F label #95CDF7, Chip Row "Reconfirm by 15 Jul 2026" warning_amber icon on #4C4162 surface, body "4 permissions: accounts, balances, transactions, products" Outfit 13sp #C1C7CE, footer "Expires 15 Jul 2026" 12sp bold #FFB4AB signalling near-expiry.

**Component 4 - List** (full-width minus 32dp): "History" section label Outfit Medium 12sp #C1C7CE; Card (full-width, 80dp, #1C2024 radius 12dp) - HSBC logo 32dp greyscale, Chip "Expired" outlined #8B9198 label #8B9198, footer "Expired 20 Jun 2026, Connected 20 Mar 2026" Outfit 12sp #8B9198.

**Component 5 - Bottom Navigation Bar** (full-width, 80dp, #1C2024): 4 tabs - "Home" home icon, "Accounts" account_balance icon, "Consents" policy icon active tint #95CDF7, "Settings" settings icon; active label #95CDF7, inactive #C1C7CE.

Do not use em-dash anywhere in labels or body copy. Do not make any headline longer than 3 lines or any subtitle longer than 25 words. Do not break the dark #101417 surface theme between sections by introducing light containers or white backgrounds. Do not place light-coloured text on a light-coloured button, or dark text on a dark button.

Trust Blue (#95CDF7) surfaces only on the active Authorised chip labels and the bottom nav indicator, leaving the #101417 canvas uncluttered; the amber Chip Row and #FFB4AB footer on Card B are the only warm signals in this restrained AISP layout.

↑↑↑ MOCKUP PROMPT
