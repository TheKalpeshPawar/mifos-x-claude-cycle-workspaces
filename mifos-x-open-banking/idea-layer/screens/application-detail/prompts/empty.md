---
ui_yaml_sha: 64d1e77304b15bebcf5570a91036dd5267b8a38e827f5a966cb61dd278263d6b
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: e630babdd69496a3324710d77582815a9ca7c4ee8853b54c265c2e16963e3aef

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: application-detail
state: empty
state_visibility: empty

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# application-detail — empty state

> Auto-generated from screens/application-detail/ui.yaml @ SHA 4d882e627dd54d96
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the empty state of the application-detail screen for **Mifos X Open Banking**, a professional open banking KMP super-app serving consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, tertiary #A0CFCB, on_tertiary #003735, error #FFB4AB, on_error #690005, error_container #93000A, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16, scrim #000000.

**Component 1 — App Bar** (64dp tall, full width): Leading back-arrow 24dp #B2D188. Title "Application Detail" Outfit Medium 18sp #E3E3D8 centered. Background #12140E, 1dp bottom divider #44483D.

**Component 2 — Hero** (centered, top margin 80dp, horizontal padding 48dp): 96dp wide x 96dp tall illustration of an empty document or folder, rendered in muted #44483D and #8F9285. empty_state archetype centered on #12140E.

**Component 3 — App Bar** (centered, top margin 24dp, horizontal padding 32dp): "No application data" Outfit SemiBold 20sp #E3E3D8 centered, max 2 lines.

**Component 4 — List Row** (centered, top margin 8dp, horizontal padding 40dp): "Select an application from the list to view its details here." Outfit Regular 14sp #C5C8BA centered, line-height 20sp, max 25 words.

**Component 5 — Button** (full width minus 64dp insets, 48dp tall, 24dp corner radius, top margin 32dp): Filled button background #354E16, label "Browse Applications" Outfit SemiBold 14sp #CDEDA3 centered.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The forest-green #354E16 call-to-action on deep #12140E guides field officers back to the application list, keeping the empty_state purposeful and calm in a regulated banking workflow.
↑↑↑ MOCKUP PROMPT
