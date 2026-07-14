<!-- source: screens/product/api.yaml -->
<!-- source_hash: regenerated-2026-07-14 -->
<!-- generated: 2026-07-14T21:00:00Z -->

# product — API Reference

> **Source:** `idea-layer/screens/product/api.yaml`  
> **Standard:** OBIE Account Information API v4.0 (OBReadProduct2)  
> Generated: 2026-07-14T21:00:00Z

---

## Endpoints

### GET /accounts/{AccountId}/product

Retrieves the product (PCA or BCA) associated with the specified account, including fee tiers,
credit interest bands, and overdraft terms.

| Field | Value |
|---|---|
| Method | `GET` |
| Path | `/accounts/{AccountId}/product` |
| Permission | `ReadProducts` (must be granted in active Open Banking consent) |
| Auth | Bearer PSU access token |
| Response DTO | `OBReadProduct2` |
| Caching | None — always-fresh fetch on screen mount |

#### Path Parameters

| Param | Type | Required | Description |
|---|---|---|---|
| `AccountId` | String | Yes | OBIE account identifier (from accounts list) |

#### Request Headers

| Header | Value |
|---|---|
| `Authorization` | `Bearer <access_token>` |
| `x-fapi-financial-id` | ASPSP financial ID (set by Ktorfit interceptor) |
| `Accept` | `application/json` |

#### Response: 200 OK

```json
{
  "Data": [
    {
      "AccountId": "string",
      "ProductId": "string",
      "ProductType": "PCA",
      "ProductName": "HSBC Advance Account",
      "PCA": {
        "ProductDetails": {
          "MonthlyMaximumCharge": "0.00",
          "Features": ["Free UK Cash Withdrawals", "Fee-free overseas spending"]
        },
        "CreditInterest": {
          "TierBandSet": [
            {
              "TierBandMethod": "Tiered",
              "TierBand": [
                {
                  "TierValueMinimum": "0.00",
                  "BandLimit": "1000.00",
                  "AER": "0.10",
                  "ApplicationFrequency": "Monthly"
                },
                {
                  "TierValueMinimum": "1000.01",
                  "BandLimit": "10000.00",
                  "AER": "0.50",
                  "ApplicationFrequency": "Monthly"
                }
              ]
            }
          ]
        },
        "Overdraft": {
          "OverdraftTierBandSet": [
            {
              "OverdraftTierBand": [
                {
                  "OverdraftType": "Arranged",
                  "EAR": "39.90"
                },
                {
                  "OverdraftType": "Unarranged",
                  "EAR": "49.90"
                }
              ]
            }
          ]
        }
      }
    }
  ]
}
```

**Empty data case:** `Data: []` or `Data[0].PCA == null && Data[0].BCA == null`  
→ ViewModel emits `ProductUiState.Empty` (informational state; not an error).  
Occurs for account types that do not carry OBProduct2 entries: GlobalMoney, Savings, CreditCard.

#### Error Responses

| HTTP Code | Reason | ViewModel Response |
|---|---|---|
| 401 | PSU access token expired | `Error("Session expired. Please re-authenticate.")` |
| 403 | Active consent does not include ReadProducts permission | `Error("Consent does not include ReadProducts.")` |
| 404 | No OBProduct2 record associated with this AccountId | `Error("No product data available for this account.")` |
| NETWORK_ERROR | Device offline or OBIE AIS endpoint unreachable | `Error(e.localizedMessage)` |

---

## ViewModel Integration

```kotlin
// Triggered on screen mount; accountId passed from NavHost
suspend fun productLoad(accountId: String) {
    uiState = ProductUiState.Loading
    runCatching { productService.getProduct(accountId) }
        .onSuccess { response ->
            val product = response.data.firstOrNull()
            uiState = when {
                product?.PCA != null || product?.BCA != null ->
                    ProductUiState.Content(product)
                else -> ProductUiState.Empty
            }
        }
        .onFailure { uiState = ProductUiState.Error(it.localizedMessage) }
}

// Retry delegates to productLoad
suspend fun retryLoad(accountId: String) = productLoad(accountId)
```

---

## Permission Gating

`ReadProducts` must be present in the PSU's active Open Banking consent.

- HTTP 403 → ViewModel emits `Error("Consent does not include ReadProducts.")` — message
  explicitly informs the user which permission is missing (CC5 capability-completeness gate).
- No silent fallback; the user must re-consent to include ReadProducts before the screen
  can load successfully.
