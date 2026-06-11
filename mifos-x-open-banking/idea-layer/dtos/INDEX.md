# DTO Registry — mifos-x-open-banking

> Auto-maintained by `/idea generate-dtos`. 71 DTOs registered.
> Last run: 2026-06-11 — MIGRATION OBP → HSBC. Full rebuild: the 68 OBP-shaped DTOs were replaced with
> the OBIE UK Open Banking Read/Write v4.0 object model (sourced from `server/apis/*.yaml`).
> Exact consumer counts + PII flags live in each `{Name}.yaml`; run `/idea generate-dtos --refresh-back-refs`
> to recompute the Consumers column after the screens re-export.

| Name | Version | Origin | Group |
|------|---------|--------|-------|
| OBActiveOrHistoricCurrencyAndAmount | 1.0.0 | rest | shared |
| OBAtm | 1.0.0 | rest | open-data |
| OBBCAProduct | 1.0.0 | rest | open-data |
| OBBranch | 1.0.0 | rest | open-data |
| OBBranchAndFinancialInstitutionIdentification | 1.0.0 | rest | shared |
| OBCashAccount6 | 1.0.0 | rest | shared |
| OBClientRegistration1 | 1.0.0 | rest | auth/dcr |
| OBClientRegistrationResponse1 | 1.0.0 | rest | auth/dcr |
| OBDomestic2 | 1.0.0 | rest | shared (pisp) |
| OBDomesticScheduled2 | 1.0.0 | rest | shared (pisp) |
| OBDomesticStandingOrder3 | 1.0.0 | rest | shared (pisp) |
| OBDomesticVRPConsentRequest | 1.0.0 | rest | vrp |
| OBDomesticVRPConsentResponse | 1.0.0 | rest | vrp |
| OBDomesticVRPControlParameters | 1.0.0 | rest | vrp |
| OBDomesticVRPRequest | 1.0.0 | rest | vrp |
| OBDomesticVRPResponse | 1.0.0 | rest | vrp |
| OBEventPolling1 | 1.0.0 | rest | events |
| OBEventPollingResponse1 | 1.0.0 | rest | events |
| OBEventSubscription1 | 1.0.0 | rest | events |
| OBEventSubscriptionResponse1 | 1.0.0 | rest | events |
| OBExchangeRate2 | 1.0.0 | rest | shared (pisp-intl) |
| OBFundsAvailableResult1 | 1.0.0 | rest | shared |
| OBFundsConfirmation1 | 1.0.0 | rest | cbpii |
| OBFundsConfirmationConsent1 | 1.0.0 | rest | cbpii |
| OBFundsConfirmationConsentResponse1 | 1.0.0 | rest | cbpii |
| OBFundsConfirmationResponse1 | 1.0.0 | rest | cbpii |
| OBOpenDataResponse | 1.0.0 | rest | open-data |
| OBPCAProduct | 1.0.0 | rest | open-data |
| OBReadAccount6 | 1.0.0 | rest | ais |
| OBReadBalance1 | 1.0.0 | rest | ais |
| OBReadBeneficiary5 | 1.0.0 | rest | ais |
| OBReadConsent1 | 1.0.0 | rest | ais |
| OBReadConsentResponse1 | 1.0.0 | rest | ais |
| OBReadDirectDebit2 | 1.0.0 | rest | ais |
| OBReadParty3 | 1.0.0 | rest | ais |
| OBReadProduct2 | 1.0.0 | rest | ais |
| OBReadScheduledPayment3 | 1.0.0 | rest | ais |
| OBReadStandingOrder6 | 1.0.0 | rest | ais |
| OBReadStatement2 | 1.0.0 | rest | ais |
| OBReadTransaction6 | 1.0.0 | rest | ais |
| OBRisk1 | 1.0.0 | rest | shared (pisp) |
| OBVRPFundsConfirmationResponse | 1.0.0 | rest | vrp |
| OBWriteDomestic2 | 1.0.0 | rest | pisp-domestic |
| OBWriteDomesticConsent4 | 1.0.0 | rest | pisp-domestic |
| OBWriteDomesticConsentResponse5 | 1.0.0 | rest | pisp-domestic |
| OBWriteDomesticResponse5 | 1.0.0 | rest | pisp-domestic |
| OBWriteDomesticScheduled2 | 1.0.0 | rest | pisp-domestic-scheduled |
| OBWriteDomesticScheduledConsent4 | 1.0.0 | rest | pisp-domestic-scheduled |
| OBWriteDomesticScheduledConsentResponse5 | 1.0.0 | rest | pisp-domestic-scheduled |
| OBWriteDomesticScheduledResponse5 | 1.0.0 | rest | pisp-domestic-scheduled |
| OBWriteDomesticStandingOrder3 | 1.0.0 | rest | pisp-domestic-standing-order |
| OBWriteDomesticStandingOrderConsent5 | 1.0.0 | rest | pisp-domestic-standing-order |
| OBWriteDomesticStandingOrderConsentResponse6 | 1.0.0 | rest | pisp-domestic-standing-order |
| OBWriteDomesticStandingOrderResponse6 | 1.0.0 | rest | pisp-domestic-standing-order |
| OBWriteFile2 | 1.0.0 | rest | pisp-file |
| OBWriteFileConsent3 | 1.0.0 | rest | pisp-file |
| OBWriteFileConsentResponse4 | 1.0.0 | rest | pisp-file |
| OBWriteFileResponse3 | 1.0.0 | rest | pisp-file |
| OBWriteFundsConfirmationResponse1 | 1.0.0 | rest | pisp-domestic |
| OBWriteInternational3 | 1.0.0 | rest | pisp-international |
| OBWriteInternationalConsent5 | 1.0.0 | rest | pisp-international |
| OBWriteInternationalConsentResponse6 | 1.0.0 | rest | pisp-international |
| OBWriteInternationalResponse5 | 1.0.0 | rest | pisp-international |
| OBWriteInternationalScheduled3 | 1.0.0 | rest | pisp-international-scheduled |
| OBWriteInternationalScheduledConsent5 | 1.0.0 | rest | pisp-international-scheduled |
| OBWriteInternationalScheduledConsentResponse6 | 1.0.0 | rest | pisp-international-scheduled |
| OBWriteInternationalScheduledResponse6 | 1.0.0 | rest | pisp-international-scheduled |
| OBWriteInternationalStandingOrder4 | 1.0.0 | rest | pisp-international-standing-order |
| OBWriteInternationalStandingOrderConsent6 | 1.0.0 | rest | pisp-international-standing-order |
| OBWriteInternationalStandingOrderConsentResponse7 | 1.0.0 | rest | pisp-international-standing-order |
| OBWriteInternationalStandingOrderResponse7 | 1.0.0 | rest | pisp-international-standing-order |
