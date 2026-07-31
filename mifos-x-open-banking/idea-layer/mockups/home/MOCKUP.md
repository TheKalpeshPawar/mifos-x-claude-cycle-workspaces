# Home — Visual Mockup

> Auto-generated from `screens/home/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-30
> Content: `screens/home/demo-data.yaml`

**Implemented** — `feature/home`, the **Home** bottom-nav tab and the NavHost start destination.
The app's only `navigation<Graph>` tab and the **only screen with a bottom sheet**.

> **This feature's `ui.yaml` was corrected during the 2026-07-30 `/idea-verify` → `/idea-heal`
> run.** Two components declared navigation source does not have. Both fixes are described in
> place below and marked **CORRECTED 2026-07-30**; the mockup documents the corrected — and
> source-verified — behaviour.

---

## Screen: Home

**Archetype** `dashboard` · **Initial state** `loading` · **States** `loading · content · empty · error`

**Deliberately thin.** Three surfaces: account switcher → hero balance → recent transactions. Three
others were removed on 2026-07-28 — the chip row, a quick-actions row (whose Pay was permanently
disabled and whose Statements was credit-card-only), and a spending-snapshot card linking to an
Insights screen that does not exist.

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **visible** — Home tab active (tab 1 of 4) | `ui.yaml#shell` |
| Top app bar | **visible** | `ui.yaml#shell` |
| Top app bar leading | none — tab root | — |
| FAB | **absent** | `ui.yaml#shell` |

Home's start route is also the NavHost start destination and the `popUpTo` target — which is why
`navigateToTab` must target a tab's `graphRoute`, never its inner `startDestinationRoute`.

---

## State: loading

```
┌─────────────────────────────────────────┐
│  Home                                   │
├─────────────────────────────────────────┤
│  ░░░░░░░░░░░░░░░░                        │  switcher shimmer
│  ┌──────────────────────────────────┐   │
│  │ ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ │   │  hero shimmer
│  └──────────────────────────────────┘   │
│  ░░░░░░░░  ░░░░░░░░  ░░░░░░░░           │  transaction shimmers
├─────────────────────────────────────────┤
│  ■ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

---

## State: content

```
┌─────────────────────────────────────────┐
│  Home                                   │
├─────────────────────────────────────────┤
│  Current account ·· 3349            ▾   │  AccountSwitcherRow
│                                          │
│  ┌──────────────────────────────────┐   │  HeroBalanceCard
│  │  Available                        │   │
│  │  £21,530.92                       │   │  displaySmall, MONO
│  │  Current £21,530.92               │   │
│  └──────────────────────────────────┘   │  TAP → opens selector sheet
│                                          │
│  RECENT                        View all →│  RecentTransactionsSection
│  ┌──────────────────────────────────┐   │
│  │ Tesco Stores            −£42.19  │   │  debit → error colour
│  │ 29 Jul 2026                      │   │
│  ├──────────────────────────────────┤   │
│  │ Salary — Mifos Ltd    +£3,120.00 │   │  credit → primary colour
│  │ 28 Jul 2026                      │   │
│  ├──────────────────────────────────┤   │
│  │ TfL Travel               −£8.40  │   │
│  │ 28 Jul 2026                      │   │
│  └──────────────────────────────────┘   │
├─────────────────────────────────────────┤
│  ■ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

```
home/
├── TopAppBar → "Home"
├── AccountSwitcherRow
├── HeroBalanceCard          → on_click: open_account_selector
├── RecentTransactionsSection
│   ├── view_all_transactions_link
│   └── transaction_row ×3   → on_click: navigate transaction-detail
└── BottomNav (Home active)
```

| Element | Token | Notes |
|---|---|---|
| Hero balance | `displaySmall`, mono, `semantic.money.neutral` | **unsigned** — a balance is a position |
| Transaction amount | mono; credit `semantic.money.credit`, debit `semantic.money.debit` | **signed** — a transaction has direction |
| Card | `surfaceContainer`, radius `medium`, elevation `level1` | |

**Home is the one screen where money is signed** — and only in the transaction rows. Credit is
trust-blue `primary`, debit is `error`. Never green/red: the two hues here stay distinguishable
under deuteranopia and protanopia, where green/red do not.

The hero balance stays **neutral and unsigned**. Signing a running balance off a per-transaction
`CreditDebitIndicator` renders a healthy account negative — a real trap this codebase documents.

### CORRECTED 2026-07-30 — the hero card opens the selector sheet

> `ui.yaml` declared `navigate_account_detail → target: account-detail` on the hero card. Source
> does not have that navigation. `HomeContent.kt:63` wires `onClick = onOpenAccountSelector`;
> `HomeScreen.kt:50` dispatches `HomeAction.OpenAccountSelector`; `onNavigateToAccountDetail`
> appears **nowhere** in `feature/home`. The file also contradicted itself — its own
> `account_selector_sheet` comment already recorded the correct wiring while the trigger still said
> navigate. Corrected to `open_account_selector` / `transform_state`.
>
> **Home does not navigate to account detail at all.** That route is reached from the Accounts tab.

**Interactions**

| Component | Action | Effect | Notes |
|---|---|---|---|
| `HeroBalanceCard` | `open_account_selector` | `transform_state` | opens `AccountSelectorSheet` — pure presentation-state flip |
| `view_all_transactions_link` | navigate | `navigate` | → `transactions` |
| `transaction_row` | navigate | `navigate` | → `transaction-detail(transactionId, accountId)` |

`homeGraph` exposes exactly **two** callbacks: `onNavigateToTransactions`,
`onNavigateToTransactionDetail`.

---

## Overlay: `AccountSelectorSheet` — the app's only bottom sheet

```
┌─────────────────────────────────────────┐
│                                          │
│  ╭──────────────────────────────────╮   │  extra_large top corners (28dp)
│  │              ▁▁▁                  │   │  drag handle
│  │  Choose an account                │   │
│  │                                    │   │
│  │  ✓ Current account ·· 3349        │   │  selected
│  │    £21,530.92                     │   │
│  │                                    │   │
│  │    BMM ACCOUNT ·· 3695            │   │
│  │    £482.10                        │   │
│  ╰──────────────────────────────────╯   │
└─────────────────────────────────────────┘
```

**Split in two on purpose**: a thin `ModalBottomSheet` wrapper plus a stateless
`AccountSelectorSheetContent` holding every interactive row. A sheet renders in its own window and
`onNodeWithTag` is unreliable against it, so tests drive the content composable directly, exactly
as they do the other `*ScreenContent`.

**Visibility lives on `HomeState` beside `uiState`, not inside `HomeData`** — it is presentation
state, not loaded data. `SelectAccount` persists the choice and closes the sheet in one action.

If a second screen ever needs a sheet, promote the wrapper to `core/ui` as a `Mifos*`.

---

## State: empty

```
┌─────────────────────────────────────────┐
│  Home                                   │
├─────────────────────────────────────────┤
│                  ( ☐ )                   │
│      No accounts connected                │
│   Your Open Banking consent has no        │
│   active accounts. Connect a bank from    │
│   Settings → Consents to get started.     │
├─────────────────────────────────────────┤
│  ■ Home │ ☐ Accounts │ ☐ Pay │ ☐ More  │
└─────────────────────────────────────────┘
```

### CORRECTED 2026-07-30 — no connect button

> `ui.yaml` declared a `connect_bank_button` → `navigate_login → target: login`. Source has no such
> navigation: `HomeEmpty.kt:37` states *"Points the PSU to Settings rather than offering its own
> connect button"*, the file contains **no `Button` and no `onClick`**, and `homeGraph` has no login
> lambda. The component was removed and `home.empty.body` retargeted to Settings → Consents;
> strings `home.empty.cta` + `.accessibility` were swept in the same edit (i18n re-verified:
> 545 declared / 517 referenced / 0 missing).

This matches the project-wide convention `beneficiaries` and `accounts` follow — the connect/renew
affordance lives **only** on the consent screens.

---

## State: error

Typed error with retry, refreshing the accounts + balances + recent-transactions composition.

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| home | `transactions` | "View all" |
| home | `transaction-detail` | recent-transaction row (`transactionId`, `accountId`) |

Both resolve to existing `screens/` directories. Home is a **tab** — no inbound nav reference.

---

## Removed in the 2026-07-28 reverse sync

| Removed | Consequence |
|---|---|
| Chip row | — |
| Quick-actions row | `HomeData.statementsAvailable` dropped; `HsbcProductCapability` has exactly one consumer again (account-detail) |
| Spending-snapshot card | `HomeData.spending` and `SpendingRowUi` dropped. `core/data`'s `SpendingCalculator` survives with its tests but has **no production caller** — kept because the `PfmDashboardRoute` placeholder implies a spending screen is still intended |
| `onNavigateToAccountDetail` | `homeGraph` down to three lambdas, then two |
