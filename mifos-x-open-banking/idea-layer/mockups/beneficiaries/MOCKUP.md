# Beneficiaries — Visual Mockup

> Auto-generated from `screens/beneficiaries/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Beneficiaries

Canvas: 393×852dp (Pixel 5) · Roboto font · Material 3 light theme · bg #F7F9FF

Shell resolved from `app-shell.yaml` + `ui.yaml#shell` overrides:
- **Top app bar**: visible (override `top_app_bar_visible: true`) · title "Beneficiaries" (titleLarge 22sp/28sp w400 #181C20) · leading `arrow_back` icon_button (24dp #266489, 48dp×48dp touch target) · trailing none · bg #F7F9FF · elevation 0 · h 64dp
- **Bottom navigation**: Home (`home`) | Accounts (`account_balance`) | Transactions (`receipt_long`) | More (`more_horiz` → settings) · selected tint #266489 · unselected tint #41474D · bg #F7F9FF · h 80dp · Accounts tab contextually active (beneficiaries is a drill-down from account-detail)
- **FAB**: hidden (override `fab_visible: false`)

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ←  Beneficiaries                            │  ← top_app_bar: h 64dp bg #F7F9FF
│                                              │    back_button: arrow_back 24dp #266489
├─────────────────────────────────────────────┤    title: titleLarge 22sp #181C20
│                                              │
│                                              │
│                                              │
│                                              │
│                      ◌                      │  ← progress_indicator: circular 48dp
│                                              │    color: #266489 (primary)
│                                              │    centered: fillMaxSize wrapContentSize
│                                              │    contentDescription: "Loading beneficiaries"
│                                              │
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← bottom_nav: h 80dp bg #F7F9FF
└─────────────────────────────────────────────┘    Accounts: tint #266489 (contextual parent)
```

### Component Hierarchy — loading

```
Screen: Beneficiaries (BeneficiariesUiState.Loading)
│
top_app_bar/ (TopAppBar small, bg #F7F9FF, elevation 0, h 64dp)
├── back_button (icon_button arrow_back 24dp tint #266489, touch 48×48dp)
│              accessibility_label: "Back to account detail"
│              on_click → navigate_back → account-detail
└── title: "Beneficiaries" (titleLarge 22sp/28sp w400 #181C20)
│
progress_indicator/ (CircularProgressIndicator, size 48dp, strokeWidth 4dp)
    color: #266489 (MaterialTheme.colorScheme.primary)
    modifier: fillMaxSize().wrapContentSize(Alignment.Center)
    contentDescription: "Loading beneficiaries"
│
BottomNav/ (NavigationBar, h 80dp bg #F7F9FF, persistent)
├── tab Home         (icon: home,           label: "Home",         tint #41474D)
├── tab Accounts     (icon: account_balance, label: "Accounts",    tint #266489 selected)
├── tab Transactions (icon: receipt_long,   label: "Transactions", tint #41474D)
└── tab More         (icon: more_horiz,     label: "More",         tint #41474D → settings)
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ←  Beneficiaries                            │  ← top_app_bar h 64dp
├─────────────────────────────────────────────┤
│                                              │
│  ┌─────────────────────────────────────┐    │  ← beneficiary_search: SearchBar
│  │ 🔍  Search by name or reference    │    │    h 48dp, radius 28dp, bg #F1F4F9
│  └─────────────────────────────────────┘    │    outline: #72787E, padding h 16dp
│                                              │    placeholder bodyLarge 16sp #72787E
│  ╭──╮  Jameson Lettings     RENT-FLAT12     │  ← BEN-001 list_item two_line h 72dp
│  │JL│  Sort Code · 40-12-09 65872310        │    avatar: circle 40dp bg #C9E6FF
│  ╰──╯                                        │    initials "JL" labelMedium 12sp #004B6F
│  ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─  │    headline bodyLarge 16sp #181C20
│  ╭──╮  John Sharma              FAMILY      │    supporting bodyMedium 14sp #41474D
│  │JS│  Sort Code · 23-05-80 11223344        │    trailing labelSmall 11sp #50606E
│  ╰──╯                                        │    divider: 1dp #DDE3EA between rows
│  ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─  │
│  ╭──╮  EDF Energy           ELEC-8841       │  ← BEN-003: name matches "ener" filter
│  │EE│  Sort Code · 60-00-01 99887766        │
│  ╰──╯                                        │
│  ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─  │
│  ╭──╮  Hargreaves Lansdown  ISA-TOPUP       │  ← BEN-004: UK.OBIE.SortCodeAccountNumber
│  │HL│  Sort Code · 11-22-33 44556677        │
│  ╰──╯                                        │
│  ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─  │
│  ╭──╮  Priya Rajan — N26 GmbH TRAVEL-EUR   │  ← BEN-005: UK.OBIE.IBAN scheme
│  │PR│  IBAN · DE89370400440532013000        │    identifier in Roboto Mono
│  ╰──╯                                        │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

**Content sub-variant — search query active ("ener" → 1 result)**

```
┌─────────────────────────────────────────────┐
│ ←  Beneficiaries                            │
├─────────────────────────────────────────────┤
│                                              │
│  ┌─────────────────────────────────────┐    │
│  │ 🔍  ener                        ✕  │    │  ← clear icon visible when query non-empty
│  └─────────────────────────────────────┘    │    on_change → filter_beneficiaries("ener")
│                                              │    no API call — client-side only
│  ╭──╮  EDF Energy           ELEC-8841       │  ← beneficiaries_filtered: [BEN-003]
│  │EE│  Sort Code · 60-00-01 99887766        │    CreditorAccount.Name "EDF Energy" contains
│  ╰──╯                                        │    "ener" (ignoreCase: true)
│                                              │
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

**Content sub-variant — search_no_results (query "zzzmatch" → 0 matches)**

```
┌─────────────────────────────────────────────┐
│ ←  Beneficiaries                            │
├─────────────────────────────────────────────┤
│                                              │
│  ┌─────────────────────────────────────┐    │
│  │ 🔍  zzzmatch                     ✕ │    │
│  └─────────────────────────────────────┘    │
│                                              │
│            [search_off]                     │  ← search_no_results empty_state
│                                              │    icon 48dp #41474D
│        No results found                     │    title headlineSmall 24sp #181C20 center
│                                              │
│   Try a different name or reference.        │  ← body bodyMedium 14sp #41474D center
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
Screen: Beneficiaries (BeneficiariesUiState.Content)
│
top_app_bar/ (as loading state)
│
LazyColumn/ (padding: h 16dp, top 8dp, verticalArrangement: 0dp gap)
│
├── beneficiary_search/ (SearchBar, id: beneficiary_search, state_binding: [content])
│   ├── leadingIcon: search 24dp #72787E (decorative)
│   ├── placeholder: "Search by name or reference" (bodyLarge 16sp #72787E)
│   ├── activeIndicatorColor: #266489 (primary)
│   ├── shape: RoundedCornerShape(28dp), bg #F1F4F9, outline #72787E
│   ├── h 48dp, width match_parent
│   ├── accessibility_label: "Search beneficiaries"
│   └── onValueChange → filterBeneficiaries(query) — client-side; no API call
│
├── beneficiaries_list/ (LazyColumn, items: beneficiaries_filtered, gap 0)
│   │
│   ├── beneficiary_row[BEN-001] (ListItem twoLine, h 72dp)
│   │   ├── leadingContent: avatar circle 40dp bg #C9E6FF
│   │   │   initials "JL" (labelMedium 12sp w500 #004B6F); aria_hidden: true
│   │   ├── headlineContent: "Jameson Lettings" (bodyLarge 16sp w400 #181C20)
│   │   ├── supportingContent: "Sort Code · 40-12-09 65872310" (bodyMedium 14sp #41474D)
│   │   ├── trailingContent: "RENT-FLAT12" (labelSmall 11sp w500 #50606E)
│   │   └── semanticsLabel: "Jameson Lettings, Sort Code account, 40-12-09 65872310"
│   ├── HorizontalDivider (1dp #DDE3EA)
│   │
│   ├── beneficiary_row[BEN-002] (ListItem twoLine, h 72dp)
│   │   ├── avatar "JS" (circle 40dp #C9E6FF / #004B6F)
│   │   ├── headline "John Sharma" (bodyLarge #181C20)
│   │   ├── supporting "Sort Code · 23-05-80 11223344" (bodyMedium #41474D)
│   │   └── trailing "FAMILY" (labelSmall #50606E)
│   ├── HorizontalDivider
│   │
│   ├── beneficiary_row[BEN-003] (ListItem twoLine, h 72dp)
│   │   ├── avatar "EE" (circle 40dp #C9E6FF / #004B6F)
│   │   ├── headline "EDF Energy" (bodyLarge #181C20)
│   │   ├── supporting "Sort Code · 60-00-01 99887766" (bodyMedium #41474D)
│   │   └── trailing "ELEC-8841" (labelSmall #50606E)
│   ├── HorizontalDivider
│   │
│   ├── beneficiary_row[BEN-004] (ListItem twoLine, h 72dp)
│   │   ├── avatar "HL" (circle 40dp #C9E6FF / #004B6F)
│   │   ├── headline "Hargreaves Lansdown" (bodyLarge #181C20)
│   │   ├── supporting "Sort Code · 11-22-33 44556677" (bodyMedium #41474D)
│   │   └── trailing "ISA-TOPUP" (labelSmall #50606E)
│   ├── HorizontalDivider
│   │
│   └── beneficiary_row[BEN-005] (ListItem twoLine, h 72dp)
│       ├── avatar "PR" (circle 40dp #C9E6FF / #004B6F)
│       ├── headline "Priya Rajan — N26 GmbH" (bodyLarge #181C20)
│       ├── supporting "IBAN · DE89370400440532013000"
│       │             scheme label bodyMedium #41474D; identifier Roboto Mono #41474D
│       └── trailing "TRAVEL-EUR" (labelSmall #50606E)
│
└── [conditional — visible only when beneficiaries_filtered.isEmpty()]
    search_no_results/ (Column centered, padding h 32dp, id: search_no_results)
    ├── icon: search_off 48dp #41474D (contentDescription: "No search results")
    ├── title: "No results found" (headlineSmall 24sp/32sp w400 #181C20 textAlign Center)
    └── body: "Try a different name or reference." (bodyMedium 14sp/20sp #41474D center)
│
BottomNav/ (Accounts tab active tint #266489)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ←  Beneficiaries                            │  ← top_app_bar h 64dp
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│           [people_outline]                  │  ← empty_beneficiaries empty_state
│                                              │    icon: people_outline 48dp #41474D
│     No beneficiaries set up                 │    title: headlineSmall 24sp #181C20
│                                              │    centered, padding h 32dp
│   No payees have been saved for this        │  ← body: bodyMedium 14sp #41474D
│   account. Set up payees in your            │    centered
│   bank app to see them here.                │
│                                              │
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: Beneficiaries (BeneficiariesUiState.Empty)
│
top_app_bar/ (as loading state)
│
empty_beneficiaries/ (Column, id: empty_beneficiaries, state_binding: [empty])
│   vertically centered (fillMaxSize wrapContentSize), padding horizontal 32dp
│   accessibility_label: "No beneficiaries set up"
│
├── icon: people_outline 48dp #41474D
│         contentDescription: "No saved beneficiaries"
├── Spacer 16dp
├── title: "No beneficiaries set up"
│           (headlineSmall 24sp/32sp w400 #181C20 textAlign Center)
├── Spacer 8dp
└── body: "No payees have been saved for this account. Set up payees in your bank app to see them here."
          (bodyMedium 14sp/20sp w400 #41474D textAlign Center)
│
BottomNav/ (Accounts tab active tint #266489)
```

---

### State: error

**Sub-variant A — Retryable: HTTP 401 TokenExpired / 429 RateLimited / NetworkError / 500 ServerError**

```
┌─────────────────────────────────────────────┐
│ ←  Beneficiaries                            │  ← top_app_bar h 64dp
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│           [error_outline]                   │  ← icon 48dp #BA1A1A (error) centered
│                                              │
│    Unable to load beneficiaries             │  ← title headlineSmall 24sp #181C20 center
│                                              │
│  Your session has expired. Please sign     │  ← body "{error.message}" bodyMedium 14sp
│  in again to continue.                     │    #41474D center; demo: HTTP 401 message
│                                              │
│      [       Try again        ]             │  ← retry_button: filled
│                                              │    h 48dp radius 9999 bg #266489 text #FFFFFF
│                                              │    visible when isRetryable(error.type)
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

**Sub-variant B — ConsentRevoked: HTTP 403**

```
┌─────────────────────────────────────────────┐
│ ←  Beneficiaries                            │  ← top_app_bar h 64dp
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│           [error_outline]                   │  ← icon 48dp #BA1A1A centered
│                                              │
│    Unable to load beneficiaries             │  ← title headlineSmall 24sp #181C20 center
│                                              │
│  Your account access consent has been      │  ← body bodyMedium 14sp #41474D center
│  revoked. Re-authorise to restore          │    demo: HTTP 403 ConsentRevoked message
│  beneficiaries access.                     │
│                                              │
│      [     View consents     ]              │  ← view_consents_button: tonal
│                                              │    h 48dp radius 9999
│                                              │    bg #D3E5F5 text #384956
│                                              │    visible only when ConsentRevoked
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
Screen: Beneficiaries (BeneficiariesUiState.Error)
│
top_app_bar/ (as loading state)
│
error_state/ (Column, id: error_state, variant: error, state_binding: [error])
│   vertically centered, padding horizontal 32dp
│   accessibility_label: "Unable to load beneficiaries"
│
├── icon: error_outline 48dp #BA1A1A
│         contentDescription: "Error loading beneficiaries"
├── Spacer 24dp
├── title: "Unable to load beneficiaries" (headlineSmall 24sp/32sp w400 #181C20 textAlign Center)
├── Spacer 8dp
├── body: "{error.message}" (bodyMedium 14sp/20sp w400 #41474D textAlign Center)
│         Sub-A demo: "Your session has expired. Please sign in again to continue."
│         Sub-B demo: "Your account access consent has been revoked. Re-authorise to restore access."
├── Spacer 24dp
│
├── retry_button (Button filled, h 48dp radius 9999, bg #266489 text #FFFFFF)
│   label: "Try again" (labelLarge 14sp/20sp w500 #FFFFFF)
│   accessibility_label: "Retry loading beneficiaries"
│   visibility_condition: error.type ∈ {TokenExpired, RateLimited, NetworkError, ServerError}
│   on_click → retryLoad() → GET /accounts/{accountId}/beneficiaries via ktorfit
│
└── view_consents_button (Button tonal, h 48dp radius 9999, bg #D3E5F5 text #384956)
    label: "View consents" (labelLarge 14sp/20sp w500 #384956)
    accessibility_label: "View and manage your account access consents"
    visibility_condition: error.type == ConsentRevoked
    on_click → navigate → consent-list
│
BottomNav/ (Accounts tab active tint #266489)
```

---

### Interaction Summary

| Component | Action | Effect | Target / Behaviour |
|---|---|---|---|
| back_button (all states) | navigate_back | navigate | Returns PSU to account-detail screen; back-stack pop; AccountId param preserved |
| beneficiary_search (content state) | filter_beneficiaries | transform_state | Client-side filter of `beneficiaries_filtered` by `CreditorAccount.Name` or `Reference` (ignoreCase); no API call; debounced input |
| retry_button (error — retryable) | retry_load | call_api | Re-fetches GET /accounts/{accountId}/beneficiaries via ktorfit; resets state Loading → Content or Error; visible for TokenExpired / RateLimited / NetworkError / ServerError |
| view_consents_button (error — 403) | navigate | navigate | Navigates to consent-list so PSU can review and re-authorise ReadBeneficiariesDetail permission; visible only when error.type == ConsentRevoked |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| top_app_bar | 393dp match_parent | 64dp | 0dp |
| back_button touch target | 48dp | 48dp | 9999dp (circular) |
| beneficiary_search | match_parent − 32dp = 361dp | 48dp | 28dp (full pill) |
| beneficiary_row (list_item two_line) | match_parent | 72dp | 0dp |
| beneficiary_avatar | 40dp | 40dp | 9999dp (circular) |
| divider between list rows | match_parent | 1dp | 0dp |
| empty / error state icon | 48dp | 48dp | — |
| retry_button | match_parent − 64dp = 265dp | 48dp | 9999dp (full pill) |
| view_consents_button | match_parent − 64dp = 265dp | 48dp | 9999dp (full pill) |
| bottom_nav | 393dp match_parent | 80dp | 0dp |
