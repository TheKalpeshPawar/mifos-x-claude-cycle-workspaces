---
ui_yaml_sha: 66c8a95765ac08cf659947bd96cf36fcad9dd366c305ca94719196dcf4ee4475
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 8f1f6fc49fa40fe155f926f4ef01e7036a1360b4de6f4a062cedb04931b86e2f

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: home
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# home — loading state

> Auto-generated from screens/home/ui.yaml @ SHA 74d6a53cff0c1f29
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the Home screen for **HSBC Open Banking**, a UK account-information app showing skeleton placeholders while account balances and recent transactions are being fetched.

Palette: primary #95CDF7, surface #101417, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, surfaceContainerHighest #313539, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, outline #8B9198

**Component 1 - Top App Bar** (393dp wide, 64dp tall): Outfit 22sp "My Accounts" in onSurface #E0E3E8. surface #101417 background. No loading indicator in the toolbar itself.

**Component 2 - Chip Row** (361dp wide, 48dp tall): Three shimmer pills each 100dp wide, 36dp tall, 18dp radius. Fill surfaceContainerHigh #262A2E with a left-to-right shimmer sweep. No labels rendered. This is the skeleton_screen chip row placeholder.

**Component 3 - Card** (361dp wide, 128dp tall, surfaceContainerHigh #262A2E, 12dp radius): Hero balance skeleton. Inside: one shimmer rect 90dp wide 14dp tall at top (account type placeholder), one shimmer rect 160dp wide 28dp tall below (balance placeholder), one shimmer rect 120dp wide 13dp tall below (available placeholder). All shimmer fills surfaceContainerHighest #313539 with sweep.

**Component 4 - Card** (361dp wide, 80dp tall, surfaceContainerHigh #262A2E, 12dp radius): Quick actions skeleton. Four circular shimmer blobs 48dp diameter evenly spaced across 361dp. Each has a shimmer rect 48dp wide 12dp tall below it. Fill surfaceContainerHighest #313539.

**Component 5 - Section Header** (361dp, 40dp): Two shimmer rects: 140dp wide 14dp tall left, 56dp wide 14dp tall right. Both 8dp radius, surfaceContainerHigh #262A2E.

**Component 6 - List** (361dp wide, 3 rows at 72dp each): Three skeleton transaction rows. Each: 40dp circular shimmer blob left, two stacked shimmer rects center (180dp wide 16dp tall, 100dp wide 12dp tall), 60dp wide 16dp tall shimmer rect right. Fill surfaceContainerHigh #262A2E, sweep animation.

**Component 7 - Card** (361dp wide, 80dp tall, surfaceContainerHigh #262A2E, 12dp radius): Spending snapshot skeleton. Two shimmer rects: 200dp wide 14dp tall, 100dp wide 20dp tall below. Fill surfaceContainerHighest #313539.

**Component 8 - Bottom Navigation Bar** (393dp wide, 80dp tall, surfaceContainer #1C2024): Four icon slots as 24dp shimmer blobs. Active slot (Home position) shows primary #95CDF7 tint to orient the user. No labels.

DO NOT use em-dash anywhere in text. DO NOT make any headline longer than 3 lines or any subtitle longer than 25 words. DO NOT break the dark theme between sections. DO NOT place light-on-light or dark-on-dark text and button combinations.

The skeleton_screen mirrors the content layout block-for-block across a surface #101417 canvas, with shimmer sweeping from surfaceContainerHigh to surfaceContainerHighest and only #95CDF7 on the active nav slot providing a restrained orientation cue during the data fetch.

↑↑↑ MOCKUP PROMPT
