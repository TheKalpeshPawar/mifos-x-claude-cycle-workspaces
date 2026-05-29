---
ui_yaml_sha: 311407aa8bae098b271a0fcb7b6d0f6b1a2c6f6f1041ffea618960562714bf2e
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: 27b8eef503d5912ac9c47f6c2af38d747a1bd1e16c4ab20ac0dd82e92e1e0c09

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: account-applications
state: empty
state_visibility: empty

project_id: 'null'
design_system_id: 'null'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# account-applications — empty state

> Auto-generated from screens/account-applications/ui.yaml @ SHA 12bf5233cfbad7f6
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the empty state of the account-applications screen for **Mifos X Open Banking**, a professional open banking KMP super-app serving consumer retail banking and field officer agent banking powered by Open Bank Project API v7.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, on_secondary #003735, secondary_container #1F4E4B, on_secondary_container #BCEBE7, tertiary #A0CFCB, on_tertiary #003735, error #FFB4AB, on_error #690005, error_container #93000A, background #12140E, on_background #E3E3D8, surface #12140E, on_surface #E3E3D8, surface_variant #44483D, on_surface_variant #C5C8BA, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, outline_variant #44483D, pending #E8A317, nav_active_indicator #354E16, scrim #000000.

**Component 1 — App Bar** (64dp tall, full width): Title "Account Applications" Outfit Medium 18sp #E3E3D8 left-aligned with 16dp leading padding. Background #12140E, zero elevation, 1dp bottom divider #44483D.

**Component 2 — Chip Row** (full width minus 32dp insets, top margin 12dp, 8dp gap, horizontally scrollable): Four filter chips 32dp tall, 16dp corner radius, all outlined 1dp #44483D. "All (0)" Outfit Regular 13sp #C5C8BA. "Pending (0)" Outfit Regular 13sp #C5C8BA. "Approved (0)" Outfit Regular 13sp #C5C8BA. "Rejected (0)" Outfit Regular 13sp #C5C8BA. empty_state archetype.

**Component 3 — Hero** (centered, top margin 80dp, horizontal padding 48dp): 112dp wide x 96dp tall illustration of an empty tray or document with a plus icon, rendered in muted tones #44483D and #8F9285. Centered on #12140E canvas.

**Component 4 — App Bar** (centered, top margin 24dp, horizontal padding 32dp): "No applications yet" Outfit SemiBold 20sp #E3E3D8 centered, max 2 lines.

**Component 5 — List Row** (centered, top margin 8dp, horizontal padding 40dp): "Submit a new account application to get started. Your applications will appear here." Outfit Regular 14sp #C5C8BA centered, line-height 20sp, max 25 words.

**Component 6 — Button** (full width minus 64dp insets, 48dp tall, 24dp corner radius, top margin 32dp): Filled button background #354E16, label "New Application" Outfit SemiBold 14sp #CDEDA3 centered.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the dark theme between sections. Do not place light text on light buttons or dark text on dark buttons.

The forest-green primary container #354E16 on the call-to-action button against deep #12140E creates an inviting empty_state that guides users toward action without urgency, keeping the layout calm and refined in character.
↑↑↑ MOCKUP PROMPT
