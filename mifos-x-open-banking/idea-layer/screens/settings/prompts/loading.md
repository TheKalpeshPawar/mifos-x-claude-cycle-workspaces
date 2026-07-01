---
ui_yaml_sha: a14204542d4a6df97e7084b25067fc3a1057dfe0f584e67c89903809f192cced
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: b8fc867648d104f35a0ee35e6eec3d4ad09948d8fadecffa38b8dc598cc58382

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: settings
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# settings — loading state

> Auto-generated from screens/settings/ui.yaml @ SHA 7a3294d5dcfd6e1b
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the settings screen for **HSBC Open Banking**, a regulated UK Open Banking AISP delivering calm, Trust Blue account-information management on Android Pixel 5.

Archetype: skeleton_screen

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, outline #8B9198

1. **Component 1 - Top App Bar** (full width, 56dp): Title "Settings" Outfit titleMedium #E0E3E8 left-aligned on #101417 container; no back arrow, no actions; root destination.

2. **Component 2 - List** (full width minus 32dp insets, shimmer skeleton): Eleven stacked shimmer blocks in two alternating heights: 14dp section-label shimmers in #262A2E and 52dp setting-row shimmers in #1C2024. Sequence top to bottom: Appearance label shimmer, Theme row shimmer; Security label shimmer, Biometric row shimmer, Session timeout row shimmer; Notifications label shimmer, Consent expiry row shimmer, Security alerts row shimmer; Account label shimmer, three account-link row shimmers; About and Legal label shimmer, four about row shimmers. All shimmers animate between #1C2024 and #262A2E with 8dp corner radius.

3. **Component 3 - Bottom Navigation Bar** (full width, 80dp): Four tabs labeled Home, Accounts, Finances, Settings; Settings tab active with icon and label in #95CDF7; three inactive tabs in #C1C7CE; container #1C2024; 48dp minimum touch target per tab.

DO NOT use an em-dash anywhere in shimmer annotations or tab labels. DO NOT render any shimmer placeholder block taller than three visual rows or annotate skeleton slots with subtitle copy exceeding 25 words. DO NOT shift the background color between sections; the entire canvas stays #101417 with shimmer blocks pulsing between #1C2024 and #262A2E throughout. DO NOT place a dark icon on a dark-filled tab or a light icon on a light-filled tab in the Bottom Navigation Bar; inactive tabs use #C1C7CE on #1C2024.

Mood: restrained patience on a near-black #101417 canvas; shimmer rows pulse in silence while the single trusted accent #95CDF7 marks the active Settings tab, orienting the user before data arrives.

↑↑↑ MOCKUP PROMPT
