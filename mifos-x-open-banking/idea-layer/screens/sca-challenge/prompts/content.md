---
ui_yaml_sha: sha256:sca-challenge-ui-2026-06-11
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
content_hash: sca-challenge-content-2026-06-11

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form

feature: sca-challenge
state: content
state_visibility: content
viewmodel: ScaChallengeViewModel

generated_by: /idea-render-screen
prompt_template_version: stitch-per-state-v3.0.0
generated_at: "2026-06-11"
---

# sca-challenge — content state

> Auto-generated from screens/sca-challenge/ui.yaml
> Strong Customer Authentication step — an above-threshold payment returned INITIATED with a one-time-code challenge.
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the **content** state of the Confirm-Payment (SCA challenge) screen for **mifos-x-open-banking**, an Open Banking KMP super-app — consumer retail banking powered by Open Bank Project API, built with Compose Multiplatform. Material 3, 393×852dp (Pixel 5), Outfit font throughout. taste-default aesthetic, dials variance 4 / motion 3 / density 5.

Palette: primary #4C662B, on_primary #FFFFFF, primary_container #CDEDA3, on_primary_container #102000, surface #FFFFFF, on_surface #1A1C16, on_surface_variant #44483D, outline #75796C, error #BA1A1A, error_bg #FFDAD6, background #F9FAEF.

Top bar titled "Confirm Payment" with a back arrow, no bottom nav. Below it a trust-signalling shield badge (verified_user icon on a primary-container tile) anchors the page.

**Component 1 - Text (challenge_title)**: headline "Enter your authentication code", Outfit title, semibold, primary colour.

**Component 2 - Text (challenge_helper)**: supporting line "We've sent a one-time code to confirm this payment. In the sandbox, enter 123." in on_surface_variant.

**Component 3 - Input (code_input)**: single outlined numeric field, 4dp corners, centered large digits with wide letter-spacing, placeholder dots, numeric keyboard, done IME action. Empty in this state.

**Component 4 - Button (confirm_payment_button)**: full-width 52dp filled primary button "Confirm Payment", 12dp corners, pinned near the bottom. DISABLED in this state because the code field is empty (isAnswerValid = answer.isNotBlank()).

DO NOT use em-dash anywhere in text. DO NOT make any headline >3 lines or any subtitle >25 words. DO NOT break the page theme between sections. DO NOT place light text on light buttons or dark text on dark buttons.

A calm, security-forward single-column form on #F9FAEF. The #4C662B accent and shield badge create a trustworthy, banking-grade feel calibrated to the taste-default aesthetic.
↑↑↑ MOCKUP PROMPT
