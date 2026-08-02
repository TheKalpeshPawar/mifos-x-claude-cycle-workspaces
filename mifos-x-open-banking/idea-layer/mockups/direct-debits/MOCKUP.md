# Direct Debits — Visual Mockup

> Auto-generated from `screens/direct-debits/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-31
> Content: `screens/direct-debits/demo-data.yaml`

**Implemented** — `feature/direct-debits`, account-scoped pushed screen. The project's canonical
single-stream feature template: copy its anatomy when scaffolding a new account-scoped list.

---

## Screen: Direct Debits

**Archetype** `index_list` · **Initial state** `loading`
**States** `loading · content · empty · unsupported · error`

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **visible** | `ui.yaml#shell.bottom_navigation_visible: true` |
| Top app bar | **visible**, title `{strings.direct_debits.title}` | `ui.yaml#shell.top_app_bar_visible: true` |
| Top app bar leading | **back** — account-scoped pushed screen | `ui.yaml#shell.top_app_bar_leading: back` |
| FAB | **absent** | `ui.yaml#shell.fab_visible: false` |

---

## State: loading

```
┌─────────────────────────────────────────┐
│  ←  Direct Debits                       │
├─────────────────────────────────────────┤
│                                          │
│                  ( ◌ )                   │  progress_indicator, circular
│                                          │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

Centred spinner rather than a skeleton — mandate count is unknowable up front.

---

## State: content

```
┌─────────────────────────────────────────┐
│  ←  Direct Debits                       │
├─────────────────────────────────────────┤
│  3 Active · 1 Inactive                   │  summary, computed in the VM
│                                          │
│  ┌──────────────────────────────────┐   │
│  │ British Gas            ( Active ) │   │  name + status badge
│  │ Last paid £84.20 · 12 Jul 2026   │   │  mono amount, unsigned
│  │ Ref 4471029922                   │   │  MandateIdentification
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │
│  │ Thames Water           ( Active ) │   │
│  │ Last paid £41.65 · 3 Jul 2026    │   │
│  │ Ref 8830041177                   │   │
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │
│  │ Vitality Health      ( Inactive ) │   │  outline badge
│  │ Last paid £29.99 · 2 May 2026    │   │
│  │ Ref 2210559043                   │   │
│  └──────────────────────────────────┘   │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

```
direct-debits/
├── TopAppBar → back + "Direct Debits"
├── summary_row: text (activeCount / inactiveCount)
├── direct_debits_list: list (vertical, items ← mandates)
│   └── mandate_card: card (radius.md, elevation 1)
│       ├── name          (titleMedium)
│       ├── status_badge  (primary tonal | outline)
│       ├── previousPayment (bodySmall — amount mono + date)
│       └── mandateIdentification (bodySmall, on-surface-variant)
└── BottomNav
```

| Element | Token | Notes |
|---|---|---|
| Card | `surfaceContainer`, radius `medium`, elevation `level1` | |
| Amount | mono, `semantic.money.neutral` | **unsigned** — a past payment, not a movement |
| Active badge | tonal, `secondaryContainer` | |
| Inactive badge | outlined, `outline` border | |
| Summary | `bodyMedium` on `onSurfaceVariant` | e.g. "3 Active · 1 Inactive" |

**The list sorts Active-first, then Inactive**, and the summary counts are computed in the
ViewModel — the UI receives finished strings. Status drives badge variant only; an inactive mandate
is not dimmed or struck through, because it remains a real historical record.

**Interactions** — none. Cards are not tappable; there is no mandate detail screen, and this app
cannot cancel a mandate (read-only under `ReadDirectDebits`).

---

## State: empty

```
┌─────────────────────────────────────────┐
│  ←  Direct Debits                       │
├─────────────────────────────────────────┤
│                  ( ☐ )                   │  receipt_long
│         No direct debits                  │
│   This account has no direct debit        │
│   mandates set up.                        │
├─────────────────────────────────────────┤
```

The fetch succeeded and the bank reported none — a real answer. No CTA: this app cannot create a
mandate.

---

## State: unsupported

```
┌─────────────────────────────────────────┐
│  ←  Direct Debits                       │
├─────────────────────────────────────────┤
│                  ( ⓘ )                   │  info_outline, NOT error
│  Direct debits aren't available for       │
│  this account                             │
│   {uiState.message}                       │  ← ASPSP's own words, verbatim
│                                          │  NO retry
├─────────────────────────────────────────┤
```

| Element | Token | Notes |
|---|---|---|
| Icon | `info_outline`, `onSurfaceVariant` | **not** `error` — a product limitation is not a fault |
| Body | `bodyMedium` on `onSurfaceVariant` | the ASPSP's explanation, verbatim rather than paraphrased |
| Retry | **absent** | the servicer refused the resource; there is nothing to retry |

Reached on a `U000` refusal, which the store fetcher records against
`AccountEndpoint.DirectDebits` (`BankingStores.kt:234`) before rethrowing. The ViewModel checks
`error.isUnsupportedForProduct()` **before** classification, so a `U000` never routes to a
retryable error kind (`DirectDebitsViewModel.kt:64`).

This is the state `scheduled-payments` was missing until 2026-07-30 — this feature and
`standing-orders` are where the pattern is correct, and the source of the fix.

---

## State: error

```
┌─────────────────────────────────────────┐
│  ←  Direct Debits                       │
├─────────────────────────────────────────┤
│                  ( ! )                   │  error_outline, error
│    Couldn't load direct debits            │
│   Check your connection and try again.    │
│  [          Try again          ]          │  CONDITIONAL — see below
├─────────────────────────────────────────┤
```

### Retry is suppressed for one error kind

| Error kind | Trigger | Retry | Why |
|---|---|:---:|---|
| `TokenExpired` | 401 | **shown** | transient; a refresh fixes it |
| `RateLimited` | 429 | **shown** | transient; back off and retry |
| `NetworkError` | IOException | **shown** | transient |
| `ServerError` | uncategorised | **shown** | more often transient than permanent |
| `ConsentRevoked` | 403 | **hidden** | the consent is gone — retrying fails identically until the PSU re-authorises |

`ConsentRevoked` suppressing retry is the deliberate difference from `scheduled-payments`, which
offers retry on all four kinds. Both are defensible; this one dead-ends rather than inviting a
guaranteed failure.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| account-detail | direct-debits | Explore option, carrying `accountId` |
| direct-debits | account-detail | back |

Gated by `availableChipsFor` — hidden on products that cannot serve the endpoint, corrected at
runtime by `recordIfUnsupported`.
