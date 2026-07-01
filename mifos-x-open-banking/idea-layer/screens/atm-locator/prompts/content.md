---
ui_yaml_sha: 10017cb86c8910c343922e455234d53499c3b1ecb237dd9c239ed7397e211a6e
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 1f6a0a58e4f6ea9c4f5bde27cc5e2dfa64d50861b40dbac16aee5afbe0e3709e

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: atm-locator
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# atm-locator — content state

> Auto-generated from screens/atm-locator/ui.yaml @ SHA 1032a8b10d2fc36f
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the atm-locator screen for **HSBC Open Banking**, a UK Open Banking AISP showing a dark-scheme map and a scrollable list of nearby HSBC ATMs derived from client-side geolocation with distance, address, and service capabilities for each result.

Palette: surface #101417, primary #95CDF7, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, secondary #B7C9D9, outline #8B9198, primaryContainer #004B6F, onPrimary #00344E, secondaryContainer #384956, onSecondaryContainer #D3E5F5

**Component 1 - Top App Bar** (full width, 56dp): Outfit medium title "Nearby ATMs" in #E0E3E8 on #101417; location-pin icon left; no elevation shadow; detail_screen archetype.

**Component 2 - Map** (full width, 200dp tall): dark-scheme map tile centred on Canary Wharf, E14; base tiles #181C20, roads #262A2E, water #1C2024; four #95CDF7 teardrop pin markers at ATM locations; user-location dot in #C9E6FF with 8dp pulse ring in #004B6F; map edge-to-edge no border radius.

**Component 3 - Chip Row** (full width minus 32dp, 40dp, 8dp top margin): three filter chips: "All" selected with #95CDF7 border and #004B6F fill and #C9E6FF label; "Deposit" and "24h" unselected in #384956 with #D3E5F5 label; 8dp gap between chips; 24dp radius each.

**Component 4 - List** (full width minus 32dp): result count caption "4 ATMs near you" in Outfit 12sp #C1C7CE 8dp below chips; four Card items stacked with 8dp gap: Card 1 on #1C2024 fill 12dp radius 12dp padding: headline "HSBC Canary Wharf" in Outfit 16sp #E0E3E8 bold, sub "8 Canada Square, E14 5HQ" in 13sp #C1C7CE, distance chip "0.3 mi" in 12sp #95CDF7, service chips labeled Deposit, Withdrawal, Contactless in #384956 with #D3E5F5 text; Card 2: headline "HSBC Bishopsgate" sub "93 Bishopsgate, EC2M 3WT" distance "0.8 mi" service chips Withdrawal, Contactless; Card 3: headline "HSBC Pall Mall" sub "69 Pall Mall, SW1Y 5EX" distance "1.2 mi" service chips Deposit, Withdrawal, 24h, Contactless; Card 4: headline "HSBC Liverpool Street" sub "25 Old Broad Street, EC2N 1HQ" distance "1.5 mi" service chip Withdrawal.

**Component 5 - Bottom Navigation Bar** (full width, 56dp, #1C2024 fill): four tabs labeled Accounts, Balances, Party, ATMs; ATMs tab active with #95CDF7 icon and label; inactive tabs in #C1C7CE.

DO NOT use an em-dash anywhere in this mockup. DO NOT render generic labels such as ATM 1, ATM 2, or Branch A; use only the real HSBC branch names and addresses listed above. DO NOT break the dark surface theme by inserting a white map background or light panel. DO NOT place dark chip label text on a dark chip background or light chip label on a light chip background.

Legible #95CDF7 location pins on a calm dark map. Mood: calm.

↑↑↑ MOCKUP PROMPT
