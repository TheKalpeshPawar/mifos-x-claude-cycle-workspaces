---
ui_yaml_sha: ac6e434d7320f353f7841e0c17d7c30db5673903d54f2d6da93b8a2edec2a784
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 3ed2b3d2a03d5f9594c310ae6d72655354c63b7282f84189215fd1c024fb10f3

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: product
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# product — loading state

> Auto-generated from screens/product/ui.yaml @ SHA e18ef22091bc3dce
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the product screen for **HSBC Open Banking**, a UK Open Banking AISP showing shimmer skeleton placeholders block-for-block while the OBReadProduct2 response fetches from HSBC's API.

Palette: surface #101417, primary #95CDF7, onSurface #E0E3E8, surfaceContainer #1C2024, onSurfaceVariant #C1C7CE, error #FFB4AB, secondary #B7C9D9, outline #8B9198, primaryContainer #004B6F, onPrimary #00344E

**Component 1 - Top App Bar** (full width, 56dp): static title "Product Details" in #E0E3E8 on #101417; back-navigation arrow left; no shimmer on the bar itself; skeleton_screen archetype.

**Component 2 - Card** (full width minus 32dp, 12dp radius, #1C2024 fill): three stacked shimmer bars inside: 180dp x 18dp rounded-4, 120dp x 14dp rounded-4, 220dp x 12dp rounded-4; shimmer gradient sweeps left-to-right at #262A2E over #1C2024 with subtle pulse; 16dp padding.

**Component 3 - List** (full width minus 32dp): shimmer section-label bar 60dp x 12dp at #262A2E; below it one 48dp shimmer row divided into a 140dp label shard and an 80dp value shard with 16dp gutter; thin divider in #41474D.

**Component 4 - List** (full width minus 32dp): shimmer section-label bar; three consecutive 48dp shimmer rows each with 200dp label shard and 90dp value shard; represents Credit Interest skeleton; dividers #41474D.

**Component 5 - List** (full width minus 32dp): shimmer section-label bar; two 48dp shimmer rows with same shard proportions; represents Overdraft skeleton.

**Component 6 - List** (full width minus 32dp): shimmer section-label bar; three 48dp shimmer rows each with 24dp circular icon shard left and 220dp text shard; represents Features skeleton.

**Component 7 - Bottom Navigation Bar** (full width, 56dp, #1C2024 fill): four tab slots with icons and labels in #C1C7CE at 60 percent opacity; no active highlight shown during fetch.

DO NOT use an em-dash anywhere in this mockup. DO NOT render any real product name, rate figure, account number, or charge value inside shimmer rectangles. DO NOT break the dark surface theme by inserting a white or light panel. DO NOT place dark text on a dark button background or light text on a light button background.

Patient #95CDF7 skeleton while product data resolves. Mood: minimal.

↑↑↑ MOCKUP PROMPT
