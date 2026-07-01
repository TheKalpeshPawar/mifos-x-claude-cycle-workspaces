---
ui_yaml_sha: 54b4dadde9c871c4dae8ce64a8dd1ffe0b3000b9f37ecda3168b3ca932573cb0
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 11cf8b64ac2be0a0ee5ca3ff91a94f0b0a17d0b2eaa5d03bed5c3aba25e05e56

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: profile
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# profile — loading state

> Auto-generated from screens/profile/ui.yaml @ SHA 0cf28e2b34e2b3fd
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the profile screen for **HSBC Open Banking**, a regulated UK Open Banking AISP where PSU Priya Sharma reviews her linked HSBC party data and active consent summary.

Archetype: skeleton_screen

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, outline #8B9198

1. **Component 1 - Top App Bar** (full width, 56dp): Title "Profile" Outfit titleMedium #E0E3E8 left-aligned on #101417; back arrow icon_arrow_back in #E0E3E8; no trailing actions.

2. **Component 2 - Card** (full width minus 32dp, 96dp): Identity header shimmer on #1C2024 container with 12dp radius. Leading 48dp circular shimmer block in #262A2E representing avatar. Two horizontal shimmer lines to the right: 180dp wide 16dp tall for name; 140dp wide 12dp tall for party type. Shimmers animate between #1C2024 and #262A2E.

3. **Component 3 - List** (full width minus 32dp, Identity section): Section label shimmer 80dp wide, 10dp tall in #262A2E. Three 56dp identity field rows each showing a 24dp circular icon shimmer in #262A2E on the leading edge followed by a 200dp text shimmer block in #1C2024; icon shimmer slots for email, phone, home positions.

4. **Component 4 - Card** (full width minus 32dp, 168dp): Consent summary shimmer on #1C2024 container 12dp radius. Top row: 20dp icon circle shimmer beside 80dp bank-name shimmer. Two detail rows: status row shimmer 140dp and expiry row shimmer 160dp. Sub-label shimmer 120dp. Four permission row shimmers 200dp each with 20dp circle shimmer on leading. Button shimmer at bottom: full width inside card, 36dp tall, #262A2E fill.

5. **Component 5 - Button** (full width minus 32dp, 48dp): Single full-width shimmer block 48dp tall, full radius pill shape, #262A2E fill, representing the sign-out button.

6. **Component 6 - Bottom Navigation Bar** (full width, 80dp): Four tabs Home, Accounts, Finances, Settings; Settings active icon and label in #95CDF7; three inactive tabs in #C1C7CE; container #1C2024.

DO NOT use an em-dash anywhere in shimmer labels or tab descriptions. DO NOT render any shimmer block taller than three visual lines or annotate skeleton placeholders with subtitle copy exceeding 25 words. DO NOT break the dark surface by inserting white or light-grey regions between card shimmers; all surfaces remain on #101417 with shimmers at #1C2024 and #262A2E. DO NOT show a light shimmer pulse on a light container background; shimmer loops are constrained to the dark range #1C2024 to #262A2E.

Mood: restrained patience on a #101417 ground; shimmer pulses quietly in neutral dark tones while #95CDF7 waits on the Settings tab, ready to give way to Priya Sharma's profile the moment data arrives.

↑↑↑ MOCKUP PROMPT
