<!-- source: screens/standing-orders/api.yaml -->
<!-- source_hash: regenerated-2026-07-16 -->
<!-- generated: 2026-07-16T00:00:00Z -->

# standing-orders — API Reference

> **Source of Truth**: `idea-layer/screens/standing-orders/api.yaml`  
> Generated: 2026-07-16T00:00:00Z

---

## Endpoints (1)

| ID | Method | Path | Auth | Permission | Response DTO |
|---|---|---|---|---|---|
| `standing-orders-list` | GET | `/accounts/{AccountId}/standing-orders` | Yes | `ReadStandingOrdersDetail` | `OBReadStandingOrder6` |

### Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `AccountId` | String | OBIE account identifier; received as nav param from account-detail |

### Response Headers

| Header | Description |
|---|---|
| `x-fapi-interaction-id` | Echoed request/response correlation UUID; log for support triage |

### Response — `OBReadStandingOrder6`

Data path: `Data.StandingOrder[]`

| Field | Description |
|---|---|
| `StandingOrderStatusCode` | OBIE enum: `Active` or `Inactive`; drives badge variant (primary / secondary) in ViewModel |
| `CreditorAccount.Name` | Beneficiary name |
| `CreditorAccount.Identification` | UK sort code + account number (`UK.OBIE.SortCodeAccountNumber` scheme, e.g. `40-12-09 65872310`) |
| `NextPaymentAmount.Amount` | Numeric next payment amount |
| `NextPaymentAmount.Currency` | ISO 4217 currency code |
| `NextPaymentDateTime` | ISO-8601 date of next scheduled payment; ViewModel formats as `dd MMM yyyy` |
| `FinalPaymentDateTime` | ISO-8601 date of last scheduled payment; nullable — `hasFinalPayment` flag set when non-null |
| `Frequency` | OBIE ISO 20022 frequency code (e.g. `IntrvlMnthDay:01:01`); decoded by `FrequencyDecoder` sealed class in ViewModel |
| `Reference` | Payment reference string (e.g. `RENT-FLAT12`, `ISA-TOPUP`) |

### Consent / Auth

- Requires `ReadStandingOrdersDetail` AISP permission granted at consent-creation time.
- `ReadStandingOrders` (without `Detail`) is NOT sufficient — it omits `NextPaymentAmount` and `Reference`.
- 403 returned by HSBC with OBIE code `UK.OBIE.Field.Missing` when consent lacks this permission; surfaced as `ConsentRevokedError` in app.

---

## Error Handling

| HTTP status | OBIE code | ViewModel error type | User message | Recovery |
|---|---|---|---|---|
| 401 | `UK.OBIE.Unauthorized` | `TokenExpiredError` | Session expired. Please log in again. | Route to login screen |
| 403 | `UK.OBIE.Field.Missing` | `ConsentRevokedError` | Account access consent has been revoked. | Route to consent-list screen |
| 429 | `UK.OBIE.RateLimit` | `RateLimitedError` | Too many requests. Please wait a moment and try again. | Retry button; retry after `Retry-After` header delay |
| 500 | `UK.OBIE.UnexpectedError` | `ServerError` | Something went wrong. Please try again later. | Retry button; persistent failure routes to support |
| 503 | `UK.OBIE.ServiceUnavailable` | `ServerError` | Something went wrong. Please try again later. | Retry with exponential backoff |
| IOException | — | `NetworkError` | No network connection. Check your connection and retry. | Retry button re-triggers `LoadStandingOrders` |

---

## Frequency Code Decoding

OBIE Frequency field uses ISO 20022 codes. `FrequencyDecoder` sealed class in ViewModel maps them:

| OBIE code (examples) | Human-readable label |
|---|---|
| `IntrvlMnthDay:01:01` | Monthly on the 1st |
| `IntrvlWkDay:01:5` | Weekly every Friday |
| `IntrvlDay:01` | Daily |
| `IntrvlYear:01:01:01` | Annually |
| _(any unrecognised code)_ | Raw OBIE code string (graceful fallback — no crash) |

---

## Notes

- This is an AISP read-only screen. No write, create, or mutation operations are performed.
- No local cache is written. Data lives only in ViewModel memory; re-fetched on every mount, pull-to-refresh, or explicit retry.
- `FinalPaymentDateTime` is optional. The `so_final_date` component is hidden when `FinalPaymentDateTime` is null.
