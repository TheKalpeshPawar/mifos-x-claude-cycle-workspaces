---
ui_yaml_sha: 23ce864f95d53e84e96f1b0c3f59d4d67febe5921e8eb4e697b2ff798f694ce8
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: cf5fd2da1321d37e22cb577b184841b7eb5bafb37ef4f60fbca04789b5ef6e29

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: recurring-subscriptions
state: error
state_visibility: error

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# recurring-subscriptions — error state

> Auto-generated from screens/recurring-subscriptions/ui.yaml @ SHA c95253bc15b7d51b
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the recurring-subscriptions screen for **HSBC Open Banking**, a UK Open Banking AISP that automatically detects recurring payments from HSBC transaction history.

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F, outline #8B9198

**Component 1 - Top App Bar** (full width 393dp, height 64dp): Outfit medium 22sp title "Recurring Payments" in #E0E3E8 on #101417. No elevation.

**Component 2 - Error State** (centered in full scroll area below app bar, 32dp horizontal insets, 80dp top spacing): Icon warning_amber 72dp in #FFB4AB centered. 16dp gap. Outfit medium 20sp heading "Couldn't load recurring payments" in #E0E3E8 center-aligned. 8dp gap. Outfit regular 14sp body "HSBC transaction data is temporarily unavailable. Check your connection or try again." in #C1C7CE center-aligned, max 3 lines. 24dp gap. Button: filled pill background #95CDF7, label "Retry" in #00344E Outfit medium 14sp, 48dp height, 160dp min-width, radius 9999dp. 8dp gap below. Outlined button: border #95CDF7, label "View cached data" in #95CDF7 Outfit medium 14sp, 48dp height, visible only if cached data exists. All elements horizontally centered. No subscription list or banner visible. Archetype: error_state.

**Component 3 - Bottom Navigation Bar** (full width, height 80dp, background #1C2024): Active "Subscriptions": autorenew icon and label #95CDF7. Inactive "Overview", "Spending", "Budgets": icon and label #8B9198.

Do not use an em-dash anywhere in this design. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark surface by placing the Error State in a visually distinct lighter panel or error-coloured background region. Do not place dark text on outlined buttons or allow contrast to fall below WCAG AA.

A spare error layout centred on the near-black canvas: warning-amber #FFB4AB contained in the icon, trust-blue #95CDF7 restoring agency on the retry button, no distraction from the regulated-fintech register. restrained.

↑↑↑ MOCKUP PROMPT
