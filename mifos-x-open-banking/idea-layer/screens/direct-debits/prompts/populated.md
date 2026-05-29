---
ui_yaml_sha: 311b028229aca9607374f911558008041fe6e2b5143fc5015fb945c2ad077cdc
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 2073095bbe1f6ba3f9b62784ea8710a63ef93bac5c7715d98cbdbe7305f4dc14

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: direct-debits
state: populated
state_visibility: populated

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# direct-debits — populated state

> Auto-generated from screens/direct-debits/ui.yaml @ SHA dda207432c396399
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the populated state of the direct-debits screen for **Mifos X Open Banking**, a Open Banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, error #FFB4AB, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title "Direct Debits" Outfit Medium 18sp #E3E3D8 left 16dp. Count badge "3 active" 28dp tall, 999dp radius, background #354E16, Outfit Medium 12sp #CDEDA3. Background #12140E.

**Component 2 — Card** (full width minus 32dp insets, top margin 20dp): Netflix card surface_container #1E201A, 12dp radius, 16dp padding. Header row: "Netflix" Outfit SemiBold 16sp #E3E3D8 left, "Active" badge 24dp tall #354E16/#CDEDA3 right. Amount row: "£15.99 / month" Outfit SemiBold 18sp #B2D188. "Next: 3 Jun 2026" Outfit Regular 13sp #C5C8BA. "Ref: DD-NF-20240301" Outfit Regular 12sp #8F9285.

**Component 3 — Card** (full width minus 32dp insets, top margin 12dp): Spotify card surface_container #1E201A, 12dp radius. "Spotify" Outfit SemiBold 16sp #E3E3D8, "Active" badge #354E16/#CDEDA3. "£10.99 / month" Outfit SemiBold 18sp #B2D188. "Next: 12 Jun 2026" #C5C8BA. "Ref: DD-SP-20231115" #8F9285.

**Component 4 — Card** (full width minus 32dp insets, top margin 12dp): PureGym card surface_container #1E201A, 12dp radius, opacity 0.6 (cancelled). "PureGym" Outfit SemiBold 16sp #E3E3D8, "Cancelled" badge outlined 1dp #44483D, Outfit Medium 12sp #8F9285. "£29.99 / month" Outfit Regular 16sp #8F9285 (muted). "Ref: DD-GYM-20220601" #8F9285.

**Component 5 — FAB** (56dp circle, bottom-right anchored, 16dp margin): Background #B2D188, plus icon 24dp #1F3701. Label "Set Up Direct Debit" Outfit Medium 14sp #1F3701 if extended FAB variant.

**Component 6 — Bottom Nav** (64dp tall, full width): 4 tabs Home, Payments (selected, indicator #354E16, icon #B2D188), Cards, Profile. Background #1E201A, top 1dp #44483D. Inactive icons #8F9285.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. The earth-green #B2D188 on active mandate amounts and the FAB signals financial control in the populated state, balanced and refined for the taste-default banking context.
↑↑↑ MOCKUP PROMPT
