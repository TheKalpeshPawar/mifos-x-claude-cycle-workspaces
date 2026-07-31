# Consent list — Visual Mockup

> Auto-generated from `screens/consent-list/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-30
> Content: `screens/consent-list/demo-data.yaml`

**Implemented** — `feature/consent-list`, reached only from **Settings → Manage consents**.

---

## Screen: Manage consents

**Archetype** `index_list` · **Initial state** `loading`
**States** `loading · content · empty · error · error_auth`

**A list of exactly one.** Despite the name, this screen shows the **current** connection only —
it reads `session.consentId()` and streams that single consent via
`ConsentDetailRepository.consentStream` + `consentDetailStore`, the same one-consent path the
detail screen uses. There is **no device-side consent history**.

**Five states — `error_auth` is split out** from generic `error` because an expired or revoked
consent is not a failure to retry; it is a state the PSU must resolve by re-authorising.

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **visible** | `ui.yaml#shell` |
| Top app bar | **visible** | `ui.yaml#shell` |
| Top app bar leading | **back** — pushed from Settings | `ui.yaml#shell` |
| FAB | **absent** | `ui.yaml#shell` |

---

## State: loading

```
┌─────────────────────────────────────────┐
│  ←  Manage consents                     │
├─────────────────────────────────────────┤
│                  ( ◌ )                   │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ■ More  │
└─────────────────────────────────────────┘
```

More stays the active tab — this screen is pushed from Settings, not a tab root.

---

## State: content

```
┌─────────────────────────────────────────┐
│  ←  Manage consents                     │
├─────────────────────────────────────────┤
│  ┌──────────────────────────────────┐   │  consent_card
│  │ 🛡  HSBC UK Personal              │   │
│  │    ( Active )                     │   │  status chip
│  │                                    │   │
│  │ Connected  29 Jun 2026            │   │
│  │ Expires    27 Sep 2026            │   │
│  │                                    │   │
│  │ Sharing                            │   │
│  │ • Accounts and balances            │   │  permission list — NEVER truncated
│  │ • Transactions                     │   │
│  │ • Standing orders, direct debits   │   │
│  │ • Beneficiaries and statements     │   │
│  │ • Account holder details           │   │
│  │                                 ›  │   │
│  └──────────────────────────────────┘   │  TAP → consent-detail
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ■ More  │
└─────────────────────────────────────────┘
```

```
consent-list/
├── TopAppBar → back + "Manage consents"
├── consent_card: card (tappable → consent-detail)
│   ├── brand + status chip
│   ├── connected / expires rows
│   └── permission list (full, untruncated)
└── BottomNav (More active)
```

| Element | Token | Notes |
|---|---|---|
| Card | `surfaceContainer`, radius `medium`, elevation `level1` | tappable |
| Active chip | tonal, `secondaryContainer` | |
| Dates | `bodyMedium`, `onSurfaceVariant` | |
| Permission bullets | `bodyMedium` on `onSurface` | |

**The permission list is never truncated.** DESIGN.md names the consent card the trust-critical
surface: *"clear 'what you're sharing' permission list, expiry, and a revoke action — always
explicit, never truncated."* No "and 3 more", no collapsed accordion. This is what the customer
agreed to share; hiding part of it behind a tap is the one thing this screen must not do.

**90-day reconfirmation.** SCA-RTS Art 36(6) / Art 10A — the expiry row is a regulatory fact, not
a convenience.

**Interactions**

| Component | Action | Target |
|---|---|---|
| `consent_card` | navigate | `consent-detail` |

---

## State: empty

```
┌─────────────────────────────────────────┐
│  ←  Manage consents                     │
├─────────────────────────────────────────┤
│                  ( ☐ )                   │
│      No bank connected                    │
│   Connect your HSBC accounts to get       │
│   started.                                │
│                                          │
│  [        Connect HSBC        ]           │  → LoginRenewRoute
├─────────────────────────────────────────┤
```

`session.consentId()` returned `null`.

**This is one of the few empty states in the app that *does* carry a CTA** — and the reason is the
same convention that keeps CTAs off `home`, `accounts` and `beneficiaries`: the connect/renew
affordance lives **only** on the consent screens. This *is* a consent screen, so the button belongs
here.

"Connect HSBC" navigates to **`LoginRenewRoute`** — the login screen reached *inside* the
authenticated host, without the onboarding intro.

---

## State: error_auth

```
┌─────────────────────────────────────────┐
│  ←  Manage consents                     │
├─────────────────────────────────────────┤
│                  ( ⚠ )                    │
│      Your connection has expired          │
│   Reconnect to keep seeing your account   │
│   information.                            │
│                                          │
│  [         Reconnect         ]            │  → LoginRenewRoute
├─────────────────────────────────────────┤
```

**Split from generic `error` deliberately.** An expired or revoked consent is not a transient
failure — retrying the same call fails identically. The affordance is **Reconnect**, not Retry, and
it routes to `LoginRenewRoute` rather than repeating a doomed request.

The glyph is a warning, not an error-red cross: an expired consent is the system working as
designed (90-day reconfirmation), not a fault.

---

## State: error

```
┌─────────────────────────────────────────┐
│  ←  Manage consents                     │
├─────────────────────────────────────────┤
│                  ( ! )                   │  error_outline, error
│    Couldn't load your consent              │
│  [          Try again          ]          │
├─────────────────────────────────────────┤
```

Transport and unexpected server failures only. Auth failures route to `error_auth` above.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| settings | consent-list | "Manage consents" row |
| consent-list | `consent-detail` | consent card tap |
| consent-list | `login` (`LoginRenewRoute`) | "Connect HSBC" / "Reconnect" |
| consent-list | settings | back |

All resolve to existing `screens/` directories.

---

## Note on the consent-management cluster

`consent-list` and `consent-detail` share one data path (`consentDetailStore`), which is kept in
**`ConsentStores.kt`** apart from `BankingStores` because consent management runs on a
**client-credentials token minted per fetch**, not the PSU bearer.
