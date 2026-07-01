---
ui_yaml_sha: f3e158d2061f9b65df0967ab629f85014d9c735d2fa883594e830970abf5feda
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 192b8dd34eb9adb1a54e842545f8e56252e3120d95b7e41b023bfc6690583f4f

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: login
state: error
state_visibility: error

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# login — error state

> Auto-generated from screens/login/ui.yaml @ SHA a4b0812550e5f4ea
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the Login screen for **HSBC Open Banking**, a UK account-information app that surfaces an OAuth failure after the HSBC consent callback returns an access-denied response.

Palette: primary #95CDF7, onPrimary #00344E, error #FFB4AB, onError #690005, errorContainer #93000A, onErrorContainer #FFDAD6, surface #101417, onSurface #E0E3E8

**Component 1 - Top App Bar** (393dp wide, 64dp tall): close icon in onSurface #E0E3E8 left. No title. surface #101417 background. Dismisses the login flow and returns the user to the previous screen.

**Component 2 - Error State** (361dp wide, centred vertically with 100dp top padding): Full-screen error_state archetype for a failed OAuth callback. error_outline icon in error #FFB4AB at 64dp, centred. Outfit 22sp "Authorisation failed" in onSurface #E0E3E8, centred, max 2 lines. Outfit 16sp "HSBC returned an error. Please try again or contact your bank if this persists." in onSurfaceVariant #C1C7CE, centred, 24dp inset.

**Component 3 - Banner** (361dp wide, 56dp, errorContainer #93000A, 8dp radius): Error detail. Outfit 13sp "Error code: ACCESS_DENIED" in onErrorContainer #FFDAD6. info_outline icon left at 20dp onErrorContainer. Helps users and support staff identify the failure class.

**Component 4 - Button** (361dp wide, 48dp tall, primary #95CDF7 fill, onPrimary #00344E label, 999dp radius): "Try again" Outfit 16sp bold. 32dp below the banner. Restarts the full consent redirect sequence.

DO NOT use em-dash anywhere in text. DO NOT make any headline longer than 3 lines or any subtitle longer than 25 words. DO NOT break the dark theme between sections. DO NOT place light-on-light or dark-on-dark text and button combinations.

The error_state archetype uses error #FFB4AB for the icon and errorContainer #93000A for the code banner while reserving #95CDF7 for the retry action, a restrained tonal hierarchy that informs without alarming on the deep surface #101417 canvas.

↑↑↑ MOCKUP PROMPT
