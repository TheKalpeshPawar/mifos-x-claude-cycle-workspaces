# SPEC — Send Money

| Field         | Value                |
|---------------|----------------------|
| Feature       | send-money-amount    |
| Flavor        | consumer             |
| Status        | approved             |
| Quality Score | 90                   |
| ViewModel     | SendMoneyViewModel   |
| Archetype     | form                 |

---

## Overview

The Send Money screen is the amount/beneficiary/rail-selection form that sits between the send-money hub and the confirm screen. The user picks a source account, enters an amount, selects (or searches) an existing beneficiary, optionally adds a reference, and chooses a payment rail (SEPA / Domestic / International) via filter chips that disable ineligible rails with a reason. On Continue the screen runs a live Confirmation-of-Funds (CBPII) pre-flight against the source account — `POST /cbpii/funds-confirmations` — and only emits a `PaymentDraft` to send-money-confirm when funds are available. The screen reads the account list, the live InterimAvailable balance (affordability hint + currency prefix), and the beneficiary list (recipient autocomplete, with `CreditorAccount.SchemeName` driving rail classification). It is mobile-only (390px baseline) with a "Send Money" top app bar (back arrow) and no bottom navigation bar.

A sandbox affordance applies: when `useSandboxTan` is set, the rail chips + fee banner + ineligible-reason are replaced by an "Internal bank transfer — sent instantly within the bank." note; large amounts to external accounts surface a `sandbox_block_reason`.

---

## Screens

| ID                | Name       | Route            | Layout | Scroll   |
|-------------------|------------|------------------|--------|----------|
| send-money-amount | Send Money | /send-money/amount| Column | Vertical |

**Shell:** Top app bar — title "Send Money", navigation_icon `arrow_back`, no actions. No bottom navigation bar.

---

## Components

| ID                    | Type       | Description                                                                                                       |
|-----------------------|------------|-----------------------------------------------------------------------------------------------------------------|
| from_account_selector | list_item  | Outlined, leading `account_balance`, trailing `expand_more`, 12dp radius — "Primary Checking — €4,820.00"; on_click select_account |
| amount_input          | input      | Outlined, "€" prefix, "0.00" placeholder, decimal keyboard, 12dp radius; required, rule `amount > 0`             |
| to_label              | text       | "To" — Outfit/label_large, `#44483D`; section heading                                                            |
| beneficiary_search    | input      | Outlined, leading `search`, "Search beneficiary..." placeholder; required; on_click filter_beneficiaries         |
| beneficiary_row       | list_item  | White card, 12dp radius, `#E1E4D5` 1dp border, 12dp padding — selectable beneficiary (e.g. "James Whitfield")    |
| reference_input       | input      | Outlined, "Payment for invoice #1234" placeholder, supporting "Max 35 characters"; max_length 35                |
| payment_type_label    | text       | "Payment Type" — Outfit/label_large, `#44483D`; section heading                                                  |
| payment_type_chips    | chip_group | Filter chips "SEPA · Domestic · International"; ineligible rails disabled with a reason; on_click select_payment_type |
| rail_ineligible_reason| text       | "International unavailable — no BIC on file for this beneficiary" — Outfit/body_small, `#44483D`                  |
| fee_banner            | box        | `#CDEDA3` fill, 8dp radius, leading `info` — "Estimated fee: Free (SEPA)", text `#102000`                        |
| internal_transfer_note| text       | "Internal bank transfer — sent instantly within the bank." — Outfit/body_medium, `#1A1C16` (sandbox path)        |
| sandbox_block_reason  | text       | "On the sandbox, amounts this large can only be sent to accounts within the bank." — Outfit/body_small, `#BA1A1A`|
| continue_button       | button     | "Continue" — filled, 12dp radius, full-width, 52dp height; on_click continue → send-money-confirm; "Checking..." while CoF runs |

---

## States

| ID              | Trigger                                  | Description                                                                                   |
|-----------------|------------------------------------------|----------------------------------------------------------------------------------------------|
| loading         | Screen entry while account + balance load| Progress indicator; no form components visible                                               |
| content         | Data loaded — the default editable form  | from_account_selector, amount_input, To section, beneficiary search + row, reference, payment type chips, ineligible reason, fee_banner, continue_button. Sandbox path swaps chips/fee for internal_transfer_note; preselected beneficiary locks beneficiary_row and hides search |
| empty           | No accounts available to send from        | Empty state: "No accounts available to send from."                                           |
| error           | Form load failed                          | `cloud_off` icon, "Could not load payment form", "Check your connection and try again", retry |
| no_network      | Network unavailable                       | Same shape as error — `cloud_off`, "Could not load payment form", retry                       |
| unauthenticated | Auth/consent invalid                      | Same shape as error — `cloud_off`, "Could not load payment form", retry                       |

---

## State Model

**ViewModel:** `SendMoneyViewModel`
**UI State Type:** `ScreenState<SendMoneyContent>`

| Content field        | Type                              | Notes                                              |
|----------------------|-----------------------------------|----------------------------------------------------|
| accounts             | List\<OBReadAccount6\>            | From-account picker source                          |
| selectedAccount      | OBReadAccount6                    | Chosen source account                              |
| beneficiaries        | List\<OBReadBeneficiary5\>        | Recipient list (reloads on account switch)         |
| selectedBeneficiary  | OBReadBeneficiary5?              | Chosen recipient                                   |
| amount / currency    | String / String                  | `Data.InstructedAmount.Amount` / `.Currency`       |
| reference            | String                           | Payment reference (≤35 chars)                      |
| paymentType          | PaymentType                      | Selected rail                                      |
| railAssessments      | Map\<PaymentType, RailAssessment\>| Per-rail eligibility + reason                       |
| fundsAvailable       | Boolean?                          | `Data.FundsAvailable` from the CoF check           |
| amountError / beneficiaryError / formError | String?     | Inline validation                                  |
| submitting           | Boolean                          | Continue in-flight                                 |
| useSandboxTan        | Boolean                          | Sandbox internal-transfer path                     |
| sandboxBlockReason   | String?                          | Large-amount sandbox restriction                   |
| continueEnabled      | Boolean (derived)                | Gate for the Continue button                        |

**Events:** `setAccount`, `onAmountChanged`, `onBeneficiaryQueryChanged`, `onBeneficiarySelected`, `onReferenceChanged`, `onPaymentTypeChanged`, `onRetry`, `onContinue`

**Actions:** `select_account`, `select_beneficiary`, `filter_beneficiaries`, `select_payment_type`, `continue`

**Nav params:** `preselectedCounterpartyId` (default ""), `accountId` (default "")

**Callbacks:** `onContinue(PaymentDraft)` → send-money-confirm; `onBack`

**Collaborators:** `PaymentRailClassifier`

**DI Dependencies:** `AccountsRepository`, `PaymentsRepository`, `BanksRepository`, `isSandbox` (named qualifier)

---

## Navigation

| From              | To                 | Trigger                     | Type     |
|-------------------|--------------------|-----------------------------|----------|
| send-money-amount | send-money-confirm | continue_button (CoF passes)| navigate |
| send-money-amount | (back)             | top app bar back arrow      | pop      |

---

## API Endpoints

| Endpoint                                                              | Method | Auth                   | Tag  | Purpose                                          |
|----------------------------------------------------------------------|--------|------------------------|------|--------------------------------------------------|
| /obie/open-banking/v4.0/aisp/accounts                                | GET    | Auth Code (accounts)   | AISP | From-account picker                              |
| /obie/open-banking/v4.0/aisp/accounts/{AccountId}/balances           | GET    | Auth Code (ReadBalances)| AISP | Live InterimAvailable balance — affordability hint|
| /obie/open-banking/v4.0/aisp/accounts/{AccountId}/beneficiaries      | GET    | Auth Code (ReadBeneficiaries)| AISP | Beneficiary list — recipient autocomplete   |
| /obie/open-banking/v4.0/cbpii/funds-confirmations                    | POST   | Auth Code (fundsconfirmations)| CBPII | Confirmation-of-Funds check on Continue    |

> Client (TPP) contract against the HSBC OBIE sandbox (`backend.owned=false`). The CoF check has an alternative when a domestic-payment-consent (Status AUTH) already exists: `GET /pisp/domestic-payment-consents/{ConsentId}/funds-confirmation` → `Data.FundsAvailableResult.FundsAvailable`.

---

## Design Tokens

| Token                           | Value           | Usage                                                       |
|---------------------------------|-----------------|------------------------------------------------------------|
| colors.light.primary            | #4C662B         | continue_button fill, beneficiary_row accent               |
| colors.light.on_primary         | #FFFFFF         | continue_button label                                      |
| colors.light.primary_container  | #CDEDA3         | fee_banner background                                      |
| colors.light.surface            | #FFFFFF         | beneficiary_row background                                 |
| colors.light.on_surface         | #1A1C16         | internal_transfer_note, input values                      |
| colors.light.on_surface_variant | #44483D         | to_label, payment_type_label, rail_ineligible_reason      |
| colors.light.surface_variant    | #E1E4D5         | beneficiary_row border                                    |
| colors.light.error              | #BA1A1A         | sandbox_block_reason text                                  |
| typography.label_large          | Outfit 14sp/500 | to_label, payment_type_label                              |
| typography.body_medium          | Outfit 14sp/400 | internal_transfer_note                                    |
| typography.body_small           | Outfit 12sp/400 | rail_ineligible_reason, sandbox_block_reason             |
| radius.md                       | 12dp            | inputs, beneficiary_row, continue_button corner radius     |
| radius.sm                       | 8dp             | fee_banner corner radius                                  |

---

_Generated by /idea export | 2026-06-15_
