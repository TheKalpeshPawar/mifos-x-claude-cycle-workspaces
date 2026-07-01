---
ui_yaml_sha: 9d40f739969ce84dbe9266a1579a215ad4fff9695ac78689558a182d28d98b69
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 3969b4c80ca7c3a9d5dff5f442d4aa53ac13ced9d4cedc108b7f4c65dd2d5241

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: pfm-dashboard
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# pfm-dashboard — empty state

> Auto-generated from screens/pfm-dashboard/ui.yaml @ SHA aab945f7fcddf2f0
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the pfm-dashboard screen for **HSBC Open Banking**, a regulated UK Open Banking AISP shown when no HSBC transaction data is yet available to compute a finance overview.

Archetype: empty_state

Palette: primary #95CDF7, surface #101417, onSurface #E0E3E8, onSurfaceVariant #C1C7CE, onPrimary #00344E, surfaceContainer #1C2024, outline #8B9198

1. **Component 1 - Top App Bar** (full width, 56dp): Title "Finances" Outfit titleMedium #E0E3E8 left-aligned on #101417; no back arrow; no actions; root tab screen.

2. **Component 2 - Chip Row** (full width minus 32dp, 40dp): Three disabled period-selector chips horizontal row 36dp height: "This month", "Last 3 months", "This year". All chips show label #8B9198 on #1C2024 container; no selected state; not interactive; outline #41474D.

3. **Component 3 - Empty State** (full width, centered vertically with generous 64dp breathing room above and below): Icon bar_chart 64dp in #C1C7CE centered. Title "No financial data yet" Outfit titleMedium #E0E3E8 centered single line. Body "Connect your HSBC account and share at least 30 days of transaction history to see your overview." bodyMedium #C1C7CE centered two lines max. Button "Set up connection" filled container #95CDF7 label #00344E Outfit labelLarge; 48dp height; pill radius; centered 24dp below body text.

4. **Component 4 - Bottom Navigation Bar** (full width, 80dp): Finances tab active icon and label #95CDF7 on #1C2024; three inactive tabs #C1C7CE; fully interactive so the user can navigate to Accounts to add a connection.

DO NOT use an em-dash in the empty-state title, body, or button label. DO NOT write the empty-state body exceeding 25 words or the title exceeding four words. DO NOT render the period-selector Chip Row as interactive or show any chip in a selected state; all chips must appear disabled with #8B9198 labels and no fill. DO NOT dim or remove the Bottom Navigation Bar; keep it fully visible and interactive so the user can navigate to the Accounts tab to set up their HSBC connection.

Mood: balanced encouragement on a wide dark #101417 canvas; a single centered Empty State with a bar_chart icon and a bold #95CDF7 call-to-action invites the first connection without applying pressure.

↑↑↑ MOCKUP PROMPT
