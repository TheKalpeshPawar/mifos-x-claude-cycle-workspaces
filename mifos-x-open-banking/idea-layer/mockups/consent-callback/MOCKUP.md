# Consent Callback — Visual Mockup

> Auto-generated from `screens/consent-callback/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Authorisation Callback

Canvas: 393×852dp · No top app bar · No bottom nav · Full-screen modal · Material 3 light theme

This is a deep-link redirect target — the user lands here from HSBC's authorisation portal after approving the FAPI PKCE flow. No chrome is shown to minimise distraction during the token exchange poll.

---

### State: loading

```
┌─────────────────────────────────────────────┐
│                                              │
│                                              │
│             [HSBC brand mark]                │  ← optional logo 48dp centred
│                                              │
│                  ◌                           │  ← loading_spinner circular #266489 48dp
│              (spinning)                      │
│                                              │
│   Completing your HSBC connection…          │  ← loading_label bodyMedium #41474D centred
│                                              │
│   This may take a few seconds.              │  ← loading_sub bodySmall #41474D centred
│                                              │
│                                              │
│                                              │
└─────────────────────────────────────────────┘
```

---

### State: content (success — auto-navigates)

```
┌─────────────────────────────────────────────┐
│                                              │
│              ✓                               │  ← success_icon check_circle 64dp #266489
│                                              │
│   Connected successfully!                   │  ← success_title headlineSmall #181C20
│                                              │
│   Your HSBC accounts are now linked.        │  ← success_body bodyMedium #41474D
│   Taking you to your accounts…             │
│                                              │
└─────────────────────────────────────────────┘
```

Auto-navigates to `accounts` after 1.5s delay (M3 motion, long 450ms ease-in-out).

---

### State: empty (AwaitingAuthorisation — consent not yet approved)

```
┌─────────────────────────────────────────────┐
│                                              │
│             [hourglass_empty]                │  ← icon 48dp #41474D centred
│                                              │
│   Still waiting for HSBC                    │  ← title headlineSmall #181C20
│   Your consent is pending approval.         │  ← body bodyMedium #41474D
│                                              │
│         [  Check again  ]                   │  ← retry_poll_button filled #266489
│         [  Cancel       ]                   │  ← cancel_button text → login
│                                              │
└─────────────────────────────────────────────┘
```

---

### State: error (token exchange failed / 400–401)

```
┌─────────────────────────────────────────────┐
│                                              │
│            [error_outline]                   │  ← icon 48dp #BA1A1A
│                                              │
│    Connection failed                        │  ← title headlineSmall #181C20
│  We couldn't complete your HSBC             │  ← body bodyMedium #41474D
│  connection. Please try again.              │
│                                              │
│         [  Try again  ]                     │  ← retry_button filled #266489 → login
│         [  Cancel     ]                     │  ← cancel_button text → home
│                                              │
└─────────────────────────────────────────────┘
```

---

### State: access_denied

```
┌─────────────────────────────────────────────┐
│                                              │
│              [block]                         │  ← icon 48dp #BA1A1A
│                                              │
│    Access not granted                       │  ← title headlineSmall #181C20
│  You declined the HSBC permissions.         │  ← body bodyMedium #41474D
│  No accounts have been linked.              │
│                                              │
│         [  Start over  ]                    │  ← restart_button filled #266489 → login
│                                              │
└─────────────────────────────────────────────┘
```

---

### State: security_error (PKCE state mismatch)

```
┌─────────────────────────────────────────────┐
│                                              │
│              [gpp_bad]                       │  ← icon 48dp #BA1A1A
│                                              │
│    Security check failed                    │  ← title headlineSmall #181C20
│  The authorisation response could not       │  ← body bodyMedium #41474D
│  be verified. This may indicate a          │
│  security issue. Please try again.         │
│                                              │
│         [  Start over  ]                    │  ← restart_button filled #266489 → login
│                                              │
└─────────────────────────────────────────────┘
```

---

### Component Hierarchy

```
(no shell — full screen, no top bar, no bottom nav)

loading_layout/ (stack vertical centred, state_binding=[loading])
│  ├── loading_spinner  (circular progress #266489 48dp)
│  ├── loading_label    (bodyMedium #41474D): "Completing your HSBC connection…"
│  └── loading_sub      (bodySmall #41474D): "This may take a few seconds."

success_layout/ (stack vertical centred, state_binding=[content])
│  ├── success_icon   (check_circle 64dp #266489)
│  ├── success_title  (headlineSmall #181C20): "Connected successfully!"
│  └── success_body   (bodyMedium #41474D): "Your HSBC accounts are now linked."

empty_layout/ (stack vertical centred, state_binding=[empty])
│  ├── icon            (hourglass_empty 48dp #41474D)
│  ├── title           (headlineSmall #181C20): "Still waiting for HSBC"
│  ├── body            (bodyMedium #41474D): "Your consent is pending approval."
│  ├── retry_poll_button (button filled → re-poll)
│  └── cancel_button   (button text → login)

error_layout/ (state_binding=[error])
│  ├── icon        (error_outline 48dp #BA1A1A)
│  ├── title       (headlineSmall #181C20): "Connection failed"
│  ├── body        (bodyMedium #41474D)
│  ├── retry_button (button filled → login)
│  └── cancel_button (button text → home)

access_denied_layout/ (state_binding=[access_denied])
│  ├── icon           (block 48dp #BA1A1A)
│  ├── title          (headlineSmall #181C20): "Access not granted"
│  ├── body           (bodyMedium #41474D)
│  └── restart_button (button filled → login)

security_error_layout/ (state_binding=[security_error])
│  ├── icon           (gpp_bad 48dp #BA1A1A)
│  ├── title          (headlineSmall #181C20): "Security check failed"
│  ├── body           (bodyMedium #41474D)
│  └── restart_button (button filled → login)
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| (auto on content) | auto_navigate | accounts |
| retry_poll_button (empty) | poll_consent_status | in-place re-poll |
| cancel_button (empty) | navigate_back | login |
| retry_button (error) | navigate_login | login |
| cancel_button (error) | navigate_home | home |
| restart_button (access_denied) | navigate_login | login |
| restart_button (security_error) | navigate_login | login |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| loading_spinner | 48dp | 48dp | circle |
| success_icon | 64dp | 64dp | circle |
| retry_poll_button | match_parent − 64dp | 48dp | 12dp |
| restart_button | match_parent − 64dp | 48dp | 12dp |
