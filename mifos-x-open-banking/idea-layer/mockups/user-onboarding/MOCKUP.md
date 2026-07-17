# User Onboarding — Visual Mockup

> Auto-generated from `screens/user-onboarding/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Welcome to Open Banking

Canvas: 393×852dp (Pixel 5) · No top app bar · No bottom nav · No FAB · Roboto font · Material 3 light theme · bg #F7F9FF

Shell override from `ui.yaml#shell`:
- `bottom_navigation_visible: false` — full-screen pager, no tab bar chrome
- `top_app_bar_visible: false` — no title bar or navigation arrow
- `fab_visible: false`

---

### State: loading

```
┌─────────────────────────────────────────────┐
│                                              │  bg: #F7F9FF (surface)
│                                              │  full-screen, no shell chrome
│                                              │
│                                              │
│                    ◌                         │  ← onboarding_loading_indicator
│               ○ spinning ○                  │    type: progress_indicator / circular
│                                              │    diameter: 48dp
│                                              │    stroke color: #266489 (primary)
│                                              │    gravity: Modifier.fillMaxSize()
│                                              │      .wrapContentSize(Alignment.Center)
│                                              │
│                                              │
│                                              │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — loading

```
Screen: UserOnboarding (UiState.Loading) — full-screen, no shell
│
└── onboarding_loading_indicator
        type: CircularProgressIndicator (M3 indeterminate)
        size: 48dp / strokeWidth: 4dp
        color: #266489 (primary)
        trackColor: #C9E6FF (primaryContainer)
        Modifier: fillMaxSize().wrapContentSize(Center)
        a11y: contentDescription = "Loading — checking your onboarding status"
        reduce-motion: static single-arc visible
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│                                              │  bg: #F7F9FF (surface)
│                                              │
│                                              │
│                                              │
│              [ error_outline ]               │  ← icon: error_outline
│                                              │    size: 48dp / tint: #BA1A1A (error)
│                                              │    align: CenterHorizontally
│           Something went wrong              │  ← title: "Something went wrong"
│                                              │    headlineSmall 24sp/32sp w400 #181C20
│   Could not load the onboarding flow.       │  ← body: "Could not load the onboarding
│   Please try again.                         │    flow. Please try again."
│                                              │    bodyMedium 14sp/20sp #41474D
│                                              │    padding h 32dp top 12dp
│                                              │
│         ┌─────────────────────┐             │
│         │      Try again      │             │  ← onboarding_error_retry_button
│         └─────────────────────┘             │    filled / bg #266489 / text #FFFFFF
│                                              │    h 56dp / radius 28dp / w ~180dp
│                                              │    on_click: retry_onboarding_init
└─────────────────────────────────────────────┘    effect: transform_state → loading
```

### Component Hierarchy — error

```
Screen: UserOnboarding (UiState.Error) — full-screen, no shell
│
└── onboarding_error_state (empty_state variant=error)
        layout: Column(Modifier.fillMaxSize(), verticalArrangement=Center,
                        horizontalAlignment=CenterHorizontally, padding h=32dp)
        │
        ├── Icon(error_outline, 48dp, tint=#BA1A1A)
        ├── Text("Something went wrong", headlineSmall, #181C20, center)
        ├── Text("Could not load the onboarding flow. Please try again.",
        │         bodyMedium, #41474D, center, topPad=12dp)
        │
        └── onboarding_error_retry_button (Button filled)
                label: "Try again" / labelLarge 14sp w500 / #FFFFFF
                containerColor: #266489 / shape radius 28dp / h 56dp / minWidth 180dp
                on_click.action: retry_onboarding_init
                effect: transform_state (DataStore re-read → loading → intro on success)
                library_refs: [kotlinx-coroutines, androidx.datastore]
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│                                              │  bg: #F7F9FF (surface)
│                                              │
│                                              │
│                                              │
│              [ info_outline ]                │  ← icon: info_outline
│                                              │    size: 48dp / tint: #41474D (onSurfaceVariant)
│                                              │    align: CenterHorizontally
│          Setup not available                │  ← title: "Setup not available"
│                                              │    headlineSmall 24sp/32sp w400 #181C20
│  Guided onboarding is currently             │  ← body: "Guided onboarding is currently
│  unavailable. You can still sign in.        │    unavailable. You can still sign in."
│                                              │    bodyMedium 14sp/20sp #41474D
│                                              │    padding h 32dp top 12dp
│                                              │
│         ┌─────────────────────┐             │
│         │    Go to sign in    │             │  ← onboarding_empty_skip_button
│         └─────────────────────┘             │    filled / bg #266489 / text #FFFFFF
│                                              │    h 56dp / radius 28dp / w ~180dp
│                                              │    on_click: navigate_to_login → login
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: UserOnboarding (UiState.Empty) — full-screen, no shell
│
└── onboarding_empty_state (empty_state variant=neutral)
        layout: Column(Modifier.fillMaxSize(), verticalArrangement=Center,
                        horizontalAlignment=CenterHorizontally, padding h=32dp)
        │
        ├── Icon(info_outline, 48dp, tint=#41474D)
        ├── Text("Setup not available", headlineSmall, #181C20, center)
        ├── Text("Guided onboarding is currently unavailable. You can still sign in.",
        │         bodyMedium, #41474D, center, topPad=12dp)
        │
        └── onboarding_empty_skip_button (Button filled)
                label: "Go to sign in" / labelLarge 14sp w500 / #FFFFFF
                containerColor: #266489 / shape radius 28dp / h 56dp / minWidth 180dp
                on_click.action: navigate_to_login
                effect: navigate → login
```

---

### State: intro

```
┌─────────────────────────────────────────────┐
│                                              │  bg: #F7F9FF (surface)
│  ●  ○  ○                                    │  ← step_indicator_intro (stepper 1/3)
│                                              │    dot 1 filled #266489 dia 10dp
│  pad top 24dp left 16dp                     │    dots 2-3 outline #C1C7CE dia 8dp
│                                              │    gap 8dp between dots
│     ┌───────────────────────────────────┐   │
│     │                                   │   │  ← hero_illustration
│     │   [ ic_open_banking_hero ]        │   │    asset: ic_open_banking_hero
│     │    bank · shield · phone          │   │    240×200dp / Modifier.align(Center)
│     │    gradient #C9E6FF → #F7F9FF    │   │    alt: "UK Open Banking — secure,
│     │                                   │   │    regulated data sharing"
│     └───────────────────────────────────┘   │    margin top 24dp
│                                              │
│  Share your HSBC data securely              │  ← intro_headline
│  with Open Banking                          │    headlineMedium 28sp/36sp w400 #181C20
│                                              │    padding h 16dp top 24dp
│  UK Open Banking is a regulated             │  ← intro_body
│  framework overseen by the Financial        │    bodyMedium 14sp/20sp w400 #41474D
│  Conduct Authority. It lets you share       │    padding h 16dp top 12dp
│  account information with authorised        │
│  apps — without sharing your password.      │
│                                              │
│  ( ✓  Secured by FAPI 1.0 Advanced )       │  ← fapi_security_badge (AssistChip)
│  ( 🏛  FCA Regulated )                      │  ← fca_regulated_badge (AssistChip)
│                                              │    bg #F1F4F9 / border #72787E
│  pad left 16dp gap 8dp between chips        │    label #41474D labelMedium 12sp
│                                              │    icon 18dp #41474D / h 32dp radius 9999
│                                              │
│  ┌─────────────────────────────────────┐    │
│  │           Get started               │    │  ← intro_next_button (Button filled)
│  └─────────────────────────────────────┘    │    bg #266489 / text #FFFFFF
│  margin h 16dp bottom 16dp                  │    h 56dp / radius 28dp / w fillParent−32dp
│                                              │    on_click: step_next → permissions_overview
└─────────────────────────────────────────────┘
```

### Component Hierarchy — intro

```
Screen: UserOnboarding (UiState.Intro) — full-screen, no shell
│
Column(Modifier.fillMaxSize().verticalScroll(), padding h=16dp top=24dp bottom=16dp)
│
├── step_indicator_intro (HorizontalStepper)
│       totalSteps=3 / currentStep=1
│       activeDot: 10dp filled #266489 / inactiveDot: 8dp outline #C1C7CE
│       gap: 8dp / alignment: Start
│
├── hero_illustration (Image)
│       painter: painterResource(R.drawable.ic_open_banking_hero)
│       Modifier: size(240dp, 200dp).align(CenterHorizontally).padding(top=24dp)
│       contentDescription: "UK Open Banking — secure, regulated data sharing"
│       contentScale: Fit
│
├── intro_headline (Text)
│       text: "Share your HSBC data securely with Open Banking"
│       style: MaterialTheme.typography.headlineMedium  // 28sp/36sp w400
│       color: #181C20 (onSurface)
│       modifier: padding(horizontal=16dp, top=24dp)
│
├── intro_body (Text)
│       text: "UK Open Banking is a regulated framework overseen by the Financial
│              Conduct Authority. It lets you share your account information with
│              authorised apps — without sharing your password."
│       style: MaterialTheme.typography.bodyMedium  // 14sp/20sp w400
│       color: #41474D (onSurfaceVariant)
│       modifier: padding(horizontal=16dp, top=12dp)
│
├── Row(horizontalArrangement=spacedBy(8dp), modifier=padding(top=16dp))
│   ├── fapi_security_badge (AssistChip)
│   │       label: "Secured by FAPI 1.0 Advanced"
│   │       leadingIcon: Icon(verified_user, 18dp)
│   │       containerColor: #F1F4F9 / border: #72787E / labelColor: #41474D
│   │       height: 32dp / shape: CircleShape (radius 9999)
│   └── fca_regulated_badge (AssistChip)
│           label: "FCA Regulated"
│           leadingIcon: Icon(account_balance, 18dp)
│           same styling as fapi_security_badge
│
└── intro_next_button (Button filled)
        text: "Get started"
        containerColor: #266489 / contentColor: #FFFFFF
        shape: RoundedCornerShape(28dp)  // extra_large
        modifier: fillMaxWidth().height(56dp).padding(top=24dp)
        on_click.action: step_next
        effect: transform_state (currentStep 1→2) → UiState.PermissionsOverview
```

---

### State: permissions_overview

```
┌─────────────────────────────────────────────┐
│                                              │  bg: #F7F9FF (surface)
│  ●  ●  ○                                    │  ← step_indicator_permissions (2/3)
│                                              │    dots 1-2 filled #266489 / dot 3 #C1C7CE
│  What we'll read                            │  ← what_we_read_header (section_header)
│  ──────────────────────────────────────     │    labelLarge 14sp/20sp w500 #181C20
│                                              │    bottom border: 1dp #C1C7CE
│  ┌─────────────────────────────────────┐    │
│  │  ◫  Account details                 │    │  ← perm_accounts
│  │     Account names, sort codes,      │    │    icon: manage_accounts 24dp #41474D
│  │     IBANs, and currency for your    │    │    headline: "Account details"
│  │     HSBC accounts                   │    │    titleSmall 14sp/20sp w500 #181C20
│  ├─────────────────────────────────────┤    │    supporting bodySmall 12sp/16sp #41474D
│  │  💰  Account balances               │    │  ← perm_balances
│  │     Current, available, and         │    │    icon: account_balance 24dp #41474D
│  │     credit-limit balances across    │    │    headline: "Account balances"
│  │     all accounts in real time       │    │
│  ├─────────────────────────────────────┤    │
│  │  📋  Transaction history            │    │  ← perm_transactions
│  │     Up to 90 days of debits and    │    │    icon: receipt_long 24dp #41474D
│  │     credits, merchant names, and   │    │    headline: "Transaction history"
│  │     transaction references          │    │
│  ├─────────────────────────────────────┤    │
│  │  ↻  Standing orders                 │    │  ← perm_standing_orders
│  │     Scheduled recurring payment    │    │    icon: autorenew 24dp #41474D
│  │     mandates on your HSBC accounts  │    │    headline: "Standing orders"
│  ├─────────────────────────────────────┤    │
│  │  ▷  Direct debits                   │    │  ← perm_direct_debits
│  │     Active direct-debit mandates   │    │    icon: subscriptions 24dp #41474D
│  │     and last amounts collected      │    │    headline: "Direct debits"
│  ├─────────────────────────────────────┤    │
│  │  📄  Statements                     │    │  ← perm_statements
│  │     Monthly summaries, opening /   │    │    icon: description 24dp #41474D
│  │     closing balances, PDF refs     │    │    headline: "Statements"
│  └─────────────────────────────────────┘    │
│                                              │
│  ⓘ Your consent lasts up to 90 days.       │  ← consent_duration_note
│    Revoke at any time via                   │    bodySmall 12sp/16sp #41474D
│    Settings → Manage consents.             │    padding h 16dp top 12dp bottom 12dp
│                                              │
│  ┌──────────┐   ┌────────────────────────┐ │
│  │   Back   │   │  Next: Guarantees →   │ │  ← permissions_back_button (outlined)
│  └──────────┘   └────────────────────────┘ │    h 48dp / radius 24dp / border #72787E
│  margin h 16dp bottom 16dp                  │    permissions_next_button (filled)
│                                              │    bg #266489 h 56dp radius 28dp
└─────────────────────────────────────────────┘
```

### Component Hierarchy — permissions_overview

```
Screen: UserOnboarding (UiState.PermissionsOverview) — full-screen, no shell
│
Column(Modifier.fillMaxSize().verticalScroll(), padding h=16dp top=24dp bottom=16dp)
│
├── step_indicator_permissions (HorizontalStepper)
│       totalSteps=3 / currentStep=2
│       dots 1-2: 10dp filled #266489 / dot 3: 8dp outline #C1C7CE
│
├── what_we_read_header (SectionHeader)
│       label: "What we'll read"
│       style: labelLarge 14sp/20sp w500 / color: #181C20
│       bottomDivider: 1dp #C1C7CE (outlineVariant)
│
├── permissions_list (Column, dividers between items)
│   ├── perm_accounts (ListItem 3-line)
│   │       leadingContent: Icon(manage_accounts, 24dp, #41474D)
│   │       headlineText: "Account details" / titleSmall 14sp w500 #181C20
│   │       supportingText: "Account names, sort codes, IBANs, and currency for your HSBC accounts"
│   │       bodySmall 12sp #41474D
│   ├── perm_balances (ListItem 3-line)
│   │       leadingContent: Icon(account_balance, 24dp, #41474D)
│   │       headlineText: "Account balances"
│   │       supportingText: "Current, available, and credit-limit balances across all authorised accounts in real time"
│   ├── perm_transactions (ListItem 3-line)
│   │       leadingContent: Icon(receipt_long, 24dp, #41474D)
│   │       headlineText: "Transaction history"
│   │       supportingText: "Up to 90 days of debits and credits, merchant names, and transaction references"
│   ├── perm_standing_orders (ListItem 3-line)
│   │       leadingContent: Icon(autorenew, 24dp, #41474D)
│   │       headlineText: "Standing orders"
│   │       supportingText: "Scheduled recurring payment mandates you have set up on your HSBC accounts"
│   ├── perm_direct_debits (ListItem 3-line)
│   │       leadingContent: Icon(subscriptions, 24dp, #41474D)
│   │       headlineText: "Direct debits"
│   │       supportingText: "Active direct-debit mandates and the most recent amounts collected on your accounts"
│   └── perm_statements (ListItem 3-line)
│           leadingContent: Icon(description, 24dp, #41474D)
│           headlineText: "Statements"
│           supportingText: "Monthly statement summaries, opening and closing balances, and available PDF references"
│
├── consent_duration_note (Text)
│       text: "Your consent lasts up to 90 days. You can revoke it at any time from Settings → Manage consents."
│       style: bodySmall 12sp/16sp / color: #41474D
│       modifier: padding(h=16dp, top=12dp, bottom=12dp)
│
└── Row(Modifier.fillMaxWidth(), horizontalArrangement=SpaceBetween)
    ├── permissions_back_button (OutlinedButton)
    │       text: "Back" / contentColor: #266489 / borderColor: #72787E
    │       shape: RoundedCornerShape(24dp) / h: 48dp / minWidth: 120dp
    │       on_click.action: step_back (currentStep 2→1) → UiState.Intro
    └── permissions_next_button (Button filled)
            text: "Next: Guarantees →" / containerColor: #266489 / contentColor: #FFFFFF
            shape: RoundedCornerShape(28dp) / h: 56dp / minWidth: 180dp
            on_click.action: step_next (currentStep 2→3) → UiState.ConsentExplainer
```

---

### State: consent_explainer

```
┌─────────────────────────────────────────────┐
│                                              │  bg: #F7F9FF (surface)
│  ●  ●  ●                                    │  ← step_indicator_trust (3/3)
│                                              │    all 3 dots filled #266489
│  What we never do                           │  ← what_we_never_do_header (section_header)
│  ──────────────────────────────────────     │    labelLarge 14sp/20sp w500 #181C20
│                                              │
│  ┌─────────────────────────────────────┐    │
│  │  💸  No payments or transfers       │    │  ← never_payments
│  │     ↑ icon money_off tint #BA1A1A   │    │    icon: money_off 24dp / tint: #BA1A1A (error)
│  │     This app is Account Information │    │    headline: "No payments or transfers"
│  │     only (AISP). We have no         │    │    titleSmall 14sp w500 #181C20
│  │     permission to initiate          │    │    supporting: "…no permission to move money"
│  │     payments or move money.         │    │    bodySmall 12sp #41474D
│  ├─────────────────────────────────────┤    │
│  │  🔒  We never see your password     │    │  ← never_password
│  │     ↑ icon lock tint #266489        │    │    icon: lock 24dp / tint: #266489 (primary)
│  │     Authenticate directly on        │    │    headline: "We never see your password"
│  │     HSBC's secure portal via SCA.  │    │
│  │     Credentials never leave HSBC.  │    │
│  ├─────────────────────────────────────┤    │
│  │  ✕  Revoke access anytime          │    │  ← never_locked_in
│  │     ↑ icon cancel tint #266489      │    │    icon: cancel 24dp / tint: #266489 (primary)
│  │     Disconnect any time from        │    │    headline: "Revoke access anytime"
│  │     Settings → Manage consents,    │    │    supporting: "…or directly from HSBC app"
│  │     or directly from HSBC app.     │    │
│  └─────────────────────────────────────┘    │
│                                              │
│  ─────────────────────────────────────────  │  ← legal_divider (1dp #C1C7CE)
│                                              │
│  Regulated by the Financial Conduct         │  ← legal_footer
│  Authority under the Payment Services       │    labelSmall 11sp/16sp w500 #41474D
│  Regulations 2017. Powered by UK Open       │    padding h 16dp top 8dp bottom 16dp
│  Banking Read/Write API v4.0 (OBIE).        │
│                                              │
│  ┌──────────┐  ┌─────────────────────────┐ │
│  │   Back   │  │   Connect to HSBC  ↗   │ │  ← trust_back_button (outlined) h 48dp
│  └──────────┘  └─────────────────────────┘ │    bg transparent / border #72787E / text #266489
│                                              │    connect_hsbc_button (filled) h 56dp
│  ┌─────────────────────────────────────┐    │    bg #266489 / icon open_in_new / → login
│  │   How does Open Banking work?       │    │  ← how_ob_works_button (TextButton)
│  └─────────────────────────────────────┘    │    text #266489 / → ob_explainer_open
│                                              │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — consent_explainer

```
Screen: UserOnboarding (UiState.ConsentExplainer) — full-screen, no shell
│
Column(Modifier.fillMaxSize().verticalScroll(), padding h=16dp top=24dp bottom=16dp)
│
├── step_indicator_trust (HorizontalStepper)
│       totalSteps=3 / currentStep=3
│       all 3 dots: 10dp filled #266489
│
├── what_we_never_do_header (SectionHeader)
│       label: "What we never do"
│       style: labelLarge 14sp/20sp w500 / color: #181C20
│       bottomDivider: 1dp #C1C7CE
│
├── reassurance_list (Column, internal HorizontalDividers, color #C1C7CE)
│   ├── never_payments (ListItem 3-line)
│   │       leadingContent: Icon(money_off, 24dp, tint=#BA1A1A)   // error
│   │       headlineText: "No payments or transfers"
│   │       supportingText: "This app is Account Information only (AISP). We have no
│   │                        permission to initiate payments or move money from your account."
│   ├── never_password (ListItem 3-line)
│   │       leadingContent: Icon(lock, 24dp, tint=#266489)   // primary
│   │       headlineText: "We never see your password"
│   │       supportingText: "You authenticate directly on HSBC's secure portal using their
│   │                        Strong Customer Authentication (SCA). Your credentials never leave HSBC."
│   └── never_locked_in (ListItem 3-line)
│           leadingContent: Icon(cancel, 24dp, tint=#266489)   // primary
│           headlineText: "Revoke access anytime"
│           supportingText: "You can disconnect HSBC data sharing at any time from Settings →
│                            Manage consents, or directly from your HSBC app."
│
├── legal_divider (HorizontalDivider, thickness=1dp, color=#C1C7CE)
│
├── legal_footer (Text)
│       text: "Regulated by the Financial Conduct Authority under the Payment Services
│              Regulations 2017. Powered by UK Open Banking Read/Write API v4.0 (OBIE)."
│       style: labelSmall 11sp/16sp w500 / color: #41474D
│       modifier: padding(h=16dp, top=8dp, bottom=16dp)
│
├── Row(Modifier.fillMaxWidth(), horizontalArrangement=SpaceBetween)
│   ├── trust_back_button (OutlinedButton)
│   │       text: "Back" / contentColor: #266489 / borderColor: #72787E
│   │       shape: RoundedCornerShape(24dp) / h: 48dp / minWidth: 120dp
│   │       on_click.action: step_back (currentStep 3→2) → UiState.PermissionsOverview
│   └── connect_hsbc_button (Button filled + leadingIcon)
│           text: "Connect to HSBC" / leadingIcon: Icon(open_in_new, 18dp)
│           containerColor: #266489 / contentColor: #FFFFFF
│           shape: RoundedCornerShape(28dp) / h: 56dp
│           on_click.action: navigate_to_login
│           effect: navigate → login (stages OBReadConsent1, begins FAPI app-to-app redirect)
│
└── how_ob_works_button (TextButton)
        text: "How does Open Banking work?"
        contentColor: #266489 / modifier: fillMaxWidth().height(40dp)
        on_click.action: open_ob_explainer
        effect: transform_state (showObExplainerSheet=true) → UiState.ObExplainerOpen
```

---

### State: ob_explainer_open

```
┌─────────────────────────────────────────────┐
│░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ │  scrim: #000000 opacity 40%
│░  ●  ●  ●                                  ░│  consent_explainer rendered below
│░  What we never do                         ░│  (pointerInput blocked by scrim)
│░  No payments · No password · Revoke...   ░│
│░  ─────────────────────────────────────   ░│
│░  Regulated by FCA…  Connect · Back       ░│
│░  How does Open Banking work?              ░│
│                                              │
│ ┌───────────────────────────────────────────┐│
│ │           ━━━━━━━━━━━━                    ││  ← drag handle 32×4dp #C1C7CE radius 2dp
│ │                                            ││    ob_explainer_sheet (ModalBottomSheet)
│ │ How UK Open Banking works                 ││  ← ob_explainer_title
│ │                                            ││    titleLarge 22sp/28sp w400 #181C20
│ │ ✋  You approve the permission request    ││  ← ob_step1 icon how_to_reg 24dp #41474D
│ │    We ask HSBC to prepare a consent      ││    headline: "You approve the permission
│ │    with the list of data categories       ││    request" titleSmall 14sp #181C20
│ │    we want to read. You review and        ││    supporting: bodySmall 12sp #41474D
│ │    approve on HSBC's secure portal,       ││
│ │    choosing which accounts to include.    ││
│ │                                            ││
│ │ 🔑  You authenticate directly with HSBC  ││  ← ob_step2 icon login 24dp #41474D
│ │    Log in on HSBC's portal using your    ││    headline: "You authenticate directly
│ │    own HSBC credentials and complete SCA. ││    with HSBC" titleSmall 14sp #181C20
│ │    We never see your password, card       ││
│ │    number, or security codes at any point.││
│ │                                            ││
│ │ 🛡  A secure token is returned to us     ││  ← ob_step3 icon shield 24dp #41474D
│ │    HSBC sends a short-lived, signed       ││    headline: "A secure token is returned
│ │    FAPI 1.0 Advanced access token.        ││    to us" titleSmall 14sp #181C20
│ │    Used to read only — cannot move money. ││
│ │                                            ││
│ │ You can revoke this access at any time   ││  ← ob_explainer_revoke_note
│ │ from Settings → Manage consents, or      ││    bodySmall 12sp/16sp #41474D
│ │ directly from your HSBC app.             ││    padding top 16dp h 24dp
│ │                                            ││
│ │ ┌─────────────────────────────────────┐  ││
│ │ │              Got it                  │  ││  ← ob_explainer_close_button (filled)
│ │ └─────────────────────────────────────┘  ││    bg #266489 / text #FFFFFF
│ │ margin h 24dp bottom 24dp                 ││    h 56dp / radius 28dp / w fillParent−48dp
│ └───────────────────────────────────────────┘│    on_click: close_ob_explainer
└─────────────────────────────────────────────┘    effect: transform_state → consent_explainer
```

### Component Hierarchy — ob_explainer_open

```
Screen: UserOnboarding (UiState.ObExplainerOpen) — consent_explainer + modal overlay
│
├── [consent_explainer content — rendered below, interaction disabled by scrim]
│       Modifier.alpha(1f) but scrim applied by ModalBottomSheetLayout system
│
└── ob_explainer_sheet (ModalBottomSheet)
        sheetShape: RoundedCornerShape(topStart=28dp, topEnd=28dp)
        containerColor: #FFFFFF (surfaceContainerLowest)
        scrimColor: #000000.copy(alpha=0.40f)
        dragHandle: Box(32dp×4dp, #C1C7CE, RoundedCornerShape(2dp))
        │
        Column(padding(h=24dp, top=16dp, bottom=24dp), gap=0)
        │
        ├── ob_explainer_title (Text)
        │       text: "How UK Open Banking works"
        │       style: titleLarge 22sp/28sp w400 / color: #181C20
        │       modifier: padding(bottom=16dp)
        │
        ├── ob_step1 (ListItem 3-line)
        │       leadingContent: Icon(how_to_reg, 24dp, #41474D)
        │       headlineText: "You approve the permission request"
        │       supportingText: "We ask HSBC to prepare a consent with the list of data
        │                        categories we want to read. You are then redirected to HSBC's
        │                        secure app or website to review and approve it — choosing which
        │                        accounts to include."
        │
        ├── ob_step2 (ListItem 3-line)
        │       leadingContent: Icon(login, 24dp, #41474D)
        │       headlineText: "You authenticate directly with HSBC"
        │       supportingText: "You log in on HSBC's portal using your own HSBC credentials and
        │                        complete Strong Customer Authentication (SCA). Mifos Open Banking
        │                        never sees your password, card number, or security codes at any point."
        │
        ├── ob_step3 (ListItem 3-line)
        │       leadingContent: Icon(shield, 24dp, #41474D)
        │       headlineText: "A secure token is returned to us"
        │       supportingText: "Once you approve, HSBC sends a short-lived, signed access token
        │                        back to this app using FAPI 1.0 Advanced — a banking-grade security
        │                        protocol. We use this token to read the account information you
        │                        approved; it cannot be used to move money."
        │
        ├── ob_explainer_revoke_note (Text)
        │       text: "You can revoke this access at any time from Settings → Manage consents,
        │              or directly from your HSBC app or HSBC online banking."
        │       style: bodySmall 12sp/16sp / color: #41474D
        │       modifier: padding(top=16dp)
        │
        └── ob_explainer_close_button (Button filled)
                text: "Got it" / containerColor: #266489 / contentColor: #FFFFFF
                shape: RoundedCornerShape(28dp)
                modifier: fillMaxWidth().height(56dp).padding(top=24dp)
                on_click.action: close_ob_explainer
                effect: transform_state (showObExplainerSheet=false) → UiState.ConsentExplainer
```

---

### Interaction Summary

Derived from current `ui.yaml` `action_contract` entries (updated post-enrichment 2026-07-14).

| Component | Action | Effect | Target |
|---|---|---|---|
| `onboarding_error_retry_button` | `retry_onboarding_init` | `transform_state` | Re-reads DataStore `onboarding_completed` flag → `loading` → `intro` on success; remains `error` on IOException |
| `onboarding_empty_skip_button` | `navigate_to_login` | `navigate` | `login` screen (bypasses educational flow) |
| `intro_next_button` | `step_next` | `transform_state` | `permissions_overview` (ViewModel `currentStep` 1→2) |
| `permissions_back_button` | `step_back` | `transform_state` | `intro` (ViewModel `currentStep` 2→1) |
| `permissions_next_button` | `step_next` | `transform_state` | `consent_explainer` (ViewModel `currentStep` 2→3) |
| `trust_back_button` | `step_back` | `transform_state` | `permissions_overview` (ViewModel `currentStep` 3→2) |
| `connect_hsbc_button` | `navigate_to_login` | `navigate` | `login` screen — stages `OBReadConsent1`, begins FAPI 1.0 Advanced app-to-app redirect to HSBC |
| `how_ob_works_button` | `open_ob_explainer` | `transform_state` | `ob_explainer_open` (sets `showObExplainerSheet=true`) |
| `ob_explainer_close_button` | `close_ob_explainer` | `transform_state` | `consent_explainer` (sets `showObExplainerSheet=false`) |

---

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| `onboarding_loading_indicator` | 48dp | 48dp | circular (strokeWidth 4dp) |
| `hero_illustration` | 240dp | 200dp | 0dp |
| `step_indicator` active dot | 10dp | 10dp | 9999 (circle) |
| `step_indicator` inactive dot | 8dp | 8dp | 9999 (circle) |
| `fapi_security_badge` (chip) | wrap content (≈ 240dp) | 32dp | 9999 (full pill) |
| `fca_regulated_badge` (chip) | wrap content (≈ 140dp) | 32dp | 9999 (full pill) |
| `intro_next_button` | match_parent − 32dp | 56dp | 28dp (extra_large) |
| `permissions_back_button` | ≈ 120dp (wrap) | 48dp | 24dp |
| `permissions_next_button` | ≈ 200dp (wrap) | 56dp | 28dp |
| `perm_accounts` (list item) | match_parent | 88dp min | 0dp |
| `perm_balances` (list item) | match_parent | 88dp min | 0dp |
| `perm_transactions` (list item) | match_parent | 88dp min | 0dp |
| `perm_standing_orders` (list item) | match_parent | 88dp min | 0dp |
| `perm_direct_debits` (list item) | match_parent | 88dp min | 0dp |
| `perm_statements` (list item) | match_parent | 88dp min | 0dp |
| `trust_back_button` | ≈ 120dp (wrap) | 48dp | 24dp |
| `connect_hsbc_button` | ≈ 200dp (wrap) | 56dp | 28dp |
| `how_ob_works_button` | match_parent | 40dp | 0dp (text button) |
| `legal_divider` | match_parent | 1dp | 0dp |
| `ob_explainer_sheet` (bottom sheet) | match_parent (393dp) | ≈ 540dp peek | 28dp (top corners) |
| `ob_explainer_close_button` | match_parent − 48dp | 56dp | 28dp |
