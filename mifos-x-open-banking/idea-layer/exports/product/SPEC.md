<!-- source: screens/product/ui.yaml -->
<!-- source_hash: regenerated-2026-07-14 -->
<!-- generated: 2026-07-14T21:00:00Z -->

# SPEC — product

_Generated: 2026-07-14 · Source: idea-layer/screens/product/ui.yaml_

---

## 1. Feature Overview

**Name:** Product Terms  
**Archetype:** detail_screen  
**Cluster:** account-extras  
**Status:** enriched → designed  
**Quality score:** 95  
**Acceptance refs:** FR-007  

**Description:**  
Displays the product terms for a PCA or BCA account via the OBIE
`GET /accounts/{AccountId}/product` endpoint (OBReadProduct2). Shows product name/type
header, monthly maximum charge, credit interest AER tier bands (with ApplicationFrequency
and range), overdraft EAR tier bands by type, and a features list. Handles empty product
data (account types without OBProduct2 entries, e.g. GlobalMoney, Savings, CreditCard) as
a dedicated informational empty state — distinct from network errors. Requires ReadProducts
permission in the active consent. Read-only display; no mutations.

**Libraries:**

| Library | Purpose |
|---|---|
| `ktorfit` | KMP REST client for OBIE AIS endpoint |

**OBIE contract:**

| DTO | Source | Permission |
|---|---|---|
| `OBReadProduct2` | `hsbc-obie-ais-v4.0:product` | ReadProducts |

---

## 2. Screen Inventory

| Screen | Archetype | Initial state | Shell |
|---|---|---|---|
| product | detail_screen | loading | Bottom nav visible · Top app bar "Product Terms" · Back leading icon · No FAB |

### 2.1 Component Layout by State

**State: `loading`**

| Component | Type | Description |
|---|---|---|
| _(unnamed)_ | progress_indicator (variant=circular) | Shown while `GET /accounts/{id}/product` is in flight |

**State: `content`**

_Product header card_

| Component | Type | Description |
|---|---|---|
| `product_header_card` | card (elevation=2) | Product identity: OBProduct2 ProductName, ProductType, ProductId |
| `product_type_label` | text (labelMedium, color=secondary, role=overline) | OBProduct2 ProductType enum (PCA / BCA / Other) |
| `product_name` | text (headlineMedium, role=title) | Human-readable product name (e.g. "HSBC Advance Account") |
| `product_id` | text (labelSmall, color=on-surface-variant, role=caption) | Product ID label referencing `{product.ProductId}` |

_Fees section_

| Component | Type | Description |
|---|---|---|
| `fees_header` | section_header | "Fees" section divider |
| `monthly_max_charge_row` | list_item | OBPCAProductDetails1 MonthlyMaximumCharge; £0.00 for fee-free accounts |

_Credit Interest section_

| Component | Type | Description |
|---|---|---|
| `credit_interest_header` | section_header | "Credit Interest" section divider |
| `credit_interest_list` | list (items_source=`{product.PCA.CreditInterest.TierBandSet}`) | Iterates OBTierBandSet1 groups |
| `tier_band_list` | list (items_source=`{item.TierBand}`) | Iterates OBTierBand1 entries within each TierBandSet |
| `tier_band_row` | list_item | AER tier: supporting_text "Up to {item.BandLimit} · paid {item.ApplicationFrequency}"; trailing "{item.AER}% AER" (titleMedium) |

_Overdraft section_

| Component | Type | Description |
|---|---|---|
| `overdraft_header` | section_header | "Overdraft" section divider |
| `overdraft_list` | list (items_source=`{product.PCA.Overdraft.OverdraftTierBandSet}`) | Iterates OBOverdraftTierbandSet1 groups |
| `overdraft_tier_list` | list (items_source=`{item.OverdraftTierBand}`) | Iterates OBOverdraftTierBand1 entries; OverdraftType distinguishes Arranged vs Unarranged |
| `overdraft_tier_row` | list_item | EAR tier: supporting_text "{item.OverdraftType} overdraft"; trailing "{item.EAR}% EAR" (titleMedium) |

_Features section_

| Component | Type | Description |
|---|---|---|
| `features_header` | section_header | "Features" section divider |
| `features_list` | list (items_source=`{product.PCA.ProductDetails.Features}`) | Marketing/capability feature strings |
| `feature_row` | list_item (leading_icon=check_circle, leading_icon_color=primary) | Single feature string; dynamic data (i18n:skip) |

**State: `empty`**

| Component | Type | Description |
|---|---|---|
| `empty_product_state` | empty_state (variant=informational, icon=info_outline) | Shown when OBReadProduct2 Data is empty or account type (GlobalMoney, Savings, CreditCard) has no PCA/BCA entry — informational, not an error; no Retry button |

**State: `error`**

| Component | Type | Description |
|---|---|---|
| `error_state` | empty_state (variant=error, icon=error_outline) | Shown on 401 / 403 / 404 / network error; body = dynamic error message from ViewModel |
| `retry_button` | button (variant=filled) | `on_click: retry_load` |

---

## 3. State Model

**ViewModel:** `ProductViewModel`

| State | Trigger | Description |
|---|---|---|
| `loading` | `productLoad(accountId)` called | `GET /accounts/{accountId}/product` in flight |
| `content` | 200 response with non-null PCA or BCA | OBProduct2 data rendered |
| `empty` | 200 response but `Data[]` empty or PCA/BCA null | Informational — account type has no product terms |
| `error` | 4xx / network failure | Error message from ViewModel; Retry available |

**State fields:**

| Field | Type | Description |
|---|---|---|
| `product.ProductName` | String | OBProduct2 human-readable name |
| `product.ProductType` | String | OBProduct2 enum: PCA / BCA / Other |
| `product.ProductId` | String | OBProduct2 product identifier |
| `product.PCA.ProductDetails.MonthlyMaximumCharge` | String | Monthly maximum fee (£0.00 for fee-free) |
| `product.PCA.CreditInterest.TierBandSet` | List | OBTierBandSet1 groups |
| `item.TierBand` | List | OBTierBand1 entries per TierBandSet |
| `item.BandLimit` | String | Upper balance limit for this tier |
| `item.AER` | String | Annual Equivalent Rate |
| `item.ApplicationFrequency` | String | Interest payment frequency |
| `item.TierValueMinimum` | String | Lower balance limit for this tier |
| `product.PCA.Overdraft.OverdraftTierBandSet` | List | OBOverdraftTierbandSet1 groups |
| `item.OverdraftTierBand` | List | OBOverdraftTierBand1 entries |
| `item.OverdraftType` | String | Arranged / Unarranged |
| `item.EAR` | String | Effective Annual Rate for overdraft |
| `product.PCA.ProductDetails.Features` | List\<String\> | Marketing/capability feature strings |
| `error.message` | String | Localised error message emitted by ViewModel |

**VM Actions:**

| Action | Signature | Side effects |
|---|---|---|
| `productLoad` | `suspend fun productLoad(accountId: String)` | Calls `GET /accounts/{accountId}/product`; emits Loading → Content / Empty / Error |
| `retryLoad` | `suspend fun retryLoad(accountId: String)` | Delegates to `productLoad(accountId)` |

**Error cases:**

| Code | Description | ViewModel response |
|---|---|---|
| HTTP 401 | PSU access token expired | `Error("Session expired. Please re-authenticate.")` |
| HTTP 403 | Consent does not include ReadProducts | `Error("Consent does not include ReadProducts.")` |
| HTTP 404 | No OBProduct2 record for AccountId | `Error("No product data available for this account.")` |
| NETWORK_ERROR | Device offline or endpoint unreachable | `Error(e.localizedMessage)` |
| EMPTY_DATA | 200 but Data[] empty or PCA/BCA null | Emit `Empty` (informational; no Retry button) |

**Capability completeness:**

| Gate | Implementation |
|---|---|
| CC5 (permission visibility) | ReadProducts required; 403 error message explicitly states missing scope |
| CC7 (network data policy) | No caching; always-fresh fetch on mount (`cache_strategy: none`) |
| CC8 (cache lifecycle) | No local cache; prevents stale charge information after bank updates |
| CC9 (error recovery) | Retry button always visible in error state; empty state intentionally has no Retry |

---

## 4. Navigation

| Entry | Source | Trigger |
|---|---|---|
| → product | account-detail | Tap Product chip or menu entry |

| From | To | Trigger |
|---|---|---|
| product | account-detail | Back navigation (top app bar back icon or system gesture) |

---

## 5. API Dependencies

| Endpoint | Method | Permission | Auth |
|---|---|---|---|
| `/accounts/{AccountId}/product` | GET | ReadProducts | Bearer PSU token |

**Request path param:**

| Param | Type | Description |
|---|---|---|
| `AccountId` | String | OBIE account identifier from accounts list |

**Response shape (summary):**

```
OBReadProduct2
  └── Data: List<OBProduct2>
        └── OBProduct2
              ├── ProductName: String
              ├── ProductType: Enum (PCA | BCA | Other)
              ├── ProductId: String
              └── PCA: OBPCAData1
                    ├── ProductDetails: OBPCAProductDetails1
                    │     ├── MonthlyMaximumCharge: String
                    │     └── Features: List<String>
                    ├── CreditInterest: OBCreditInterest1
                    │     └── TierBandSet: List<OBTierBandSet1>
                    │           └── TierBand: List<OBTierBand1>
                    │                 ├── TierValueMinimum: String
                    │                 ├── BandLimit: String (upper bound)
                    │                 ├── AER: String
                    │                 └── ApplicationFrequency: Enum
                    └── Overdraft: OBOverdraft1
                          └── OverdraftTierBandSet: List<OBOverdraftTierbandSet1>
                                └── OverdraftTierBand: List<OBOverdraftTierBand1>
                                      ├── OverdraftType: Enum (Arranged | Unarranged)
                                      └── EAR: String
```

---

## 6. Design Tokens

Design system: **Open Banking — Trust Blue** (Material 3, seed `#266489`, aesthetic: minimalist-ui)

| Token | Value | Usage in this feature |
|---|---|---|
| `colors.primary` | `#266489` | `check_circle` feature icon, active nav |
| `colors.secondary` | `#50606E` | Product type overline label |
| `colors.on_surface_variant` | `#41474D` | Product ID caption, section headers |
| `colors.error` | `#BA1A1A` | Error state icon |
| `colors.surface_container` | `#EBEEF3` | Product header card background |
| `typography.headlineMedium` | 28sp / 400 | Product name (title) |
| `typography.titleMedium` | 16sp / 500 | AER and EAR trailing values |
| `typography.labelMedium` | 12sp / 500 | Product type overline, section headers |
| `typography.labelSmall` | 11sp / 500 | Product ID caption |
| `typography.bodyMedium` | 14sp / 400 | Tier band supporting text |
| `typography.mono` (Roboto Mono) | — | AER / EAR / charge amounts for readability |
| `spacing.screen_padding` | 16dp | Horizontal screen padding |
| `rounded.medium` | 12dp | Product header card radius |
| `accessibility.min_touch_target_dp` | 48dp | Retry button |
