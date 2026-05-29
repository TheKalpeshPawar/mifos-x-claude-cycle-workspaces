# API Reference — Products

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | products                                    |
| Base URL | https://apisandbox.openbankproject.com      |

---

## GET /obp/v5.0.0/banks/{bankId}/products

**Auth:** DirectLogin
**Tag:** Product
**Trigger:** `ProductsLoaded` on screen open / `RetryLoad` event

Fetches the full list of banking products offered by the bank from OBP v5.0.0. The `ProductsViewModel` transforms the response into `List<BankProduct>` and maps `category` to `ProductCategory` for filter-chip state management. The four products rendered in the UI (Instant Access Savings, Fixed Rate Bond 1yr, Personal Loan, Platinum Credit Card) are constructed from this endpoint's response combined with feature-specific display metadata.

### Path Parameters

| Name   | Type   | Required | Description                              |
|--------|--------|----------|------------------------------------------|
| bankId | String | Yes      | Bank identifier — e.g. `gh.29.uk`        |

### Response Fields

| Field                        | Type                | Description                                                       |
|------------------------------|---------------------|-------------------------------------------------------------------|
| products                     | List\<Product\>     | Array of product objects for the given bank                       |
| products[].code              | String              | Unique product code — e.g. `"EQB-SAV-001"`                        |
| products[].name              | String              | Human-readable product name                                       |
| products[].category          | String              | Product category enum: `SAVINGS`, `LOANS`, `CARDS`, `MORTGAGES`, `CURRENT` |
| products[].family            | String              | Product family grouping — e.g. `"Personal Banking"`               |
| products[].super_family      | String              | Super-family grouping — e.g. `"Deposits"`, `"Credit"`             |
| products[].more_info_url     | String              | Canonical URL for full product detail page                        |
| products[].details           | ProductDetails      | Product-specific attributes (rate, term, min deposit, etc.)       |
| products[].meta              | ProductMeta         | Regulatory metadata (licence ID + name)                           |
| products[].meta.license.id   | String              | Regulatory licence identifier — e.g. `"CBK-DTL-2019-001"`        |
| products[].meta.license.name | String              | Regulatory licence full name                                      |

### Demo Data

The following five items represent a realistic OBP products response for the `gh.29.uk` sandbox bank. The UI renders four of them (filtered by category):

| code              | name                           | category  | family           | super_family        | details summary                                              |
|-------------------|--------------------------------|-----------|------------------|---------------------|--------------------------------------------------------------|
| EQB-SAV-001       | Equity Jijenge Savings Account | SAVINGS   | Personal Banking | Deposits            | 3.5% p.a. on balances > KES 10,000; min KES 1,000; fee KES 0 |
| EQB-CUR-001       | Equity Current Account         | CURRENT   | Personal Banking | Transactional       | Overdraft up to KES 100,000; min KES 0; fee KES 250/mo       |
| EQB-LN-SME-002    | Equity Biashara Loan           | LOANS     | Business Banking | Credit              | Max KES 5,000,000; up to 60 months; 14% p.a. reducing        |
| EQB-CARD-VISA-001 | Equity Visa Debit Card         | CARDS     | Cards            | Payment Instruments | Daily limit KES 200,000; international; fee KES 500 issuance |
| EQB-MTG-001       | Equity Home Loan               | MORTGAGES | Personal Banking | Credit              | Max KES 50,000,000; up to 25 years; 12.5% p.a. fixed 3yr    |

**UI card ↔ API category mapping:**

| UI Product Card        | API category | Displayed rate     | Demo product code  |
|------------------------|--------------|--------------------|---------------------|
| Instant Access Savings | SAVINGS      | 4.5% AER           | EQB-SAV-001         |
| Fixed Rate Bond 1yr    | SAVINGS      | 5.1% AER           | EQB-SAV-001 (FRB variant) |
| Personal Loan          | LOANS        | From 6.9% APR      | EQB-LN-SME-002      |
| Platinum Credit Card   | CARDS        | 0% for 20 months   | EQB-CARD-VISA-001   |

> The display rates shown in the UI are enriched values from the UI layer spec. The `details` block in demo-data.yaml carries raw OBP sandbox values; the `ProductsViewModel` augments them with display-formatted strings for `ias_rate`, `frb_rate`, `pl_rate`, and `pcc_rate` components.

### Error Codes

| Code | OBP Message         | UI Handling                                                     |
|------|---------------------|-----------------------------------------------------------------|
| 400  | INVALID_BANK_ID     | Show error state; log `LOAD_FAILED`; display retry button       |
| 401  | USER_NOT_LOGGED_IN  | Navigate to login screen; clear session                         |
| 404  | BANK_NOT_FOUND      | Show error state ("Unable to load products"); display retry     |
| 503  | SERVICE_UNAVAILABLE | Show error state with `cloud_off` icon; `NETWORK_TIMEOUT` event |

---

_Generated by /idea export | 2026-05-30_
