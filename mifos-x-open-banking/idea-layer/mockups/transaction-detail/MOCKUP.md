# Transaction detail — Visual Mockup

> Auto-generated from `screens/transaction-detail/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-30
> Content: `screens/transaction-detail/demo-data.yaml`

**Implemented** — `feature/transaction-detail`,
`TransactionDetailRoute(transactionId, accountId)`.

---

## Screen: Transaction detail

**Archetype** `detail_screen` · **Initial state** `loading` · **States** `loading · content · error · empty`

**Resolves one record client-side.** There is no per-transaction endpoint. The ViewModel owns a
single `transactionDetailsStream(accountId)` — the memory-cached `transactionDetailsStore`, keyed
by **account** — and filters that list by `transactionId`:

| Outcome | State |
|---|---|
| a row matches | `content` |
| fetch succeeded, **no** match | `empty` |
| fetch failed | `error` |

That distinction is why `empty` exists on a detail screen at all: "this account's transactions
loaded but none has that id" is a real answer, not a failure.

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **visible** | `ui.yaml#shell` |
| Top app bar | **visible** | `ui.yaml#shell` |
| Top app bar leading | **back** | `ui.yaml#shell` |
| FAB | **absent** | `ui.yaml#shell` |

---

## State: loading

```
┌─────────────────────────────────────────┐
│  ←  Transaction                         │
├─────────────────────────────────────────┤
│                  ( ◌ )                   │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

---

## State: content

```
┌─────────────────────────────────────────┐
│  ←  Transaction                         │
├─────────────────────────────────────────┤
│  ┌──────────────────────────────────┐   │  amount_card
│  │           −£42.19                 │   │  displaySmall, mono, SIGNED
│  │         Tesco Stores              │   │
│  │      29 Jul 2026, 14:02           │   │
│  │        ( Groceries )              │   │
│  └──────────────────────────────────┘   │
│                                          │
│  DETAILS                                 │
│  ┌──────────────────────────────────┐   │
│  │ Status            Booked         │   │
│  │ Type              Card payment   │   │
│  │ Balance after     £21,530.92     │   │  UNSIGNED, neutral
│  │ Reference         TESCO 4471 ⧉   │   │  copy affordance
│  └──────────────────────────────────┘   │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

```
transaction-detail/
├── TopAppBar → back + "Transaction"
├── amount_card: card
│   ├── amount    (displaySmall, mono, signed + coloured)
│   ├── merchant  (titleMedium)
│   ├── timestamp (bodyMedium, on-surface-variant)
│   └── category tag
├── details_header: section_header
└── details_list: list
    ├── status_row · type_row
    ├── balance_after_row      (UNSIGNED, neutral)
    └── reference_row + copy_button
└── BottomNav
```

| Element | Token | Notes |
|---|---|---|
| Amount | `displaySmall`, mono; credit `primary`, debit `error` | **signed** |
| Balance after | `bodyLarge`, mono, `semantic.money.neutral` | **unsigned** |
| Card | `surfaceContainer`, radius `medium`, elevation `level1` | |
| Copy icon | `primary`, 24dp in a 48dp target | |

### The `balanceIsCredit` trap — the reason "Balance after" is unsigned

HSBC sets the per-transaction `Balance.CreditDebitIndicator` to the **transaction's** direction,
not the balance's. Every debit on an account in credit therefore arrives marked `Debit`. The
sandbox returns `Balance {Debit, ITBD, 21530.92}` for an account whose `/balances` reports
`{Credit, ITBD, 21530.92}`.

**Signing the running balance off that indicator rendered £21,530.92 as −£21,530.92.** So the
running balance is displayed **unsigned and neutral**, while the transaction amount above it is
signed and coloured. Two money treatments on one screen, and the difference is a shipped bug fix —
do not unify them.

`TransactionDetail` (`core/model`) is a **richer model than `TransactionItem`**; the slim list row
model was insufficient for this screen.

**Interactions**

| Component | Action | Effect | Notes |
|---|---|---|---|
| `copy_button` | `CopyReference` | `emit_event` | emits `CopyToClipboard`; the **Screen** performs it against `LocalClipboardManager` |

**Copy is a UI concern, not a ViewModel one.** The ViewModel emits an event and the composable
touches the clipboard — the same seam `statements` uses for file delivery and `send-money` uses for
the browser launch. Non-`Nothing` event type.

---

## State: empty

```
┌─────────────────────────────────────────┐
│  ←  Transaction                         │
├─────────────────────────────────────────┤
│                  ( ☐ )                   │  search_off
│      Transaction not found                │
│   This transaction isn't in the account's │
│   available history.                      │
├─────────────────────────────────────────┤
```

The account's transactions loaded, but none matched. Most likely a stale deep link or a
transaction that has aged out of the available window. No retry — refetching the same list yields
the same absence.

---

## State: error

```
┌─────────────────────────────────────────┐
│  ←  Transaction                         │
├─────────────────────────────────────────┤
│                  ( ! )                   │  error_outline, error
│      Couldn't load this transaction        │
│  [          Try again          ]          │
├─────────────────────────────────────────┤
```

The account's transaction fetch failed. Retry calls `stream.refresh()`.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| transactions | transaction-detail | row tap (`transactionId`, `accountId`) |
| home | transaction-detail | recent-transaction row tap |
| statement-detail | transaction-detail | statement transaction row tap |
| transaction-detail | *(caller)* | back |

**Three inbound callers** — the most of any screen in the app. All pass both ids, because the
screen needs `accountId` to fetch the list it filters.
