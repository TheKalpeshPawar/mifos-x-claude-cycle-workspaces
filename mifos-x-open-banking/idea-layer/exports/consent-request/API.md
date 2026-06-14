# API Reference — Review & Grant Access (Consent Request)

| Field    | Value                                                      |
|----------|------------------------------------------------------------|
| Feature  | consent-request                                            |
| Base URL | https://secure.sandbox.ob.hsbc.co.uk                      |

---

## POST /obie/open-banking/v4.0/aisp/account-access-consents

**Auth:** Client Credentials (`Bearer {cc_access_token}` — acquired by `ObpAuthRepository` before the call; NOT the PSU's DirectLogin token)
**Tag:** AccountInformation
**Trigger:** `ConsentRequestAction.GrantClicked` — fires after the PSU taps "Grant access"

Registers an OBIE account-access-consent with the ASPSP (HSBC UK sandbox). The request body (`OBReadConsent1`) carries all 10 permission clusters and an optional `ExpirationDateTime` (defaults to creation + 90 days). On a `201 Created` the ASPSP returns `OBReadConsentResponse1` with `Data.ConsentId` and `Data.Status = "AWAU"` (awaiting PSU authorisation). The `ConsentId` becomes the `openbanking_intent_id` for the subsequent signed authorise request built in `bank-authorize-handoff`.

FAPI 1.0 Advanced security: mTLS QWAC transport + detached `x-jws-signature` on this write endpoint + `x-idempotency-key` for safe retry. These are applied by the OkHttp/Ktor network interceptor layer, not surfaced in UI state.

### Request Headers

| Header                | Example Value                              | Description                                                      |
|-----------------------|--------------------------------------------|------------------------------------------------------------------|
| Authorization         | Bearer {cc_access_token}                   | Client-credentials access token from HSBC token endpoint         |
| x-fapi-financial-id   | {fapi_financial_id}                        | ASPSP-specific FAPI financial institution ID                     |
| x-fapi-interaction-id | {uuid}                                     | Unique UUID per interaction for FAPI audit trail                 |
| x-jws-signature       | {detached_jws}                             | Detached JWS signature (FAPI 1.0 Advanced write-endpoint signing) |
| x-idempotency-key     | {idempotency_key}                          | Safe retry — ASPSP deduplicates on this key per consent          |
| Content-Type          | application/json                           |                                                                  |

### Request Body — OBReadConsent1

```json
{
  "Data": {
    "Permissions": [
      "ReadAccountsDetail",
      "ReadBalances",
      "ReadTransactionsDetail",
      "ReadBeneficiariesDetail",
      "ReadStandingOrdersDetail",
      "ReadDirectDebits",
      "ReadScheduledPaymentsDetail",
      "ReadParty",
      "ReadProducts",
      "ReadStatementsDetail"
    ],
    "ExpirationDateTime": "2026-09-11T09:41:18.204Z"
  },
  "Risk": {}
}
```

### Response Fields — OBReadConsentResponse1 (201 Created)

| Field                      | Type    | Description                                                                            |
|----------------------------|---------|----------------------------------------------------------------------------------------|
| Data.ConsentId             | String  | ASPSP-assigned consent ID — stored as `consentId` in ViewModel; used as `openbanking_intent_id` |
| Data.Status                | String  | `AWAU` — awaiting PSU authorisation. Full enum: `AWAU \| AUTH \| RJCT \| CANC \| EXPD` |
| Data.CreationDateTime      | String  | ISO-8601 UTC consent creation timestamp                                                 |
| Data.StatusUpdateDateTime  | String  | ISO-8601 UTC last status update timestamp                                               |
| Data.Permissions           | Array   | Echo of the requested permission clusters                                               |
| Data.ExpirationDateTime    | String  | Echo of the requested expiry; open-ended if absent                                     |
| Links.Self                 | String  | Canonical URL for this consent resource                                                 |
| Meta.TotalPages            | Integer | Always 1 for a single consent resource                                                  |

### Demo Response (201 Created)

| Data.ConsentId        | Data.Status | Data.CreationDateTime      | Data.ExpirationDateTime    | Data.Permissions count |
|-----------------------|-------------|----------------------------|----------------------------|------------------------|
| aac-9f2c1b7e-3d44-4a02 | AWAU       | 2026-06-12T09:41:18.204Z   | 2026-09-11T09:41:18.204Z   | 10                     |

> Links.Self: `https://secure.sandbox.ob.hsbc.co.uk/obie/open-banking/v4.0/aisp/account-access-consents/aac-9f2c1b7e-3d44-4a02`

### Demo Request Body (OBReadConsent1)

| Data.Permissions (all 10)     | Data.ExpirationDateTime    | Risk  |
|-------------------------------|----------------------------|-------|
| ReadAccountsDetail, ReadBalances, ReadTransactionsDetail, ReadBeneficiariesDetail, ReadStandingOrdersDetail, ReadDirectDebits, ReadScheduledPaymentsDetail, ReadParty, ReadProducts, ReadStatementsDetail | 2026-09-11T09:41:18.204Z | {} |

### Error Codes

| Code | OBIE Error Key          | UI Message (error banner)                                                      |
|------|-------------------------|--------------------------------------------------------------------------------|
| 400  | UK.OBIE.Field.Invalid   | "We couldn't start your connection. Please check your network and try again."  |
| 401  | UNAUTHORIZED            | "We couldn't authorise this connection. Please try again."                     |
| 403  | OB_INVALID_CONSENT_STATUS | "This connection is no longer valid. Please start again."                    |
| 429  | TOO_MANY_REQUESTS       | "Too many attempts. Please wait a moment and try again."                       |
| 500  | OB_UNEXPECTED_ERROR     | "Something went wrong on our end. Please try again in a moment."              |

---

_Generated by /idea export | 2026-06-15_
