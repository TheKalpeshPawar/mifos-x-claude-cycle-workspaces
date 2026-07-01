---
ui_yaml_sha: 89368ce68522a27b426af78efafaade84222dfd7246d861a644ffa9b3030c8b6
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 23f4f1d1322a5f3f35aa134afb62730ad47b90d3e8be520337d79e9302b1019a

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: consent-callback
state: error
state_visibility: error

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-callback — error state

> Auto-generated from screens/consent-callback/ui.yaml @ SHA ec6ef0d53646df61
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the consent-callback screen for **HSBC Open Banking**, a UK AISP app that encountered a network or API error while processing the OAuth redirect from the HSBC authorisation portal, built on Trust Blue minimalist Material 3 DARK on 393x852dp Pixel 5.

Palette: surface #101417, onSurface #E0E3E8, primary #95CDF7, onPrimary #00344E, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F

**Component 1 - Top App Bar** (full-width, 64dp): Outfit Medium 20sp "Connecting HSBC" #E0E3E8 on #101417; no back-arrow; no trailing actions; archetype error_state.

**Component 2 - Error State** (centred, full-width minus 32dp, 320dp vertical): cloud_off icon 72dp #FFB4AB centred; Outfit Medium 22sp headline "Connection failed" #E0E3E8 centred; 8dp gap; Outfit Regular 14sp "We received your HSBC redirect but could not complete the connection. Check your network and try again." #C1C7CE centred; 16dp gap below.

**Component 3 - Button** (full-width minus 32dp, 48dp): filled "Try again" Outfit Medium 14sp #00344E on #95CDF7 container radius 24dp; centred 24dp below body.

**Component 4 - Button** (full-width minus 32dp, 48dp): text button "Back to Home" Outfit Medium 14sp #C1C7CE radius 24dp; 8dp gap below; allows PSU to exit the callback flow.

Do not use em-dash anywhere in labels or body copy. Do not make any headline longer than 3 lines or any subtitle longer than 25 words. Do not break the dark #101417 surface theme between sections by introducing light containers or white backgrounds. Do not place light-coloured text on a light-coloured button, or dark text on a dark button.

No bottom navigation bar on this transient OAuth screen; cloud_off in #FFB4AB is the only warm signal against the calm #101417 canvas, and Trust Blue (#95CDF7) on "Try again" gives the PSU a minimal and restrained single recovery path.

↑↑↑ MOCKUP PROMPT
