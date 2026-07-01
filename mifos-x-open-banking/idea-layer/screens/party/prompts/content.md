---
ui_yaml_sha: 30a818627889bd9f5dc82a6ee7b672b5de2bb72e9d847e0b2b417c34501973de
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: ff0eda775a615d68d12e9755f3a217925f807bef75147e848b6f3bc6f9d5066c

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: party
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# party — content state

> Auto-generated from screens/party/ui.yaml @ SHA a89a1272393e594d
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the party screen for **HSBC Open Banking**, a UK Open Banking AISP presenting OBReadParty2 account-holder identity data including legal name, party type, contact details, and registered address for the authenticated customer.

Palette: surface #101417, primary #95CDF7, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, secondary #B7C9D9, outline #8B9198, primaryContainer #004B6F, onPrimary #00344E, secondaryContainer #384956

**Component 1 - Top App Bar** (full width, 56dp): Outfit medium title "Account Holder" in #E0E3E8 on #101417; back-navigation arrow left; no elevation shadow; detail_screen archetype.

**Component 2 - Card** (full width minus 32dp, 12dp radius, #1C2024 fill): circular avatar 48dp in #004B6F with initials "PS" in Outfit 16sp #C9E6FF; headline "Priya Sharma" in Outfit 20sp #E0E3E8 bold beside avatar; supporting line "Sole account holder" in Outfit 14sp #C1C7CE; pill chip labeled "Individual" in #D3E5F5 on #384956 background, 4dp radius, 8dp horizontal padding; 16dp internal padding.

**Component 3 - List** (full width minus 32dp): section label "Contact" in Outfit 12sp #95CDF7 uppercase with 8dp top padding; three 48dp rows: icon email-outline in #8B9198 with label "priya.sharma@example.com" in #E0E3E8; icon phone-android in #8B9198 with label "+44 7700 900000" in #E0E3E8; icon phone-outline in #8B9198 with label "+44 20 7946 0000" in #E0E3E8; role captions in #C1C7CE 12sp; dividers #41474D.

**Component 4 - List** (full width minus 32dp): section label "Address" in Outfit 12sp #95CDF7 uppercase; nested card on #1C2024 background 12dp radius 16dp padding: caption "Residential" in Outfit 12sp #C1C7CE; address lines "14 Canada Square, Canary Wharf", "London, E14 4AB" and "United Kingdom" each in Outfit 14sp #E0E3E8 stacked with 4dp line gap.

**Component 5 - Bottom Navigation Bar** (full width, 56dp, #1C2024 fill): four tabs labeled Accounts, Balances, Party, ATMs; Party tab active with #95CDF7 icon and label; inactive tabs in #C1C7CE.

DO NOT use an em-dash anywhere in this mockup. DO NOT render a consent banner, error rail, or shimmer block alongside the populated identity data. DO NOT break the dark surface theme by introducing a white or light-grey panel. DO NOT place dark text on a dark button background or light text on a light button background.

Clear #95CDF7 identity data rendered with regulated-industry restraint. Mood: restrained.

↑↑↑ MOCKUP PROMPT
