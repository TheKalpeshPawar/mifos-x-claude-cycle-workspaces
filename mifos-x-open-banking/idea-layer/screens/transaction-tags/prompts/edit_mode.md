---
ui_yaml_sha: sha256:transaction-tags-ui-2026-06-02
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
content_hash: transaction-tags-edit-mode-2026-06-02

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: detail_screen

feature: transaction-tags
state: edit_mode
state_visibility: edit_mode
viewmodel: TransactionTagsViewModel

project_id: '17153754672098888646'
design_system_id: '2005644667042354169'

generated_by: /idea export
prompt_template_version: stitch-per-state-v3.0.0
generated_at: "2026-06-02"
---

# transaction-tags — edit_mode state

> Auto-generated from screens/transaction-tags/ui.yaml @ SHA 1a21ef20e69601c4
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the edit_mode state of the transaction-tags screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, background #12140E, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, error #FFB4AB, pending #E8A317.

**Component 1 — App Bar** (64dp tall, full width): Title "Edit Tags" Outfit Medium 18sp #E3E3D8 centered. Leading cancel icon 24dp #8F9285. Trailing "Done" text button Outfit Medium 14sp #B2D188. Zero elevation, background #12140E.

**Component 2 — Card** (full width minus 32dp insets, top margin 16dp, 12dp corner radius, background #1E201A): "Whole Foods Market" Outfit SemiBold 16sp #E3E3D8, "-£67.84" Outfit Bold 18sp #FFB4AB right, "23 May 2026 at 14:32" Outfit Regular 12sp #8F9285.

**Component 3 — Text** (full width minus 32dp insets, top margin 20dp): "Tags" Outfit Medium 14sp #C5C8BA. Hint "Tap a tag to remove it" Outfit Regular 12sp #8F9285 top margin 2dp.

**Component 4 — Chip Row** (full width minus 32dp insets, top margin 8dp, wrappable, 8dp gap): Five chips in edit mode. "#groceries" filled #354E16, trailing x icon. "#work-expense" outlined #44483D with delete x icon active. "#rent", "#holiday", "#gym" outlined with x icon. Each chip 32dp tall, 16dp corner radius. Outfit Medium 13sp labels.

**Component 5 — Text Field** (full width minus 32dp insets, top margin 12dp): Active focused outlined field 56dp tall, 12dp corner radius, outline 2dp #B2D188, label "Add new tag" Outfit Regular 12sp #B2D188 (floating focused), cursor blinking #B2D188. Trailing "Add" button #354E16 background #CDEDA3 label.

**Component 6 — Divider** (full width minus 32dp insets, top margin 16dp): 1dp #44483D.

**Component 7 — Text Field** (full width minus 32dp insets, top margin 12dp): Multiline outlined 80dp, label "Notes" Outfit Regular 12sp #8F9285, value "Grocery run for the week, includes meal prep." Outfit Regular 14sp #E3E3D8. Focus outline #B2D188.

**Component 8 — List Row** (full width minus 32dp insets, top margin 8dp, 56dp tall): Receipt section, same spec as content state.

**Component 9 — Button** (full width minus 32dp insets, top margin 24dp, bottom 32dp): Filled pill 48dp, background #B2D188, "Save Changes" Outfit SemiBold 16sp #1F3701.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E with active-edit emphasis. The earth-green accent #B2D188 on the focused input outline, Done action, and Save button keeps the editing context vibrant yet restrained; x icons on chips give clear, balanced affordance for tag removal.
↑↑↑ MOCKUP PROMPT
