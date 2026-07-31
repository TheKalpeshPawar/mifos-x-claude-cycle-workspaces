# Account holder — Visual Mockup

> Auto-generated from `screens/account-holder/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-30
> Content: `screens/account-holder/demo-data.yaml`

**Implemented** — `feature/account-holder`, `AccountHolderRoute(accountId)`. **Renamed from
`profile`** in the 2026-07-28 reverse sync.

---

## Screen: Account holder

**Archetype** `detail_screen` · **Initial state** `loading` · **States** `loading · content · empty · error`

**Identity only.** The screen shows the account holder's name, type and contact rows — and nothing
else. Consent status, expiry, the permissions list and sign-out were all **removed**: consent and
sign-out live on the consent screens, reached via Settings → Consents. Event type is `Nothing`;
`Content` carries just the `PartyProfile`.

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **visible** | `ui.yaml#shell.bottom_navigation_visible: true` |
| Top app bar | **visible** | `ui.yaml#shell` |
| Top app bar leading | **back** | `ui.yaml#shell.top_app_bar_leading: back` |
| FAB | **absent** | `ui.yaml#shell` |

---

## State: loading

```
┌─────────────────────────────────────────┐
│  ←  Account holder                      │
├─────────────────────────────────────────┤
│                  ( ◌ )                   │  loading_indicator
│         Loading account holder…           │  loading_caption
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

One of the few loading states in the app with a **caption** beside the spinner. The party endpoint
sits behind a revocable consent and can be slower than a balance read; the caption stops a slow
fetch reading as a hang, the same reasoning `payment-consent` uses for its stage detail.

---

## State: content

```
┌─────────────────────────────────────────┐
│  ←  Account holder                      │
├─────────────────────────────────────────┤
│  ┌──────────────────────────────────┐   │  identity_card
│  │              (MN)                 │   │  avatar — initials
│  │           Mr Nico                 │   │  display_name, headlineSmall
│  │       Account holder              │   │  role_label, bodyMedium
│  └──────────────────────────────────┘   │
│                                          │
│  CONTACT                                 │  identity_section_header
│  ┌──────────────────────────────────┐   │
│  │ ✉  Email                          │   │  email_row
│  │    nico.m@example.co.uk           │   │
│  ├──────────────────────────────────┤   │
│  │ ☎  Mobile                         │   │  mobile_row
│  │    +44 7700 900312                │   │
│  ├──────────────────────────────────┤   │
│  │ ⌂  Address                        │   │  address_row
│  │    12 Chandler Way, London        │   │
│  │    E14 9GE                        │   │
│  └──────────────────────────────────┘   │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

```
account-holder/
├── TopAppBar → back + "Account holder"
├── identity_card: card
│   ├── avatar: avatar (initials)
│   ├── display_name: text (headlineSmall)
│   └── role_label: text (bodyMedium, on-surface-variant)
├── identity_section_header: section_header
└── identity_section: stack
    ├── email_row: list_item
    ├── mobile_row: list_item
    └── address_row: list_item
└── BottomNav
```

| Element | Token | Notes |
|---|---|---|
| Identity card | `surfaceContainer`, radius `medium`, elevation `level1` | centred content |
| Avatar | `secondaryContainer` / `onSecondaryContainer` | initials — OBIE carries no party imagery |
| Display name | `headlineSmall` on `onSurface` | |
| Role label | `bodyMedium` on `onSurfaceVariant` | e.g. "Account holder" |
| Row label | `bodySmall` on `onSurfaceVariant` | |
| Row value | `bodyLarge` on `onSurface` | |
| Leading icon | `onSurfaceVariant`, 24dp | |

**No money tokens and no mono binding** — this screen shows an identity, not a figure.

**Rows are not tappable.** No mailto, no tel, no map. This is an AISP read of `OBReadParty2`; the
app displays the contact details the bank holds, it does not act on them.

**Interactions** — back only. `PartyProfile` is read from the memory-cached `partyStore` via the
stateless `ProfileRepository` (kept under its old `core/data` name after the screen rename).

---

## State: empty

```
┌─────────────────────────────────────────┐
│  ←  Account holder                      │
├─────────────────────────────────────────┤
│                  ( ☐ )                   │  person_off
│      No account holder details             │
│   The bank didn't return party            │
│   information for this account.            │
├─────────────────────────────────────────┤
```

A successful fetch that carried no party record. No CTA — nothing the customer can do.

---

## State: error

```
┌─────────────────────────────────────────┐
│  ←  Account holder                      │
├─────────────────────────────────────────┤
│                  ( ! )                   │  error_outline, error
│   Couldn't load account holder details     │
│   Check your connection and try again.    │
│  [          Try again          ]          │
├─────────────────────────────────────────┤
```

Retry calls `stream.refresh()` on the `ScreenDataStream` the ViewModel owns.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| account-detail | account-holder | **"Account holder" chip** (`AccountDetailChip.Party`), carrying `accountId` |
| account-holder | account-detail | back |

**`accountId` is always the account-detail nav argument, never empty.** That matters: the deleted
Settings → Profile row passed an empty `selectedAccountId`, producing a malformed
`GET /accounts//party` → 403. Repointing the chip off its dead `PlaceholderScreen` fixed the class
of bug, not just the route.

The chip's enum member is still named `Party` in source — only the screen was renamed.

---

## Removed in the 2026-07-28 reverse sync

| Removed | Where it lives now |
|---|---|
| Consent status + expiry | `consent-detail` |
| Permissions list | `consent-detail` |
| Sign-out | `consent-detail` "Remove access" — the app's **only** logout path |
| Settings → Profile row | deleted; entry is the account-detail chip |
| `PartyRoute` placeholder | deleted |
