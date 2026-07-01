---
ui_yaml_sha: 2f2a6c96ff6e2c74c96d19567b252075cd0b6d28aa6c9b12c9aa6a48cb3ac2e2
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: cedc6d14b745fb8d1479c75ab6f1144c3bf977a7d83e3e12dbc9d387ac40cabf

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: accounts
state: consent_expiring
state_visibility: consent_expiring

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# accounts — consent_expiring state

> Auto-generated from screens/accounts/ui.yaml @ SHA a104c57bdc8ea46e
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the consent_expiring state of the Accounts screen for **HSBC Open Banking**, a UK account-information AISP app showing consent-gated account balances.

Palette: primary #95CDF7, onPrimary #00344E, primaryContainer #004B6F, onPrimaryContainer #C9E6FF, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, outline #8B9198, onSurfaceVariant #C1C7CE, error #FFB4AB, errorContainer #93000A, onErrorContainer #FFDAD6, secondary #B7C9D9.

**Component 1 - Top App Bar** (64dp tall, full width): Title "My Accounts" Outfit Medium 18sp #E0E3E8 centered. Leading shield icon 24dp #95CDF7. Trailing bell icon with 8dp amber dot badge 24dp #8B9198. Background #101417, zero elevation. This detail_screen variant renders the full Accounts screen with a consent warning.

**Component 2 - Consent Expiry Banner** (full width, 64dp tall, background #93000A, sticky below app bar, no corner radius): Leading warning-amber icon 20dp #FFDAD6 with 16dp left padding. Body text "Consent expires in 3 days" Outfit Medium 14sp #FFDAD6 with 12dp left margin. Trailing text Button "Reconfirm" Outfit SemiBold 13sp #FFB4AB with 16dp right padding. This is the screen's primary urgency indicator.

**Component 3 - Stat Block** (full width minus 32dp insets, 80dp tall, top margin 16dp, background #1C2024, 12dp corner radius): Label "Total Balance" Outfit Regular 12sp #C1C7CE. Value "£34,997.13" Outfit SemiBold 32sp #E0E3E8 monospaced. Sub-label "Consent valid until 4 Jul 2026, 5 accounts" Outfit Regular 12sp #8B9198.

**Component 4 - Chip Row** (full width minus 32dp insets, 32dp tall, top margin 16dp, horizontally scrollable): Five filter Chips. Active "All" background #95CDF7 label #00344E Outfit Medium 13sp. Inactive "Current", "Savings", "Credit", "Mortgage" outline 1dp #8B9198 label #C1C7CE Outfit Regular 13sp.

**Component 5 - Account List** (full width minus 32dp insets, top margin 16dp): Five List Cards, each 76dp tall, background #1C2024, 12dp corner radius, 8dp gap. Left 40dp circle icon background #004B6F; center subtype Outfit Regular 12sp #8B9198 + nickname Outfit Medium 14sp #E0E3E8 + masked ref Outfit Regular 11sp #8B9198; right balance #95CDF7 (positive) or #FFB4AB (negative) Outfit SemiBold 16sp monospaced + badge #004B6F label #C9E6FF.

Account rows:
- "Current Account" / "HSBC Advance" / "40-02-50 xxxxxx" / "£2,847.63" badge "Available"
- "Savings" / "Regular Saver" / "40-02-50 xxxxxx" / "£15,200.00" badge "Balance"
- "Credit Card" / "HSBC Platinum" / "4929 xxxx xxxx 3812" / "-£1,243.50" badge "Outstanding"
- "Cash ISA" / "Easy ISA" / "40-47-00 xxxxxx" / "£8,450.00" badge "Balance"
- "Mortgage" / "HSBC Flexible" / "Ref xxxx-0042" / "£187,500.00" badge "Outstanding"

**Component 6 - Bottom Navigation Bar** (56dp tall, full width, pinned bottom, background #1C2024): Active "Accounts" icon and label #95CDF7 Outfit Medium 11sp. Inactive "Transactions" and "Consent" icon and label #8B9198 Outfit Regular 11sp.

DO NOT use em-dash anywhere in text. DO NOT make any headline >3 lines or any subtitle >25 words. DO NOT break the page theme between sections. DO NOT place light text on light buttons or dark text on dark buttons.

The errorContainer #93000A Banner delivers urgency without dismantling the dark surface. The accent #95CDF7 persists on positive balances and the active tab, keeping this consent_expiring screen restrained and trust-forward even as the expiry deadline demands the customer's attention.

↑↑↑ MOCKUP PROMPT
