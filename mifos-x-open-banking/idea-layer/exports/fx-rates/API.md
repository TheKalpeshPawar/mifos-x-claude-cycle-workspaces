# API Reference — Exchange Rates

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | fx-rates                                    |
| Base URL | https://apisandbox.openbankproject.com      |

---

## GET /obp/v5.1.0/banks/{bankId}/currencies

**Auth:** DirectLogin
**Tag:** FX
**Trigger:** `loadFxScreen()` on screen open — populates from_currency_select and to_currency_select dropdown options (components bound via `api.ref: obp_currencies`)

Fetches the full list of currencies supported by the bank. The ViewModel filters to `is_enabled: true` entries and maps each to a dropdown option showing the currency code and name. Loaded once on screen entry; cached until navigated away.

### Path Parameters

| Name   | Type   | Value       | Description                  |
|--------|--------|-------------|------------------------------|
| bankId | String | ke.equity.001 | Bank identifier (demo value) |

### Response Fields

| Field         | Type    | Description                                      |
|---------------|---------|--------------------------------------------------|
| currency_code | String  | ISO 4217 code e.g. "GBP", "EUR", "USD", "KES"  |
| name          | String  | Human-readable name e.g. "British Pound"         |
| is_enabled    | Boolean | Whether the currency is active and selectable    |

### Demo Data

| currency_code | name                  | is_enabled |
|---------------|-----------------------|------------|
| KES           | Kenyan Shilling       | true       |
| USD           | US Dollar             | true       |
| EUR           | Euro                  | true       |
| GBP           | British Pound         | true       |
| TZS           | Tanzanian Shilling    | true       |
| UGX           | Ugandan Shilling      | true       |
| ZAR           | South African Rand    | true       |
| AED           | UAE Dirham            | true       |
| CNY           | Chinese Yuan          | true       |

### Error Codes

| Code | Message                                  | UI Handling                                                         |
|------|------------------------------------------|---------------------------------------------------------------------|
| 401  | Unauthorized — missing or invalid token  | Navigate to login                                                   |
| 404  | Bank not found                           | from_currency_select + to_currency_select show error banner: "Could not load supported currencies. Please try again." with retry |
| 500  | Internal server error                    | Same banner as 404; screen enters error state if converter cannot render |

---

## GET /obp/v5.1.0/banks/{bankId}/fx/{fromCurrencyCode}/{toCurrencyCode}

**Auth:** DirectLogin
**Tag:** FX
**Trigger:** Screen load (6 popular pairs pre-fetched in parallel) + currency pair change in converter (re-fetch for new pair) + `RetryLoadEvent`

Called once per currency pair. On screen entry, `FxRatesViewModel` issues 6 parallel requests for the Popular Pairs section and 1 for the converter's default pair (GBP/EUR). When the user changes from/to or swaps, only the affected pair is re-fetched. Amount recalculation (`convertedAmount = sendAmount * exchangeRate`) is performed client-side on cached `conversion_value` without an additional API call.

### Path Parameters

| Name             | Type   | Description                   | Demo Values                   |
|------------------|--------|-------------------------------|-------------------------------|
| bankId           | String | Bank identifier               | ke.equity.001                 |
| fromCurrencyCode | String | Source currency ISO 4217 code | GBP, EUR, USD                 |
| toCurrencyCode   | String | Target currency ISO 4217 code | EUR, USD, JPY, INR, GBP, KES  |

### Response Fields

| Field                    | Type   | Description                                                        |
|--------------------------|--------|--------------------------------------------------------------------|
| bank_id                  | String | Bank identifier matching path parameter                            |
| from_currency_code       | String | Source currency code confirmed by server                           |
| to_currency_code         | String | Target currency code confirmed by server                           |
| conversion_value         | Double | Rate: 1 unit of from_currency = N units of to_currency; drives converted_result_display and rate_info_text |
| inverse_conversion_value | Double | Inverse rate for display when pair is swapped                      |
| effective_date           | String | ISO-8601 UTC timestamp when rate was last published; drives last_updated_text |

### Demo Rate Data — Popular Pairs

| Pair    | bank_id       | conversion_value | inverse_conversion_value | effective_date           | change  | direction |
|---------|---------------|------------------|--------------------------|--------------------------|---------|-----------|
| GBP/EUR | ke.equity.001 | 1.1672           | 0.8568                   | 2026-05-26T00:00:00Z     | +0.2%   | up        |
| GBP/USD | ke.equity.001 | 1.2834           | 0.7791                   | 2026-05-26T00:00:00Z     | -0.1%   | down      |
| GBP/JPY | ke.equity.001 | 193.45           | 0.005169                 | 2026-05-26T00:00:00Z     | +0.4%   | up        |
| EUR/USD | ke.equity.001 | 1.0993           | 0.9097                   | 2026-05-26T00:00:00Z     | -0.3%   | down      |
| USD/INR | ke.equity.001 | 83.22            | 0.01202                  | 2026-05-26T00:00:00Z     | 0.0%    | neutral   |
| EUR/GBP | ke.equity.001 | 0.8568           | 1.1672                   | 2026-05-26T00:00:00Z     | -0.2%   | down      |

Also available in demo-data.yaml (obp_fx_rate): USD/KES = 129.45, EUR/KES = 140.22, GBP/KES = 163.87.

### Converter Default Binding

| Field                  | Value                                                        |
|------------------------|--------------------------------------------------------------|
| from_currency_select   | GBP                                                          |
| to_currency_select     | EUR                                                          |
| send_amount_input      | 1,000                                                        |
| converted_result_display | = 1,167.20 EUR (1000 * 1.1672)                             |
| rate_info_text         | "Rate: 1 GBP = 1.1672 EUR"                                  |
| last_updated_text      | "Rates updated: 14 May 2026, 15:42 UTC" (from effective_date)|

### Error Codes

| Code | Message                              | UI Handling                                                                               |
|------|--------------------------------------|-------------------------------------------------------------------------------------------|
| 401  | Unauthorized — missing or invalid token | Navigate to login                                                                      |
| 404  | Currency pair not supported          | Affected rate row: empty box with currency_exchange icon + "No exchange rate available for {PAIR}."; converter: rate_info_text shows error banner "Rate data temporarily unavailable. Please retry." |
| 500  | Internal server error                | Converter and rate rows show error banners with retry; screen error state if all 7 requests fail |

---

_Generated by /idea export | 2026-05-30_
