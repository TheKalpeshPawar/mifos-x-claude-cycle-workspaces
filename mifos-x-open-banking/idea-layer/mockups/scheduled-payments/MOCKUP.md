# Scheduled payments — Visual Mockup

> Auto-generated from `screens/scheduled-payments/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-30
> Content: `screens/scheduled-payments/demo-data.yaml`

**Implemented** — `feature/scheduled-payments`, account-scoped pushed screen. Reached from the
account-detail Explore list, gated per product.

---

## Screen: Scheduled payments

**Archetype** `index_list` · **Initial state** `loading`
**States** `loading · content · empty · unsupported · error`

Five states. `unsupported` was added **2026-07-30** — see the note under that variant; until then
this feature declared four, unlike both its capability-gated siblings.

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **visible** | `ui.yaml#shell.bottom_navigation_visible: true` |
| Top app bar | **visible**, title `{strings.sp_screen_title}` | `ui.yaml#shell.top_app_bar_visible: true` |
| Top app bar leading | **back** — account-scoped pushed screen | `ui.yaml#shell.top_app_bar_leading: back` |
| FAB | **absent** | `ui.yaml#shell.fab_visible: false` |

---

## State: loading

```
┌─────────────────────────────────────────┐
│  ←  Scheduled payments                  │
├─────────────────────────────────────────┤
│                                          │
│                  ( ◌ )                   │  progress_indicator, circular
│                                          │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

A centred spinner, not a shimmer skeleton. The list length is unknown up front (unlike `accounts`,
where three cards are always plausible), so a skeleton would guess at a shape it cannot know.

---

## State: content

```
┌─────────────────────────────────────────┐
│  ←  Scheduled payments                  │
├─────────────────────────────────────────┤
│  ┌──────────────────────────────────┐   │
│  │ HMRC Self Assessment             │   │  payee, titleMedium
│  │ 08-32-00 12001039                │   │  mono, on-surface-variant
│  │ ( 📅 Execution date )   GBP 842.00│   │  type chip + amount (mono)
│  │ HMRC-SA-2526                     │   │  reference, bodySmall
│  │ Thu 31 Jul 2026                  │   │  scheduled date
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │
│  │ Northern Gas                     │   │
│  │ 20-45-77 30021144                │   │
│  │ ( ↓ Arrival date )      GBP 96.40│   │
│  │ NG-Q3-2026                       │   │
│  │ Mon 3 Aug 2026                   │   │
│  └──────────────────────────────────┘   │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

```
scheduled-payments/
├── TopAppBar → back + "Scheduled payments"
├── scheduled_payments_list: list (vertical, items ← payments)
│   └── scheduled_payment_card: card (radius.md, elevation 1)
│       ├── payeeName          (titleMedium)
│       ├── creditorIdentification (bodySmall, mono, on-surface-variant)
│       ├── scheduledType chip + amountLabel (mono)
│       ├── reference          (bodySmall, on-surface-variant)
│       └── scheduledDateLabel (bodySmall)
└── BottomNav
```

| Element | Token | Notes |
|---|---|---|
| Card | `surfaceContainer`, radius `medium`, elevation `level1` | |
| Amount | mono, `semantic.money.neutral` | **unsigned** — a scheduled instruction is not a movement |
| Sort code / account no. | mono, `onSurfaceVariant` | `08-32-00 12001039` |
| Type chip | tonal, `secondaryContainer` | |
| Date | `bodySmall` | `EEE d MMM yyyy` — "Thu 31 Jul 2026" |

**The `scheduledType` chip carries real meaning, not decoration.** `Execution date` (icon
`calendar_today`) means the money **leaves** the account that day; `Arrival date` (icon
`arrow_downward`) means funds **arrive at the beneficiary** that day. Those are different promises,
and the enum → label mapping lives with the composable that renders it.

Read-only under AISP consent (`ReadScheduledPaymentsDetail`). There is no edit or cancel affordance —
this app reads scheduled payments, it does not manage them.

**Interactions** — none. Cards are not tappable; there is no scheduled-payment detail screen.

---

## State: empty

```
┌─────────────────────────────────────────┐
│  ←  Scheduled payments                  │
├─────────────────────────────────────────┤
│                                          │
│                  ( ☐ )                   │  schedule glyph
│                                          │
│       No scheduled payments               │
│                                          │
│   This account has no future-dated        │
│   payments set up.                        │
│                                          │
├─────────────────────────────────────────┤
```

**Empty means the bank answered "none".** The fetch succeeded and returned an empty
`Data.ScheduledPayment[]` — a real answer, not a failure. Distinct from `unsupported` below, which
means the question could not be asked at all.

---

## State: unsupported

```
┌─────────────────────────────────────────┐
│  ←  Scheduled payments                  │
├─────────────────────────────────────────┤
│                                          │
│                  ( ⓘ )                   │  info_outline, NOT error
│                                          │
│  Scheduled payments aren't available     │
│  for this account                         │
│                                          │
│   {uiState.message}                       │  ← ASPSP's own words, verbatim
│                                          │
│                                          │  NO retry — nothing to retry
├─────────────────────────────────────────┤
```

| Element | Token | Notes |
|---|---|---|
| Icon | `info_outline`, `onSurfaceVariant` | **not** `error` — a product limitation is not a fault |
| Title | `headlineMedium`, centred | states what the product does not offer |
| Body | `bodyMedium` on `onSurfaceVariant` | the ASPSP's own message, rendered verbatim rather than paraphrased |
| Retry | **absent** | there is nothing to retry |

> **Added 2026-07-30** (`/idea-heal`, closing
> `DISCOVERY:scheduled-payments:missing-unsupported-state`). All three capability-gated features —
> this one, `direct-debits`, `standing-orders` — record a `U000` refusal in their store fetcher
> (`BankingStores.kt:377` here) before rethrowing. Only the other two declared an `unsupported`
> state, because the 2026-07-28 reverse sync back-filled it into them from source and missed this
> feature. Without the state, a `U000` fell through to the retryable error path and a PSU on a
> credit card saw a Retry that could never succeed.
>
> **Idea-layer only as of this mockup.** Source `ScheduledPaymentsUiState` still ships four states
> and `classifyScheduledPaymentsError` still routes `U000` to `NetworkError`. The dead-end Retry
> persists on device until `/implement` lands the source half. This variant describes intended
> design, not shipped behaviour.

Reached when the account's HSBC product does not expose the resource — a credit card, per
`HsbcProductCapability`. Chips are normally hidden for unsupported products, so this surface is
mostly for deep links and back-navigation, where prediction was bypassed.

---

## State: error

```
┌─────────────────────────────────────────┐
│  ←  Scheduled payments                  │
├─────────────────────────────────────────┤
│                                          │
│                  ( ! )                   │  error_outline, error
│                                          │
│   Couldn't load scheduled payments        │
│                                          │
│   Check your connection and try again.    │
│                                          │
│  [          Try again          ]          │  filled
├─────────────────────────────────────────┤
```

Four error kinds, **all retryable**: `TokenExpired` (401) · `ConsentRevoked` (403) ·
`RateLimited` (429) · `NetworkError`.

`ConsentRevoked` still offers Retry rather than dead-ending — it will fail again until the PSU
re-authorises, but the screen routes them back through a failure they can see rather than a blank.

`RetryLoad` calls `stream.refresh()` on the `ScreenDataStream` the ViewModel owns — never
`repository.refresh()`; repositories here are stateless process-scoped gateways.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| account-detail | scheduled-payments | Explore option, carrying `accountId` |
| scheduled-payments | account-detail | back |

Entry is the account-detail Explore list, gated by `availableChipsFor`. `ScheduledPayments` is
hidden on a credit card — it and `Beneficiaries` are the mirror of `Statements`, which is
credit-card-**only**.
