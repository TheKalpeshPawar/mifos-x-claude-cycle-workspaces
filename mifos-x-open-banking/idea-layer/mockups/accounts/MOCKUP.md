# Accounts — Visual Mockup

> Auto-generated from `screens/accounts/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Accounts

Canvas: 393×852dp · Top app bar · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│  Accounts                                    │  ← top_app_bar titleMedium #181C20
├─────────────────────────────────────────────┤
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← skeleton_card_1 96dp radius 12dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │    surfaceVariant #DDE3EA pulse 1.5s
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← skeleton_card_2 96dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← skeleton_card_3 96dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│  Accounts                                    │
├─────────────────────────────────────────────┤
│                                              │
│  Total balance                               │  ← total_balance_summary stat_block
│  £12,450.90                                 │  ← value headlineLarge #181C20
│  3 accounts                                  │  ← sublabel bodySmall #41474D
│                                              │
│ (All) (Current) (Savings) (Credit) (Global) │  ← account_type_filter chip_group h-scroll
│                                              │    selected chip bg #C9E6FF text #004B6F
│ ┌─────────────────────────────────────────┐ │
│ │ [account] CurrentAccount      £4,281.55 │ │  ← account_card elevation 1 radius 12dp
│ │           HSBC Advance Current          │ │    icon account_balance primary #266489
│ │           40-05-15 12345678             │ │    balance headlineSmall
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │ [savings]  Savings           £6,832.11  │ │
│ │           HSBC Regular Saver            │ │
│ │           40-05-15 87654321             │ │
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │ [credit]   CreditCard       -£1,337.24  │ │  ← balance color error #BA1A1A
│ │           HSBC Rewards CC               │ │    badge "Balance owed" tonal
│ │           40-05-15 11223344  [owed]     │ │
│ └─────────────────────────────────────────┘ │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (bg #F7F9FF, title "Accounts")
total_balance_summary/ (stat_block, padding top 12dp h 16dp)
│  ├── label:    "Total balance" (labelMedium #41474D)
│  ├── value:    "£12,450.90" (headlineLarge #181C20)
│  └── sublabel: "3 accounts" (bodySmall #41474D)
account_type_filter/ (chip_group single-select h-scroll, padding h 16dp)
│  ├── filter_all     "All"           (selected by default)
│  ├── filter_current "Current"
│  ├── filter_savings "Savings"
│  ├── filter_credit  "Credit"
│  └── filter_global  "Global"
accounts_list/ (list vertical gap 8dp padding h 16dp)
└── account_card × N (card elevation 1 padding 16dp radius 12dp)
     ├── account_type_icon  (icon lg #266489, decorative)
     ├── account_subtype    (labelSmall #50606E): "CurrentAccount"
     ├── account_nickname   (titleMedium #181C20): "HSBC Advance Current"
     ├── account_number     (bodySmall #41474D): "40-05-15 12345678"
     ├── balance_amount     (headlineSmall, normal=#181C20, credit_card=#BA1A1A)
     └── balance_type_badge (badge tonal, visible_when showBalanceBadge)
BottomNav (always)
```

---

### State: consent_expiring

Same as content with additional banner pinned to bottom:

```
┌─────────────────────────────────────────────┐
│  Accounts                                    │
├─────────────────────────────────────────────┤
│  [content as above — account cards visible]  │
│                                              │
│  ┌─ ⚠ ──────────────────────────────────┐  │  ← consent_expiry_banner
│  │  Your consent expires in 12 days      │  │    variant warning, sticky bottom
│  │  Reconfirm to keep your accounts      │  │    bg errorContainer #FFDAD6
│  │  connected.  [Reconfirm]              │  │    CTA text button → consent-detail
│  └────────────────────────────────────────┘ │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│  Accounts                                    │
├─────────────────────────────────────────────┤
│                                              │
│          [account_balance_wallet]            │  ← icon 48dp #41474D centred
│                                              │
│       No accounts found                     │  ← title headlineSmall #181C20
│  There are no accounts linked to your       │  ← body bodyMedium #41474D
│  Open Banking consent.                      │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│  Accounts                                    │
├─────────────────────────────────────────────┤
│                                              │
│           [error_outline]                    │  ← icon 48dp #BA1A1A
│                                              │
│    Unable to load accounts                  │  ← title headlineSmall #181C20
│  We couldn't retrieve your accounts.        │  ← body bodyMedium #41474D
│                                              │
│         [  Try again  ]                     │  ← retry_button filled #266489
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| filter_all / filter_current etc. | filter_accounts | in-place list filter |
| account_card | navigate_account_detail | account-detail (accountId) |
| reconfirm_button (banner) | navigate_reconfirm_consent | consent-detail (consentId) |
| retry_button (error) | retry_load | in-place retry |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| total_balance_summary | match_parent | ~64dp | 0 |
| account_card | match_parent − 32dp | 96dp | 12dp |
| filter chip (each) | wrap | 32dp | 9999 |
| consent_expiry_banner | match_parent | ~72dp | 0 |
| bottom_nav | match_parent | 80dp | 0 |
