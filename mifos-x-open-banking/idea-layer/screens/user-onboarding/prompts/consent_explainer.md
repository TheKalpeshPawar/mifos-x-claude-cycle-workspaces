---
ui_yaml_sha: 927a4ea2aa924d185dec8870cbdfc9f4ac91b01311daef7f791259aeb739a5f9
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 32272e57c7ee11e661d0107264ec4de3e8add20b190a197fe210e3c0fe818a8b

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: user-onboarding
state: consent_explainer
state_visibility: consent_explainer

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# user-onboarding — consent_explainer state

> Auto-generated from screens/user-onboarding/ui.yaml @ SHA 55a0c923a370a87e
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the consent_explainer state of the User Onboarding screen for **HSBC Open Banking**, a UK account-information app that reassures users about what this app never does before the final HSBC redirect button.

Palette: primary #95CDF7, onPrimary #00344E, primaryContainer #004B6F, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, surfaceContainer #1C2024, outline #8B9198

**Component 1 - Stat Block** (393dp wide, 24dp tall): Step progress indicator. Dots 1 and 2: 8dp filled primaryContainer #004B6F with check_mark (completed). Dot 3: 8dp filled primary #95CDF7 (active). Centred, 16dp top margin.

**Component 2 - Section Header** (361dp, 48dp): "What we never do" Outfit 18sp bold onSurface #E0E3E8, left-aligned. This is the consent_explainer step of the detail_screen onboarding flow, the trust gate before final redirect.

**Component 3 - List** (361dp wide, 3 rows at 80dp each): Row 1: money_off icon onSurfaceVariant #C1C7CE 24dp, "Never make payments" Outfit 16sp onSurface #E0E3E8, "We are read-only. Payments require a separate PISP service." Outfit 13sp onSurfaceVariant. Row 2: lock icon onSurfaceVariant, "Never ask for your password" Outfit 16sp onSurface, "Authentication happens on HSBC's portal, not in this app." Outfit 13sp onSurfaceVariant. Row 3: cancel icon onSurfaceVariant, "No lock-in" Outfit 16sp onSurface, "Revoke access in seconds from the Consents screen." Outfit 13sp onSurfaceVariant. Rows separated by 1dp outlineVariant #41474D dividers.

**Component 4 - Banner** (361dp wide, 48dp, surfaceContainer #1C2024, 8dp radius): Outfit 12sp "This app acts as an FCA-authorised AISP under PSD2 and the UK Open Banking Standard." in onSurfaceVariant #C1C7CE.

**Component 5 - Button** (361dp wide, 48dp tall, primary #95CDF7 fill, onPrimary #00344E label, 999dp radius): "Connect to HSBC" Outfit 16sp bold, open_in_new icon right. Full-width. Opens HSBC in the system browser.

**Component 6 - Button** (361dp wide, 48dp tall, surfaceContainer #1C2024 fill outlined by outline #8B9198, onSurface #E0E3E8 label, 999dp radius): "Back" Outfit 16sp. Full-width outlined tonal. 8dp below primary button.

**Component 7 - Button** (361dp wide, 40dp tall, transparent fill, primary #95CDF7 label): "How does Open Banking work?" Outfit 14sp. Text-only style, centred, 4dp below Back button.

DO NOT use em-dash anywhere in text. DO NOT make any headline longer than 3 lines or any subtitle longer than 25 words. DO NOT break the dark theme between sections. DO NOT place light-on-light or dark-on-dark text and button combinations.

Three plainly worded reassurances earn the user's trust before the "Connect to HSBC" button appears in #95CDF7, a minimal and sequenced reveal that closes onboarding with complete transparency.

↑↑↑ MOCKUP PROMPT
