---
ui_yaml_sha: 10017cb86c8910c343922e455234d53499c3b1ecb237dd9c239ed7397e211a6e
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 64067da0ad75379e04550b0695c488ec7422a3dbd6765f4024b396f65c961446

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: atm-locator
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# atm-locator — empty state

> Auto-generated from screens/atm-locator/ui.yaml @ SHA a9fa0bf17232eeef
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the atm-locator screen for **HSBC Open Banking**, a UK Open Banking AISP showing a no-results message when no HSBC ATMs are found within range of the user's current geolocation.

Palette: surface #101417, primary #95CDF7, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, secondary #B7C9D9, outline #8B9198, primaryContainer #004B6F, onPrimary #00344E, secondaryContainer #384956

**Component 1 - Top App Bar** (full width, 56dp): static title "Nearby ATMs" in #E0E3E8 on #101417; location-pin icon left; no shadow.

**Component 2 - Map** (full width, 200dp tall): dark-scheme map tile centred on user location; no pin markers; subtle crosshair icon in #C1C7CE at centre; base tiles #181C20 roads #262A2E; edge-to-edge; empty_state archetype.

**Component 3 - Chip Row** (full width minus 32dp, 40dp): three filter chips: "All" selected with #95CDF7 border and #004B6F fill; "Deposit" and "24h" unselected in #384956 with #D3E5F5 label; 8dp gap; 24dp radius.

**Component 4 - Empty State** (centered, 393dp wide, 260dp tall, generous vertical breathing room): location-off icon 72dp in #95CDF7; heading "No ATMs found nearby" in Outfit 22sp #E0E3E8 centered; body "There are no HSBC ATMs within your current search radius. Try expanding the area or removing a service filter." in Outfit 14sp #C1C7CE centered max 280dp; 24dp gaps.

**Component 5 - Button** (280dp wide, 48dp tall, #95CDF7 fill, 24dp radius): label "Expand search area" in Outfit 14sp #00344E bold; centered horizontally; 24dp below body text.

**Component 6 - Bottom Navigation Bar** (full width, 56dp, #1C2024 fill): four tabs labeled Accounts, Balances, Party, ATMs; ATMs tab active with #95CDF7 icon and label; inactive tabs in #C1C7CE.

DO NOT use an em-dash anywhere in this mockup. DO NOT render any ATM card, service chip, or distance label when no results exist. DO NOT break the dark surface theme by inserting a white map tile or light panel. DO NOT place dark text on a dark button background or light text on a light button background.

Honest #95CDF7 wayfinding in a no-results zone. Mood: balanced.

↑↑↑ MOCKUP PROMPT
