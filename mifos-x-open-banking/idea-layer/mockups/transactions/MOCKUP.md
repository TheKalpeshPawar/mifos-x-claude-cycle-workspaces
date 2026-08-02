# Transactions — Visual Mockup

> Auto-generated from `screens/transactions/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-31
> Content: `screens/transactions/demo-data.yaml`

**Implemented** — `feature/transactions`, account-scoped pushed screen.

> **Do not copy this feature as a template for a stream screen.** It is a **suspend cursor-pager**,
> not a `ScreenDataStream` feature — the one structural exception among the account-scoped lists.

---

## Screen: Transactions

**Archetype** `index_list` · **Initial state** `loading` · **States** `loading · content · empty · error`

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
│  ←  Transactions                        │
├─────────────────────────────────────────┤
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░       │  shimmer rows
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░       │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░       │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

---

## State: content

```
┌─────────────────────────────────────────┐
│  ←  Transactions                        │
├─────────────────────────────────────────┤
│  JULY 2026                               │  date group header
│  ┌──────────────────────────────────┐   │
│  │ Tesco Stores            −£42.19  │   │  debit → error
│  │ 29 Jul · ( Groceries )           │   │  tx_category_tag
│  ├──────────────────────────────────┤   │
│  │ Salary — Mifos Ltd    +£3,120.00 │   │  credit → primary
│  │ 28 Jul · ( Income )              │   │
│  ├──────────────────────────────────┤   │
│  │ TfL Travel               −£8.40  │   │
│  │ 28 Jul · ( Transport )           │   │
│  └──────────────────────────────────┘   │
│                                          │
│  JUNE 2026                               │
│  ┌──────────────────────────────────┐   │
│  │ Northern Gas            −£96.40  │   │
│  │ 30 Jun · ( Utilities )           │   │
│  └──────────────────────────────────┘   │
│                  ( ◌ )                   │  page-load footer
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

```
transactions/
├── TopAppBar → back + "Transactions"
├── transactions_list: list (vertical, paged)
│   ├── date_group_header: section_header
│   └── transaction_row: list_item
│       ├── merchant   (bodyLarge)
│       ├── date + tx_category_tag (bodySmall + tag)
│       └── amount     (bodyLarge, mono, signed)
└── page_loading_footer: progress_indicator [while fetching next page]
└── BottomNav
```

| Element | Token | Notes |
|---|---|---|
| Group header | `labelMedium` on `onSurfaceVariant`, uppercase | month grouping |
| Merchant | `bodyLarge` on `onSurface` | |
| Amount | mono; credit `semantic.money.credit`, debit `semantic.money.debit` | **signed** |
| Category tag | tonal, `secondaryContainer` | |
| Row min height | `accessibility.min_touch_target_dp` | 48dp |

**Amounts are signed and coloured here** — credit trust-blue `primary`, debit `error`, each with an
explicit `+`/`−`. Never green/red: these two hues stay distinguishable under deuteranopia and
protanopia, and the sign means colour is never the sole signal.

### The pager — a suspend cursor, not a stream

The list pages through a **suspend cursor**, appending as the PSU scrolls. Consequences that shape
the design:

- **No pull-to-refresh.** There is no stream to refresh; a refresh gesture would restart the cursor
  and lose scroll position.
- **The next-page indicator is a list footer**, not a screen-level spinner — existing rows stay
  visible and interactive while page N+1 loads.
- **A page-load failure does not replace the screen.** It surfaces at the footer with a retry
  affordance; already-loaded transactions remain.

> **Known gap:** `tx_category_tag` has **no `accessibility_label`**. One of exactly two such
> components in the project (the other is `settings/app_version_row`). A screen-reader user hears
> the merchant, date and amount but not the category. Recorded, not fixed here.

**Interactions**

| Component | Action | Effect | Notes |
|---|---|---|---|
| `transaction_row` | navigate | `navigate` | → `transaction-detail(transactionId, accountId)` |

---

## State: empty

```
┌─────────────────────────────────────────┐
│  ←  Transactions                        │
├─────────────────────────────────────────┤
│                  ( ☐ )                   │  receipt_long
│         No transactions                   │
│   This account has no activity in the     │
│   available period.                       │
├─────────────────────────────────────────┤
```

The first page returned nothing. No CTA.

---

## State: error

```
┌─────────────────────────────────────────┐
│  ←  Transactions                        │
├─────────────────────────────────────────┤
│                  ( ! )                   │  error_outline, error
│      Couldn't load transactions            │
│  [          Try again          ]          │
├─────────────────────────────────────────┤
```

**First-page failures only.** A failure on page N+1 stays at the footer — see above.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| account-detail | transactions | Explore chip, carrying `accountId` |
| home | transactions | "View all" |
| transactions | `transaction-detail` | row tap |

**Reached from two places, never from a tab.** The Pay tab replaced a Transactions tab that was
itself only a placeholder — the real list was and still is reached from account detail and from
Home's "View all".

---

## Removed in the 2026-07-28 reverse sync

| Removed | Why |
|---|---|
| `category` route param | not a route argument in source |
| `pfm` entry point | the PFM screens were never built |
