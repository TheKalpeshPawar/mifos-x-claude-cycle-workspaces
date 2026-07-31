# Transaction detail — API Contracts

> Generated from `screens/transaction-detail/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Endpoints: 1 · DTOs: 1

Base path `/obie/open-banking/v4.0/aisp`.

## Endpoint summary

| # | ID | Method | Path | Permission | Response DTO | Cache |
|---|---|---|---|---|---|---|
| 1 | `transactions` | GET | `/accounts/{AccountId}/transactions` | ReadTransactionsDetail | `OBReadTransaction6` | cache-first |

**There is no per-transaction endpoint.** OBIE AIS v4.0 exposes transactions only as an
account-scoped collection, so this screen fetches the account's list and resolves one record
**client-side** by `transactionId`.

## Client-side resolution

```kotlin
transactionDetailsStream(accountId)          // memory store, keyed by ACCOUNT
    .mapContent { list -> list.firstOrNull { it.transactionId == transactionId } }
// match  -> Content
// no match on a successful fetch -> Empty   (NOT an error)
// fetch failed -> Error
```

The Empty case is load-bearing: a transaction that has aged out of the returned window is not a
failure the customer can act on, and rendering it as an error would invite a pointless Retry.

## Fields consumed

| Rendered | Source | Note |
|---|---|---|
| amount header | `Amount { Amount, Currency }` | signed off `Transaction.CreditDebitIndicator` |
| merchant name | `MerchantDetails.MerchantName` | **falls back** to `TransactionInformation` for non-card credits, which carry no `MerchantDetails` |
| status badge | `Status` | `BOOK` Booked · `PDNG` Pending |
| booking / value dates | `BookingDateTime`, `ValueDateTime` | |
| reference | `TransactionInformation` | the copy-to-clipboard payload |
| running balance | `Balance.Amount` | **unsigned** — see the trap below |
| card scheme | `CardInstrument` | present only on card transactions |

`TransactionsResponse` is mapped by `toTransactionDetails(accountId)` into a rich
`core/model/.../banking/TransactionDetail.kt`. The slim `TransactionItem` used by the list
carried too little for this screen.

## The `balanceIsCredit` trap

HSBC sets the per-transaction `Balance.CreditDebitIndicator` to the **transaction's** direction,
not the balance's, so every debit on an account in credit arrives as `Debit`.

Sandbox: `Balance {Debit, ITBD, 21530.92}` on an account whose `/balances` reports
`{Credit, ITBD, 21530.92}`. Signing on it renders £21,530.92 as −£21,530.92.

**`TransactionDetail.balanceIsCredit` must not sign the balance.** The running balance is
displayed unsigned.

## Error matrix

| HTTP | Kind | Retry? | UI action |
|---|---|:--:|---|
| 401 | `TokenExpiredError` | ✅ | Retry |
| 403 | `ConsentWithdrawnError` | ✗ | **Go Back** CTA, not Retry (TC-TXNDTL-007) |
| — | `TransactionNotFoundError` | ✗ | error state |
| — | `NetworkError` | ✅ | recoverable, Retry |
| — | *no match in a successful fetch* | — | **Empty**, not an error |

## Cache

`transactionDetailsStore` — `createMemoryStore(fetcher)`, keyed by **AccountId**, not
TransactionId. Consent-scoped read-only data, never Room-persisted.

`cache_strategy: cache-first`: the client-side resolve depends on the account's list already
being resident, so a cache miss costs a full account fetch to render one row.

## Source binding

`core/network/api/Aisp.kt` `getTransactions` · `BankingStores.transactionDetailsStore` (memory,
account-keyed) · `TransactionDetailRepository` (stateless) ·
`core/model/.../banking/TransactionDetail.kt` + `toTransactionDetails(accountId)`.
