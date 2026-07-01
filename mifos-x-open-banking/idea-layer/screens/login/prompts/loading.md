---
ui_yaml_sha: f3e158d2061f9b65df0967ab629f85014d9c735d2fa883594e830970abf5feda
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: e6fc23184076f3b07e1e9109d253dc75558c6d7ee4ecc9661ecf6700ddbc3a55

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: login
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# login — loading state

> Auto-generated from screens/login/ui.yaml @ SHA 55169ba4ee0f061d
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the Login screen for **HSBC Open Banking**, a UK account-information app showing skeleton placeholders while the consent request layout is being prepared.

Palette: primary #95CDF7, surface #101417, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, surfaceContainerHighest #313539, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, outline #8B9198

**Component 1 - Top App Bar** (393dp wide, 64dp tall): Shimmer rect 80dp wide 20dp tall at left (back-arrow placeholder). surfaceContainerHigh #262A2E fill with sweep. surface #101417 background.

**Component 2 - Card** (361dp wide, 148dp tall, surfaceContainerHigh #262A2E, 12dp radius): Skeleton explainer card: the skeleton_screen representation of the HSBC consent card. Three shimmer blocks: 28dp circle top-left (logo), 240dp wide 18dp tall rect (headline), 200dp wide 14dp tall rect (body). Shimmer fill surfaceContainerHighest #313539 with left-to-right sweep.

**Component 3 - Section Header** (361dp, 40dp): Single shimmer rect 160dp wide 14dp tall, 8dp radius, surfaceContainerHigh #262A2E.

**Component 4 - List** (361dp wide, 5 rows at 56dp each): Five skeleton permission rows. Each: 20dp circle shimmer blob left, 200dp wide 16dp tall shimmer rect center. Fill surfaceContainerHigh #262A2E with sweep.

**Component 5 - Stat Block** (361dp wide, 56dp): Two stacked shimmer rects: 180dp wide 14dp tall, 130dp wide 12dp tall. Represents the consent validity block.

**Component 6 - Button** (361dp wide, 48dp tall, surfaceContainerHigh #262A2E fill, 999dp radius): Shimmer placeholder for "Continue to HSBC". No label.

**Component 7 - Button** (361dp wide, 48dp tall, surfaceContainer #1C2024 fill outlined by outlineVariant #41474D, 999dp radius): Shimmer placeholder for "Cancel". No label.

DO NOT use em-dash anywhere in text. DO NOT make any headline longer than 3 lines or any subtitle longer than 25 words. DO NOT break the dark theme between sections. DO NOT place light-on-light or dark-on-dark text and button combinations.

The skeleton_screen maps every consent block to a shimmer placeholder on surface #101417 so the transition to content is seamless and balanced, with #95CDF7 deliberately absent from the loading canvas until the user's intent can be confirmed.

↑↑↑ MOCKUP PROMPT
