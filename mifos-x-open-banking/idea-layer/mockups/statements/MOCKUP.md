# Statements — Visual Mockup

> Auto-generated from `screens/statements/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Statements

Canvas: 393×852dp (Pixel 5) · Top app bar: small variant, title "Statements", leading back arrow · Bottom nav visible · No FAB · Roboto font · Material 3 light theme · bg #F7F9FF

Shell (from `app-shell.yaml` + `ui.yaml#shell`):
- Top app bar: small variant, h 64dp, bg #F7F9FF, title "Statements" (titleLarge 22sp #181C20), leading arrow_back tint #266489. Per `ui.yaml#shell.top_app_bar_leading: back`.
- Bottom navigation: Home | Accounts | Transactions | More. Icons: home / account_balance / receipt_long / more_horiz. bg #F7F9FF, h 80dp. This is a sub-screen reached via tap — no tab is selected/highlighted.
- FAB: hidden per `ui.yaml#shell.fab_visible: false`.

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Statements                                │  ← top_app_bar: bg #F7F9FF, h 64dp
│                                              │    leading: arrow_back 24dp tint #266489
│                                              │    title: "Statements" titleLarge 22sp #181C20
├─────────────────────────────────────────────┤  ← content area starts, padding 16dp
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← skeleton_row_1: 361×72dp
│  ░  shimmer placeholder row 1  ░░░░░░░░░░  │    radius 8dp, bg #DDE3EA (surfaceVariant)
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │    shimmer pulse animation 1.5s loop
│                                              │    gap 12dp below
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← skeleton_row_2: 361×72dp
│  ░  shimmer placeholder row 2  ░░░░░░░░░░  │    radius 8dp, bg #DDE3EA
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │    delay +0.2s for cascade effect
│                                              │    gap 12dp below
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← skeleton_row_3: 361×72dp
│  ░  shimmer placeholder row 3  ░░░░░░░░░░  │    radius 8dp, bg #DDE3EA
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │    delay +0.4s for cascade effect
│                                              │
│  [remainder of content area empty / bg]     │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← bottom_nav: bg #F7F9FF, h 80dp
└─────────────────────────────────────────────┘
```

### Component Hierarchy — loading

```
Screen: Statements (StatementsUiState.Loading)
│
TopAppBar/ (small variant, bg #F7F9FF, elevation level0, h 64dp)
│   ├── leading: NavigationIcon arrow_back
│   │           (icon 24dp, tint #266489, touch target 48dp×48dp)
│   │           → navigation back to previous screen (account-detail)
│   └── title: "Statements"
│              (titleLarge 22sp/28sp w400 #181C20, truncate if needed)
│
statements_skeleton/ (Column, scroll: false, padding 16dp, gap 12dp between items)
│   accessibility_label: "Loading statements" (reduce-motion: static #DDE3EA fill, no animation)
│
├── skeleton_row_1 (shimmer variant:list, 361dp×72dp, radius 8dp,
│                   bg #DDE3EA, pulse animation 1.5s, delay 0s)
├── skeleton_row_2 (shimmer variant:list, 361dp×72dp, radius 8dp,
│                   bg #DDE3EA, pulse animation 1.5s, delay 0.2s)
└── skeleton_row_3 (shimmer variant:list, 361dp×72dp, radius 8dp,
                    bg #DDE3EA, pulse animation 1.5s, delay 0.4s)

BottomNav/ (persistent, fixed bottom, h 80dp, bg #F7F9FF)
├── tab Home         (icon: home,            label: "Home",         tint #41474D, unselected)
├── tab Accounts     (icon: account_balance,  label: "Accounts",     tint #41474D, unselected)
├── tab Transactions (icon: receipt_long,     label: "Transactions", tint #41474D, unselected)
└── tab More         (icon: more_horiz,       label: "More",         tint #41474D, unselected)
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← Statements                                │  ← top_app_bar: bg #F7F9FF, h 64dp
│                                              │
├─────────────────────────────────────────────┤  ← lazy_column starts (padding 0dp)
│                                              │
│  May 2026                              [⬇]  │  ← statement_row[0], min h 72dp, bg #F7F9FF
│  Closing balance: £2,847.63                 │    headline: bodyLarge 16sp/24sp w400 #181C20
│  1 May 2026 – 31 May 2026                   │    supporting: bodyMedium 14sp/20sp w400 #41474D
│                                              │    trailing date: bodySmall 12sp/16sp #41474D
│  ─────────────────────────────────────────  │  ← statement_row_divider: 1dp #C1C7CE
│                                              │
│  April 2026                            [⬇]  │  ← statement_row[1], min h 72dp, bg #F7F9FF
│  Closing balance: £2,610.40                 │    ripple on tap → navigate_statement_detail
│  1 Apr 2026 – 30 Apr 2026                   │    [⬇] = download_statement_button idle
│                                              │          icon: file_download 24dp tint #266489
│  ─────────────────────────────────────────  │          touch target 48dp×48dp
│                                              │
│  March 2026                            [⬇]  │  ← statement_row[2], min h 72dp, bg #F7F9FF
│  Closing balance: £2,314.92                 │
│  1 Mar 2026 – 31 Mar 2026                   │
│                                              │
│  ─────────────────────────────────────────  │
│                                              │
│  February 2026                         [⬇]  │  ← statement_row[3], min h 72dp, bg #F7F9FF
│  Closing balance: £1,988.57                 │
│  1 Feb 2026 – 28 Feb 2026                   │
│                                              │
│  ─────────────────────────────────────────  │
│                                              │
│  January 2026                          [⬇]  │  ← statement_row[4], min h 72dp, bg #F7F9FF
│  Closing balance: £1,754.10                 │
│  1 Jan 2026 – 31 Jan 2026                   │
│                                              │
│  ─────────────────────────────────────────  │
│                                              │
│  December 2025                         [⬇]  │  ← statement_row[5], min h 72dp, bg #F7F9FF
│  Closing balance: £1,502.88                 │    [last row — no divider after]
│  1 Dec 2025 – 31 Dec 2025                   │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘

  Download in-progress variant for statement_row:
  ┌────────────────────────────────────────────┐
  │  May 2026                            [◌]   │  ← [◌] = CircularProgressIndicator
  │  Closing balance: £2,847.63                │    24dp, tint #266489 (replaces file_download)
  │  1 May 2026 – 31 May 2026                  │    downloadState[STMT-2026-05] == InProgress
  └────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
Screen: Statements (StatementsUiState.Content — 6 statements from demo-data.yaml, DESC)
│
TopAppBar/ (small variant, bg #F7F9FF, elevation level0)
│   ├── leading: arrow_back (24dp, tint #266489, touch 48dp) → navigate_back
│   └── title: "Statements" (titleLarge 22sp #181C20)
│
statements_list/ (LazyColumn, scroll: vertical, padding 0dp, bg #F7F9FF)
│   accessibility_label: "Statement list, sorted most recent first"
│   items_source: statements sorted DESC by StartDateTime
│
├── statement_row[0] (ListItem, minHeight 72dp, bg #F7F9FF, clickable + ripple)
│   content layout: Row(padding h 16dp v 12dp, verticalAlignment CenterVertically)
│   ├── Column(weight 1, gap 4dp):
│   │   ├── headline  (bodyLarge 16sp/24sp w400 #181C20): "May 2026"
│   │   └── supporting (bodyMedium 14sp/20sp w400 #41474D): "Closing balance: £2,847.63"
│   └── Column(horizontalAlignment End, gap 4dp):
│       ├── trailing_date (bodySmall 12sp/16sp w400 #41474D): "1 May 2026 – 31 May 2026"
│       └── download_statement_button[STMT-2026-05-40051512345678]
│           (IconButton standard, touch 48dp×48dp, stopPropagation=true)
│           idle:       Icon(file_download, 24dp, tint #266489)
│           in-progress: CircularProgressIndicator(size 24dp, strokeWidth 2dp, tint #266489)
│           accessibility_label (idle): "Download May 2026 statement"
│           loading_accessibility_label: "Downloading May 2026 statement"
│           on_click → download_statement(STMT-2026-05-40051512345678, 40051512345678)
│               action_contract: effect=persist_file
│               calls GET /accounts/40051512345678/statements/STMT-2026-05.../file
│               streams PDF/CSV → platform file handler
│   on_click → navigate_statement_detail(STMT-2026-05-40051512345678, 40051512345678)
│       action_contract: effect=navigate, target=statement-detail
│
├── statement_row_divider (HorizontalDivider, h 1dp, color #C1C7CE, match_parent)
│
├── statement_row[1] (ListItem, minHeight 72dp, bg #F7F9FF, ripple)
│   ├── headline: "April 2026"  · supporting: "Closing balance: £2,610.40"
│   ├── trailing_date: "1 Apr 2026 – 30 Apr 2026"
│   └── download_statement_button[STMT-2026-04-40051512345678]
│   on_click → navigate_statement_detail(STMT-2026-04-40051512345678, 40051512345678)
│
├── statement_row_divider
│
├── statement_row[2] (ListItem, minHeight 72dp, bg #F7F9FF, ripple)
│   ├── headline: "March 2026"  · supporting: "Closing balance: £2,314.92"
│   ├── trailing_date: "1 Mar 2026 – 31 Mar 2026"
│   └── download_statement_button[STMT-2026-03-40051512345678]
│   on_click → navigate_statement_detail(STMT-2026-03-40051512345678, 40051512345678)
│
├── statement_row_divider
│
├── statement_row[3] (ListItem, minHeight 72dp, bg #F7F9FF, ripple)
│   ├── headline: "February 2026"  · supporting: "Closing balance: £1,988.57"
│   ├── trailing_date: "1 Feb 2026 – 28 Feb 2026"
│   └── download_statement_button[STMT-2026-02-40051512345678]
│   on_click → navigate_statement_detail(STMT-2026-02-40051512345678, 40051512345678)
│
├── statement_row_divider
│
├── statement_row[4] (ListItem, minHeight 72dp, bg #F7F9FF, ripple)
│   ├── headline: "January 2026"  · supporting: "Closing balance: £1,754.10"
│   ├── trailing_date: "1 Jan 2026 – 31 Jan 2026"
│   └── download_statement_button[STMT-2026-01-40051512345678]
│   on_click → navigate_statement_detail(STMT-2026-01-40051512345678, 40051512345678)
│
├── statement_row_divider
│
└── statement_row[5] (ListItem, minHeight 72dp, bg #F7F9FF, ripple)
    ├── headline: "December 2025"  · supporting: "Closing balance: £1,502.88"
    ├── trailing_date: "1 Dec 2025 – 31 Dec 2025"
    └── download_statement_button[STMT-2025-12-40051512345678]
    on_click → navigate_statement_detail(STMT-2025-12-40051512345678, 40051512345678)

BottomNav/ (persistent, h 80dp, bg #F7F9FF)
├── tab Home         (icon: home,            label: "Home",         tint #41474D, unselected)
├── tab Accounts     (icon: account_balance,  label: "Accounts",     tint #41474D, unselected)
├── tab Transactions (icon: receipt_long,     label: "Transactions", tint #41474D, unselected)
└── tab More         (icon: more_horiz,       label: "More",         tint #41474D, unselected)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Statements                                │  ← top_app_bar: bg #F7F9FF, h 64dp
│                                              │
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│                                              │
│              [description]                   │  ← icon: description 48dp, tint #41474D
│                                              │    (M3 Symbols Outlined — document icon)
│                                              │    centred horizontally and vertically
│          No statements yet                  │  ← title: titleMedium 16sp/24sp w500 #181C20
│                                              │    centred, padding top 16dp
│   Statements will appear here once your     │  ← body: bodyMedium 14sp/20sp w400 #41474D
│   account generates periodic statements.   │    centred, padding top 8dp
│   They are produced monthly by HSBC.       │    padding h 32dp
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
Screen: Statements (StatementsUiState.Empty)
│
TopAppBar/ (small variant, bg #F7F9FF)
│   ├── leading: arrow_back → navigate_back
│   └── title: "Statements"
│
empty_statements/ (Column, gravity: center, padding 32dp, fillMaxSize)
│   accessibility_label: "No statements yet"
│
├── Icon (description, size 48dp, tint #41474D onSurfaceVariant,
│         contentDescription: "No statements")
├── Spacer (height 16dp)
├── title (Text, style titleMedium 16sp/24sp w500 #181C20, textAlign Center):
│         "No statements yet"
├── Spacer (height 8dp)
└── body  (Text, style bodyMedium 14sp/20sp w400 #41474D, textAlign Center):
          "Statements will appear here once your account generates periodic statements.
           They are produced monthly by HSBC."

BottomNav/ (persistent, h 80dp, bg #F7F9FF)
├── Home · Accounts · Transactions · More (all unselected, tint #41474D)
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Statements                                │  ← top_app_bar: bg #F7F9FF, h 64dp
│                                              │
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│             [error_outline]                  │  ← icon: error_outline 48dp, tint #BA1A1A
│                                              │    centred horizontally and vertically
│      Unable to load statements              │  ← title: titleMedium 16sp/24sp w500 #181C20
│                                              │    centred, padding top 16dp
│   Session expired.                          │  ← body: bodyMedium 14sp/20sp w400 #41474D
│   Please re-authenticate.                  │    centred, from error.message
│                                              │    demo: HTTP 401 error scenario
│                                              │
│       [         Try again         ]         │  ← retry_button: Button variant:filled
│                                              │    bg #266489, text #FFFFFF "Try again"
│                                              │    h 48dp, cornerRadius 20dp
│                                              │    horizontalPadding 24dp, min touch 48dp
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
Screen: Statements (StatementsUiState.Error — demo: HTTP 401, "Session expired.")
│
TopAppBar/ (small variant, bg #F7F9FF)
│   ├── leading: arrow_back → navigate_back
│   └── title: "Statements"
│
error_state/ (Column, gravity: center, padding 32dp, fillMaxSize)
│   accessibility_label: "Unable to load statements"
│
├── Icon (error_outline, size 48dp, tint #BA1A1A error,
│         contentDescription: "Error loading statements")
├── Spacer (height 16dp)
├── title (Text, style titleMedium 16sp/24sp w500 #181C20, textAlign Center):
│         "Unable to load statements"
├── Spacer (height 8dp)
├── body  (Text, style bodyMedium 14sp/20sp w400 #41474D, textAlign Center):
│         "Session expired. Please re-authenticate."
│         [resolved from error.message via ViewModel http_error_map:
│          HTTP 401 → "Session expired. Please re-authenticate."
│          HTTP 403 → "Consent does not include ReadStatements."
│          HTTP 429 → "Too many requests. Please wait and retry."
│          network  → e.localizedMessage]
├── Spacer (height 24dp)
└── retry_button (Button variant:filled, bg #266489, contentColor #FFFFFF,
                  shape RoundedCornerShape 20dp, padding horizontal 24dp,
                  modifier height 48dp, min touch 48dp)
    label: "Try again"
    accessibility_label: "Retry loading statements"
    on_click → retry_load(accountId) → delegates to statementsLoad(accountId)
        action_contract: effect=call_api
        re-issues GET /accounts/{accountId}/statements
        transitions: Loading → Content | Empty | Error

BottomNav/ (persistent, h 80dp, bg #F7F9FF)
├── Home · Accounts · Transactions · More (all unselected, tint #41474D)
```

---

### Interaction Summary

| Component | Action | Effect | Target / Behaviour |
|---|---|---|---|
| arrow_back (top app bar) | navigate_back | navigate | Pops back stack to account-detail screen |
| statement_row (any, tap row body) | navigate_statement_detail | navigate | statement-detail screen (params: statementId=item.StatementId, accountId=accountId) |
| download_statement_button (idle → tap) | download_statement | persist_file | Calls GET /accounts/{AccountId}/statements/{StatementId}/file; Accept: application/pdf, text/csv; streams bytes → platform file handler; button switches to CircularProgress during download; stops event propagation preventing parent row tap |
| download_statement_button (in-progress) | — | — | Spinner shown (downloadState[statementId] == InProgress); tap suppressed |
| retry_button (error state) | retry_load | call_api | Delegates to statementsLoad(accountId); re-issues GET /accounts/{AccountId}/statements; screen transitions Loading → Content \| Empty \| Error |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| top_app_bar | match_parent | 64dp | 0 |
| statement_row | match_parent | 72dp min (wrap content) | 0 |
| download_statement_button (touch) | 48dp | 48dp | 9999dp (circular) |
| download_statement_button (icon/spinner) | 24dp | 24dp | — |
| statement_row_divider | match_parent | 1dp | 0 |
| empty_statements icon | 48dp | 48dp | — |
| error_state icon | 48dp | 48dp | — |
| retry_button | wrap + h-padding 24dp each side | 48dp | 20dp |
| skeleton_row × 3 | match_parent − 32dp (361dp) | 72dp | 8dp |
| bottom_nav | match_parent | 80dp | 0 |
