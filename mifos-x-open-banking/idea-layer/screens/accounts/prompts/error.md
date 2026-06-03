---
ui_yaml_sha: 32104a29c04c671ed5b57d3bf8d3f614dc3c4a3c7f3991600922913889eb8f9c
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 7d55c2368c5d6d321302bbcb6f4401a04449e7161787bab942ebe6bfd822fef8

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: accounts
state: error
state_visibility: error

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# accounts — error state

> Auto-generated from screens/accounts/ui.yaml @ SHA 7787f1d324cd8516
> Stitch DesignSystem: 2005644667042354169
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the **error** state of the My Accounts screen for **mifos-x-open-banking**, a consumer Open Banking app powered by Open Bank Project API v7 and built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: background #12140E, surface #12140E, onSurface #E3E3D8, primary #B2D188, onPrimary #1F3701, primaryContainer #354E16, onPrimaryContainer #CDEDA3, secondary #A0CFCB, surfaceContainer #1E201A, surfaceContainerHigh #282A24, error #FFB4AB, errorContainer #93000A, onErrorContainer #FFDAD6, outline #8F9285, onSurfaceVariant #C5C8BA.

**Component 1 — Top App Bar** (64dp tall, full width): Title "My Accounts" Outfit Medium 18sp #E3E3D8 start-aligned with 16dp leading inset. Trailing help icon 24dp #C5C8BA at 16dp trailing inset, 48dp tap target. Zero elevation, background #12140E. error_state archetype — no search bar, no filter tabs visible in this state.

**Component 2 — Error Illustration** (centered, top margin 72dp): 140dp wide x 140dp tall illustration of a broken bank link or disconnected cloud rendered in muted tones #44483D / #8F9285 on #12140E background. Conveys "data unavailable" without harsh alarm tones. No red fill; use error container #93000A only as a faint inner ring accent if any color accent is needed.

**Component 3 — Error Title** (centered, top margin 24dp, horizontal padding 32dp): "Could not load accounts" Outfit SemiBold 22sp #E3E3D8, text-align center, max 2 lines.

**Component 4 — Error Body** (centered, top margin 8dp, horizontal padding 40dp): "Check your connection and try again. Your account data will appear here once restored." Outfit Regular 14sp #C5C8BA, line-height 20sp, text-align center, max 3 lines.

**Component 5 — Retry Button** (full width minus 48dp horizontal insets, top margin 32dp): Filled Button 48dp tall, corner radius 12dp, background #B2D188, leading refresh icon 20dp #1F3701, label "Retry" Outfit SemiBold 16sp #1F3701. Touch target 48dp minimum.

**Component 6 — Bottom Navigation Bar** (fixed bottom, full width, 80dp tall): BottomBar background #1E201A, top border 1dp #44483D. Four nav items: Accounts (active, indicator pill background #354E16, icon + label #CDEDA3), Payments (inactive #C5C8BA), Cards (inactive #C5C8BA), More (inactive #C5C8BA). Icons 24dp, labels Outfit Regular 12sp. Active indicator 64dp x 32dp pill.

DO NOT use em-dash anywhere in text. DO NOT make any headline >3 lines or any subtitle >25 words. DO NOT break the page theme between sections. DO NOT place light text on light buttons or dark text on dark buttons.

The earth-green #B2D188 retry button anchors calm authority against the near-black #12140E surface, signaling that recovery is a single, low-friction action. The error_state archetype layout strips all account content rails, centering the illustration and message with generous top clearance so the screen communicates clearly without visual noise. Regulated-industry restraint keeps palette variance measured and motion absent, reinforcing trust even in a failure scenario.

↑↑↑ MOCKUP PROMPT
