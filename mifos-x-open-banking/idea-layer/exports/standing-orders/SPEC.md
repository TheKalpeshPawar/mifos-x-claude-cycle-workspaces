# Standing orders — Feature Specification

> Generated from `screens/standing-orders/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `184752493fd0`
> Endpoints: 1 · DTOs: 1 · Components: 7 · Test scenarios: 12

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

Read-only list of recurring outbound standing orders from `OBReadStandingOrder6`. Shows payee,
status badge, next payment amount, **human-readable frequency**, next and optional final
payment date, sort code / account number and reference.

| Attribute | Value |
|---|---|
| Feature ID | `standing-orders` · Flow `recurring-and-statements` · Cluster payments-context |
| Priority | should (FR-006) · Status approved · quality 95 |
| Archetype | index_list · Route `StandingOrdersRoute(accountId: String)` |
| Source module | `feature/standing-orders` — **implemented** |

## 2. Screen inventory

`progress_indicator` · `back_button` · `summary_row` (text) · `standing_orders_list` ·
`empty_standing_orders` · **`unsupported_standing_orders`** · `error_state`.

## 3. State model — `StandingOrdersViewModel`

**Fields:** `accountId` · `uiState: StandingOrdersUiState` · **Default:** `Loading`
**UiState:** `Loading` · `Content` · `Empty` · **`Unsupported`** · `Error`
**Error kinds:** `TokenExpired` · `ConsentRevoked` · `RateLimited` · `ServerError` · `NetworkError`
**Actions:** `RetryLoad` · **Events:** none · **DI:** `SavedStateHandle` · `StandingOrdersRepository`

Same shape as `direct-debits`: `isUnsupportedForProduct()` checked **before** classification,
`Unsupported` terminal. Stateless-gateway repository; ViewModel owns the stream.

### Frequency decoding

The OBIE `Frequency` is a machine code, not display text. `IntrvlWkDay:01:5` decodes to
"Weekly on Fridays" (TC-SO-009). Decoding happens in the **ViewModel**, so composables receive
a finished string — consistent with money and dates throughout the app.

## 4. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `account-detail` | Standing Orders Explore option | `standing-orders` (accountId) |
| top-app-bar leading | back | `account-detail` |

**Gated chip** — `StandingOrders` = {PersonalCurrentAccount, ForeignCurrency}.

## 5. API dependencies

| ID | Method | Path | Permission | Response DTO |
|---|---|---|---|---|
| `standing-orders-list` | GET | `/accounts/{AccountId}/standing-orders` | ReadStandingOrdersDetail | `OBReadStandingOrder6` |

Error matrix identical to `direct-debits` — see `exports/direct-debits/API.md`, with
`AccountEndpoint.StandingOrders` as the recorded endpoint (`BankingStores.kt:320`).

## 6. Design tokens

`list_item`, `chip` status badge (Active `primary` / Inactive `secondary`), `amount` mono.
Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 7. Test mapping

TC-SO-001 active orders render · 002 loading · 003 empty · 004 401 + Retry · 005 back ·
006 inactive secondary badge · 007 403 distinct message · 008 429 specific message ·
009 **`IntrvlWkDay:01:5` decodes** · 010 **pull-to-refresh re-triggers load** ·
011 accessibility labels on all interactive elements + key data · 012 network error message
→ `feature/standing-orders/src/commonTest/.../StandingOrdersViewModelTest.kt` + Robolectric +
instrumented.

Twelve scenarios — the most of any payments-context feature, and the only one covering
pull-to-refresh and a systematic accessibility sweep.

> **Gap:** as with `direct-debits`, no scenario covers the `Unsupported` state.

## 8. Notes

`docs.yaml` declares `flow_ref: recurring-and-statements`.
