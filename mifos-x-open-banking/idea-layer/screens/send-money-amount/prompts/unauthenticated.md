---
design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: send-money-amount
state: unauthenticated
state_visibility: unauthenticated

project_id: 'null'
design_system_id: 'null'

generated_by: idea-render-screen (LLM-local) v1.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# send-money-amount — unauthenticated state

> Auto-generated from screens/send-money-amount/ui.yaml
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT
Design the unauthenticated (session expired) state of the send money amount-entry screen for **Mifos X Open Banking**, a Open Banking KMP super-app — consumer retail banking + field officer agent banking powered by Open Bank Project API v7, built with Compose Multiplatform across Android, iOS, Desktop, and Web. The secure session timed out before the form could load.

Palette: primary #4C662B, on_primary #FFFFFF, primary_container #CDEDA3, on_primary_container #102000, background #F9FAEF, on_background #1A1C16, on_surface_variant #44483D.

**Component 1 — App Bar** (64dp tall, full width): Leading back-arrow icon 24dp #44483D, title "Send Money" Outfit SemiBold 22sp #1A1C16. Background #F9FAEF, zero elevation.

**Component 2 — Lock illustration** (centered): 96dp circle background #CDEDA3 with lock icon 48dp #102000.

**Component 3 — Headline** "Session expired" Outfit Bold 20sp #1A1C16, centered, top margin 24dp.

**Component 4 — Supporting text** "Your secure session timed out. Sign in again to continue your transfer." Outfit Regular 14sp #44483D, centered, max 320dp width, max 25 words.

**Component 5 — Primary button** (full width minus 64dp insets, max 320dp, top margin 24dp): Filled button 48dp tall, 12dp radius, background #4C662B, leading login icon 20dp, label "Sign in again" Outfit SemiBold 14sp #FFFFFF. Navigates to login.

Do not use em-dash anywhere in text. Do not break the page theme between sections. Do not place light text on light buttons. Never render an OBP login username anywhere.

Vertically centered session-expired state on #F9FAEF, calm and secure, refined for this regulated open banking context.
↑↑↑ MOCKUP PROMPT
