---
ui_yaml_sha: 32104a29c04c671ed5b57d3bf8d3f614dc3c4a3c7f3991600922913889eb8f9c
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: dff45c06afc92c26a61292936e498c48293c6dbc38c78cc4c011eba5c44fe50a

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: accounts
state: loading
state_visibility: loading

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# accounts — loading state

> Auto-generated from screens/accounts/ui.yaml @ SHA 8b6a35515ba1b8cb
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the My Accounts screen for **mifos-x-open-banking**, a Open Banking KMP super-app for consumer and field-officer banking built with Compose Multiplatform.

Palette: background #12140E, surface #12140E, onSurface #E3E3D8, primary #B2D188, onPrimary #1F3701, primaryContainer #354E16, secondary #A0CFCB, surfaceContainer #1E201A, surfaceContainerHigh #282A24, outline #8F9285, outlineVariant #44483D, accent #4C662B.

**Component 1 — Top App Bar Shimmer** (56dp tall, full width, background #12140E): Left-aligned 120dp x 22dp shimmer for the title; 24dp x 24dp circular shimmer right-inset 16dp for the help icon. Base #1E201A, highlight #282A24, 1200ms sweep. skeleton_screen archetype.

**Component 2 — Search Bar Shimmer** (52dp tall, full width minus 32dp insets, top margin 12dp, corner radius 12dp): Single rounded-rectangle shimmer spanning the search field. Base #1E201A, highlight #282A24, 1200ms cadence. No filter tabs.

**Component 3 — Bank Group 1 Header Shimmer** (36dp tall, full width minus 32dp insets, top margin 20dp): 20dp x 20dp icon shimmer left; 140dp x 14dp name + 80dp x 12dp count stacked center (4dp gap); 64dp x 14dp subtotal shimmer right. Base #1E201A, highlight #282A24.

**Component 4 — Account Card Shimmer 1** (88dp tall, full width minus 32dp insets, top margin 8dp, corner radius 12dp, background #1E201A): Top row: 160dp x 16dp label left, 72dp x 20dp pill badge right. Middle: 100dp x 22dp balance shimmer. Bottom: 16dp x 16dp icon + 180dp x 12dp IBAN shimmer, 6dp gap.

**Component 5 — Account Card Shimmer 2** (88dp tall, top margin 8dp, same layout as Component 4): Mirrors Component 4 exactly. Base #282A24, highlight #44483D for visual separation.

**Component 6 — Bank Group 2 Header Shimmer** (36dp tall, full width minus 32dp insets, top margin 20dp): Same structure as Component 3. Base #1E201A, highlight #282A24, 1200ms sweep.

**Component 7 — Account Card Shimmer 3** (88dp tall, top margin 8dp, same layout as Component 4): Single business account card shimmer, same dimensions and tokens as Component 4.

**Component 8 — Divider Shimmer** (1dp tall, full width minus 32dp insets, top margin 16dp): Static thin bar, color #44483D, no animation.

**Component 9 — Total Balance Footer Shimmer** (52dp tall, full width minus 32dp insets, top margin 8dp, corner radius 12dp, background #1E201A): 140dp x 14dp label shimmer left, 80dp x 20dp total shimmer right, both vertically centered with 16dp padding.

**Component 10 — FAB Shimmer** (56dp x 56dp, bottom-right, 16dp inset, corner radius 16dp): Square shimmer, base #354E16, highlight #4C662B, for the add account FAB.

DO NOT use em-dash anywhere in text. DO NOT make any headline >3 lines or any subtitle >25 words. DO NOT break the page theme between sections. DO NOT place light text on light buttons or dark text on dark buttons.

Full vertically scrollable layout on #12140E background. Shimmer placeholders pulse between #1E201A and #282A24 in a calm, steady rhythm signaling data in transit. The earthy accent #B2D188 and grounding #4C662B keep the loading state composed and balanced.

↑↑↑ MOCKUP PROMPT
