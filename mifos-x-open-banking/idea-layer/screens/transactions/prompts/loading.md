---
ui_yaml_sha: 0dff95644480441c813a12ec1e4b235c143956736621078e5327ff9fef0397ce
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 1a92e790af1efe1325789803188e2e915f4e11dbbd85d9c12964ed4c15f13537

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: transactions
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# transactions — loading state

> Auto-generated from screens/transactions/ui.yaml @ SHA 821ec56c82166bfb
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the transactions screen for **HSBC Open Banking**, a UK AISP app displaying shimmer skeleton placeholders while HSBC current account transaction data loads from the Open Banking API.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, secondary #B7C9D9, outline #8B9198

Archetype: skeleton_screen

**Component 1 - Top App Bar** (56dp h, full 393dp w, bg #101417): shimmer bar 120dp wide 20dp h replacing title; arrow-back icon 24dp #E0E3E8 visible since navigation remains live; top-of-screen anchored.

**Component 2 - Stat Block** (full width minus 32dp, bg #1C2024, 12dp radius, 16dp padding): two shimmer cells side-by-side; left shimmer pill 80dp x 20dp; right shimmer pill 80dp x 20dp; shimmer gradient sweeps left-to-right over #262A2E base; no monetary values rendered.

**Component 3 - Chip Row** (horizontal scroll, 16dp start, 8dp gap): four pill shimmer chips 96dp x 32dp each, bg #262A2E; no chip labels or icons visible during skeleton state.

**Component 4 - List** (full width): two date-group skeleton sections; each group starts with shimmer bar 160dp x 12dp bg #262A2E as date header; five rows per group 64dp h; each row has shimmer circle 40dp left, shimmer bar 180dp x 14dp centre, shimmer bar 64dp x 14dp right; dividers #41474D; no merchant names, amounts, or categories rendered.

**Component 5 - Bottom Navigation Bar** (56dp h, bg #1C2024, full width): four nav items at 30% opacity; no active-state highlight applied during loading.

DO NOT render any real merchant name, amount, date, or category label during the skeleton state. DO NOT use an em-dash or any visible text in shimmer placeholder bars. DO NOT apply credit colour #95CDF7 or debit colour #FFB4AB to any skeleton element. DO NOT show the Chip Row active state or Stat Block monetary values while HSBC data is still loading.

Mood: calm and restrained shimmer rhythm; #95CDF7 is withheld until HSBC transaction data resolves, keeping the dark #101417 field quiet and the skeleton motion minimal.

↑↑↑ MOCKUP PROMPT
