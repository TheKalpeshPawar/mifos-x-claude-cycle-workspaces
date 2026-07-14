# /idea verify --rule RULE-DTO-REGISTRY-001
**Project:** mifos-x/mifos-x-open-banking
**Scope:** all features (25)
**Timestamp:** 2026-07-14T15:00:00Z
**Cache mode:** cold (full re-evaluation after prior session wrote incorrect D6 result)
**Rule evaluated:** RULE-DTO-REGISTRY-001 v1.0.0 (note: invoked as `RULE-DTO-REGISTRY-0017` — typo for canonical `RULE-DTO-REGISTRY-001`; evaluated against canonical rule)
**Prior run:** 2026-07-14T14:00:00Z — claimed PASS but incorrectly cleared D6 for OBReadATMResponse1

---

## Prior Session State (already applied, carried forward)

The T14:00 session applied three fixes before declaring PASS:

| Fix | File | Change |
|---|---|---|
| FIX-1 (D2) | `screens/statements/api.yaml` | `response_dto: Binary` → `response_dto: null` |
| FIX-2 (D5) | 16 `dtos/*.yaml` files | `used_by[].feature` camelCase → kebab-case |
| FIX-3 (D6 partial) | `dtos/OAuthTokenResponse.yaml` | Added `owned: false` + `implicit_doc_ref: "api_manifest.yaml#base_urls.oauth2"` |

FIX-3 resolves OAuthTokenResponse's D6 check. However, `OBReadATMResponse1` was not addressed and retains a D6 violation.

---

## Sub-Check Results

### D1-REGISTRY-PRESENT — PASS

`idea-layer/dtos/` has 21 files. 19 features with non-empty `endpoints:` in api.yaml. Quorum met.

---

### D2-EVERY-CONSUMER-REF-RESOLVES — PASS

All structured `response_dto:`, `request_dto:`, and `vm_mapping.dto:` values across all 25 features resolve to registry entries. FIX-1 from prior session removed the `Binary` pseudo-type from `screens/statements/api.yaml`.

| Feature | DTO refs | Status |
|---|---|---|
| home | OBReadAccount6, OBReadBalance1, OBReadTransaction6 | PASS |
| accounts | OBReadAccount6, OBReadBalance1 | PASS |
| account-detail | OBReadAccount6, OBReadBalance1 | PASS |
| transactions | OBReadTransaction6, OBTransaction6 | PASS |
| transaction-detail | OBReadTransaction6 | PASS |
| statements | OBReadStatement2, null (binary download) | PASS |
| statement-detail | OBReadStatement2, OBReadTransaction6 | PASS |
| beneficiaries | OBReadBeneficiary5 | PASS |
| standing-orders | OBReadStandingOrder6 | PASS |
| direct-debits | OBReadDirectDebit2 | PASS |
| scheduled-payments | OBReadScheduledPayment3 | PASS |
| party | OBReadParty2, OBReadParty3 | PASS |
| profile | OBReadParty2 | PASS |
| product | OBReadProduct2 | PASS |
| atm-locator | OBReadATMResponse1, AtmDisplayItem | PASS |
| consent-list | OBReadConsentResponse1 | PASS |
| consent-detail | OBReadConsentResponse1 | PASS |
| consent-callback | OAuthTokenResponse, OBReadConsentResponse1 | PASS |
| login | OBReadConsentResponse1, OBReadConsent1 | PASS |
| pfm-dashboard | (no endpoints) | SKIP |
| spending-by-category | (no endpoints) | SKIP |
| settings | (no endpoints) | SKIP |
| budgets | (no endpoints) | SKIP |
| recurring-subscriptions | (no endpoints) | SKIP |
| user-onboarding | (no endpoints) | SKIP |

`DTO_REF_UNKNOWN` violations: **0**

---

### D3-NO-DUPLICATE-NAMES — PASS

21 files × 21 unique `name:` values. No duplicates.

---

### D4-NO-SHADOW-OF-SHARED — PASS

Shared baselines (ErrorEnvelope, PaginationCursor, PaginatedEnvelope, AuthSession) — none shadowed by any of the 21 project DTOs.

---

### D5-USED-BY-FRESH — PASS

All direct consumer references (api.yaml `response_dto:`/`request_dto:`/`vm_mapping.dto:`) confirmed present in the corresponding DTO's `used_by[]`. FIX-2 from prior session converted 16 DTOs from camelCase to kebab-case feature names.

No `DTO_USED_BY_DRIFT` violations for any direct api.yaml reference.

---

### D6-ORIGIN-MATCHES-SERVER — **FAIL** (1 error)

**Server spec:** `idea-layer/server/apis/account-information.yaml` (OBIE AIS v4.0, `owned: false`)
**Evaluated:** all 21 DTOs with `source.origin: rest`

| DTO | Endpoint | In server spec? | owned:false? | implicit_doc_ref? | Verdict |
|---|---|---|---|---|---|
| OBReadAccount6 | `/accounts` | YES | — | — | PASS |
| OBAccount6 | `/accounts/{AccountId}` | YES | — | — | PASS |
| OBCashAccount3 | `/accounts/{AccountId}` | YES | — | — | PASS |
| OBActiveOrHistoricCurrencyAndAmount | `/accounts/{AccountId}/balances` | YES | — | — | PASS |
| OBCashBalance3 | `/accounts/{AccountId}/balances` | YES | — | — | PASS |
| OBReadBalance1 | `/accounts/{AccountId}/balances` | YES | — | — | PASS |
| OBReadBalance1 | `/accounts/{AccountId}/balances` | YES | — | — | PASS |
| OBReadTransaction6 | `/accounts/{AccountId}/transactions` | YES | — | — | PASS |
| OBTransaction6 | `/accounts/{AccountId}/transactions` | YES | — | — | PASS |
| OBReadStatement2 | `/accounts/{AccountId}/statements` | YES | — | — | PASS |
| OBReadBeneficiary5 | `/accounts/{AccountId}/beneficiaries` | YES | — | — | PASS |
| OBReadStandingOrder6 | `/accounts/{AccountId}/standing-orders` | YES | — | — | PASS |
| OBReadDirectDebit2 | `/accounts/{AccountId}/direct-debits` | YES | — | — | PASS |
| OBReadScheduledPayment3 | `/accounts/{AccountId}/scheduled-payments` | YES | — | — | PASS |
| OBReadParty2 | `/accounts/{AccountId}/party` | YES | — | — | PASS |
| OBReadParty3 | `/accounts/{AccountId}/parties` | YES | — | — | PASS |
| OBReadProduct2 | `/accounts/{AccountId}/product` | YES | — | — | PASS |
| OBReadConsent1 | `/account-access-consents` | YES | — | — | PASS |
| OBReadConsentResponse1 | `/account-access-consents/{ConsentId}` | YES | — | — | PASS |
| OAuthTokenResponse | `/oauth2/token` | NO | **YES** | `api_manifest.yaml#base_urls.oauth2` | PASS (FIX-3) |
| **OBReadATMResponse1** | **/atms** | **NO** | **NO** | **NONE** | **FAIL** |
| AtmDisplayItem | synthetic (vm_mapping) | — | — | — | SKIP (no origin:rest) |

**Violation:**

```
error_code: DTO_ORIGIN_DRIFT
dto:        OBReadATMResponse1
endpoint:   /atms
found_in:   idea-layer/server/apis/account-information.yaml → ABSENT
owned_flag: missing (no source.owned: false)
doc_ref:    none
consumer:   atm-locator (api_id: atms)
context:    HSBC ATM Open Data public API (base: https://api.hsbc.com/v2.0/uk/open-banking)
            — separate product from OBIE AIS; unauthenticated; not OBIE-spec'd
```

**Suggested fix (choose one):**

Option A — Add `owned: false` + `implicit_doc_ref`:
```yaml
# idea-layer/dtos/OBReadATMResponse1.yaml
source:
  origin: rest
  endpoint: "/atms"
  owned: false
  implicit_doc_ref: "api_manifest.yaml#base_urls.atm_open_data"
```
Then add `base_urls.atm_open_data: "https://api.hsbc.com/v2.0/uk/open-banking"` to `idea-layer/server/api_manifest.yaml`.

Option B — Add an ATM Open Data spec file:
```
idea-layer/server/apis/atm-open-data.yaml
```
Declaring the `GET /atms` operation with the public base URL.

Option A is cheaper; Option B is more rigorous for multi-developer discovery.

---

### D7-REPLACED-BY-RESOLVES — PASS

No `replaced_by:` declarations in any of the 21 DTOs. No check required.

---

## Summary

```
Rule:    RULE-DTO-REGISTRY-001 v1.0.0
Scope:   all features (25) × all DTOs (21)
Overall: FAIL
```

| Sub-check | Scope | Status | Violations |
|---|---|---|---|
| D1-REGISTRY-PRESENT | project | ✓ PASS | — |
| D2-EVERY-CONSUMER-REF-RESOLVES | per-feature | ✓ PASS | 0 |
| D3-NO-DUPLICATE-NAMES | project | ✓ PASS | 0 |
| D4-NO-SHADOW-OF-SHARED | project | ✓ PASS | 0 |
| D5-USED-BY-FRESH | per-feature | ✓ PASS | 0 |
| D6-ORIGIN-MATCHES-SERVER | per-DTO | ✗ **FAIL** | 1 (OBReadATMResponse1) |
| D7-REPLACED-BY-RESOLVES | per-feature | ✓ PASS | 0 |

**Blocking rule IDs:** `RULE-DTO-REGISTRY-001` (D6)
**Correction from T14 run:** Prior session declared D6 PASS after fixing OAuthTokenResponse only. OBReadATMResponse1 `/atms` violation was missed; this run surfaces it.
