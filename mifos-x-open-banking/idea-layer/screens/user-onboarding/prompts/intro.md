---
ui_yaml_sha: 927a4ea2aa924d185dec8870cbdfc9f4ac91b01311daef7f791259aeb739a5f9
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 477a3a6ca90d40c54bbdc5a57444f1a163df3c321a7004fd9807e17e60327c67

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: user-onboarding
state: intro
state_visibility: intro

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# user-onboarding — intro state

> Auto-generated from screens/user-onboarding/ui.yaml @ SHA 1e3faa656a931f2e
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the intro state of the User Onboarding screen for **HSBC Open Banking**, a UK account-information app that welcomes first-time users and establishes consent intent before the three-step onboarding flow.

Palette: primary #95CDF7, onPrimary #00344E, primaryContainer #004B6F, onPrimaryContainer #C9E6FF, secondary #B7C9D9, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE

**Component 1 - Stat Block** (393dp wide, 24dp tall): Step progress indicator. Three dots centred horizontally. Dot 1 is active: 8dp filled circle in primary #95CDF7. Dots 2 and 3 are inactive: 6dp hollow circles in outline #8B9198. 16dp top margin from safe area.

**Component 2 - Card** (361dp wide, 176dp tall, surfaceContainer #1C2024, 12dp radius): Hero panel. Abstract shield graphic with a keyhole detail in primary #95CDF7 over onPrimary #00344E background, centred, 72dp tall. This is the detail_screen welcome panel for a first-time Open Banking user.

**Component 3 - Section Header** (361dp, auto): Outfit 26sp bold "See all your HSBC accounts in one place" in onSurface #E0E3E8, left-aligned, max 2 lines. 24dp below the hero card.

**Component 4 - Banner** (361dp wide, auto, surfaceContainer #1C2024, 8dp radius, 16dp padding): Outfit 16sp "This app reads your HSBC balance, transactions, and statements using the UK Open Banking Standard. We never move money or share your data." in onSurfaceVariant #C1C7CE. Two lines max.

**Component 5 - Chip Row** (361dp wide, 40dp): Two trust chips side by side with 8dp gap. Chip 1: verified_user icon, "FAPI 2.0 Secured", primaryContainer #004B6F fill, onPrimaryContainer #C9E6FF label Outfit 13sp. Chip 2: account_balance icon, "FCA Regulated", same fill and label colours.

**Component 6 - Button** (361dp wide, 48dp tall, primary #95CDF7 fill, onPrimary #00344E label, 999dp radius): "Get started" Outfit 16sp bold. Full-width, 24dp below the chip row.

DO NOT use em-dash anywhere in text. DO NOT make any headline longer than 3 lines or any subtitle longer than 25 words. DO NOT break the dark theme between sections. DO NOT place light-on-light or dark-on-dark text and button combinations.

The intro state opens on surface #101417 with a single #95CDF7 filled call-to-action, pairing the shield illustration and two trust chips to create a calm, regulatory-confident entry point before the user steps into Open Banking consent.

↑↑↑ MOCKUP PROMPT
