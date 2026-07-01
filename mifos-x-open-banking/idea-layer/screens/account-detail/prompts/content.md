---
ui_yaml_sha: 0120895d6ee57bd035a4abe15da76e75865b30a5f02a3bb1e89215c380a564a0
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: a5b430d52eeee33d87872d2e2fa1cc18e31f8d4d8dbda0c6743a0e13abc04614

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: account-detail
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# account-detail — content state

> Auto-generated from screens/account-detail/ui.yaml @ SHA d85847d3da18f239
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the account-detail screen for **HSBC Open Banking**, a UK AISP app that surfaces HSBC current account balances and metadata under PSD2 read-only consent.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, secondary #B7C9D9, error #FFB4AB, outline #8B9198

Archetype: detail_screen

**Component 1 - Top App Bar** (56dp h, full 393dp w): Outfit medium 22sp "HSBC Current Account" #E0E3E8 on #101417 surface; leading arrow-back icon 24dp #E0E3E8; no trailing icons; top-of-screen anchored.

**Component 2 - Card** (full width minus 32dp insets, 12dp radius, bg #1C2024): headline Outfit 600 18sp "HSBC Advance Current Account" #E0E3E8; supporting line "Sort code: 40-05-15, Acc no: 12345678" Outfit 400 14sp #B7C9D9; meta line "GBP · Servicer: HSBC UK BANK PLC" Outfit 12sp #8B9198; footer "Last updated: 29 Jun 2026, 09:14 BST" Outfit 12sp #8B9198; 16dp internal padding all sides.

**Component 3 - Banner** (full width minus 32dp, 8dp radius, bg #004B6F): shield icon 16dp #95CDF7 inline-left; "Read-only Open Banking access. Your money cannot be moved." Outfit 13sp #C9E6FF; 12dp vertical padding, 16dp horizontal padding.

**Component 4 - List** (full width, section label "Balances" Outfit 600 16sp #E0E3E8): three rows 56dp each, dividers #41474D; row 1 label "InterimAvailable" Outfit 400 16sp #E0E3E8 left, value monospace "+£2,341.56" Outfit 600 16sp #95CDF7 right; row 2 "ClosingAvailable" #E0E3E8 left, monospace "+£2,279.12" #95CDF7 right; row 3 "OpeningCleared" #E0E3E8 left, monospace "+£2,341.56" #95CDF7 right; all amounts Roboto Mono.

**Component 5 - Chip Row** (horizontal scroll, 16dp start, 8dp gap, section label "Explore" Outfit 600 16sp #E0E3E8): seven assist chips bg #1C2024 stroke #41474D label #E0E3E8; chip labels: "Transactions", "Statements", "Standing Orders", "Direct Debits", "Scheduled", "Beneficiaries", "ATM Locator"; each paired with 18dp icon.

**Component 6 - Bottom Navigation Bar** (56dp h, bg #1C2024, full width): four items; "Accounts" active icon account-balance #95CDF7 label #95CDF7; "PFM" icon insights #8B9198 label #8B9198; "Consents" icon verified-user #8B9198 label #8B9198; "Profile" icon person #8B9198 label #8B9198.

DO NOT use an em-dash anywhere in text or labels. DO NOT render any headline longer than three lines or any supporting text longer than 25 words. DO NOT switch to a light surface colour in any section while the rest of the screen uses the dark #101417 background. DO NOT place dark-coloured text on a dark chip or button surface where contrast would fail WCAG AA.

Mood: restrained and balanced fintech detail view; accent #95CDF7 marks every live balance value, keeping the dark surface calm and the HSBC data sharply legible.

↑↑↑ MOCKUP PROMPT
