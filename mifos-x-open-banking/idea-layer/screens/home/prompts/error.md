---
ui_yaml_sha: 66c8a95765ac08cf659947bd96cf36fcad9dd366c305ca94719196dcf4ee4475
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 1bdca6aa4f1b913c30c47a7d67b00dea6001f4ba0ac27293c6915409b34a1f24

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: home
state: error
state_visibility: error

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# home — error state

> Auto-generated from screens/home/ui.yaml @ SHA 725781c9fc541f1c
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the Home screen for **HSBC Open Banking**, a UK account-information app that surfaces a recoverable network failure with a single retry action and no content rails.

Palette: primary #95CDF7, onPrimary #00344E, error #FFB4AB, onError #690005, errorContainer #93000A, onErrorContainer #FFDAD6, surface #101417, onSurface #E0E3E8

**Component 1 - Top App Bar** (393dp wide, 64dp tall): Outfit 22sp "My Accounts" in onSurface #E0E3E8, surface #101417 background, no elevation.

**Component 2 - Error State** (361dp wide, centred vertically with 120dp top padding): The error_state archetype for a failed HSBC accounts fetch. Centred layout: cloud_off icon in error #FFB4AB at 64dp. Outfit 22sp "Could not load accounts" in onSurface #E0E3E8, centred, max 2 lines, 16dp below icon. Outfit 16sp "Check your connection and try again. Your account data is safe." in onSurfaceVariant #C1C7CE, centred, 24dp horizontal inset, 24dp below headline.

**Component 3 - Button** (280dp wide, 48dp tall, primary #95CDF7 fill, onPrimary #00344E label, 999dp radius): "Try again" Outfit 16sp bold, centred. 32dp below the error state body. Tapping retries the HSBC accounts fetch.

**Component 4 - Bottom Navigation Bar** (393dp wide, 80dp tall, surfaceContainer #1C2024): Four tabs. Home is active: icon and label in primary #95CDF7. Accounts, Insights, Profile inactive in onSurfaceVariant #C1C7CE.

DO NOT use em-dash anywhere in text. DO NOT make any headline longer than 3 lines or any subtitle longer than 25 words. DO NOT break the dark theme between sections. DO NOT place light-on-light or dark-on-dark text and button combinations.

The error_state archetype keeps surface #101417 uncluttered, using error #FFB4AB only for the icon while reserving #95CDF7 for the retry button, a calm signal hierarchy that informs without alarming in this regulated-fintech context.

↑↑↑ MOCKUP PROMPT
