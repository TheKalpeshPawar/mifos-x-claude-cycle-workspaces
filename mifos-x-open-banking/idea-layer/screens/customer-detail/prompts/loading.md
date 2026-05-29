---
ui_yaml_sha: 446998a2d04bdffe5c3942db1e66ab81cccc8fbd49ed6f0a6c91223077a1b2ce
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: b821904910ca5da6b098bd2f1e9b9f16446c8a881013c56f1111cf3fa7d74079

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: customer-detail
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# customer-detail — loading state

> Auto-generated from screens/customer-detail/ui.yaml @ SHA 5f5e15606d09a89e
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the customer detail screen for **Mifos X Open Banking**, a professional open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, secondary #A0CFCB, error #FFB4AB, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317.

**Component 1 — App Bar Shimmer** (64dp tall, full width, background #12140E): Title shimmer 160dp wide 20dp tall centered. Shimmer base #1E201A highlight #282A24 1200ms.

**Component 2 — Hero Shimmer** (full width, background #1E201A, 24dp padding): Circle shimmer 64dp diameter centered. Two stacked rect shimmers 140dp and 100dp wide below. skeleton_screen archetype.

**Component 3 — Chip Row Shimmer** (top margin 16dp): 3 pill shimmers 90dp wide 32dp tall, 8dp gap.

**Component 4 — Card Shimmer** (full width minus 32dp insets, 160dp tall, 12dp corner radius, background #1E201A, top margin 16dp): Header shimmer 100dp wide 14dp. 4 row shimmers each 56dp tall full width, 1dp dividers #282A24.

**Component 5 — Card Shimmer** x2 (same style, 60dp tall each, top margin 8dp).

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. Shimmer base #1E201A and highlight #282A24 at 1200ms cadence keep the skeleton calm and professional, matching the measured motion dial of the trusted open banking design system.

↑↑↑ MOCKUP PROMPT
