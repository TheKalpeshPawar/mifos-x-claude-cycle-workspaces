---
ui_yaml_sha: f78a3dba3aff3089e2451e41f32781ab4fe14bcec47d87ec57ad572302aa3a0c
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 9c538df3792798dfc4d8c388b31b30c16c0ab06d6f53e5aea99a68c9495535e3

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: standing-orders
state: empty
state_visibility: empty

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# standing-orders — empty state

> Auto-generated from screens/standing-orders/ui.yaml @ SHA 83b8314f858f8c16
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the empty state of the standing-orders screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Standing Orders" Outfit Medium 18sp #E3E3D8 centered. Zero elevation, background #12140E.

**Component 2 — Hero** (centered, top margin 80dp): 120dp wide illustration of a calendar with a recurring arrow rendered in #44483D / #8F9285 on #12140E background, conveying "no scheduled payments yet" in neutral muted tones. empty_state archetype.

**Component 3 — Text** (centered, top margin 24dp, horizontal padding 48dp): "No Standing Orders Yet" Outfit SemiBold 20sp #E3E3D8 centered, max 2 lines.

**Component 4 — Text** (centered, top margin 8dp, horizontal padding 48dp): "Set up recurring payments for rent, subscriptions, or regular bills and they will appear here." Outfit Regular 14sp #8F9285 centered, max 25 words, line-height 20sp.

**Component 5 — Button** (full width minus 64dp insets, top margin 32dp): Filled button 48dp tall, 24dp corner radius, background #B2D188, leading plus-circle icon 20dp #1F3701, label "Create Standing Order" Outfit SemiBold 15sp #1F3701.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Centered layout on #12140E with generous vertical breathing room. The earth-green accent #B2D188 on the primary button provides clear forward momentum calibrated to the trustworthy open banking aesthetic; muted neutrals on the illustration keep the empty state calm rather than alarming.
↑↑↑ MOCKUP PROMPT
