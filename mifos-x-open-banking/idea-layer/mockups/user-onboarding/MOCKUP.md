# User Onboarding — Visual Mockup

> Auto-generated from `screens/user-onboarding/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Content: Static educational AISP/FAPI copy — no network calls
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Welcome to Open Banking

Canvas: 393×852dp · No top app bar · No bottom nav · Full screen · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│                                              │
│                   ◌                          │  ← onboarding_loading_indicator circular
│                                              │    #266489 centred (DataStore flag check)
│                                              │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│            [error_outline]                   │  ← icon 48dp #BA1A1A
│    Something went wrong                    │
│  Could not initialise onboarding.          │
│         [  Try again  ]                     │  ← onboarding_error_retry_button filled
└─────────────────────────────────────────────┘
```

---

### State: empty (onboarding disabled by feature flag)

```
┌─────────────────────────────────────────────┐
│            [info_outline]                    │  ← icon 48dp #41474D
│    Onboarding not available                │
│  Guided setup is currently unavailable.    │
│         [  Go to sign in  ]                 │  ← onboarding_empty_skip_button → login
└─────────────────────────────────────────────┘
```

---

### State: intro (Step 1 of 3)

```
┌─────────────────────────────────────────────┐
│                                              │
│         ●  ○  ○                             │  ← step_indicator_intro stepper 1/3
│                                              │    dot 1 filled primary, 2+3 outline
│         ┌─────────────────────┐             │
│         │                     │             │
│         │  [hero illustration] │             │  ← hero_illustration ic_open_banking_hero
│         │   bank + shield     │             │    content_description: "UK Open Banking
│         │   + phone           │             │    — secure, regulated data sharing"
│         └─────────────────────┘             │    approx 240×200dp centred
│                                              │
│   Your bank data,                           │  ← intro_headline headlineMedium #181C20
│   securely shared                          │
│                                              │
│   Connect your HSBC accounts read-only     │  ← intro_body bodyMedium #41474D
│   via the UK Open Banking standard.         │
│   No passwords shared. FCA regulated.       │
│                                              │
│   ( 🔒 FAPI 1.0 Advanced )                 │  ← fapi_security_badge chip assist
│   ( 🏛  FCA Regulated )                    │  ← fca_regulated_badge chip assist
│                                              │
│         [  Get started  ]                   │  ← intro_next_button filled #266489
│                                              │    → permissions_overview state
└─────────────────────────────────────────────┘
```

---

### State: permissions_overview (Step 2 of 3)

```
┌─────────────────────────────────────────────┐
│                                              │
│         ●  ●  ○                             │  ← step_indicator_permissions stepper 2/3
│                                              │
│  What we'll read from your bank             │  ← what_we_read_header section_header
│                                              │
│  🏦  Account details                        │  ← perm_accounts list_item
│     Names, sort codes, and IBANs for       │    icon manage_accounts
│     your authorised accounts               │
│  💰  Balances                               │  ← perm_balances icon account_balance
│     Current, savings, and credit card      │
│     balances in real time                  │
│  📋  Transactions                           │  ← perm_transactions icon receipt_long
│     Up to 90 days of debits and credits    │
│  ↻  Standing orders                         │  ← perm_standing_orders icon autorenew
│     Scheduled recurring payment mandates   │
│  ▸  Direct debits                           │  ← perm_direct_debits icon subscriptions
│     Active mandates authorised on account  │
│  📄  Statements                             │  ← perm_statements icon description
│     Monthly statement summaries and PDFs   │
│                                              │
│   ℹ Consent lasts up to 90 days and is    │  ← consent_duration_note bodySmall #41474D
│     revocable at any time from Settings.   │
│                                              │
│  [Back]             [  Next: Guarantees  ] │  ← outlined + filled buttons
│                                              │
└─────────────────────────────────────────────┘
```

---

### State: consent_explainer (Step 3 of 3)

```
┌─────────────────────────────────────────────┐
│                                              │
│         ●  ●  ●                             │  ← step_indicator_trust stepper 3/3
│                                              │
│  What we will never do                      │  ← what_we_never_do_header section_header
│                                              │
│  💸  We can't make payments                 │  ← never_payments icon money_off #BA1A1A
│     This is a read-only service. No        │
│     PISP capability — we cannot move money │
│  🔒  We never see your password            │  ← never_password icon lock #266489
│     You sign in directly on HSBC's own     │
│     portal using app-to-app redirect.      │
│  ✕  You can leave at any time              │  ← never_locked_in icon cancel #266489
│     Revoke your consent any time from      │
│     Settings → Manage consents.            │
│                                              │
│  ─────────────────────────────────────────  │  ← legal_divider
│                                              │
│  Regulated by the FCA under PSR 2017.       │  ← legal_footer labelSmall #41474D
│  Data shared via OBIE Open Banking v4.0.   │
│                                              │
│  [Back]        [  Connect to HSBC ↗  ]    │  ← outlined + filled (→ login)
│  [How does Open Banking work?]              │  ← how_ob_works_button text → ob_explainer
└─────────────────────────────────────────────┘
```

---

### State: ob_explainer_open (bottom sheet overlay on consent_explainer)

```
┌─────────────────────────────────────────────┐
│         ●  ●  ●                             │  ← consent_explainer behind (dimmed)
│         [consent_explainer — dimmed]        │
│                                              │
│  ┌─────────────────────────────────────────┐│
│  │  ━━━━━━━━━━━━                           ││  ← drag handle
│  │  How Open Banking works                 ││  ← ob_explainer_title titleLarge #181C20
│  │                                          ││
│  │  ✋  Grant permission                   ││  ← ob_step1 icon how_to_reg
│  │     You approve what data the app can   ││
│  │     read on HSBC's secure portal.       ││
│  │  🔑  Sign in with HSBC                  ││  ← ob_step2 icon login
│  │     Authenticate directly on HSBC       ││
│  │     using your online banking or app.   ││
│  │     We never receive your credentials.  ││
│  │  🛡  Get a secure token                 ││  ← ob_step3 icon shield
│  │     HSBC issues a short-lived signed   ││
│  │     FAPI access token. No password      ││
│  │     ever touches our servers.           ││
│  │                                          ││
│  │  You can revoke this consent at any    ││  ← ob_explainer_revoke_note bodySmall #41474D
│  │  time from Settings → Manage consents. ││
│  │                                          ││
│  │  [  Got it  ]                           ││  ← ob_explainer_close_button filled
│  └─────────────────────────────────────────┘│  → consent_explainer state
└─────────────────────────────────────────────┘
```

### Component Hierarchy — (all states, no shell)

```
Screen: full-screen, no top_app_bar, no BottomNav

--- LOADING ---
onboarding_loading_indicator/ (circular progress_indicator centred)

--- ERROR ---
onboarding_error_state/ (empty_state variant=error icon=error_outline)
└── onboarding_error_retry_button (filled → retry_onboarding_init)

--- EMPTY ---
onboarding_empty_state/ (empty_state variant=neutral icon=info_outline)
└── onboarding_empty_skip_button (filled → login)

--- INTRO (step 1) ---
step_indicator_intro/ (stepper 1/3, dots, horizontal)
hero_illustration/ (image ic_open_banking_hero 240×200dp centred)
intro_headline/ (headlineMedium #181C20)
intro_body/ (bodyMedium #41474D)
fapi_security_badge/ (chip assist icon verified_user)
fca_regulated_badge/ (chip assist icon account_balance)
intro_next_button/ (filled → permissions_overview)

--- PERMISSIONS OVERVIEW (step 2) ---
step_indicator_permissions/ (stepper 2/3)
what_we_read_header/ (section_header)
permissions_list/ (list vertical 6 items)
│  ├── perm_accounts   (icon manage_accounts)
│  ├── perm_balances   (icon account_balance)
│  ├── perm_transactions (icon receipt_long)
│  ├── perm_standing_orders (icon autorenew)
│  ├── perm_direct_debits (icon subscriptions)
│  └── perm_statements (icon description)
consent_duration_note/ (bodySmall #41474D)
permissions_back_button/ (outlined → intro)
permissions_next_button/ (filled → consent_explainer)

--- CONSENT EXPLAINER (step 3) ---
step_indicator_trust/ (stepper 3/3)
what_we_never_do_header/ (section_header)
reassurance_list/
│  ├── never_payments (icon money_off #BA1A1A)
│  ├── never_password (icon lock #266489)
│  └── never_locked_in (icon cancel #266489)
legal_divider/ (divider)
legal_footer/ (labelSmall #41474D): "Regulated by FCA under PSR 2017 · OBIE v4.0"
connect_hsbc_button/ (filled icon open_in_new → login)
trust_back_button/ (outlined → permissions_overview)
how_ob_works_button/ (text → ob_explainer_open)

--- OB EXPLAINER BOTTOM SHEET ---
ob_explainer_sheet/ (bottom_sheet, peek over consent_explainer)
│  ├── ob_explainer_title (titleLarge)
│  ├── ob_step1 (list_item icon how_to_reg)
│  ├── ob_step2 (list_item icon login)
│  ├── ob_step3 (list_item icon shield)
│  ├── ob_explainer_revoke_note (bodySmall #41474D)
│  └── ob_explainer_close_button (filled → consent_explainer)
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| onboarding_error_retry_button | retry_onboarding_init | loading state |
| onboarding_empty_skip_button | navigate_to_login | login |
| intro_next_button | step_next | permissions_overview |
| permissions_back_button | step_back | intro |
| permissions_next_button | step_next | consent_explainer |
| trust_back_button | step_back | permissions_overview |
| connect_hsbc_button | navigate_to_login | login (begins FAPI flow) |
| how_ob_works_button | open_ob_explainer | ob_explainer_open |
| ob_explainer_close_button | close_ob_explainer | consent_explainer |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| hero_illustration | 240dp | 200dp | 0 |
| stepper (3 dots) | 80dp | 12dp | 0 |
| trust/assist chip | wrap | 32dp | 9999 |
| cta filled button | match_parent − 64dp | 56dp | 28dp |
| back outlined button | wrap | 48dp | 24dp |
| ob_explainer_sheet | match_parent | ~500dp peek | 28dp top corners |
