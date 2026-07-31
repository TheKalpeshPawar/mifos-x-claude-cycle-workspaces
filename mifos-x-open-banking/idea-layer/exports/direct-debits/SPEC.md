# Direct debits — Feature Specification

> Generated from `screens/direct-debits/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `dc2ab5eef0fa`
> Endpoints: 1 · DTOs: 1 · Components: 7 · Test scenarios: 9

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

Read-only list of direct-debit mandates from `OBReadDirectDebit2`. Summary chips (Active /
Inactive count), then cards sorted Active-first showing originator name, status badge, previous
payment amount and collection date.

| Attribute | Value |
|---|---|
| Feature ID | `direct-debits` · Flow `recurring-and-statements` · Cluster payments-context |
| Priority | should (FR-006) · Status approved · quality 95 |
| Archetype | index_list · Route `DirectDebitsRoute(accountId: String)` |
| Source module | `feature/direct-debits` — **implemented** |

**This is the canonical single-stream feature template.** Copy its anatomy for a new
account-scoped screen; it has no `components/` package, which is the point — add one only when
a composable is shared across states.

## 2. Screen inventory

`loading_skeleton` (skeleton) · `back_button` · `mandate_summary_chips` (chip_group) ·
`direct_debits_list` (list) · `empty_direct_debits` · **`unsupported_direct_debits`** ·
`error_state`.

File layout: `DirectDebitsScreen.kt` (internal Screen + internal `DirectDebitsScreenContent`
hand-written `when`), then one file per state — `Content/Skeleton/Empty/Error/Unsupported.kt`.

## 3. State model — `DirectDebitsViewModel`

**Fields:** `accountId: String` · `uiState: DirectDebitsUiState` · **Default:** `Loading`
**UiState:** `Loading` · `Content` · `Empty` · **`Unsupported`** · `Error`
**Error kinds:** `TokenExpired` · `ConsentRevoked` · `RateLimited` · `ServerError` ·
`NetworkError` — keyed on **`isRetriable`** (account-detail's keys on `recoverable`; copy the
shape, not the enum)
**Actions:** `RetryLoad` · **Events:** none · **DI:** `SavedStateHandle` · `DirectDebitsRepository`

### `Unsupported` is checked before error classification

A `U000` refusal is a statement about the **product**, not a retryable failure:

```kotlin
is ScreenState.Error -> if (error.isUnsupportedForProduct()) {
    DirectDebitsUiState.Unsupported(error.obieMessage().orEmpty())
} else {
    DirectDebitsUiState.Error(classifyDirectDebitsError(error))
}
```

Get this order wrong and a savings account shows a Retry button that can never succeed.
`Unsupported` is a **terminal** state — no Retry.

Stateless-gateway repository; ViewModel owns the stream; `RetryLoad → stream.refresh()`;
structural empty via `emptyIfContent { summary.isEmpty }`.

## 4. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `account-detail` | Direct Debits Explore option | `direct-debits` (accountId) |
| top-app-bar leading | back | `account-detail` |

**Gated chip** — `DirectDebits` = {PersonalCurrentAccount} **only**, the narrowest of the five.

### Nav-arg pinning

`ACCOUNT_ID_ARG` must equal `DirectDebitsRoute`'s property name. This feature's test asserts
only `assertEquals("accountId", …ACCOUNT_ID_ARG)`, which never reads the route and **still
passes after a rename** — write the serial-descriptor form instead (see
`exports/account-detail/SPEC.md#3`).

## 5. API dependencies

| ID | Method | Path | Permission | Response DTO |
|---|---|---|---|---|
| `direct-debits-list` | GET | `/accounts/{AccountId}/direct-debits` | ReadDirectDebits | `OBReadDirectDebit2` |

### Error matrix

| HTTP | Kind | Retry? |
|---|---|:--:|
| 400 `U000` | **`Unsupported`** (not an error kind) | ✗ terminal |
| 401 | `TokenExpired` | ✅ |
| 403 | `ConsentRevoked` | ✗ |
| 429 | `RateLimited` | ✅ back-off |
| 500 | `ServerError` | ✅ |
| — | `NetworkError` | ✅ |

## 6. Design tokens

`list_item`, `chip` status badges, `amount` (mono, formatted in the ViewModel —
`formatMandateDate` returns an unparseable date **unchanged** rather than blanking it: a value
the bank did send is more useful in an odd format than silently dropped).
Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 7. Test mapping

TC-DD-001 mandates render · 002 skeleton · 003 empty · 004 401 + Retry · 005 back ·
006 **403 without Retry** · 007 429 with Retry · 008 network + Retry · 009 i18n coverage
→ `feature/direct-debits/src/commonTest/.../DirectDebitsViewModelTest.kt` +
`androidUnitTest/.../DirectDebitsScreenRobolectricTest.kt` +
`androidInstrumentedTest/.../DirectDebitsScreenInstrumentedTest.kt`.

TC-DD-006 pins the differentiated recovery — 403 must **not** offer Retry.

> **Gap:** no scenario covers the `Unsupported` state, despite it being this feature's most
> distinctive behaviour and the reason `DirectDebitsUnsupported.kt` exists. Recorded, not
> invented.

## 8. Notes

`build.gradle.kts:38-53` + its `android { }` block is the reference dependency block for a
store-backed screen feature. It includes `commonTest { implementation(projects.core.network) }`
— without it a fake typed on `NetworkResult`/`NetworkError` will not compile.
