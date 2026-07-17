# Transaction Detail — Visual Mockup

> Auto-generated from `screens/transaction-detail/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Transaction Detail

Canvas: 393×852dp (Pixel 5) · Top app bar visible · No bottom nav · No FAB · Roboto font · Material 3 light theme · bg #F7F9FF

Shell resolved from `ui.yaml#shell` (overrides `app-shell.yaml` defaults):
- **Top app bar**: visible · variant small · h 56dp · title "Transaction Detail" · leading back arrow (icon: arrow_back, 48dp, tint #266489) · bg #F7F9FF · title style titleLarge 22sp #181C20
- **Bottom navigation**: **HIDDEN** — `bottom_navigation_visible: false` (detail screen; no rail tabs)
- **FAB**: hidden — `fab_visible: false`
- Usable body: 852 − 56 = **796dp** (scrollable LazyColumn, screen_padding 16dp horizontal)

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Transaction Detail                        │  ← top_app_bar h 56dp bg #F7F9FF
│                                              │    title titleLarge 22sp #181C20
├─────────────────────────────────────────────┤    leading: back_button arrow_back #266489
│                                              │
│                                              │
│                                              │
│                                              │
│                   ◌                          │  ← progress_indicator circular
│              (spinning)                      │    tint #266489 (primary), size 48dp
│                                              │    centered horizontally + vertically
│                                              │    in 796dp body viewport
│                                              │
│                                              │
│                                              │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — loading

```
Screen: Transaction Detail  (TransactionDetailUiState.Loading)
│
top_app_bar/ (variant:small, bg:#F7F9FF, h:56dp, elevation:0)
├── back_button     (icon_button arrow_back, tint:#266489, size:48dp, always visible)
└── title           "Transaction Detail" (titleLarge 22sp #181C20)

body/ (Column, fill, bg:#F7F9FF, contentPadding 16dp horizontal)
└── Box (fillMaxSize, contentAlignment:Center)
    └── progress_indicator  (circular, tint:#266489, size:48dp)
        accessibility_label: "{strings.transaction_detail_loading}"

BottomNav/ : HIDDEN (ui.yaml#shell.bottom_navigation_visible = false)
```

---

### State: content

Primary fixture: TX-20260626-0001 · Tesco Stores · Debit · Booked · MCC 5411 (demo-data.yaml `transaction`)

```
┌─────────────────────────────────────────────┐
│ ← Transaction Detail                        │  ← top_app_bar h 56dp bg #F7F9FF
│                                              │    back_button arrow_back #266489 leading
├─────────────────────────────────────────────┤
│                                              │    padding top 24dp horizontal 16dp
│              -£42.17                         │  ← amount_header displaySmall 36sp/line44
│                                              │    color #BA1A1A (error — Debit indicator)
│               GBP                            │  ← transaction_currency_meta labelMedium
│                                              │    12sp #41474D centered, margin bottom 16dp
│  Tesco Stores                               │  ← merchant_name headlineMedium 28sp #181C20
│                                              │    MerchantDetails.MerchantName present
│  ┌──────────┐                               │
│  │ Booked   │                               │  ← status_badge chip assist
│  └──────────┘                               │    bg #C9E6FF text #004B6F labelLarge 14sp
│                                              │    radius 99dp padding h 12dp v 6dp
│ ─────────────────────────────────────────── │  ← header_separator divider h 1dp #C1C7CE
│                                              │    margin vertical 12dp
│ ┌─────────────────────────────────────────┐ │  ← detail_card elevation 1 bg #F1F4F9
│ │ TRANSACTION DETAILS                      │ │    radius 12dp margin h 0dp padding 16dp
│ │                                          │ │  ← detail_card_header titleSmall 14sp #41474D
│ │  Booking date                            │ │  ← booking_date_row list_item two-line
│ │  2026-06-26T11:22:00Z                   │ │    label bodyMedium #41474D
│ │ ──────────────────────────────────────  │ │    supporting bodyMedium #181C20
│ │  Value date                              │ │  ← value_date_row list_item two-line
│ │  2026-06-26T11:22:00Z                   │ │    divider outlineVariant #C1C7CE
│ │ ──────────────────────────────────────  │ │
│ │  Category                                │ │  ← category_row
│ │  Groceries                               │ │    client-derived from MCC 5411
│ │ ──────────────────────────────────────  │ │
│ │  Merchant code (MCC)                     │ │  ← mcc_row VISIBLE — MCC 5411 ≠ null
│ │  5411                                    │ │    (hidden for credits with null MCC)
│ │ ──────────────────────────────────────  │ │
│ │  Balance after               £447.63     │ │  ← balance_after_row single-line + trailing
│ │ ──────────────────────────────────────  │ │    Balance.CreditDebitIndicator=Credit → no −
│ │  Reference                         [⧉]  │ │  ← reference_row two-line + trailing_icon
│ │  TESCO STORES 3476 LONDON               │ │    content_copy icon 24dp tint #266489
│ │ ──────────────────────────────────────  │ │    tap anywhere on row → copy_to_clipboard
│ │  Bank code                               │ │  ← bank_code_row two-line
│ │  DR · HSBC                              │ │    ProprietaryBankTransactionCode.Code/Issuer
│ └─────────────────────────────────────────┘ │    (card bottom radius 12dp)
│                                              │
└─────────────────────────────────────────────┘
```

**Credit variant note** (fixture TX-20260625-0001 · ACME LTD · Credit · Booked):
- `amount_header` renders `+£2400.00` in color **#266489** (primary — Credit indicator)
- `merchant_name` shows "ACME LTD" (MerchantDetails.MerchantName present for salary credit)
- `status_badge` remains Booked → bg #C9E6FF / text #004B6F unchanged
- `mcc_row` is **HIDDEN** — `MerchantCategoryCode: null` (salary credit has no card MCC)

**Pending variant note** (fixture TX-20260629-0001 · Pret A Manger · Debit · Pending):
- `status_badge` renders "Pending" → bg **#D3E5F5** (secondaryContainer) / text **#384956** (onSecondaryContainer)
- `ValueDateTime` (2026-06-30) differs from `BookingDateTime` (2026-06-29) — both rows show distinct dates

### Component Hierarchy — content

```
Screen: Transaction Detail  (TransactionDetailUiState.Content)
│
top_app_bar/ (variant:small, bg:#F7F9FF, h:56dp)
├── back_button     (icon_button arrow_back, tint:#266489, size:48dp, always visible)
│   action_contract: effect:navigate → transactions
└── title           "Transaction Detail" (titleLarge 22sp #181C20)

body/ (LazyColumn, fill, bg:#F7F9FF, contentPadding start:24dp end:16dp h:16dp)
│
├── amount_header       (Text displaySmall 36sp, color:#BA1A1A [debit] / #266489 [credit])
│                        value:"-£42.17" · centered · Roboto Mono
├── transaction_currency_meta (Text labelMedium 12sp #41474D) · "GBP" · centered
├── Spacer 16dp
├── merchant_name       (Text headlineMedium 28sp #181C20) · "Tesco Stores"
├── Spacer 8dp
├── status_badge        (AssistChip, label:"Booked")
│                        bg:#C9E6FF text:#004B6F labelLarge 14sp radius:99dp
├── Spacer 12dp
├── header_separator    (Divider, color:#C1C7CE, thickness:1dp)
├── Spacer 12dp
│
└── detail_card         (Card elevation:1 bg:#F1F4F9 radius:12dp padding:16dp)
    ├── detail_card_header  (Text titleSmall 14sp #41474D) · "TRANSACTION DETAILS"
    ├── Spacer 12dp
    ├── booking_date_row    (ListItem two-line h:72dp)
    │     label:        "Booking date"       bodyMedium #41474D
    │     supporting:   "2026-06-26T11:22:00Z"  bodyMedium #181C20
    ├── Divider (color:#C1C7CE)
    ├── value_date_row      (ListItem two-line h:72dp)
    │     label:        "Value date"         bodyMedium #41474D
    │     supporting:   "2026-06-26T11:22:00Z"  bodyMedium #181C20
    ├── Divider
    ├── category_row        (ListItem two-line h:72dp)
    │     label:        "Category"           bodyMedium #41474D
    │     supporting:   "Groceries"          bodyMedium #181C20
    ├── Divider
    ├── mcc_row             (ListItem two-line h:72dp, visible:MCC≠null)
    │     label:        "Merchant code (MCC)" bodyMedium #41474D
    │     supporting:   "5411"               bodyMedium #181C20
    ├── Divider
    ├── balance_after_row   (ListItem one-line h:56dp)
    │     label:        "Balance after"      bodyMedium #41474D
    │     trailing:     "£447.63"            bodyMedium #181C20
    ├── Divider
    ├── reference_row       (ListItem two-line h:72dp, clickable entire row)
    │     label:        "Reference"          bodyMedium #41474D
    │     supporting:   "TESCO STORES 3476 LONDON"  bodyMedium #181C20
    │     trailing_icon: content_copy 24dp tint:#266489
    │     action_contract: effect:copy_clipboard → ClipboardService
    ├── Divider
    └── bank_code_row       (ListItem two-line h:72dp)
          label:        "Bank code"          bodyMedium #41474D
          supporting:   "DR · HSBC"          bodyMedium #181C20

BottomNav/ : HIDDEN
```

---

### State: error

Primary sub-state shown: **recoverable** (TokenExpiredError / NetworkError — shows Retry).
Non-recoverable sub-state (ConsentWithdrawnError / TransactionNotFoundError): Retry hidden, Go Back shown.

```
┌─────────────────────────────────────────────┐
│ ← Transaction Detail                        │  ← top_app_bar h 56dp bg #F7F9FF
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│            [error_outline]                   │  ← icon error_outline 48dp
│                                              │    tint #BA1A1A (error) centered
│    Transaction unavailable                  │  ← error_state title headlineMedium
│                                              │    28sp #181C20 centered
│  Session expired. Please log in again.      │  ← error_state body bodyMedium
│                                              │    14sp #41474D centered
│                                              │    (error.message from demo fixture)
│                                              │
│       ┌─────────────────────────┐            │
│       │       Try again          │            │  ← retry_button filled
│       └─────────────────────────┘            │    visible: error.recoverable=true
│                                              │    bg #266489 text #FFFFFF
│ - - - - - - - - - - - - - - - - - - - - -  │    (401 TokenExpiredError — recoverable)
│                                              │
│       ┌─────────────────────────┐            │
│       │       Go back            │            │  ← go_back_button outlined
│       └─────────────────────────┘            │    visible: error.recoverable=false
│                                              │    border #266489 text #266489
│                                              │    (403 ConsentWithdrawn — non-recoverable)
│                                              │
└─────────────────────────────────────────────┘
```

Note: only ONE button is visible at a time — either `retry_button` (recoverable) or `go_back_button` (non-recoverable). The dashed separator above is for documentation only.

### Component Hierarchy — error

```
Screen: Transaction Detail  (TransactionDetailUiState.Error)
│
top_app_bar/ (variant:small, bg:#F7F9FF, h:56dp)
├── back_button     (icon_button arrow_back, tint:#266489, always visible)
│   action_contract: effect:navigate → transactions
└── title           "Transaction Detail" (titleLarge 22sp #181C20)

body/ (Column, fillMaxSize, bg:#F7F9FF, contentPadding 24dp, arrangement:Center)
│
└── error_state     (EmptyStateComponent variant:error)
    ├── icon        error_outline 48dp tint:#BA1A1A   centered
    ├── title       {strings.transaction_detail_error_title}
    │               headlineMedium 28sp #181C20 centered
    ├── body        {error.message}  (e.g. "Session expired. Please log in again.")
    │               bodyMedium 14sp #41474D centered  margin top 8dp
    ├── Spacer 24dp
    ├── retry_button    (Button filled, visible:error.recoverable)
    │                   label:"Try again" labelLarge 14sp
    │                   bg:#266489 text:#FFFFFF radius:99dp h:40dp w:wrap+horizontal pad 24dp
    │                   action_contract: effect:call_api (ktorfit GET /transactions)
    └── go_back_button  (Button outlined, visible:!error.recoverable)
                        label:"Go back" labelLarge 14sp
                        border:#266489 text:#266489 radius:99dp h:40dp
                        action_contract: effect:navigate → transactions

BottomNav/ : HIDDEN
```

---

### State: empty

Triggered when: OBReadTransaction6 returns 200 but `transactionId` absent in result list.
Distinct from error state — no API error, data fetch succeeded, client filter returned zero matches.

```
┌─────────────────────────────────────────────┐
│ ← Transaction Detail                        │  ← top_app_bar h 56dp bg #F7F9FF
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│            [receipt_long]                    │  ← icon receipt_long 48dp
│                                              │    tint #41474D (onSurfaceVariant)
│    Transaction not found                    │  ← transaction_empty_state title
│                                              │    headlineMedium 28sp #181C20 centered
│  This transaction is no longer available.   │  ← body bodyMedium 14sp #41474D centered
│  It may have been removed or your consent   │    ({strings.transaction_detail_empty_body})
│  scope has changed.                         │
│                                              │
│       ┌─────────────────────────┐            │
│       │       Go back            │            │  ← transaction_empty_back_button outlined
│       └─────────────────────────┘            │    border #266489 text #266489 radius 99dp
│                                              │    action_contract: effect:navigate → transactions
│                                              │    NO Retry offered (fetch succeeded)
│                                              │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: Transaction Detail  (TransactionDetailUiState.Empty)
│
top_app_bar/ (variant:small, bg:#F7F9FF, h:56dp)
├── back_button     (icon_button arrow_back, tint:#266489, always visible)
│   action_contract: effect:navigate → transactions
└── title           "Transaction Detail" (titleLarge 22sp #181C20)

body/ (Column, fillMaxSize, bg:#F7F9FF, contentPadding 24dp, arrangement:Center)
│
└── transaction_empty_state  (EmptyStateComponent variant:neutral)
    ├── icon        receipt_long 48dp tint:#41474D   centered
    ├── title       {strings.transaction_detail_empty_title}
    │               headlineMedium 28sp #181C20 centered
    ├── body        {strings.transaction_detail_empty_body}
    │               bodyMedium 14sp #41474D centered  margin top 8dp
    ├── Spacer 24dp
    └── transaction_empty_back_button  (Button outlined)
                    label:"Go back" labelLarge 14sp
                    border:#266489 text:#266489 radius:99dp h:40dp
                    action_contract: effect:navigate → transactions
                    (no retry — TransactionNotFoundError is non-recoverable)

BottomNav/ : HIDDEN
```

---

### Interaction Summary

| Component | Action | Effect | Target / Value |
|---|---|---|---|
| back_button (top app bar, all states) | navigate_back | navigate | transactions screen |
| reference_row copy icon (content state) | copy_to_clipboard | copy_clipboard | `transaction.TransactionInformation` ("TESCO STORES 3476 LONDON") via ClipboardService |
| retry_button (error state, recoverable=true) | retry_load | call_api | GET /accounts/{AccountId}/transactions (ktorfit re-fetch; visible: 401 / NetworkError only) |
| go_back_button (error state, recoverable=false) | navigate_back | navigate | transactions screen (403 ConsentWithdrawn / TransactionNotFoundError) |
| transaction_empty_back_button (empty state) | navigate_back | navigate | transactions screen |

---

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| top_app_bar | 393dp (match_parent) | 56dp | 0 |
| back_button | 48dp | 48dp | 99dp (icon_button circular ripple) |
| amount_header | match_parent − 32dp (329dp) | 44dp (displaySmall line height) | 0 |
| transaction_currency_meta | match_parent − 32dp | 16dp (labelMedium line height) | 0 |
| merchant_name | match_parent − 32dp | 36dp (headlineMedium line height) | 0 |
| status_badge chip | wrap_content (~84dp) | 32dp | 99dp (full) |
| header_separator | match_parent | 1dp | 0 |
| detail_card | 361dp (393 − 32dp screen margin) | wrap_content (~540dp) | 12dp (medium) |
| detail_card_header label | 329dp (card content width) | 20dp | 0 |
| booking_date_row | 329dp | 72dp (two-line) | 0 |
| value_date_row | 329dp | 72dp (two-line) | 0 |
| category_row | 329dp | 72dp (two-line) | 0 |
| mcc_row (when visible) | 329dp | 72dp (two-line) | 0 |
| balance_after_row | 329dp | 56dp (one-line + trailing) | 0 |
| reference_row | 329dp | 72dp (two-line + trailing icon) | 0 |
| bank_code_row | 329dp | 72dp (two-line) | 0 |
| error_outline icon | 48dp | 48dp | 0 (material icon) |
| receipt_long icon | 48dp | 48dp | 0 |
| retry_button | match_parent − 32dp (329dp) | 40dp | 99dp (filled button) |
| go_back_button | match_parent − 32dp (329dp) | 40dp | 99dp (outlined button) |
| transaction_empty_back_button | match_parent − 32dp (329dp) | 40dp | 99dp |
| progress_indicator | 48dp | 48dp | circular |
