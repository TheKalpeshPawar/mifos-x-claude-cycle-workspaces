# Direct debits — API Contracts

> Generated from `screens/direct-debits/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Endpoints: 1 · DTOs: 1

Base path `/obie/open-banking/v4.0/aisp`. AIS read on the PSU bearer.

## Endpoint summary

| # | ID | Method | Path | Permission | Response DTO | Cache |
|---|---|---|---|---|---|---|
| 1 | `direct-debits-list` | GET | `/accounts/{AccountId}/direct-debits` | ReadDirectDebits | `OBReadDirectDebit2` | memory |

## 1 · Direct debits list

```json
{
  "Data": { "DirectDebit": [
    { "AccountId": "123456791", "DirectDebitId": "6",
      "MandateRelatedInformation": {
        "MandateIdentification": "eb4268b3-3ca8-48ca-8c63-39b4e341c39",
        "Frequency": { "Type": "ADHO" } },
      "DirectDebitStatusCode": "ACTV",
      "Name": "Towbar Club 3 - We Love Towbars",
      "PreviousPaymentDateTime": "2019-06-19T10:55:46+00:00",
      "PreviousPaymentAmount": { "Amount": "19.17", "Currency": "GBP" } }
  ] },
  "Links": { "Self": "…/accounts/123456791/direct-debits" },
  "Meta": { "TotalPages": 1 }
}
```

`DirectDebitStatusCode`: `ACTV` Active · `INAC` Inactive. The list sorts Active-first and the
summary chips count each partition.

`PreviousPaymentAmount` / `PreviousPaymentDateTime` are **optional** — a newly-set mandate has
never collected. The card omits that line entirely rather than rendering an empty row.

## `U000` — the product-gating signal

A savings account (`SVGS`) answers:

```json
{ "Code": "400", "Id": "…", "Message": "Bad Request",
  "Errors": [ { "ErrorCode": "U000", "Message": "This action is not allowed on the account type" } ] }
```

This is **not** a failure. `DirectDebits` = `{PersonalCurrentAccount}` only — the narrowest
capability in the app.

The **store fetcher** records it before rethrowing (`BankingStores.kt:210`):

```kotlin
is NetworkResult.Error -> {
    result.error.recordIfUnsupported(accountId, AccountEndpoint.DirectDebits, capabilityRegistry)
    throw result.error.toThrowable()
}
```

Recording happens in the fetcher, never a ViewModel — the fetcher is the one point every call
passes, including a deep link that bypasses the gated chip entirely.

The ViewModel then maps it to the terminal `Unsupported` state **before** error classification,
so it never reaches a retryable error kind.

## Error matrix

| HTTP | ErrorCode | Kind | UI action |
|---|---|---|---|
| 400 | `U000` | — | **`Unsupported`** terminal state; chip hidden on the next visit |
| 401 | `UK.OBIE.Header.Invalid` | `TokenExpired` | Retry |
| 403 | `UK.OBIE.Resource.ConsentMismatch` | `ConsentRevoked` | message **without** Retry |
| 429 | `UK.OBIE.Rules.TooManyRequests` | `RateLimited` | Retry with back-off |
| 500 | `UK.OBIE.Unexpected.ServerError` | `ServerError` | Retry |
| — | — | `NetworkError` | Retry |
| — | — | empty `Data.DirectDebit[]` | Empty state, not an error |

`isUnsupportedForProduct()` (`core/data/.../util/ObieErrorCodes.kt:35`) guards on `BadRequest`
**and** `U000` in the body, falling back to a substring match when the body will not parse.

## Cache

`createMemoryStore(fetcher)` — no validator, no `markFresh()`, no Room. Direct-debit mandates
are consent-scoped read-only data whose cached copy could outlive the consent that permitted
it. Only `accountsStore` and `transactionsStore` are Room-persisted.

## Source binding

`core/network/api/Aisp.kt` `getDirectDebits` · `BankingStores.directDebitsStore` (memory,
capability-gated) · `DirectDebitsRepositoryImpl` (stateless gateway — the reference
implementation) · `DirectDebitsSummary` model.
