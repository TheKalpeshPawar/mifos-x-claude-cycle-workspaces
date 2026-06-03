---
ui_yaml_sha: 7e3c1f0a9b2d4e6f
design_md_hash: 71b53c295bf863d34057f16264caf37a11512e794d356b3bec219352550d05ec
app_shell_hash: ad7a6b42b2ae10e63ef270f15d857bd44445d775e8d9b09313b31e6569df95b4
design_read_hash: 1639ea0545fdbc1ba9ce1eef5369eae224a6f4f57f07f0639b699652daeb8558
content_hash: login-oauth-redirecting-2026-06-02

design_read_aesthetic: taste-default
design_read_dials: {variance: 4, motion: 3, density: 5}
aesthetic_variant_override: null
archetype: loading

feature: login
state: oauth_redirecting
state_visibility: oauth_redirecting
viewmodel: LoginViewModel

project_id: 'null'
design_system_id: 'null'

generated_by: /idea export
prompt_template_version: stitch-per-state-v3.0.0
generated_at: "2026-06-02"
---

# login — oauth_redirecting state

> Auto-generated from screens/login/ui.yaml @ SHA 7e3c1f0a9b2d4e6f
> Stitch DesignSystem: (pending DESIGN.md upload — run /idea-export-stitch sub-plan 02)
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the oauth redirecting state of the Login screen for **Mifos Open Banking**, a Kotlin Multiplatform open-banking super-app for consumer retail banking and field officer agent banking. Full-screen takeover, vertically and horizontally centered, while the system browser opens for OAuth.

Palette: primary #B2D188, on_primary #1F3701, primary_container #354E16, on_primary_container #CDEDA3, secondary #A0CFCB, background #12140E, on_surface #E3E3D8, surface_container #1E201A, surface_container_high #282A24, outline #8F9285, error #FFB4AB, on_surface_variant #C5C8BA.

**Component 1 — Logo** (80dp square, centered, vertical center of screen): Mifos X mark tinted #B2D188, 24dp bottom margin.

**Component 2 — Title** (full width minus 32dp insets, centered): "Redirecting to Open Bank Project" Outfit SemiBold 22sp #E3E3D8.

**Component 3 — Message** (full width minus 32dp insets, top margin 8dp, centered): "Opening your browser for secure OAuth authentication" Outfit Regular 14sp #C5C8BA.

**Component 4 — Spinner** (centered, top margin 24dp): Circular indeterminate progress indicator 32dp, track #282A24, sweep #B2D188.

Do not use em-dash anywhere in text. Do not make any headline more than 3 lines or any subtitle more than 25 words. Do not break the page theme between sections. Do not place light text on light buttons or dark text on dark buttons.

Centered layout on #12140E. The sage green #B2D188 spinner keeps the browser handoff feeling calm and trustworthy.

↑↑↑ MOCKUP PROMPT
