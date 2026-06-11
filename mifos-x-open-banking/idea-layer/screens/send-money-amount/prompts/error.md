---
design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: send-money-amount
state: error
state_visibility: error

project_id: 'null'
design_system_id: 'null'

generated_by: idea-render-screen (LLM-local) v1.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# send-money-amount — error state

> Auto-generated from screens/send-money-amount/ui.yaml
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the error state of the send money amount-entry screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web. The form failed to load.

Palette: primary #4C662B, on_primary #FFFFFF, error #BA1A1A, error_container #FFDAD6, on_error_container #410002, background #F9FAEF, on_background #1A1C16, on_surface_variant #44483D, outline #75796C.

**Component 1 — App Bar** (64dp tall, full width): Leading back-arrow icon 24dp #44483D, title "Send Money" Outfit SemiBold 22sp #1A1C16. Background #F9FAEF, zero elevation.

**Component 2 — Error illustration** (centered): 96dp circle background #FFDAD6 with cloud_off icon 48dp #BA1A1A.

**Component 3 — Headline** "Could not load payment form" Outfit Bold 20sp #1A1C16, centered, top margin 24dp.

**Component 4 — Supporting text** "Check your connection and try again" Outfit Regular 14sp #44483D, centered, max 320dp width.

**Component 5 — Primary button** (full width minus 64dp insets, max 320dp, top margin 24dp): Filled button 48dp tall, 12dp radius, background #4C662B, leading refresh icon 20dp, label "Try again" Outfit SemiBold 14sp #FFFFFF. Triggers retry.

**Component 6 — Secondary button** (same width, top margin 10dp): Outlined button 48dp tall, 12dp radius, 1dp #75796C, label "Back" Outfit SemiBold 14sp #4C662B. Returns to send-money.

Do not use em-dash anywhere in text. Do not break the page theme between sections. Do not place light text on light buttons.

Vertically centered error state on #F9FAEF, reassuring and recoverable, refined for this regulated open banking context.
↑↑↑ MOCKUP PROMPT
