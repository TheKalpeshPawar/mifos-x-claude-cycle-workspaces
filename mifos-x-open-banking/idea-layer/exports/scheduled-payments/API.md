<!-- source: screens/scheduled-payments/api.yaml -->
<!-- source_hash: regenerated-2026-07-16 -->
<!-- generated: 2026-07-16T00:00:00Z -->

# scheduled-payments — API Reference

> **Source of Truth**: `idea-layer/screens/scheduled-payments/api.yaml`  
> Generated: 2026-07-16T00:00:00Z

---

## Endpoints (1)

| ID | Method | Path | Auth | Permission | Response DTO |
|---|---|---|---|---|---|
| `scheduled-payments-list` | GET | `/accounts/{AccountId}/scheduled-payments` | Yes | `ReadScheduledPaymentsDetail` | `OBReadScheduledPayment3` |

### Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `AccountId` | String | OBIE account identifier; received as nav param from account-detail |

### Response — `OBReadScheduledPayment3`

Data path: `Data.ScheduledPayment[]`

| Field | Description |
|---|---|
| `ScheduledPaymentDateTime` | ISO-8601 future date of the scheduled payment; ViewModel formats as `EEE d MMM yyyy` |
| `ScheduledType` | OBIE enum: `Execution` (money leaves account) or `Arrival` (funds arrive at beneficiary) |
| `Reference` | Payment narrative / reference string |
| `InstructedAmount.Amount` | Numeric payment amount |
| `InstructedAmount.Currency` | ISO 4217 currency code (e.g. `GBP`) |
| `CreditorAccount.Name` | Payee display name |
| `CreditorAccount.Identification` | UK sort code + account number (e.g. `08-32-00 12001039`) |

### Consent / Auth

- Requires `ReadScheduledPaymentsDetail` AISP permission granted at consent-creation time.
- `ReadScheduledPayments` alone is NOT sufficient — it omits key fields.
- 403 returned by HSBC when consent lacks this permission; surfaced in app as `ConsentRevoked` error state.

---

## Error Handling

| HTTP status | OBIE / type | ViewModel error type | Recovery |
|---|---|---|---|
| 401 | Token expired or invalid | `TokenExpired` | Route to login screen |
| 403 | Consent does not include `ReadScheduledPaymentsDetail` | `ConsentRevoked` | Route to consent-list screen |
| 429 | Rate limit exceeded | `RateLimited` | Retry button; exponential back-off |
| IOException | Network timeout / no connectivity | `NetworkError` | Retry button re-triggers `LoadScheduledPayments` |

---

## Notes

- This is an AISP read-only screen. No write, create, or mutation operations are performed.
- No local cache is written. Data lives only in ViewModel memory; re-fetched on every mount or explicit retry.
- `ScheduledType` chip icon and a11y string are derived in ViewModel, not served by the API.
