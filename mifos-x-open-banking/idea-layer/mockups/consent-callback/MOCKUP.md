# Authorisation Callback — Visual Mockup

> Auto-generated from `screens/consent-callback/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Authorisation Callback

Canvas: 393×852dp (Pixel 5) · No top app bar · No bottom nav · No FAB · Full-screen modal · Roboto font · Material 3 light theme · bg #F7F9FF

Shell (resolved from `ui.yaml#shell` override): ALL chrome suppressed — `bottom_navigation_visible: false`, `top_app_bar_visible: false`, `fab_visible: false`. This is a FAPI-1.0-Advanced OAuth redirect landing screen; no navigation chrome is rendered to maintain PSU focus during token exchange and consent-status polling.

---

### State: loading

(loading_layout: stack vertical · align=center · justify=center · padding=spacing.xl 48dp · state_binding=[loading])

```
┌──────────────────────────────────────────────────┐ 393dp
│                                                  │
│                                                  │
│                                                  │
│                       ◌                          │ ← loading_spinner  CircularProgressIndicator
│                   (spinning)                     │   variant:circular  diameter:48dp  stroke:4dp
│                                                  │   color #266489 (primary)
│                                                  │   a11y: "Verifying HSBC authorisation"
│                  [── 48dp ──]                    │ ← Spacer(spacing.xl = 48dp)
│                                                  │
│       Verifying your authorisation…             │ ← loading_headline  titleMedium
│                                                  │   16sp / w500 / lh24  #181C20 (onSurface)
│                                                  │   textAlign:center
│                  [── 8dp ──]                     │ ← Spacer(spacing.sm = 8dp)
│                                                  │
│  Securely exchanging credentials with HSBC.     │ ← loading_body  bodySmall
│       This takes a few seconds.                 │   12sp / w400 / lh16  #41474D (onSurfaceVariant)
│                                                  │   textAlign:center  maxWidth:280dp
│                                                  │
│                                                  │
└──────────────────────────────────────────────────┘
                    852dp tall
```

### Component Hierarchy — loading

```
Screen: Authorisation Callback  (ConsentCallbackUiState.Loading)
│  bg: #F7F9FF (surface)   no shell chrome
│
loading_layout  (Column, horizontalAlignment=Center, verticalArrangement=Center)
│  padding: 48dp all sides (spacing.xl)
│  fillMaxSize: true
│  a11y label: "Authorisation in progress"
│
├── loading_spinner  (CircularProgressIndicator)
│     variant: indeterminate / circular
│     size: 48dp   stroke: 4dp
│     color: #266489 (primary)
│     contentDescription: "Verifying HSBC authorisation"
│
├── Spacer(height = 48dp)   ← spacing.xl
│
├── loading_headline  (Text)
│     value: "Verifying your authorisation…"
│     style: titleMedium  size:16sp  weight:500  lineHeight:24sp
│     color: #181C20 (onSurface)
│     textAlign: Center
│
├── Spacer(height = 8dp)   ← spacing.sm
│
└── loading_body  (Text)
      value: "Securely exchanging credentials with HSBC. This takes a few seconds."
      style: bodySmall  size:12sp  weight:400  lineHeight:16sp
      color: #41474D (onSurfaceVariant)
      textAlign: Center   maxWidth: 280dp
```

---

### State: content

(success_layout: stack vertical · align=center · justify=center · padding=spacing.xl 48dp · state_binding=[content])
Auto-navigates to `accounts` after 1,500 ms via M3 Long easing (450ms cubic-bezier(0.2, 0.0, 0, 1.0)).

```
┌──────────────────────────────────────────────────┐
│                                                  │
│                                                  │
│                       ✓                          │ ← success_icon  check_circle  64dp
│                     (filled)                     │   tint #266489 (primary)
│                                                  │   a11y: "HSBC authorisation successful"
│                  [── 24dp ──]                    │ ← Spacer(spacing.lg = 24dp)
│                                                  │
│              Connected to HSBC                   │ ← success_headline  headlineSmall
│                                                  │   24sp / w400 / lh32  #181C20 (onSurface)
│                                                  │   textAlign:center
│                  [── 8dp ──]                     │ ← Spacer(spacing.sm = 8dp)
│                                                  │
│   Your account data is ready. Taking you to     │ ← success_body  bodyMedium
│           your accounts now.                    │   14sp / w400 / lh20  #41474D (onSurfaceVariant)
│                                                  │   textAlign:center  maxWidth:280dp
│                                                  │
│                                                  │
└──────────────────────────────────────────────────┘
```

Auto-navigates to `accounts` screen (→ `idea-layer/screens/accounts/`) after 1,500 ms.
Motion: M3 Long 450ms cubic-bezier(0.2, 0.0, 0, 1.0). Reduce-motion: navigate immediately.

### Component Hierarchy — content

```
Screen: Authorisation Callback  (ConsentCallbackUiState.Content)
│  bg: #F7F9FF (surface)   no shell chrome
│  auto-navigate → accounts after 1,500 ms
│
success_layout  (Column, horizontalAlignment=Center, verticalArrangement=Center)
│  padding: 48dp all sides (spacing.xl)
│  fillMaxSize: true
│  a11y label: "Authorisation complete"
│
├── success_icon  (Icon)
│     asset: check_circle (Material Symbols, Filled)
│     size: 64dp
│     tint: #266489 (primary)
│     contentDescription: "HSBC authorisation successful"
│
├── Spacer(height = 24dp)   ← spacing.lg
│
├── success_headline  (Text)
│     value: "Connected to HSBC"
│     style: headlineSmall  size:24sp  weight:400  lineHeight:32sp
│     color: #181C20 (onSurface)
│     textAlign: Center
│
├── Spacer(height = 8dp)   ← spacing.sm
│
└── success_body  (Text)
      value: "Your account data is ready. Taking you to your accounts now."
      style: bodyMedium  size:14sp  weight:400  lineHeight:20sp
      color: #41474D (onSurfaceVariant)
      textAlign: Center   maxWidth: 280dp
```

---

### State: empty

(awaiting_state: EmptyState · state_binding=[empty] · icon=hourglass_empty · AwaitingAuthorisation scenario)
Displayed when GET /account-access-consents/{ConsentId} returns `Status: AwaitingAuthorisation`
after a successful token exchange — HSBC has not yet updated the consent record.

```
┌──────────────────────────────────────────────────┐
│                                                  │
│                                                  │
│                       ⧗                          │ ← awaiting icon  hourglass_empty  48dp
│                                                  │   tint #41474D (onSurfaceVariant)
│                                                  │   neutral — not an error state
│                  [── 16dp ──]                    │
│                                                  │
│         Waiting for HSBC to confirm              │ ← awaiting_title  headlineSmall
│                                                  │   24sp / w400 / lh32  #181C20 (onSurface)
│                  [── 8dp ──]                     │
│                                                  │
│   HSBC has not yet updated the consent          │ ← awaiting_body  bodyMedium
│   status. Please wait a moment or try           │   14sp / w400 / lh20  #41474D (onSurfaceVariant)
│   again.                                        │   maxWidth:280dp  textAlign:center
│                                                  │
│                  [── 24dp ──]                    │
│                                                  │
│  ┌──────────────────────────────────────────┐   │ ← poll_again_button  FilledButton
│  │              Check again                 │   │   bg #266489  label #FFFFFF
│  └──────────────────────────────────────────┘   │   h:48dp  radius:12dp  labelLarge
│                                                  │   width: match_parent − 96dp (≈297dp)
│                                                  │
└──────────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: Authorisation Callback  (ConsentCallbackUiState.Empty)
│  bg: #F7F9FF (surface)   no shell chrome
│  trigger: ConsentStatus == AwaitingAuthorisation after token exchange
│
awaiting_state  (EmptyState, alignment=center, padding=48dp)
│  a11y label: "Waiting for HSBC to confirm authorisation"
│  icon: hourglass_empty   size:48dp   tint: #41474D (onSurfaceVariant)
│  title: "Waiting for HSBC to confirm"
│         headlineSmall / 24sp / w400 / #181C20
│  body:  "HSBC has not yet updated the consent status. Please wait a moment or try again."
│         bodyMedium / 14sp / w400 / #41474D
│
└── poll_again_button  (Button variant=filled)
      label: "Check again"
      a11y: "Check consent status again"
      bg: #266489 (primary)    label-color: #FFFFFF (onPrimary)
      height: 48dp   corner-radius: 12dp (M3 shape.cornerLarge)
      width: match_parent − 96dp (padding 48dp each side)
      on_click: poll_consent_status
        effect: call_api
        GET /account-access-consents/{ConsentId} via Ktorfit (client_credentials token)
        resolves → Loading then Content (Authorised) or stays Empty (still pending)
```

---

### State: error

(error_state: EmptyState variant=error · state_binding=[error] · icon=cancel)
Displayed on HTTP 400/401 during token exchange, `Status: Rejected`, `Status: Revoked`, or NetworkError.

```
┌──────────────────────────────────────────────────┐
│                                                  │
│                                                  │
│                       ✕                          │ ← error icon  cancel  48dp
│                                                  │   tint #BA1A1A (error)
│                                                  │
│                  [── 16dp ──]                    │
│                                                  │
│          Authorisation was declined              │ ← error_title  headlineSmall
│                                                  │   24sp / w400 / lh32  #181C20 (onSurface)
│                  [── 8dp ──]                     │
│                                                  │
│  HSBC reported that the consent was not         │ ← error_body  bodyMedium
│  approved. Please try connecting again or       │   14sp / w400 / lh20  #41474D (onSurfaceVariant)
│  contact HSBC if you believe this is            │   maxWidth:280dp  textAlign:center
│  an error.                                      │
│                                                  │
│                  [── 24dp ──]                    │
│                                                  │
│  ┌──────────────────────────────────────────┐   │ ← retry_button  FilledButton
│  │              Try again                   │   │   bg #266489  label #FFFFFF
│  └──────────────────────────────────────────┘   │   h:48dp  radius:12dp  width:≈297dp
│                                                  │
└──────────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
Screen: Authorisation Callback  (ConsentCallbackUiState.Error)
│  bg: #F7F9FF (surface)   no shell chrome
│  triggers: HTTP 400/401 token exchange · ConsentStatus.Rejected · ConsentStatus.Revoked · NetworkError
│
error_state  (EmptyState, variant=error, alignment=center, padding=48dp)
│  a11y label: "Authorisation was declined by HSBC"
│  icon: cancel   size:48dp   tint: #BA1A1A (error)
│  title: "Authorisation was declined"
│         headlineSmall / 24sp / w400 / #181C20
│  body:  "HSBC reported that the consent was not approved. Please try connecting again
│          or contact HSBC if you believe this is an error."
│         bodyMedium / 14sp / w400 / #41474D
│
└── retry_button  (Button variant=filled)
      label: "Try again"
      a11y: "Return to login to try connecting again"
      bg: #266489 (primary)    label-color: #FFFFFF (onPrimary)
      height: 48dp   corner-radius: 12dp
      width: match_parent − 96dp
      on_click: navigate_retry
        effect: navigate   target: login (→ idea-layer/screens/login/)
        side-effects: LocalStorage.clearOAuthState(), LocalStorage.clearConsentId()
                      Navigator.navigate(Route.Login)
```

---

### State: access_denied

(access_denied_state: EmptyState variant=error · state_binding=[access_denied] · icon=block)
Displayed immediately when the HSBC redirect URI carries `error=access_denied` — PSU actively declined
data sharing at the HSBC authorisation portal. No token exchange is attempted.

```
┌──────────────────────────────────────────────────┐
│                                                  │
│                                                  │
│                       ⊘                          │ ← access_denied icon  block  48dp
│                                                  │   tint #BA1A1A (error)
│                                                  │
│                  [── 16dp ──]                    │
│                                                  │
│              Access not shared                   │ ← denied_title  headlineSmall
│                                                  │   24sp / w400 / lh32  #181C20 (onSurface)
│                  [── 8dp ──]                     │
│                                                  │
│  You chose not to share your HSBC account       │ ← denied_body  bodyMedium
│  data. You can start again at any time.         │   14sp / w400 / lh20  #41474D (onSurfaceVariant)
│                                                  │   maxWidth:280dp  textAlign:center
│                                                  │
│                  [── 24dp ──]                    │
│                                                  │
│  ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐   │ ← denied_cta_button  OutlinedButton
│  │             Start over                   │   │   stroke #266489  label #266489  bg:transparent
│  └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘   │   h:48dp  radius:12dp  width:≈297dp
│                                                  │   outlined = lower-urgency voluntary action
└──────────────────────────────────────────────────┘
```

### Component Hierarchy — access_denied

```
Screen: Authorisation Callback  (ConsentCallbackUiState.AccessDenied)
│  bg: #F7F9FF (surface)   no shell chrome
│  trigger: HSBC redirect error=access_denied (PSU actively declined — no token exchange)
│
access_denied_state  (EmptyState, variant=error, alignment=center, padding=48dp)
│  a11y label: "Access to HSBC account data was not shared"
│  icon: block   size:48dp   tint: #BA1A1A (error)
│  title: "Access not shared"
│         headlineSmall / 24sp / w400 / #181C20
│  body:  "You chose not to share your HSBC account data. You can start again at any time."
│         bodyMedium / 14sp / w400 / #41474D
│
└── denied_cta_button  (Button variant=outlined)
      label: "Start over"
      a11y: "Start the account connection process again"
      stroke: #266489 (primary)   1dp border   bg: transparent
      label-color: #266489 (primary)
      height: 48dp   corner-radius: 12dp
      width: match_parent − 96dp
      note: outlined variant signals lower urgency — PSU voluntarily declined, not a failure
      on_click: navigate_retry
        effect: navigate   target: login (→ idea-layer/screens/login/)
        side-effects: LocalStorage.clearOAuthState(), LocalStorage.clearConsentId()
                      Navigator.navigate(Route.Login)
```

---

### State: security_error

(security_error_state: EmptyState variant=error · state_binding=[security_error] · icon=security)
Displayed immediately on FAPI state parameter or id_token nonce mismatch — potential CSRF or replay
attack detected. No token exchange is attempted; all local auth state is invalidated.

```
┌──────────────────────────────────────────────────┐
│                                                  │
│                                                  │
│                       🛡                          │ ← security_error icon  security  48dp
│                                                  │   tint #BA1A1A (error)
│                                                  │   (FAPI state/nonce mismatch — CSRF gate)
│                  [── 16dp ──]                    │
│                                                  │
│            Security check failed                 │ ← security_error_title  headlineSmall
│                                                  │   24sp / w400 / lh32  #181C20 (onSurface)
│                  [── 8dp ──]                     │
│                                                  │
│  The authorisation response could not be        │ ← security_error_body  bodyMedium
│  verified. Please start the connection          │   14sp / w400 / lh20  #41474D (onSurfaceVariant)
│  process again.                                 │   maxWidth:280dp  textAlign:center
│                                                  │
│                  [── 24dp ──]                    │
│                                                  │
│  ┌──────────────────────────────────────────┐   │ ← security_retry_button  FilledButton
│  │             Start again                  │   │   bg #266489  label #FFFFFF
│  └──────────────────────────────────────────┘   │   h:48dp  radius:12dp  width:≈297dp
│                                                  │   filled = highest-urgency action required
└──────────────────────────────────────────────────┘
```

### Component Hierarchy — security_error

```
Screen: Authorisation Callback  (ConsentCallbackUiState.SecurityError)
│  bg: #F7F9FF (surface)   no shell chrome
│  trigger: route_params.state ≠ stored oauth_state  OR  id_token nonce ≠ stored nonce
│  note: fires immediately, before any token exchange is attempted
│
security_error_state  (EmptyState, variant=error, alignment=center, padding=48dp)
│  a11y label: "Security verification failed"
│  icon: security   size:48dp   tint: #BA1A1A (error)
│  title: "Security check failed"
│         headlineSmall / 24sp / w400 / #181C20
│  body:  "The authorisation response could not be verified.
│          Please start the connection process again."
│         bodyMedium / 14sp / w400 / #41474D
│
└── security_retry_button  (Button variant=filled)
      label: "Start again"
      a11y: "Start the connection process again from login"
      bg: #266489 (primary)    label-color: #FFFFFF (onPrimary)
      height: 48dp   corner-radius: 12dp
      width: match_parent − 96dp
      note: STRONGER than navigate_retry — revokes all tokens to prevent replay exploitation
      on_click: navigate_login
        effect: navigate   target: login (→ idea-layer/screens/login/)
        side-effects: LocalStorage.clearAll(), TokenStore.revokeAll()
                      Navigator.navigate(Route.Login)
```

---

### Interaction Summary

| Component | Action | Effect | Target / Notes |
|---|---|---|---|
| poll_again_button (empty) | poll_consent_status | call_api | Re-polls GET /account-access-consents/{ConsentId} via Ktorfit; transitions → Loading, then resolves to Content or stays Empty |
| retry_button (error) | navigate_retry | navigate | login — clears oauth_state + ConsentId, then Route.Login |
| denied_cta_button (access_denied) | navigate_retry | navigate | login — clears oauth_state + ConsentId, then Route.Login |
| security_retry_button (security_error) | navigate_login | navigate | login — clearAll() + TokenStore.revokeAll() + Route.Login (full auth state purge) |
| (automatic, content) | auto-navigate | navigate | accounts — 1,500 ms after content state renders; M3 Long 450ms ease |

> **navigate_retry vs navigate_login**: Both route to `login`, but `navigate_login` also calls `LocalStorage.clearAll()` and `TokenStore.revokeAll()` — a complete purge appropriate for a security violation.

---

### Dimensions Table

| Component | Width | Height | Corner Radius | Notes |
|---|---|---|---|---|
| loading_spinner | 48dp | 48dp | circle | stroke-width 4dp · color #266489 |
| success_icon (check_circle) | 64dp | 64dp | — | tint #266489; larger to reinforce success |
| hourglass_empty icon | 48dp | 48dp | — | tint #41474D (neutral, not error) |
| cancel icon (error) | 48dp | 48dp | — | tint #BA1A1A (error) |
| block icon (access_denied) | 48dp | 48dp | — | tint #BA1A1A (error) |
| security icon (security_error) | 48dp | 48dp | — | tint #BA1A1A (error) |
| poll_again_button | match_parent − 96dp (≈297dp) | 48dp | 12dp | FilledButton · M3 shape.cornerLarge |
| retry_button | match_parent − 96dp (≈297dp) | 48dp | 12dp | FilledButton · M3 shape.cornerLarge |
| denied_cta_button | match_parent − 96dp (≈297dp) | 48dp | 12dp | OutlinedButton · border 1dp #266489 |
| security_retry_button | match_parent − 96dp (≈297dp) | 48dp | 12dp | FilledButton · M3 shape.cornerLarge |
| loading_layout / success_layout | match_parent (393dp) | match_parent (852dp) | — | padding 48dp all sides (spacing.xl) |
| awaiting_state / error_state / etc. | match_parent | match_parent | — | EmptyState · padding 48dp all sides |
