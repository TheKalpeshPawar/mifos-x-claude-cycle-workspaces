# Transaction detail — Feature Specification

> Generated from `screens/transaction-detail/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `5aa85cf5fd7a`
> Endpoints: 1 · DTOs: 1 · Components: 10 · Test scenarios: 11

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

Full detail for a single transaction: a large colour-coded amount header (credit `primary`,
debit `error`) with ISO 4217 currency label, merchant name, Booked/Pending badge, booking and
value dates, and a copyable reference.

| Attribute | Value |
|---|---|
| Feature ID | `transaction-detail` · Flow `transaction-review` · Cluster transactions |
| Priority | must (FR-005) · Status approved · quality 95 |
| Archetype | detail_screen · Route `TransactionDetailRoute(transactionId, accountId)` |
| Source module | `feature/transaction-detail` — **implemented** |

## 2. Resolve one record client-side

**No per-transaction endpoint exists.** This screen owns a single
`transactionDetailsStream(accountId)` — the memory-cached `transactionDetailsStore`, keyed by
*account* — and **filters that list by `transactionId` in the ViewModel**.

| Outcome | State |
|---|---|
| a row matches | `Content` |
| successful fetch, no match | **`Empty`** — not an error |
| fetch failed | `Error` |

That Empty/Error split matters: a transaction that has aged out of the returned window is not a
failure.

Uses a **new rich `core/model/.../banking/TransactionDetail.kt`** — the slim `TransactionItem`
carried too little — mapped by `toTransactionDetails(accountId)` from `TransactionsResponse`.

**Both route properties are arg keys.** The ViewModel reads `TRANSACTION_ID_ARG` **and**
`ACCOUNT_ID_ARG`; both must equal their route property names.

## 3. Screen inventory

`progress_indicator` · `back_button` · `amount_header` · `transaction_currency_meta` ·
`merchant_name` · `status_badge` (chip) · `header_separator` (divider) · `detail_card` ·
`error_state` · `transaction_empty_state`.

Merchant name falls back to `TransactionInformation` for non-card credits, which carry no
`MerchantDetails`.

## 4. State model — `TransactionDetailViewModel`

**Fields:** `transactionId` · `accountId` · `uiState` · **Default:** `Loading`
**UiState:** `Loading` · `Content` · `Error` · `Empty`
**Error kinds:** `TokenExpiredError` · `ConsentWithdrawnError` · `TransactionNotFoundError` ·
`NetworkError`
**Actions:** `RetryLoad` · **`CopyReference`**
**DI:** `SavedStateHandle` · `TransactionDetailRepository`

### Clipboard is a UI concern

`CopyReference` is emitted as an event the **Screen** performs against Compose's
`LocalClipboardManager` — the ViewModel never touches the platform. Same seam as
`send-money`'s `LaunchAuthorisation`: platform work that needs the composition belongs to the
composable, not the state machine.

## 5. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `transactions` | tap a row | `transaction-detail` (transactionId, accountId) |
| **`home`** | tap a recent-transaction row | same |
| back | top-app-bar leading | `transactions` |

Two entry points — the host wires `onNavigateToTransactionDetail(transactionId, accountId)` on
**both** `transactionsScreen` and `homeGraph`.

## 6. API dependencies

| ID | Method | Path | Permission | Response DTO | Cache |
|---|---|---|---|---|---|
| `transactions` | GET | `/accounts/{AccountId}/transactions` | ReadTransactionsDetail | `OBReadTransaction6` | cache-first |

Full contract in `API.md`.

## 7. Design tokens

`amount` header at display scale, mono; credit `primary`, debit `error`. `status_badge` uses
`secondaryContainer` for Pending — the same neutral-slate choice as `payment-status`'s
in-progress chip, for the same reason: pending is not success.
Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 8. Test mapping

TC-TXNDTL-001 full detail renders · 002 credit in `primary` · 003 loading · 004 not-found ·
005 back · 006 401 + Retry · 007 **403 shows Go Back, not Retry** · 008 **copy reference writes
to clipboard** · 009 Pending `secondaryContainer` badge · **010 Empty when transactionId absent
from the list** · 011 network error recoverable
→ `feature/transaction-detail/src/commonTest/.../TransactionDetailViewModelTest.kt` +
Robolectric. Ships Roborazzi goldens.

## 9. Notes

`data-flow.yaml` declares `cache_strategy: cache-first` — the client-side resolve depends on
the account's transaction list already being resident, so a cache miss costs a full fetch.
