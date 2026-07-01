---
ui_yaml_sha: f9e175a0bb9de365db4c0803b856f44cd0182761536411bcd689e30e8f3ab0d5
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 8b226001c6569efcb761443a432767e29cf5bbaef63e6187daf971479f92df9d

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: transaction-detail
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# transaction-detail — content state

> Auto-generated from screens/transaction-detail/ui.yaml @ SHA d92bb27ecef86952
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the transaction-detail screen for **HSBC Open Banking**, a UK AISP app showing a full OBTransaction6 record for a single HSBC current account transaction.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, secondary #B7C9D9, error #FFB4AB, outline #8B9198

Archetype: detail_screen

**Component 1 - Top App Bar** (56dp h, full 393dp w): Outfit medium 22sp "Transaction Detail" #E0E3E8 on #101417; leading arrow-back icon 24dp #E0E3E8; no trailing actions.

**Component 2 - Stat Block** (full width, bg #101417, 24dp top padding, 16dp h-padding): hero amount "- £87.00" centred Outfit 700 40sp Roboto Mono #FFB4AB; subline "GBP · British Gas Payments Ltd" centred Outfit 400 14sp #B7C9D9; status Chip "Booked" 28dp h bg #1C2024 stroke #41474D label Outfit 12sp #E0E3E8 centred below subline; 12dp gap between hero, subline, and chip.

**Component 3 - Card** (full width minus 32dp, 12dp radius, bg #1C2024): section header "Transaction Details" Outfit 600 14sp #B7C9D9 16dp top-padding 16dp left-padding; seven List rows 56dp each with dividers #41474D; row layout: label left Outfit 400 14sp #B7C9D9, value right Outfit 400 14sp #E0E3E8; rows: "Booking Date" paired with "30 Jun 2026"; "Value Date" paired with "30 Jun 2026"; "Category" paired with "Bills and Utilities"; "MCC" paired with "4911 Electric Services"; "Balance After" label #B7C9D9 paired with monospace "+£2,254.56" Outfit 600 14sp Roboto Mono #95CDF7 right; "Reference" paired with "BRITISH GAS 7842001"; "Bank Transaction Code" paired with "DomesticPayment · DirectDebit".

**Component 4 - Bottom Navigation Bar** (56dp h, bg #1C2024, full width): "Accounts" active icon account-balance #95CDF7 label #95CDF7; "PFM" icon insights #8B9198; "Consents" icon verified-user #8B9198; "Profile" icon person #8B9198.

DO NOT use an em-dash anywhere in transaction metadata or screen labels. DO NOT make the merchant subline or any Card row value span longer than three visible lines. DO NOT apply a light surface to the detail Card or the hero amount header region. DO NOT render the debit hero amount in primary #95CDF7 since debits must use error #FFB4AB and credits must use primary #95CDF7.

Mood: refined and balanced transaction receipt; the hero debit in #FFB4AB anchors the screen, the balance-after in #95CDF7 confirms the account impact, and the spare dark Card keeps every OBTransaction6 field scannable.

↑↑↑ MOCKUP PROMPT
