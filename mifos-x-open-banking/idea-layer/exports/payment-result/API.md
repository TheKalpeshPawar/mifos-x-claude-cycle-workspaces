# API Reference — Payment Sent

| Field    | Value                                            |
|----------|--------------------------------------------------|
| Feature  | payment-result                                   |
| Base URL | https://secure.sandbox.ob.hsbc.co.uk             |
| Contract | Client (TPP) — HSBC OBIE sandbox, backend.owned=false |

> All endpoints below are ASPSP-hosted OBIE v4.0 resources consumed by the app as a TPP. There are no owned/server-side endpoints for this screen — `API.md` documents the client contract against HSBC.

---

## GET /obie/open-banking/v4.0/pisp/domestic-payments/{DomesticPaymentId}

**Auth:** Client Credentials grant token (status reads do not need the Authorization Code token)
**Tag:** pisp-domestic
**Trigger:** `on_mount` — fires once when the screen opens; also re-fired by the `RetryStatusPoll` event

Reads the submitted domestic-payment resource by its `DomesticPaymentId` to confirm `Data.Status`. The bank authorise + callback has already completed and the payment was submitted (`POST /pisp/domestic-payments`); this screen polls the created resource to surface the settlement outcome. SCA happened at the bank during authorise — none here.

### Path Parameters

| Name              | Type   | Description                                                                |
|-------------------|--------|---------------------------------------------------------------------------|
| DomesticPaymentId | String | `Data.DomesticPaymentId` returned by the preceding submit POST            |

### Response Fields — `OBWriteDomesticResponse5`

| Field                                       | Type   | Description                                                                                       |
|---------------------------------------------|--------|--------------------------------------------------------------------------------------------------|
| Data.DomesticPaymentId                      | String | ASPSP-assigned payment resource id — surfaced as the shortened Transaction ID row                |
| Data.ConsentId                              | String | Identifier of the consent this payment was created from                                           |
| Data.Status                                 | String | ExternalPaymentTransactionStatus1Code — ACSC/ACSP → success view; RJCT → routes to payment-declined|
| Data.StatusUpdateDateTime                   | String | ISODateTime of the last status update — surfaced as the posted time                               |
| Data.CreationDateTime                       | String | When the payment resource was created                                                             |
| Data.Charges                                | Array  | Optional Charges[] — summed for the Charge row ('0.00' when absent)                               |
| Data.Initiation.InstructedAmount.Amount     | String | Decimal string — the amount paid                                                                  |
| Data.Initiation.InstructedAmount.Currency   | String | ISO 4217 currency code                                                                            |
| Data.Initiation.CreditorAccount.Name        | String | Beneficiary account name. COUNTERPARTY rule applies — never render a raw login username           |

### Demo Data — terminal success (ACSC)

| Field                                     | Demo Value                          |
|-------------------------------------------|-------------------------------------|
| Data.DomesticPaymentId                    | dp-7a21c9f4-3b02-4e88               |
| Data.ConsentId                            | dpc-5f8a3c21-9e44-4b07             |
| Data.Status                               | AcceptedSettlementCompleted         |
| Data.StatusUpdateDateTime                 | 2026-06-12T09:09:02+01:00           |
| Data.Charges[0].Amount                    | 0.00 GBP                            |
| Data.Initiation.InstructedAmount.Amount   | 150.00                              |
| Data.Initiation.InstructedAmount.Currency | GBP                                 |
| Data.Initiation.CreditorAccount.Name      | James Whitfield                     |

> An in-process variant (`AcceptedSettlementInProcess` / ACSP) is also a terminal success view — same layout, "● COMPLETED" pill. See demo-data.yaml#/collections/get_domestic_payment_status_in_process.

### Error Codes

| Code | OBIE Message            | UI Behaviour                                                          |
|------|-------------------------|----------------------------------------------------------------------|
| 400  | OB.Field.Invalid        | show_error_state — bad DomesticPaymentId                              |
| 401  | UNAUTHORIZED            | show_error_state — token expired/invalid                             |
| 404  | OB.Resource.NotFound    | show_error_state — no payment resource for the supplied id (err-dp-9c41a7) |
| 429  | TOO_MANY_REQUESTS       | show_error_state — back off and retry via RetryStatusPoll            |
| 500  | OB.UnexpectedError      | show_error_state                                                     |

### Status Mapping

| `Data.Status` (OBIE)            | Code | Screen outcome                       |
|---------------------------------|------|--------------------------------------|
| AcceptedSettlementCompleted     | ACSC | "● COMPLETED" pill, success view     |
| AcceptedSettlementInProcess     | ACSP | "● COMPLETED" pill, success view     |
| Rejected                        | RJCT | navigate → payment-declined          |

---

_Generated by /idea export | 2026-06-15_
