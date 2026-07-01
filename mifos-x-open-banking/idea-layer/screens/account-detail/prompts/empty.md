---
ui_yaml_sha: 0120895d6ee57bd035a4abe15da76e75865b30a5f02a3bb1e89215c380a564a0
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 385855009bfe210b04aa5ab3a8b3567bc5d9e266061a1f5a46da9b26067da487

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: account-detail
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# account-detail — empty state

> Auto-generated from screens/account-detail/ui.yaml @ SHA 61ad60b8afb4640e
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the account-detail screen for **HSBC Open Banking**, a UK AISP app that shows when no balance data has been returned for the selected HSBC account.

Palette: primary #95CDF7, onPrimary #00344E, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, secondary #B7C9D9, error #FFB4AB, outline #8B9198

Archetype: empty_state

**Component 1 - Top App Bar** (56dp h, full 393dp w): Outfit 22sp "HSBC Current Account" #E0E3E8 on #101417; leading arrow-back icon 24dp #E0E3E8; no trailing controls.

**Component 2 - Card** (full width minus 32dp, 12dp radius, bg #1C2024): title "HSBC Advance Current Account" Outfit 600 18sp #E0E3E8; supporting "Sort code: 40-05-15, Acc no: 12345678" Outfit 400 14sp #B7C9D9; meta "GBP · HSBC UK BANK PLC" Outfit 12sp #8B9198; 16dp padding.

**Component 3 - Banner** (full width minus 32dp, 8dp radius, bg #004B6F): shield icon 16dp #95CDF7 inline-left; "Read-only Open Banking access. Your money cannot be moved." Outfit 13sp #C9E6FF; 12dp vertical padding.

**Component 4 - Empty State** (centered, generous vertical space, bg #101417): account-balance-wallet icon 64dp #41474D; title "No balance data available" Outfit 600 20sp #E0E3E8; body "HSBC has not returned balance records for this account. Consent may be limited or the account type may not support balance queries." Outfit 400 14sp #B7C9D9; Button "View Transactions" 48dp full-width bg #95CDF7 label #00344E Outfit 600 14sp; 24dp spacing between elements.

**Component 5 - Chip Row** (horizontal scroll, 16dp start, section label "Explore" Outfit 600 16sp #E0E3E8): six assist chips bg #1C2024 stroke #41474D label #E0E3E8; labels: "Transactions", "Statements", "Standing Orders", "Direct Debits", "Scheduled", "Beneficiaries".

**Component 6 - Bottom Navigation Bar** (56dp h, bg #1C2024, full width): "Accounts" active icon account-balance #95CDF7 label #95CDF7; "PFM", "Consents", "Profile" each icon and label #8B9198.

DO NOT use an em-dash in any label or body copy. DO NOT make the headline longer than three lines or any body copy subtitle longer than 25 words. DO NOT render a light-themed section break within the dark-surface screen. DO NOT place a dark text label on a dark-coloured button where contrast is insufficient for WCAG AA compliance.

Mood: restrained and minimal empty state; #95CDF7 on the single call-to-action Button is the only warm touch in an otherwise quiet, data-absent HSBC account surface.

↑↑↑ MOCKUP PROMPT
