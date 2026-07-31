# Product — Feature Specification

> Generated from `screens/product/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `c67110ce2e1d`
> Endpoints: 1 · DTOs: 1 · Components: 12 · Test scenarios: 9

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

Product terms for a PCA or BCA account: product name/type header, monthly maximum charge,
credit-interest AER tiers, overdraft EAR tiers by type, and a feature list.

| Attribute | Value |
|---|---|
| Feature ID | `product` · Cluster account-extras |
| Priority | could (FR-007) · Status approved · quality 95 |
| Archetype | detail_screen · Route `ProductRoute(accountId: String)` |
| Source module | `feature/product` — **implemented** |

## 2. The only storeless screen — do not copy

**`product` is the one feature not backed by a stream.** `data-flow.yaml` declares
`cache_strategy: none`, and `ProductRepository.getProduct(accountId): NetworkResult<ProductTerms?, NetworkError>`
is a bare `suspend` call over `Aisp.getProduct` — no store, no `AppStoreRegistry` qualifier, no
`registerForLogout`. The ViewModel maps the raw `NetworkResult` onto Loading/Content/Empty/Error
by hand instead of inheriting `ScreenDataStream`'s machinery.

**Why:** the bank can revise product terms, and a cached copy would misstate the charges a
customer is subject to. Do not copy this shape unless the data genuinely must not be cached.

Its fake therefore returns a `NetworkResult` directly, with no buffered refresh trigger — the
`replay = 16` rule for `ScreenDataStream` fakes does not apply.

## 3. Screen inventory

`progress_indicator` · `product_header_card` · `fees_header` + `monthly_max_charge_row` ·
`credit_interest_header` + `credit_interest_list` · `overdraft_header` + `overdraft_list` ·
`features_header` + `features_list` · `empty_product_state` · `error_state`.

## 4. State model — `ProductViewModel`

**Fields:** `accountId` · `product: ProductTerms?` · `uiState: ProductUiState` · **Default:** `Loading`
**UiState:** `Loading` · `Content` · `Empty` · `Error`
**Error kinds:** `TokenExpiredError` · `ConsentScopeError` · `ProductNotFoundError` · `NetworkError`
**Actions:** `ProductLoad` · `RetryLoad` · **Events:** none · **DI:** `SavedStateHandle` · `ProductRepository`

### Two different outcomes both mean Empty

A `Success(null)` — the mapper found neither a `PCA` nor a `BCA` block, the normal answer for
GlobalMoney, Savings and CreditCard — **and an HTTP 404** both render Empty. Neither is a
failure a customer can act on, so neither gets the error icon or a Retry. 401 / 403 / transport
keep the error state.

## 5. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `account-detail` | Product Explore option | `product` (accountId) |
| top-app-bar leading | back | `account-detail` |

**Ungated** — a product either exists or the empty state explains it. Shipped by repointing the
existing `AccountDetailChip.Product` branch off the dead `ProductsRoute` placeholder, so the
nine-chips-in-order suites stayed green.

## 6. API dependencies

| ID | Method | Path | Permission | Response DTO |
|---|---|---|---|---|
| `product` | GET | `/accounts/{AccountId}/product` | ReadProducts | `OBReadProduct2` |

Full contract in `API.md`.

## 7. Design tokens

`card`, `section_header` ×4, `list_item` rows for tiers.

> **The `%%` trap.** Compose Multiplatform's resource formatter does **not** collapse Android's
> `%%` escape, so `"%1$s%% AER"` renders `0.15%% AER`. Write a single `%`. No assertion catches
> this — tags and counts pass — so **look at a screenshot golden** after touching any templated
> string. This feature shipped exactly that defect with every test green.

## 8. Test mapping

TC-PROD-001 all sections render · 002 loading · 003 403 ReadProducts + Retry · 004 401 ·
005 **empty for account types with no OBProduct2 entry** · 006 **empty on 404** · 007 back ·
008 BCA renders from the `BCA` block · 009 network failure
→ `feature/product/src/commonTest/.../ProductViewModelTest.kt` + Robolectric. Ships Roborazzi
goldens.

## 9. Stale-artifact fix applied 2026-07-30

A **three-way contradiction** on 404 handling:

| Artifact | Said |
|---|---|
| `data-flow.yaml:29-33` | `state: empty` — with a comment citing api.yaml as its authority |
| `api.yaml:18-19` | "ViewModel emits Error(...)" |
| `tests.yaml` TC-PROD-006 | `state: error` |

Resolved to **empty**: a bank holding no product record is not a failure the customer can act
on, and it is the same outcome as TC-PROD-005 reached by a different route. `api.yaml` and
TC-PROD-006 were corrected; `data-flow.yaml` was already right. All three now agree.

`docs.yaml` declares no `flow_ref`.
