# /idea verify --rule RULE-DTO-REGISTRY-001
**Project:** mifos-x/mifos-x-open-banking
**Scope:** all features (25)
**Timestamp:** 2026-07-14T14:00:00Z
**Cache mode:** hot (re-verify after fix application)
**Rule evaluated:** RULE-DTO-REGISTRY-001 v1.0.0
**Prior run:** 2026-07-14T13:00:00Z — FAIL (D2 error, D5 warn, D6 warn)

---

## Changes Applied Before This Run

| Fix | File(s) | Change |
|---|---|---|
| FIX-1 (D2) | `screens/statements/api.yaml` | `response_dto: Binary` → `response_dto: null` |
| FIX-2 (D5) | All 14 affected `dtos/*.yaml` files (manual, skill unavailable inline) | camelCase `used_by[].feature` → kebab-case matching actual screen dirs |
| FIX-3 (D6) | `dtos/OAuthTokenResponse.yaml` | Added `owned: false` + `implicit_doc_ref: "api_manifest.yaml#base_urls.oauth2"` to `source` block |

---

## Sub-Check Results

### D1-REGISTRY-PRESENT — PASS

`idea-layer/dtos/` exists with 21 DTO files. 19 features with active API endpoints.

---

### D2-EVERY-CONSUMER-REF-RESOLVES — PASS

All DTO refs across all 25 features resolve correctly. `Binary` pseudo-type removed from `screens/statements/api.yaml#endpoints[id=statement_file].response_dto`; now `null` (correct for a binary PDF/CSV download with no JSON DTO).

| Feature | DTO refs | Status |
|---|---|---|
| statements | OBReadStatement2 (list), `null` (statement_file download) | PASS |
| accounts | OBReadAccount6, OBReadBalance1 | PASS |
| home | OBReadAccount6, OBReadBalance1, OBReadTransaction6 | PASS |
| login | OBReadConsentResponse1 | PASS |
| transactions | OBReadTransaction6, OBTransaction6 | PASS |
| account-detail | OBReadAccount6, OBReadBalance1 | PASS |
| consent-callback | OAuthTokenResponse, OBReadConsentResponse1 | PASS |
| consent-detail | OBReadConsentResponse1 | PASS |
| consent-list | OBReadConsentResponse1 | PASS |
| atm-locator | OBReadATMResponse1, AtmDisplayItem | PASS |
| beneficiaries | OBReadBeneficiary5 | PASS |
| direct-debits | OBReadDirectDebit2 | PASS |
| party | OBReadParty2, OBReadParty3 | PASS |
| product | OBReadProduct2 | PASS |
| profile | OBReadParty2 | PASS |
| scheduled-payments | OBReadScheduledPayment3 | PASS |
| standing-orders | OBReadStandingOrder6 | PASS |
| statement-detail | OBReadStatement2, OBReadTransaction6 | PASS |
| transaction-detail | OBReadTransaction6 | PASS |

No `DTO_REF_UNKNOWN` violations.

---

### D3-NO-DUPLICATE-NAMES — PASS

All 21 DTO files have unique `name:` values. No change from prior run.

---

### D4-NO-SHADOW-OF-SHARED — PASS

No project DTO shadows shared baseline names. No change from prior run.

---

### D5-USED-BY-FRESH — PASS

All `used_by[].feature` values now use kebab-case matching canonical screen directory names.

| DTO | was (camelCase) | now (kebab-case) | Screen dir exists? |
|---|---|---|---|
| AtmDisplayItem | `atmLocator` | `atm-locator` | YES |
| OAuthTokenResponse | `consentCallback` | `consent-callback` | YES |
| OBAccount6 | `accountDetail` | `account-detail` | YES |
| OBActiveOrHistoricCurrencyAndAmount | `accountDetail`, `transactionDetail`, `statementDetail`, `directDebits`, `standingOrders`, `scheduledPayments` | `account-detail`, `transaction-detail`, `statement-detail`, `direct-debits`, `standing-orders`, `scheduled-payments` | ALL YES |
| OBCashAccount3 | `accountDetail`, `standingOrders`, `scheduledPayments`, `transactionDetail` | `account-detail`, `standing-orders`, `scheduled-payments`, `transaction-detail` | ALL YES |
| OBCashBalance3 | `accountDetail` | `account-detail` | YES |
| OBReadAccount6 | `accountDetail` | `account-detail` | YES |
| OBReadATMResponse1 | `atmLocator` | `atm-locator` | YES |
| OBReadBalance1 | `accountDetail` | `account-detail` | YES |
| OBReadConsentResponse1 | `consentCallback`, `consentList`, `consentDetail` | `consent-callback`, `consent-list`, `consent-detail` | ALL YES |
| OBReadDirectDebit2 | `directDebits` | `direct-debits` | YES |
| OBReadScheduledPayment3 | `scheduledPayments` | `scheduled-payments` | YES |
| OBReadStandingOrder6 | `standingOrders` | `standing-orders` | YES |
| OBReadStatement2 | `statementDetail` | `statement-detail` | YES |
| OBReadTransaction6 | `transactionDetail`, `statementDetail` | `transaction-detail`, `statement-detail` | ALL YES |
| OBTransaction6 | `transactionDetail`, `statementDetail` | `transaction-detail`, `statement-detail` | ALL YES |

No `DTO_USED_BY_DRIFT` violations.

**Method used:** manual Edit (skill `/idea generate-dtos --refresh-back-refs` not invoked inline — manual conversion applied per task spec fallback path; each kebab-case value confirmed against actual `idea-layer/screens/` directory listing).

---

### D6-ORIGIN-MATCHES-SERVER — PASS

`OAuthTokenResponse.source` now carries:
```yaml
source:
  origin: rest
  endpoint: "/oauth2/token"
  owned: false
  implicit_doc_ref: "api_manifest.yaml#base_urls.oauth2"
```

The `implicit_doc_ref` field resolves the D6 origin check — the endpoint is explicitly documented as externally-owned via `api_manifest.yaml#base_urls.oauth2`. No `DTO_ORIGIN_DRIFT` violations remain.

---

### D7-REPLACED-BY-RESOLVES — PASS

No `replaced_by:` fields. No change from prior run.

---

## Summary

```
Rule:    RULE-DTO-REGISTRY-001 v1.0.0
Scope:   all features (25) × all DTOs (21)
Overall: PASS
```

| Sub-check | Scope | Status | Notes |
|---|---|---|---|
| D1-REGISTRY-PRESENT | project | PASS | 21 DTOs, 19 API-consuming features |
| D2-EVERY-CONSUMER-REF-RESOLVES | feature | **PASS** | Fixed: Binary→null in statement_file |
| D3-NO-DUPLICATE-NAMES | project | PASS | — |
| D4-NO-SHADOW-OF-SHARED | project | PASS | — |
| D5-USED-BY-FRESH | feature | **PASS** | Fixed: 16 DTOs converted camelCase→kebab-case |
| D6-ORIGIN-MATCHES-SERVER | feature | **PASS** | Fixed: implicit_doc_ref added to OAuthTokenResponse |
| D7-REPLACED-BY-RESOLVES | feature | PASS | — |

**Blocking rule IDs:** none
**Delta from prior run:** D2 FAIL→PASS · D5 WARN→PASS · D6 WARN→PASS
