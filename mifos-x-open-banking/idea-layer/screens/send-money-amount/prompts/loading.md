---
design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: send-money-amount
state: loading
state_visibility: loading

project_id: 'null'
design_system_id: 'null'

generated_by: idea-render-screen (LLM-local) v1.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# send-money-amount — loading state

> Auto-generated from screens/send-money-amount/ui.yaml
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the loading state of the send money amount-entry screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web.

Palette: primary #4C662B, primary_container #CDEDA3, background #F9FAEF, on_background #1A1C16, surface #FFFFFF, surface_variant #E1E4D5, on_surface_variant #44483D, outline_variant #C5C8BA.

**Component 1 — App Bar** (64dp tall, full width): Real back-arrow icon 24dp #44483D and static title "Send Money" Outfit SemiBold 22sp #1A1C16. Background #F9FAEF, zero elevation. skeleton_screen archetype below.

**Component 2 — From Account shimmer card** (full width minus 40dp insets, top margin 8dp, 12dp radius, surface #FFFFFF, 1dp #C5C8BA): 44dp rounded-square shimmer + two stacked line shimmers (30% then 70% width). Shimmer base #E1E4D5 pulsing opacity 1->0.5 at 1500ms.

**Component 3 — Amount field shimmer** (full width minus 40dp insets, top margin 18dp): Rectangular shimmer block 56dp tall, 12dp corner radius, preceded by an 80dp x 11dp label shimmer.

**Component 4 — Beneficiary search shimmer** (full width minus 40dp insets, top margin 14dp): 80dp x 11dp label shimmer then a 56dp tall, 12dp radius field shimmer.

**Component 5 — Beneficiary row shimmer** (full width minus 40dp insets, top margin 0, 12dp radius, surface #FFFFFF, 1dp #C5C8BA): 40dp circle avatar shimmer + two line shimmers (50% then 65% width).

**Component 6 — Reference field shimmer** (full width minus 40dp insets, top margin 14dp): 80dp x 11dp label shimmer then a 56dp tall field shimmer.

**Component 7 — Payment Type chip shimmer** (full width minus 40dp insets, top margin 0): 80dp x 11dp label shimmer then a row of three 88dp x 34dp chip shimmers, 8dp gap, 8dp corner radius.

**Component 8 — Fee banner shimmer** (full width minus 40dp insets, top margin 8dp): Rectangular shimmer block 48dp tall, 8dp corner radius.

**Component 9 — Continue button shimmer** (full width minus 40dp insets, top margin 8dp): Pill-ish shimmer 52dp tall, 12dp corner radius.

Do not use em-dash anywhere in text. Do not break the page theme between sections.

Full vertically scrollable layout on #F9FAEF. Shimmer placeholders use #E1E4D5 as the rest tone with a gentle opacity pulse at 1500ms, keeping the loading state calm and steady rather than flickery, calibrated to the professional open banking aesthetic.
↑↑↑ MOCKUP PROMPT
