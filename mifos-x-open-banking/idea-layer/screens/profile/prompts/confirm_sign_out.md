---
ui_yaml_sha: 54b4dadde9c871c4dae8ce64a8dd1ffe0b3000b9f37ecda3168b3ca932573cb0
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 02dc918bb32a8810722ee89b5a0efb3bf4330a40224740ed3740b3b464b5c3ad

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: profile
state: confirm_sign_out
state_visibility: confirm_sign_out

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# profile — confirm_sign_out state

> Auto-generated from screens/profile/ui.yaml @ SHA 026129182d1b55a6
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the confirm_sign_out state of the profile screen for **HSBC Open Banking**, a regulated UK Open Banking AISP showing a modal confirmation dialog after PSU Priya Sharma taps the sign-out button.

Archetype: detail_screen

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, error #FFB4AB, errorContainer #93000A, onErrorContainer #FFDAD6, scrim #000000

1. **Component 1 - Top App Bar** (full width, 56dp): Title "Profile" Outfit titleMedium dimmed under scrim; back arrow dimmed; non-interactive; background #101417 at 60 percent opacity behind scrim.

2. **Component 2 - Card** (full width minus 32dp, identity header region): "Priya Sharma" title and "Personal Payment Service User" subtitle visible but dimmed under #000000 scrim at 60 percent opacity; avatar "PS" circle visible through scrim; no interaction possible.

3. **Component 3 - Card** (full width minus 32dp, consent summary region): HSBC Connection card showing "HSBC UK", "Consent status: Active", "Consent expiry: 14 Oct 2026" visible through #000000 scrim at 60 percent opacity; four check_circle permission rows partially visible; non-interactive.

4. **Component 4 - Card** (320dp wide centered horizontally, centered vertically, dialog): Modal alert dialog floating above scrim. Container #262A2E 12dp radius; 24dp internal padding. Title "Sign out?" Outfit titleLarge #E0E3E8 bold. Body "You will be returned to the login screen. Your locally cached account data will be cleared." bodyMedium #C1C7CE two lines max. Button row right-aligned with 8dp gap: text button "Cancel" label #95CDF7 no fill; filled button "Sign out" container #93000A label #FFDAD6 pill radius 36dp height.

5. **Component 5 - Bottom Navigation Bar** (full width, 80dp): All four tabs visible under scrim at reduced opacity; Settings tab retains #95CDF7 indicator but non-interactive; container #1C2024.

DO NOT use an em-dash in the dialog title or body copy. DO NOT write the dialog body longer than two lines or exceeding 25 words. DO NOT use the same fill treatment for Cancel and Sign-out buttons; Cancel must be text-only with #95CDF7 label while Sign-out is filled #93000A with #FFDAD6 label. DO NOT show any screen region outside the dialog card at full opacity; the #000000 scrim at 60 percent must dim the entire background uniformly.

Mood: calm clarity of destructive intent; the #262A2E dialog rises above the dimmed #101417 profile with #95CDF7 on Cancel and #93000A on Sign-out, making the choice visually unambiguous without panic.

↑↑↑ MOCKUP PROMPT
