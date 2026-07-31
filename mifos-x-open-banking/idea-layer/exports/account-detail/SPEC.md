# Account detail — Feature Specification

> Generated from `screens/account-detail/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `63022c4bdb68`
> Endpoints: 2 · DTOs: 2 · Components: 10 · Test scenarios: 14

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

Single account detail — metadata, all balance types from `OBCashBalance3`, an Open Banking
trust badge, and the **Explore options** entry points to nine sibling screens.

| Attribute | Value |
|---|---|
| Feature ID | `account-detail` |
| Cluster | account |
| Priority | must (FR-003, FR-004) |
| Status | approved · quality 95 |
| Archetype | detail_screen |
| Source module | `feature/account-detail` — **implemented** |
| Route | `AccountDetailRoute(accountId: String)` |

**Two merged streams.** This is the reference exemplar for the two-stream shape: account
metadata and balances merged in the ViewModel via `combineScreenStates`, with `DETAIL_CACHE_KEY`
and `BALANCES_CACHE_KEY` named separately rather than colliding on `CACHE_KEY`.

## 2. Screen inventory

Content order: `account_header_card` → *description card* → Balances section → Explore options.

| Component | Type | Bound states |
|---|---|---|
| `loading_spinner` | progress_indicator | loading |
| `back_button` | icon_button | all |
| `account_header_card` · `open_banking_badge` | card ×2 | content |
| `balances_header` + `balances_list` | section_header, list | content |
| `balances_empty_state` | empty_state | content (no balances) |
| `actions_header` + `action_chips` | section_header, chip_row | content |
| `error_state` | empty_state | error |

**No `Empty.kt`, no `Unsupported.kt`.** Empty reuses `AccountDetailContent` with
`balances = emptyList()`; there is no Unsupported state at all.

### The description card

Renders OBIE `Description` verbatim and is **omitted when blank** rather than drawn empty,
guarded with `isNotBlank()` because the field is free text and a whitespace-only value would
leave a heading above an empty line. It earns its place because `AccountTypeCode` reports
`CACC` for a Global Money wallet exactly as for an ordinary current account — the description
is frequently the only thing that says what the product is.

### Explore options — a column, not chips

`ExploreOptionsColumn` (renamed from `ExploreChipRow`): full-width vertical list, each option a
`Row` with a 24dp leading icon tinted `primary`, a `titleMedium` label and a trailing chevron,
with a `HorizontalDivider` between adjacent options and none after the last. No `AssistChip`,
no outline. The `AccountDetailChip` enum and its test tags were kept, so the suites still
address them.

## 3. State model — `AccountDetailViewModel`

**State fields:** `accountId: String` (nav arg) · `uiState: AccountDetailUiState`
**State defaults:** `uiState = Loading`

`AccountDetailUiState`: `Loading` · `Content` · `Empty` · `Error`
`AccountDetailErrorKind` keys on **`recoverable`** (direct-debits' keys on `isRetriable` —
copy the shape, not the enum).

**Actions:** `RetryLoad`
**Nav callbacks:** `onNavigateToChip(chip, accountId)` · `onBack → popBackStack()`
**DI:** `SavedStateHandle` · `AccountDetailRepository` · `AccountCapabilityRegistry`

The capability registry is combined as a plain `Flow<Set<AccountEndpoint>>`, **not** a
`ScreenState`.

### Nav-arg pinning

`ACCOUNT_ID_ARG` must equal the route's property name — type-safe nav serialises `accountId`
into `SavedStateHandle` under exactly that name. Rename the property without the constant and
the lookup returns `null`, `.orEmpty()` yields a blank id, and the screen fails **silently**.

This feature carries the only serial-descriptor assertion in the repo (`AccountDetailViewModelTest.kt:244-247`):

```kotlin
val descriptor = AccountDetailRoute.serializer().descriptor
assertEquals(1, descriptor.elementsCount)
assertEquals(AccountDetailViewModel.ACCOUNT_ID_ARG, descriptor.getElementName(0))
```

Siblings only assert `assertEquals("accountId", …ACCOUNT_ID_ARG)`, which never reads the route
and still passes after a rename. **Write the descriptor form.**

## 4. Navigation — the app's main hub

| Trigger | Target |
|---|---|
| back | `accounts` |
| `AccountDetailChip.Transactions` | `transactions` |
| `.Statements` | `statements` |
| `.StandingOrders` | `standing-orders` |
| `.DirectDebits` | `direct-debits` |
| `.ScheduledPayments` | `scheduled-payments` |
| `.Beneficiaries` | `beneficiaries` |
| `.Product` | `product` |
| `.Party` | `account-holder` |
| `.AtmLocator` | `_placeholder:atm-locator` — arg-less `PlaceholderScreen` |

Nine chips, fixed declaration order. Suites assert all nine in order, so **adding a member
breaks them** — direct-debits, standing-orders, scheduled-payments and product all shipped by
repointing an existing `navigateFromChip` branch off a dead placeholder instead.

## 5. Product-capability gating

Five chips gate: **StandingOrders · DirectDebits · Statements · ScheduledPayments · Beneficiaries**.
Statements is **credit-card-only**; ScheduledPayments and Beneficiaries are its mirror — every
product *except* credit card.

Three layers: **predict** (`HsbcProductCapability.supports`), **correct** (the store *fetcher*
calls `recordIfUnsupported` on a `U000` before rethrowing — never a ViewModel, because the
fetcher is the one point every call passes including a deep link), **render**
(`availableChipsFor`, `internal` to this feature — a new gated feature re-implements it).

Gating **fails open**: `HsbcProductType.Unknown` and unlisted endpoints stay permissive, and
`productTypeOrUnknown()` reports `Unknown` for every non-`Content` state so the row doesn't
flicker while loading.

**This Explore list is the only gated surface in the app.**

## 6. API dependencies

| ID | Method | Path | Permission | Response DTO |
|---|---|---|---|---|
| `account-detail` | GET | `/accounts/{AccountId}` | ReadAccountsDetail | `OBReadAccount6` |
| `balances` | GET | `/accounts/{AccountId}/balances` | ReadBalances | `OBReadBalance1` |

Full contracts in `API.md`.

## 7. Design tokens

`design-tokens.yaml` 2.1.0 — `card` on `surfaceContainer`, `section_header`
(`titleSmall`/`onSurfaceVariant`), `amount` (mono; balances **unsigned**, `neutral`).
Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 8. Test mapping

TC-ACCTDTL-001 … TC-ACCTDTL-014 → `feature/account-detail/src/commonTest/.../AccountDetailViewModelTest.kt`
and `androidUnitTest/.../AccountDetailScreenRobolectricTest.kt`.

> **Gap:** all 14 scenarios in `tests.yaml` carry an **empty `description`**. The ids exist and
> the file parses, but the assertions are undocumented — the only feature in the corpus in that
> state. Recorded rather than invented; filling them is `/idea-test-generate` work.

## 9. Stale-artifact fixes applied 2026-07-30

| Was | Now |
|---|---|
| `chip_party` → `target: party` (screen renamed 2026-07-28) | `target: account-holder` |
| `chip_atm_locator` → `target: atm-locator` + `params: {accountId}` | `_placeholder:atm-locator`, `params: {}` — `AtmLocatorRoute` is an arg-less data object |
| `dangling_nav_target:` block | `placeholder_bound_chips:` — no longer dangling |

`docs.yaml` declares no `flow_ref` despite `flows/account-browsing.yaml` existing.
