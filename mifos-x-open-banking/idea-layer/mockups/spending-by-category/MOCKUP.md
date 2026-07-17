# Spending by Category — Visual Mockup

> Auto-generated from `screens/spending-by-category/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Spending by Category

Canvas: 393×852dp (Pixel 5) · Top app bar (small, back leading) · Bottom nav (Home | Accounts | Transactions | More) · No FAB · Roboto font · Material 3 light theme · Background #F7F9FF

Shell resolved from `app-shell.yaml` + `ui.yaml#shell`:
- Top app bar: enabled, title "Spending by Category", leading back arrow, variant small.
- Bottom navigation: enabled — Home (home) | Accounts (account_balance) | Transactions (receipt_long) | More (more_horiz → settings). No tab is selected (sub-screen, not a primary nav destination).
- FAB: disabled (`fab_visible: false`).
- Period selector (`period_selector`) is bound to ALL states `[loading, content, empty, error]` and is always rendered below the top app bar.

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ←  Spending by Category                     │  ← top_app_bar bg #F7F9FF h 64dp
│                                              │    leading icon arrow_back 24dp #266489
├─────────────────────────────────────────────┤    title titleLarge 22sp/28sp w400 #181C20
│                                              │    elevation 0 → 2 on content scroll
│ (This month ✓)  (Last month)  (3 months) → │  ← period_selector chip_group h-scroll
│                                              │    chip h 32dp, padding h 8dp v 6dp
│                                              │    "This month" selected: bg #C9E6FF
│ ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░    │    text #004B6F, radius 9999 (pill)
│ ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░    │  ← skeleton_card shimmer 80dp h
│                                              │    bg #DDE3EA pulse 1.5s, radius 12dp
│ ░░░░░░░░░░░░░░░░░░░░░                       │  ← skeleton_text shimmer 60%×16dp r 8dp
│                                              │
│ ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░    │  ← skeleton_block_1 shimmer 56dp h r 8dp
│                                              │
│ ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░    │  ← skeleton_block_2 shimmer 56dp h r 8dp
│                                              │
│ ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░    │  ← skeleton_block_3 shimmer 56dp h r 8dp
│                                              │
│   [8dp gap between skeleton blocks]         │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← bottom_nav bg #F7F9FF h 80dp
└─────────────────────────────────────────────┘    icon+label pairs, all unselected #41474D
```

### Component Hierarchy — loading

```
Screen: Spending by Category (SpendingByCategoryUiState.Loading)
│
top_app_bar/ (SmallTopAppBar, bg #F7F9FF, h 64dp, elevation 0 → 2 on scroll)
├── leading: back_arrow   (icon arrow_back 24dp #266489, navigatesBack())
└── title: "Spending by Category"  (titleLarge 22sp/28sp w400 #181C20)

period_selector/ (chip_group variant:single_select, scroll_direction:horizontal,
│                 padding h 16dp v 8dp, state_binding: all, gap 8dp between chips)
│   accessibility_label: "Period filter"
├── period_this_month  "This month"  (filter chip, selected:true, bg #C9E6FF, text #004B6F,
│                                     radius 9999, h 32dp, min touch 48dp)
├── period_last_month  "Last month"  (filter chip, unselected, outline #72787E, text #41474D)
└── period_3_months    "3 months"    (filter chip, unselected, outline #72787E, text #41474D)

loading_skeleton/ (stack vertical, gap 8dp, padding h 16dp t 8dp b 16dp)
│   accessibility_label: "Computing your spending breakdown"
│   reduce-motion: static #DDE3EA fill (no pulse)
├── skeleton_card    (shimmer variant:card,   80dp h, radius 12dp, bg #DDE3EA, pulse 1.5s)
├── skeleton_text    (shimmer variant:text,   16dp h × 60% width,  radius 8dp,  bg #DDE3EA)
├── skeleton_block_1 (shimmer variant:block,  56dp h, radius 8dp,  bg #DDE3EA)
├── skeleton_block_2 (shimmer variant:block,  56dp h, radius 8dp,  bg #DDE3EA)
└── skeleton_block_3 (shimmer variant:block,  56dp h, radius 8dp,  bg #DDE3EA)

BottomNav/ (persistent, always rendered)
├── tab Home         (icon:home,           label:"Home",         unselected, tint #41474D)
├── tab Accounts     (icon:account_balance, label:"Accounts",    unselected, tint #41474D)
├── tab Transactions (icon:receipt_long,   label:"Transactions", unselected, tint #41474D)
└── tab More         (icon:more_horiz,     label:"More",         unselected, tint #41474D)
```

---

### State: content

(Default period: this_month — June 2026, from demo-data.yaml)

```
┌─────────────────────────────────────────────┐
│ ←  Spending by Category                     │  ← top_app_bar bg #F7F9FF h 64dp
├─────────────────────────────────────────────┤
│                                              │
│ (This month ✓)  (Last month)  (3 months) → │  ← period_selector; "This month" active
│                                              │    selected bg #C9E6FF text #004B6F
│ ┌─────────────────────────────────────────┐ │  ← spend_summary_card bg #F7F9FF elevation 1
│ │ Total Spend — June 2026                 │ │    radius 12dp, padding 16dp, margin h 16dp
│ │                                          │ │    label: labelMedium 12sp/16sp #41474D
│ │ £1,840.00                               │ │    amount: headlineMedium 28sp/36sp #BA1A1A
│ └─────────────────────────────────────────┘ │
│                                              │
│  🧾 Bills                        £1,356.00  │  ← category_row[0]; icon receipt_long 24dp
│     4 transactions · 73.7%                  │    label bodyLarge 16sp #181C20
│     ████████████████████░░░░░░   73.7%     │    supporting bodyMedium 14sp #41474D
│ ──────────────────────────────────────────  │    trailing bodyLarge 16sp #181C20 end
│  🛒 Groceries                     £198.00   │  ← category_row[1]; icon shopping_cart 24dp
│     9 transactions · 10.8%                  │    progress bar #266489 on #E0E3E8
│     █████░░░░░░░░░░░░░░░░░░░░░   10.8%     │    h 4dp radius 2dp, margin h 16dp
│ ──────────────────────────────────────────  │    divider 1dp #C1C7CE full_width
│  🍽 Dining                          £88.00  │  ← category_row[2]; icon restaurant 24dp
│     5 transactions · 4.8%                   │
│     ██░░░░░░░░░░░░░░░░░░░░░░░░    4.8%     │
│ ──────────────────────────────────────────  │
│  📺 Subscriptions                   £63.00  │  ← category_row[3]; icon subscriptions 24dp
│     5 transactions · 3.4%                   │
│     █░░░░░░░░░░░░░░░░░░░░░░░░░    3.4%     │
│ ──────────────────────────────────────────  │
│  🚌 Transport                       £41.00  │  ← category_row[4]; icon directions_transit
│     8 transactions · 2.2%                   │    all rows tappable → transactions screen
│     ▌░░░░░░░░░░░░░░░░░░░░░░░░░    2.2%     │    with URI-encoded category filter
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
Screen: Spending by Category (SpendingByCategoryUiState.Content — this_month, June 2026)
│
top_app_bar/ (SmallTopAppBar, bg #F7F9FF, h 64dp)
├── leading: back_arrow (icon arrow_back 24dp #266489)
└── title: "Spending by Category" (titleLarge 22sp/28sp w400 #181C20)

period_selector/ (chip_group single_select h-scroll, padding h 16dp v 8dp, gap 8dp)
│   accessibility_label: "Period filter"
├── period_this_month  "This month" (selected: bg #C9E6FF text #004B6F radius 9999 h 32dp)
│   on_click → selectPeriod(this_month) — transform_state, re-aggregates Room debits current month
├── period_last_month  "Last month" (unselected: outline #72787E text #41474D)
│   on_click → selectPeriod(last_month) — transform_state, re-aggregates Room debits prev month
└── period_3_months    "3 months"   (unselected: outline #72787E text #41474D)
    on_click → selectPeriod(3_months) — transform_state, re-aggregates Room debits last 90 days

spend_summary_card/ (card bg #F7F9FF, elevation 1, radius 12dp, padding 16dp,
│                    margin h 16dp v 8dp; display-only)
│   accessibility_label: "Total spend June 2026: £1,840.00"
│   stack vertical gap 4dp:
├── total_spend_label  (labelMedium 12sp/16sp w500 #41474D): "Total Spend — June 2026"
└── total_spend_amount (headlineMedium 28sp/36sp w400 #BA1A1A): "£1,840.00"
    accessibility_label: "Total spend £1,840.00"

category_list/ (list vertical, divider:true outlineVariant #C1C7CE,
│               padding h 16dp, items_source:categories, sorted amount desc)
│   accessibility_label: "Spending categories"
│
├── category_row[0] — Bills (tappable, ripple #C9E6FF, min touch 48dp)
│   on_click → navigateCategoryTransactions(category:"Bills") → transactions (filter:Bills)
│   stack vertical gap 0:
│   ├── row_content/ (h 56dp, stack horizontal alignment center_vertical, padding h 16dp)
│   │   ├── icon receipt_long     (24dp #50606E decorative, margin end 16dp)
│   │   ├── stack vertical gap 2dp weight 1:
│   │   │   ├── label "Bills"     (bodyLarge 16sp/24sp w400 #181C20, maxLines 1 ellipsis)
│   │   │   └── supporting "4 transactions · 73.7%"  (bodyMedium 14sp/20sp w400 #41474D)
│   │   └── trailing "£1,356.00"  (bodyLarge 16sp/24sp w400 #181C20 align end)
│   └── category_progress_bar[Bills]
│       (linear_progress h 4dp radius 2dp, margin h 16dp b 8dp,
│        value 0.737, indicator #266489, track #E0E3E8)
│       accessibility_label: "Bills spending share"
│
├── [divider 1dp #C1C7CE full_width]
│
├── category_row[1] — Groceries (tappable)
│   on_click → navigateCategoryTransactions(category:"Groceries") → transactions
│   ├── icon shopping_cart 24dp #50606E; label "Groceries"; supporting "9 transactions · 10.8%"
│   ├── trailing "£198.00"; progress value:0.108 indicator:#266489 track:#E0E3E8
│
├── [divider 1dp #C1C7CE]
│
├── category_row[2] — Dining (tappable)
│   on_click → navigateCategoryTransactions(category:"Dining") → transactions
│   ├── icon restaurant 24dp #50606E; label "Dining"; supporting "5 transactions · 4.8%"
│   ├── trailing "£88.00"; progress value:0.048 indicator:#266489 track:#E0E3E8
│
├── [divider 1dp #C1C7CE]
│
├── category_row[3] — Subscriptions (tappable)
│   on_click → navigateCategoryTransactions(category:"Subscriptions") → transactions
│   ├── icon subscriptions 24dp #50606E; label "Subscriptions"; supporting "5 transactions · 3.4%"
│   ├── trailing "£63.00"; progress value:0.034 indicator:#266489 track:#E0E3E8
│
├── [divider 1dp #C1C7CE]
│
└── category_row[4] — Transport (tappable)
    on_click → navigateCategoryTransactions(category:"Transport") → transactions
    ├── icon directions_transit 24dp #50606E; label "Transport"; supporting "8 transactions · 2.2%"
    └── trailing "£41.00"; progress value:0.022 indicator:#266489 track:#E0E3E8

BottomNav/ (persistent)
├── tab Home         (unselected, tint #41474D)
├── tab Accounts     (unselected, tint #41474D)
├── tab Transactions (unselected, tint #41474D)
└── tab More         (unselected, tint #41474D)
```

---

### State: empty

(EC-SBC-001 — no debit transactions in Room cache for selected period)

```
┌─────────────────────────────────────────────┐
│ ←  Spending by Category                     │  ← top_app_bar bg #F7F9FF h 64dp
├─────────────────────────────────────────────┤
│                                              │
│ (This month ✓)  (Last month)  (3 months) → │  ← period_selector still interactive
│                                              │    (EC-SBC-001: period selector remains
│                                              │     active so user can switch windows)
│                                              │
│                                              │
│                  [pie_chart]                 │  ← icon pie_chart 48dp #41474D centred
│                                              │
│          No spending data                   │  ← title headlineSmall 24sp/32sp #181C20
│                                              │    centred, weight 400
│   No debit transactions were found for     │
│   this period. Try a different time         │  ← body bodyMedium 14sp/20sp #41474D
│   window or check back later.               │    centred, padding h 32dp
│                                              │
│                                              │
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: Spending by Category (SpendingByCategoryUiState.Empty — EC-SBC-001)
│
top_app_bar/ (SmallTopAppBar, bg #F7F9FF, h 64dp)
├── leading: back_arrow (icon arrow_back 24dp #266489)
└── title: "Spending by Category" (titleLarge 22sp w400 #181C20)

period_selector/ (chip_group h-scroll — remains fully interactive in empty state)
│   accessibility_label: "Period filter"
├── period_this_month  "This month" (selected filter chip, bg #C9E6FF text #004B6F)
│   on_click → selectPeriod(this_month) — transform_state
├── period_last_month  "Last month" (unselected)
│   on_click → selectPeriod(last_month) — transform_state
└── period_3_months    "3 months"   (unselected)
    on_click → selectPeriod(3_months) — transform_state

empty_state/ (vertically centred in remaining viewport, padding horizontal 32dp)
│   accessibility_label: "No spending data for this period"
├── icon  (pie_chart 48dp #41474D, decorative:false,
│          contentDescription: "No spending data")
├── title (headlineSmall 24sp/32sp w400 #181C20 center):
│         "No spending data"
└── body  (bodyMedium 14sp/20sp w400 #41474D center):
          "No debit transactions were found for this period. Try a different time window or check back later."

BottomNav/ (persistent)
├── tab Home (unselected #41474D) | Accounts | Transactions | More
```

---

### State: error

(EC-SBC-002 — Room query or in-memory aggregation throws exception)

```
┌─────────────────────────────────────────────┐
│ ←  Spending by Category                     │  ← top_app_bar bg #F7F9FF h 64dp
├─────────────────────────────────────────────┤
│                                              │
│ (This month ✓)  (Last month)  (3 months) → │  ← period_selector (visible, bound to error)
│                                              │
│                                              │
│                                              │
│              [warning_amber]                │  ← icon warning_amber 48dp #BA1A1A centred
│                                              │
│       Unable to compute spending            │  ← title headlineSmall 24sp/32sp #181C20
│                                              │    centred weight 400
│   There was a problem reading your          │
│   transaction data. Your cached             │  ← body bodyMedium 14sp/20sp #41474D
│   data may be unavailable.                  │    centred, padding h 32dp
│                                              │
│        [ ◎  Try again ]                     │  ← retry_button tonal variant
│                                              │    bg #C9E6FF text #004B6F h 48dp
│                                              │    radius 9999, min touch 48dp
│                                              │    margin h 32dp
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
Screen: Spending by Category (SpendingByCategoryUiState.Error — EC-SBC-002)
│
top_app_bar/ (SmallTopAppBar, bg #F7F9FF, h 64dp)
├── leading: back_arrow (icon arrow_back 24dp #266489)
└── title: "Spending by Category" (titleLarge 22sp w400 #181C20)

period_selector/ (chip_group h-scroll — visible in error state per state_binding)
│   accessibility_label: "Period filter"
├── period_this_month  "This month" (selected, bg #C9E6FF text #004B6F)
│   on_click → selectPeriod(this_month)
├── period_last_month  "Last month" (unselected)
│   on_click → selectPeriod(last_month)
└── period_3_months    "3 months"   (unselected)
    on_click → selectPeriod(3_months)

error_state/ (vertically centred in remaining viewport, padding horizontal 32dp)
│   accessibility_label: "Unable to compute your spending breakdown"
├── icon  (warning_amber 48dp #BA1A1A, decorative:false,
│          contentDescription: "Computation error")
├── title (headlineSmall 24sp/32sp w400 #181C20 center):
│         "Unable to compute spending"
├── body  (bodyMedium 14sp/20sp w400 #41474D center):
│         "There was a problem reading your transaction data. Your cached data may be unavailable."
└── retry_button (button variant:tonal, h 48dp, bg #C9E6FF label-color #004B6F,
                  radius 9999, min touch 48dp, margin top 16dp h 32dp)
    label: "Try again"
    accessibility_label: "Try again"
    on_click → retryCompute(period:selected_period) — transform_state,
               re-triggers category_spend_compute from local Room cache (no network call)

BottomNav/ (persistent)
├── tab Home (unselected #41474D) | Accounts | Transactions | More
```

---

### Interaction Summary

| Component | Action | Effect | Target / Behaviour |
|---|---|---|---|
| period_this_month chip | select_period (period: this_month) | transform_state | Re-aggregates cached Room debit transactions for the current calendar month by category; no network call; transitions UiState loading → content \| empty \| error |
| period_last_month chip | select_period (period: last_month) | transform_state | Re-aggregates cached Room debit transactions for the previous calendar month by category; no network call |
| period_3_months chip | select_period (period: 3_months) | transform_state | Re-aggregates cached Room debit transactions for the last 90 days by category; no network call |
| category_row[Bills] | navigate_category_transactions (category: "Bills") | navigate | transactions screen, categoryFilter=Bills URI-encoded; shows all debit transactions contributing to Bills spend total |
| category_row[Groceries] | navigate_category_transactions (category: "Groceries") | navigate | transactions screen, categoryFilter=Groceries URI-encoded |
| category_row[Dining] | navigate_category_transactions (category: "Dining") | navigate | transactions screen, categoryFilter=Dining URI-encoded |
| category_row[Subscriptions] | navigate_category_transactions (category: "Subscriptions") | navigate | transactions screen, categoryFilter=Subscriptions URI-encoded |
| category_row[Transport] | navigate_category_transactions (category: "Transport") | navigate | transactions screen, categoryFilter=Transport URI-encoded |
| retry_button (error) | retry_compute (period: selected_period) | transform_state | Re-triggers category_spend_compute for the currently selected period from local Room cache; no network call; transitions error → loading → content \| empty \| error |

---

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| top_app_bar | match_parent | 64dp | 0 |
| period_chip (single) | hug content (min 48dp touch) | 32dp | 9999dp (full pill) |
| period_chip_group scroll container | match_parent | 48dp | 0 |
| spend_summary_card | match_parent − 32dp | wrap (~80dp) | 12dp |
| category_row content area | match_parent | 56dp (row) + 20dp (progress) = 76dp | 0 (divider list style) |
| category_progress_bar | match_parent − 32dp | 4dp | 2dp |
| skeleton_card | match_parent − 32dp | 80dp | 12dp |
| skeleton_text | 60% (match_parent − 32dp) | 16dp | 8dp |
| skeleton_block_1 / _2 / _3 | match_parent − 32dp | 56dp | 8dp |
| empty_state / error_state icon container | 48dp | 48dp | 9999dp (circular) |
| retry_button | match_parent − 64dp | 48dp | 9999dp (full pill) |
| bottom_nav bar | match_parent | 80dp | 0 |
