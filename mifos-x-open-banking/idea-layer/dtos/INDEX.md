# DTO Registry Index — mifos-x-open-banking

> Auto-maintained by `/idea generate-dtos`. Last generated: 2026-07-14.
> Source: HSBC UK Open Banking AIS v4.0 + HSBC Open Data public API.
> Standard: OBIE (Open Banking Implementation Entity) UK.

| Name | Version | Origin | Tier | Consumers | Notes |
|------|---------|--------|------|-----------|-------|
| AtmDisplayItem | 1.0.0 | synthetic | medium | 1 (atmLocator) | ViewModel projection from OBReadATMResponse1 |
| OBActiveOrHistoricCurrencyAndAmount | 1.0.0 | rest | medium | 9 (home, accounts, accountDetail, transactions, transactionDetail, statementDetail, directDebits, standingOrders, scheduledPayments) | Shared monetary amount type used across all resource types |
| OBAccount6 | 1.0.0 | rest | medium | 3 (home, accounts, accountDetail) | Account record item extracted from OBReadAccount6 |
| OBCashAccount3 | 1.0.0 | rest | medium | 8 (home, accounts, accountDetail, beneficiaries, standingOrders, scheduledPayments, transactions, transactionDetail) | Account identification scheme; PII |
| OBCashBalance3 | 1.0.0 | rest | medium | 3 (home, accounts, accountDetail) | Balance record item extracted from OBReadBalance1 |
| OBReadAccount6 | 1.0.0 | rest | medium | 3 (home, accounts, accountDetail) | Envelope — GET /accounts, GET /accounts/{AccountId} |
| OBReadATMResponse1 | 1.0.0 | rest | medium | 1 (atmLocator) | HSBC Open Data public endpoint; no auth |
| OBReadBalance1 | 1.0.0 | rest | medium | 3 (home, accounts, accountDetail) | Envelope — GET /accounts/{AccountId}/balances |
| OBReadBeneficiary5 | 1.0.0 | rest | medium | 1 (beneficiaries) | Envelope — GET /accounts/{AccountId}/beneficiaries; PII |
| OBReadConsent1 | 1.0.0 | rest | maximum | 1 (login) | Request body for POST /account-access-consents |
| OBReadConsentResponse1 | 1.0.0 | rest | maximum | 4 (login, consentCallback, consentList, consentDetail) | Consent resource; status lifecycle |
| OBReadDirectDebit2 | 1.0.0 | rest | medium | 1 (directDebits) | Envelope — GET /accounts/{AccountId}/direct-debits |
| OBReadParty2 | 1.0.0 | rest | maximum | 2 (party, profile) | Envelope — GET /accounts/{AccountId}/party; PII |
| OBReadParty3 | 1.0.0 | rest | maximum | 1 (party) | Envelope — GET /accounts/{AccountId}/parties; PII |
| OBReadProduct2 | 1.0.0 | rest | medium | 1 (product) | Envelope — GET /accounts/{AccountId}/product |
| OBReadScheduledPayment3 | 1.0.0 | rest | medium | 1 (scheduledPayments) | Envelope — GET /accounts/{AccountId}/scheduled-payments |
| OBReadStatement2 | 1.0.0 | rest | medium | 2 (statements, statementDetail) | Envelope — GET .../statements[/{StatementId}] |
| OBReadStandingOrder6 | 1.0.0 | rest | medium | 1 (standingOrders) | Envelope — GET /accounts/{AccountId}/standing-orders |
| OBReadTransaction6 | 1.0.0 | rest | medium | 4 (home, transactions, transactionDetail, statementDetail) | Envelope — GET .../transactions; paginated via Links.Next |
| OBTransaction6 | 1.0.0 | rest | maximum | 4 (home, transactions, transactionDetail, statementDetail) | Transaction record item; PII on creditor/debtor accounts |
| OAuthTokenResponse | 1.0.0 | rest | maximum | 1 (consentCallback) | FAPI-1.0-Advanced token exchange response |

## Summary

- **Total DTOs:** 21
- **This run (2026-07-14):** new=0 / removed=1 (OBReadOffer1 — offers capability dropped) / unchanged=21 — all api.yaml files reconcile cleanly
- **OBIE AIS v4.0 envelope types:** 15
- **OBIE inner / item types:** 5 (OBAccount6, OBCashAccount3, OBCashBalance3, OBActiveOrHistoricCurrencyAndAmount, OBTransaction6)
- **Client synthetic types:** 1 (AtmDisplayItem)
- **PII-tagged DTOs:** OBCashAccount3, OBReadBeneficiary5, OBReadParty2, OBReadParty3, OBTransaction6, OAuthTokenResponse
- **tier=maximum (auth/payment-critical):** OBReadConsent1, OBReadConsentResponse1, OBReadParty2, OBReadParty3, OBTransaction6, OAuthTokenResponse
- **Screens with no API (client-only, no DTOs):** budgets, pfm-dashboard, recurring-subscriptions, settings, spending-by-category, user-onboarding
- **Consumer coverage:** all 25 screens accounted for

## Home-screen OBIE shape coverage (explicitly required)

| Required DTO | Registered | Role |
|---|---|---|
| OBReadAccount6 | OBReadAccount6.yaml | Envelope for /accounts — account-switcher chip strip |
| OBAccount6 | OBAccount6.yaml | Item type from OBReadAccount6.Data.Account[] |
| OBCashAccount3 | OBCashAccount3.yaml | Nested account identifier in OBAccount6.Account[] |
| OBReadBalance1 | OBReadBalance1.yaml | Envelope for /accounts/{id}/balances — hero balance |
| OBCashBalance3 | OBCashBalance3.yaml | Item type from OBReadBalance1.Data.Balance[] |
| OBActiveOrHistoricCurrencyAndAmount | OBActiveOrHistoricCurrencyAndAmount.yaml | Monetary amount in OBCashBalance3.Amount and OBTransaction6.Amount |
| OBReadTransaction6 | OBReadTransaction6.yaml | Envelope for /accounts/{id}/transactions — recent-transactions section |
| OBTransaction6 | OBTransaction6.yaml | Item type from OBReadTransaction6.Data.Transaction[] |

All 8 home-screen OBIE shapes registered. ✓
