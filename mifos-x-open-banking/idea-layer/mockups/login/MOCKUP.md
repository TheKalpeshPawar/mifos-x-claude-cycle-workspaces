# Login — Visual Mockup

> Auto-generated from `screens/login/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Connect with HSBC

Canvas: 393×852dp · Pixel 5 · Top app bar (small, back arrow, title "Connect with HSBC") · No bottom nav · No FAB · Material 3 light theme · Roboto

Shell: `ui.yaml#shell` declares `bottom_navigation_visible: false`, `top_app_bar_visible: true`, `top_app_bar_leading: back`, `fab_visible: false`. The global bottom nav (Home / Accounts / Transactions / More from app-shell.yaml) is suppressed — this is a consent-initiation flow, not a primary destination.

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← Connect with HSBC                         │  ← top_app_bar bg #F7F9FF, titleMedium 16sp/500
├─────────────────────────────────────────────┤
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  [HSBC]                                 │ │  ← hsbc_logo ic_hsbc_logo, 48dp h, centred
│ │                                          │ │
│ │  ✓ Regulated UK Open Banking            │ │  ← ob_regulated_badge labelSmall 11sp #266489
│ │    connection                           │ │    icon_leading verified_user 16dp #266489
│ │                                          │ │
│ │  Connect with HSBC                      │ │  ← explainer_headline titleMedium 16sp #181C20
│ │  You'll be redirected to HSBC to        │ │  ← explainer_body bodySmall 12sp #41474D
│ │  approve permissions and select         │ │
│ │  accounts. Your credentials are never   │ │
│ │  shared with this app.                  │ │
│ │                                          │ │
│ │  ─────────────────────────────          │ │  ← card_divider outlineVariant #C1C7CE
│ │                                          │ │
│ │  🔒 Secured with FAPI 1.0 Advanced,    │ │  ← security_notice labelSmall 11sp #41474D
│ │     mTLS, and PS256-signed tokens.      │ │    icon_leading lock_outline 16dp #41474D
│ └─────────────────────────────────────────┘ │  ← card elevation 1dp, radius 12dp, bg #F1F4F9
│                                              │
│  Permissions requested                       │  ← permissions_header labelLarge 14sp #181C20
│                                              │
│  ✓ Account details                          │  ← permission_row (ReadAccountsDetail)
│    Account identifiers, sort code,          │    icon check_circle_outline 24dp #266489
│    account number, nickname                 │    headline bodyMedium #181C20
│                                              │    supporting bodySmall #41474D
│  ✓ Balances                                 │  ← permission_row (ReadBalances)
│    Current and available balances           │
│    for each account                         │
│                                              │
│  ✓ Transaction history                      │  ← permission_row (ReadTransactionsDetail)
│    Debits and credits with merchant,        │
│    amount, and date                         │
│                                              │
│  ✓ Beneficiaries                            │  ← permission_row (ReadBeneficiariesDetail)
│    Saved payees on your account             │
│                                              │
│  ✓ Standing orders                          │  ← permission_row (ReadStandingOrdersDetail)
│    Scheduled recurring payment instructions │
│                                              │
│  ✓ Direct debits                            │  ← permission_row (ReadDirectDebits)
│    Active direct debit mandates and         │
│    their status                             │
│                                              │
│  ✓ Scheduled payments                       │  ← permission_row (ReadScheduledPaymentsDetail)
│    One-off future-dated payment             │
│    instructions                             │
│                                              │
│  ✓ Statements                               │  ← permission_row (ReadStatementsDetail)
│    Monthly statement metadata and           │
│    PDF references                           │
│                                              │
│  ✓ Product information                      │  ← permission_row (ReadProducts)
│    Interest rates and product features      │
│    attached to your accounts                │
│                                              │
│  ✓ Account holder name                      │  ← permission_row (ReadParty)
│    Full legal name registered on the        │
│    account                                  │
│                                              │
│  Your consent is valid for 90 days and      │  ← consent_validity_note bodySmall 12sp #41474D
│  covers transactions from 30 Mar 2026.      │
│  Expires 26 Sep 2026                        │  ← consent_expiry_display labelMedium 12sp #266489
│                                              │    VM-computed from ExpirationDateTime
│  ┌──────────────────────────────────────┐   │
│  │   Continue to HSBC  ↗               │   │  ← continue_hsbc_button FilledButton 48dp
│  └──────────────────────────────────────┘   │    bg #266489, text onPrimary #FFFFFF
│                                              │    icon open_in_new, radius 12dp
│            Cancel                            │  ← cancel_button TextButton onSurface #181C20
│                                              │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/  (small, bg #F7F9FF, title "Connect with HSBC" titleMedium, leading ← back arrow)
hsbc_explainer_card/  (Card elevation 1, cornerRadius 12dp, bg #F1F4F9, padding 16dp)
│  ├── hsbc_logo            (image ic_hsbc_logo, 48dp h, centred, no tint)
│  │                         contentDescription: "HSBC logo"
│  ├── ob_regulated_badge   (text labelSmall 11sp #266489, icon_leading verified_user 16dp #266489)
│  │                         value: "Regulated UK Open Banking connection"
│  │                         a11y: "Verified: Regulated UK Open Banking connection"
│  ├── explainer_headline   (text titleMedium 16sp #181C20)
│  │                         value: "Connect with HSBC"
│  ├── explainer_body       (text bodySmall 12sp #41474D)
│  │                         value: "You'll be redirected to HSBC to approve permissions…"
│  ├── card_divider         (Divider, color outlineVariant #C1C7CE, thickness 1dp)
│  └── security_notice      (text labelSmall 11sp #41474D, icon_leading lock_outline 16dp #41474D)
│                            value: "Secured with FAPI 1.0 Advanced, mTLS, and PS256-signed tokens."
permissions_header/  (SectionHeader labelLarge 14sp #181C20): "Permissions requested"
permissions_list/  (LazyColumn vertical, 10 rows, items=requested_permissions from VM)
│  └── permission_row × 10  (ListItem, minHeight 56dp, icon check_circle_outline 24dp #266489)
│       ├── headline_text   (bodyMedium 14sp #181C20): "Account details" … "Account holder name"
│       └── supporting_text (bodySmall 12sp #41474D): per-scope human-readable description
│           a11y: "{item.label}: {item.description}"
consent_validity_note   (text bodySmall 12sp #41474D, paddingTop 8dp)
consent_expiry_display  (text labelMedium 12sp #266489): "Expires 26 Sep 2026"
                         a11y: "Consent expires 26 Sep 2026"
continue_hsbc_button    (FilledButton, h 48dp, w match_parent−32dp, radius 12dp, bg #266489)
                         label "Continue to HSBC" onPrimary #FFFFFF, trailing icon open_in_new
                         a11y: "Continue to HSBC — opens HSBC app or website"
cancel_button           (TextButton, h 48dp, label "Cancel" onSurface #181C20, centred)
                         a11y: "Cancel — return to previous screen"
```

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Connect with HSBC                         │  ← top_app_bar bg #F7F9FF, same as content
├─────────────────────────────────────────────┤
│                                              │
│  ▓▓▓▓▓▓▓▓▓▓▓▓▓░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← loading_indicator LinearProgressIndicator
│                                              │    primary #266489, match_parent w, 4dp h
│                                              │    indeterminate animation, animated left→right
│                                              │    a11y: "Connecting to HSBC"
│                                              │
│    Preparing your secure connection…        │  ← loading_label bodyMedium 14sp #41474D
│                                              │    centred horizontally, paddingTop 24dp
│                                              │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — loading

```
top_app_bar/  (small, bg #F7F9FF, title "Connect with HSBC", leading ← back)
loading_indicator/  (LinearProgressIndicator indeterminate, primary #266489, 4dp h, match_parent w)
                    a11y: "Connecting to HSBC" (aria-live polite on state entry)
loading_label/  (text bodyMedium 14sp #41474D, centred, paddingTop 24dp)
                value: "Preparing your secure connection…"
                a11y: "Connecting to HSBC"
```

---

### State: authorising

```
┌─────────────────────────────────────────────┐
│ ← Connect with HSBC                         │  ← top_app_bar bg #F7F9FF, same as content
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                    ◌                         │  ← authorising_spinner CircularProgressIndicator
│                (spinning)                    │    48dp, primary #266489, centred
│                                              │    a11y: "Waiting for HSBC authorisation"
│                                              │
│    Waiting for HSBC authorisation…          │  ← authorising_label bodyMedium 14sp #41474D
│                                              │    centred, paddingTop 16dp
│    Complete sign-in in the HSBC app or      │  ← authorising_hint bodySmall 12sp #41474D
│    website, then return here.               │    centred, paddingTop 8dp
│                                              │
│                                              │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — authorising

```
top_app_bar/  (small, bg #F7F9FF, title "Connect with HSBC", leading ← back)
authorising_spinner/  (CircularProgressIndicator 48dp, primary #266489, centred, paddingTop 64dp)
                      a11y: "Waiting for HSBC authorisation" (aria-live assertive on state entry)
authorising_label/    (text bodyMedium 14sp #41474D, centred, paddingTop 16dp)
                      value: "Waiting for HSBC authorisation…"
authorising_hint/     (text bodySmall 12sp #41474D, centred, paddingTop 8dp)
                      value: "Complete sign-in in the HSBC app or website, then return here."
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Connect with HSBC                         │  ← top_app_bar bg #F7F9FF, same as content
├─────────────────────────────────────────────┤
│                                              │
│             [error_outline]                  │  ← icon 48dp, color error #BA1A1A, centred
│                                              │    paddingTop 64dp
│     Could not connect to HSBC               │  ← error_state.title headlineSmall 24sp #181C20
│                                              │    centred, paddingTop 16dp
│  Unable to reach HSBC. Check your           │  ← error_state.body bodyMedium 14sp #41474D
│  connection and try again.                  │    centred, paddingTop 8dp
│  (NetworkException message; other error     │    VM maps to one of 5 user-safe messages:
│   paths show distinct copy from VM)         │    400/401/500/FapiRedirect variants
│                                              │
│  ┌──────────────────────────────────────┐   │
│  │         Try again                   │   │  ← retry_button FilledButton 48dp #266489
│  └──────────────────────────────────────┘   │    text onPrimary #FFFFFF, radius 12dp
│                                              │    on_click → start_oauth (effect: share_external)
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
top_app_bar/  (small, bg #F7F9FF, title "Connect with HSBC", leading ← back)
error_state/  (EmptyState variant=error, paddingTop 64dp, centred)
│  ├── icon         (error_outline 48dp, tint error #BA1A1A, centred)
│  ├── title        (text headlineSmall 24sp #181C20, centred, paddingTop 16dp)
│  │                value: "Could not connect to HSBC"
│  │                a11y: "Connection error. Could not connect to HSBC."
│  ├── body         (text bodyMedium 14sp #41474D, centred, paddingTop 8dp)
│  │                value: VM-mapped user message (e.g. "Unable to reach HSBC. Check your
│  │                connection and try again." for NetworkException)
│  └── retry_button (FilledButton, h 48dp, w match_parent−32dp, radius 12dp, bg #266489)
                     label "Try again" onPrimary #FFFFFF
                     a11y: "Try again — retry connecting to HSBC"
                     on_click → start_oauth (effect: share_external)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Connect with HSBC                         │  ← top_app_bar bg #F7F9FF, same as content
├─────────────────────────────────────────────┤
│                                              │
│             [manage_search]                  │  ← icon 48dp, onSurfaceVariant #41474D, centred
│                                              │    paddingTop 64dp
│     No permissions configured               │  ← login_empty_state.title headlineSmall 24sp #181C20
│                                              │    centred, paddingTop 16dp
│  No Open Banking read scopes are            │  ← login_empty_state.body bodyMedium 14sp #41474D
│  available to request.                      │    centred, paddingTop 8dp
│                                              │
│  ┌──────────────────────────────────────┐   │
│  │         Go back                     │   │  ← login_empty_back_button FilledButton 48dp
│  └──────────────────────────────────────┘   │    bg #266489, text onPrimary #FFFFFF, radius 12dp
│                                              │    on_click → navigate_back → user-onboarding
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
top_app_bar/  (small, bg #F7F9FF, title "Connect with HSBC", leading ← back)
login_empty_state/  (EmptyState variant=neutral, paddingTop 64dp, centred)
│  ├── icon                    (manage_search 48dp, tint onSurfaceVariant #41474D, centred)
│  ├── title                   (text headlineSmall 24sp #181C20, centred, paddingTop 16dp)
│  │                           value: "No permissions configured"
│  │                           a11y: "No permissions. No Open Banking scopes are available."
│  ├── body                    (text bodyMedium 14sp #41474D, centred, paddingTop 8dp)
│  │                           value: "No Open Banking read scopes are available to request."
│  └── login_empty_back_button (FilledButton, h 48dp, w match_parent−32dp, radius 12dp, bg #266489)
                                label "Go back" onPrimary #FFFFFF
                                a11y: "Go back — return to previous screen"
                                on_click → navigate_back (effect: navigate, target: user-onboarding)
```

---

### Interaction Summary

| Component | Action | Effect | Description |
|---|---|---|---|
| back arrow (top app bar) | navigate_back | navigate | Returns to user-onboarding; no side-effects, no consent staged |
| continue_hsbc_button | start_oauth | share_external | POST /account-access-consents (ktorfit, client_credentials); builds PS256-signed FAPI 1.0 Advanced /authorize URL (jose4j); launches HSBC app-to-app redirect for SCA and account selection |
| cancel_button | navigate_back | navigate | Abandons consent flow; returns to user-onboarding; no consent staged and no OAuth state stored |
| retry_button (error state) | start_oauth | share_external | Re-triggers consent-create POST (ktorfit) and FAPI redirect (jose4j) after prior failure; same flow as continue_hsbc_button |
| login_empty_back_button (empty state) | navigate_back | navigate | Returns to user-onboarding when no OBIE permissions are available; prevents zero-scope OBReadConsent1 that HSBC would reject (HTTP 400) |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| hsbc_explainer_card | match_parent − 32dp | wrap_content | 12dp |
| hsbc_logo | centred | 48dp | n/a |
| ob_regulated_badge icon | 16dp | 16dp | n/a |
| permission_row (ListItem) | match_parent | 56dp min | 0 |
| permission_row icon (check_circle_outline) | 24dp | 24dp | n/a |
| continue_hsbc_button | match_parent − 32dp | 48dp | 12dp |
| cancel_button | match_parent − 32dp | 48dp | 0 (text variant) |
| loading_indicator (linear) | match_parent | 4dp | 0 |
| authorising_spinner | 48dp | 48dp | circle |
| retry_button | match_parent − 32dp | 48dp | 12dp |
| login_empty_back_button | match_parent − 32dp | 48dp | 12dp |
| error_outline icon | 48dp | 48dp | n/a |
| manage_search icon | 48dp | 48dp | n/a |
