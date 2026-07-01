---
ui_yaml_sha: 9d40f739969ce84dbe9266a1579a215ad4fff9695ac78689558a182d28d98b69
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 7d4315b1e2ac5eaced9e6747009c0ae2d286b781da71eb1bf4cb9a62215ecf00

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: error_state

feature: pfm-dashboard
state: error
state_visibility: error

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# pfm-dashboard — error state

> Auto-generated from screens/pfm-dashboard/ui.yaml @ SHA 8e4110316f6f930b
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the error state of the pfm-dashboard screen for **HSBC Open Banking**, a regulated UK Open Banking AISP shown when HSBC transaction data cannot be fetched due to a temporary upstream failure.

Archetype: error_state

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, onPrimary #00344E, surfaceContainer #1C2024, error #FFB4AB, outline #8B9198

1. **Component 1 - Top App Bar** (full width, 56dp): Title "Finances" Outfit titleMedium #E0E3E8 left-aligned on #101417; no back arrow; no actions; root tab screen.

2. **Component 2 - Chip Row** (full width minus 32dp, 40dp): Three disabled period-selector chips: "This month", "Last 3 months", "This year". All chips show label #8B9198 on #1C2024; not interactive; outline #41474D; 36dp height.

3. **Component 3 - Error State** (full width, centered vertically with generous breathing room): Icon warning_amber 48dp in #FFB4AB centered. Title "Unable to load finances" Outfit titleMedium #E0E3E8 centered single line. Body "We could not retrieve your HSBC transaction data. This may be a temporary issue." bodyMedium #C1C7CE centered two lines max. Button "Try again" filled container #95CDF7 label #00344E Outfit labelLarge; 48dp height; pill radius; centered 24dp below body.

4. **Component 4 - Bottom Navigation Bar** (full width, 80dp): Finances tab active icon and label #95CDF7 on #1C2024; Home, Accounts, Settings inactive #C1C7CE; all tabs fully interactive.

DO NOT use an em-dash in the error title, body, or button label. DO NOT write the error body exceeding 25 words or the title exceeding four words. DO NOT fill the area behind the warning_amber icon with an error-container background; use the icon outline color #FFB4AB only on the icon itself, not a filled colored card behind it. DO NOT remove the period-selector Chip Row from the layout; keep it disabled above the Error State to preserve visual parity with the content state so the user understands this is a data failure not a missing feature.

Mood: restrained composure; warning_amber #FFB4AB names the failure clearly on a dark #101417 canvas, and a centered #95CDF7 retry button redirects Priya toward resolution without adding visual alarm.

↑↑↑ MOCKUP PROMPT
