---
ui_yaml_sha: a14204542d4a6df97e7084b25067fc3a1057dfe0f584e67c89903809f192cced
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 415c945ad5eee2dadb8f3a199f446878e311b46af82f4778a75fa6e7daa8a59a

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: settings
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# settings — content state

> Auto-generated from screens/settings/ui.yaml @ SHA c307489c17e0bc70
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the settings screen for **HSBC Open Banking**, a regulated UK Open Banking AISP delivering calm, Trust Blue account-information management on Android Pixel 5.

Archetype: detail_screen

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, surfaceContainer #1C2024, primaryContainer #004B6F, onPrimaryContainer #C9E6FF, outline #8B9198

1. **Component 1 - Top App Bar** (full width, 56dp): Title "Settings" Outfit titleMedium #E0E3E8 left-aligned on #101417 container; no back arrow; no overflow menu; root screen.

2. **Component 2 - List** (full width minus 32dp, Appearance section): Section label "Appearance" labelMedium #C1C7CE uppercase. One row: leading icon contrast_rtl_off in #C1C7CE; title "Theme" bodyLarge #E0E3E8; supporting "Follows device theme" bodyMedium #C1C7CE; trailing Switch in system-default position; 56dp row height; divider #41474D below.

3. **Component 3 - List** (full width minus 32dp, Security section): Section label "Security" labelMedium #C1C7CE. Row 1: icon fingerprint #C1C7CE; title "Biometric unlock" bodyLarge #E0E3E8; supporting "Use fingerprint or face to open the app" bodyMedium #C1C7CE; trailing Switch ON thumb #95CDF7 track #004B6F; 56dp height. Row 2: icon timer #C1C7CE; title "Session timeout" bodyLarge #E0E3E8; trailing "30 minutes" #C1C7CE; chevron_right.

4. **Component 4 - List** (full width minus 32dp, Notifications section): Section label "Notifications" labelMedium #C1C7CE. Row 1: leading icon notifications_active in #C1C7CE; title "Consent expiry alerts" bodyLarge #E0E3E8; supporting "Alert 7 days before consent expires" bodyMedium #C1C7CE; trailing Switch ON (#95CDF7 thumb, #004B6F track). Row 2: leading icon security in #C1C7CE; title "Security alerts" bodyLarge #E0E3E8; supporting "Notify on new device login" bodyMedium #C1C7CE; trailing Switch ON.

5. **Component 5 - List** (full width minus 32dp, Account section): Section label "Account" labelMedium #C1C7CE. Row 1: leading icon policy in #C1C7CE; title "Manage consents" bodyLarge #E0E3E8; trailing chevron_right #8B9198. Row 2: leading icon account_circle in #C1C7CE; title "Your profile" bodyLarge #E0E3E8; trailing chevron_right #8B9198. Row 3: leading icon delete_sweep in #C1C7CE; title "Clear local data" bodyLarge #E0E3E8; trailing chevron_right #8B9198. All rows 56dp height.

6. **Component 6 - List** (full width minus 32dp, About and Legal section): Section label "About and Legal" labelMedium #C1C7CE. Row 1: icon article in #C1C7CE; title "Terms of use"; trailing chevron_right. Row 2: icon privacy_tip; title "Privacy policy"; trailing chevron_right. Row 3: icon info_outline; title "Open-source licences"; trailing chevron_right. Row 4: icon info; title "App version"; trailing text "2.4.1 (build 290)" bodyMedium #C1C7CE (no chevron). All row titles bodyLarge #E0E3E8; 56dp height.

7. **Component 7 - Bottom Navigation Bar** (full width, 80dp): Four tabs: Home, Accounts, Finances, Settings; Settings active icon and label #95CDF7 on #1C2024; three inactive tabs #C1C7CE; 48dp touch target.

DO NOT use an em-dash anywhere in row titles, supporting text, or section labels. DO NOT write any section header longer than two words or any supporting row subtitle exceeding 25 words. DO NOT introduce a lighter background color between sections; every surface stays on #101417 and section labels render on #101417 background throughout. DO NOT render a Switch with a light thumb on a light track; active Switch uses #95CDF7 thumb on #004B6F track, inactive uses #8B9198 thumb on #41474D track.

Mood: minimal calm across five grouped settings sections; Switches and the active nav tab carry #95CDF7 as the only color accent on a dark #101417 canvas, keeping every preference legible without decoration.

↑↑↑ MOCKUP PROMPT
