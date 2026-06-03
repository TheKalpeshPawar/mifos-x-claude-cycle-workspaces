---
ui_yaml_sha: 7e3c1f0a9b2d4e6f
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: login-error-2026-06-02

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: form

feature: login
state: error
state_visibility: error
viewmodel: LoginViewModel

project_id: 'null'
design_system_id: 'null'

generated_by: /idea export
prompt_template_version: stitch-per-state-v3.0.0
generated_at: "2026-06-02"
---

# login — error state

> Auto-generated from screens/login/ui.yaml @ SHA 7e3c1f0a9b2d4e6f
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the Login screen for **Mifos Open Banking**, a Kotlin Multiplatform open-banking super-app for consumer retail banking and field officer agent banking. An error banner appears above the Sign In button; inputs are re-enabled for retry.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB, on_surface_variant #C5C8BA.

**Component 1 — Logo** (80dp square, centered, top margin 48dp): Mifos X mark tinted #B2D188, 16dp bottom margin.

**Component 2 — Headline** (full width minus 32dp insets, centered): "Welcome Back" Outfit SemiBold 24sp #B2D188. No subtitle below it.

**Component 3 — Username Field** (full width minus 32dp insets, top margin 24dp): Outlined Text Field 56dp tall, 4dp corner radius, outline #8F9285, background #1E201A, value "john.doe" 16sp #E3E3D8.

**Component 4 — Password Field** (full width minus 32dp insets, top margin 12dp): Outlined Text Field same style showing masked dots, trailing eye visibility-toggle icon #C5C8BA.

**Component 5 — Remember Row** (full width minus 32dp insets, top margin 8dp): Left-aligned row — checkbox tint #B2D188 plus label "Keep me signed in" Outfit Regular 14sp #E3E3D8.

**Component 6 — Error Banner** (full width minus 32dp insets, top margin 16dp): Filled card background #4A0E0C, 8dp corner radius, 16dp padding, leading alert icon #FFB4AB 20dp plus message "Invalid username or password. Please check your credentials and try again." Outfit Regular 13sp #FFB4AB.

**Component 7 — Sign In Button** (full width minus 32dp insets, top margin 16dp): Filled Button 48dp tall, 8dp corner radius, background #B2D188, label "Sign In" Outfit SemiBold 16sp #1F3701 centered, enabled for retry.

**Component 8 — OR Divider Row** (full width minus 32dp insets, top margin 24dp): Centered row — thin #282A24 line, "OR" Outfit Medium 12sp #C5C8BA with 16dp horizontal padding, thin #282A24 line.

**Component 9 — OAuth Button** (full width minus 32dp insets, top margin 24dp): Outlined Button 48dp tall, 8dp corner radius, outline #B2D188, leading open-in-browser icon, label "Sign in with OBP Account" Outfit Medium 16sp #B2D188 centered.

**Component 10 — OAuth Hint** (full width minus 32dp insets, top margin 4dp, centered): "Redirects to Open Bank Project for secure authentication" Outfit Regular 13sp #C5C8BA.

**Component 11 — Bottom Divider** (full width minus 32dp insets, top margin 16dp): Thin #282A24 line.

**Component 12 — Forgot Link** (full width minus 32dp insets, top margin 16dp, centered): "Forgot Password?" Outfit Regular 14sp #A0CFCB, 44dp tap height.

**Component 13 — Footer** (full width minus 32dp insets, top margin 8dp, bottom margin 32dp, centered): "Powered by Mifos" Outfit Bold 14sp #B2D188, weight 700.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Scrollable layout on #12140E. The #FFB4AB error tint stays restrained against the calm sage theme, while the bold footer keeps the brand grounded at the base.

↑↑↑ MOCKUP PROMPT
