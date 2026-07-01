---
ui_yaml_sha: 89368ce68522a27b426af78efafaade84222dfd7246d861a644ffa9b3030c8b6
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 4d529553ad925b229e36a15e0cbb02fc7322d34e58271345ab9c759ec35706ae

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: consent-callback
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-callback — content state

> Auto-generated from screens/consent-callback/ui.yaml @ SHA 71115d89dea351dd
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the consent-callback screen for **HSBC Open Banking**, a UK AISP app confirming that the PSU successfully authorised account access on the HSBC portal and the OAuth token exchange completed, built on Trust Blue minimalist Material 3 DARK on 393x852dp Pixel 5.

Palette: surface #101417, onSurface #E0E3E8, primary #95CDF7, onPrimary #00344E, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F

**Component 1 - Top App Bar** (full-width, 64dp): Outfit Medium 20sp "HSBC Connected" #E0E3E8 on #101417; no back-arrow (transient deep-link, not navigable back); no trailing actions; archetype screen.

**Component 2 - Stat Block** (centred, full-width minus 32dp, 220dp vertical): check_circle icon 72dp #95CDF7 centred; 16dp gap; Outfit Medium 24sp "Access granted" #E0E3E8 centred; 8dp gap; Outfit Regular 15sp "Your HSBC current and savings accounts are now connected. Balances and transactions will refresh automatically." #C1C7CE centred.

**Component 3 - Banner** (full-width minus 32dp, 56dp, #004B6F radius 8dp): shield icon 20dp #95CDF7 left; Outfit Regular 13sp "Connection secured under UK Open Banking. You can revoke access any time from Consents." #C9E6FF persistent.

**Component 4 - Button** (full-width minus 32dp, 48dp): filled "Go to Consents" Outfit Medium 14sp #00344E on #95CDF7 container radius 24dp; 24dp gap below banner.

**Component 5 - Button** (full-width minus 32dp, 48dp): outlined "Back to Home" Outfit Medium 14sp #95CDF7 border #95CDF7 radius 24dp; 8dp gap below first button.

Do not use em-dash anywhere in labels or body copy. Do not make any headline longer than 3 lines or any subtitle longer than 25 words. Do not break the dark #101417 surface theme between sections by introducing light containers or white backgrounds. Do not place light-coloured text on a light-coloured button, or dark text on a dark button.

No bottom navigation bar on this transient OAuth landing; the check_circle icon and headline in Trust Blue (#95CDF7) deliver clear success feedback against the calm #101417 field, then two buttons route the PSU onward with minimal and restrained choreography.

↑↑↑ MOCKUP PROMPT
