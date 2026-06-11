---
design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: send-money-amount
state: empty
state_visibility: empty

project_id: 'null'
design_system_id: 'null'

generated_by: idea-render-screen (LLM-local) v1.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# send-money-amount — empty state

> Auto-generated from screens/send-money-amount/ui.yaml
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the empty state of the send money amount-entry screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web. The empty state appears when the user has no eligible account to send from.

Palette: primary #4C662B, on_primary #FFFFFF, primary_container #CDEDA3, on_primary_container #102000, background #F9FAEF, on_background #1A1C16, surface #FFFFFF, on_surface_variant #44483D, outline #75796C.

**Component 1 — App Bar** (64dp tall, full width): Leading back-arrow icon 24dp #44483D, title "Send Money" Outfit SemiBold 22sp #1A1C16. Background #F9FAEF, zero elevation.

**Component 2 — Empty illustration** (centered): 96dp circle background #CDEDA3 with account_balance_wallet icon 48dp #102000.

**Component 3 — Headline** "No accounts available to send from" Outfit Bold 20sp #1A1C16, centered, max 3 lines, top margin 24dp.

**Component 4 — Supporting text** "You don't have an eligible account on this bank to fund a transfer. Open or link an account to start sending money." Outfit Regular 14sp #44483D, centered, max 300dp width, max 25 words.

**Component 5 — Primary button** (full width minus 64dp insets, max 320dp, top margin 28dp): Filled button 48dp tall, 12dp radius, background #4C662B, leading account_balance icon 20dp, label "View my accounts" Outfit SemiBold 14sp #FFFFFF. Navigates to accounts.

**Component 6 — Secondary button** (same width, top margin 10dp): Outlined button 48dp tall, 12dp radius, 1dp #75796C, label "Back" Outfit SemiBold 14sp #4C662B. Returns to send-money.

Do not use em-dash anywhere in text. Do not make the headline more than 3 lines or the subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons.

Vertically centered empty state on #F9FAEF, calm and reassuring, refined for this regulated open banking context.
↑↑↑ MOCKUP PROMPT
