# Statement Detail — Visual Mockup

> Auto-generated from `screens/statement-detail/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Statement Detail

Canvas: 393×852dp (Pixel 5) · Top app bar (small, back + StatementReference) · Bottom nav visible · No FAB · Roboto · Material 3 light theme · bg #F7F9FF

Shell resolved from `app-shell.yaml` + `ui.yaml#shell`:
- Top app bar: small variant, leading back arrow (`arrow_back` 24dp #41474D), title = `statement.StatementReference` (fallback "Statement Detail"), no trailing actions.
- Bottom navigation: Home (`home`) | Accounts (`account_balance`) | Transactions (`receipt_long`) | More (`more_horiz`). Statement-detail is reached from the Transactions/Statements flow; Transactions tab reflects origin.
- FAB: hidden (`fab_visible: false`).

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Statement Detail                          │  ← top_app_bar small bg #F7F9FF elevation 0dp
├─────────────────────────────────────────────┤   title fallback titleLarge #181C20
│                                              │   leading arrow_back 24dp tint #41474D
│                                              │
│                                              │
│                                              │
│                                              │
│                    ◌                         │  ← progress_indicator circular 40dp
│                                              │   color primary #266489 strokeWidth 4dp
│                                              │   layout Box(fillMaxSize) Alignment.Center
│                                              │   accessibility_label: "Loading statement"
│                                              │
│                                              │
│                                              │
│                                              │
│                                              │
│                                              │
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← BottomNav bg #F7F9FF h 80dp
│  #41474D   #41474D      #266489     #41474D │   Transactions tab selected tint #266489
└─────────────────────────────────────────────┘
```

### Component Hierarchy — loading

```
Screen: StatementDetail (StatementDetailUiState.Loading)
│
progress_indicator/ (CircularProgressIndicator)
│   size: 40dp, strokeWidth: 4dp, color: #266489 (primary)
│   layout: Box(Modifier.fillMaxSize(), contentAlignment = Alignment.Center)
│   accessibility_label: "Loading statement"
│
top_app_bar/ (TopAppBar small variant, containerColor #F7F9FF, scrolledContainerColor #F7F9FF)
│   ├── NavigationIconButton (arrow_back 24dp, tint #41474D, minTouch 48dp)
│   │   contentDescription: "Navigate back"
│   └── title (titleLarge 22sp/28sp w400 #181C20): "Statement Detail"   [fallback]
│
BottomNav/ (NavigationBar bg #F7F9FF, h 80dp, tonalElevation 0dp)
├── Home         (icon:home           label:"Home"         selected:false tint #41474D)
├── Accounts     (icon:account_balance label:"Accounts"    selected:false tint #41474D)
├── Transactions (icon:receipt_long   label:"Transactions" selected:true  tint #266489)
└── More         (icon:more_horiz     label:"More"         selected:false tint #41474D)
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← MAY-2026-STMT                             │  ← top_app_bar title = StatementReference
├─────────────────────────────────────────────┤   titleLarge #181C20; back arrow #41474D
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← statement_header_card
│ │  MAY-2026-STMT                          │ │   bg surfaceContainer #EBEEF3
│ │  01 May 2026 – 31 May 2026             │ │   elevation 2 (3dp), radius 12dp
│ │  RegularPeriodic                        │ │   padding 16dp, margin h 16dp v 8dp
│ │  Created 01 Jun 2026, 06:00            │ │   accessibility_label: "Statement period header"
│ └─────────────────────────────────────────┘ │   ↑ reference labelMedium 12sp #50606E
│                                              │   ↑ period titleMedium 16sp #181C20
│  Balances                                    │  ← balances_header section_header
│                                              │   labelMedium 12sp w500 #41474D h 48dp
│  OpeningBalance          £2,610.40 GBP      │  ← balance_row[0] list_item h 56dp
│                                              │   leading bodyMedium #181C20
│                                              │   trailing titleMedium #64597B (tertiary/Credit)
│  ClosingBalance          £2,847.63 GBP      │  ← balance_row[1] list_item h 56dp
│                                              │   trailing titleMedium #64597B (tertiary/Credit)
│  Fees                                        │  ← fees_header (visible: length > 0)
│                                              │   labelMedium 12sp #41474D
│  Monthly maintenance fee      £0.00 GBP     │  ← fee_row list_item h 56dp
│                                              │   leading bodyMedium #181C20
│                                              │   trailing bodyMedium #181C20 (Debit, neutral)
│  Interest                                    │  ← interest_header (visible: length > 0)
│                                              │   labelMedium 12sp #41474D
│  In-credit interest           £0.21 GBP     │  ← interest_row list_item h 56dp
│                                              │   trailing bodyMedium #64597B (tertiary/Credit)
│  Transactions                                │  ← transactions_header section_header
│                                              │   labelMedium 12sp #41474D
│  03 May 2026                                 │  ← txn_row[0] TXN-2026-05-001
│  TESCO STORES 3225 LONDON    −£82.50 GBP    │   overline labelSmall 11sp #41474D
│                                              │   text bodyMedium 14sp #181C20
│                                              │   trailing titleSmall 14sp #BA1A1A (error/Debit)
│  10 May 2026                                 │  ← txn_row[1] TXN-2026-05-002
│  BACS CREDIT ACME CORP PAYROLL+£3,200.00 GBP│   trailing titleSmall #64597B (tertiary/Credit)
│  15 May 2026                                 │  ← txn_row[2] TXN-2026-05-003
│  SO LANDLORD RENT MAY 2026   −£650.00 GBP   │   trailing titleSmall #BA1A1A
│  22 May 2026                                 │  ← txn_row[3] TXN-2026-05-004
│  BRITISH GAS ENERGY BILLS    −£230.48 GBP   │   trailing titleSmall #BA1A1A
│  24 May 2026                                 │  ← txn_row[4] TXN-2026-05-005
│  TFL TRAVEL LONDON            −£45.00 GBP   │   trailing titleSmall #BA1A1A
│  28 May 2026                                 │  ← txn_row[5] TXN-2026-05-006
│  NETFLIX.COM                  −£12.99 GBP   │   trailing titleSmall #BA1A1A
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← download_pdf_button (outlined)
│ │ ⬇  Download PDF                         │ │   border 1dp #266489, text #266489
│ └─────────────────────────────────────────┘ │   h 48dp, radius 9999dp (full pill)
│                                              │   enabled_when: downloadState != Downloading
│ ▓▓▓▓▓▓▓▓▓▓▓▓░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← download_progress linear indeterminate
│ (visible_when: downloadState == Downloading) │   color #266489, h 4dp, w match_parent
│                                              │
│ ╔═══════════════════════════════════════╗   │  ← download_result_snackbar
│ ║ PDF saved to device              ✕   ║   │   bg inverseSurface #2D3135
│ ╚═══════════════════════════════════════╝   │   text inverseOnSurface #EEF1F6
│ (visible_when: Downloaded || DownloadError) │   auto_dismiss 4000ms; error: "Download failed"
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
Screen: StatementDetail (StatementDetailUiState.Content)
│  statement = OBStatement2 (MAY-2026-STMT)
│  statementTransactions = List<OBTransaction6>[6]
│
LazyColumn(verticalArrangement=spacedBy(0dp), contentPadding=PaddingValues(h=16dp, bottom=16dp))
│
├── statement_header_card/ (Card, elevation 2 / tonalElevation 3dp)
│   │  bg #EBEEF3 (surfaceContainer), radius 12dp, padding 16dp
│   │  margin set by outer column horizontal padding 16dp + additional 0dp inset
│   │  accessibility_label: "Statement period header"
│   ├── statement_reference  (Text labelMedium 12sp/16sp w500 #50606E)
│   │                         value: "MAY-2026-STMT"
│   ├── statement_period     (Text titleMedium 16sp/24sp w500 #181C20)
│   │                         value: "01 May 2026 – 31 May 2026"
│   ├── statement_type       (Text bodySmall 12sp/16sp w400 #41474D)
│   │                         value: "RegularPeriodic"
│   └── statement_created    (Text labelSmall 11sp/16sp w500 #41474D)
│                             value: "Created 01 Jun 2026, 06:00"
│
├── balances_header           (SectionHeader h 48dp, labelMedium #41474D padding h 0dp)
│                              label: "Balances"
│
├── balance_row[0]  (ListItem h 56dp, divider below outlineVariant #C1C7CE)
│   ├── supporting_text "OpeningBalance"  (bodyMedium 14sp #181C20 weight 1)
│   └── trailing "£2,610.40 GBP"         (titleMedium 16sp #64597B align end)
│       — CreditDebitIndicator=Credit → color role tertiary #64597B
│
├── balance_row[1]  (ListItem h 56dp)
│   ├── supporting_text "ClosingBalance"  (bodyMedium 14sp #181C20 weight 1)
│   └── trailing "£2,847.63 GBP"         (titleMedium 16sp #64597B align end)
│
├── fees_header  (visible_when: statement.StatementFee.length > 0)
│                label: "Fees"
│
├── fee_row[0]  (ListItem h 56dp, divider below)
│   ├── supporting_text "Monthly maintenance fee" (bodyMedium 14sp #181C20 weight 1)
│   └── trailing "£0.00 GBP"              (bodyMedium 14sp #181C20 align end)
│       — Debit; £0.00 rendered neutral (no error colour for zero fee)
│
├── interest_header  (visible_when: statement.StatementInterest.length > 0)
│                     label: "Interest"
│
├── interest_row[0]  (ListItem h 56dp)
│   ├── supporting_text "In-credit interest" (bodyMedium 14sp #181C20 weight 1)
│   └── trailing "£0.21 GBP"               (bodyMedium 14sp #64597B align end)
│       — CreditDebitIndicator=Credit → tertiary #64597B
│
├── transactions_header  (SectionHeader h 48dp labelMedium #41474D)
│                         label: "Transactions"
│
├── statement_txn_row[0]  (ListItem 3-line h 72dp, clickable, ripple, divider below)
│   │  on_click → navigate_transaction_detail (effect:navigate)
│   │  params: { transactionId:"TXN-2026-05-001", accountId:"40051512345678" }
│   ├── overline         "03 May 2026"              (labelSmall 11sp #41474D)
│   ├── supporting_text  "TESCO STORES 3225 LONDON" (bodyMedium 14sp #181C20 weight 1)
│   └── trailing         "−£82.50 GBP"              (titleSmall 14sp #BA1A1A align end)
│
├── statement_txn_row[1]  (ListItem 3-line h 72dp, clickable, divider below)
│   │  on_click → navigate_transaction_detail
│   │  params: { transactionId:"TXN-2026-05-002", accountId:"40051512345678" }
│   ├── overline         "10 May 2026"
│   ├── supporting_text  "BACS CREDIT ACME CORP PAYROLL" (bodyMedium #181C20)
│   └── trailing         "+£3,200.00 GBP"               (titleSmall #64597B — Credit)
│
├── statement_txn_row[2]  (ListItem 3-line h 72dp, clickable, divider below)
│   │  params: { transactionId:"TXN-2026-05-003", accountId:"40051512345678" }
│   ├── overline         "15 May 2026"
│   ├── supporting_text  "SO LANDLORD RENT MAY 2026"
│   └── trailing         "−£650.00 GBP"              (#BA1A1A — Debit)
│
├── statement_txn_row[3]  (ListItem 3-line h 72dp, clickable, divider below)
│   │  params: { transactionId:"TXN-2026-05-004", accountId:"40051512345678" }
│   ├── overline         "22 May 2026"
│   ├── supporting_text  "BRITISH GAS ENERGY BILLS"
│   └── trailing         "−£230.48 GBP"              (#BA1A1A)
│
├── statement_txn_row[4]  (ListItem 3-line h 72dp, clickable, divider below)
│   │  params: { transactionId:"TXN-2026-05-005", accountId:"40051512345678" }
│   ├── overline         "24 May 2026"
│   ├── supporting_text  "TFL TRAVEL LONDON"
│   └── trailing         "−£45.00 GBP"               (#BA1A1A)
│
├── statement_txn_row[5]  (ListItem 3-line h 72dp, clickable)
│   │  params: { transactionId:"TXN-2026-05-006", accountId:"40051512345678" }
│   ├── overline         "28 May 2026"
│   ├── supporting_text  "NETFLIX.COM"
│   └── trailing         "−£12.99 GBP"               (#BA1A1A)
│
├── download_pdf_button  (OutlinedButton, fillMaxWidth, h 48dp, radius 9999dp)
│   icon: download 18dp, label: "Download PDF"
│   border: 1dp #266489, contentColor: #266489
│   enabled_when: downloadState != Downloading
│   margin top 16dp
│   accessibility_label: "Download statement as PDF"
│   on_click → download_statement_pdf (effect: persist_file via ktor-client-download)
│
├── download_progress  (LinearProgressIndicator, w fillMaxWidth, h 4dp, color #266489)
│   visible_when: downloadState == Downloading
│   animate show/hide 150ms emphasis easing cubic-bezier(0.2,0.0,0,1.0)
│
└── download_result_snackbar  (Snackbar, bg #2D3135, contentColor #EEF1F6)
    visible_when: downloadState ∈ { Downloaded, DownloadError }
    message_success: "PDF saved to device"
    message_error: "Download failed"
    auto_dismiss: 4000ms
    action_icon: close 18dp #EEF1F6

top_app_bar/ (TopAppBar small, bg #F7F9FF)
│   back → navigateUp() to statements
│   title "MAY-2026-STMT"

BottomNav/ (persistent)
├── Home         (home          selected:false tint #41474D)
├── Accounts     (account_balance selected:false tint #41474D)
├── Transactions (receipt_long  selected:true  tint #266489)
└── More         (more_horiz    selected:false tint #41474D)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← MAY-2026-NEW                              │  ← top_app_bar title = StatementReference
├─────────────────────────────────────────────┤   (empty-transactions scenario ref)
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← statement_header_card (still shown)
│ │  MAY-2026-NEW                           │ │   bg #EBEEF3 elevation 2 radius 12dp
│ │  01 May 2026 – 31 May 2026             │ │   padding 16dp
│ │  RegularPeriodic                        │ │
│ │  Created 01 Jun 2026, 06:00            │ │
│ └─────────────────────────────────────────┘ │
│                                              │
│  Balances                                    │  ← balances_header
│  OpeningBalance          £500.00 GBP        │  ← Credit → trailing titleMedium #64597B
│  ClosingBalance          £500.00 GBP        │  ← Credit → trailing titleMedium #64597B
│                                              │
│  [Fees section HIDDEN — StatementFee: []]    │  ← fees_header/list hidden (visible_when false)
│  [Interest section HIDDEN — array empty]     │  ← interest_header/list hidden
│                                              │
│  Transactions                                │  ← transactions_header (always shown)
│                                              │
│                                              │
│             [receipt_long]                   │  ← empty_txns_state icon 48dp #41474D
│                                              │   icon: receipt_long, size 48dp
│    No transactions this period              │  ← title headlineSmall 24sp #181C20 centred
│                                              │
│   This statement period has no              │  ← body bodyMedium 14sp #41474D centred
│   transaction records.                      │
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← download_pdf_button still available
│ │ ⬇  Download PDF                         │ │   border #266489; text #266489
│ └─────────────────────────────────────────┘ │   h 48dp radius 9999dp
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: StatementDetail (StatementDetailUiState.Empty)
│  statement = OBStatement2 (MAY-2026-NEW)
│  statementTransactions = [] (empty array — valid OBIE edge case)
│
LazyColumn (padding h 16dp bottom 16dp)
│
├── statement_header_card/ (Card bg #EBEEF3 elevation 2 radius 12dp padding 16dp)
│   ├── statement_reference  "MAY-2026-NEW"              (labelMedium #50606E)
│   ├── statement_period     "01 May 2026 – 31 May 2026" (titleMedium #181C20)
│   ├── statement_type       "RegularPeriodic"            (bodySmall #41474D)
│   └── statement_created    "Created 01 Jun 2026, 06:00" (labelSmall #41474D)
│
├── balances_header  "Balances"  (labelMedium #41474D h 48dp)
├── balance_row[0]   "OpeningBalance  £500.00 GBP"  trailing titleMedium #64597B
├── balance_row[1]   "ClosingBalance  £500.00 GBP"  trailing titleMedium #64597B
│
│   ← fees_header: NOT RENDERED (StatementFee.length == 0)
│   ← fees_list:   NOT RENDERED
│   ← interest_header: NOT RENDERED (StatementInterest.length == 0)
│   ← interest_list:   NOT RENDERED
│
├── transactions_header  "Transactions"  (labelMedium #41474D h 48dp)
│
├── empty_txns_state/ (Column vertically centred, padding h 32dp v 24dp)
│   │  accessibility_label: "No transactions this period"
│   ├── icon  (receipt_long 48dp tint #41474D)
│   │   contentDescription: "No transactions this period"
│   ├── Spacer 16dp
│   ├── title (headlineSmall 24sp/32sp w400 #181C20 textAlign=Center)
│   │         "No transactions this period"
│   ├── Spacer 8dp
│   └── body  (bodyMedium 14sp/20sp w400 #41474D textAlign=Center)
│             "This statement period has no transaction records."
│
└── download_pdf_button  (OutlinedButton fillMaxWidth h 48dp radius 9999dp)
    icon: download 18dp, label: "Download PDF"
    border 1dp #266489, contentColor #266489
    margin top 16dp
    accessibility_label: "Download statement as PDF"
    on_click → download_statement_pdf (effect: persist_file)

top_app_bar/ title "MAY-2026-NEW"
BottomNav/ (persistent — Transactions tab #266489)
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Statement Detail                          │  ← top_app_bar fallback title
├─────────────────────────────────────────────┤   (StatementReference unavailable on error)
│                                              │
│                                              │
│                                              │
│             [error_outline]                  │  ← icon 48dp tint #BA1A1A (error) centred
│                                              │   contentDescription: "Error loading statement"
│    Unable to load statement                 │  ← title headlineSmall 24sp #181C20 centred
│                                              │
│   Session expired.                          │  ← body bodyMedium 14sp #41474D centred
│   Please re-authenticate.                   │   {error.message} dynamic:
│                                              │   HTTP 401 → "Session expired. Please re-authenticate."
│                                              │   HTTP 403 → "Consent does not include ReadStatements."
│                                              │   HTTP 404 → "Statement not found."
│                                              │   NETWORK  → device localizedMessage
│                                              │
│        [        Try again        ]           │  ← retry_button filled h 48dp
│                                              │   bg #266489 text #FFFFFF radius 9999dp
│                                              │   accessibility: "Retry loading statement"
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
Screen: StatementDetail (StatementDetailUiState.Error)
│  message: dynamic per StatementDetailErrorCode
│  demo: HTTP 401 → "Session expired. Please re-authenticate."
│
error_state/ (variant:error, Box fillMaxSize Alignment.Center, padding h 32dp)
│   accessibility_label: "Unable to load statement"
│
├── icon  (error_outline 48dp tint #BA1A1A)
│   contentDescription: "Error loading statement"
│
├── Spacer 16dp
│
├── title (headlineSmall 24sp/32sp w400 #181C20 textAlign=Center)
│         "Unable to load statement"
│
├── Spacer 8dp
│
├── body  (bodyMedium 14sp/20sp w400 #41474D textAlign=Center)
│         "{error.message}" — rendered per errorCode:
│         StatementNotFound           → "Statement not found."
│         ConsentMissingReadStatements → "Consent does not include ReadStatements."
│         SessionExpired              → "Session expired. Please re-authenticate."
│         StatementFileNotFound       → "Download failed. PDF not yet available."
│         NetworkError                → device e.localizedMessage
│
├── Spacer 24dp
│
└── retry_button (Button variant:filled, fillMaxWidth(0.7f), h 48dp, radius 9999dp)
    bg #266489, contentColor #FFFFFF, minTouchTarget 48dp
    label: "Try again"
    accessibility_label: "Retry loading statement"
    on_click → retry_load (effect: call_api)
               delegates to statementDetailLoad(accountId, statementId)
               screen transitions → Loading state

top_app_bar/ title "Statement Detail" (fallback)
BottomNav/ (persistent — Transactions tab #266489)
```

---

### Interaction Summary

| Component | Action | Effect | Target / Behaviour |
|---|---|---|---|
| back arrow (top_app_bar leading) | navigate_back | navigate | System back stack pop → returns to `statements` screen |
| statement_txn_row (any row, content state) | navigate_transaction_detail | navigate | `transaction-detail` screen; route params: `transactionId`, `accountId` per tapped row |
| download_pdf_button (content + empty state) | download_statement_pdf | persist_file | GET /statements/{id}/file (Accept: application/pdf) via ktor-client-download; DownloadState: Idle → Downloading → Downloaded(uri) or DownloadError(message); platform share/save sheet presented on success |
| retry_button (error state) | retry_load | call_api | Delegates to statementDetailLoad(accountId, statementId); re-executes parallel GET statements/{id} + GET statements/{id}/transactions; screen returns to Loading |

---

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| statement_header_card | match_parent (outer column padding h 16dp) | ~96dp wrap_content + 16dp padding | 12dp |
| balance_row (list_item) | match_parent | 56dp | 0 |
| fee_row (list_item) | match_parent | 56dp | 0 |
| interest_row (list_item) | match_parent | 56dp | 0 |
| section_header | match_parent | 48dp | 0 |
| statement_txn_row (3-line list_item) | match_parent | 72dp | 0 |
| download_pdf_button | match_parent − 32dp (fillMaxWidth + column padding) | 48dp | 9999dp (full pill) |
| download_progress (linear) | match_parent | 4dp | 2dp |
| download_result_snackbar | match_parent − 16dp | 48dp min | 4dp |
| empty_txns_state icon | 48dp | 48dp | n/a (icon) |
| error icon | 48dp | 48dp | n/a (icon) |
| retry_button | 70% of match_parent | 48dp | 9999dp |
| top_app_bar | match_parent | 56dp | 0 |
| bottom_nav | match_parent | 80dp | 0 |
