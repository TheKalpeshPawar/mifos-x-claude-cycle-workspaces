---
ui_yaml_sha: 10017cb86c8910c343922e455234d53499c3b1ecb237dd9c239ed7397e211a6e
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 38bf8e45c84358e0a2d6ea0ea339346bf5e014ebc2917e37f041b0b7735b1ae3

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: atm-locator
state: error
state_visibility: error

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# atm-locator — error state

> Auto-generated from screens/atm-locator/ui.yaml @ SHA adeedcc1531ae465
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the atm-locator screen for **HSBC Open Banking**, a UK Open Banking AISP displaying a failure message when geolocation permission is denied or the HSBC ATM directory request cannot be completed.

Palette: surface #101417, primary #95CDF7, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, errorContainer #93000A, secondary #B7C9D9, outline #8B9198, primaryContainer #004B6F, onPrimary #00344E

**Component 1 - Top App Bar** (full width, 56dp): static title "Nearby ATMs" in #E0E3E8 on #101417; location-pin icon left; no shadow.

**Component 2 - Error State** (centered vertically within remaining 796dp, 393dp wide): circular badge 72dp in #93000A containing location-off icon in #FFB4AB; heading "Location unavailable" in Outfit 22sp #E0E3E8 centered; body "We could not access your location or load HSBC ATM data. Enable location access and try again." in Outfit 14sp #C1C7CE centered max 280dp; 24dp gap between elements; error_state archetype.

**Component 3 - Button** (280dp wide, 48dp tall, #95CDF7 fill, 24dp radius): label "Retry" in Outfit 14sp #00344E bold; centered horizontally; 24dp below body text.

**Component 4 - Bottom Navigation Bar** (full width, 56dp, #1C2024 fill): four tabs labeled Accounts, Balances, Party, ATMs; ATMs tab active with #95CDF7 icon and label; inactive tabs in #C1C7CE.

DO NOT use an em-dash anywhere in this mockup. DO NOT render any ATM card, map tile, filter chip, or shimmer block alongside the error state. DO NOT break the dark surface theme by inserting a white or light-grey panel behind the error illustration. DO NOT place dark text on a dark button background or light text on a light button background.

Steady #95CDF7 retry prompt on a composed dark error surface. Mood: calm.

↑↑↑ MOCKUP PROMPT
