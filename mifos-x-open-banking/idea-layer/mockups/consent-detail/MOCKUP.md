# Consent detail — Visual Mockup

> Auto-generated from `screens/consent-detail/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-31

**Implemented** — `feature/consent-detail`. Reached from `consent-list`. **The app's only
sign-out surface.**

---

## Screen: Consent detail

**Archetype** `detail_screen` · **Initial state** `loading`
**States** `loading · content · revoke_confirm · revoking · error · empty`

Six states, two of which exist purely to make revocation safe. `revoke_confirm` is a **gate with no
API call**; `revoking` is a **lock**. Together they are the second `irreversible_action` surface in
the app, alongside send-money's review step.

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **visible** — More tab active | `ui.yaml#shell` |
| Top app bar | **visible** | `ui.yaml#shell` |
| Top app bar leading | **back** | `ui.yaml#shell` |
| FAB | **absent** | `ui.yaml#shell` |

---

## State: loading

```
┌─────────────────────────────────────────┐
│  ←  Consent                             │
├─────────────────────────────────────────┤
│                  ( ◌ )                   │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ■ More  │
└─────────────────────────────────────────┘
```

---

## State: content

```
┌─────────────────────────────────────────┐
│  ←  Consent                             │
├─────────────────────────────────────────┤
│  ┌──────────────────────────────────┐   │
│  │ 🛡  HSBC UK Personal   ( Active ) │   │
│  │                                    │   │
│  │ Consent ID   812774903            │   │  mono
│  │ Connected    29 Jun 2026          │   │
│  │ Expires      27 Sep 2026          │   │
│  └──────────────────────────────────┘   │
│                                          │
│  WHAT YOU'RE SHARING                     │
│  ┌──────────────────────────────────┐   │
│  │ • Accounts and balances           │   │  full list, NEVER truncated
│  │ • Transactions                    │   │
│  │ • Standing orders, direct debits  │   │
│  │ • Beneficiaries and statements    │   │
│  │ • Account holder details          │   │
│  └──────────────────────────────────┘   │
│                                          │
│  [        Reconfirm access        ]      │  tonal → LoginRenewRoute
│           Remove access                  │  text, error-tinted label
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ■ More  │
└─────────────────────────────────────────┘
```

| Element | Token | Notes |
|---|---|---|
| Card | `surfaceContainer`, radius `medium`, elevation `level1` | |
| Consent ID | `bodyMedium`, mono, `onSurfaceVariant` | |
| Permission bullets | `bodyMedium` on `onSurface` | full list, untruncated |
| Reconfirm | tonal, `secondaryContainer` | |
| Remove access | text button, `error` label | destructive, **lowest** emphasis |

**Remove access is a text button, not a filled error-red one.** Weight comes from the confirmation
gate, not from alarm colour — the same principle as send-money's confirm CTA staying `primary`. A
prominent red button invites a mis-tap on the one action that ends the session.

**Interactions**

| Component | Action | Effect |
|---|---|---|
| Reconfirm access | navigate | → `login` (`LoginRenewRoute`) |
| Remove access | `ShowRevokeConfirm` | `transform_state` — **no API call** |

---

## State: revoke_confirm

```
┌─────────────────────────────────────────┐
│  ←  Consent                             │
├─────────────────────────────────────────┤
│              ( dimmed content )          │
│  ╭──────────────────────────────────╮   │  dialog
│  │  Remove access?                   │   │
│  │                                    │   │
│  │  This signs you out and stops      │   │
│  │  this app seeing your HSBC         │   │
│  │  account information. You can      │   │
│  │  reconnect at any time.            │   │
│  │                                    │   │
│  │        Cancel      Remove access   │   │  same-weight pair
│  ╰──────────────────────────────────╯   │
└─────────────────────────────────────────┘
```

**A gate, and nothing has happened yet.** Tapping Remove access opens this dialog and makes **no
API call**. It satisfies the `irreversible_action` contract:

1. A distinct surface stating exactly what will be committed.
2. The confirm names the action — "Remove access", not "OK".
3. A **same-weight escape** adjacent to it — Cancel is not smaller or greyer.
4. Confirming locks the UI (see `revoking`), so double-submission is impossible.

The copy states both consequences — signed out **and** data access stops — plus the reversibility
("reconnect at any time"). That last clause is the honest difference from a payment: consent
revocation is destructive but **reversible**; a payment is not.

---

## State: revoking

```
┌─────────────────────────────────────────┐
│                                          │
│                  ( ◌ )                   │
│         Removing access…                  │
│                                          │
└─────────────────────────────────────────┘
   all controls locked
```

A lock state. `AppLogout.logOut()` runs three steps **in order**:

1. **Best-effort revoke** — `consentRevokeRepository.revokeConsent(consentId())` wrapped in
   `runCatching`. An expired, already-revoked, 404 or network-failed consent still proceeds.
2. **`consentSession.forgetAll()`** — removes the PSU tokens. **This is the actual logout.** The
   tokens live in secure `Settings` via `SettingsConsentSession`, *not* in the DataStore
   `UserData`, so `clearUserData()` alone could never sign the user out.
3. **`userDataRepository.clearUserData()` + `storeCacheManager.clearAll()`**.

Step 1 being best-effort is deliberate: a PSU must be able to sign out even when the bank is
unreachable. Step 2 is why the order cannot be rearranged.

On completion the ViewModel raises `ConsentDetailEvent.LoggedOut`.

---

## State: empty

The consent id resolved to nothing — already revoked elsewhere, or session cleared. Offers
**Connect HSBC** → `LoginRenewRoute`, matching `consent-list`'s empty state.

---

## State: error

Standard error surface with retry. A **failed revoke does not land here** — `AppLogout` swallows it
by design and proceeds to sign out locally.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| consent-list | consent-detail | consent card tap |
| consent-detail | `login` | Reconfirm access / Connect HSBC → `LoginRenewRoute` |
| consent-detail | **onboarding** | after `LoggedOut` |

**Sign-out navigation is explicit, not reactive.** `ConsentDetailEvent.LoggedOut` bubbles through
an `onLoggedOut` callback threaded `RootNavScreen → authenticatedGraph → authenticatedNavbarGraph →
AuthenticatedNavbarNavigationScreen → consentDetailScreen`, where the root navigator routes to
`authGraph`. Nothing observes `ConsentSession` reactively — deliberately.

---

## Why this screen owns logout

The account-holder screen used to offer sign-out; it is now identity-only. `AppLogout`
(`core/data/.../user/AppLogout.kt`, Koin `single`) is the **one** logout path — reuse it for any
future sign-out surface rather than re-implementing revoke + forget + clear.
