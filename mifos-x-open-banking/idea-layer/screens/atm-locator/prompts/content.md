---
ui_yaml_sha: c8c8040af254236430df923e229edc7208f4a0e351a42c63baa151d487b8456e
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 76855f7765aa148d33085782c0024982190eab3757c80ec28983b2f7dc447fb6

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: atm-locator
state: content
state_visibility: content

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# atm-locator — content state

> Auto-generated from screens/atm-locator/ui.yaml @ SHA 51591fb6bce3f31e
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the content state of the ATM Locator screen for **Mifos X Open Banking**, a open banking KMP super-app for consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, background #12140E, on_surface #E3E3D8, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB.

**Component 1 — App Bar** (64dp tall, full width): Title "ATM & Branches" Outfit Medium 18sp #E3E3D8 centered. Leading back-arrow icon 24dp tinted #B2D188. Zero elevation, background #12140E.

**Component 2 — Text Field** (full width minus 32dp insets, top margin 16dp): Outlined lookup field 56dp tall, 12dp corner radius, label "Find location" Outfit Regular 14sp #8F9285, leading find icon 20dp #C5C8BA, outline 1dp #44483D.

**Component 3 — Card** (full width minus 32dp insets, top margin 12dp): surfaceContainer #1E201A background, 12dp corner radius, 16dp padding. Leading location-dot icon 20dp #B2D188. Label "Use my location for nearby ATMs" Outfit Regular 14sp #C5C8BA. Trailing "Enable" text button Outfit Medium 14sp #B2D188.

**Component 4 — Chip Row** (full width minus 32dp insets, top margin 16dp, horizontally scrollable): Four filter chips, 32dp tall, 16dp corner radius, 8dp gap. "All" chip filled #354E16 with label Outfit Medium 13sp #CDEDA3. "ATMs", "Branches", "24/7" chips outlined 1dp #44483D Outfit Regular 13sp #C5C8BA.

**Component 5 — List Row** (full width minus 32dp insets, top margin 8dp): Section header "3 ATMs found within 500m" Outfit SemiBold 13sp #8F9285 uppercase, top margin 16dp.

**Component 6 — Card** (full width minus 32dp insets, top margin 8dp): surfaceContainerHigh #282A24 background, 12dp corner radius, 16dp padding. Title "Mifos ATM - Oxford Street" Outfit SemiBold 16sp #E3E3D8. Row: "0.2km away" Outfit Regular 13sp #C5C8BA, "Open 24/7" Outfit Regular 13sp #B2D188, "300 GBP max withdrawal" Outfit Regular 13sp #C5C8BA. Footer "Get Directions" Outfit Medium 14sp #B2D188 with arrow-right 16dp.

**Component 7 — Card** (full width minus 32dp insets, top margin 8dp): Same shape as Component 6. Title "Mifos ATM - Bond Street Station" Outfit SemiBold 16sp #E3E3D8. Row: "0.5km away" Outfit Regular 13sp #C5C8BA, "Open 24/7" Outfit Regular 13sp #B2D188. Footer "Get Directions" Outfit Medium 14sp #B2D188.

**Component 8 — Card** (full width minus 32dp insets, top margin 8dp, bottom 24dp): surfaceContainerHigh #282A24 background, 12dp corner radius, 16dp padding. Branch icon 20dp #A0CFCB top-right badge. Title "Mifos Branch - Mayfair" Outfit SemiBold 16sp #E3E3D8. Row: "0.8km away" Outfit Regular 13sp #C5C8BA, "Mon-Fri 9am-5pm" Outfit Regular 13sp #C5C8BA. Tags row: "Cashier", "FX", "Safe Deposit" outlined chips 8dp radius Outfit Regular 12sp #C5C8BA. Footer "Get Directions" Outfit Medium 14sp #B2D188.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Full scrollable layout on #12140E. The earth-green accent #B2D188 on selected chip, direction links, and open-status labels creates a calm, balanced financial feel that stays minimal and refined throughout.
↑↑↑ MOCKUP PROMPT
