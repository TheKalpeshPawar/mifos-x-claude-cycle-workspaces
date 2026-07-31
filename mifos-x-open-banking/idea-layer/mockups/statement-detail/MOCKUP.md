# Statement detail — Visual Mockup

> Auto-generated from `screens/statement-detail/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-31
> Content: `screens/statement-detail/demo-data.yaml`

**Implemented** — `feature/statement-detail`, `StatementDetailRoute(accountId, statementId)`. The
**second exemplar of the two-stream shape** after `account-detail`.

---

## Screen: Statement detail

**Archetype** `detail_screen` · **Initial state** `loading` · **States** `loading · content · empty · error`

**Two streams, merged in the ViewModel.** Statement metadata (`statementDetailStore`) and the
statement's transactions (`statementTransactionsStore`) are combined via `combineScreenStates`.
Both stores are keyed by the **composite** `"$accountId|$statementId"` — a pattern unique to this
feature and its metadata sibling.

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
│  ←  Statement                           │
├─────────────────────────────────────────┤
│                  ( ◌ )                   │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

One spinner covers **both** streams — `combineScreenStates` holds Loading until each resolves.

---

## State: content

```
┌─────────────────────────────────────────┐
│  ←  Statement                           │
├─────────────────────────────────────────┤
│  ┌──────────────────────────────────┐   │  summary card
│  │ 1 Jun – 30 Jun 2026              │   │  titleLarge
│  │ Statement 0042                    │   │  mono
│  │                                    │   │
│  │ Opening balance      £1,042.18    │   │  mono, neutral
│  │ Closing balance      £1,204.55    │   │
│  │ Payments in          £3,120.00    │   │
│  │ Payments out         £2,957.63    │   │
│  └──────────────────────────────────┘   │
│                                          │
│  [        Download PDF        ]          │  tonal
│                                          │
│  TRANSACTIONS                            │
│  ┌──────────────────────────────────┐   │
│  │ Tesco Stores            −£42.19  │   │  TransactionItem — reused
│  │ 29 Jun 2026                      │   │
│  ├──────────────────────────────────┤   │
│  │ Salary — Mifos Ltd    +£3,120.00 │   │
│  │ 28 Jun 2026                      │   │
│  └──────────────────────────────────┘   │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

```
statement-detail/
├── TopAppBar → back + "Statement"
├── summary_card: card (period, id, four balance rows)
├── download_button: button (tonal)
├── transactions_header: section_header
└── statement_transactions_list: list
    └── transaction_row → transaction-detail
└── BottomNav
```

| Element | Token | Notes |
|---|---|---|
| Summary card | `surfaceContainer`, radius `medium`, elevation `level1` | |
| Statement id | `bodyMedium`, mono, `onSurfaceVariant` | |
| Balance figures | mono, `semantic.money.neutral` | **unsigned** — positions, not movements |
| Transaction amount | mono; credit `primary`, debit `error` | **signed** — movements |
| Download | tonal, `secondaryContainer` | |

**The two money treatments differ within one screen, and that is deliberate.** Summary balances are
neutral and unsigned; transaction rows are signed and coloured. A closing balance is a position; a
transaction is a movement. This is the same split `home` makes between its hero card and its
recent-transaction rows.

**`TransactionItem` is reused verbatim** from `transactions` — same row model, same formatting,
same navigation target. Do not fork a statement-specific variant.

**Interactions**

| Component | Action | Effect | Notes |
|---|---|---|---|
| `download_button` | `DownloadStatement` | `call_api` | reuses `StatementFileRepository` + `StatementFileHandler` from `statements` |
| `transaction_row` | navigate | `navigate` | → `transaction-detail(transactionId, accountId)` |

### The download seam is borrowed, not re-declared

This feature injects the **same** `StatementFileRepository` and the **same** `StatementFileHandler`
interface that `feature/statements` declared, so its event type is non-`Nothing` too (with a
`DownloadState`). Critically it does **not** own a second platform binding — the single
`expect`/`actual` in `cmp-navigation` serves both features.

That is the payoff of the seam being declared as an interface the feature *uses* rather than
*implements*: a second consumer costs nothing.

---

## State: empty

```
┌─────────────────────────────────────────┐
│  ←  Statement                           │
├─────────────────────────────────────────┤
│                  ( ☐ )                   │
│      No transactions in this period        │
│   This statement covers a period with no  │
│   activity.                                │
├─────────────────────────────────────────┤
```

**Empty applies to the transaction list, not the statement.** The summary card and Download PDF
button **remain visible** — a statement with no activity is still a real statement with real
balances and a downloadable PDF. Replacing the whole screen would hide both.

---

## State: error

```
┌─────────────────────────────────────────┐
│  ←  Statement                           │
├─────────────────────────────────────────┤
│                  ( ! )                   │  error_outline, error
│      Couldn't load this statement          │
│  [          Try again          ]          │
├─────────────────────────────────────────┤
```

Retry refreshes **both** streams. A failed **download** does not land here — it surfaces as a
snackbar over intact content, exactly as in `statements`.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| statements | statement-detail | statement card tap (`accountId`, `statementId`) |
| statement-detail | `transaction-detail` | transaction row tap |
| statement-detail | statements | back |

Both targets resolve to existing `screens/` directories.

---

## Composite keying — worth knowing before copying this screen

Both stores key on `"$accountId|$statementId"`. Only this feature and its metadata store do that;
every other account-scoped store keys on `accountId` alone. If you copy this screen as a template,
copy the composite key deliberately — a single-id key here would collide across statements of the
same account and serve the wrong period's transactions from cache.
