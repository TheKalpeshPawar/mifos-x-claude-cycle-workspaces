# Standing Orders — Visual Mockup

> Auto-generated from `screens/standing-orders/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-31
> Content: `screens/standing-orders/demo-data.yaml`

**Implemented** — `feature/standing-orders`, account-scoped pushed screen. Third of the three
capability-gated list features, alongside `direct-debits` and `scheduled-payments`.

---

## Screen: Standing Orders

**Archetype** `index_list` · **Initial state** `loading`
**States** `loading · content · empty · unsupported · error`

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **visible** | `ui.yaml#shell.bottom_navigation_visible: true` |
| Top app bar | **visible**, title `{strings.standing_orders_screen_title}` | `ui.yaml#shell.top_app_bar_visible: true` |
| Top app bar leading | **back** | `ui.yaml#shell.top_app_bar_leading: back` |
| FAB | **absent** | `ui.yaml#shell.fab_visible: false` |

---

## State: loading

```
┌─────────────────────────────────────────┐
│  ←  Standing Orders                     │
├─────────────────────────────────────────┤
│                  ( ◌ )                   │  progress_indicator, circular
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

---

## State: content

```
┌─────────────────────────────────────────┐
│  ←  Standing Orders                     │
├─────────────────────────────────────────┤
│  3 Active · 1 Inactive                   │  SummaryLabel, computed in VM
│                                          │
│  ┌──────────────────────────────────┐   │
│  │ Jameson Lettings       ( Active ) │   │  creditor + status badge
│  │ 40-12-09 65872310                │   │  mono identification
│  │ £850.00 · Monthly on the 1st     │   │  amount + decoded frequency
│  │ Next 1 Aug 2026                  │   │
│  │ Ref RENT-FLAT12                  │   │
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │
│  │ Oakwood Savings        ( Active ) │   │
│  │ 23-05-80 11223344                │   │
│  │ £200.00 · Every 2 weeks          │   │
│  │ Next 4 Aug 2026                  │   │
│  │ Final 4 Aug 2027                 │   │  conditional — hasFinalPayment
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │
│  │ Old Gym Membership   ( Inactive ) │   │
│  │ 60-00-01 99887766                │   │
│  │ £29.00 · Monthly on the 15th     │   │
│  └──────────────────────────────────┘   │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

```
standing-orders/
├── TopAppBar → back + "Standing Orders"
├── summary_row: text (SummaryLabel)
├── standing_orders_list: list (vertical, items ← orders)
│   └── standing_order_card: card (radius.md, elevation 1)
│       ├── creditorName          (titleMedium)
│       ├── status_badge          (Active tonal | Inactive outline)
│       ├── creditorIdentification (bodySmall, mono)
│       ├── nextPaymentAmount + frequencyLabel (bodySmall, amount mono)
│       ├── nextPaymentDate       (bodySmall)
│       └── finalPaymentDate      (bodySmall) [visible_when hasFinalPayment]
└── BottomNav
```

| Element | Token | Notes |
|---|---|---|
| Card | `surfaceContainer`, radius `medium`, elevation `level1` | |
| Amount | mono, `semantic.money.neutral` | **unsigned** — a recurring instruction, not a movement |
| Identification | mono, `onSurfaceVariant` | sort code + account number |
| Active badge | tonal, `secondaryContainer` | |
| Inactive badge | outlined, `outline` border | |

**Frequency is decoded, never raw.** OBIE ships ISO 20022 codes — `IntrvlMnthDay`, `IntrvlWkDay`,
`IntrvlDay`, `IntrvlYear` — which a customer cannot read. A sealed `FrequencyDecoder` in the
ViewModel turns them into "Monthly on the 1st", "Every 2 weeks". Never render the raw code.

**`Final` appears only when there is one.** `hasFinalPayment` gates that row rather than printing
an em dash: an open-ended standing order has no final payment, and a blank labelled row implies
missing data rather than absent data.

**Interactions** — none. Read-only; this app cannot amend or cancel a standing order.

---

## State: empty

```
┌─────────────────────────────────────────┐
│  ←  Standing Orders                     │
├─────────────────────────────────────────┤
│                  ( ☐ )                   │  event_repeat
│         No standing orders                │
│   This account has no standing orders     │
│   set up.                                 │
├─────────────────────────────────────────┤
```

---

## State: unsupported

```
┌─────────────────────────────────────────┐
│  ←  Standing Orders                     │
├─────────────────────────────────────────┤
│                  ( ⓘ )                   │  info_outline, NOT error
│  Standing orders aren't available for     │
│  this account                             │
│   {uiState.message}                       │  ← ASPSP's own words, verbatim
│                                          │  NO retry
├─────────────────────────────────────────┤
```

| Element | Token | Notes |
|---|---|---|
| Icon | `info_outline`, `onSurfaceVariant` | **not** `error` |
| Body | `bodyMedium` on `onSurfaceVariant` | ASPSP explanation, verbatim |
| Retry | **absent** | nothing to retry |

`U000` recorded against `AccountEndpoint.StandingOrders` at `BankingStores.kt:344` before
rethrowing; the ViewModel checks `isUnsupportedForProduct()` ahead of classification. Identical
contract to `direct-debits` — these two are where the pattern is correct, and the reference for the
`scheduled-payments` fix landed 2026-07-30.

---

## State: error

```
┌─────────────────────────────────────────┐
│  ←  Standing Orders                     │
├─────────────────────────────────────────┤
│                  ( ! )                   │  error_outline, error
│    Couldn't load standing orders           │
│   Check your connection and try again.    │
│  [          Try again          ]          │
├─────────────────────────────────────────┤
```

Four kinds — `TokenExpired` 401, `ConsentRevoked` 403, `RateLimited` 429, `NetworkError` — mapped
to typed user-facing messages in the ViewModel.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| account-detail | standing-orders | Explore option, carrying `accountId` |
| standing-orders | account-detail | back |

Gated by `availableChipsFor`, corrected at runtime by `recordIfUnsupported`.
