# Accounts — Visual Mockup

> Auto-generated from `screens/accounts/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-30
> Content: `screens/accounts/demo-data.yaml`

**Implemented** — `feature/accounts`, `AccountsScreen` / `AccountsViewModel`, bottom-nav tab
(`AccountsTab`, order 1). This mockup documents shipped behaviour, reverse-synced 2026-07-28.

---

## Screen: Accounts

**Archetype** `index_list` · **Initial state** `loading` · **States** `loading · content · empty · error`

Screen state is the shared `ScreenState<AccountsData>` from `core-base`, not a feature-local sealed
interface. It carries two members the four rendered states do not surface separately —
`NoNetwork` and `Unauthenticated` — which fold into the error surface.

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **visible** — Accounts tab active (tab 2 of 4) | `ui.yaml#shell.bottom_navigation_visible: true` |
| Top app bar | **visible**, title `{strings.accounts.screen.title}` | `ui.yaml#shell.top_app_bar_visible: true` |
| Top app bar leading | none — tab root | — |
| FAB | **absent** | `ui.yaml#shell.fab_visible: false` |

---

## State: loading — `AccountsSkeleton`

```
┌─────────────────────────────────────────┐
│  Accounts                               │
├─────────────────────────────────────────┤
│  ┌──────────────────────────────────┐   │
│  │ ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ │   │  shimmer, 96dp, radius.md
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │
│  │ ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ │   │  shimmer ×3
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │
│  │ ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ │   │
│  └──────────────────────────────────┘   │
├─────────────────────────────────────────┤
│  ☐ Home │ ■ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

```
accounts/
├── TopAppBar → "Accounts"
├── loading_skeleton: stack (vertical, gap spacing.sm, padding spacing.md)
│   └── shimmer ×3 (variant card, 96dp, radius.md)
└── BottomNav (Accounts active)
```

Three cards at the **real content height** (96dp), so the transition to content does not jump.
The filter row is absent while loading — filtering nothing is meaningless.

---

## State: content

```
┌─────────────────────────────────────────┐
│  Accounts                               │
├─────────────────────────────────────────┤
│  (All) ( Current ) ( Savings ) (Credit) │  chip_group, single-select
│                                          │
│  ┌──────────────────────────────────┐   │  account_card
│  │ ▣  CACC                          │   │  labelSmall, secondary
│  │    Current account ·· 3349       │   │  titleMedium
│  │    80-20-01 10203349    £21,530.92│   │  bodySmall / headlineSmall mono
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │
│  │ ▣  SVGS                          │   │
│  │    BMM ACCOUNT ·· 3695           │   │
│  │    80-12-25 90953695       £482.10│   │
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │
│  │ ▣  CARD                          │   │
│  │    Credit card •••• 7654         │   │
│  │    •••• •••• •••• 7654    £1,204.55│   │
│  │                    ( balance owed )│   │  badge, tonal, conditional
│  └──────────────────────────────────┘   │
├─────────────────────────────────────────┤
│  ☐ Home │ ■ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

```
accounts/
├── TopAppBar → "Accounts"
├── account_type_filter: chip_group (horizontal, single-select)
│   └── filter_all · filter_current · filter_savings · filter_credit   [type: chip]
├── accounts_list: list (vertical, items ← rows, key ← item.id)
│   └── account_card: card (elevation 1, radius.md, padding spacing.md)
│       └── stack (horizontal, center_vertical, gap spacing.md)
│           ├── account_type_icon: icon (icon.lg, primary, decorative)
│           ├── account_text_column: stack (vertical, weight 1)
│           │   ├── account_subtype: text (labelSmall, secondary)
│           │   ├── account_nickname: text (titleMedium)
│           │   └── account_number: text (bodySmall, on-surface-variant)
│           └── balance_column: stack (vertical, end)
│               ├── balance_amount: text (headlineSmall, end)
│               └── balance_owed_badge: badge (tonal) [visible_when isBalanceOwed]
└── BottomNav (Accounts active)
```

| Element | Token | Notes |
|---|---|---|
| Card | `surfaceContainer`, radius `medium`, elevation `level1` | tonal, no drop shadow |
| Type icon | `primary`, `icon.lg` | `decorative: true` — excluded from the a11y tree |
| Nickname | `titleMedium` | resolved by `accountDisplayName` in `core/ui` |
| Identifier | `bodySmall` on `onSurfaceVariant`, mono | `formatAccountIdentifier` |
| Balance | `headlineSmall`, mono, `semantic.money.neutral` | **unsigned** |
| Owed badge | tonal, `secondaryContainer` | credit cards only |
| Row target | `accessibility.min_touch_target_dp` | 48dp min |

**Four filter chips, and deliberately no Global.** `AccountFilter` declares only
`ALL / CURRENT / SAVINGS / CREDIT`. A Global Money wallet reports `CACC`, indistinguishable here
from a current account, so it already sits under Current; a Global chip could never match and would
render a permanently empty list. The only runtime signal is the free-text `Description`, which
account-detail surfaces instead.

**Interactions**

| Component | Action | Effect | Notes |
|---|---|---|---|
| `filter_*` | `FilterAccounts(ALL\|CURRENT\|SAVINGS\|CREDIT)` | `transform_state` | **client-side**, no API round-trip; re-emits `AccountsData` |
| `account_card` | `navigate_account_detail` | `navigate` | → `account-detail` with `accountId` |

Card tap is a **nav-host callback** (`accountsGraph(onNavigateToAccountDetail)`), not an
`AccountsAction` member — `AccountsAction` has only `FilterAccounts` and `RetryLoad`.

---

## State: empty — `AccountsEmpty`

```
┌─────────────────────────────────────────┐
│  Accounts                               │
├─────────────────────────────────────────┤
│                                          │
│                  ( ☐ )                   │  account_balance_wallet
│                                          │
│         No accounts to show               │
│                                          │
│   Your consent doesn't include any        │
│   accounts yet.                           │
│                                          │
├─────────────────────────────────────────┤
│  ☐ Home │ ■ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

No CTA. Connecting or renewing a consent lives on the consent screens, reached via Settings →
Consents — the same convention `beneficiaries` and `home` follow. A second entry point here would
fork the consent journey.

The filter row is hidden in empty: chips over an empty list imply filtering caused it.

---

## State: error — `AccountsError`

```
┌─────────────────────────────────────────┐
│  Accounts                               │
├─────────────────────────────────────────┤
│                                          │
│                  ( ! )                   │  error_outline, error, 64dp
│                                          │
│      Couldn't load your accounts          │
│                                          │
│   Check your connection and try again.    │
│                                          │
│  [          Try again          ]          │  retry_button, filled
├─────────────────────────────────────────┤
│  ☐ Home │ ■ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

| Element | Token | Notes |
|---|---|---|
| Icon | `error` | 64dp |
| Title | `headlineMedium`, centred | |
| Body | `bodyMedium` on `onSurfaceVariant` | |
| Retry | `primary`, radius `full` | |

**Interactions**

| Component | Action | Effect | Notes |
|---|---|---|---|
| `retry_button` | `RetryLoad` | `call_api` | re-runs the `combineContent` stream over **both** accounts and balances |

`ScreenState.NoNetwork` and `.Unauthenticated` both render here. Retry is always offered — every
error reaching this surface is transient or re-authorisable.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| accounts | `account-detail` | `account_card` tap, carrying `accountId` |

Resolves to an existing `screens/` directory. Accounts is a **tab**, so it has no inbound nav
reference — it is reached from the bottom bar.

---

## Removed in the 2026-07-28 reverse sync

Recorded so they are not reintroduced as "missing":

| Removed | Why |
|---|---|
| `consent_expiring` state | no such `ScreenState` or `UiState` member in source |
| `navigateReconfirmConsent` action | `AccountsAction` has only `FilterAccounts`, `RetryLoad` |
| `total_balance_summary` stat block | `AccountsContent` renders only the filter row and the card list |
| `filter_global` chip | `AccountFilter` declares four members, no Global |
