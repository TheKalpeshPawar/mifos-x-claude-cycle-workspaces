# PFM Dashboard — Visual Mockup

> Auto-generated from `screens/pfm-dashboard/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-17T06:00:00Z

---

## Screen: My Finances

Canvas: 393×852dp (Pixel 5) · Top app bar visible · Bottom nav visible · No FAB · Roboto font · Material 3 light theme · bg #F7F9FF

Shell (from `app-shell.yaml` + `ui.yaml#shell`):
Top app bar: enabled, small variant, title = "My Finances" (titleMedium 16sp/24sp w500 #181C20), bg #F7F9FF, no trailing actions.
Bottom navigation: Home | Accounts | Transactions | More — icons: home / account_balance / receipt_long / more_horiz — bg #F7F9FF, h 80dp.
pfm-dashboard is NOT a bottom nav tab — it is reached from the Home screen spending snapshot card (navigateToPfm). No nav item is highlighted on this screen (all tabs unselected, tint #41474D). The old nav label "PFM" in slot 3 was incorrect and has been removed.
FAB: hidden per `ui.yaml#shell.fab_visible: false`.

---

### State: loading

```
┌─────────────────────────────────────────────┐
│  My Finances                                 │  ← top_app_bar small, bg #F7F9FF
│                                              │    title titleMedium 16sp/24sp w500 #181C20
├─────────────────────────────────────────────┤
│                                              │  [scroll starts; padding horizontal 16dp]
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │  ← shimmer row 1: h=120dp, radius 12dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │    #DDE3EA surfaceVariant, pulse 1.5s
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │    skeleton: net worth card
│                                              │    gap 16dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │  ← shimmer row 2: h=80dp, radius 12dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │    skeleton: spend/income chart card
│                                              │    gap 16dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │  ← shimmer row 3: h=200dp, radius 12dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │    skeleton: top categories list
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │
│                                              │    gap 16dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │  ← shimmer row 4: h=80dp, radius 12dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │    skeleton: insight cards
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More │  ← bottom_nav h 80dp bg #F7F9FF
└─────────────────────────────────────────────┘    all tabs unselected tint #41474D
```

### Component Hierarchy — loading

```
Screen: My Finances (PfmDashboardUiState.Loading)
│
loading_shimmer/ (shimmer rows=4, stack vertical gap 16dp,
│                 padding horizontal 16dp top 16dp bottom 16dp)
│   accessibility_label: "Loading your finances overview"
│   reduce-motion: static fill (no pulse animation)
│
├── shimmer_row_1  (variant:card, h=120dp, radius 12dp, width match_parent−32dp)
│                   skeleton of net_worth_card
├── shimmer_row_2  (variant:card, h=80dp,  radius 12dp, width match_parent−32dp)
│                   skeleton of spending_income_card
├── shimmer_row_3  (variant:card, h=200dp, radius 12dp, width match_parent−32dp)
│                   skeleton of top_categories list (accounts for 8 rows + header)
└── shimmer_row_4  (variant:card, h=80dp,  radius 12dp, width match_parent−32dp)
                    skeleton of insights section

BottomNav/ (persistent, always rendered)
├── Home         (icon:home,          label:"Home",         unselected, tint #41474D)
├── Accounts     (icon:account_balance,label:"Accounts",    unselected, tint #41474D)
├── Transactions (icon:receipt_long,  label:"Transactions", unselected, tint #41474D)
└── More         (icon:more_horiz,    label:"More",         unselected, tint #41474D)
```

---

### State: content

Screen scrolls vertically. Canvas 393×852dp; content exceeds viewport — user scrolls to reach insights and chips. Bottom nav persists as overlay.

```
┌─────────────────────────────────────────────┐
│  My Finances                                 │  ← top_app_bar small bg #F7F9FF
│                                              │    titleMedium 16sp #181C20
├─────────────────────────────────────────────┤
│                                              │  padding top 12dp horizontal 16dp
│  ┌──────────────────────────────────────┐   │  ← period_selector segmented_button
│  │ [ 7 days ]  [ 30 days ✓ ]  [3 months]│  │    h 40dp, unselected bg #EBEEF3 text #41474D
│  └──────────────────────────────────────┘   │    selected bg #C9E6FF text #004B6F radius 9999
│                                              │    (default selected: "30 days")
│ ┌─────────────────────────────────────────┐ │  ← net_worth_card elevation 2 (3dp shadow)
│ │  Net worth                              │ │    bg #EBEEF3 radius 12dp padding 16dp
│ │                                          │ │    margin h 0dp (padded by screen 16dp)
│ │  £14,955.45                             │ │  ← net_worth_amount displaySmall 36sp #266489
│ │  Across 3 accounts                      │ │  ← net_worth_sub bodySmall 12sp #41474D
│ │  ─────────────────────────────────────  │ │    divider #DDE3EA 1dp
│ │  Everyday Current         £2,847.63     │ │  ← breakdown_current list_item compact
│ │  ISA Saver               £12,450.00     │ │  ← breakdown_savings list_item compact
│ │  Platinum Mastercard       −£342.18     │ │  ← breakdown_credit trailing_color #BA1A1A
│ └─────────────────────────────────────────┘ │
│                                              │
│  Spending vs Income                         │  ← spending_income_header titleSmall
│                                              │    14sp/20sp w500 #41474D (onSurfaceVariant)
│ ┌─────────────────────────────────────────┐ │  ← spending_income_card elevation 1 (1dp)
│ │                                          │ │    bg #F1F4F9 radius 12dp padding 16dp
│ │    ▐████▌          ▐███▌                │ │  ← spending_income_bars bar_chart
│ │    ▐████▌          ▐███▌                │ │    Income bar #266489 (height 7 units ≈ £2,400)
│ │    ▐████▌          ▐███▌                │ │    Spend bar  #BA1A1A (height 5 units ≈ £1,840)
│ │    ▐████▌          ▐███▌                │ │
│ │    ▐████▌          ▐███▌                │ │
│ │    Income          Spend                 │ │    labelSmall 11sp #41474D below bars
│ │    £2,400.00       £1,840.00            │ │
│ │                                          │ │
│ │  ✓ You saved £560.00 this period        │ │  ← net_cashflow_label labelMedium 12sp #266489
│ └─────────────────────────────────────────┘ │    (net_cashflow_direction positive → primary)
│                                              │
│  Top spending categories                    │  ← top_categories_header titleSmall #41474D
│                                              │
│  Bills · 4 transactions          £1,356.00  │  ← category_row list_item, tappable
│  ████████████████████████████████████████   │    progress_linear #266489 73.7%
│                                              │    (progress bar h 4dp radius 2dp)
│  Groceries · 9 transactions        £198.00  │
│  ██████                                     │    10.8%
│                                              │
│  Dining · 5 transactions            £88.00  │
│  ███                                        │    4.8%
│                                              │
│  Subscriptions · 5 transactions     £63.00  │
│  ██                                         │    3.4%
│                                              │
│  Transport · 8 transactions         £41.00  │
│  █                                          │    2.2%
│                                              │
│  Entertainment · 3 transactions     £32.00  │
│  █                                          │    1.7%
│                                              │
│  Health · 2 transactions            £22.00  │
│  █                                          │    1.2%
│                                              │
│  Other · 6 transactions             £40.00  │
│  █                                          │    2.2%
│                                              │
│                [ View all categories → ]    │  ← view_all_categories text_button
│                                              │    labelMedium 12sp #266489
│  Insights                                   │  ← insights_header titleSmall #41474D
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← insight_card[0] elevation 1 radius 12dp
│ │  📈  Dining is up this month            │ │    bg #F1F4F9 padding 16dp
│ │      You spent £88 on dining in the    │ │    icon trending_up 20dp #266489
│ │      last 30 days, 14% more than the   │ │    title titleSmall 14sp #181C20
│ │      prior period (£77).               │ │    body bodySmall 12sp #41474D
│ └─────────────────────────────────────────┘ │
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← insight_card[1] elevation 1 radius 12dp
│ │  👍  Healthy savings rate               │ │    icon thumb_up 20dp #266489
│ │      You saved £560 this period —      │ │
│ │      23% of your income.               │ │
│ │      Great work, Priya!                 │ │
│ └─────────────────────────────────────────┘ │
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← insight_card[2] elevation 1 radius 12dp
│ │  📉  Transport spending down            │ │    icon trending_down 20dp #266489
│ │      Transport costs fell to £41 from  │ │
│ │      £51 last month — £10 saved on     │ │
│ │      your commute.                      │ │
│ └─────────────────────────────────────────┘ │
│                                              │
│  ┤◯ pie_chart By category┤ ┤◯ savings Budgets┤ ┤◯ autorenew Subscriptions┤ →  │
│  ← pfm_nav_chips chip_group horizontal scroll, chip h 32dp radius 9999    │
│    outline #72787E bg transparent, icon+label #41474D                      │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
Screen: My Finances (PfmDashboardUiState.Content)
│   [scrollable column, padding horizontal 16dp, bottom 32dp]
│
period_selector/ (segmented_button, 3 options, h 40dp, width match_parent,
│                 margin top 12dp bottom 16dp)
├── option[0]  period_7d    label:"7 days"   value:"7d"    unselected (#EBEEF3, text #41474D)
├── option[1]  period_30d   label:"30 days"  value:"30d"   selected   (#C9E6FF, text #004B6F)
└── option[2]  period_3m    label:"3 months" value:"3m"    unselected (#EBEEF3, text #41474D)
    on_click → selectPeriod(period: selected.value)  —  re-triggers loadFinancesOverview

net_worth_card/ (card elevation:2 bg:#EBEEF3 radius:12dp padding:16dp,
│               margin bottom 16dp; display only, no click)
│  stack vertical gap 4dp:
├── net_worth_label   (labelMedium 12sp/16sp w500 #50606E): "Net worth"
│                      accessibility_label: "Net worth section"
├── net_worth_amount  (displaySmall 36sp/44sp w400 #266489): "£14,955.45"
│                      accessibility_label: "Net worth £14,955.45"
├── net_worth_sub     (bodySmall 12sp/16sp w400 #41474D): "Across 3 accounts"
│   [divider 1dp #DDE3EA, margin vertical 8dp]
└── net_worth_breakdown/ (stack vertical spacing:4dp)
    ├── breakdown_current  (list_item compact, h 32dp): "Everyday Current    £2,847.63"
    │                       a11y: "Everyday current account balance £2,847.63"
    ├── breakdown_savings  (list_item compact, h 32dp): "ISA Saver          £12,450.00"
    │                       a11y: "ISA saver account balance £12,450.00"
    └── breakdown_credit   (list_item compact, h 32dp): "Platinum Mastercard  −£342.18"
                            trailing_color #BA1A1A
                            a11y: "Platinum Mastercard outstanding balance −£342.18"

spending_income_header/ (text titleSmall 14sp/20sp w500 #41474D, margin bottom 8dp):
│                         "Spending vs Income"

spending_income_card/ (card elevation:1 bg:#F1F4F9 radius:12dp padding:16dp,
│                      margin bottom 16dp; display only, no click)
│  stack vertical gap 12dp:
├── spending_income_bars/ (bar_chart, dual bars, h ~80dp)
│   ├── income_bar  (label:"Income",  value:2400.00, color:#266489  primary)
│   │               a11y: "Income £2,400.00"
│   └── spend_bar   (label:"Spend",   value:1840.00, color:#BA1A1A  error)
│                   a11y: "Spending £1,840.00"
└── net_cashflow_label (labelMedium 12sp/16sp w500 #266489):
                        "You saved £560.00 this period"
                        a11y: "Net saving of £560.00 this period"

top_categories_header/ (text titleSmall 14sp/20sp w500 #41474D, margin bottom 8dp):
│                        "Top spending categories"

top_categories_list/ (stack vertical spacing:4dp, items_source: top_categories)
│   Each category_row: list_item + progress_linear child; tappable → navigate
│
├── category_row[Bills]        (list_item compact tappable)
│   ├── label "Bills"    supporting "4 transactions"    trailing "£1,356.00"
│   └── category_spend_bar (progress_linear value:73.7 max:100 color:#266489 h:4dp)
│       a11y: "Bills represents 73.7% of total spending"
│   on_click → navigateSpendingByCategory(category:"Bills")
│
├── category_row[Groceries]    (list_item compact tappable)
│   ├── label "Groceries"  supporting "9 transactions"  trailing "£198.00"
│   └── category_spend_bar (progress_linear value:10.8 max:100 color:#266489 h:4dp)
│   on_click → navigateSpendingByCategory(category:"Groceries")
│
├── category_row[Dining]       (list_item compact tappable)
│   ├── label "Dining"  supporting "5 transactions"  trailing "£88.00"
│   └── category_spend_bar (progress_linear value:4.8 max:100 color:#266489 h:4dp)
│   on_click → navigateSpendingByCategory(category:"Dining")
│
├── category_row[Subscriptions](list_item compact tappable)
│   ├── label "Subscriptions"  supporting "5 transactions"  trailing "£63.00"
│   └── category_spend_bar (progress_linear value:3.4 max:100 color:#266489 h:4dp)
│   on_click → navigateSpendingByCategory(category:"Subscriptions")
│
├── category_row[Transport]    (list_item compact tappable)
│   ├── label "Transport"  supporting "8 transactions"  trailing "£41.00"
│   └── category_spend_bar (progress_linear value:2.2 max:100 color:#266489 h:4dp)
│   on_click → navigateSpendingByCategory(category:"Transport")
│
├── category_row[Entertainment](list_item compact tappable)
│   ├── label "Entertainment"  supporting "3 transactions"  trailing "£32.00"
│   └── category_spend_bar (progress_linear value:1.7 max:100 color:#266489 h:4dp)
│   on_click → navigateSpendingByCategory(category:"Entertainment")
│
├── category_row[Health]       (list_item compact tappable)
│   ├── label "Health"  supporting "2 transactions"  trailing "£22.00"
│   └── category_spend_bar (progress_linear value:1.2 max:100 color:#266489 h:4dp)
│   on_click → navigateSpendingByCategory(category:"Health")
│
└── category_row[Other]        (list_item compact tappable)
    ├── label "Other"  supporting "6 transactions"  trailing "£40.00"
    └── category_spend_bar (progress_linear value:2.2 max:100 color:#266489 h:4dp)
    on_click → navigateSpendingByCategory(category:"Other")

view_all_categories/ (text_button labelMedium 12sp #266489, align:end, margin vertical 8dp)
│   label: "View all categories"
│   a11y:  "View all spending categories"
│   on_click → navigateSpendingByCategory(category: null) — no category pre-filter

insights_header/ (text titleSmall 14sp/20sp w500 #41474D, margin top 8dp bottom 8dp):
│               "Insights"

insights_list/ (stack vertical spacing:8dp, items_source: insights)
│
├── insight_card[0]/ (card elevation:1 bg:#F1F4F9 radius:12dp padding:16dp)
│   stack horizontal gap 12dp alignment:top:
│   ├── insight_icon   (icon trending_up 20dp #266489, decorative:false,
│   │                   contentDescription: "Trending up")
│   └── stack vertical gap 4dp weight:1:
│       ├── insight_title (titleSmall 14sp/20sp w500 #181C20):
│       │                  "Dining is up this month"
│       └── insight_body  (bodySmall 12sp/16sp w400 #41474D):
│                          "You spent £88 on dining in the last 30 days, 14% more than the prior period (£77)."
│
├── insight_card[1]/ (card elevation:1 bg:#F1F4F9 radius:12dp padding:16dp)
│   ├── insight_icon   (icon thumb_up 20dp #266489)
│   ├── insight_title  "Healthy savings rate"
│   └── insight_body   "You saved £560 this period — 23% of your income. Great work, Priya!"
│
└── insight_card[2]/ (card elevation:1 bg:#F1F4F9 radius:12dp padding:16dp)
    ├── insight_icon   (icon trending_down 20dp #266489)
    ├── insight_title  "Transport spending down"
    └── insight_body   "Transport costs fell to £41 from £51 last month — £10 saved on your commute."

pfm_nav_chips/ (chip_group, scroll_direction:horizontal, h 32dp, padding v 8dp,
│               gap 8dp between chips)
├── chip_spending/     (chip icon:pie_chart  label:"By category"   outline:#72787E)
│   a11y: "Go to spending by category"
│   on_click → navigateSpendingByCategory(category: null)
│
├── chip_budgets/      (chip icon:savings    label:"Budgets"        outline:#72787E)
│   a11y: "Go to budgets"
│   on_click → navigateBudgets()
│
└── chip_subscriptions/(chip icon:autorenew label:"Subscriptions"  outline:#72787E)
    a11y: "Go to recurring subscriptions"
    on_click → navigateRecurringSubscriptions()

BottomNav/ (persistent)
├── Home         (icon:home,          label:"Home",         unselected, tint #41474D)
├── Accounts     (icon:account_balance,label:"Accounts",    unselected, tint #41474D)
├── Transactions (icon:receipt_long,  label:"Transactions", unselected, tint #41474D)
└── More         (icon:more_horiz,    label:"More",         unselected, tint #41474D)
```

---

### State: empty

Shown when no transactions exist in the local Room/SQLDelight pfm_cache.db after account sync (EC-PFM-001). Period selector is NOT shown — there is no data to compute with.

```
┌─────────────────────────────────────────────┐
│  My Finances                                 │  ← top_app_bar small bg #F7F9FF
│                                              │
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│                                              │
│               [bar_chart]                    │  ← icon bar_chart 48dp #41474D centred
│                                              │    contentDescription: "No spending data"
│                                              │
│     No transaction data yet                 │  ← title headlineSmall 24sp/32sp #181C20
│                                              │    text-align centre
│   Your spending overview will appear once   │  ← body bodyMedium 14sp/20sp #41474D
│   your transactions are loaded from the     │    text-align centre
│   AIS connection.                           │    padding horizontal 32dp
│                                              │
│                                              │
│                                              │
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: My Finances (PfmDashboardUiState.Empty — EC-PFM-001: no cached transactions)
│
empty_state_view/ (empty_state, vertically centred, padding horizontal 32dp)
│   accessibility_label: "No transaction data yet. Your spending overview will appear once transactions are loaded."
│
├── icon  (bar_chart 48dp #41474D, decorative:false,
│          contentDescription: "No spending data available")
├── title (headlineSmall 24sp/32sp w400 #181C20 align:center):
│         "No transaction data yet"
└── body  (bodyMedium 14sp/20sp w400 #41474D align:center):
          "Your spending overview will appear once your transactions are loaded from the AIS connection."

NOTE: No retry button for EC-PFM-001 (empty cache is not an error; data loads passively as AIS syncs).

BottomNav/ (persistent — no tab selected)
```

---

### State: error

Shown when an exception occurs during Room/SQLDelight read or aggregation computation (EC-PFM-002). Includes a retry button that re-dispatches `reloadFinances`.

```
┌─────────────────────────────────────────────┐
│  My Finances                                 │  ← top_app_bar small bg #F7F9FF
│                                              │
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│             [warning_amber]                  │  ← icon warning_amber 48dp #BA1A1A centred
│                                              │    contentDescription: "Error loading finances"
│                                              │
│     Could not load your finances            │  ← title headlineSmall 24sp/32sp #181C20
│                                              │    text-align centre
│   Something went wrong while computing     │  ← body bodyMedium 14sp/20sp #41474D
│   your finances overview.                  │    text-align centre
│   Please try again.                         │    padding horizontal 32dp
│                                              │
│         [      Try again      ]              │  ← retry button (error_view action)
│                                              │    variant:filled, h 56dp, bg #266489
│                                              │    label #FFFFFF, radius 9999
│                                              │    → reloadFinances()
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
Screen: My Finances (PfmDashboardUiState.Error — EC-PFM-002: AggregationError)
│
error_view/ (error_state, vertically centred, padding horizontal 32dp)
│   accessibility_label: "Could not load your finances. Something went wrong. Try again button available."
│
├── icon  (warning_amber 48dp #BA1A1A, decorative:false,
│          contentDescription: "Error loading finances")
├── title (headlineSmall 24sp/32sp w400 #181C20 align:center):
│         "Could not load your finances"
├── body  (bodyMedium 14sp/20sp w400 #41474D align:center):
│         "Something went wrong while computing your finances overview. Please try again."
└── pfm_error_retry_button (id:pfm_error_retry_button, button variant:filled, h 56dp,
                            bg #266489, label-color #FFFFFF, radius 9999, min-touch 56dp)
    label: "Try again"             [resolves {strings.pfm_dashboard.error.retry}]
    accessibility_label: "Retry loading your finances"
    action_contract: effect:transform_state, external_library_refs:[kotlinx-coroutines]
    on_click → reloadFinances()  — re-dispatches loadFinancesOverview(selectedPeriod) via
                                   kotlinx-coroutines; transitions: error → loading → content | empty | error

BottomNav/ (persistent — no tab selected)
```

---

### Interaction Summary

| Component | Action | Effect | Target / Behaviour |
|---|---|---|---|
| period_selector | select_period | transform_state | In-place re-computation: switches PfmPeriod (7d/30d/3m); re-triggers loadFinancesOverview with new kotlinx-datetime window; net worth unchanged, period metrics recomputed; transitions content → loading → content \| error |
| category_row (Bills) | navigate_spending_by_category | navigate | spending-by-category screen, param category:"Bills" — pre-filters AIS debits to this MerchantCategory for the selected PFM period |
| category_row (Groceries) | navigate_spending_by_category | navigate | spending-by-category screen, param category:"Groceries" |
| category_row (Dining) | navigate_spending_by_category | navigate | spending-by-category screen, param category:"Dining" |
| category_row (Subscriptions) | navigate_spending_by_category | navigate | spending-by-category screen, param category:"Subscriptions" |
| category_row (Transport) | navigate_spending_by_category | navigate | spending-by-category screen, param category:"Transport" |
| category_row (Entertainment) | navigate_spending_by_category | navigate | spending-by-category screen, param category:"Entertainment" |
| category_row (Health) | navigate_spending_by_category | navigate | spending-by-category screen, param category:"Health" |
| category_row (Other) | navigate_spending_by_category | navigate | spending-by-category screen, param category:"Other" |
| view_all_categories | navigate_spending_by_category | navigate | spending-by-category screen, no category filter — shows all AIS debit categories ranked by amount |
| chip_spending | navigate_spending_by_category | navigate | spending-by-category screen, no category pre-filter |
| chip_budgets | navigate_budgets | navigate | budgets screen — monthly spend targets vs actuals |
| chip_subscriptions | navigate_recurring_subscriptions | navigate | recurring-subscriptions screen — detected standing orders and regular subscription debits |
| pfm_error_retry_button | reload_finances | transform_state | Retry from error state; re-dispatches reloadFinances() → loadFinancesOverview(selectedPeriod) via kotlinx-coroutines; transitions error → loading → content \| empty \| error |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| period_selector | match_parent − 32dp | 40dp | 9999dp (pill segments) |
| net_worth_card | match_parent − 32dp | wrap (~172dp) | 12dp |
| breakdown_current / breakdown_savings / breakdown_credit | match_parent | 32dp | 0 |
| spending_income_card | match_parent − 32dp | wrap (~120dp) | 12dp |
| spending_income_bars | match_parent − 32dp | 80dp | 0 |
| category_row (each) | match_parent − 32dp | wrap (~56dp) | 8dp |
| category_spend_bar (progress) | match_parent | 4dp | 2dp |
| insight_card (each) | match_parent − 32dp | wrap (~80dp) | 12dp |
| insight_icon | 20dp | 20dp | — |
| chip (each) | hug content min 80dp | 32dp | 9999dp (full pill) |
| retry_button (error) | match_parent − 64dp | 56dp | 9999dp (full pill) |
| empty icon | 48dp | 48dp | — |
| error icon | 48dp | 48dp | — |
| bottom_nav | match_parent | 80dp | 0 |
