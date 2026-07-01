---
ui_yaml_sha: dc51a93dfe2c575708401b94ec0aad258941119f5f0891dc9bcbab82740013cd
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: de499bf2f1e495e5fa0c50bbfc4523e1123544e148fd977a5856885a36883471

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: consent-detail
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# consent-detail — loading state

> Auto-generated from screens/consent-detail/ui.yaml @ SHA 4d8f7d366b24ba97
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the consent-detail screen for **HSBC Open Banking**, a UK AISP app fetching a single HSBC consent record and its full permission list, built on Trust Blue minimalist Material 3 DARK on 393x852dp Pixel 5.

Palette: surface #101417, onSurface #E0E3E8, primary #95CDF7, onPrimary #00344E, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, primaryContainer #004B6F

**Component 1 - Top App Bar** (full-width, 64dp): Outfit Medium 22sp "Consent detail" #E0E3E8 on #101417; back-arrow leading; archetype skeleton_screen.

**Component 2 - Card** (full-width minus 32dp, 88dp, #1C2024 radius 12dp): circle shimmer 40dp left; shimmer block 120dp wide 16dp tall right of circle; shimmer block 200dp wide 12dp tall below; animated sweep from #1C2024 to #262A2E.

**Component 3 - Banner** (full-width minus 32dp, 48dp, #1C2024): full-width shimmer rect 18dp tall radius 8dp; same sweep #1C2024 to #262A2E.

**Component 4 - List** (full-width minus 32dp): section label shimmer 88dp wide 10dp tall; four row skeletons 48dp each - circle shimmer 20dp left, line shimmer 200dp wide 14dp tall right; sweep synchronised with card above.

**Component 5 - List** (full-width minus 32dp): section label shimmer 72dp wide 10dp tall; 11 row skeletons 48dp each - circle shimmer 20dp left, line shimmers alternating 200dp and 240dp wide 14dp tall plus supporting line 160dp wide 11dp tall; preserves the permission list density from the content state.

**Component 6 - Button** (full-width minus 32dp, 48dp): full-width rect shimmer 48dp tall radius 24dp; no visible label.

Do not use em-dash anywhere in labels or body copy. Do not make any headline longer than 3 lines or any subtitle longer than 25 words. Do not break the dark #101417 surface theme between sections by introducing light containers or white backgrounds. Do not place light-coloured text on a light-coloured button, or dark text on a dark button.

Skeleton shimmer sweeps uniformly from #1C2024 to #262A2E across all blocks in synchrony; Trust Blue (#95CDF7) holds only on the back-arrow, keeping the restrained dark field calm while the PSU waits for the HSBC consent record to resolve.

↑↑↑ MOCKUP PROMPT
