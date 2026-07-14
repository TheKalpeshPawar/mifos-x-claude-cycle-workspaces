# Recurring Payments — Visual Mockup

> Auto-generated from `screens/recurring-subscriptions/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Source: kotlinx-datetime pattern detection over cached DataStore transactions
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Recurring Payments

Canvas: 393×852dp · Top app bar with back · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Recurring Payments                        │  ← top_app_bar
├─────────────────────────────────────────────┤
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← loading_skeleton shimmer × 5 rows
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │    each ~64dp radius 8dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
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
│ ← Recurring Payments                        │
├─────────────────────────────────────────────┤
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │ ℹ  Detected by analysing your past     │ │  ← detected_notice banner bg #DDE3EA
│ │    transactions. Not from the bank.    │ │    icon info_outline bodyMedium #41474D
│ └─────────────────────────────────────────┘ │
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  Estimated monthly spend                │ │  ← summary_card elevation 1 radius 12dp
│ │  £142.49                               │ │  ← summary_amount headlineMedium #BA1A1A
│ │  6 recurring payments detected         │ │  ← summary_count bodySmall #41474D
│ └─────────────────────────────────────────┘ │
│                                              │
│  ↻  Netflix                    £15.99       │  ← subscription_row list_item
│     Monthly · Next 14 Aug 2026              │    icon autorenew #266489
│     [detected]                              │    detected_badge assist chip
│  ↻  Spotify                    £9.99        │
│     Monthly · Next 21 Aug 2026              │
│     [detected]                              │
│  ↻  Amazon Prime               £8.99        │
│     Monthly · Next 17 Aug 2026              │
│     [detected]                              │
│  ↻  Apple iCloud+              £2.99        │
│     Monthly · Next 19 Aug 2026              │
│     [detected]                              │
│  ↻  Adobe Creative Cloud       £54.99       │
│     Monthly · Next 09 Aug 2026              │
│     [detected]                              │
│  ↻  Sky TV Package             £49.54       │
│     Monthly · Next 03 Aug 2026              │
│     [detected]                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title "Recurring Payments", leading back)
detected_notice/ (banner icon info_outline, bg #DDE3EA padding 12dp margin h 16dp)
│  "These payments were detected by analysing your transaction history.
│   They are not official bank-registered mandates."
summary_card/ (card elevation 1 radius 12dp padding 16dp margin h 16dp v 8dp)
│  ├── summary_label  (labelMedium #50606E): "Estimated monthly spend"
│  ├── summary_amount (headlineMedium #BA1A1A): "£142.49"  [normalised 30-day]
│  └── summary_count  (bodySmall #41474D): "6 recurring payments detected"
subscriptions_list/ (list vertical, items_source=subscriptions, sorted monthly DESC)
└── subscription_row × N (list_item icon autorenew #266489 on_click=show_merchant_history)
     ├── label        (titleMedium #181C20): "Netflix"  [item.merchant]
     ├── supporting   (bodySmall #41474D): "Monthly · Next 14 Aug 2026"
     ├── trailing     (bodyMedium #181C20): "£15.99"  [item.amount]
     └── detected_badge (chip assist labelSmall): "detected"
BottomNav (always)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Recurring Payments                        │
├─────────────────────────────────────────────┤
│            [autorenew]                       │  ← icon 48dp #41474D
│    No recurring payments found             │  ← title headlineSmall #181C20
│  No recurring payment patterns were       │  ← body bodyMedium #41474D
│  detected in your recent transactions.    │
│  Import more transactions to improve      │
│  detection.                               │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Recurring Payments                        │
├─────────────────────────────────────────────┤
│            [error_outline]                   │  ← icon 48dp #BA1A1A
│    Unable to load recurring payments       │
│  Could not read cached transactions.       │
│         [  Try again  ]                     │  ← retry_button outlined
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| back_button | navigate_back | pfm-dashboard |
| subscription_row | show_merchant_transaction_history | transactions (merchant filter) |
| retry_button (error) | retry_load_subscriptions | in-place (DataStore re-read) |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| detected_notice banner | match_parent − 32dp | ~56dp | 12dp |
| summary_card | match_parent − 32dp | ~80dp | 12dp |
| subscription_row | match_parent | 72dp | 0 |
| detected_badge chip | wrap | 24dp | 9999 |
| shimmer_row | match_parent − 32dp | 64dp | 8dp |
