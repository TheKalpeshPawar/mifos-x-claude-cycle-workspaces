---
ui_yaml_sha: ac6e434d7320f353f7841e0c17d7c30db5673903d54f2d6da93b8a2edec2a784
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 5411b1d99c0fd1b145885902baafe8dbd7f886e2b8704828893583fc7a4a955e

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: product
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# product — content state

> Auto-generated from screens/product/ui.yaml @ SHA a4ff65cbaa4aa91a
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the product screen for **HSBC Open Banking**, a UK Open Banking AISP that surfaces OBReadProduct2 account-product details including fees, credit interest rates, overdraft terms, and eligibility features for the authenticated customer.

Palette: surface #101417, primary #95CDF7, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, secondary #B7C9D9, outline #8B9198, primaryContainer #004B6F, onPrimary #00344E, errorContainer #93000A

**Component 1 - Top App Bar** (full width, 56dp): Outfit medium title "Product Details" in #E0E3E8 on #101417 background; back-navigation arrow left, share icon right; no elevation shadow; detail_screen archetype.

**Component 2 - Card** (full width minus 32dp, 12dp radius, #1C2024 fill): headline "HSBC Classic Credit Account" in Outfit 20sp #E0E3E8 bold; supporting line "PersonalCurrentAccount" in Outfit 14sp #C1C7CE; mono account reference "GB29NWBK60161331926819" in Outfit 12sp #8B9198; 16dp internal padding all sides.

**Component 3 - List** (full width minus 32dp): section label "Fees" in Outfit 12sp #95CDF7 uppercase with 8dp top padding; one 48dp row with label "Monthly max charge" in #E0E3E8 and trailing value "0.00 GBP" in #C1C7CE; hairline divider #41474D.

**Component 4 - List** (full width minus 32dp): section label "Credit Interest" in Outfit 12sp #95CDF7 uppercase; three 48dp rows: label "Purchase (EAR)" with trailing value "19.9% variable"; label "Cash advance (EAR)" with trailing value "29.9% variable"; label "Promotional rate" with trailing value "0% on balance transfers for 12 months"; values right-aligned in #C1C7CE; dividers #41474D.

**Component 5 - List** (full width minus 32dp): section label "Overdraft" in Outfit 12sp #95CDF7 uppercase; two 48dp rows: label "Arranged limit" with trailing value "500.00 GBP"; label "Arranged rate (EAR)" with trailing value "39.9%; buffer 0.00 GBP"; values in #C1C7CE; divider #41474D.

**Component 6 - List** (full width minus 32dp): section label "Features" in Outfit 12sp #95CDF7 uppercase; three 48dp rows each prefixed with check-circle icon in #95CDF7: row "No monthly account fee"; row "Free UK ATM cash withdrawals"; row "FSCS protected up to 85,000 GBP"; text in #E0E3E8 14sp.

**Component 7 - Bottom Navigation Bar** (full width, 56dp, #1C2024 fill): four tabs labeled Accounts, Balances, Party, ATMs; Accounts tab active with #95CDF7 icon and label; inactive tabs in #C1C7CE.

DO NOT use an em-dash anywhere in this mockup. DO NOT make any headline longer than three lines or any subtitle longer than 25 words. DO NOT break the dark surface theme by introducing a white or light-grey panel between content sections. DO NOT place dark text on a dark button background or light text on a light button background.

Calm #95CDF7 trust-blue data-spec on a near-black canvas. Mood: restrained.

↑↑↑ MOCKUP PROMPT
