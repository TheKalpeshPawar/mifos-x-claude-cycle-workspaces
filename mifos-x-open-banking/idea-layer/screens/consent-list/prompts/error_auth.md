---
ui_yaml_sha: 873a3d34112d09657c43fb2cbb8ef9113e41cd60883696b1b6463664ce7e9627
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: e477de8231dfe1f7b0f85f3bd033504488bd2f200a3c29f0726533c1bb169a8b

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: consent-list
state: error_auth
state_visibility: error_auth

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-list — error_auth state

> Auto-generated from screens/consent-list/ui.yaml @ SHA e48e2ff518a6e0e5
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error_auth state of the consent-list screen for **HSBC Open Banking**, a UK AISP app whose Open Banking session has expired, requiring the PSU to re-authenticate before viewing consents, built on Trust Blue minimalist Material 3 DARK on 393x852dp Pixel 5.

Palette: surface #101417, onSurface #E0E3E8, primary #95CDF7, onPrimary #00344E, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F

**Component 1 - Top App Bar** (full-width, 64dp): Outfit Medium 22sp "Consents" #E0E3E8 on #101417; back-arrow leading; no trailing actions; archetype detail_screen.

**Component 2 - Error State** (centred, full-width minus 32dp, 320dp vertical): lock_reset icon 72dp #FFB4AB centred; Outfit Medium 22sp headline "Session expired" #E0E3E8 centred; 8dp gap; Outfit Regular 14sp "Your Open Banking session has timed out. Sign in again to view and manage your HSBC consents." #C1C7CE centred; 16dp gap below body.

**Component 3 - Button** (full-width minus 32dp, 48dp): filled "Re-authenticate" Outfit Medium 14sp #00344E on #95CDF7 container radius 24dp; centred 24dp below body.

**Component 4 - Bottom Navigation Bar** (full-width, 80dp, #1C2024): tabs "Home" home icon, "Accounts" account_balance icon, "Consents" policy icon active tint #95CDF7, "Settings" settings icon; active #95CDF7, inactive #C1C7CE.

Do not use em-dash anywhere in labels or body copy. Do not make any headline longer than 3 lines or any subtitle longer than 25 words. Do not break the dark #101417 surface theme between sections by introducing light containers or white backgrounds. Do not place light-coloured text on a light-coloured button, or dark text on a dark button.

The lock_reset icon in #FFB4AB distinguishes this auth-specific error from a generic network failure; a calm #101417 backdrop and a single Trust Blue (#95CDF7) button keep the UX minimal, giving the PSU immediate recovery without alarm.

↑↑↑ MOCKUP PROMPT
