# Beneficiaries — Visual Mockup

> Auto-generated from `screens/beneficiaries/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-31
> Content: `screens/beneficiaries/demo-data.yaml`

**Implemented** — `feature/beneficiaries`, `BeneficiariesRoute(accountId)`. Reached from the
account-detail Explore list (`AccountDetailChip.Beneficiaries`).

---

## Screen: Beneficiaries

**Archetype** `index_list` · **Initial state** `loading` · **States** `loading · content · empty · error`

Four states, **not five** — despite being product-gated at the *prediction* layer. `Beneficiaries`
is hidden on a credit card by `availableChipsFor`, but its store fetcher does **not** call
`recordIfUnsupported`, so no `U000` is ever recorded and no `unsupported` state exists. That is a
real asymmetry with `direct-debits` / `standing-orders` / `scheduled-payments`, whose fetchers do
record it. A deep-link visitor on an unsupported product lands on the generic error surface here.

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **visible** | `ui.yaml#shell` |
| Top app bar | **visible**, title `{strings.beneficiaries.screen_title}` | `ui.yaml#shell` |
| Top app bar leading | **back** — via `back_button` icon_button | `ui.yaml#components[back_button]` |
| FAB | **absent** | `ui.yaml#shell` |

---

## State: loading

```
┌─────────────────────────────────────────┐
│  ←  Beneficiaries                       │
├─────────────────────────────────────────┤
│                  ( ◌ )                   │  progress_indicator, circular
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

The search bar is **absent** while loading — searching nothing is meaningless, the same reasoning
that hides `accounts`' filter row in its loading and empty states.

---

## State: content

```
┌─────────────────────────────────────────┐
│  ←  Beneficiaries                       │
├─────────────────────────────────────────┤
│  ┌ 🔍 Search beneficiaries ──────────┐  │  search_bar
│  └──────────────────────────────────┘   │
│                                          │
│  ┌──────────────────────────────────┐   │
│  │ (JL)  Jameson Lettings           │   │  avatar + two_line row
│  │       Sort Code · 40-12-09 65872310│  │
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │
│  │ (JS)  John Sharma                │   │
│  │       Sort Code · 23-05-80 11223344│  │
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │
│  │ (EE)  EDF Energy                 │   │
│  │       Sort Code · 60-00-01 99887766│  │
│  └──────────────────────────────────┘   │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

```
beneficiaries/
├── TopAppBar
│   ├── back_button: icon_button (arrow_back)
│   └── title: "Beneficiaries"
├── beneficiary_search: search_bar
├── beneficiaries_list: list (vertical, items ← beneficiaries)
│   └── beneficiary_row: list_item (two_line)
│       ├── beneficiary_avatar: avatar (initials)
│       ├── headline: name (bodyLarge)
│       └── supporting: schemeLabel · identification (bodyMedium, mono)
└── BottomNav
```

| Element | Token | Notes |
|---|---|---|
| Row min height | `accessibility.min_touch_target_dp` | 48dp |
| Avatar | `secondaryContainer` / `onSecondaryContainer` | initials, not a photo — OBIE carries no payee imagery |
| Headline | `bodyLarge` on `onSurface` | payee name |
| Supporting | `bodyMedium` on `onSurfaceVariant`, mono | scheme + identification |
| Search bar | `form.field.radius` (8dp), `surfaceContainer` | |

**Search filters client-side.** `BeneficiariesAction` declares `Search` — renamed from a modelled
`filterBeneficiaries` in the 2026-07-28 reverse sync. No API round-trip; the payee list is already
resident.

**No monetary values anywhere.** A beneficiary is an identity, not a balance — so no mono amount
column and no `semantic.money` token binding on this screen.

**Interactions** — rows are **not tappable**. There is no beneficiary detail screen and this app
cannot add, edit or delete a payee (read-only under AISP consent).

---

## State: content — search with no matches

```
┌─────────────────────────────────────────┐
│  ←  Beneficiaries                       │
├─────────────────────────────────────────┤
│  ┌ 🔍 zzz ──────────────────────────┐   │  search_bar retains the query
│  └──────────────────────────────────┘   │
│                                          │
│                  ( 🔍 )                  │  search_no_results
│         No matches                        │
│   No beneficiaries match "zzz".           │
│                                          │
├─────────────────────────────────────────┤
```

A **distinct** component (`search_no_results`) from the empty state below, and the distinction
matters: this is still `content` — the account *has* payees, the query just matched none. The
search bar stays visible and keeps the query so the PSU can correct it. Collapsing this into
`empty` would tell the customer they have no payees when they have three.

---

## State: empty

```
┌─────────────────────────────────────────┐
│  ←  Beneficiaries                       │
├─────────────────────────────────────────┤
│                  ( ☐ )                   │  group_off / person_off
│         No beneficiaries                  │
│   This account has no saved payees.       │
│   Manage your consent in Settings →       │
│   Consents.                               │
├─────────────────────────────────────────┤
```

**Points at Settings rather than offering its own connect button** — the deliberate project-wide
convention. The connect/renew affordance lives only on the consent screens; a second entry point
here would fork the consent journey. `home` and `accounts` follow the same rule.

The search bar is hidden in this state — there is nothing to search.

---

## State: error

```
┌─────────────────────────────────────────┐
│  ←  Beneficiaries                       │
├─────────────────────────────────────────┤
│                  ( ! )                   │  error_outline, error
│    Couldn't load beneficiaries             │
│   Check your connection and try again.    │
│  [          Try again          ]          │
├─────────────────────────────────────────┤
```

Five error kinds: `TokenExpired` 401 · `ConsentRevoked` 403 · `RateLimited` 429 · `NetworkError` ·
`ServerError`.

Because there is no `unsupported` state, a `U000` product refusal also lands here — as
`ServerError`, with a Retry that cannot succeed. Narrower in practice than the
`scheduled-payments` defect was, since nothing records the refusal and the chip is normally hidden,
but the same shape. Worth knowing before treating this screen as a template for a gated feature.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| account-detail | beneficiaries | Explore option (`AccountDetailChip.Beneficiaries`), carrying `accountId` |
| beneficiaries | account-detail | `back_button` |

---

## Removed / renamed in the 2026-07-28 reverse sync

| Change | Detail |
|---|---|
| renamed | `filterBeneficiaries` → `Search` — `BeneficiariesAction` declares `Search` |
| removed | `loadBeneficiaries` action — the initial load is stream collection in `init{}` |
| removed | `navigateToConsents` / `navigateBack` actions — both are nav-host callbacks, not action members |
| removed | `AisApiService` DI — the ViewModel injects `BeneficiariesRepository`, not the raw API service |
