---
ui_yaml_sha: 927a4ea2aa924d185dec8870cbdfc9f4ac91b01311daef7f791259aeb739a5f9
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 3326c371d76d10b73e28e5e50c2ff02170ac20f3d304b56b72e78360f7b205ba

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: user-onboarding
state: permissions_overview
state_visibility: permissions_overview

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# user-onboarding — permissions_overview state

> Auto-generated from screens/user-onboarding/ui.yaml @ SHA a88664ca4fd3e71b
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the permissions_overview state of the User Onboarding screen for **HSBC Open Banking**, a UK account-information app that shows the full set of HSBC data permissions requested before the user proceeds to consent.

Palette: primary #95CDF7, onPrimary #00344E, primaryContainer #004B6F, onPrimaryContainer #C9E6FF, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, surfaceContainer #1C2024

**Component 1 - Stat Block** (393dp wide, 24dp tall): Step progress indicator. Dot 1: 8dp filled primaryContainer #004B6F with check_mark icon onPrimaryContainer (completed). Dot 2: 8dp filled primary #95CDF7 (active). Dot 3: 6dp hollow outline #8B9198 (inactive). Centred, 16dp top margin.

**Component 2 - Section Header** (361dp, 48dp): "What we read from HSBC" Outfit 18sp bold onSurface #E0E3E8, left-aligned. This is the permissions_overview step of the detail_screen onboarding flow.

**Component 3 - List** (361dp wide, 6 rows at 64dp each): Each row has a leading icon in primary #95CDF7 at 24dp, a title in Outfit 16sp onSurface #E0E3E8, and a supporting line in Outfit 13sp onSurfaceVariant #C1C7CE. Row 1: manage_accounts "Account details" / "Name, account number, sort code". Row 2: account_balance "Balances" / "Current and available balance". Row 3: receipt_long "Transaction history" / "Up to 12 months of transactions". Row 4: autorenew "Standing orders" / "Recurring payment instructions". Row 5: subscriptions "Direct debits" / "Active mandates and amounts". Row 6: description "Statements" / "Monthly PDF statements". Rows separated by 1dp outlineVariant #41474D dividers.

**Component 4 - Banner** (361dp wide, 56dp, surfaceContainer #1C2024, 8dp radius): timer icon onSurfaceVariant #C1C7CE at 20dp left. Outfit 14sp "Access for 90 days. Renew or revoke at any time from Consents." in onSurfaceVariant #C1C7CE.

**Component 5 - Button** (361dp wide, 48dp tall, surfaceContainer #1C2024 fill outlined by outline #8B9198, onSurface #E0E3E8 label, 999dp radius): "Back" Outfit 16sp. Full-width outlined tonal.

**Component 6 - Button** (361dp wide, 48dp tall, primary #95CDF7 fill, onPrimary #00344E label, 999dp radius): "Next" Outfit 16sp bold. Full-width. 8dp below the Back button.

DO NOT use em-dash anywhere in text. DO NOT make any headline longer than 3 lines or any subtitle longer than 25 words. DO NOT break the dark theme between sections. DO NOT place light-on-light or dark-on-dark text and button combinations.

Each HSBC data type becomes a readable List row on surface #101417, with #95CDF7 leading icons drawing the eye down the permission set and onto the calm Next button at the base of this consent step.

↑↑↑ MOCKUP PROMPT
