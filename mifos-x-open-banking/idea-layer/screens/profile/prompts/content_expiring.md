---
ui_yaml_sha: 54b4dadde9c871c4dae8ce64a8dd1ffe0b3000b9f37ecda3168b3ca932573cb0
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 56d9d205cc8ec9022e2dc9280eb2eed3dab09b08e806d512129cf635d9dd7cb0

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: profile
state: content_expiring
state_visibility: content_expiring

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# profile — content_expiring state

> Auto-generated from screens/profile/ui.yaml @ SHA 6d0835530c7f4509
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content_expiring state of the profile screen for **HSBC Open Banking**, a regulated UK Open Banking AISP alerting PSU Priya Sharma that her HSBC consent expires in 5 days and prompting renewal.

Archetype: detail_screen

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, surfaceContainer #1C2024, errorContainer #93000A, onErrorContainer #FFDAD6, error #FFB4AB, outline #8B9198

1. **Component 1 - Top App Bar** (full width, 56dp): Title "Profile" Outfit titleMedium #E0E3E8 left-aligned on #101417; back arrow in #E0E3E8.

2. **Component 2 - Card** (full width minus 32dp, 88dp): Identity header on #1C2024 12dp radius. 48dp circular avatar "PS" Outfit titleMedium #95CDF7 on #004B6F fill. Title "Priya Sharma" titleLarge #E0E3E8. Subtitle "Personal Payment Service User" bodyMedium #C1C7CE.

3. **Component 3 - List** (full width minus 32dp, Identity section): Section label "Identity" labelMedium #C1C7CE. Row 1: icon email #C1C7CE; "priya.sharma@example.com" bodyLarge #E0E3E8. Row 2: icon phone; "+44 7700 900 123". Row 3: icon home; "42 Fairfield Road, London, SW1A 1AA". All rows 56dp height, dividers #41474D.

4. **Component 4 - Banner** (full width minus 32dp, 80dp): Consent expiry warning. Container #93000A 12dp radius. Leading icon warning_amber 24dp in #FFDAD6. Body "Your HSBC consent expires in 5 days. Renew now to keep your data in sync." bodyMedium #FFDAD6 two lines max. Trailing tonal button "Renew" container #FFDAD6 label #690005 labelMedium; aligned to trailing edge 36dp height.

5. **Component 5 - Card** (full width minus 32dp, HSBC Connection section): Section label "HSBC Connection" labelMedium #C1C7CE above card. Card container #1C2024 12dp radius. Header: icon account_balance #C1C7CE; "HSBC UK" titleMedium #E0E3E8. Status row: icon schedule in #FFB4AB; label "Consent status" bodyMedium #C1C7CE; trailing "Expiring soon" labelMedium #FFB4AB. Expiry row: icon timer_off #FFB4AB; label "Consent expiry" bodyMedium #C1C7CE; trailing "5 days - 14 Oct 2026" bodyMedium #FFB4AB. Sub-label "Permissions granted" labelSmall #C1C7CE with 8dp top margin. Four permission rows icon check_circle #95CDF7: "Read account details", "Read balances", "Read transaction details", "Read party data" bodyMedium #E0E3E8. Tonal button "Manage consent" full width inside card; container #004B6F; label #C9E6FF.

6. **Component 6 - Button** (full width minus 32dp, 48dp): Outlined "Sign out" full width; outline #FFB4AB; label #FFB4AB; pill radius.

7. **Component 7 - Bottom Navigation Bar** (full width, 80dp): Settings active #95CDF7; three inactive #C1C7CE on #1C2024.

DO NOT use an em-dash in the Banner body, status row labels, or expiry trailing text. DO NOT write the Banner body exceeding 25 words or stretch it beyond two lines. DO NOT introduce green or amber accent to signal expiry; use only error-family tokens #93000A, #FFB4AB, #FFDAD6 for the warning surface and text. DO NOT render the Renew button label dark on a dark container; the button must use #690005 label on #FFDAD6 container for readable contrast.

Mood: restrained urgency without alarm; the #93000A Banner rises on the dark #101417 screen while #95CDF7 permission checkmarks confirm access still stands, nudging Priya toward renewal with calm precision.

↑↑↑ MOCKUP PROMPT
