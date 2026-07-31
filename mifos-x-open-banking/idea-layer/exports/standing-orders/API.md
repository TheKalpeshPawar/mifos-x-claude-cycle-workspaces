# Standing orders — API Contracts

> Generated from `screens/standing-orders/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Endpoints: 1 · DTOs: 1

Base path `/obie/open-banking/v4.0/aisp`. AIS read on the PSU bearer.

## Endpoint summary

| # | ID | Method | Path | Permission | Response DTO | Cache |
|---|---|---|---|---|---|---|
| 1 | `standing-orders-list` | GET | `/accounts/{AccountId}/standing-orders` | ReadStandingOrdersDetail | `OBReadStandingOrder6` | memory |

## 1 · Standing orders list

```json
{
  "Data": { "StandingOrder": [
    { "AccountId": "123456791",
      "StandingOrderStatusCode": "ACTV",
      "NextPaymentDateTime": "2019-07-19T10:55:46+00:00",
      "NextPaymentAmount": { "Amount": "12.33", "Currency": "GBP" },
      "CreditorAccount": { "SchemeName": "UK.OBIE.SortCodeAccountNumber", "Identification": "80200110203349", "Name": "Mr Nico" },
      "MandateRelatedInformation": {
        "MandateIdentification": "YZ1733719911",
        "Frequency": { "PointInTime": "01", "Type": "WEEK" } },
      "RemittanceInformation": { "Structured": [ { "CreditorReferenceInformation": { "Reference": "JGUGU1684990055196" } } ] } }
  ] },
  "Links": { "Self": "…/accounts/123456791/standing-orders" },
  "Meta": { "TotalPages": 1 }
}
```

`StandingOrderStatusCode`: `ACTV` Active · `INAC` Inactive.

Note `RemittanceInformation.Structured[]` is an **array of objects**, each wrapping a
`CreditorReferenceInformation.Reference` — not a flat string. Reaching for
`RemittanceInformation.Reference` returns nothing.

## Frequency decoding

`MandateRelatedInformation.Frequency` is a machine code. The sandbox returns the
`{PointInTime, Type}` object form (`{"PointInTime": "01", "Type": "WEEK"}`), but the OBIE
standard also permits the flat string form `IntrvlWkDay:01:5`, which TC-SO-009 pins.

| Code | Meaning |
|---|---|
| `WEEK` / `IntrvlWkDay:{interval}:{day}` | weekly on day *n* (1 = Monday) |
| `MNTH` / `IntrvlMnthDay:{interval}:{day}` | monthly on day *n* |
| `ADHO` | ad-hoc, no schedule |

Decoding happens in the **ViewModel** — composables receive a finished string such as
"Weekly on Fridays", consistent with money and date formatting throughout the app.

## `U000` — product gating

`StandingOrders` = `{PersonalCurrentAccount, ForeignCurrency}`. A savings or credit-card
account answers `400 U000`, recorded by the store fetcher (`BankingStores.kt:320`) against
`AccountEndpoint.StandingOrders` before rethrowing, then mapped to the terminal `Unsupported`
state **before** error classification.

Mechanism identical to `direct-debits` — see `exports/direct-debits/API.md#u000--the-product-gating-signal`.

## Error matrix

| HTTP | ErrorCode | Kind | UI action |
|---|---|---|---|
| 400 | `U000` | — | **`Unsupported`** terminal state |
| 401 | `UK.OBIE.Header.Invalid` | `TokenExpired` | Retry |
| 403 | `UK.OBIE.Resource.ConsentMismatch` | `ConsentRevoked` | distinct message, no Retry |
| 429 | `UK.OBIE.Rules.TooManyRequests` | `RateLimited` | rate-limit-specific message + Retry |
| 500 | `UK.OBIE.Unexpected.ServerError` | `ServerError` | Retry |
| — | — | `NetworkError` | Retry |
| — | — | empty `Data.StandingOrder[]` | Empty state |

## Cache

`createMemoryStore(fetcher)` — consent-scoped read-only data, never Room-persisted.

Pull-to-refresh (TC-SO-010) calls `stream.refresh()` on the stream the ViewModel already holds
— not `repository.refresh()`, which does not exist on a stateless gateway.

## Source binding

`core/network/api/Aisp.kt` `getStandingOrders` · `BankingStores.standingOrdersStore` (memory,
capability-gated) · `StandingOrdersRepository` (stateless).
