# Statement Detail — Visual Mockup

> Auto-generated from `screens/statement-detail/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Statement Detail

Canvas: 393×852dp · Top app bar title = StatementReference · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Statement Detail                          │  ← top_app_bar (fallback title)
├─────────────────────────────────────────────┤
│                   ◌                          │  ← circular progress #266489
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← STMT-2026-06-001                          │  ← top_app_bar = StatementReference
├─────────────────────────────────────────────┤
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  STATEMENT                              │ │  ← overline labelSmall #50606E
│ │  June 2026                              │ │  ← period titleLarge #181C20
│ │  01 Jun – 30 Jun 2026                   │ │  ← date_range bodyMedium #41474D
│ │                                          │ │
│ │  Opening balance   £3,842.20            │ │  ← opening_balance (list_item compact)
│ │  Closing balance   £4,281.55            │ │  ← closing_balance
│ │  Interest          £0.00                │ │  ← interest
│ │  Fees              £0.00                │ │  ← fees
│ │                                          │ │
│ │  [  ⬇ Download PDF  ]                   │ │  ← download_button tonal #266489
│ │  [downloading ────]  (if Downloading)   │ │    progress_indicator inline on download
│ └─────────────────────────────────────────┘ │
│                                              │
│  Transactions                                │  ← section_header titleSmall #181C20
│                                              │
│  ┌──────────────────────────────────────┐   │
│  │ 🛒  Sainsbury's           -£24.80   │   │  ← tx_row card elevation 0 radius 8dp
│  │     01 Jun 2026                      │   │
│  └──────────────────────────────────────┘   │
│  ┌──────────────────────────────────────┐   │
│  │ 💷  Salary — Acme Ltd   +£2,850     │   │
│  │     02 Jun 2026                      │   │
│  └──────────────────────────────────────┘   │
│  ┌──────────────────────────────────────┐   │
│  │ ☕  Costa Coffee         -£4.35      │   │
│  │     05 Jun 2026                      │   │
│  └──────────────────────────────────────┘   │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title=statement.StatementReference, leading back → statements)
statement_header_card/ (card elevation 2 radius 12dp padding 16dp margin h 16dp)
│  ├── statement_reference  (overline labelSmall #50606E): "STMT-2026-06-001"
│  ├── period_title         (titleLarge #181C20): "June 2026"
│  ├── date_range           (bodyMedium #41474D): "01 Jun – 30 Jun 2026"
│  ├── statement_type       (labelSmall #41474D): "Regular"
│  ├── amounts_list/
│  │    ├── opening_balance (list_item compact): "Opening balance  £3,842.20"
│  │    ├── closing_balance (list_item compact): "Closing balance  £4,281.55"
│  │    ├── interest_row    (list_item compact): "Interest  £0.00"
│  │    └── fees_row        (list_item compact): "Fees  £0.00"
│  ├── download_button      (button tonal icon download): "Download PDF"
│  └── download_progress    (progress_indicator linear, visible_when Downloading)
section_header/ (text titleSmall #181C20): "Transactions"
statement_transactions_list/ (list vertical, items=statementTransactions)
└── tx_row × N (card elevation 0 radius 8dp padding v 12dp h 16dp)
     ├── tx_icon    (icon categoryIcon, md, #50606E)
     ├── tx_name    (bodyMedium #181C20): "Sainsbury's"
     ├── tx_date    (bodySmall #41474D): "01 Jun 2026"
     └── tx_amount  (bodyMedium, credit=#266489, debit=#BA1A1A)
BottomNav (always)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← STMT-2026-06-001                          │
├─────────────────────────────────────────────┤
│ [statement_header_card still shown]          │
│ [download_button visible]                    │
│                                              │
│            [description]                     │  ← icon 48dp #41474D
│    No transactions in this statement        │  ← title headlineSmall #181C20
│  This statement period contains no          │  ← body bodyMedium #41474D
│  transaction records.                       │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Statement Detail                          │
├─────────────────────────────────────────────┤
│            [error_outline]                   │  ← icon 48dp #BA1A1A
│    Unable to load statement                 │
│         [  Try again  ]                     │  ← retry_button filled #266489
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| back arrow | navigate_back | statements |
| download_button | download_statement_pdf | ktor-client-download → platform share sheet |
| tx_row | navigate_transaction_detail | transaction-detail (transactionId, accountId) |
| retry_button | retry_load | in-place retry |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| statement_header_card | match_parent − 32dp | ~220dp | 12dp |
| download_button | match_parent − 48dp | 48dp | 12dp |
| download_progress | match_parent − 48dp | 4dp | 0 |
| tx_row | match_parent − 32dp | 64dp min | 8dp |
