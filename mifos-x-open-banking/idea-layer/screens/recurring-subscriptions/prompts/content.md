---
ui_yaml_sha: 23ce864f95d53e84e96f1b0c3f59d4d67febe5921e8eb4e697b2ff798f694ce8
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 35b953b8071c71abb20f732a96518f0527c81c3d9dcff4b8c988f4b4f27b0b33

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: recurring-subscriptions
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# recurring-subscriptions — content state

> Auto-generated from screens/recurring-subscriptions/ui.yaml @ SHA efa78f2c0f2f3e11
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the recurring-subscriptions screen for **HSBC Open Banking**, a UK Open Banking AISP that automatically detects recurring payments from HSBC transaction history.

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F, outline #8B9198

**Component 1 - Top App Bar** (full width 393dp, height 64dp): Outfit medium 22sp title "Recurring Payments" in #E0E3E8 left-aligned on #101417. No elevation.

**Component 2 - Banner** (full width minus 32dp insets, 12dp radius, background #004B6F, 12dp vertical padding, 16dp horizontal padding): Icon info_outline 20dp in #95CDF7 left-aligned. Beside icon: Outfit regular 13sp "Detected automatically from your HSBC transaction history. Last updated today." in #C9E6FF. Archetype: screen.

**Component 3 - Stat Block** (full width minus 32dp insets, 12dp radius, background #1C2024, 16dp padding): Outfit regular 12sp label "Monthly total" in #C1C7CE tracked. Monospace bold 28sp "£78.94" in #FFB4AB (debit). Supporting Outfit regular 12sp "6 subscriptions detected" in #8B9198. 20dp vertical internal padding.

**Component 4 - List** (full width minus 32dp insets, scrollable, 1dp dividers #41474D, 0dp gap): Six subscription rows each 72dp tall. Each row layout: left 40x40dp circle avatar background #004B6F with first-letter initial in #95CDF7 Outfit medium 18sp. Centre column: Outfit medium 16sp merchant name #E0E3E8, below it Outfit regular 13sp "Monthly" in #C1C7CE. Trailing column: monospace Outfit 16sp amount in #FFB4AB right-aligned, below Outfit 12sp next charge date in #8B9198. Small Chip "Detected" 24dp height, outlined border #95CDF7, label #95CDF7 Outfit 12sp, pill radius. Rows in order: Netflix £10.99 "N" next 8 Jul, Spotify £11.99 "S" next 12 Jul, Amazon Prime £8.99 "A" next 3 Jul, Apple iCloud+ £2.99 "A" next 16 Jul, YouTube Premium £13.99 "Y" next 5 Jul, PureGym £29.99 "P" next 1 Jul.

**Component 5 - Bottom Navigation Bar** (full width, height 80dp, background #1C2024): Active "Subscriptions": icon autorenew filled, icon and label #95CDF7 Outfit 12sp. Inactive "Overview", "Spending", "Budgets": icon and label #8B9198.

Do not use an em-dash anywhere in this design. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark surface between the info banner, stat block, and subscription list with any lighter panel or gradient. Do not place dark text on the info banner background or light text on dark avatar circles without adequate contrast.

Recurring merchants surface in a clean monochrome list anchored by trust-blue #95CDF7 detection chips and avatars, the total monthly debit in #FFB4AB giving cost awareness at a glance. calm.

↑↑↑ MOCKUP PROMPT
