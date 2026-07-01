---
ui_yaml_sha: f3e158d2061f9b65df0967ab629f85014d9c735d2fa883594e830970abf5feda
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 250df1520dc98383fcc1fb705c65f26a76ca8c5ca82e908a137ac9bf251ca6fd

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: login
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# login — content state

> Auto-generated from screens/login/ui.yaml @ SHA 9a036b48badf2d94
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the Login screen for **HSBC Open Banking**, a UK account-information app that presents the full Open Banking consent request before redirecting the user to HSBC's secure portal.

Palette: primary #95CDF7, onPrimary #00344E, primaryContainer #004B6F, onPrimaryContainer #C9E6FF, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, surfaceContainer #1C2024

**Component 1 - Top App Bar** (393dp wide, 64dp tall): No title. arrow_back icon in onSurface #E0E3E8 left. surface #101417 background.

**Component 2 - Card** (361dp wide, 148dp tall, surfaceContainer #1C2024, 12dp radius): HSBC consent explainer, the detail_screen entry point. Top row: hexagonal HSBC red marque icon 28dp left, "FCA Regulated" Outfit 12sp onSurfaceVariant #C1C7CE right. Headline: Outfit 18sp "HSBC will share your account data with this app" in onSurface #E0E3E8, max 2 lines. Body: Outfit 14sp "This app is read-only. We never make payments or store your HSBC password." in onSurfaceVariant #C1C7CE. Divider 1dp outlineVariant #41474D. Footer: "Authorised by the FCA under Open Banking (PSD2)." Outfit 12sp onSurfaceVariant.

**Component 3 - Section Header** (361dp, 48dp): "Permissions requested" Outfit 14sp onSurfaceVariant #C1C7CE left. No trailing action.

**Component 4 - List** (361dp wide, 10 rows at 56dp each): Each row has check_circle_outline icon in primary #95CDF7 at 20dp left and Outfit 16sp label in onSurface #E0E3E8. Rows: "Account details", "Balances", "Transaction history", "Beneficiaries", "Standing orders", "Direct debits", "Scheduled payments", "Statements", "Parties", "Products". Rows separated by 1dp outlineVariant #41474D dividers.

**Component 5 - Banner** (361dp wide, 64dp, surfaceContainer #1C2024, 8dp radius): Consent duration. Outfit 14sp "Access granted for 90 days" in onSurface #E0E3E8 left. Below: Outfit 12sp "Expires 29 September 2026" in onSurfaceVariant #C1C7CE.

**Component 6 - Button** (361dp wide, 48dp tall, primary #95CDF7 fill, onPrimary #00344E label, 999dp radius): "Continue to HSBC" Outfit 16sp bold, open_in_new icon right. Full-width. Tapping opens HSBC's portal in the system browser.

**Component 7 - Button** (361dp wide, 48dp tall, surfaceContainer #1C2024 fill, onSurface #E0E3E8 label outlined, 999dp radius): "Cancel" Outfit 16sp. Full-width outlined tonal style. 8dp below the primary button.

DO NOT use em-dash anywhere in text. DO NOT make any headline longer than 3 lines or any subtitle longer than 25 words. DO NOT break the dark theme between sections. DO NOT place light-on-light or dark-on-dark text and button combinations.

Clear Outfit type on surface #101417 surfaces every permission the user grants before the HSBC redirect, with #95CDF7 on check icons and the primary action button providing a restrained visual hierarchy that earns trust before authentication.

↑↑↑ MOCKUP PROMPT
