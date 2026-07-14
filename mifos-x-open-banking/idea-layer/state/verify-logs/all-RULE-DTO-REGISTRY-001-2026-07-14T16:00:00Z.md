# /idea verify --rule RULE-DTO-REGISTRY-001

**Project:** mifos-x/mifos-x-open-banking  
**Run at:** 2026-07-14T16:00:00Z  
**Scope:** ALL features (25)  
**Rule:** RULE-DTO-REGISTRY-001 — DTO Registry: Every DTO Ref Must Resolve  
**Overall:** PASS

---

## Sub-check Matrix

| Sub-check | Scope | Status | Notes |
|-----------|-------|--------|-------|
| D1-REGISTRY-PRESENT | project | PASS | 21 DTOs in idea-layer/dtos/; 15+ has_api features |
| D2-EVERY-CONSUMER-REF-RESOLVES | per-feature | PASS | 0 violations across 25 features; all response_dto/request_dto refs resolve |
| D3-NO-DUPLICATE-NAMES | project | PASS | 21 unique names; no collision |
| D4-NO-SHADOW-OF-SHARED | project | PASS | No project DTO shadows ErrorEnvelope/PaginationCursor/PaginatedEnvelope/AuthSession |
| D5-USED-BY-FRESH | per-feature | PASS (warn) | used_by[] consistent; prior T14:00 run fixed 16 back-refs |
| D6-ORIGIN-MATCHES-SERVER | per-feature | **PASS** (was FAIL) | See D6 resolution below |
| D7-REPLACED-BY-RESOLVES | per-feature | PASS | No replaced_by declarations in any DTO |

---

## D6 Resolution: OBReadATMResponse1

**Prior state (T15:00):** FAIL — `error_code: DTO_ORIGIN_DRIFT`

OBReadATMResponse1 declared `source.origin: rest, endpoint: "/atms"` but `/atms`
was absent from all files under `idea-layer/server/apis/`. The only server spec
was `account-information.yaml` (OBIE AIS v4.0), which does not include the Open
Data ATM endpoint (separate, unauthenticated product).

**Fix applied:** `idea-layer/server/apis/open-data.yaml` (API-002) was added,
documenting the HSBC Open Data API (base: https://api.hsbc.com/open-banking/v2.2).
It declares:

```yaml
flows:
  reference-data:
    endpoints:
      - id: atms
        method: GET
        path: "/atms"
        response_dto: OBReadATMResponse1
        consumers: [atm-locator]
```

D6 predicate: `OBReadATMResponse1.source.endpoint ("/atms")` matches
`server/apis/open-data.yaml#flows.reference-data.endpoints[id=atms].path` → **PASS**.

OBReadATMResponse1.yaml already had `owned: false`; no DTO file edit was required.
`api_manifest.yaml` already cross-references API-002 via `related_apis[id=API-002]`.

---

## D6 No-Regression: OAuthTokenResponse

`OAuthTokenResponse` declares `source.origin: rest, endpoint: "/oauth2/token",
owned: false, implicit_doc_ref: "api_manifest.yaml#base_urls.oauth2"`.

Status: **PASS** — unchanged from T14:00 run. The `owned: false` + `implicit_doc_ref`
linkage to `api_manifest.yaml#base_urls.oauth2` ("https://sandbox.ob.hsbc.co.uk/mock/obie/open-banking/v1.1/oauth2")
provides documented server-side provenance without requiring an explicit path entry
in server/apis/. No regression.

---

## D2 Detail: All Consumer Refs Resolve

Features with DTO refs scanned:

| Feature | DTOs referenced | Resolved |
|---------|----------------|---------|
| atm-locator | OBReadATMResponse1, AtmDisplayItem | ✓ both exist |
| login | OBReadConsent1, OBReadConsentResponse1 | ✓ |
| consent-callback | OAuthTokenResponse, OBReadConsentResponse1 | ✓ |
| home | OBReadAccount6, OBReadBalance1, OBReadTransaction6 | ✓ |
| accounts | OBReadAccount6, OBReadBalance1 | ✓ |
| account-detail | OBReadAccount6, OBReadBalance1 | ✓ |
| transactions | OBReadTransaction6 | ✓ |
| beneficiaries | OBReadBeneficiary5 | ✓ |
| standing-orders | OBReadStandingOrder6 | ✓ |
| direct-debits | OBReadDirectDebit2 | ✓ |
| scheduled-payments | OBReadScheduledPayment3 | ✓ |
| statements | OBReadStatement2 | ✓ (`null` on statement-file is not a DTO ref) |
| statement-detail | OBReadStatement2, OBReadTransaction6 | ✓ |
| product | OBReadProduct2 | ✓ |
| party | OBReadParty2, OBReadParty3 | ✓ |
| profile | OBReadParty2 | ✓ |
| consent-detail | OBReadConsentResponse1 | ✓ |
| consent-list | OBReadConsentResponse1 | ✓ |
| pfm-dashboard | (no api.yaml DTO refs) | n/a |
| budgets | (no api.yaml DTO refs) | n/a |
| spending-by-category | (no api.yaml DTO refs) | n/a |
| recurring-subscriptions | (no api.yaml DTO refs) | n/a |
| user-onboarding | (no api.yaml DTO refs) | n/a |
| settings | (no api.yaml DTO refs) | n/a |
| transaction-detail | (inlined from transactions) | n/a |

**Violations:** 0

---

## D4 Detail: Shared Baseline Names

Shared baseline (`templates/shared/common-dtos.yaml`):
- ErrorEnvelope, PaginationCursor, PaginatedEnvelope, AuthSession

Project registry names (21):
AtmDisplayItem, OAuthTokenResponse, OBAccount6, OBActiveOrHistoricCurrencyAndAmount,
OBCashAccount3, OBCashBalance3, OBReadAccount6, OBReadATMResponse1, OBReadBalance1,
OBReadBeneficiary5, OBReadConsent1, OBReadConsentResponse1, OBReadDirectDebit2,
OBReadParty2, OBReadParty3, OBReadProduct2, OBReadScheduledPayment3,
OBReadStandingOrder6, OBReadStatement2, OBReadTransaction6, OBTransaction6

Intersection: **0** — no shadow.

---

## Summary

```
RULE-DTO-REGISTRY-001
  D1  PASS  registry present (21 DTOs)
  D2  PASS  0 unresolved refs
  D3  PASS  0 duplicates
  D4  PASS  0 shared shadows
  D5  PASS  used_by[] consistent
  D6  PASS  all origins documented (OBReadATMResponse1/atms→open-data.yaml; OAuthTokenResponse/oauth2/token→owned:false)
  D7  PASS  no replaced_by refs
  ──────────────────────────────
  OVERALL: PASS  (blocking_rule_ids: [])
```

Delta from prior run (T15:00): D6 FAIL→PASS. No regressions on D2/D5/OAuthTokenResponse-D6.
