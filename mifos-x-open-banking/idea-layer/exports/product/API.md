# Product — API Contracts

> Generated from `screens/product/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Endpoints: 1 · DTOs: 1

Base path `/obie/open-banking/v4.0/aisp`. AIS read on the PSU bearer.

## Endpoint summary

| # | ID | Method | Path | Permission | Response DTO | Cache |
|---|---|---|---|---|---|---|
| 1 | `product` | GET | `/accounts/{AccountId}/product` | ReadProducts | `OBReadProduct2` | **none** |

**`cache_strategy: none` — the only screen in the app with no cache at all.** The bank can
revise product terms, and a cached copy would misstate the charges a customer is subject to.
No store, no `AppStoreRegistry` qualifier, no `registerForLogout`; a bare
`suspend fun getProduct(accountId): NetworkResult<ProductTerms?, NetworkError>`.

## 1 · Account product

`GET /accounts/{AccountId}/product` → `200` `OBReadProduct2`

```json
{
  "Data": { "Product": [
    { "ProductName": "BMM ACCOUNT", "ProductId": "10", "AccountId": "1123456841",
      "ProductType": "Other",
      "OtherProductType": { "Name": "Savings", "Description": "BMM ACCOUNT" } }
  ] },
  "Links": { "Self": "…/accounts/1123456841/product" },
  "Meta": { "TotalPages": 1 }
}
```

That sandbox response is the **thin** shape — `ProductType: "Other"` with no terms. The rich
shape carries a `PCA` (personal current account) or `BCA` (business current account) block.

## The `PCA` / `BCA` sub-tree

`Product.kt` originally modelled only name/id/type, so **eight new DTO classes** were needed:
`ProductBlock`, `ProductDetails`, `CreditInterest`, `TierBandSet`, `TierBand`, `Overdraft`,
`OverdraftTierBandSet`, `OverdraftTierBand`.

One `ProductBlock` serves **both** `PCA` and `BCA` — the fields read are identically shaped.

`ProductTerms` (`core/model`) flattens the nested band groups into plain lists, so the feature
never sees an OBIE shape:

| Rendered section | Source |
|---|---|
| header | `ProductName`, resolved product type |
| monthly maximum charge | `ProductDetails` |
| credit-interest AER tiers | `CreditInterest.TierBandSet[].TierBand[]` + `ApplicationFrequency` + band range |
| overdraft EAR tiers | `Overdraft.OverdraftTierBandSet[].OverdraftTierBand[]`, by type |
| feature list | `ProductDetails` |

## Two routes to Empty

| Outcome | Why it is Empty, not Error |
|---|---|
| `Success(null)` — mapper found neither a `PCA` nor a `BCA` block | the normal answer for GlobalMoney, Savings and CreditCard |
| **HTTP 404** | the bank holds no product record for this account |

Neither is a failure a customer can act on, so neither gets the error icon or a Retry.

> **Corrected 2026-07-30.** `api.yaml` previously said 404 emits `Error(...)`, contradicting
> `data-flow.yaml:29-33` — which maps 404 → `state: empty` and cites *this file* as its
> authority — and `tests.yaml` TC-PROD-006, which asserted `state: error`. A three-way
> contradiction. Resolved to Empty; `api.yaml` and TC-PROD-006 were both corrected.

## Error matrix

| HTTP | Kind | Retry? | UI |
|---|---|:--:|---|
| 401 | `TokenExpiredError` | ✅ | Error + Retry |
| 403 | `ConsentScopeError` | ✅ | Error — ReadProducts absent from the consent |
| **404** | — | ✗ | **Empty** — no product data available |
| — | `NetworkError` | ✅ | Error + Retry |
| `Success(null)` | — | ✗ | **Empty** |

## Rendering trap — `%%`

Compose Multiplatform's resource formatter does **not** collapse Android's `%%` escape, so
`"%1$s%% AER"` renders as `0.15%% AER`. Write a single `%`.

This feature shipped exactly that defect with **every test green** — tag and count assertions
pass regardless of what the glyphs say. It is why Roborazzi goldens exist here: look at the
image after touching any templated string.

## Source binding

`core/network/api/Aisp.kt` `getProduct` · `core/network/.../model/ais/product/` (the eight new
DTO classes) · `ProductRepository` — a **storeless one-shot**, unlike every other repository in
the app.
