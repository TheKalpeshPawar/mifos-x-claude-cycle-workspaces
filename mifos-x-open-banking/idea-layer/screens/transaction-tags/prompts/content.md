---
ui_yaml_sha: f162f673e5eabb53b6f5fc399cb0b97950ede9692369889ef42ab38f8db913ef
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: b400bd7fa56ef83a0379809fbe8098aeea8838a859bcc776de8fc12814d1be55

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: transaction-tags
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# transaction-tags — content state

> Auto-generated from screens/transaction-tags/ui.yaml @ SHA 41df49fe6a3f821a
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the content state of the transaction-tags screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Tag Transaction" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow 24dp #B2D188. Trailing "Save" text button Outfit Medium 14sp #B2D188. Zero elevation, background #12140E.

**Component 2 — Card** (full width minus 32dp insets, top margin 16dp, 12dp corner radius, background #1E201A): Transaction header. Merchant "Whole Foods Market" Outfit SemiBold 16sp #E3E3D8 left. Amount "-£67.84" Outfit Bold 20sp #FFB4AB right. Date "23 May 2026 at 14:32" Outfit Regular 12sp #8F9285 top margin 4dp left.

**Component 3 — Text** (full width minus 32dp insets, top margin 20dp): "Tags" Outfit Medium 14sp #C5C8BA. Below: hint "Tap a tag to remove it" Outfit Regular 12sp #8F9285 top margin 2dp.

**Component 4 — Chip Row** (full width minus 32dp insets, top margin 8dp, horizontally scrollable, 8dp gap): Five filter chips 32dp tall, 16dp corner radius. "#groceries" and "#work-expense" filled #354E16, label #CDEDA3 Outfit Medium 13sp. "#rent", "#holiday", "#gym" outlined 1dp #44483D, label #C5C8BA Outfit Regular 13sp. Each chip has a trailing x icon 14dp to remove.

**Component 5 — Text Field** (full width minus 32dp insets, top margin 12dp): Outlined field 56dp tall, 12dp corner radius, label "Add tag" Outfit Regular 12sp #8F9285, focus outline #B2D188. Trailing "Add" button 36dp tall, 8dp corner radius, background #354E16, label Outfit Medium 13sp #CDEDA3.

**Component 6 — Divider** (full width minus 32dp insets, top margin 16dp): 1dp rule #44483D.

**Component 7 — Text Field** (full width minus 32dp insets, top margin 12dp): Multiline outlined field 80dp tall, 12dp corner radius, label "Notes" Outfit Regular 12sp #8F9285, placeholder "Add a note about this transaction." Outfit Regular 14sp #8F9285. Focus outline #B2D188.

**Component 8 — Divider** (full width minus 32dp insets, top margin 16dp): 1dp rule #44483D.

**Component 9 — List Row** (full width minus 32dp insets, top margin 8dp, 56dp tall): Leading receipt icon 24dp #8F9285. Center: "Receipt" Outfit Medium 14sp #E3E3D8 top, "Tap to attach a receipt image" Outfit Regular 12sp #8F9285 bottom. Trailing camera icon 24dp #B2D188.

**Component 10 — Button** (full width minus 32dp insets, top margin 24dp, bottom 32dp): Filled pill button 48dp tall, 100dp corner radius, background #B2D188, label "Save" Outfit SemiBold 16sp #1F3701.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. The earth-green accent #B2D188 on the Save button, focus rings, and camera icon keeps the layout vibrant and balanced; tag chips in #354E16 reinforce financial categorization with a calm, refined visual hierarchy.
↑↑↑ MOCKUP PROMPT
