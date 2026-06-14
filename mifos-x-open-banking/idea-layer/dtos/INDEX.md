# DTO Registry — mifos-x-open-banking

> Auto-maintained by `/idea generate-dtos`. 72 DTOs registered.
> Last run: 2026-06-12 — `--refresh-back-refs` + OBTokenResponse registration + DTO-name drift reconciliation (OBP→HSBC OBIE).
> Rebuilt `used_by[]` back-references across all 39 screens from current `api.yaml` + `data-flow.yaml`.
> Exact PII flags live in each `{Name}.yaml`; shapes unchanged from the 2026-06-11 migration.

| Name | Version | Origin | Group | Consumers |
|------|---------|--------|-------|-----------|
| OBActiveOrHistoricCurrencyAndAmount | 1.0.0 | rest | shared | 25 |
| OBAtm | 1.0.0 | rest | open-data | 2 |
| OBBCAProduct | 1.0.0 | rest | open-data | 2 |
| OBBranch | 1.0.0 | rest | open-data | 2 |
| OBBranchAndFinancialInstitutionIdentification | 1.0.0 | rest | shared | 2 |
| OBCashAccount6 | 1.0.0 | rest | shared | 19 |
| OBClientRegistration1 | 1.0.0 | rest | auth/dcr | 3 |
| OBClientRegistrationResponse1 | 1.0.0 | rest | auth/dcr | 3 |
| OBDomestic2 | 1.0.0 | rest | shared (pisp) | 3 |
| OBDomesticScheduled2 | 1.0.0 | rest | shared (pisp) | 1 |
| OBDomesticStandingOrder3 | 1.0.0 | rest | shared (pisp) | 2 |
| OBDomesticVRPConsentRequest | 1.0.0 | rest | vrp | 1 |
| OBDomesticVRPConsentResponse | 1.0.0 | rest | vrp | 1 |
| OBDomesticVRPControlParameters | 1.0.0 | rest | vrp | 1 |
| OBDomesticVRPRequest | 1.0.0 | rest | vrp | 1 |
| OBDomesticVRPResponse | 1.0.0 | rest | vrp | 1 |
| OBEventPolling1 | 1.0.0 | rest | events | 2 |
| OBEventPollingResponse1 | 1.0.0 | rest | events | 2 |
| OBEventSubscription1 | 1.0.0 | rest | events | 2 |
| OBEventSubscriptionResponse1 | 1.0.0 | rest | events | 2 |
| OBExchangeRate2 | 1.0.0 | rest | shared (pisp-intl) | 2 |
| OBFundsAvailableResult1 | 1.0.0 | rest | shared | 2 |
| OBFundsConfirmation1 | 1.0.0 | rest | cbpii | 2 |
| OBFundsConfirmationConsent1 | 1.0.0 | rest | cbpii | 2 |
| OBFundsConfirmationConsentResponse1 | 1.0.0 | rest | cbpii | 2 |
| OBFundsConfirmationResponse1 | 1.0.0 | rest | cbpii | 2 |
| OBOpenDataResponse | 1.0.0 | rest | open-data | 3 |
| OBPCAProduct | 1.0.0 | rest | open-data | 2 |
| OBReadAccount6 | 1.0.0 | rest | ais | 9 |
| OBReadBalance1 | 1.0.0 | rest | ais | 7 |
| OBReadBeneficiary5 | 1.0.0 | rest | ais | 3 |
| OBReadConsent1 | 1.0.0 | rest | ais | 1 |
| OBReadConsentResponse1 | 1.0.0 | rest | ais | 4 |
| OBReadDirectDebit2 | 1.0.0 | rest | ais | 2 |
| OBReadParty3 | 1.0.0 | rest | ais | 3 |
| OBReadProduct2 | 1.0.0 | rest | ais | 1 |
| OBReadScheduledPayment3 | 1.0.0 | rest | ais | 1 |
| OBReadStandingOrder6 | 1.0.0 | rest | ais | 2 |
| OBReadStatement2 | 1.0.0 | rest | ais | 1 |
| OBReadTransaction6 | 1.0.0 | rest | ais | 7 |
| OBRisk1 | 1.0.0 | rest | shared (pisp) | 10 |
| OBTokenResponse | 1.0.0 | rest | auth/oauth | 2 |
| OBVRPFundsConfirmationResponse | 1.0.0 | rest | vrp | 1 |
| OBWriteDomestic2 | 1.0.0 | rest | pisp-domestic | 1 |
| OBWriteDomesticConsent4 | 1.0.0 | rest | pisp-domestic | 2 |
| OBWriteDomesticConsentResponse5 | 1.0.0 | rest | pisp-domestic | 2 |
| OBWriteDomesticResponse5 | 1.0.0 | rest | pisp-domestic | 2 |
| OBWriteDomesticScheduled2 | 1.0.0 | rest | pisp-domestic-scheduled | 1 |
| OBWriteDomesticScheduledConsent4 | 1.0.0 | rest | pisp-domestic-scheduled | 1 |
| OBWriteDomesticScheduledConsentResponse5 | 1.0.0 | rest | pisp-domestic-scheduled | 1 |
| OBWriteDomesticScheduledResponse5 | 1.0.0 | rest | pisp-domestic-scheduled | 1 |
| OBWriteDomesticStandingOrder3 | 1.0.0 | rest | pisp-domestic-standing-order | 2 |
| OBWriteDomesticStandingOrderConsent5 | 1.0.0 | rest | pisp-domestic-standing-order | 2 |
| OBWriteDomesticStandingOrderConsentResponse6 | 1.0.0 | rest | pisp-domestic-standing-order | 2 |
| OBWriteDomesticStandingOrderResponse6 | 1.0.0 | rest | pisp-domestic-standing-order | 2 |
| OBWriteFile2 | 1.0.0 | rest | pisp-file | 1 |
| OBWriteFileConsent3 | 1.0.0 | rest | pisp-file | 1 |
| OBWriteFileConsentResponse4 | 1.0.0 | rest | pisp-file | 1 |
| OBWriteFileResponse3 | 1.0.0 | rest | pisp-file | 1 |
| OBWriteFundsConfirmationResponse1 | 1.0.0 | rest | pisp-domestic | 1 |
| OBWriteInternational3 | 1.0.0 | rest | pisp-international | 1 |
| OBWriteInternationalConsent5 | 1.0.0 | rest | pisp-international | 1 |
| OBWriteInternationalConsentResponse6 | 1.0.0 | rest | pisp-international | 1 |
| OBWriteInternationalResponse5 | 1.0.0 | rest | pisp-international | 1 |
| OBWriteInternationalScheduled3 | 1.0.0 | rest | pisp-international-scheduled | 1 |
| OBWriteInternationalScheduledConsent5 | 1.0.0 | rest | pisp-international-scheduled | 1 |
| OBWriteInternationalScheduledConsentResponse6 | 1.0.0 | rest | pisp-international-scheduled | 1 |
| OBWriteInternationalScheduledResponse6 | 1.0.0 | rest | pisp-international-scheduled | 1 |
| OBWriteInternationalStandingOrder4 | 1.0.0 | rest | pisp-international-standing-order | 1 |
| OBWriteInternationalStandingOrderConsent6 | 1.0.0 | rest | pisp-international-standing-order | 1 |
| OBWriteInternationalStandingOrderConsentResponse7 | 1.0.0 | rest | pisp-international-standing-order | 1 |
| OBWriteInternationalStandingOrderResponse7 | 1.0.0 | rest | pisp-international-standing-order | 1 |
