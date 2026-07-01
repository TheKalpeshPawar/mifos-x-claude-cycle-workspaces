---
ui_yaml_sha: 66c8a95765ac08cf659947bd96cf36fcad9dd366c305ca94719196dcf4ee4475
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 19bde8abe476849c31cbff02ef3bf40d06cf2f05e275b90b5915d8f231402ffb

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: home
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# home — content state

> Auto-generated from screens/home/ui.yaml @ SHA 357bad7eddf9c466
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the Home screen for **HSBC Open Banking**, a UK account-information app that surfaces live HSBC balances and transactions via read-only Open Banking consent.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, outline #8B9198

**Component 1 - Top App Bar** (393dp wide, 64dp tall): Outfit 22sp "My Accounts" in onSurface #E0E3E8, surface #101417 background, no elevation, no leading icon.

**Component 2 - Chip Row** (361dp wide, 48dp tall, 16dp horizontal padding): Three account-selector chips: "Current Account", "Savings", "Credit Card". Active chip uses primaryContainer #004B6F fill with onPrimaryContainer #C9E6FF label at Outfit 14sp. Inactive chips use surfaceContainerHighest #313539 fill, onSurfaceVariant #C1C7CE label. 8dp gap between chips. This is the detail_screen account switcher.

**Component 3 - Card** (361dp wide, 128dp tall, surfaceContainer #1C2024, 12dp radius): Hero balance for "HSBC Current Account" (sort code 40-12-34, account ••••5678). Outfit 13sp "Current Account" onSurfaceVariant #C1C7CE top row. Outfit 30sp bold "£3,241.85" onSurface #E0E3E8. Outfit 13sp "Available £3,019.42" onSurfaceVariant below. Outfit 12sp "••••5678" outline #8B9198 at bottom.

**Component 4 - Card** (361dp wide, 80dp tall, surfaceContainer #1C2024, 12dp radius): Quick actions row, four icon buttons at equal spacing. Icons in primary #95CDF7 at 24dp: send (Pay), receipt_long (Transactions), description (Statements), shield (Consents). Each has Outfit 12sp label in onSurfaceVariant #C1C7CE below.

**Component 5 - Section Header** (361dp, 48dp): "Recent transactions" Outfit 14sp onSurfaceVariant #C1C7CE left. "View all" text button primary #95CDF7 right.

**Component 6 - List** (361dp wide, 5 rows at 72dp each): Row 1: grocery icon, "Waitrose and Partners" Outfit 16sp onSurface #E0E3E8, "27 Jun 2026" 12sp onSurfaceVariant, "-£42.18" 16sp error #FFB4AB right. Row 2: coffee icon, "Pret A Manger", "27 Jun 2026", "-£6.80" error #FFB4AB. Row 3: bank icon, "BACS CREDIT Acme Corp Ltd", "26 Jun 2026", "+£2,850.00" primary #95CDF7. Row 4: water icon, "Thames Water", "26 Jun 2026", "-£28.50" error #FFB4AB. Row 5: train icon, "TfL Contactless", "25 Jun 2026", "-£9.40" error #FFB4AB. Rows separated by 1dp outlineVariant #41474D dividers.

**Component 7 - Card** (361dp wide, 80dp tall, surfaceContainer #1C2024, 12dp radius): Spending snapshot. "Spending this month" Outfit 14sp onSurfaceVariant left. "£847.20" Outfit 20sp onSurface #E0E3E8 below. "Top category: Groceries" Outfit 13sp onSurfaceVariant. chevron_right icon onSurfaceVariant #C1C7CE at right edge.

**Component 8 - Bottom Navigation Bar** (393dp wide, 80dp tall, surfaceContainer #1C2024): Four tabs. Home is active: icon and label in primary #95CDF7. Accounts, Insights, Profile are inactive: icons and labels in onSurfaceVariant #C1C7CE.

DO NOT use em-dash anywhere in text. DO NOT make any headline longer than 3 lines or any subtitle longer than 25 words. DO NOT break the dark theme between sections. DO NOT place light-on-light or dark-on-dark text and button combinations.

The detail_screen lays every financial figure in clear Outfit type on surface #101417, with #95CDF7 marking credit amounts, active tab, and interactive affordances for a calm, regulated read of household money.

↑↑↑ MOCKUP PROMPT
