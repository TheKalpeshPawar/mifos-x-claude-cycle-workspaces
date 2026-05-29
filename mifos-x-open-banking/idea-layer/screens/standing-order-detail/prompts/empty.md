---
ui_yaml_sha: a1448cadef7246768dbb0cfbf2db2a732fde45be45f4f072a644677b222e1f9f
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 1a952819884accb160c1e5f00048070f6a3e9457bb05200d869b83e39c347438

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: standing-order-detail
state: empty
state_visibility: empty

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# standing-order-detail — empty state

> Auto-generated from screens/standing-order-detail/ui.yaml @ SHA 4ffb6ddb318e1b3f
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the empty state of the standing order detail screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title "Standing Order Detail" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow 24dp tinted #B2D188. Background #12140E, zero elevation.

**Component 2 — Hero** (centered, top margin 80dp): 120dp x 120dp illustration of a circular arrows icon with a disconnected link rendered in neutral tones #44483D / #8F9285 on #12140E. Conveys "no data found" without alarm. empty_state archetype.

**Component 3 — Text** (centered, top margin 32dp, horizontal padding 48dp): "No details are available for this standing order." Outfit SemiBold 20sp #E3E3D8 centered, max 2 lines.

**Component 4 — Text** (centered, top margin 8dp, horizontal padding 48dp): "This standing order may have been cancelled or the details could not be retrieved." Outfit Regular 14sp #8F9285 centered, line-height 20sp, max 25 words.

**Component 5 — Button** (full width minus 64dp insets, top margin 32dp): Filled pill button 48dp tall, 999dp corner radius, background #B2D188, leading list icon 20dp #1F3701, label "Back to Standing Orders" Outfit SemiBold 15sp #1F3701 centered.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Centered layout with generous vertical breathing room on #12140E. The earthy green accent #B2D188 on the back button provides a clear recovery action, keeping the no-data state calm and composed within the trust-first open banking atmosphere.
↑↑↑ MOCKUP PROMPT
