---
ui_yaml_sha: 10017cb86c8910c343922e455234d53499c3b1ecb237dd9c239ed7397e211a6e
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: cf35317784f7971320558d5e86bad704e25f8f3745a2d425b8c1ff38ad91c054

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: atm-locator
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# atm-locator — loading state

> Auto-generated from screens/atm-locator/ui.yaml @ SHA ed65281d507c4fc0
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the atm-locator screen for **HSBC Open Banking**, a UK Open Banking AISP showing shimmer skeleton placeholders while geolocation is being detected and HSBC ATM directory data fetches.

Palette: surface #101417, primary #95CDF7, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, secondary #B7C9D9, outline #8B9198, primaryContainer #004B6F, onPrimary #00344E

**Component 1 - Top App Bar** (full width, 56dp): static title "Nearby ATMs" in #E0E3E8 on #101417; location-pin icon left; no shimmer on the bar itself; skeleton_screen archetype.

**Component 2 - Map** (full width, 200dp tall): solid shimmer rectangle 393dp x 200dp in #262A2E; a single pulsing dot at centre in #95CDF7 at 50 percent opacity to indicate location lookup in progress; no tile content, no road lines.

**Component 3 - Chip Row** (full width minus 32dp, 40dp): three pill-shaped shimmer placeholders 72dp x 32dp each in #262A2E spaced 8dp apart; 24dp radius; no labels.

**Component 4 - List** (full width minus 32dp): shimmer count bar 100dp x 12dp in #262A2E; four Card-shaped shimmer blocks each 361dp x 96dp with 12dp radius stacked 8dp apart; each block contains three internal shimmer shards: 160dp x 16dp top, 200dp x 13dp middle, 80dp x 12dp bottom; shimmer gradient sweeps left-to-right at #262A2E over #1C2024 with subtle pulse.

**Component 5 - Bottom Navigation Bar** (full width, 56dp, #1C2024 fill): four tab slots in #C1C7CE at 60 percent opacity; no active highlight shown during fetch.

DO NOT use an em-dash anywhere in this mockup. DO NOT render any ATM name, address, distance, or service chip inside shimmer blocks. DO NOT break the dark surface theme by inserting any white map tile or light panel. DO NOT place dark text on a dark button background or light text on a light button background.

Patient #95CDF7 pulse while location resolves. Mood: minimal.

↑↑↑ MOCKUP PROMPT
