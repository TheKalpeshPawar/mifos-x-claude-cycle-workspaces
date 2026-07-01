---
ui_yaml_sha: 54b4dadde9c871c4dae8ce64a8dd1ffe0b3000b9f37ecda3168b3ca932573cb0
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 4f2a3891b8c70e2d1a59f6d4c2e8b053a1d7f9e6c4b2a8d0f3e1c7a9b5d2e8f

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: profile
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# profile — content state

> Auto-generated from screens/profile/ui.yaml @ SHA 3a1b7cf9e2d4f805
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the profile screen for **HSBC Open Banking**, a regulated UK Open Banking AISP where PSU Priya Sharma reviews her linked HSBC party data and active consent summary.

Archetype: detail_screen

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, surfaceContainer #1C2024, primaryContainer #004B6F, onPrimaryContainer #C9E6FF, outline #8B9198

1. **Component 1 - Top App Bar** (full width, 56dp): Title "Profile" Outfit titleMedium #E0E3E8 left-aligned on #101417; back arrow in #E0E3E8; no trailing action.

2. **Component 2 - Card** (full width minus 32dp, 88dp): Identity header on #1C2024 container 12dp radius. Leading 48dp circular avatar with initials "PS" Outfit titleMedium #95CDF7 on #004B6F fill; 4dp border-radius full. Title "Priya Sharma" Outfit titleLarge #E0E3E8 bold. Subtitle "Personal Payment Service User" bodyMedium #C1C7CE. Vertical gap 4dp between title and subtitle.

3. **Component 3 - List** (full width minus 32dp, Identity section): Section label "Identity" labelMedium #C1C7CE uppercase. Row 1: leading icon email in #C1C7CE; headline "priya.sharma@example.com" bodyLarge #E0E3E8; 56dp row height. Row 2: icon phone; headline "+44 7700 900 123" bodyLarge #E0E3E8. Row 3: icon home; headline "42 Fairfield Road, London, SW1A 1AA" bodyLarge #E0E3E8. All icons #C1C7CE; dividers #41474D.

4. **Component 4 - Card** (full width minus 32dp, HSBC Connection): Section label "HSBC Connection" labelMedium #C1C7CE uppercase above card. Card container #1C2024 12dp radius. Header row: icon account_balance in #C1C7CE; label "HSBC UK" titleMedium #E0E3E8. Status row: icon verified in #95CDF7; label "Consent status" bodyMedium #C1C7CE; trailing "Active" labelMedium #95CDF7. Expiry row: icon schedule in #C1C7CE; label "Consent expiry" bodyMedium #C1C7CE; trailing "14 Oct 2026" bodyMedium #E0E3E8. Sub-label "Permissions granted" labelSmall #C1C7CE with 8dp top margin. Four permission rows each: icon check_circle in #95CDF7; labels "Read account details", "Read balances", "Read transaction details", "Read party data" bodyMedium #E0E3E8. Tonal button "Manage consent" full width inside card; container #004B6F; label #C9E6FF; 36dp height.

5. **Component 5 - Button** (full width minus 32dp, 48dp): Outlined button "Sign out" full width; outline color #FFB4AB; label #FFB4AB; 48dp height; pill radius.

6. **Component 6 - Bottom Navigation Bar** (full width, 80dp): Four tabs Home, Accounts, Finances, Settings; Settings active icon and label #95CDF7 on #1C2024; three inactive tabs #C1C7CE.

DO NOT use an em-dash anywhere in row labels, permission names, or supporting text. DO NOT write the permissions sub-section header longer than two words or any supporting subtitle exceeding 25 words. DO NOT shift to a lighter surface inside the HSBC Connection card; all card internals remain on #1C2024 against the #101417 page background. DO NOT apply a filled dark button style to the sign-out action; the outlined #FFB4AB border on #101417 is the required treatment.

Mood: calm trust rendered through a clean dark identity card, precise consent details, and #95CDF7 permission checkmarks that tell Priya exactly what HSBC can see on her behalf.

↑↑↑ MOCKUP PROMPT
