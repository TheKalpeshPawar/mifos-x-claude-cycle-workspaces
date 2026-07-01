---
ui_yaml_sha: b176ea2d469f885b24e961885ac2755e38a0e1865e6d2f063caf8d6eec8ce214
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: de44f8f0d287dd6dabe12e07bae156a692c5913b6c142cda9980a1ab669dee60

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: scheduled-payments
state: error
state_visibility: error

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# scheduled-payments — error state

> Auto-generated from screens/scheduled-payments/ui.yaml @ SHA e7aced03ce432ada
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the scheduled-payments screen for **HSBC Open Banking**, a UK AISP reference app that failed to retrieve OBReadScheduledPayment3 data from HSBC, within the Trust Blue minimalist Material 3 dark system on a 393x852dp Pixel 5.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, error #FFB4AB, onSurfaceVariant #C1C7CE, errorContainer #93000A, onErrorContainer #FFDAD6, outline #8B9198

**Component 1 - Top App Bar** (full width, 64dp, bg #101417): back-arrow icon 24dp #95CDF7 left; title Outfit medium 22sp "Scheduled Payments" #E0E3E8.

**Component 2 - Error State** (361dp wide, vertically centered in remaining height, centered, generous vertical breathing room): error-outline icon 64dp #FFB4AB centered; Outfit medium 20sp "Could not load payments" #E0E3E8 below icon, 16dp gap; Outfit regular 14sp "We could not connect to HSBC to retrieve your scheduled payment data. Check your connection and try again." #C1C7CE centered, 2-line max; 24dp gap below body. This is the error_state archetype.

**Component 3 - Button** (200dp wide, 48dp height, r=full, bg #95CDF7, label Outfit medium 16sp "Try again" #00344E): centered horizontally below the error message.

**Component 4 - Bottom Navigation Bar** (full width, 80dp, bg #1C2024): items "Home", "Accounts", "Payments", "More"; "Payments" filled icon #95CDF7; inactive #C1C7CE.

Do not show any scheduled payment list skeleton or Card rows in the error state; only the icon, message, and Retry button are visible. Do not use the error color #FFB4AB as the Retry button container; the button is filled primary #95CDF7 with #00344E label only. Do not add a secondary navigation shortcut or support link within the error message; one Retry action only. Do not include an HTTP status code or API diagnostic string in the user-facing copy; plain English recovery text only.

Composed failure, single recovery path. Regulated fintech dignity. Tone: calm, #95CDF7 minimal.

↑↑↑ MOCKUP PROMPT
