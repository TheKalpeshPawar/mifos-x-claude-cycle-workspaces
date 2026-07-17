# Transactions — Visual Mockup

> Auto-generated from `screens/transactions/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Transactions

Canvas: 393×852dp (Pixel 5) · Top app bar (back arrow, title "Transactions") · Bottom nav (Transactions tab selected) · Roboto font · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Transactions                              │  ← top_app_bar small; back_arrow leading
├─────────────────────────────────────────────┤  │  title "Transactions" titleLarge #181C20
│                                              │
│                                              │
│                                              │
│                  ◌                           │  ← loading_spinner; M3 CircularProgressIndicator
│            (animating)                       │    colour #266489 (primary); 48dp; centred
│                                              │    full-screen — no other content visible
│                                              │
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│ ⌂ Home  ◫ Accounts  ☰ Transactions  ⋯ More  │  ← bottom_nav; Transactions icon receipt_long
└─────────────────────────────────────────────┘    selected tint #266489; unselected #41474D
```

### Component Hierarchy — loading

```
top_app_bar/ (small variant; leading icon back_arrow #181C20; title "Transactions" titleLarge #181C20)
loading_spinner/ (CircularProgressIndicator; colour primary #266489; modifier fillMaxSize; wrapContentSize Center)
BottomNav/ (items: Home icon home · Accounts icon account_balance · Transactions icon receipt_long ★ · More icon more_horiz)
         (selected indicator colour #266489; unselected #41474D; bg #F7F9FF)
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← Transactions                              │  ← top_app_bar small; back_arrow
├─────────────────────────────────────────────┤
│                                              │
│  Money in             Money out             │  ← period_summary stat_block
│  +£2,400.00           −£1,394.04            │    two-column; h 56dp; padding h 16dp v 8dp
│  [#266489 titleMedium] [#BA1A1A titleMedium]│    credit label bodySmall #41474D
│                       divider outlineVariant│    debit  label bodySmall #41474D
│                                              │
│  ┌──────────────────────────────────────────┐│  ← filter_chips chip_row h-scroll
│  │● All  ↓ Money in  ↑ Money out  📅 Date  ││    gap 8dp; padding h 16dp; no clip
│  └──────────────────────────────────────────┘│    filter_all: filled bg #266489 label #FFFFFF
│                                              │    others: outlined border #72787E label #41474D
│  ┌──────────────────────────────────────────┐│  ← search_field text_field
│  │ 🔍  Search transactions              ✕  ││    leading icon search #41474D
│  └──────────────────────────────────────────┘│    trailing icon clear #41474D (visible on input)
│                                              │    radius 28dp; h 48dp; bg #EBEEF3
│  28 Jun 2026                                 │  ← date_group_header; labelSmall #41474D
│  ┌──────────────────────────────────────┐   │    sticky; h 24dp; padding h 16dp
│  │ ↑  NETFLIX.COM              -£10.99  │   │  ← transaction_row; arrow_upward Debit icon
│  │    [Subscriptions]                   │   │    amount titleMedium #BA1A1A
│  └──────────────────────────────────────┘   │    radius 8dp; elev 0; padding v 12dp h 16dp
│  ┌──────────────────────────────────────┐   │
│  │ ↑  COSTA COFFEE 1847 LONDON   -£3.65 │   │  ← Dining category chip; assist style
│  │    [Dining]                          │   │    chip bg #EBEEF3; label labelSmall #41474D
│  └──────────────────────────────────────┘   │
│  ┌──────────────────────────────────────┐   │  ← Pending row (Status=Pending)
│  │ ↑  SPOTIFY AB               -£11.99  │   │    tx_pending_badge warning tonal
│  │    [Subscriptions]  [⚠ Pending]      │   │    badge bg #FFDAD6 label #93000A labelSmall
│  └──────────────────────────────────────┘   │
│                                              │
│  27 Jun 2026                                 │
│  ┌──────────────────────────────────────┐   │
│  │ ↑  PRET A MANGER 083 LONDON   -£8.45 │   │
│  │    [Dining]                          │   │
│  └──────────────────────────────────────┘   │
│  ┌──────────────────────────────────────┐   │
│  │ ↑  AMAZON UK MARKETPLACE     -£31.99 │   │
│  │    [Shopping]                        │   │
│  └──────────────────────────────────────┘   │
│                                              │
│  25 Jun 2026                                 │
│  ┌──────────────────────────────────────┐   │
│  │ ↓  SALARY ACME LTD        +£2,400.00 │   │  ← Credit; arrow_downward icon; #266489
│  │    [Income]                          │   │    amount titleMedium primary #266489
│  └──────────────────────────────────────┘   │
│                                              │
│  ··· (24 Jun: BRITISH GAS -£78.00 Bills)    │  ← below fold; 2 more date groups in list
│  ··· (23 Jun: JAMESON LETTINGS -£1,200.00)  │
│                                              │
│         [  Load more transactions  ]         │  ← load_more_button text variant
│                                              │    visible_when has_next_page && !is_paginating
│ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─   │  ← pagination_loader linear #266489
│    (linear progress — visible while paging) │    visible_when is_paginating=true
├─────────────────────────────────────────────┤
│ ⌂ Home  ◫ Accounts  ☰ Transactions  ⋯ More  │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (small; back_arrow leading #181C20; title "Transactions" titleLarge #181C20; bg #F7F9FF)
period_summary/ (stat_block; Row; padding h 16dp v 8dp; h 56dp; divider outlineVariant #C1C7CE)
│  ├── total_credit/ (Column weight 1)
│  │    ├── label  "Money in"   (bodySmall #41474D)
│  │    └── value  "+£2,400.00" (titleMedium #266489 Roboto Mono)
│  └── total_debit/  (Column weight 1)
│       ├── label  "Money out"   (bodySmall #41474D)
│       └── value  "−£1,394.04" (titleMedium #BA1A1A Roboto Mono)
filter_chips/ (chip_row LazyRow h-scroll; padding h 16dp; gap 8dp; no wrap)
│  ├── filter_all        "All" (FilterChip filled; bg #266489 label #FFFFFF; selected=true)
│  ├── filter_money_in   "Money in"  (FilterChip outlined; icon arrow_downward 18dp)
│  ├── filter_money_out  "Money out" (FilterChip outlined; icon arrow_upward 18dp)
│  └── filter_date_range "Date range"(FilterChip outlined; icon date_range 18dp)
search_field/ (OutlinedTextField; shape RoundedCornerShape 28dp; h 48dp; padding h 16dp)
│    leadingIcon: search 20dp #41474D; trailingIcon: clear 20dp #41474D (visible when input)
│    placeholder: "Search transactions" (bodyMedium #41474D); bg #EBEEF3
transactions_list/ (LazyColumn; padding h 16dp; contentPadding bottom 16dp; grouped by LocalDate)
│  ├── [GROUP] 28 Jun 2026
│  │    ├── date_group_header "28 Jun 2026" (labelSmall #41474D; stickyHeader; h 24dp)
│  │    ├── transaction_row: NETFLIX.COM
│  │    │    ├── leading  icon arrow_upward 24dp (Debit; tint #BA1A1A bg errorContainer #FFDAD6 r 9999)
│  │    │    ├── tx_merchant   "NETFLIX.COM"       (bodyMedium #181C20; maxLines 1 ellipsis)
│  │    │    ├── tx_category_tag [Subscriptions]   (AssistChip; labelSmall; bg #EBEEF3 #41474D)
│  │    │    └── trailing       "−£10.99"          (titleMedium #BA1A1A Roboto Mono)
│  │    ├── transaction_row: COSTA COFFEE 1847 LONDON
│  │    │    ├── leading  icon arrow_upward (Debit)
│  │    │    ├── tx_merchant   "COSTA COFFEE 1847 LONDON" (bodyMedium #181C20)
│  │    │    ├── tx_category_tag [Dining]
│  │    │    └── trailing       "−£3.65" (titleMedium #BA1A1A)
│  │    └── transaction_row: SPOTIFY AB  ★ PENDING
│  │         ├── leading  icon arrow_upward (Debit)
│  │         ├── tx_merchant   "SPOTIFY AB"         (bodyMedium #181C20)
│  │         ├── tx_category_tag [Subscriptions]
│  │         ├── tx_pending_badge [⚠ Pending]       (SuggestionChip tonal; bg #FFDAD6 label #93000A)
│  │         └── trailing       "−£11.99"           (titleMedium #BA1A1A)
│  ├── [GROUP] 27 Jun 2026
│  │    ├── date_group_header "27 Jun 2026"
│  │    ├── transaction_row: PRET A MANGER 083 LONDON (↑ Debit; -£8.45 #BA1A1A; [Dining])
│  │    └── transaction_row: AMAZON UK MARKETPLACE    (↑ Debit; -£31.99 #BA1A1A; [Shopping])
│  ├── [GROUP] 25 Jun 2026
│  │    └── transaction_row: SALARY ACME LTD (↓ Credit; +£2,400.00 #266489; [Income])
│  ├── [GROUP] 24 Jun 2026
│  │    └── transaction_row: BRITISH GAS DIRECT DEBIT (↑ Debit; -£78.00 #BA1A1A; [Bills])
│  └── [GROUP] 23 Jun 2026
│       └── transaction_row: JAMESON LETTINGS RENT JUNE (↑ Debit; -£1,200.00 #BA1A1A; [Bills])
load_more_button/ (TextButton; label "Load more transactions"; h 40dp r 12dp #266489)
│    visible_when: has_next_page=true AND is_paginating=false
pagination_loader/ (LinearProgressIndicator; colour #266489; h 4dp match_parent)
│    visible_when: is_paginating=true  (replaces load_more_button during page fetch)
BottomNav/ (Home·Accounts·Transactions★·More; selected icon receipt_long #266489)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Transactions                              │
├─────────────────────────────────────────────┤
│                                              │
│  Money in     +£0.00    Money out   −£0.00  │  ← period_summary still visible (zero totals
│  [#266489]              [#BA1A1A]           │    reflect filtered empty result set)
│                                              │
│  ┌──────────────────────────────────────────┐│  ← filter_chips still visible (bound to empty)
│  │● All  ↓ Money in  ↑ Money out  📅 Date  ││    shows active filter context
│  └──────────────────────────────────────────┘│
│  ┌──────────────────────────────────────────┐│  ← search_field still visible (bound to empty)
│  │ 🔍  Search transactions              ✕  ││
│  └──────────────────────────────────────────┘│
│                                              │
│                                              │
│              [receipt_long]                  │  ← empty icon 48dp #41474D; centred
│                                              │
│         No transactions found               │  ← headlineSmall #181C20; centred
│                                              │
│   No transactions match your current        │  ← bodyMedium #41474D; centred; padding h 32dp
│   filters for this period.                  │
│                                              │
│                                              │
│        [  Clear filters  ]                  │  ← clear_filters_button OutlinedButton
│                                             │     label "Clear filters" #266489; h 40dp r 12dp
│                                              │
├─────────────────────────────────────────────┤
│ ⌂ Home  ◫ Accounts  ☰ Transactions  ⋯ More  │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
top_app_bar/ (small; back_arrow; title "Transactions")
period_summary/ (same as content; totals "+£0.00" / "−£0.00" reflect filtered zero set)
│  ├── total_credit  "+£0.00"  (titleMedium #266489)
│  └── total_debit   "−£0.00"  (titleMedium #BA1A1A)
filter_chips/ (same as content; state_binding includes empty; h-scroll chip row)
│  ├── filter_all / filter_money_in / filter_money_out / filter_date_range
search_field/ (same as content; state_binding includes empty)
empty_transactions/ (Column centred; fillMaxSize; padding h 32dp)
│  ├── empty_icon             (Icon receipt_long 48dp #41474D; decorative)
│  ├── empty_title            (headlineSmall #181C20): "No transactions found"
│  ├── empty_body             (bodyMedium #41474D; textAlign Center):
│  │                           "No transactions match your current filters for this period."
│  └── clear_filters_button   (OutlinedButton; label "Clear filters"; border #266489; h 40dp r 12dp)
BottomNav/ (Transactions selected)
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Transactions                              │
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│              [error_outline]                 │  ← icon 48dp #BA1A1A; centred
│                                              │
│      Unable to load transactions            │  ← headlineSmall #181C20; centred
│                                              │
│   No network connection. Please check       │  ← bodyMedium #41474D; centred; padding h 32dp
│   your connection and retry.               │    (NetworkError — recoverable=true)
│                                              │
│         [  Try again  ]                      │  ← retry_button FilledButton; bg #266489
│                                             │     label "Try again"; h 40dp r 12dp
│                                              │    visible_when error.recoverable=true
│                                              │    HIDDEN for 403 ConsentWithdrawnError
│                                              │
├─────────────────────────────────────────────┤
│ ⌂ Home  ◫ Accounts  ☰ Transactions  ⋯ More  │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
top_app_bar/ (small; back_arrow; title "Transactions")
error_state/ (Column centred; fillMaxSize; padding h 32dp; variant=error)
│  ├── error_icon     (Icon error_outline; 48dp; tint #BA1A1A; decorative)
│  ├── error_title    (headlineSmall #181C20): "Unable to load transactions"
│  ├── error_body     (bodyMedium #41474D; textAlign Center; resolved by ViewModel per HTTP status):
│  │       401 TokenExpiredError     → "Session expired. Please log in again."
│  │       403 ConsentWithdrawnError → "Access to transactions has been withdrawn."
│  │       429 RateLimitError        → "Too many requests. Please wait a moment and retry."
│  │       null NetworkError         → "No network connection. Please check your connection and retry."
│  └── retry_button   (FilledButton; label "Try again"; bg #266489 text #FFFFFF; h 40dp r 12dp)
│           visible_when: error.recoverable=true
│           HIDDEN for 403 ConsentWithdrawnError (recoverable=false)
BottomNav/ (Transactions selected)
```

---

### Interaction Summary

| Component | Action | Effect | Target / Outcome |
|---|---|---|---|
| filter_all chip | filter_transactions (filter: all) | transform_state | Resets CreditDebitIndicator filter; recomputes period totals from full in-memory list |
| filter_money_in chip | filter_transactions (filter: credit) | transform_state | Shows CreditDebitIndicator=Credit rows only; recomputes period totals |
| filter_money_out chip | filter_transactions (filter: debit) | transform_state | Shows CreditDebitIndicator=Debit rows only; recomputes period totals |
| filter_date_range chip | open_date_range_picker | transform_state | Opens date-range bottom sheet; on confirm resets cursor and re-fetches with date bounds |
| search_field | search_transactions | transform_state | Case-insensitive match on TransactionInformation and MerchantDetails.MerchantName |
| transaction_row | navigate_transaction_detail | navigate | transaction-detail (transactionId, accountId) |
| load_more_button | load_more_transactions | call_api | GET Links.Next cursor; appends OBTransaction6 rows; updates has_next_page |
| clear_filters_button (empty) | clear_filters | transform_state | Resets filter + date range + search to defaults; returns to content if rows remain |
| retry_button (error) | retry_load | call_api | GET /accounts/{AccountId}/transactions from page one; resets pagination cursor |

---

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| top_app_bar | match_parent (393dp) | 64dp | 0 |
| period_summary | match_parent | 56dp | 0 |
| filter chip (each) | wrap_content | 32dp | 9999dp (full pill) |
| search_field | match_parent − 32dp (361dp) | 48dp | 28dp (extra_large) |
| date_group_header | match_parent | 24dp | 0 |
| transaction_row | match_parent − 32dp | 64dp min (wrap) | 8dp (small) |
| tx_category_tag chip | wrap_content | 24dp | 9999dp (full) |
| tx_pending_badge | wrap_content | 20dp | 9999dp (full) |
| load_more_button | match_parent − 32dp | 40dp | 12dp (medium) |
| pagination_loader (linear) | match_parent | 4dp | 0 |
| empty_icon / error_icon | 48dp | 48dp | n/a |
| clear_filters_button | 200dp | 40dp | 12dp (medium) |
| retry_button | 200dp | 40dp | 12dp (medium) |
| bottom_nav | match_parent | 80dp | 0 |
