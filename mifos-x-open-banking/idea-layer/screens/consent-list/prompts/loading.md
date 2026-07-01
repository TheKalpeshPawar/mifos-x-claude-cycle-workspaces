---
ui_yaml_sha: 873a3d34112d09657c43fb2cbb8ef9113e41cd60883696b1b6463664ce7e9627
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 7b524fce9dd1fc065879fe242ba0b72e8550959de281459d052c27d28707cca3

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: consent-list
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-list — loading state

> Auto-generated from screens/consent-list/ui.yaml @ SHA d3df58b94ebb2580
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the consent-list screen for **HSBC Open Banking**, a UK AISP app fetching active and historical AISP consents from HSBC, built on Trust Blue minimalist Material 3 DARK on 393x852dp Pixel 5.

Palette: surface #101417, onSurface #E0E3E8, primary #95CDF7, onPrimary #00344E, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F

**Component 1 - Top App Bar** (full-width, 64dp): Outfit Medium 22sp "Consents" #E0E3E8 on #101417; back-arrow leading; no trailing actions; archetype skeleton_screen.

**Component 2 - Banner** (full-width minus 32dp, 60dp, #1C2024): full-width shimmer rect 20dp tall animated sweep from #1C2024 to #262A2E; no real text; mirrors the reconfirm banner position from content state.

**Component 3 - List** (full-width minus 32dp): section label shimmer 80dp wide 10dp tall; Card skeleton A (full-width, 104dp, #1C2024 radius 12dp) - circle shimmer 40dp left, line shimmer 120dp wide 16dp right of circle, two line shimmers 220dp and 140dp wide 12dp tall below; Card skeleton B (full-width, 112dp, #1C2024 radius 12dp) - same circle shimmer, two line shimmers, plus extra short shimmer 160dp for the urgency chip position; 8dp gap between cards.

**Component 4 - List** (full-width minus 32dp): section label shimmer 72dp wide 10dp tall; Card skeleton (full-width, 72dp, #1C2024 radius 12dp) - circle shimmer 32dp left, two line shimmers 100dp and 160dp wide 12dp tall; all shimmer sweep #1C2024 to #262A2E in synchrony.

**Component 5 - Bottom Navigation Bar** (full-width, 80dp, #1C2024): tabs "Home" home icon, "Accounts" account_balance icon, "Consents" policy icon active tint #95CDF7, "Settings" settings icon; no shimmer on nav bar; active label #95CDF7, inactive #C1C7CE.

Do not use em-dash anywhere in labels or body copy. Do not make any headline longer than 3 lines or any subtitle longer than 25 words. Do not break the dark #101417 surface theme between sections by introducing light containers or white backgrounds. Do not place light-coloured text on a light-coloured button, or dark text on a dark button.

Shimmer sweeps uniformly from #1C2024 to #262A2E across every skeleton card, keeping the calm #101417 field intact; Trust Blue (#95CDF7) holds only on the active nav tab, giving the PSU a restrained pulse of incoming HSBC consent data.

↑↑↑ MOCKUP PROMPT
