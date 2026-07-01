---
ui_yaml_sha: 89368ce68522a27b426af78efafaade84222dfd7246d861a644ffa9b3030c8b6
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 048c7320ee2d4cbb11b18ce9aad56bd6bee28c1cfeb9e0f7c7bd045aeedbd65b

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: consent-callback
state: access_denied
state_visibility: access_denied

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-callback — access_denied state

> Auto-generated from screens/consent-callback/ui.yaml @ SHA 802fd078a1d9d175
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the access_denied state of the consent-callback screen for **HSBC Open Banking**, a UK AISP app displaying the outcome after the PSU actively declined to authorise account access on the HSBC portal, built on Trust Blue minimalist Material 3 DARK on 393x852dp Pixel 5.

Palette: surface #101417, onSurface #E0E3E8, primary #95CDF7, onPrimary #00344E, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F

**Component 1 - Top App Bar** (full-width, 64dp): Outfit Medium 20sp "Access not granted" #E0E3E8 on #101417; no back-arrow; no trailing actions; archetype screen.

**Component 2 - Stat Block** (centred, full-width minus 32dp, 220dp vertical): block icon 72dp #C1C7CE centred; 16dp gap; Outfit Medium 22sp "You declined access" #E0E3E8 centred; 8dp gap; Outfit Regular 14sp "You chose not to share your HSBC account data. You can connect at any time from the Consents screen." #C1C7CE centred; 16dp gap below.

**Component 3 - Button** (full-width minus 32dp, 48dp): filled "Try connecting again" Outfit Medium 14sp #00344E on #95CDF7 container radius 24dp; centred 24dp below body.

**Component 4 - Button** (full-width minus 32dp, 48dp): outlined "Back to Home" Outfit Medium 14sp #95CDF7 border #95CDF7 radius 24dp; 8dp gap below first button.

Do not use em-dash anywhere in labels or body copy. Do not make any headline longer than 3 lines or any subtitle longer than 25 words. Do not break the dark #101417 surface theme between sections by introducing light containers or white backgrounds. Do not place light-coloured text on a light-coloured button, or dark text on a dark button.

No bottom navigation bar on this transient OAuth screen; the block icon in neutral #C1C7CE avoids alarm since this is a deliberate PSU choice; Trust Blue (#95CDF7) on both buttons signals that the consent journey can restart without penalty, keeping the UX restrained and non-judgmental.

↑↑↑ MOCKUP PROMPT
