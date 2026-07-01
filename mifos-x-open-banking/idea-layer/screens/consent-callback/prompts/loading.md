---
ui_yaml_sha: 89368ce68522a27b426af78efafaade84222dfd7246d861a644ffa9b3030c8b6
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 34d6728f8d9c061e620f3e2dc17bfd43a92e6d026b0940abebb18e7d60567693

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: consent-callback
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-callback — loading state

> Auto-generated from screens/consent-callback/ui.yaml @ SHA d3e9fb83836cf197
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the consent-callback screen for **HSBC Open Banking**, a UK AISP app processing the OAuth 2.0 redirect after the PSU approved account access on the HSBC authorisation portal, built on Trust Blue minimalist Material 3 DARK on 393x852dp Pixel 5.

Palette: surface #101417, onSurface #E0E3E8, primary #95CDF7, onPrimary #00344E, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F

**Component 1 - Top App Bar** (full-width, 64dp): Outfit Medium 20sp "Connecting HSBC" #E0E3E8 on #101417; no back-arrow (deep-link entry, back navigation disabled); no trailing actions; archetype skeleton_screen.

**Component 2 - Stat Block** (centred, full-width minus 32dp, 200dp vertical): circular progress_indicator 56dp diameter #95CDF7 track centred; 24dp gap below; shimmer block 200dp wide 22dp tall radius 6dp sweep #1C2024 to #262A2E centred (title placeholder); 8dp gap; shimmer block 260dp wide 14dp tall radius 6dp sweep same (body placeholder); animating simultaneously with circular indicator.

**Component 3 - Banner** (full-width minus 32dp, 52dp, #1C2024 radius 8dp): shimmer block full-width 16dp tall radius 6dp sweep #1C2024 to #262A2E; mirrors the progress status banner position from the content state.

Do not use em-dash anywhere in labels or body copy. Do not make any headline longer than 3 lines or any subtitle longer than 25 words. Do not break the dark #101417 surface theme between sections by introducing light containers or white backgrounds. Do not place light-coloured text on a light-coloured button, or dark text on a dark button.

No bottom navigation bar appears on this transient deep-link landing screen; Trust Blue (#95CDF7) on the circular progress indicator is the sole active element, keeping the calm #101417 field minimal while the HSBC authorisation code is exchanged for an access token.

↑↑↑ MOCKUP PROMPT
