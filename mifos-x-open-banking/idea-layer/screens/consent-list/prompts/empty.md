---
ui_yaml_sha: 873a3d34112d09657c43fb2cbb8ef9113e41cd60883696b1b6463664ce7e9627
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: f4f5b05b5e92b290a02dd1e439edbbf00ecc57b0e8b58565608518b92cac84f0

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: consent-list
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-list — empty state

> Auto-generated from screens/consent-list/ui.yaml @ SHA 2b488008bd7b8528
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the consent-list screen for **HSBC Open Banking**, a UK AISP app with no connected consents yet, built on Trust Blue minimalist Material 3 DARK on 393x852dp Pixel 5.

Palette: surface #101417, onSurface #E0E3E8, primary #95CDF7, onPrimary #00344E, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F

**Component 1 - Top App Bar** (full-width, 64dp): Outfit Medium 22sp "Consents" #E0E3E8 on #101417; back-arrow icon leading; no trailing actions.

**Component 2 - Empty State** (centred, full-width minus 32dp, 320dp vertical breathing room, archetype empty_state): shield_outlined icon 72dp #C1C7CE centred; Outfit Medium 22sp headline "No consents yet" #E0E3E8 centred; 8dp gap; Outfit Regular 14sp "Connect your HSBC account to start reading balances, transactions, and more." #C1C7CE centred; 16dp gap below body.

**Component 3 - Button** (full-width minus 32dp, 48dp): filled "Connect HSBC account" Outfit Medium 14sp #00344E on #95CDF7 container radius 24dp; centred horizontally 24dp below body text.

**Component 4 - Bottom Navigation Bar** (full-width, 80dp, #1C2024): tabs "Home" home icon, "Accounts" account_balance icon, "Consents" policy icon active tint #95CDF7, "Settings" settings icon; active label #95CDF7, inactive #C1C7CE.

Do not use em-dash anywhere in labels or body copy. Do not make any headline longer than 3 lines or any subtitle longer than 25 words. Do not break the dark #101417 surface theme between sections by introducing light containers or white backgrounds. Do not place light-coloured text on a light-coloured button, or dark text on a dark button.

The shield icon in muted #C1C7CE signals security context without alarm; Trust Blue (#95CDF7) fills only the single call-to-action button, making the first HSBC connection the obvious and minimal next step for the PSU.

↑↑↑ MOCKUP PROMPT
