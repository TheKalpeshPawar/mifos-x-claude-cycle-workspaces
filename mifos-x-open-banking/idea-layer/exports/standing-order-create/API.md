# API Reference — New Standing Order

| Field    | Value                                            |
|----------|--------------------------------------------------|
| Feature  | standing-order-create                            |
| Base URL | https://secure.sandbox.ob.hsbc.co.uk             |
| Contract | Client (TPP) — HSBC OBIE sandbox, backend.owned=false |

> Both endpoints are ASPSP-hosted OBIE PISP v4.0 resources consumed by the app as a TPP. No owned/server-side endpoints exist for this screen. Creation is a two-step consent flow: **this screen** POSTs the consent (step 1); payment-authorize-handoff submits after the bank authorise + callback (step 2).

---

## POST /obie/open-banking/v4.0/pisp/domestic-standing-order-consents  ← this screen's submit

**Auth:** Client Credentials grant token
**Tag:** pisp-domestic-standing-order — request `OBWriteDomesticStandingOrderConsent5`, response `OBWriteDomesticStandingOrderConsentResponse6`
**Trigger:** `onSubmit` — fires when the user taps "Create standing order"

Stages the recurring standing-order instruction. The ASPSP returns a `ConsentId` with Status `AwaitingAuthorisation` (AWAU). After this the screen navigates to payment-authorize-handoff to complete authorisation and submit.

### Request Fields

| Field                                       | Type   | Notes                                                                                  |
|---------------------------------------------|--------|---------------------------------------------------------------------------------------|
| Data.Permission                             | String | Fixed value `Create`                                                                   |
| Data.Initiation.Frequency                   | String | OBIE schedule code, e.g. `IntrvlMnthDay:01:05` (monthly), `IntrvlWkDay:01:05` (weekly), `EvryDay` (daily) — mapped from the chip + chosen anchor weekday/day |
| Data.Initiation.Reference                   | String | Optional payment reference                                                             |
| Data.Initiation.NumberOfPayments            | String | Optional total count (derived from an end date when set)                               |
| Data.Initiation.FirstPaymentDateTime        | String | ISO 8601 — the recurrence anchor (chosen start date at T00:00:00)                      |
| Data.Initiation.RecurringPaymentAmount.Amount| String| Decimal string > 0 — per-occurrence amount                                             |
| Data.Initiation.RecurringPaymentAmount.Currency| String| ISO 4217 (source account currency)                                                  |
| Data.Initiation.FirstPaymentAmount.Amount   | String | Decimal string — defaults to the recurring amount                                      |
| Data.Initiation.FirstPaymentAmount.Currency | String | ISO 4217                                                                               |
| Data.Initiation.CreditorAccount.SchemeName  | String | e.g. `UK.OBIE.SortCodeAccountNumber` (from the selected payee)                         |
| Data.Initiation.CreditorAccount.Identification| String| Creditor account identification (selected payee)                                       |
| Data.Initiation.CreditorAccount.Name        | String | Creditor account name (selected payee)                                                 |
| Risk                                        | Object | OBRisk block (may be empty `{}`)                                                       |

### Response Fields

| Field                  | Type   | Notes                                                          |
|------------------------|--------|---------------------------------------------------------------|
| Data.ConsentId         | String | Carried to payment-authorize-handoff to drive authorise + submit|
| Data.Status            | String | `AwaitingAuthorisation` (AWAU) on creation                    |
| Data.CreationDateTime  | String | When the consent was staged                                   |
| Data.Initiation        | Object | Echoed standing-order initiation block                       |

### Demo Data — request → response (GBP 92.00/month to British Gas)

| Field                                        | Demo Value                  |
|----------------------------------------------|-----------------------------|
| Data.Initiation.Frequency                    | IntrvlMnthDay:01:05         |
| Data.Initiation.Reference                    | Gas and Electric            |
| Data.Initiation.NumberOfPayments             | 12                          |
| Data.Initiation.FirstPaymentDateTime         | 2026-07-05T00:00:00+01:00   |
| Data.Initiation.RecurringPaymentAmount       | 92.00 GBP                   |
| Data.Initiation.CreditorAccount.Identification| 60000412009988             |
| Data.Initiation.CreditorAccount.Name         | British Gas                 |
| Response Data.ConsentId                      | dsoc-8c14a7e2-6f30-4b91     |
| Response Data.Status                         | AwaitingAuthorisation       |

### Error Codes

| Code | OBIE Message                      | UI Behaviour                                                  |
|------|-----------------------------------|--------------------------------------------------------------|
| 400  | OB.Field.Invalid                  | Inline soc_error_text — e.g. "Initiation.FirstPaymentDateTime must be a future date" (err-dsoc-1f73c8) |
| 401  | UNAUTHORIZED                      | Inline error — token expired/invalid                         |
| 403  | OB.Resource.InvalidConsentStatus  | Inline error — consent state conflict                        |
| 429  | TOO_MANY_REQUESTS                 | Inline error — back off and retry                            |
| 500  | OB.UnexpectedError                | Inline error                                                 |

---

## POST /obie/open-banking/v4.0/pisp/domestic-standing-orders  ← payment-authorize-handoff (not this screen)

**Auth:** Authorization Code grant token
**Tag:** pisp-domestic-standing-order — request `OBWriteDomesticStandingOrder3`, response `OBWriteDomesticStandingOrderResponse6`
**Trigger:** `post_authorize_callback` — invoked by payment-authorize-handoff after the bank authorise + callback

Submits the authorised standing order referencing the now-Authorised `ConsentId`. `Data.Initiation` must byte-match the consent. Documented here for completeness of the create flow; this screen does not call it directly.

| Request field    | Type   | Notes                                                  |
|------------------|--------|--------------------------------------------------------|
| Data.ConsentId   | String | Must equal the authorised consent ConsentId            |
| Data.Initiation  | Object | Must match the consent's initiation exactly            |
| Risk             | Object | OBRisk block matching the consent                      |

| Response field              | Type   | Notes                                       |
|-----------------------------|--------|---------------------------------------------|
| Data.DomesticStandingOrderId| String | Unique standing-order resource id           |
| Data.ConsentId              | String | Echoed consent id                           |
| Data.Status                 | String | e.g. `InitiationPending` / `InitiationCompleted`|
| Data.CreationDateTime       | String | When the order was created                   |

**Demo:** `dso-4e90b71c-22a5`, Status `InitiationCompleted`, ConsentId `dsoc-8c14a7e2-6f30-4b91`.

---

## Local Cache Write

After a successful submit (step 2), the created standing order may be appended to the per-account `standing-orders-created:{accountId}` entry in the Room JSON cache so it shows in the derived list immediately, alongside reads from `GET /pisp/domestic-standing-orders/{DomesticStandingOrderId}`.

---

## Submit Flow

`onSubmit` validates the form → POSTs the consent → on AWAU response, sets `form.created = true` and `form.consentId`, then navigates to payment-authorize-handoff carrying the `ConsentId`. The handoff orchestrates consent → bank authorise → callback → submit. SCA happens at the bank.

---

_Generated by /idea export | 2026-06-15_
