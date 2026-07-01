---
ui_yaml_sha: 9d40f739969ce84dbe9266a1579a215ad4fff9695ac78689558a182d28d98b69
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: ad3b1f6c92e74a085d2c9e1b3f47a6d8e5c2b9f0a1d4e7c3b8f2a5d9e6c1b4f

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: pfm-dashboard
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# pfm-dashboard — loading state

> Auto-generated from screens/pfm-dashboard/ui.yaml @ SHA c2f4e9a17b3d0580
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the pfm-dashboard screen for **HSBC Open Banking**, a regulated UK Open Banking AISP computing Priya Sharma's personal finance overview from HSBC transaction data.

Archetype: skeleton_screen

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, outline #8B9198

1. **Component 1 - Top App Bar** (full width, 56dp): Title "Finances" Outfit titleMedium #E0E3E8 left-aligned on #101417; no back arrow; no actions; root tab screen.

2. **Component 2 - Chip Row** (full width minus 32dp, 40dp): Three shimmer chip blocks in a horizontal row, each 88dp wide 36dp tall, rounded full radius, in #262A2E animating to #1C2024; representing period-selector chips "This month", "Last 3 months", "This year" before they load.

3. **Component 3 - Card** (full width minus 32dp, 128dp): Net-worth shimmer on #1C2024 12dp radius. One wide shimmer line 200dp tall 20dp for amount; one 120dp wide 12dp tall sub-label; three 100dp wide 12dp tall breakdown rows stacked with 8dp gap. All shimmers between #1C2024 and #262A2E.

4. **Component 4 - Card** (full width minus 32dp, 180dp): Spending-income chart shimmer on #1C2024 12dp radius. Header: one 160dp shimmer line 14dp tall. Bar zone: four pairs of 40dp wide 80dp tall bar shimmers side by side with 8dp gap between pairs, heights varied to suggest income vs spend. Net cashflow shimmer: 100dp wide 12dp tall at bottom of card.

5. **Component 5 - List** (full width minus 32dp, top categories): Section label shimmer 120dp wide 10dp tall in #262A2E. Seven category row shimmers each 48dp tall: 20dp circle shimmer leading, 140dp label shimmer, 160dp progress-bar shimmer trailing in #262A2E on #1C2024 track.

6. **Component 6 - Bottom Navigation Bar** (full width, 80dp): Finances tab active icon and label #95CDF7 on #1C2024; Home, Accounts, Settings inactive #C1C7CE; 48dp touch targets.

DO NOT use an em-dash anywhere in shimmer annotations or tab labels. DO NOT render shimmer blocks taller than the content they replace or annotate skeleton slots with subtitle text exceeding 25 words. DO NOT lighten the canvas background between sections; the entire screen stays #101417 with shimmers pulsing between #1C2024 and #262A2E. DO NOT color the active Finances tab in shimmer state; keep the #95CDF7 indicator live on the nav bar so the user knows where they are.

Mood: balanced patience; slim shimmer bars and card-shaped shimmer blocks pulse on a #101417 canvas while HSBC transaction data aggregates, the lone #95CDF7 Finances tab grounding the user's context.

↑↑↑ MOCKUP PROMPT
