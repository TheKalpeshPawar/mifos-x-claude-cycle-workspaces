---
ui_yaml_sha: f162f673e5eabb53b6f5fc399cb0b97950ede9692369889ef42ab38f8db913ef
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 6e845ee40fa7f76bc049625ed018032565972d4ff7a31e1b22467b56f3aef368

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: transaction-tags
state: save_success
state_visibility: save_success

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# transaction-tags — save_success state

> Auto-generated from screens/transaction-tags/ui.yaml @ SHA c0c6c128aaa5c79b
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the save_success state of the transaction-tags screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Tag Transaction" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow 24dp #B2D188. Zero elevation, background #12140E.

**Component 2 — Card** (full width minus 32dp insets, top margin 16dp, 12dp corner radius, background #1E201A): "Whole Foods Market" Outfit SemiBold 16sp #E3E3D8, "-£67.84" Outfit Bold 18sp #FFB4AB right, "23 May 2026 at 14:32" Outfit Regular 12sp #8F9285.

**Component 3 — Text** (full width minus 32dp insets, top margin 20dp): "Tags" Outfit Medium 14sp #C5C8BA.

**Component 4 — Chip Row** (full width minus 32dp insets, top margin 8dp): Five chips showing saved tags. "#groceries" and "#work-expense" filled #354E16 label #CDEDA3. "#rent", "#holiday", "#gym" outlined #44483D. All 32dp tall, 16dp corner radius.

**Component 5 — Banner** (full width minus 32dp insets, top margin 16dp, 48dp tall, 12dp corner radius, background #354E16): Leading checkmark icon 20dp #CDEDA3. Text "Tags and notes saved" Outfit Medium 14sp #CDEDA3. Trailing success icon 20dp #B2D188.

**Component 6 — Text** (full width minus 32dp insets, top margin 12dp): "Notes" Outfit Medium 14sp #C5C8BA, value "Grocery run for the week, includes meal prep." Outfit Regular 14sp #E3E3D8 top margin 4dp.

**Component 7 — List Row** (full width minus 32dp insets, top margin 8dp, 56dp tall, background #1E201A, 12dp corner radius): "Receipt" Outfit Medium 14sp #E3E3D8, "Tap to attach a receipt image" Outfit Regular 12sp #8F9285, camera icon 24dp #B2D188 trailing.

**Component 8 — Button** (full width minus 32dp insets, top margin 24dp, bottom 32dp): Filled pill 48dp, background #B2D188, label "Done" Outfit SemiBold 16sp #1F3701 with checkmark icon 20dp #1F3701 leading.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. The earth-green accent #B2D188 on the success banner, Done button, and save icon delivers calm, balanced confirmation; the banner in #354E16 reinforces completion with a restrained, refined visual close.
↑↑↑ MOCKUP PROMPT
