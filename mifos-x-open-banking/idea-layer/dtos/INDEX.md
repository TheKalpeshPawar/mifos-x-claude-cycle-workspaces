# DTO Registry Index — mifos-x-open-banking

> Reverse-synced 2026-07-28 by `/gap-analysis-project` against the shipped source.
> Extended 2026-07-30 by `/idea-data-flow` with the PISP write contracts (F5 remediation).
> Source: HSBC UK Open Banking AIS v4.0 + PIS v4.0 (OBIE UK standard).

These entries describe the OBIE **wire contract**. Source models the same contract
under a different package layout — `core/network/model/ais/{resource}/` — and maps
each response into a flat domain type in `core/model` before it reaches a ViewModel.
The `source_binding` column names that mapping so the two sides stay traceable.

| Name | Version | Origin | Tier | Consumers | Source binding |
|------|---------|--------|------|-----------|----------------|
| OBActiveOrHistoricCurrencyAndAmount | 1.0.0 | rest | medium | 9 (home, accounts, account-detail, transactions, transaction-detail, statement-detail, direct-debits, standing-orders, scheduled-payments) | `model/ais/*/Amount.kt` |
| OBAccount6 | 1.0.0 | rest | medium | 3 (home, accounts, account-detail) | `model/ais/accounts/Account.kt` → `BankAccount` / `AccountWithBalance` |
| OBCashAccount3 | 1.0.0 | rest | medium | 8 (home, accounts, account-detail, beneficiaries, standing-orders, scheduled-payments, transactions, transaction-detail) | `model/ais/*/CreditorAccount.kt`, `DebtorAccount.kt`; PII |
| OBCashBalance3 | 1.0.0 | rest | medium | 3 (home, accounts, account-detail) | `model/ais/balances/Balance.kt` → `AccountBalance` |
| OBReadAccount6 | 1.0.0 | rest | medium | 3 (home, accounts, account-detail) | `AccountsResponse.kt` / `AccountDetailsResponse.kt` |
| OBReadBalance1 | 1.0.0 | rest | medium | 3 (home, accounts, account-detail) | `BalancesResponse.kt` |
| OBReadBeneficiary5 | 1.0.0 | rest | medium | 1 (beneficiaries) | `BeneficiariesResponse.kt` → `BeneficiaryItem`; PII |
| OBReadConsent1 | 1.0.0 | rest | maximum | 1 (login) | `model/hsbcPermission/request/HSBCCreateConsentRequest.kt` |
| OBReadConsentResponse1 | 1.0.0 | rest | maximum | 4 (login, consent-callback, consent-list, consent-detail) | `model/hsbcPermission/response/HSBCCreateConsentResponse.kt` → `ConsentSummary` |
| OBReadDirectDebit2 | 1.0.0 | rest | medium | 1 (direct-debits) | `DirectDebitsResponse.kt` → `DirectDebitItem` |
| OBReadParty2 | 1.0.0 | rest | maximum | 1 (account-holder) | `model/ais/party/PartyResponse.kt` → `PartyProfile` via `PartyMapper`; PII |
| OBReadParty3 | 1.0.0 | rest | maximum | 0 | `model/ais/parties/PartiesResponse.kt` — **UNCONSUMED**; see note below |
| OBReadProduct2 | 1.0.0 | rest | medium | 1 (product) | `ProductResponse.kt` → `ProductTerms` |
| OBReadScheduledPayment3 | 1.0.0 | rest | medium | 1 (scheduled-payments) | `ScheduledPaymentsResponse.kt` → `ScheduledPaymentItem` |
| OBReadStatement2 | 1.0.0 | rest | medium | 2 (statements, statement-detail) | `StatementsResponse.kt` / `StatementDetailsResponse.kt` → `StatementPeriod` / `StatementDetail` |
| OBReadStandingOrder6 | 1.0.0 | rest | medium | 1 (standing-orders) | `StandingOrdersResponse.kt` → `StandingOrderItem` |
| OBReadTransaction6 | 1.0.0 | rest | medium | 4 (home, transactions, transaction-detail, statement-detail) | `TransactionsResponse.kt` / `StatementTransactionsResponse.kt` → `TransactionsPage`; paginated via Links.Next |
| OBTransaction6 | 1.0.0 | rest | maximum | 4 (home, transactions, transaction-detail, statement-detail) | `model/ais/transactions/Transaction.kt` → `TransactionItem` / `TransactionDetail`; PII |
| OAuthTokenResponse | 1.0.0 | rest | maximum | 1 (consent-callback) | `model/oauth/PsuTokenResponse.kt`, `RefreshTokenResponse.kt` |

## Summary

- **Total DTOs:** 19
- **This run (2026-07-28):** removed=2 (`AtmDisplayItem`, `OBReadATMResponse1` — the atm-locator screen and the HSBC Open Data endpoint are both unimplemented)
- **OBIE AIS v4.0 envelope types:** 14
- **OBIE inner / item types:** 5 (OBAccount6, OBCashAccount3, OBCashBalance3, OBActiveOrHistoricCurrencyAndAmount, OBTransaction6)
- **Client synthetic types:** 0
- **PII-tagged:** OBCashAccount3, OBReadBeneficiary5, OBReadParty2, OBReadParty3, OBTransaction6, OAuthTokenResponse
- **tier=maximum:** OBReadConsent1, OBReadConsentResponse1, OBReadParty2, OBReadParty3, OBTransaction6, OAuthTokenResponse
- **Screens with no API (client-only):** settings, licences, user-onboarding
- **Consumer coverage:** all 20 screens accounted for

## Notes

**OBReadParty3 is registered but unconsumed.** `Aisp.getParties()` exists on the network
client and has a serialization test, but no store, repository or feature calls it. The
account-holder screen reads the singular `/party` endpoint only. Kept in the registry
because the client surface is real; consumer count is honestly 0.

**PISP wire models are deliberately absent from this registry.** `core/network/model/pisp/`
ships a complete domestic + international payment / scheduled-payment / standing-order
request-and-response surface. Nothing consumes it, and `idea-plan.yaml` declares payment
initiation out of scope. Recorded as drift in `idea-plan.yaml#api_surface.out_of_scope_drift`
rather than legitimised here.

## Home-screen OBIE shape coverage

| Required DTO | Registered | Role |
|---|---|---|
| OBReadAccount6 | OBReadAccount6.yaml | Envelope for /accounts — account-switcher chip strip |
| OBAccount6 | OBAccount6.yaml | Item type from OBReadAccount6.Data.Account[] |
| OBCashAccount3 | OBCashAccount3.yaml | Nested account identifier |
| OBReadBalance1 | OBReadBalance1.yaml | Envelope for /accounts/{id}/balances — hero balance card |
| OBCashBalance3 | OBCashBalance3.yaml | Item type from OBReadBalance1.Data.Balance[] |
| OBActiveOrHistoricCurrencyAndAmount | OBActiveOrHistoricCurrencyAndAmount.yaml | Monetary amount |
| OBReadTransaction6 | OBReadTransaction6.yaml | Envelope for /accounts/{id}/transactions — recent-transactions section |
| OBTransaction6 | OBTransaction6.yaml | Item type from OBReadTransaction6.Data.Transaction[] |

All 8 home-screen OBIE shapes registered. ✓

## PISP write contracts (added 2026-07-30, `/idea-data-flow` F5)

These five were referenced by `send-money`, `payment-consent` and `payment-status` but
registered nowhere, which failed RULE-DATA-FLOW-001 F5 on 3 of 23 features. They are the
app's **first write contracts** — every AIS entry above is read-only.

| Name | Version | Origin | Tier | Consumers | Source binding |
|------|---------|--------|------|-----------|----------------|
| OBWriteDomesticConsent4 | 1.0.0 | rest | maximum | 1 (send-money) | `model/pisp/domesticPayment/request/DomesticPaymentConsentRequest.kt` — ships, unconsumed |
| OBWriteDomesticConsentResponse5 | 1.0.0 | rest | maximum | 2 (send-money, payment-consent) | `model/pisp/domesticPayment/response/DomesticPaymentConsentResponse.kt` — ships, unconsumed |
| OBWriteDomestic2 | 1.0.0 | rest | maximum | 1 (send-money) | `model/pisp/domesticPayment/request/DomesticPaymentRequest.kt` — ships, unconsumed |
| OBWriteDomesticResponse5 | 1.0.0 | rest | maximum | 2 (send-money, payment-status) | `model/pisp/domesticPayment/response/DomesticPaymentResponse.kt` — ships, unconsumed |
| OBWriteFundsConfirmationResponse1 | 1.0.0 | rest | high | 1 (send-money) | **not modelled in source** — no funds-confirmation DTO ships |

Two properties distinguish the write contracts from every AIS entry above:

- **`OBWriteDomesticConsent4` and `OBWriteDomestic2` are signed writes.** Both require a
  detached `x-jws-signature` (PS256) and an `x-idempotency-key`. Omitting the signature
  returns `400 U019`. No AIS read needs either header.
- **`OBWriteDomesticResponse5.status` is not a boolean.** A successful submit returns
  `AcceptedSettlementInProcess` — accepted, not settled. Consumers must map it through
  `design-tokens.yaml#semantic.payment_disposition` and must never render in-progress as sent.

### Naming correction 2026-07-30

`screens/account-holder/api.yaml` referenced `PartyResponse`, the source-side class name.
Every other dto ref in the idea-layer — 23 of 24 — uses the OBIE wire name, which is what
this registry keys on. Retargeted to `OBReadParty2`, whose `source_binding` preserves the
link to `PartyResponse.kt`. `OBReadParty2` / `OBReadParty3` also carried `used_by` entries
for `party` and `profile`; `party` was renamed to `account-holder` on 2026-07-28 and
`profile` was deleted, so both were corrected.
