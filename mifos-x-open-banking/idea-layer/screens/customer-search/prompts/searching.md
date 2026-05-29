---
ui_yaml_sha: 211923c9f8558a327f161786a206bf7a76aa3989313d251dec81b13885e4ee21
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 033758b6bb57441b31665a41cbdea26db6890d8f3be0d695649e6cb71656dd01

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: customer-search
state: searching
state_visibility: searching

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# customer-search — searching state

> Auto-generated from screens/customer-search/ui.yaml @ SHA d2ada055332ff9dd
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the searching state of the customer-lookup screen for **Mifos X Open Banking**, a mobile KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, error #FFB4AB, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16.

**Component 1 — App Bar** (64dp tall, full width): Title "Find Customer" Outfit Medium 18sp #E3E3D8 left 16dp. Background #12140E.

**Component 2 — Text Field** (full width minus 32dp insets, top margin 16dp): Active lookup field 48dp tall, 24dp radius, background #1E201A, focus ring 1dp #B2D188. Value "John" Outfit Regular 14sp #E3E3D8, cursor visible #B2D188. Trailing circular progress spinner 18dp #B2D188. Active retrieval state.

**Component 3 — Chip Row** (full width minus 32dp insets, top margin 12dp): "All" selected #354E16. Others outlined #44483D.

**Component 4 — List Row** (full width minus 32dp insets, top margin 16dp): 3 skeleton-shimmer card placeholders (results loading). Each 72dp tall, 12dp radius, #1E201A with shimmer sweep #282A24 1200ms. Layout matches full customer card: 40dp circle left, 3 text-line shimmers right.

**Component 5 — Button** (full width minus 32dp insets, top margin 16dp, opacity 0.4 disabled): 2 faded button shimmers 48dp, #1E201A background, labels "Onboard New Customer" / "Onboard Business Customer" Outfit Medium 14sp #8F9285.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. The lookup field focus ring and spinner both in #B2D188 signal active retrieval in a calm, purposeful way calibrated to the restrained taste-default banking aesthetic.
↑↑↑ MOCKUP PROMPT
