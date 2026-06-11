---
ui_yaml_sha: sha256:sca-challenge-ui-2026-06-11
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
content_hash: sca-challenge-submitting-2026-06-11

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form

feature: sca-challenge
state: submitting
state_visibility: submitting
viewmodel: ScaChallengeViewModel

generated_by: /idea-render-screen
prompt_template_version: stitch-per-state-v3.0.0
generated_at: "2026-06-11"
---

# sca-challenge — submitting state

> Auto-generated from screens/sca-challenge/ui.yaml
> isSubmitting == true — the entered code is being verified against the INITIATED request's challenge.
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the **submitting** state of the Confirm-Payment (SCA challenge) screen for **mifos-x-open-banking**, an Open Banking KMP super-app. Material 3, 393×852dp (Pixel 5), Outfit font throughout. taste-default aesthetic, dials variance 4 / motion 3 / density 5.

Palette: primary #4C662B, on_primary #FFFFFF, primary_container #CDEDA3, on_primary_container #102000, surface #FFFFFF, on_surface #1A1C16, on_surface_variant #44483D, outline #75796C, background #F9FAEF.

Same layout as the content state — back arrow disabled, "Confirm Payment" top bar, shield badge, headline, helper line — but the screen is mid-verification.

**Component 1 - Text (challenge_title)**: "Enter your authentication code" headline, unchanged.

**Component 2 - Text (challenge_helper)**: "We've sent a one-time code to confirm this payment. In the sandbox, enter 123." unchanged.

**Component 3 - Input (code_input)**: DISABLED, showing the entered code "123" in a muted on_surface_variant treatment, not editable.

**Component 4 - Button (confirm_payment_button)**: full-width 52dp filled primary button, DISABLED, with an inline circular spinner (on_primary) to the left of the label "Confirming…". A measured single-spinner motion matching the motion dial 3 — no other animation.

DO NOT use em-dash anywhere in text. DO NOT make any headline >3 lines or any subtitle >25 words. DO NOT break the page theme between sections. DO NOT place light text on light buttons or dark text on dark buttons.

A focused, reassuring in-flight moment — the form locks and a single quiet spinner signals progress on #F9FAEF, calibrated to the taste-default aesthetic.
↑↑↑ MOCKUP PROMPT
