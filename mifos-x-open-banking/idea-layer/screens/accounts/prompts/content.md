---
ui_yaml_sha: 2f2a6c96ff6e2c74c96d19567b252075cd0b6d28aa6c9b12c9aa6a48cb3ac2e2
design_md_hash: a3958d1ca6f307ebba64f58c9addd9531aafd615c1fa4c1b350e7b6683badd73
app_shell_hash: c60afae56a9af273fdbab8a83d90027037612b4f72cf0c6a85bc872d34e9ab76
design_read_hash: 513c061d12f3a90e84d6e98e1e037b131e59fa3ca5c5f3c0abfc6ba87d24bcaf
content_hash: c81863011cd8acb779b8725a3a9e58a373885d06007db4ec191ef34425f5d587

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 5}
aesthetic_variant_override: null
archetype: screen

feature: accounts
state: content
state_visibility: content

project_id: '5458150709735075451'
design_system_id: '8085591672064527850'

generated_by: stitch-prompt-build.ts v2.0.0
prompt_template_version: stitch-per-state-v3.0.0
craft_rules_version: v1.0.0
---

# accounts — content state

> Auto-generated from screens/accounts/ui.yaml @ SHA 70f310160b44f8c6
> Stitch DesignSystem: 8085591672064527850
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the content state of the Accounts screen for **HSBC Open Banking**, a UK account-information AISP app showing consent-gated account balances.

Palette: primary #95CDF7, onPrimary #00344E, primaryContainer #004B6F, onPrimaryContainer #C9E6FF, surface #101417, onSurface #E0E3E8, surfaceContainer #1C2024, surfaceContainerHigh #262A2E, outline #8B9198, onSurfaceVariant #C1C7CE, error #FFB4AB, secondary #B7C9D9.

**Component 1 - Top App Bar** (64dp tall, full width): Title "My Accounts" Outfit Medium 18sp #E0E3E8 centered. Leading shield icon 24dp #95CDF7. Trailing bell icon 24dp #8B9198. Background #101417, zero elevation. This detail_screen renders the full account list on the Accounts screen.

**Component 2 - Stat Block** (full width minus 32dp insets, 80dp tall, top margin 24dp, background #1C2024, 12dp corner radius): Label "Total Balance" Outfit Regular 12sp #C1C7CE uppercase. Hero value "£34,997.13" Outfit SemiBold 32sp #E0E3E8 monospaced. Sub-label "5 accounts across 2 institutions" Outfit Regular 12sp #8B9198.

**Component 3 - Chip Row** (full width minus 32dp insets, 32dp tall, top margin 16dp, horizontally scrollable): Five filter Chips. Active "All" background #95CDF7 label #00344E Outfit Medium 13sp 16dp corner radius. Inactive "Current", "Savings", "Credit", "Mortgage" outline 1dp #8B9198 background transparent label #C1C7CE Outfit Regular 13sp.

**Component 4 - Account List** (full width minus 32dp insets, top margin 16dp): Five List Cards, each 76dp tall, background #1C2024, 12dp corner radius, 8dp vertical gap. Each row left-to-right: 40dp circle #004B6F leading icon in institution accent; center column subtype Outfit Regular 12sp #8B9198 + nickname Outfit Medium 14sp #E0E3E8 + masked reference Outfit Regular 11sp #8B9198; right column balance amount Outfit SemiBold 16sp monospaced (#95CDF7 positive, #FFB4AB negative) + balance-type Badge 20dp tall 6dp corner radius background #004B6F label #C9E6FF Outfit Regular 10sp.

Account rows in order:
- Subtype "Current Account" / Nickname "HSBC Advance" / Ref "40-02-50 xxxxxx" / Amount "£2,847.63" / Badge "Available"
- Subtype "Savings" / Nickname "Regular Saver" / Ref "40-02-50 xxxxxx" / Amount "£15,200.00" / Badge "Balance"
- Subtype "Credit Card" / Nickname "HSBC Platinum" / Ref "4929 xxxx xxxx 3812" / Amount "-£1,243.50" / Badge "Outstanding"
- Subtype "Cash ISA" / Nickname "Easy ISA" / Ref "40-47-00 xxxxxx" / Amount "£8,450.00" / Badge "Balance"
- Subtype "Mortgage" / Nickname "HSBC Flexible" / Ref "Ref xxxx-0042" / Amount "£187,500.00" / Badge "Outstanding"

**Component 5 - Bottom Navigation Bar** (56dp tall, full width, pinned bottom, background #1C2024): Active tab "Accounts" icon and label #95CDF7 Outfit Medium 11sp. Inactive "Transactions" and "Consent" icon and label #8B9198 Outfit Regular 11sp.

DO NOT use em-dash anywhere in text. DO NOT make any headline >3 lines or any subtitle >25 words. DO NOT break the page theme between sections. DO NOT place light text on light buttons or dark text on dark buttons.

The steel-blue #95CDF7 on positive balances, the active tab indicator, and the shield icon creates a calm editorial hierarchy across the account list. The near-black #101417 surface keeps each balance figure and institution reference legible with minimal visual noise, appropriate for a regulated UK Open Banking screen.

↑↑↑ MOCKUP PROMPT
