---
ui_yaml_sha: 2f2a6c96ff6e2c74c96d19567b252075cd0b6d28aa6c9b12c9aa6a48cb3ac2e2
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: 90cfa160758ac4320b2018c46b4bd72be31595ad0227465e77d2481dede6c73c

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: empty_state

feature: accounts
state: empty
state_visibility: empty

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# accounts — empty state

> Auto-generated from screens/accounts/ui.yaml @ SHA 51dadc322fa54e53
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the empty state of the Accounts screen for **HSBC Open Banking**, a UK account-information AISP app showing consent-gated account balances.

Palette: primary #95CDF7, onPrimary #00344E, primaryContainer #004B6F, onPrimaryContainer #C9E6FF, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, outline #8B9198, onSurfaceVariant #C1C7CE, secondary #B7C9D9, inversePrimary #266489, tertiary #CFC0E8.

**Component 1 - Top App Bar** (64dp tall, full width): Title "My Accounts" Outfit Medium 18sp #E0E3E8 centered. Leading shield icon 24dp #95CDF7. Background #101417, zero elevation. This is the empty_state archetype for the Accounts screen when no accounts are included in the active Open Banking consent.

**Component 2 - Illustration Area** (centered, top margin 80dp): Account-balance-wallet icon 96dp x 96dp outline-style, 4dp stroke, color #004B6F on a 160dp diameter circle halo background #1C2024. Icon conveys "no accounts linked" without alarming visual weight.

**Component 3 - Empty Title** (centered, top margin 24dp, horizontal padding 32dp): "No accounts selected" Outfit SemiBold 22sp #E0E3E8, centered, max 2 lines.

**Component 4 - Empty Subtext** (centered, top margin 8dp, horizontal padding 40dp): "Your Open Banking consent does not include any accounts. Re-authorise to choose which accounts to share." Outfit Regular 14sp #C1C7CE, line-height 20sp, centered, max 25 words.

**Component 5 - Re-authorise Button** (full width minus 64dp insets, top margin 32dp): Filled pill Button 48dp tall, corner radius 9999dp, background #95CDF7, leading refresh-lock icon 20dp #00344E, label "Re-authorise Access" Outfit SemiBold 15sp #00344E centered.

**Component 6 - Learn More Link** (centered, top margin 16dp): Text Button "What is Open Banking consent?" Outfit Medium 13sp #8B9198, no background, no leading icon. 48dp minimum tap target height.

**Component 7 - Bottom Navigation Bar** (56dp tall, full width, pinned bottom, background #1C2024): Active "Accounts" icon and label #95CDF7 Outfit Medium 11sp. Inactive "Transactions" and "Consent" icon and label #8B9198 Outfit Regular 11sp.

DO NOT use em-dash anywhere in text. DO NOT make any headline >3 lines or any subtitle >25 words. DO NOT break the page theme between sections. DO NOT place light text on light buttons or dark text on dark buttons.

Centered layout on #101417 with generous vertical breathing room above and below the illustration. The filled #95CDF7 re-authorise button is the sole action on this empty_state, keeping the screen calm and guidance-oriented rather than punitive for a regulated Open Banking context.

↑↑↑ MOCKUP PROMPT
