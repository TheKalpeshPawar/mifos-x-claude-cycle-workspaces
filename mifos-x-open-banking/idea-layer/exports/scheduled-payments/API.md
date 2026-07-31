# Scheduled payments — API Contracts

> Generated from `screens/scheduled-payments/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Endpoints: 1 · DTOs: 1

Base path `/obie/open-banking/v4.0/aisp`. AIS read on the PSU bearer.

## Endpoint summary

| # | ID | Method | Path | Permission | Response DTO | Cache |
|---|---|---|---|---|---|---|
| 1 | `scheduled-payments-list` | GET | `/accounts/{AccountId}/scheduled-payments` | ReadScheduledPaymentsDetail | `OBReadScheduledPayment3` | memory |

## 1 · Scheduled payments list

```json
{
  "Data": { "ScheduledPayment": [
    { "AccountId": "123456791",
      "ScheduledPaymentId": "7",
      "ScheduledPaymentDateTime": "2019-06-02T00:00:00+00:00",
      "ScheduledType": "Execution",
      "Reference": "1234567891",
      "DebtorReference": "123455678",
      "InstructedAmount": { "Amount": "19.17", "Currency": "GBP" },
      "CreditorAccount": {
        "SchemeName": "UK.OBIE.SortCodeAccountNumber",
        "Identification": "80200110203349",
        "Name": "Mr Nico",
        "SecondaryIdentification": "00022" },
      "CreditorAgent": { "SchemeName": "UK.OBIE.BICFI", "Identification": "HSBCDEFF325", "Name": "Omega Bank", "PostalAddress": { … } } }
  ] },
  "Links": { "Self": "…/accounts/123456791/scheduled-payments" },
  "Meta": { "TotalPages": 1 }
}
```

### `ScheduledType` drives the date label

| Value | Chip label | Meaning |
|---|---|---|
| `Execution` | "Execution date" | the day the bank *sends* the money |
| `Arrival` | "Arrival date" | the day it *reaches* the payee |

TC-SP-007 pins this. Labelling an Arrival date as an Execution date misstates when a customer's
money leaves — the same class of mistake as calling an in-progress payment "sent".

Two reference fields, easily confused: `Reference` is the payee-facing payment reference;
`DebtorReference` is the PSU's own note.

## Product gating

`ScheduledPayments` = `ALL_PRODUCTS − CreditCard` — {PersonalCurrentAccount, Savings,
ForeignCurrency}. The **mirror of Statements** (credit-card-only): a credit card is the one
product that hides Scheduled and shows Statements.

The store fetcher records a `U000` against `AccountEndpoint.ScheduledPayments`
(`BankingStores.kt:353`) before rethrowing, so account-detail hides the chip on the next visit.

> **Divergence from its siblings:** this feature declares **no `Unsupported` UiState**. A `U000`
> therefore surfaces through the ordinary error path rather than a terminal product-refusal
> state, unlike `direct-debits` and `standing-orders`. The gating still works — the chip hides —
> but a PSU who reaches the screen by deep link sees a retryable error for a product refusal
> that can never succeed. Recorded, not invented.

## Error matrix

| HTTP | ErrorCode | Kind | Retry? |
|---|---|---|:--:|
| 400 | `U000` | falls through to the generic error path — see above | ✅ (arguably wrong) |
| 401 | `UK.OBIE.Header.Invalid` | `TokenExpired` | ✅ |
| 403 | `UK.OBIE.Resource.ConsentMismatch` | `ConsentRevoked` | ✅ |
| 429 | `UK.OBIE.Rules.TooManyRequests` | `RateLimited` | ✅ back-off |
| — | — | `NetworkError` | ✅ |
| — | — | empty `Data.ScheduledPayment[]` | Empty state |

All four declared kinds are retriable — unlike `direct-debits`, where `ConsentRevoked` is
terminal. Here a consent-scope 403 offers Retry because re-authorising in Consents is a path
back.

## Cache

`createMemoryStore(fetcher)` — consent-scoped read-only data, never Room-persisted.

## Source binding

`core/network/api/Aisp.kt` `getScheduledPayments` · `BankingStores.scheduledPaymentsStore`
(memory, capability-gated) · `ScheduledPaymentsRepository` (stateless) ·
`ScheduledPaymentMapper` → `ScheduledPaymentItem`.
