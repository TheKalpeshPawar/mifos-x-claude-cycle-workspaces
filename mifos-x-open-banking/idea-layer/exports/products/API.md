# API Reference — Products

| Field | Value |
|---|---|
| Feature | products |
| Base URL | https://apisandbox.openbankproject.com |
| Auth Scheme | DirectLogin (header: `DirectLogin token=<token>`) |
| OBP Version | v5.0.0 |

---

## GET /obp/v5.0.0/banks/{bank_id}/products

**Tag:** Product
**Purpose:** Fetch the full product catalogue for a bank. Results are filtered client-side by `selectedCategory` in `ProductsViewModel`. Pass the optional `category` query parameter to request a server-side pre-filtered list when network efficiency is required.

### Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| bank_id | String | Yes | OBP bank identifier (e.g. `gh.29.uk`) |

### Query Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| category | String | No | Filter by product category. Accepted values: `SAVINGS`, `LOANS`, `CARDS`, `MORTGAGES`, `CURRENT`. Omit to return all categories. |

### Request Headers

| Header | Value |
|---|---|
| Authorization | `DirectLogin token=<token>` |
| Content-Type | `application/json` |

### Response — 200 OK

```json
{
  "products": [
    {
      "bank_id": "gh.29.uk",
      "code": "INSTANT_ACCESS_SAVINGS",
      "parent_product_code": "",
      "name": "Instant Access Savings",
      "category": "SAVINGS",
      "family": "SAVINGS",
      "super_family": "DEPOSITS",
      "more_info_url": "https://example.com/products/instant-access-savings",
      "details": {
        "aer": "4.5",
        "rate_type": "variable",
        "min_deposit": "0",
        "access_type": "instant",
        "notice_period_days": 0
      },
      "features": [
        { "id": "AER_4_5", "name": "4.5% AER", "feature_id": "AER_4_5" },
        { "id": "INSTANT_ACCESS", "name": "Instant access", "feature_id": "INSTANT_ACCESS" },
        { "id": "NO_MIN_DEPOSIT", "name": "No minimum deposit", "feature_id": "NO_MIN_DEPOSIT" }
      ],
      "meta": {
        "license": { "id": "OBP-CC-BY-4.0", "name": "Open Licence" }
      }
    },
    {
      "bank_id": "gh.29.uk",
      "code": "FIXED_RATE_BOND_1YR",
      "parent_product_code": "",
      "name": "Fixed Rate Bond 1yr",
      "category": "SAVINGS",
      "family": "SAVINGS",
      "super_family": "DEPOSITS",
      "more_info_url": "https://example.com/products/fixed-rate-bond-1yr",
      "details": {
        "aer": "5.1",
        "rate_type": "fixed",
        "min_deposit": "1000",
        "term_months": 12,
        "interest_payment": "at_maturity"
      },
      "features": [
        { "id": "AER_5_1", "name": "5.1% AER", "feature_id": "AER_5_1" },
        { "id": "TERM_12M", "name": "12-month term", "feature_id": "TERM_12M" },
        { "id": "FSCS_PROTECTED", "name": "FSCS protected", "feature_id": "FSCS_PROTECTED" }
      ],
      "meta": {
        "license": { "id": "OBP-CC-BY-4.0", "name": "Open Licence" }
      }
    },
    {
      "bank_id": "gh.29.uk",
      "code": "PERSONAL_LOAN",
      "parent_product_code": "",
      "name": "Personal Loan",
      "category": "LOANS",
      "family": "LOANS",
      "super_family": "CREDIT",
      "more_info_url": "https://example.com/products/personal-loan",
      "details": {
        "apr_representative": "6.9",
        "rate_type": "representative",
        "min_amount": "1000",
        "max_amount": "25000",
        "min_term_months": 12,
        "max_term_months": 84
      },
      "features": [
        { "id": "APR_FROM_6_9", "name": "From 6.9% APR", "feature_id": "APR_FROM_6_9" },
        { "id": "UP_TO_25K", "name": "Up to £25,000", "feature_id": "UP_TO_25K" },
        { "id": "TERMS_1_7YR", "name": "1–7 year terms", "feature_id": "TERMS_1_7YR" }
      ],
      "meta": {
        "license": { "id": "OBP-CC-BY-4.0", "name": "Open Licence" }
      }
    },
    {
      "bank_id": "gh.29.uk",
      "code": "PLATINUM_CREDIT_CARD",
      "parent_product_code": "",
      "name": "Platinum Credit Card",
      "category": "CARDS",
      "family": "CREDIT_CARDS",
      "super_family": "CREDIT",
      "more_info_url": "https://example.com/products/platinum-credit-card",
      "details": {
        "intro_rate": "0",
        "intro_rate_months": 20,
        "intro_rate_type": "purchase",
        "annual_fee": "0",
        "contactless": true,
        "apple_pay": true,
        "google_pay": true
      },
      "features": [
        { "id": "ZERO_PCT_20M", "name": "0% for 20 months", "feature_id": "ZERO_PCT_20M" },
        { "id": "NO_ANNUAL_FEE", "name": "No annual fee", "feature_id": "NO_ANNUAL_FEE" },
        { "id": "CONTACTLESS", "name": "Contactless & Apple/Google Pay", "feature_id": "CONTACTLESS" }
      ],
      "meta": {
        "license": { "id": "OBP-CC-BY-4.0", "name": "Open Licence" }
      }
    }
  ]
}
```

### Response Fields

| Field | Type | Description |
|---|---|---|
| products | List\<Product\> | Array of bank product objects |
| bank_id | String | OBP bank identifier |
| code | String | Unique product code — used as key for apply / detail navigation |
| parent_product_code | String | Parent product code (empty string if top-level) |
| name | String | Human-readable product name |
| category | String | Product category — `SAVINGS`, `LOANS`, `CARDS`, `MORTGAGES`, `CURRENT` |
| family | String | Product family grouping |
| super_family | String | Top-level product family |
| more_info_url | String | URL to full product detail page |
| details | ProductDetails | Nested object with rate, fee, term, and eligibility data (schema varies by category) |
| features | List\<ProductFeature\> | Ordered list of display features for badge chips |
| features[].id | String | Feature identifier |
| features[].name | String | Display name shown in feature badge |
| meta.license | License | OBP data licence metadata |

### ProductDetails — by Category

| Category | Key Fields |
|---|---|
| SAVINGS (variable) | aer, rate_type="variable", min_deposit, access_type, notice_period_days |
| SAVINGS (fixed) | aer, rate_type="fixed", min_deposit, term_months, interest_payment |
| LOANS | apr_representative, min_amount, max_amount, min_term_months, max_term_months |
| CARDS | intro_rate, intro_rate_months, intro_rate_type, annual_fee, contactless, apple_pay, google_pay |
| MORTGAGES | ltv_max, rate_type, svr, initial_term_months, arrangement_fee |

### Error Codes

| HTTP Code | OBP Error | Description |
|---|---|---|
| 400 | INVALID_BANK_ID | The provided bank_id is not a valid OBP bank identifier |
| 401 | USER_NOT_LOGGED_IN | DirectLogin token is missing, malformed, or expired |
| 404 | BANK_NOT_FOUND | No bank matches the provided bank_id |
| 503 | SERVICE_UNAVAILABLE | OBP backend is temporarily unavailable — surface error state with retry |

---

## Client-Side Category Filtering

The `ProductsViewModel` holds `selectedCategory: ProductCategory` (default `ALL`). When the user taps a category chip, `CategoryFilterChanged` is dispatched, updating `selectedCategory` and re-filtering the cached `products` list without a network call. Enum mapping:

| UI Tab | Query Param / Enum | OBP category value |
|---|---|---|
| All | ProductCategory.ALL | (no filter — show all) |
| Savings | ProductCategory.SAVINGS | SAVINGS |
| Loans | ProductCategory.LOANS | LOANS |
| Cards | ProductCategory.CARDS | CARDS |
| Mortgages | ProductCategory.MORTGAGES | MORTGAGES |

---

*Generated by /idea export | 2026-05-25*
