---
ui_yaml_sha: 54b4dadde9c871c4dae8ce64a8dd1ffe0b3000b9f37ecda3168b3ca932573cb0
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 50b6b5ef08119940e6601e20cba1ec0226b218a9a2ec3612dbaac367811e5d21

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: profile
state: error
state_visibility: error

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# profile — error state

> Auto-generated from screens/profile/ui.yaml @ SHA 1b2288152da9c948
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the profile screen for **HSBC Open Banking**, a regulated UK Open Banking AISP shown when Priya Sharma's HSBC party data cannot be loaded due to a network or service error.

Archetype: error_state

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, onPrimary #00344E, surfaceContainer #1C2024, error #FFB4AB, outline #8B9198

1. **Component 1 - Top App Bar** (full width, 56dp): Title "Profile" Outfit titleMedium #E0E3E8 on #101417; back arrow in #E0E3E8; fully interactive.

2. **Component 2 - Error State** (full width, centered vertically with generous breathing room above and below): Icon cloud_off 48dp in #C1C7CE centered. Title "Could not load profile" Outfit titleMedium #E0E3E8 centered single line. Body "Check your connection and try again. Your HSBC consent remains active." bodyMedium #C1C7CE centered two lines max. Button "Try again" filled container #95CDF7 label #00344E Outfit labelLarge; 48dp height; pill radius; centered below body with 24dp top margin.

3. **Component 3 - Bottom Navigation Bar** (full width, 80dp): Four tabs Home, Accounts, Finances, Settings; Settings active icon and label #95CDF7 on #1C2024; three inactive tabs #C1C7CE; fully interactive so the user can navigate away.

DO NOT use an em-dash in the error title or body text. DO NOT write the error body exceeding 25 words or the title exceeding four words. DO NOT apply a red error-container fill or #FFB4AB color to the cloud_off icon; use neutral #C1C7CE for the icon so the state reads as informational rather than alarming. DO NOT dim or remove the Bottom Navigation Bar; keep it fully visible and interactive so Priya can navigate to other screens while the issue resolves.

Mood: restrained composure; a single centered Error State on a wide dark #101417 canvas with a clear #95CDF7 retry button signals that something went wrong without escalating the user's anxiety.

↑↑↑ MOCKUP PROMPT
