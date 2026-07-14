# Transaction Detail — Visual Mockup

> Auto-generated from `screens/transaction-detail/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Transaction Detail

Canvas: 393×852dp · Top app bar with back arrow · No bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Transaction Detail                        │  ← top_app_bar
├─────────────────────────────────────────────┤
│                                              │
│                   ◌                          │  ← circular progress #266489 centred
│               (spinning)                     │
│                                              │
└─────────────────────────────────────────────┘
```

---

### State: content (debit transaction example)

```
┌─────────────────────────────────────────────┐
│ ← Transaction Detail                        │
├─────────────────────────────────────────────┤
│                                              │
│             -£24.80                          │  ← amount_header displaySmall #BA1A1A
│                                              │    sign = "-" for debit
│             GBP                              │    currency labelMedium #41474D
│                                              │
│  ┌─────────────────────────────────────────┐│
│  │  🛒  Sainsbury's                        ││  ← merchant_name titleMedium #181C20
│  │      Groceries                          ││  ← category_label bodySmall #41474D
│  │      MCC: 5411 – Grocery Stores         ││  ← mcc_row bodySmall #41474D
│  └─────────────────────────────────────────┘│
│                                              │
│  ── Transaction details ──────────────────  │
│                                              │
│  Status           Booked                    │  ← status_row (list_item)
│  Date             14 Jul 2026               │  ← booking_date_row
│  Value date       14 Jul 2026               │  ← value_date_row
│  Running balance  £4,256.75 GBP             │  ← balance_after_row
│                                              │
│  ── Reference ────────────────────────────  │
│                                              │
│  SAINSBUR*STORE1234                         │  ← tx_information bodyMedium mono #181C20
│  [⧉ Copy]                                  │  ← copy_reference_button icon_button
│                                              │
│  ── Bank transaction code ────────────────  │
│                                              │
│  PMT / DomesticCreditTransfer               │  ← proprietary_code bodySmall #41474D
│                                              │
└─────────────────────────────────────────────┘
```

### State: content (credit transaction example)

```
┌─────────────────────────────────────────────┐
│ ← Transaction Detail                        │
├─────────────────────────────────────────────┤
│                                              │
│             +£2,850.00                       │  ← amount_header displaySmall #266489
│             GBP                              │    sign = "+" for credit
│                                              │
│  ┌─────────────────────────────────────────┐│
│  │ 💷  Salary — Acme Ltd                   ││
│  │     Income                              ││
│  └─────────────────────────────────────────┘│
│  …[remaining fields same structure]…        │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title "Transaction Detail", leading back ← → transactions)
back_button/ (icon_button arrow_back, always visible)
amount_header/ (text displaySmall, state_binding=[content])
│  color: credit=#266489, debit=#BA1A1A
│  value: "{CreditDebitIndicator == Credit ? '+' : '-'}£{Amount.Amount}"
currency_label/ (text labelMedium #41474D): "GBP"
merchant_card/ (card elevation 1 radius 12dp padding 16dp)
│  ├── category_icon      (icon, md, #266489)
│  ├── merchant_name      (titleMedium #181C20): "Sainsbury's"
│  ├── category_label     (bodySmall #41474D): "Groceries"
│  └── mcc_row            (bodySmall #41474D): "MCC: 5411 – Grocery Stores"
transaction_details_section/ (section_header "Transaction details")
detail_list/ (list vertical)
│  ├── status_row         (list_item supporting="Status" trailing="Booked")
│  ├── booking_date_row   (list_item supporting="Date" trailing="14 Jul 2026")
│  ├── value_date_row     (list_item supporting="Value date" trailing="14 Jul 2026")
│  └── balance_after_row  (list_item supporting="Running balance" trailing="£4,256.75 GBP")
reference_section/ (section_header "Reference")
tx_information/ (text bodyMedium Roboto Mono #181C20): "SAINSBUR*STORE1234"
copy_reference_button/ (icon_button content_copy, clipboard action)
bank_code_section/ (section_header "Bank transaction code")
proprietary_code/ (text bodySmall #41474D): "PMT / DomesticCreditTransfer"
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Transaction Detail                        │
├─────────────────────────────────────────────┤
│                                              │
│            [error_outline]                   │  ← icon 48dp #BA1A1A centred
│                                              │
│    Transaction unavailable                  │  ← title headlineSmall #181C20
│  This transaction could not be loaded.      │  ← body bodyMedium #41474D
│                                              │
│         [  Try again  ]                     │  ← retry_button filled (recoverable)
│         [  Go back    ]                     │  ← back_button text (non-recoverable)
│                                              │
└─────────────────────────────────────────────┘
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Transaction Detail                        │
├─────────────────────────────────────────────┤
│                                              │
│            [receipt_long]                    │  ← icon 48dp #41474D centred
│                                              │
│   Transaction not found                     │  ← title headlineSmall #181C20
│  This transaction is no longer available.   │  ← body bodyMedium #41474D
│                                              │
│         [  Go back  ]                       │  ← navigate_back → transactions
│                                              │
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| back arrow / back_button | navigate_back | transactions |
| copy_reference_button | copy_to_clipboard | system clipboard |
| retry_button (error) | retry_load | in-place (recoverable: 401/network) |
| back_button (error non-recoverable) | navigate_back | transactions |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| amount_header | match_parent | 52dp | 0 |
| merchant_card | match_parent − 32dp | ~80dp | 12dp |
| detail_list rows | match_parent | 48dp each | 0 |
| tx_information | match_parent − 32dp | wrap | 0 |
| copy_reference_button | 48dp | 48dp | circle |
