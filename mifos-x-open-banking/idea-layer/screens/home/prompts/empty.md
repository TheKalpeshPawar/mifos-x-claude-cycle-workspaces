---
ui_yaml_sha: 66c8a95765ac08cf659947bd96cf36fcad9dd366c305ca94719196dcf4ee4475
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 64cf81ce95145876341a4ae551a04f5079f7cf989994a13e73c8df981972ff07

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: home
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# home — empty state

> Auto-generated from screens/home/ui.yaml @ SHA 0794fdc2974723ad
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the Home screen for **HSBC Open Banking**, a UK account-information app that prompts the user to connect their HSBC account when no active consent exists.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, outline #8B9198

**Component 1 - Top App Bar** (393dp wide, 64dp tall): Outfit 22sp "My Accounts" in onSurface #E0E3E8, surface #101417 background, no elevation.

**Component 2 - Empty State** (361dp wide, centred vertically with 120dp top padding): This is the empty_state archetype for a user who has not yet granted Open Banking consent. Centred layout: shield_outlined icon in onSurfaceVariant #C1C7CE at 64dp. Outfit 22sp "No accounts connected" in onSurface #E0E3E8, centred, max 2 lines, 16dp below icon. Outfit 16sp "Connect your HSBC account to view balances, transactions, and spending insights in one place." in onSurfaceVariant #C1C7CE, centred, 24dp horizontal inset, 24dp below headline.

**Component 3 - Button** (280dp wide, 48dp tall, primary #95CDF7 fill, onPrimary #00344E label, 999dp radius): "Connect HSBC account" Outfit 16sp bold, centred. 32dp below the empty state body. Tapping launches the onboarding consent flow.

**Component 4 - Bottom Navigation Bar** (393dp wide, 80dp tall, surfaceContainer #1C2024): Four tabs. Home is active: icon and label in primary #95CDF7. Accounts, Insights, Profile are inactive in onSurfaceVariant #C1C7CE.

DO NOT use em-dash anywhere in text. DO NOT make any headline longer than 3 lines or any subtitle longer than 25 words. DO NOT break the dark theme between sections. DO NOT place light-on-light or dark-on-dark text and button combinations.

The empty_state centres a single action on surface #101417, letting #95CDF7 carry full weight on the connect button while every other surface stays quiet in surfaceContainer and onSurfaceVariant tones, a restrained regulated-fintech prompt.

↑↑↑ MOCKUP PROMPT
