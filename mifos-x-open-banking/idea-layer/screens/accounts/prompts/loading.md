---
ui_yaml_sha: 2f2a6c96ff6e2c74c96d19567b252075cd0b6d28aa6c9b12c9aa6a48cb3ac2e2
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 92c231541f9ff241e9c59853669b1acf6f5b80fc585b961c14903223b0c0a5d9

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: skeleton_screen

feature: accounts
state: loading
state_visibility: loading

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# accounts — loading state

> Auto-generated from screens/accounts/ui.yaml @ SHA cf5501b18ae4bec8
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the loading state of the Accounts screen for **HSBC Open Banking**, a UK account-information AISP app showing consent-gated account balances.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, outline #8B9198, onSurfaceVariant #C1C7CE, secondary #B7C9D9, error #FFB4AB, inversePrimary #266489, surfaceBright #363A3E.

**Component 1 - Top App Bar Shimmer** (64dp tall, full width): Title-slot shimmer 120dp wide x 20dp tall, centered. Leading icon-slot shimmer 24dp circle. Background #101417, zero elevation. Shimmer base #1C2024, highlight pulse #262A2E, 1200ms horizontal sweep. This is the skeleton_screen archetype for the accounts loading experience.

**Component 2 - Stat Block Shimmer** (full width minus 32dp insets, 80dp tall, top margin 24dp, 12dp corner radius, background #1C2024): One large rectangle shimmer 200dp wide x 36dp tall representing the total-balance hero figure, with a 80dp wide x 14dp label shimmer below it. Same 1200ms sweep cadence as Component 1.

**Component 3 - Chip Row Shimmer** (full width minus 32dp insets, 32dp tall, top margin 16dp, horizontally scrollable): Five pill-shaped Chip shimmers in a row, each 64dp wide x 32dp tall, 16dp corner radius, 8dp gap. Represents the account-type filter row (All / Current / Savings / Credit / Mortgage) not yet loaded.

**Component 4 - Account Card List Shimmer** (full width minus 32dp insets, top margin 16dp): Four stacked Card shimmers, each 76dp tall, 12dp corner radius, 8dp gap, background #1C2024. Each Card row contains: left 40dp circle shimmer (account-type icon placeholder), center column with 180dp x 16dp + 120dp x 12dp text-line shimmers, right column with 80dp x 20dp amount shimmer + 48dp x 16dp badge shimmer. All shimmer base #262A2E highlight #363A3E.

**Component 5 - Bottom Navigation Bar** (56dp tall, full width, pinned bottom, background #1C2024): Three tab-slot shimmers each 80dp wide x 28dp tall, evenly distributed, representing Accounts / Transactions / Consent tabs.

DO NOT use em-dash anywhere in text. DO NOT make any headline >3 lines or any subtitle >25 words. DO NOT break the page theme between sections. DO NOT place light text on light buttons or dark text on dark buttons.

Full dark layout on #101417 with all content rails replaced by pulsing shimmer blocks. The steel-blue accent #95CDF7 remains absent during loading, preserving a calm and restrained atmosphere while the AISP data pipeline fetches consent-scoped account records.

↑↑↑ MOCKUP PROMPT
