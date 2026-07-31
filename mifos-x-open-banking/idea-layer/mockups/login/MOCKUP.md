# Login — Visual Mockup

> Auto-generated from `screens/login/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-31

**Implemented** — `feature/login`. Two entry points: `LoginRoute` (from onboarding, inside
`authGraph`) and **`LoginRenewRoute`** (from the consent screens, inside the authenticated host,
without the onboarding intro).

---

## Screen: Connect your bank

**Archetype** `auth` · **Initial state** `content`
**States** `content · loading · authorising · error · empty`

**Initial state is `content`, not `loading`** — unusual in this app, and correct. Nothing is
fetched on entry: the screen renders immediately and only starts work when the PSU taps Connect.

**There is no password field, and never will be.** The PSU authenticates **app-to-app at HSBC**
under FAPI 1.0 Advanced. This app never sees a credential — the single most important thing the
design has to communicate.

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **hidden** | `ui.yaml#shell` |
| Top app bar | **visible** | `ui.yaml#shell` |
| Top app bar leading | **back** from `LoginRenewRoute`; **none** from onboarding | route-dependent |
| FAB | **absent** | `ui.yaml#shell` |

---

## State: content

```
┌─────────────────────────────────────────┐
│  ←  Connect your bank                   │  back only on LoginRenewRoute
├─────────────────────────────────────────┤
│                                          │
│            ┌──────────────┐              │
│            │   HSBC UK    │              │  bank_card
│            │   Personal   │              │
│            └──────────────┘              │
│                                          │
│   You'll be taken to HSBC to sign in     │
│   and choose what to share. This app      │
│   never sees your password.               │
│                                          │
│   What you'll share                       │
│   • Accounts and balances                 │  permission preview
│   • Transactions                          │  BEFORE consent is staged
│   • Standing orders, direct debits        │
│   • Beneficiaries and statements          │
│   • Account holder details                │
│                                          │
│   ( FAPI 1.0 Advanced )  ( 90-day consent )│  trust chips
│                                          │
│  [        Connect with HSBC        ]      │  primary CTA
└─────────────────────────────────────────┘
   no bottom nav
```

| Element | Token | Notes |
|---|---|---|
| Bank card | `surfaceContainer`, radius `medium`, elevation `level1` | |
| Explainer | `bodyMedium` on `onSurfaceVariant` | password-free claim leads |
| Permission bullets | `bodyMedium` on `onSurface` | **full list, untruncated** |
| Trust chips | assist, `secondaryContainer` | non-interactive badges |
| CTA | `primary`, radius `full`, filled | |

**The permission list appears here, before consent is staged.** DESIGN.md's rule — *"always
explicit, never truncated"* — applies at the point of asking, not only at the point of review. A
PSU should know what they are about to authorise before they leave the app.

**90-day consent is stated up front** (SCA-RTS Art 36(6) / Art 10A), not discovered at expiry.

**Interactions**

| Component | Action | Effect | Notes |
|---|---|---|---|
| `connect_button` | `StartOAuth` | `call_api` | creates the consent, builds the authorize URL, stashes `state`/`nonce`/`consentId` in `PendingAuthStore`, then `BrowserLauncher.launch(url)` |

---

## State: loading

```
┌─────────────────────────────────────────┐
│                  ( ◌ )                   │
│         Preparing your connection…        │
└─────────────────────────────────────────┘
```

`LoginRepository.createConsentAndBuildAuthorizationUrl()` — POST `/account-access-consents` on a
**client-credentials** token, returning the authorize URL plus `state`, `nonce` and `consentId`.
Brief, but a real network round-trip.

---

## State: authorising

```
┌─────────────────────────────────────────┐
│                  ( ◌ )                   │
│         Opening HSBC…                     │
│                                          │
│   Continue in your browser. You'll come   │
│   back here automatically.                │
└─────────────────────────────────────────┘
```

**The app is no longer in the foreground.** The PSU is at HSBC completing SCA. This state exists so
that returning to a backgrounded app shows something coherent rather than a stale form.

The copy sets the expectation that return is **automatic** — it is: HSBC's redirect re-enters via
`ConsentRedirectBus`, and `consent-callback` takes over. There is no "paste the code" step and no
manual return button.

---

## State: error

```
┌─────────────────────────────────────────┐
│                  ( ! )                   │  error_outline, error
│      Couldn't start the connection         │
│   Check your connection and try again.    │
│  [          Try again          ]          │
└─────────────────────────────────────────┘
```

Consent-creation failures — transport, or the ASPSP refusing to stage. Retry re-runs
`StartOAuth` from the beginning, minting a **fresh** `state`/`nonce`; a stale pending
authorisation is never reused.

---

## State: empty

Synthetic — no configured bank brand to offer. `default_brand: uk-personal` is set in
`PROJECT_CONFIG.yaml`, so there is no production path to it. It exists so the state surface is
exhaustive and testable, like `settings`' Empty and Error.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| user-onboarding | login (`LoginRoute`) | "Continue" |
| consent-list · consent-detail | login (**`LoginRenewRoute`**) | Connect HSBC / Reconnect / Reconfirm access |
| login | *external browser* | `BrowserLauncher.launch(authorizeUrl)` |
| *(redirect)* | `consent-callback` | via `ConsentRedirectBus` — **not** a navigation from here |

**The two routes matter.** `LoginRoute` sits in `authGraph` and shows no back arrow — the PSU came
from onboarding and has nowhere to return to. `LoginRenewRoute` sits inside the authenticated host
and **does** show back, because the PSU came from Settings → Consents and may reasonably change
their mind.

---

## What this screen deliberately does not have

| Absent | Why |
|---|---|
| Password / PIN field | The PSU authenticates at HSBC. This app never sees a credential — FAPI 1.0 Advanced, `private_key_jwt`, PKCE S256 |
| "Remember me" | There is no app-side identity to remember; the consent *is* the session |
| Biometric prompt | Not shipped. Removed from the settings spec in the 2026-07-28 reverse sync |
| Bank picker | Single brand (`uk-personal`). The bank card states which bank, it does not offer a choice |
| Manual code entry | Return is automatic via `ConsentRedirectBus` |
