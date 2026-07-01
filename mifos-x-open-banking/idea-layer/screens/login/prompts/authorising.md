---
ui_yaml_sha: f3e158d2061f9b65df0967ab629f85014d9c735d2fa883594e830970abf5feda
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 373461ab7618e4223228456d022408045a164b18a1ffeaf278f5074f494af418

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: login
state: authorising
state_visibility: authorising

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# login — authorising state

> Auto-generated from screens/login/ui.yaml @ SHA fa4c586db38ff07b
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the authorising state of the Login screen for **HSBC Open Banking**, a UK account-information app processing an OAuth callback after the user granted consent on HSBC's secure portal.

Palette: primary #95CDF7, onPrimary #00344E, primaryContainer #004B6F, onPrimaryContainer #C9E6FF, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, surfaceContainer #1C2024

**Component 1 - Top App Bar** (393dp wide, 64dp tall): No title. No navigation icon. Back navigation is disabled during the OAuth callback. surface #101417 background.

**Component 2 - Stat Block** (361dp wide, 48dp): Indeterminate linear progress bar in primary #95CDF7, 4dp track height, animated sweep. Full 361dp width. This is the detail_screen in-flight authorisation indicator. No user interaction is available.

**Component 3 - Card** (361dp wide, 136dp tall, surfaceContainer #1C2024, 12dp radius): Status message. check_circle icon in primaryContainer #004B6F at 32dp, centred. Outfit 20sp "Completing authorisation" in onSurface #E0E3E8, centred, 12dp below icon. Outfit 14sp "You approved access on the HSBC portal. Confirming your consent now." in onSurfaceVariant #C1C7CE, centred, 24dp inset, 8dp below headline. No action buttons present.

**Component 4 - Banner** (361dp wide, 56dp, primaryContainer #004B6F, 8dp radius): lock icon in onPrimaryContainer #C9E6FF at 20dp left. Outfit 14sp "Do not close this app." in onPrimaryContainer #C9E6FF. 16dp gap between icon and text.

DO NOT use em-dash anywhere in text. DO NOT make any headline longer than 3 lines or any subtitle longer than 25 words. DO NOT break the dark theme between sections. DO NOT place light-on-light or dark-on-dark text and button combinations.

The authorising state strips every interactive surface, letting the #95CDF7 progress bar and a single reassurance card communicate handshake progress with minimal motion, a calm and deliberate interstitial for a FAPI 2.0 regulated consent callback.

↑↑↑ MOCKUP PROMPT
