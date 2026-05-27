# API.md — direct-debit-detail

OBP API version: **v7.0.0**
Auth: Bearer token (OBP OAuth 2.0 / Direct Login)

---

## Endpoint 1 — Get Standing Order Detail

**Trigger:** `LoadMandate` (screen entry, retry tap)

```
GET /obp/v7.0.0/banks/{bankId}/accounts/{accountId}/standing-orders/{standingOrderId}
```

### Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| bankId | String | Yes | OBP bank identifier |
| accountId | String | Yes | Account that owns the mandate |
| standingOrderId | String | Yes | Unique standing order identifier |

### Headers

| Header | Value |
|---|---|
| Authorization | Bearer {token} |
| Content-Type | application/json |

### Response — 200 OK

```json
{
  "standing_order_id": "so-8f3d2a",
  "bank_id": "gh.29.uk",
  "account_id": "8ca8a7e4-6d02-40e3-a129-0b2bf89de9f0",
  "counterparty_name": "Thames Water Utilities Ltd",
  "amount": {
    "value": "48.50",
    "currency": "GBP"
  },
  "frequency": "MONTHLY",
  "start_date": "2024-01-15",
  "next_payment_date": "2026-06-15",
  "status": "active",
  "reference": "WATER-ACC-TW-99102",
  "recent_payments": [
    {
      "payment_id": "pmt-001",
      "date": "2026-05-15",
      "amount": {
        "value": "48.50",
        "currency": "GBP"
      },
      "status": "completed"
    },
    {
      "payment_id": "pmt-002",
      "date": "2026-04-15",
      "amount": {
        "value": "48.50",
        "currency": "GBP"
      },
      "status": "completed"
    }
  ]
}
```

### Response Fields

| Field | Type | Nullable | Description |
|---|---|---|---|
| standing_order_id | String | No | Unique mandate identifier |
| bank_id | String | No | OBP bank identifier |
| account_id | String | No | Owning account identifier |
| counterparty_name | String | No | Name of the payee/creditor |
| amount.value | String | No | Decimal string amount |
| amount.currency | String | No | ISO-4217 currency code |
| frequency | String | No | WEEKLY \| MONTHLY \| QUARTERLY \| ANNUALLY |
| start_date | String | No | ISO-8601 date mandate started |
| next_payment_date | String | Yes | ISO-8601 date of next scheduled payment; null if cancelled |
| status | String | No | active \| pending \| cancelled \| suspended |
| reference | String | Yes | Mandate reference string |
| recent_payments | List | No | Most recent payments against this mandate (≤10) |
| recent_payments[].payment_id | String | No | Payment identifier |
| recent_payments[].date | String | No | ISO-8601 payment date |
| recent_payments[].amount.value | String | No | Payment amount |
| recent_payments[].amount.currency | String | No | Payment currency |
| recent_payments[].status | String | No | completed \| failed \| pending |

### Error Responses

| HTTP Status | OBP Error Code | UI Handling |
|---|---|---|
| 401 | USER_NOT_LOGGED_IN | Clear session → navigate to Login |
| 403 | INSUFFICIENT_AUTHORISATION | Show error state: "You do not have permission to view this mandate" |
| 404 | MANDATE_NOT_FOUND | Show empty state: "No mandate found" |
| 500 | OBP_CONNECTOR_CANNOT_OBTAIN_RESPONSE | Show error state with retry |

---

## Endpoint 2 — Cancel Standing Order

**Trigger:** `OnCancelClicked` → user confirms in CancelConfirmDialog

```
DELETE /obp/v7.0.0/banks/{bankId}/accounts/{accountId}/standing-orders/{standingOrderId}
```

### Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| bankId | String | Yes | OBP bank identifier |
| accountId | String | Yes | Account that owns the mandate |
| standingOrderId | String | Yes | Mandate to cancel |

### Headers

| Header | Value |
|---|---|
| Authorization | Bearer {token} |
| Content-Type | application/json |

### Request Body

None (DELETE with path parameters only).

### Response — 200 OK

```json
{
  "success": true,
  "message": "Standing order successfully cancelled."
}
```

### Response Fields

| Field | Type | Nullable | Description |
|---|---|---|---|
| success | Boolean | No | true on successful cancellation |
| message | String | No | Human-readable confirmation message |

### Error Responses

| HTTP Status | OBP Error Code | UI Handling |
|---|---|---|
| 401 | USER_NOT_LOGGED_IN | Clear session → navigate to Login |
| 403 | INSUFFICIENT_AUTHORISATION | Snackbar: "You are not authorised to cancel this mandate" |
| 404 | MANDATE_NOT_FOUND | Snackbar: "Mandate not found — it may have already been cancelled" |
| 500 | CANCEL_FAILED | Snackbar: "Cancellation failed. Please try again." |

---

## Domain Models (Kotlin)

```kotlin
data class StandingOrderDetail(
    val standingOrderId: String,
    val bankId: String,
    val accountId: String,
    val counterpartyName: String,
    val amountValue: String,
    val amountCurrency: String,
    val frequency: MandateFrequency,
    val startDate: String,
    val nextPaymentDate: String?,
    val status: MandateStatus,
    val reference: String?,
    val recentPayments: List<MandatePayment>
)

data class MandatePayment(
    val paymentId: String,
    val date: String,
    val amountValue: String,
    val amountCurrency: String,
    val status: PaymentStatus
)

enum class MandateFrequency { WEEKLY, MONTHLY, QUARTERLY, ANNUALLY }
enum class MandateStatus { active, pending, cancelled, suspended }
enum class PaymentStatus { completed, failed, pending }

data class CancelMandateResult(
    val success: Boolean,
    val message: String
)
```

---

## Repository Interface

```kotlin
interface DirectDebitRepository {
    suspend fun getStandingOrderDetail(
        bankId: String,
        accountId: String,
        standingOrderId: String
    ): Result<StandingOrderDetail>

    suspend fun cancelStandingOrder(
        bankId: String,
        accountId: String,
        standingOrderId: String
    ): Result<CancelMandateResult>
}
```
