# Account Detail — Visual Mockup

> Auto-generated from `screens/account-detail/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Account Detail

Canvas: 393×852dp · Top app bar with back arrow · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← HSBC Advance Current                      │  ← top_app_bar dynamic title (account Nickname)
├─────────────────────────────────────────────┤
│                                              │
│                   ◌                          │  ← loading_spinner circular #266489 centred
│               (spinning)                     │    48dp diameter
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← HSBC Advance Current                      │
├─────────────────────────────────────────────┤
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  CurrentAccount                         │ │  ← account_subtype_label labelMedium #50606E
│ │  HSBC Advance Current                   │ │  ← account_nickname headlineMedium #181C20
│ │  40-05-15 12345678                      │ │  ← account_identification bodyMedium #41474D
│ │  GBP                                    │ │  ← account_currency labelSmall #41474D
│ │  Servicer: 40-05-15                     │ │  ← account_servicer bodySmall #41474D
│ │  Last updated: 14 Jul 2026 09:15        │ │  ← account_last_updated labelSmall #41474D
│ └─────────────────────────────────────────┘ │
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  ✓ UK Open Banking – AISP regulated     │ │  ← open_banking_badge outlined card
│ └─────────────────────────────────────────┘ │    labelSmall #266489 elevation 0
│                                              │
│  Balances                                    │  ← balances_header section_header
│                                              │
│  InterimAvailable        £4,281.55 GBP      │  ← balance_row list_item
│  InterimBooked           £4,190.22 GBP      │    supporting_text = Type (bodyMedium)
│  OpeningBooked           £4,150.00 GBP      │    trailing = Amount (titleMedium #181C20)
│                                              │
│  Explore                                     │  ← actions_header section_header
│                                              │
│  ← scroll →                                 │
│  [◫ Transactions] [≡ Statements] [↻ SOs]   │  ← action_chips chip_row h-scroll
│  [📋 Direct Debits] [🗓 Scheduled] [👥 Bens] [ATM]│
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title=account.Nickname, leading back ← → accounts)
back_button/ (icon_button arrow_back always visible)
account_header_card/ (card elevation 2, padding 16dp, radius 12dp, margin h 16dp)
│  ├── account_subtype_label   (labelMedium #50606E): "CurrentAccount"
│  ├── account_nickname        (headlineMedium #181C20): "HSBC Advance Current"
│  ├── account_identification  (bodyMedium #41474D): "40-05-15 12345678"
│  ├── account_currency        (labelSmall #41474D): "GBP"
│  ├── account_servicer        (bodySmall #41474D): "Servicer: 40-05-15"
│  └── account_last_updated    (labelSmall #41474D): "Last updated: 14 Jul 2026 09:15"
open_banking_badge/ (card outlined elevation 0, margin h 16dp)
│  └── open_banking_badge_text (labelSmall #266489): "UK Open Banking – AISP regulated"
balances_header/ (section_header, padding h 16dp)
balances_list/ (list items=balances, padding h 16dp, gap 0)
│  └── balance_row × N (list_item)
│       ├── supporting_text: "InterimAvailable" / "InterimBooked" / "OpeningBooked"
│       └── trailing_content: "£4,281.55 GBP" (titleMedium #181C20)
actions_header/ (section_header, padding h 16dp)
action_chips/ (chip_row h-scroll, padding h 16dp, gap 8dp)
│  ├── chip_transactions    (chip icon receipt_long, → transactions)
│  ├── chip_statements      (chip icon description, → statements)
│  ├── chip_standing_orders (chip icon autorenew, → standing-orders)
│  ├── chip_direct_debits   (chip icon subscriptions, → direct-debits)
│  ├── chip_scheduled_payments (chip icon schedule, → scheduled-payments)
│  ├── chip_beneficiaries   (chip icon people, → beneficiaries)
│  └── chip_atm_locator     (chip icon atm, → atm-locator)
BottomNav (always)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← HSBC Advance Current                      │
├─────────────────────────────────────────────┤
│ [account_header_card — account identity shown] │
│ [open_banking_badge visible]                 │
│                                              │
│          [account_balance_wallet]            │  ← icon 48dp #41474D centred
│                                              │
│    No balances available                    │  ← title headlineSmall #181C20
│  Balance information is not available       │  ← body bodyMedium #41474D
│  for this account at this time.             │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Account Detail                            │
├─────────────────────────────────────────────┤
│                                              │
│            [error_outline]                   │  ← icon 48dp #BA1A1A
│                                              │
│    Unable to load account                   │  ← title headlineSmall #181C20
│  Your consent may have expired or been      │  ← body bodyMedium #41474D (VM-mapped)
│  revoked. Please reconnect.                 │
│                                              │
│         [  Try again  ]                     │  ← retry_button filled (recoverable only)
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| back_button / top bar back | navigate_back | accounts |
| account_header_card | (display only) | — |
| chip_transactions | navigate_transactions | transactions (accountId) |
| chip_statements | navigate_statements | statements (accountId) |
| chip_standing_orders | navigate_standing_orders | standing-orders (accountId) |
| chip_direct_debits | navigate_direct_debits | direct-debits (accountId) |
| chip_scheduled_payments | navigate_scheduled_payments | scheduled-payments (accountId) |
| chip_beneficiaries | navigate_beneficiaries | beneficiaries (accountId) |
| chip_atm_locator | navigate_atm_locator | atm-locator (accountId) |
| retry_button (error) | retry_load | in-place retry |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| account_header_card | match_parent − 32dp | wrap (~140dp) | 12dp |
| open_banking_badge | match_parent − 32dp | 36dp | 8dp |
| balance_row | match_parent | 56dp min | 0 |
| action chip (each) | wrap | 32dp | 9999 |
| loading_spinner | 48dp | 48dp | circle |
