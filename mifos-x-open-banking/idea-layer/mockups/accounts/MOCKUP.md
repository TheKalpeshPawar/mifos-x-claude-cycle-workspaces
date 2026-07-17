# Accounts — Visual Mockup

> Auto-generated from `screens/accounts/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Accounts

Canvas: 393×852dp (Pixel 5) · Top app bar (small variant, title "Accounts", bg #F7F9FF) · Bottom nav (4 tabs: Home | Accounts● | Transactions | More) · No FAB · Roboto / Roboto Mono · Material 3 light theme

---

### State: loading

Shell: Top app bar visible — title "Accounts" titleMedium 500w #181C20, bg #F7F9FF. Bottom nav visible — Accounts tab selected #266489. FAB hidden.

```
┌─────────────────────────────────────────────┐
│  Accounts                                    │  ← top_app_bar small variant, bg #F7F9FF
├─────────────────────────────────────────────┤
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← skeleton_card_1  96dp h, radius 12dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │    surfaceVariant #DDE3EA shimmer pulse 1.5s
│                                              │    stack vertical gap 8dp padding 16dp all
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← skeleton_card_2  96dp h, radius 12dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← skeleton_card_3  96dp h, radius 12dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│                                              │
│                                              │
│                                              │
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts●  ☰ Transactions  ⋯ More│  ← bottom_nav bg #F7F9FF selected #266489
└─────────────────────────────────────────────┘
```

### Component Hierarchy — loading

```
top_app_bar/ (small, bg #F7F9FF, title "Accounts" titleMedium 500w #181C20, leading auto)
loading_skeleton/ (stack vertical, gap 8dp [spacing.sm], padding 16dp all [spacing.md])
├── skeleton_card_1  (shimmer, card variant, 96dp h, radius 12dp, bg #DDE3EA, pulse 1.5s ease)
├── skeleton_card_2  (shimmer, card variant, 96dp h, radius 12dp, bg #DDE3EA)
└── skeleton_card_3  (shimmer, card variant, 96dp h, radius 12dp, bg #DDE3EA)
BottomNav/ (4 tabs: Home | Accounts● | Transactions | More; selected #266489; bg #F7F9FF; 80dp h)
```

---

### State: content

Shell: Top app bar visible — title "Accounts". Bottom nav visible — Accounts tab selected. FAB hidden. Scrollable content below app bar.

```
┌─────────────────────────────────────────────┐
│  Accounts                                    │  ← top_app_bar titleMedium 500w #181C20
├─────────────────────────────────────────────┤
│                                              │
│  Total balance                               │  ← total_balance_summary stat_block
│  £15,797.63                                  │    labelMedium 500w 12sp #41474D
│  5 accounts                                  │    headlineLarge 400w 32sp #181C20
│                                              │    bodySmall 400w 12sp #41474D
│                                              │    padding top 16dp h 16dp bottom 4dp
│ [●All] [Current] [Savings] [Credit] [Global] │  ← account_type_filter chip_group h-scroll
│                                              │    selected: bg #C9E6FF text #004B6F radius 9999
│ ┌─────────────────────────────────────────┐ │    unselected: outline #72787E text #41474D
│ │ [acct_bal]  CurrentAccount  £2,847.63   │ │  ← account_card  elev 1 radius 12dp pad 16dp
│ │             Everyday Current            │ │    icon account_balance lg #266489 decorative
│ │             40-05-15 12345678           │ │    subtype labelSmall 500w 11sp #50606E
│ └─────────────────────────────────────────┘ │    nickname titleMedium 500w 16sp #181C20
│ ┌─────────────────────────────────────────┐ │    number bodySmall 400w 12sp #41474D (Mono)
│ │ [savings]   Savings         £12,450.00  │ │    balance headlineSmall 400w 24sp #181C20
│ │             ISA Saver                   │ │
│ │             60-16-13 31926819           │ │
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │ [credit]    CreditCard       £342.18    │ │  ← balance headlineSmall #BA1A1A (error)
│ │             Platinum Mastercard [owed]  │ │    badge "Balance owed" tonal visible
│ │             xxxx xxxx xxxx 7654         │ │    badge bg #FFDAD6 text #93000A radius 9999
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │ [public]    GlobalMoney      £500.00    │ │  ← icon public lg #266489
│ │             Global Money                │ │    balance headlineSmall #181C20
│ │             GB29HBUK40051512340001      │ │
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │ [cur_exch]  GlobalWallet   USD 250.00   │ │  ← icon currency_exchange lg #266489
│ │             Global Wallet — USD         │ │    native currency code, not £ symbol
│ │             GB29HBUK40051512340002      │ │
│ └─────────────────────────────────────────┘ │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts●  ☰ Transactions  ⋯ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (small, bg #F7F9FF, title "Accounts" titleMedium 500w #181C20, leading auto)
total_balance_summary/ (stat_block, padding top 16dp h 16dp bottom 4dp)
│  ├── label:    "Total balance"   (labelMedium 500w 12sp/16sp #41474D)
│  ├── value:    "£15,797.63"      (headlineLarge 400w 32sp/40sp #181C20)
│  └── sublabel: "5 accounts"      (bodySmall 400w 12sp/16sp #41474D)
account_type_filter/ (chip_group single-select h-scroll, padding h 16dp bottom 8dp gap 8dp)
│  ├── filter_all     "All"         (selected: bg #C9E6FF text #004B6F radius 9999 h 32dp)
│  ├── filter_current "Current"     (unselected: outline #72787E text #41474D)
│  ├── filter_savings "Savings"
│  ├── filter_credit  "Credit"
│  └── filter_global  "Global"
accounts_list/ (list vertical gap 8dp, padding h 16dp, items_source filteredAccounts)
└── account_card × 5 (card elevation 1, padding 16dp, radius 12dp, bg #FFFFFF)
     └── stack horizontal alignment=center_vertical gap 16dp:
          ├── account_type_icon    (icon lg 24dp, #266489, decorative: true)
          ├── account_text_column  (stack vertical gap 4dp, weight 1)
          │    ├── account_subtype  (labelSmall 500w 11sp/16sp #50606E)
          │    ├── account_nickname (titleMedium 500w 16sp/24sp #181C20)
          │    └── account_number   (bodySmall 400w 12sp/16sp #41474D Roboto Mono)
          └── balance_column       (stack vertical alignment=end gap 2dp)
               ├── balance_amount     (headlineSmall 400w 24sp/32sp)
               │    color: #181C20 normal | #BA1A1A CreditCard+Debit
               └── balance_type_badge (badge tonal, visible_when showBalanceBadge)
                    "Balance owed" | bg #FFDAD6 | text #93000A | radius 9999
BottomNav/ (always; 80dp h; bg #F7F9FF)
```

---

### State: consent_expiring

Shell: Top app bar visible — title "Accounts". Bottom nav visible — Accounts tab selected. FAB hidden. Consent expiry banner sticky above bottom nav (14 days remaining per active consent aac-7f3b9d2e-…).

```
┌─────────────────────────────────────────────┐
│  Accounts                                    │  ← top_app_bar titleMedium #181C20
├─────────────────────────────────────────────┤
│                                              │
│  Total balance                               │  ← total_balance_summary (same as content)
│  £15,797.63                                  │
│  5 accounts                                  │
│                                              │
│ [●All] [Current] [Savings] [Credit] [Global] │  ← account_type_filter (same as content)
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← scrollable account cards (same 5)
│ │ [acct_bal]  CurrentAccount  £2,847.63   │ │
│ │             Everyday Current            │ │
│ │             40-05-15 12345678           │ │
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │ [savings]   Savings         £12,450.00  │ │
│ │             ISA Saver                   │ │
│ └─────────────────────────────────────────┘ │
│ ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐ │
│   CreditCard / GlobalMoney / GlobalWallet   │  ← below fold — scroll to reveal
│ └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘ │
│                                              │
│  ┌─ ⚠ ──────────────────────────────────┐  │  ← consent_expiry_banner
│  │  Consent expires in 14 days           │  │    variant warning, sticky bottom
│  │  Re-confirm to keep your accounts     │  │    bg #FFDAD6, border-left #BA1A1A
│  │  connected.          [Reconfirm →]    │  │    icon warning_amber 24dp #41474D
│  └────────────────────────────────────────┘ │    CTA text button "Reconfirm" #266489
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts●  ☰ Transactions  ⋯ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — consent_expiring

```
top_app_bar/ (small, bg #F7F9FF, title "Accounts" titleMedium 500w #181C20)
[All content-state children — total_balance_summary, account_type_filter, accounts_list — render identically]
consent_expiry_banner/ (banner warning, sticky bottom, above BottomNav, z-index 50)
│  ├── banner_icon      (icon warning_amber 24dp, #41474D)
│  ├── banner_title     (titleSmall 500w 14sp/20sp #181C20):
│  │   "Consent expires in 14 days"
│  ├── banner_body      (bodySmall 400w 12sp/16sp #41474D):
│  │   "Re-confirm to keep your accounts connected."
│  └── reconfirm_button (button text variant, label "Reconfirm", #266489)
│       on_click → navigate_reconfirm_consent → consent-detail
│       params: consentId = "aac-7f3b9d2e-1a4c-4f8e-b3d1-9e2a5c6f0d4b"
│       action_contract: effect=navigate
BottomNav/ (always; 80dp h)
```

---

### State: empty

Shell: Top app bar visible — title "Accounts". Bottom nav visible — Accounts tab selected. FAB hidden. Content area displays centred empty state.

```
┌─────────────────────────────────────────────┐
│  Accounts                                    │  ← top_app_bar titleMedium #181C20
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│                                              │
│       [account_balance_wallet icon]          │  ← icon 48dp colour #41474D centred
│                                              │
│          No accounts found                  │  ← title headlineSmall 400w 24sp #181C20
│                                              │    text-align: centre
│   There are no accounts linked to your      │  ← body bodyMedium 400w 14sp #41474D
│   Open Banking consent. Contact your        │    text-align: centre
│   bank or re-authorise access.              │    padding h 32dp
│                                              │
│                                              │
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts●  ☰ Transactions  ⋯ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
top_app_bar/ (small, bg #F7F9FF, title "Accounts" titleMedium 500w #181C20)
empty_accounts/ (empty_state, centred vertical + horizontal, padding h 32dp)
│  ├── icon   (account_balance_wallet, 48dp, colour #41474D, decorative: false)
│  ├── title  (headlineSmall 400w 24sp/32sp #181C20, text-align centre):
│  │   "No accounts found"
│  └── body   (bodyMedium 400w 14sp/20sp #41474D, text-align centre):
│      "There are no accounts linked to your Open Banking consent.
│       Contact your bank or re-authorise access."
BottomNav/ (always; 80dp h)
```

---

### State: error

Shell: Top app bar visible — title "Accounts". Bottom nav visible — Accounts tab selected. FAB hidden. Content area displays centred error state with primary-filled Retry CTA.

```
┌─────────────────────────────────────────────┐
│  Accounts                                    │  ← top_app_bar titleMedium #181C20
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│            [error_outline icon]              │  ← icon 48dp colour #BA1A1A centred
│                                              │
│       Unable to load accounts               │  ← title headlineSmall 400w 24sp #181C20
│                                              │    text-align: centre
│   We couldn't retrieve your accounts.       │  ← body bodyMedium 400w 14sp #41474D
│   Check your connection and try again.      │    text-align: centre, padding h 32dp
│                                              │
│           [   Try again   ]                  │  ← retry_button filled
│                                              │    bg #266489 text #FFFFFF radius 9999
│                                              │    labelLarge 500w 14sp min-touch 48dp
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts●  ☰ Transactions  ⋯ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
top_app_bar/ (small, bg #F7F9FF, title "Accounts" titleMedium 500w #181C20)
error_accounts/ (error_state, centred vertical + horizontal, padding h 32dp)
│  ├── icon          (error_outline, 48dp, colour #BA1A1A, decorative: false)
│  ├── title         (headlineSmall 400w 24sp/32sp #181C20, text-align centre):
│  │   "Unable to load accounts"
│  ├── body          (bodyMedium 400w 14sp/20sp #41474D, text-align centre):
│  │   "We couldn't retrieve your accounts. Check your connection and try again."
│  └── retry_button  (button filled, label "Try again", bg #266489, text #FFFFFF,
│       radius 9999, padding h 24dp, min-touch 48dp)
│       on_click → retry_load
│       action_contract: effect=call_api
│       external_library_refs: [ktorfit, hsbc-obie-ais-v4.0:accounts,
│         hsbc-obie-ais-v4.0:balances]
│       description: "Re-triggers parallel fetch: GET /accounts → OBReadAccount6,
│         then GET /accounts/{AccountId}/balances per account via
│         coroutineScope async/awaitAll to rebuild AccountWithBalance rows."
BottomNav/ (always; 80dp h)
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| filter_all chip | filter_accounts (subtype: null) | client-side list filter — no API round-trip |
| filter_current chip | filter_accounts (subtype: CurrentAccount) | client-side list filter — no API round-trip |
| filter_savings chip | filter_accounts (subtype: Savings) | client-side list filter — no API round-trip |
| filter_credit chip | filter_accounts (subtype: CreditCard) | client-side list filter — no API round-trip |
| filter_global chip | filter_accounts (subtype: GlobalMoney,GlobalWallet) | client-side list filter — no API round-trip |
| account_card (any of 5) | navigate_account_detail (accountId: item.AccountId) | account-detail screen — effect: navigate |
| reconfirm_button (consent_expiring banner) | navigate_reconfirm_consent (consentId: activeConsentId) | consent-detail screen — effect: navigate |
| retry_button (error state) | retry_load | call_api — GET /accounts + GET /accounts/{AccountId}/balances via ktorfit |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| top_app_bar | match_parent | 64dp | 0 |
| total_balance_summary (stat_block) | match_parent | ~68dp | 0 |
| account_type_filter row | match_parent (scrollable) | 32dp chip height | 0 (row) |
| filter chip (each) | wrap_content + 12dp h padding | 32dp | 9999 (full pill) |
| accounts_list container | match_parent | fill_remaining | 0 |
| account_card | match_parent − 32dp | 96dp | 12dp |
| account_type_icon | 24dp | 24dp | 0 |
| balance_type_badge ("Balance owed") | wrap_content | 20dp | 9999 |
| consent_expiry_banner | match_parent | ~72dp | 0 |
| empty_accounts / error_accounts | match_parent | fill_remaining | 0 |
| retry_button (filled) | wrap_content (min 120dp) | 48dp | 9999 |
| bottom_nav | match_parent | 80dp | 0 |
