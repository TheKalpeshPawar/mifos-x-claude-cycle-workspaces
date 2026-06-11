---
ui_yaml_sha: sha256:sca-challenge-ui-2026-06-11
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
content_hash: sca-challenge-error-2026-06-11

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form

feature: sca-challenge
state: error
state_visibility: error
viewmodel: ScaChallengeViewModel

generated_by: /idea-render-screen
prompt_template_version: stitch-per-state-v3.0.0
generated_at: "2026-06-11"
---

# sca-challenge — error state

> Auto-generated from screens/sca-challenge/ui.yaml
> errorMessage != null — the answered challenge was rejected; the field is re-enabled for retry.
> Messages map from OBP codes 40014 / 40011 / 40009 / 30279, else a generic retry message.
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the **error** state of the Confirm-Payment (SCA challenge) screen for **mifos-x-open-banking**, an Open Banking KMP super-app. Material 3, 393×852dp (Pixel 5), Outfit font throughout. taste-default aesthetic, dials variance 4 / motion 3 / density 5.

Palette: primary #4C662B, on_primary #FFFFFF, primary_container #CDEDA3, surface #FFFFFF, on_surface #1A1C16, on_surface_variant #44483D, outline #75796C, error #BA1A1A, error_bg #FFDAD6, on_error_bg #410002, background #F9FAEF.

Same layout as content — back arrow, "Confirm Payment" top bar, shield badge, headline, helper line — with an error surface added.

**Component 1 - Text (challenge_title)**: "Enter your authentication code" headline, unchanged.

**Component 2 - Text (challenge_helper)**: "We've sent a one-time code to confirm this payment. In the sandbox, enter 123." unchanged.

**Component 3 - Box (challenge_error)**: a soft error surface on error_bg #FFDAD6 with on_error_bg text, 8dp corners, 16dp padding, an error_outline icon, placed directly above the code field. Message "That code wasn't accepted. Please check it and try again." role=alert.

**Component 4 - Input (code_input)**: outlined field flagged isError with an error-coloured border, showing a rejected value, still editable for retry.

**Component 5 - Button (confirm_payment_button)**: full-width 52dp filled primary button "Confirm Payment", RE-ENABLED so the user can try again.

DO NOT use em-dash anywhere in text. DO NOT make any headline >3 lines or any subtitle >25 words. DO NOT break the page theme between sections. DO NOT place light text on light buttons or dark text on dark buttons.

A clear, non-alarming recovery moment — a tonal error surface and an error-bordered field guide the retry on #F9FAEF, calibrated to the taste-default aesthetic.
↑↑↑ MOCKUP PROMPT
