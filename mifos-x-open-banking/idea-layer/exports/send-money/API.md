# Send money — API Contracts

> Generated from `screens/send-money/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `7d924d371fb0` · Endpoints: 3 · DTOs: 5
>
> Re-stamped 2026-07-31. `api.yaml` did not change in that pass — the three endpoints, five
> DTOs and the error matrix below are byte-identical to the 07-30 export. Only the
> feature-level source hash moved, because `ui.yaml` gained the review-card rows, the
> step indicator and the no-payees affordance.

Base path `/obie/open-banking/v4.0/pisp` (AIS resources are `v4.0/aisp`; OAuth is `v1.1`).

## Endpoint summary

| # | ID | Method | Path | Auth | JWS | Idem | Cache |
|---|---|---|---|---|:--:|:--:|:--:|
| 1 | `domestic-payment-consent-create` | POST | `/domestic-payment-consents` | CC token, scope=payments | ✅ | ✅ | none |
| 2 | `domestic-payment-funds-confirmation` | GET | `/domestic-payment-consents/{ConsentId}/funds-confirmation` | PSU bearer | — | — | none |
| 3 | `domestic-payment-submit` | POST | `/domestic-payments` | PSU bearer | ✅ | ✅ | none |

No table column: this project owns no server-side tables. `cache_strategy: none` — a cached
payment response could show a stale "accepted" for a payment that later failed, or invite a
duplicate submission. Duplicate protection comes from the idempotency key, not a cache.

## Write-call header contract

New to this app — no AIS read needs either header.

**`x-jws-signature`** — detached PS256 over the request body, header claims `b64: false` plus
`crit: ["b64", "http://openbanking.org.uk/iat", ".../iss", ".../tan"]`. Detached means the
payload segment is stripped, leaving `header..signature`. Reuses `signPs256` from
`core/network/BuildClientAssertion.kt`, already shipped for the FAPI client assertion.
**Absent → `400` `U019` "Missing information related to signature"** (captured live).

**`x-idempotency-key`** — ≤40 chars, generated once per staged payment and reused across the
consent stage, the submit, and every retry of either.

**`x-fapi-interaction-id`** — UUID per request; HSBC echoes it for support tracing.
**`x-fapi-financial-id`** — fixed OB institution identifier.

## 1 · Create payment consent

`POST /domestic-payment-consents` → `201` `OBWriteDomesticConsentResponse5`

Request `OBWriteDomesticConsent4`:

```json
{
  "Data": {
    "Initiation": {
      "InstructionIdentification": "MFX20260730T1042330001",
      "EndToEndIdentification": "E2E-RENT-FLAT12-202607",
      "InstructedAmount": { "Amount": "850.00", "Currency": "GBP" },
      "DebtorAccount":  { "SchemeName": "UK.OBIE.SortCodeAccountNumber", "Identification": "80200110203349", "Name": "Mr Nico" },
      "CreditorAccount":{ "SchemeName": "UK.OBIE.SortCodeAccountNumber", "Identification": "40120965872310", "Name": "Jameson Lettings" },
      "RemittanceInformation": { "Unstructured": ["RENT-FLAT12"] }
    }
  },
  "Risk": { "PaymentContextCode": "TransferToThirdParty" }
}
```

**Note what is absent.** No `MerchantCategoryCode`, no `MerchantCustomerIdentification`, no
`DeliveryAddress`. `OBRisk1` declares no required properties, so a consumer payment sends
`PaymentContextCode` alone.

Spec-required on `Initiation`: `InstructionIdentification`, `EndToEndIdentification`,
`InstructedAmount`, `CreditorAccount`. `DebtorAccount` is **optional** in the spec but this
app always supplies it — the PSU picked the account in step 1.

Response carries `Data.ConsentId`, `Data.Status` (`AWAU` → `AUTH` | `RJCT`) and an echoed
`Data.Initiation` that must be resent byte-identically on submit.

## 2 · Funds confirmation

`GET /domestic-payment-consents/{ConsentId}/funds-confirmation` → `200`
`OBWriteFundsConfirmationResponse1` → `Data.FundsAvailableResult.{FundsAvailable, FundsAvailableDateTime}`

Optional pre-submit check, callable only once the consent is `Authorised` (needs the PSU
token). `FundsAvailable: false` surfaces as `InsufficientFunds` and the payment is **not**
submitted.

## 3 · Submit payment

`POST /domestic-payments` → `201` `OBWriteDomesticResponse5`

Request `OBWriteDomestic2` carries `Data.ConsentId` + a **byte-identical echo** of the staged
`Data.Initiation`. Any divergence returns `400 U008`.

Response: `Data.DomesticPaymentId`, `ConsentId`, `Status`, `CreationDateTime`,
`StatusUpdateDateTime`, echoed `Initiation`.

**`Status` is not a boolean.** A successful submit returns `AcceptedSettlementInProcess` —
accepted, not settled. Consumers map it through
`design-tokens.yaml#semantic.payment_disposition`; see `payment-status` for the tracking read.

## Error matrix

| HTTP | ErrorCode | Meaning | UI action |
|---|---|---|---|
| 400 | `U019` | missing/malformed detached JWS | non-recoverable + support ref; **no Retry** |
| 400 | `U014` | payment outside control parameters | return to Amount step |
| 400 | `U002` | invalid field (usually CreditorAccount.Identification) | return to Recipient step |
| 400 | `U008` | staged consent ≠ submitted order | discard staged consent, restart |
| 400 | `U009` | consent not Authorised | Re-authorise → `payment-consent` |
| 401 | `UK.OBIE.Header.Invalid` | token expired | Retry after re-mint |
| 403 | `UK.OBIE.Resource.ConsentMismatch` | consent revoked | View Consents |
| 429 | `UK.OBIE.Rules.TooManyRequests` | rate limited | back-off, honour `Retry-After` |

Errors arrive in the OB envelope `{Code, Id, Message, Errors[{ErrorCode, Message, Path}]}`.
Quote `Id` in support tickets — it is what `SignatureMissing` surfaces to the PSU.

## Source surface

| | |
|---|---|
| Ships, unconsumed | `core/network/model/pisp/domesticPayment/{request,response}/` — serialization-tested, all-nullable |
| Missing | `Pisp.kt` client · detached-JWS signer · idempotency-key handling · payments-scope token path |
