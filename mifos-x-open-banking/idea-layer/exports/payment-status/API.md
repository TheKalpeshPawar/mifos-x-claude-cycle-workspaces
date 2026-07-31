# Payment status — API Contracts

> Generated from `screens/payment-status/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `6d8300925fe7` · Endpoints: 1 · DTOs: 1

Base path `/obie/open-banking/v4.0/pisp`.

## Endpoint summary

| # | ID | Method | Path | Auth | JWS | Idem | Cache |
|---|---|---|---|---|:--:|:--:|:--:|
| 1 | `domestic-payment-read` | GET | `/domestic-payments/{DomesticPaymentId}` | CC token, scope=payments | — | — | memory |

A **pure read** — no JWS and no idempotency key, unlike the two `send-money` writes. Readable
on the client-credentials payments token, so tracking survives expiry of the single-payment
PSU token obtained during authorisation.

Headers: `x-fapi-interaction-id` (UUID per request; HSBC echoes it for support tracing),
`x-fapi-financial-id`.

## 1 · Read payment

`GET /domestic-payments/{DomesticPaymentId}` → `200` `OBWriteDomesticResponse5`

```json
{
  "Data": {
    "DomesticPaymentId": "PMT-812774903-01",
    "ConsentId": "812774903",
    "Status": "AcceptedSettlementInProcess",
    "CreationDateTime": "2026-07-30T10:44:05+00:00",
    "StatusUpdateDateTime": "2026-07-30T10:44:05+00:00",
    "Initiation": {
      "InstructedAmount": { "Amount": "850.00", "Currency": "GBP" },
      "DebtorAccount":  { "SchemeName": "UK.OBIE.SortCodeAccountNumber", "Identification": "80200110203349", "Name": "Mr Nico" },
      "CreditorAccount":{ "SchemeName": "UK.OBIE.SortCodeAccountNumber", "Identification": "40120965872310", "Name": "Jameson Lettings" },
      "RemittanceInformation": { "Unstructured": ["RENT-FLAT12"] }
    }
  },
  "Links": { "Self": "…/domestic-payments/PMT-812774903-01" },
  "Meta": { "TotalPages": 1 }
}
```

The echoed `Data.Initiation` is the substance of the screen — it supplies amount, payee,
reference and funding account, all formatted in the ViewModel via `core/common` FormatMoney.

## Status → disposition

**`Status` is not a boolean.** A successful submit returns `AcceptedSettlementInProcess` —
accepted, not settled.

| Disposition | OBIE statuses | UI | Poll? |
|---|---|---|:--:|
| `in_progress` | `AcceptedSettlementInProcess`, `AcceptedWithoutPosting`, `Pending` | progress chip + "money has not left your account yet" | ✅ |
| `terminal_success` | `AcceptedSettlementCompleted`, `AcceptedCreditSettlementCompleted` | success chip | ✗ |
| `terminal_failure` | `Rejected` | error chip + new-payment CTA | ✗ |

**Unknown status policy:** treat as `in_progress` and keep polling. Guessing success on an
unmapped code is the worst available failure mode.

## Poll contract

| Parameter | Value |
|---|---|
| runs while | `disposition == in_progress` |
| stops when | terminal success or terminal failure |
| initial interval | 3000 ms |
| backoff | ×1.5, capped 30000 ms |
| max duration | 600000 ms |
| on `429` | double the current interval; keep the last known status rendered |

Polling never starts on a terminal status — it cannot change, so the request is pure waste and
an easy way to earn a rate limit.

## Error matrix

| HTTP | ErrorCode | Meaning | UI action |
|---|---|---|---|
| 400 | `U011` | resource cannot be found — unknown `DomesticPaymentId` | `PaymentNotFound`; **no Retry** — the resource does not exist |
| 401 | `UK.OBIE.Header.Invalid` | payments-scope token expired | Retry after the client re-mints |
| 403 | `UK.OBIE.Resource.ConsentMismatch` | payment consent revoked | **informational only** — a revoked consent does NOT reverse a payment that already settled; the copy must not imply the money came back |
| 429 | `UK.OBIE.Rules.TooManyRequests` | rate limited — most likely the poll is too aggressive | back off; keep last known status on screen |

Errors arrive in the OB envelope `{Code, Id, Message, Errors[{ErrorCode, Message, Path}]}`.

## Caching

`cache_strategy: memory` — `createMemoryStore(fetcher)` keyed by `DomesticPaymentId`. Room
persistence is deliberately not used: a payment status written to disk could outlive the
consent that permitted the read and be shown to a PSU as current when hours stale. Matches
every consent-scoped store in the app.

## Source surface

| | |
|---|---|
| Ships, unconsumed | `core/network/model/pisp/domesticPayment/response/DomesticPaymentResponse.kt` — serialization-tested |
| Missing | `Pisp.kt` client · payments-scope client-credentials token path |

No JWS signer or idempotency handling needed here — this feature makes no write.
