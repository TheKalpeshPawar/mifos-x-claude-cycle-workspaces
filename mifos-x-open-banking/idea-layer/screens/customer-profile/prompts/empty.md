---
ui_yaml_sha: ed2405e9b0ab40e84eddfcb7e669dd5d6df03b6a59f4997cb41c63dd2313c905
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 6f5beb1b10ed445f4bf1fadd157dea2dd360ce2e20e6d0f2fd38522fd80776b5

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: customer-profile
state: empty
state_visibility: empty

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# customer-profile — empty state

> Auto-generated from screens/customer-profile/ui.yaml @ SHA 67d6be8f241ef2d8
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the empty state of the customer-profile screen for **Mifos X Open Banking**, a professional open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, error #FFB4AB, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title "Customer Profile" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow 24dp #B2D188. Background #12140E, zero elevation.

**Component 2 — Hero** (centered, top margin 96dp): Illustrated empty-state graphic 160dp x 160dp, person-silhouette outline rendered in #44483D on #12140E background. empty_state archetype centered layout with generous vertical breathing room.

**Component 3 — App Bar** (centered, top margin 24dp, horizontal padding 48dp): Title text "No profile data yet" Outfit SemiBold 22sp #E3E3D8, centered, max 1 line.

**Component 4 — List Row** (centered, top margin 8dp, horizontal padding 48dp): Subtext "Complete your profile to access all banking services and verify your identity." Outfit Regular 14sp #8F9285, line-height 20sp, centered, max 3 lines.

**Component 5 — Button** (full width minus 64dp insets, top margin 40dp): Filled pill button 48dp tall, 999dp corner radius, background #B2D188, label "Complete Profile" Outfit SemiBold 15sp #1F3701 centered.

**Component 6 — Bottom Nav** (64dp tall, full width, anchored bottom): 4 tabs Home, Payments, **Profile** (selected, indicator #354E16, icon #B2D188), Settings. Background #1E201A, top 1dp #44483D. Inactive icons #8F9285.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Centered layout on #12140E with generous vertical breathing room. Anchored by #B2D188 on the primary action, the composition stays calm and balanced, conveying that completing this step is safe and positive.
↑↑↑ MOCKUP PROMPT
