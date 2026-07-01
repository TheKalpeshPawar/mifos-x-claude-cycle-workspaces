---
ui_yaml_sha: 30a818627889bd9f5dc82a6ee7b672b5de2bb72e9d847e0b2b417c34501973de
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 8fb2687799de52f18a3763b2a25d4b65ecb93b2bd0253ca6b9d557775bd190d4

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: party
state: consent_required
state_visibility: consent_required

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# party — consent_required state

> Auto-generated from screens/party/ui.yaml @ SHA 7035c3614ed976cb
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the consent_required state of the party screen for **HSBC Open Banking**, a UK Open Banking AISP prompting the PSU to re-authorise their Open Banking consent before OBReadParty2 account-holder data can be retrieved from HSBC.

Palette: surface #101417, primary #95CDF7, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, secondary #B7C9D9, outline #8B9198, primaryContainer #004B6F, onPrimary #00344E, onPrimaryContainer #C9E6FF

**Component 1 - Top App Bar** (full width, 56dp): Outfit medium title "Account Holder" in #E0E3E8 on #101417; back-navigation arrow left; no elevation shadow; detail_screen archetype.

**Component 2 - Banner** (full width minus 32dp, 80dp, #004B6F fill, 12dp radius): lock-outline icon 24dp in #C9E6FF positioned 16dp from left; headline "Consent required" in Outfit 14sp #C9E6FF bold; supporting line "Your Open Banking authorisation has expired. Re-authorise to view holder details." in Outfit 13sp #C9E6FF max 260dp wide; 16dp internal padding.

**Component 3 - Card** (full width minus 32dp, 12dp radius, #1C2024 fill): circular avatar 48dp in #004B6F with initials "PS" in #C9E6FF; name "Priya Sharma" in Outfit 20sp #E0E3E8 beside avatar; supporting line "Sole account holder" in Outfit 14sp #C1C7CE; three masked data rows: row labeled "Email" in #C1C7CE 12sp with a 180dp redacted bar in #41474D; row labeled "Mobile" with 140dp redacted bar in #41474D; row labeled "Address" with 220dp redacted bar in #41474D; 16dp padding.

**Component 4 - Button** (280dp wide, 48dp tall, #95CDF7 fill, 24dp radius): label "Re-authorise with HSBC" in Outfit 14sp #00344E bold; centered horizontally below the card; 24dp top margin.

**Component 5 - Bottom Navigation Bar** (full width, 56dp, #1C2024 fill): four tabs labeled Accounts, Balances, Party, ATMs; Party tab active with #95CDF7 icon and label; inactive tabs in #C1C7CE.

DO NOT use an em-dash anywhere in this mockup. DO NOT reveal any real email address, phone number, or postal address inside the masked rows when consent has not been granted. DO NOT break the dark surface theme by introducing a white or light consent panel. DO NOT place dark text on a dark button background or light text on a light button background.

Secure #95CDF7 consent gate, unambiguous and calm. Mood: restrained.

↑↑↑ MOCKUP PROMPT
