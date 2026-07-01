---
ui_yaml_sha: b176ea2d469f885b24e961885ac2755e38a0e1865e6d2f063caf8d6eec8ce214
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: b0ebf52a85c9bfbe7367a8e60439f277c3d08ba80c2d57386fca604f3dcc6908

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: scheduled-payments
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# scheduled-payments — content state

> Auto-generated from screens/scheduled-payments/ui.yaml @ SHA e013eaa59ca5ac5e
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the scheduled-payments screen for **HSBC Open Banking**, a UK AISP reference app surfacing future-dated one-off payment data from OBReadScheduledPayment3 within the Trust Blue minimalist Material 3 dark system on a 393x852dp Pixel 5.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, error #FFB4AB, onSurfaceVariant #C1C7CE, outline #8B9198, primaryContainer #004B6F, secondary #B7C9D9

**Component 1 - Top App Bar** (full width, 64dp height, bg #101417): back-arrow icon 24dp #95CDF7 at left, 48dp touch target; title Outfit medium 22sp "Scheduled Payments" #E0E3E8; no elevation separator.

**Component 2 - List** (361dp wide, scrollable, 16dp horizontal padding, bg #101417): 4 stacked Cards with 8dp gap between; archetype detail_screen.

**Component 3 - Card** (361x96dp, r=12dp, bg #1C2024): Outfit medium 16sp "Lloyds Bank - Mortgage" #E0E3E8 left; monospaced 16sp "GBP 1,247.00" #FFB4AB right-aligned; Outfit regular 14sp "Executes 15 Jul 2026" #C1C7CE second row; caption 12sp "Ref: MORTP-2026-07" #8B9198; no action button.

**Component 4 - Card** (361x96dp, r=12dp, bg #1C2024): "Thames Water" #E0E3E8; monospaced "GBP 42.19" #FFB4AB right; "Executes 22 Jul 2026" #C1C7CE; caption "Ref: WATER-JUL26" #8B9198.

**Component 5 - Card** (361x96dp, r=12dp, bg #1C2024): "HMRC PAYE" #E0E3E8; monospaced "GBP 685.00" #FFB4AB right; "Executes 31 Jul 2026" #C1C7CE; caption "Ref: PAYE-Q2-2026" #8B9198.

**Component 6 - Card** (361x96dp, r=12dp, bg #1C2024): "Spotify UK Ltd" #E0E3E8; monospaced "GBP 10.99" #FFB4AB right; "Executes 01 Aug 2026" #C1C7CE; caption "Ref: SPOT-0801" #8B9198.

**Component 7 - Bottom Navigation Bar** (full width, 80dp, bg #1C2024): items "Home", "Accounts", "Payments", "More"; "Payments" filled icon and label #95CDF7; inactive tabs #C1C7CE.

Do not render any payment initiation or cancellation CTA; this screen is AISP read-only and has no write access. Do not apply green or celebratory color to amounts; all scheduled outgoing values use monospaced #FFB4AB exclusively. Do not add Card drop shadows, gradient fills, or decorative dividers; surfaces are flat on #101417 per the minimalist-ui low-motion system. Do not place identically-toned text on a same-tone button container; #00344E labels pair only with #95CDF7 containers.

Calm regulated fintech. Future payments legible at a glance. No noise, no decoration. Tone: restrained, #95CDF7 minimal.

↑↑↑ MOCKUP PROMPT
