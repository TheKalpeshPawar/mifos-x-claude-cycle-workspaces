# Transactions — API Contracts

> Generated from `screens/transactions/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Endpoints: 1 · DTOs: 1

Base path `/obie/open-banking/v4.0/aisp`. AIS read on the PSU bearer.

## Endpoint summary

| # | ID | Method | Path | Permission | Response DTO | Paging |
|---|---|---|---|---|---|---|
| 1 | `transactions` | GET | `/accounts/{AccountId}/transactions` | ReadTransactionsDetail | `OBReadTransaction6` | cursor via `Links.Next` |

## 1 · Transactions

```json
{
  "Data": { "Transaction": [
    { "AccountId": "1123456841", "TransactionId": "13756",
      "TransactionReference": "DOMESTIC.PAYMENTS -- 19870",
      "CreditDebitIndicator": "Debit", "Status": "BOOK",
      "TransactionMutability": "Immutable",
      "BookingDateTime": "2026-07-09T15:30:02+00:00",
      "ValueDateTime": "2026-07-09T15:30:02+00:00",
      "TransactionInformation": "DOMESTIC.PAYMENTS -- 19870",
      "Amount": { "Amount": "10.00", "Currency": "GBP" },
      "ChargeAmount": { "Amount": "0.00", "Currency": "GBP" },
      "BankTransactionCode": { "Code": "ICDT", "SubCode": "OTHR" },
      "Balance": { "CreditDebitIndicator": "Debit", "Type": "ITBD", "Amount": { "Amount": "21530.92", "Currency": "GBP" } },
      "MerchantDetails": { "MerchantName": "HSBC Sample Merchant", "MerchantCategoryCode": "4511" },
      "CreditorAccount": { … }, "DebtorAccount": { … }, "CardInstrument": { … } }
  ] },
  "Links": {
    "Self": "…/transactions",
    "Next": "…/transactions?page=1",
    "Last": "…/transactions?page=2" },
  "Meta": { "TotalPages": 3 }
}
```

`Status`: `BOOK` booked · `PDNG` pending. Pending rows get a badge and are visually distinct
(TC-TXN-010).

## Cursor pagination — bypasses Store5

`TransactionsRepository` exposes `suspend firstPage(accountId)` / `nextPage(nextLink)`
returning `NetworkResult<TransactionsPage, NetworkError>`, hitting `Aisp` **directly**. It is
the only cursor-paging pattern in the repo.

Paging follows `Links.Next` verbatim rather than constructing `?page=n` — the bank owns the
cursor format. `hasNextPage` is simply `Links.Next != null`.

A **date-range change resets the cursor** and re-requests from page 1 with ISO-8601 bounds
(`fromBookingDateTime` / `toBookingDateTime`). Credit/debit chips and free-text search do
**not** re-request — they filter the resident list in memory.

## The `Balance.CreditDebitIndicator` trap

HSBC sets the per-transaction `Balance.CreditDebitIndicator` to the **transaction's** direction,
not the balance's. Every debit on an account in credit arrives as `Debit`.

The sandbox returns `Balance {Debit, ITBD, 21530.92}` for an account whose `/balances` reports
`{Credit, ITBD, 21530.92}`. Signing on it rendered £21,530.92 as **−£21,530.92**.

**Running balances are displayed unsigned.** The row's own amount is signed off
`Transaction.CreditDebitIndicator`, which is correct.

## Error matrix

| HTTP | ErrorCode | Meaning | UI action |
|---|---|---|---|
| 401 | `UK.OBIE.Header.Invalid` | token expired | Error + **Retry** |
| 403 | `UK.OBIE.Resource.ConsentMismatch` | ReadTransactionsDetail absent or consent revoked | Error **without Retry** (TC-TXN-004) |
| 429 | `UK.OBIE.Rules.TooManyRequests` | rate limited | Retry with back-off |
| 500 | `UK.OBIE.Unexpected.ServerError` | HSBC-side failure | Error + Retry |
| — | — | no rows match the active filter | Empty state, not an error |

## Cache

`transactionsStore` is one of only **two Room-persisted stores** (with `accountsStore`). Its
fetcher must call `validator.markFresh()` inside the Success branch or the TTL never starts,
and its SoT reader must emit `null` for an empty table
(`rows.takeIf { it.isNotEmpty() }?.map { … }`) so cold start is Loading, not a premature Empty.

That store backs `feature/home`'s recent-transactions preview via `transactionsStream`. **This
screen does not use it** — it pages directly.

## Source binding

`core/network/api/Aisp.kt` `getTransactions` / `getTransactionsPage` ·
`TransactionsRepositoryImpl.kt:47-51` (the direct-`Aisp` paging path) ·
`BankingStores.transactionsStore` (Room-persisted; consumed by home, not here).
