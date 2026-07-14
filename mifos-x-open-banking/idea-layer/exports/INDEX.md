# Export Index — mifos-x-open-banking

> Generated: 2026-07-13T21:54:32Z  
> Source: 25 feature screens under `idea-layer/screens/`  
> Artifacts: SPEC.md + API.md per feature (MOCKUP/Stitch: pending)

---

## Export Summary

| Artifact | Count |
|---|---|
| Features indexed | 25 |
| SPEC.md exported | 25 |
| API.md exported | 25 |
| MOCKUP.md exported | 0 |
| Stitch generated | 0 |

---

## Feature Export Registry

| Feature | SPEC.md | API.md | MOCKUP | Status | Quality |
|---|---|---|---|---|---|
| account-detail | ✅ 94L | ✅ 31L | — | designed | 94 |
| accounts | ✅ 91L | ✅ 31L | — | designed | 94 |
| atm-locator | ✅ 84L | ✅ 30L | — | designed | 89 |
| beneficiaries | ✅ 95L | ✅ 29L | — | designed | 91 |
| budgets | ✅ 95L | ✅ 25L | — | designed | 94 |
| consent-callback | ✅ 80L | ✅ 33L | — | designed | 94 |
| consent-detail | ✅ 86L | ✅ 24L | — | designed | 95 |
| consent-list | ✅ 96L | ✅ 27L | — | designed | 95 |
| direct-debits | ✅ 91L | ✅ 28L | — | designed | 95 |
| home | ✅ 110L | ✅ 34L | — | designed | 91 |
| login | ✅ 79L | ✅ 22L | — | designed | 93 |
| party | ✅ 80L | ✅ 24L | — | enriched | 93 |
| pfm-dashboard | ✅ 87L | ✅ 24L | — | enriched | 93 |
| product | ✅ 79L | ✅ 24L | — | enriched | 93 |
| profile | ✅ 90L | ✅ 23L | — | enriched | 93 |
| recurring-subscriptions | ✅ 82L | ✅ 23L | — | enriched | 94 |
| scheduled-payments | ✅ 83L | ✅ 25L | — | designed | 92 |
| settings | ✅ 95L | ✅ 24L | — | enriched | 94 |
| spending-by-category | ✅ 83L | ✅ 23L | — | designed | 93 |
| standing-orders | ✅ 87L | ✅ 26L | — | designed | 93 |
| statement-detail | ✅ 98L | ✅ 31L | — | designed | 93 |
| statements | ✅ 102L | ✅ 30L | — | design_partial | 94 |
| transaction-detail | ✅ 109L | ✅ 30L | — | enriched | 94 |
| transactions | ✅ 112L | ✅ 31L | — | enriched | 95 |
| user-onboarding | ✅ 97L | ✅ 23L | — | designed | 95 |

---

## Roundtrip Status

All 25 exports passed structural validation:
- Every SPEC.md ≥ 30 lines (min observed: 79L — login)
- Every API.md ≥ 15 lines (min observed: 22L — login)
- No placeholder text detected

---

## Warnings

- **6 features still at `enriched` status** (party, pfm-dashboard, product, profile, recurring-subscriptions, settings, transaction-detail, transactions): exports generated but docs.yaml not advanced to `designed`. Run `/idea approve {feature}` to gate for implementation.
- **1 feature at `design_partial`** (statements): exports present; source YAML may need a re-enrich pass.
- **`transaction-detail` and `transactions`** had blank status in docs.yaml — treated as `enriched` for export purposes.
- **MOCKUP.md / Stitch not generated** for any feature. Run `/idea export --mockup` or `/idea export --stitch` when ready.

---

## Next Steps

```
/idea approve {feature}      # gate enriched features for implementation
/idea export --mockup        # generate MOCKUP.md for all features
/implement {feature}         # after approve — begin KMP codegen
```

Roundtrip manifest: `idea-layer/EXPORT_MATRIX.yaml`
