# Beneficiaries — API Contracts

> Generated from `screens/beneficiaries/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Endpoints: 1 · DTOs: 1

Base path `/obie/open-banking/v4.0/aisp`. AIS read on the PSU bearer — no JWS, no idempotency.

## Endpoint summary

| # | ID | Method | Path | Permission | Response DTO | Cache |
|---|---|---|---|---|---|---|
| 1 | `beneficiaries-list` | GET | `/accounts/{AccountId}/beneficiaries` | ReadBeneficiariesDetail | `OBReadBeneficiary5` | memory |

## 1 · Beneficiaries list

```json
{
  "Data": { "Beneficiary": [
    { "AccountId": "123456791", "Reference": "BFRS.RFRNC.545",
      "CreditorAccount": {
        "SchemeName": "UK.OBIE.SortCodeAccountNumber",
        "Identification": "80200110203350",
        "Name": "Mr Dharani C",
        "SecondaryIdentification": "00023" },
      "CreditorAgent": { "SchemeName": "UK.OBIE.BICFI", "Identification": "HSBCDEFF325", "Name": "Omega Bank", "PostalAddress": { … } } }
  ] },
  "Links": { "Self": "…/accounts/123456791/beneficiaries" }
}
```

**All creditor name and identification fields are PII.**

Note the live sandbox response has **no `Meta.TotalPages`** on this endpoint, unlike most AIS
resources — do not assume it is present.

### Scheme-label mapping (ViewModel layer)

| `SchemeName` | Display label |
|---|---|
| `UK.OBIE.SortCodeAccountNumber` | Sort Code |
| `UK.OBIE.IBAN` | IBAN |
| `UK.OBIE.Paym` | Paym |
| `UK.OBIE.PAN` | Card |
| *(default)* | Account |

## Client-side search

`Search` filters the resident list — **no API round-trip**:

```kotlin
beneficiaries.filter {
    it.CreditorAccount.Name.contains(query, ignoreCase = true) ||
    it.Reference.contains(query, ignoreCase = true)
}
```

Reference matching is why TC-BEN-010 exists separately from TC-BEN-006: a PSU searching
"RENT" is looking for the reference, not the payee name.

## Error matrix

| HTTP | ErrorCode | Kind | UI action |
|---|---|---|---|
| 401 | `UK.OBIE.Header.Invalid` | `TokenExpiredError` | Retry; VM clears the stale token first |
| 403 | `UK.OBIE.Resource.ConsentMismatch` | `ConsentRevokedError` | **View Consents** → consent-list |
| 429 | `UK.OBIE.Rules.TooManyRequests` | `RateLimitedError` | Retry with back-off |
| 500 | `UK.OBIE.Unexpected.ServerError` | `ServerError` | Retry |
| — | — | `NetworkError` | Retry |
| — | — | empty `Data.Beneficiary[]` | Empty state, not an error |

## Product gating

Beneficiaries is one of five gated Explore options — offered on every product **except** a
credit card (the mirror of Statements, which is credit-card-only). Prediction is
`HsbcProductCapability.supports`; correction is the store fetcher recording a `U000` refusal
before rethrowing.

## Source binding

`core/network/api/Aisp.kt` `getBeneficiaries` · `BankingStores.beneficiariesStore`
(`createMemoryStore` — consent-scoped, never Room) · `BeneficiariesRepository` (stateless) ·
`BeneficiaryMapper` → `BeneficiaryItem`.
