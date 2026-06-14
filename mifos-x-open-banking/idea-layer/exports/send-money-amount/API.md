# API Reference — Send Money

| Field    | Value                                            |
|----------|--------------------------------------------------|
| Feature  | send-money-amount                                |
| Base URL | https://secure.sandbox.ob.hsbc.co.uk             |
| Contract | Client (TPP) — HSBC OBIE sandbox, backend.owned=false |

> All endpoints are ASPSP-hosted OBIE v4.0 resources consumed by the app as a TPP. No owned/server-side endpoints exist for this screen — `API.md` documents the client contract.

---

## GET /obie/open-banking/v4.0/aisp/accounts

**Auth:** Authorization Code token (scope `accounts`), authorised account-access-consent (Status AUTH)
**Tag:** AISP — DTO `OBReadAccount6`

Lists the PSU's authorised accounts for the From-account picker.

| Response field                         | Type   | Notes                          |
|----------------------------------------|--------|--------------------------------|
| Data.Account[].AccountId               | String | Account resource id            |
| Data.Account[].Nickname                | String | Display label                  |
| Data.Account[].Currency                | String | ISO 4217 — drives amount prefix|
| Data.Account[].Account[].Identification| String | Sort-code/account number       |

**Demo:** `acc-30000012345678` "Everyday Current" GBP (Oliver Bennett); `acc-30000098765432` "Rainy Day Saver" GBP.

---

## GET /obie/open-banking/v4.0/aisp/accounts/{AccountId}/balances

**Auth:** Authorization Code token, scope `ReadBalances`
**Tag:** AISP — DTO `OBReadBalance1`

Live balance for the selected source account — drives the affordability hint and the amount-entry currency prefix. Prefer `Type InterimAvailable`.

| Response field               | Type   | Notes                         |
|------------------------------|--------|-------------------------------|
| Data.Balance[].Type          | String | Prefer `InterimAvailable`     |
| Data.Balance[].Amount.Amount | String | e.g. "2483.57"                |
| Data.Balance[].Amount.Currency| String| e.g. "GBP"                    |

**Demo:** InterimAvailable 2483.57 GBP on `acc-30000012345678`.

---

## GET /obie/open-banking/v4.0/aisp/accounts/{AccountId}/beneficiaries

**Auth:** Authorization Code token, scope `ReadBeneficiariesBasic`/`Detail`
**Tag:** AISP — DTO `OBReadBeneficiary5`

Beneficiary list for the selected account (reloads on account switch). `CreditorAccount.SchemeName` drives rail classification (`UK.OBIE.IBAN` vs `UK.OBIE.SortCodeAccountNumber`).

| Response field                                  | Type   | Notes                       |
|-------------------------------------------------|--------|-----------------------------|
| Data.Beneficiary[].BeneficiaryId                | String | Beneficiary resource id     |
| Data.Beneficiary[].CreditorAccount.Name         | String | Recipient name              |
| Data.Beneficiary[].CreditorAccount.SchemeName   | String | Drives rail classification  |
| Data.Beneficiary[].CreditorAccount.Identification| String | Account identification      |

**Demo:** James Whitfield (`20415587224190`), British Gas (`60000412009988`), Thames Water (`40020755663210`) — all `UK.OBIE.SortCodeAccountNumber`.

---

## POST /obie/open-banking/v4.0/cbpii/funds-confirmations

**Auth:** Authorization Code token (scope `fundsconfirmations`) + a `ConsentId` in the payload
**Tag:** CBPII — request `OBFundsConfirmation1`, response `OBFundsConfirmationResponse1`
**Trigger:** `onContinue` — the Confirmation-of-Funds pre-flight before navigating to confirm

Confirms the entered amount is available on the source account against a standing funds-confirmation-consent. `InstructedAmount.Currency` MUST equal the account currency.

### Request Fields

| Field                          | Type   | Notes                                   |
|--------------------------------|--------|-----------------------------------------|
| Data.ConsentId                 | String | funds-confirmation-consent id           |
| Data.Reference                 | String | Free-text reference                     |
| Data.InstructedAmount.Amount   | String | Decimal string — the entered amount     |
| Data.InstructedAmount.Currency | String | ISO 4217 — must match account currency  |

### Response Fields

| Field                      | Type    | Notes                                       |
|----------------------------|---------|---------------------------------------------|
| Data.FundsConfirmationId   | String  | Resource id                                 |
| Data.FundsAvailable        | Boolean | Gate — Continue proceeds only when `true`   |
| Data.ConsentId             | String  | Echoed consent id                           |

### Demo Data

| Field                          | Demo Value                |
|--------------------------------|---------------------------|
| Request ConsentId              | cofc-7b41e2a9-5d10-49c8   |
| Request InstructedAmount       | 150.00 GBP                |
| Response FundsConfirmationId   | fc-9d2f7c01-aa34          |
| Response FundsAvailable        | true                      |

### Error Codes

| Code | OBIE Message                      | UI Behaviour                                                  |
|------|-----------------------------------|--------------------------------------------------------------|
| 400  | OB.Field.Invalid                  | Inline error — currency mismatch (err-cof-7f2a1b: "InstructedAmount.Currency must match the account currency (GBP)") |
| 401  | UNAUTHORIZED                      | Route to unauthenticated state                               |
| 403  | OB.Resource.InvalidConsentStatus  | Inline error — funds-confirmation-consent not authorised     |

### Alternative CoF path

When a domestic-payment-consent already exists and is Status AUTH, use
`GET /obie/open-banking/v4.0/pisp/domestic-payment-consents/{ConsentId}/funds-confirmation`
which returns `Data.FundsAvailableResult.FundsAvailable` instead.

---

## Continue Flow

On Continue: validate (amount > 0, beneficiary selected) → run the CoF check → if `Data.FundsAvailable == true`, emit a `PaymentDraft` and navigate to send-money-confirm. The Continue label shows "Checking..." while the check runs. On `FundsAvailable == false` or an error, surface the inline `formError` and keep the form editable.

---

_Generated by /idea export | 2026-06-15_
