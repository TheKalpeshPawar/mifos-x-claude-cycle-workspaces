---
ui_yaml_sha: 0120895d6ee57bd035a4abe15da76e75865b30a5f02a3bb1e89215c380a564a0
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: a4aeb90aaaea8592ab1551e1a7075864cf7dfcf7168f13c2e8099fd1b3031902

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: account-detail
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# account-detail — loading state

> Auto-generated from screens/account-detail/ui.yaml @ SHA d4587d6d01e78ba4
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the account-detail screen for **HSBC Open Banking**, a UK AISP app showing shimmer skeleton placeholders while HSBC current account data loads over the Open Banking API.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, secondary #B7C9D9, outline #8B9198

Archetype: skeleton_screen

**Component 1 - Top App Bar** (56dp h, full 393dp w, bg #101417): shimmer pill 160dp wide 20dp h replacing title text; leading arrow-back icon 24dp #E0E3E8 visible since navigation is always live; top-of-screen anchored.

**Component 2 - Card** (full width minus 32dp, 12dp radius, bg #1C2024): three shimmer bars stacked with 8dp row gap; bar 1 200dp wide 18dp h for title placeholder; bar 2 260dp wide 14dp h for sort-code line; bar 3 180dp wide 12dp h for meta line; shimmer gradient sweeps left-to-right over #262A2E base at low contrast.

**Component 3 - Banner** (full width minus 32dp, 8dp radius, bg #004B6F): single shimmer bar full-width 13dp h at 50% opacity; structure preserved so layout does not shift on data arrival.

**Component 4 - List** (full width, section label shimmer 80dp x 14dp): three skeleton rows 56dp each, dividers #41474D; each row has a 160dp shimmer bar left and a 80dp shimmer bar right; shimmer bg #262A2E; no real balance values or account identifiers rendered.

**Component 5 - Chip Row** (horizontal scroll, 16dp start, 8dp gap): six rounded-pill shimmer chips 96dp x 32dp each, bg #262A2E; no labels or icons visible during skeleton state.

**Component 6 - Bottom Navigation Bar** (56dp h, bg #1C2024, full width): four nav items with icons at 30% opacity; no active-state highlight applied during loading.

DO NOT show any real account number, balance figure, or text string during the skeleton state. DO NOT use an em-dash or any readable label in shimmer placeholder bars. DO NOT introduce a light surface or alter the dark Material 3 shell structure during loading. DO NOT render the Retry button or any error-tinted element while HSBC data is still in flight.

Mood: restrained and calm shimmer skeleton; #95CDF7 is absent until HSBC data resolves, keeping the dark #101417 surface silent and the loading rhythm minimal.

↑↑↑ MOCKUP PROMPT
