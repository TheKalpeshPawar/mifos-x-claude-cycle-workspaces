# Beneficiaries — Feature Specification

> Generated from `screens/beneficiaries/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `f54a4a1ddab7`
> Endpoints: 1 · DTOs: 1 · Components: 7 · Test scenarios: 10

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

Read-only list of saved payees for an account, from `OBReadBeneficiary5`. Displays avatar
initials, creditor name, scheme-type label (Sort Code / IBAN / Paym), account identifier and
payment reference. Supports client-side search by name **or** reference.

| Attribute | Value |
|---|---|
| Feature ID | `beneficiaries` · Flow `recurring-and-statements` · Cluster payments-context |
| Priority | should (FR-006) · Status approved · quality 95 |
| Archetype | index_list · Route `BeneficiariesRoute(accountId: String)` |
| Source module | `feature/beneficiaries` — **implemented** |

**The plainest account-scoped list template.** Its empty state points the PSU at Settings for
consent management rather than offering its own connect button — the connect/renew affordance
lives only on the consent screens.

## 2. Screen inventory

`progress_indicator` (loading) · `back_button` (icon_button) · `beneficiary_search` (search_bar,
content) · `beneficiaries_list` (list, content) · `search_no_results` (empty_state, *within*
content) · `empty_beneficiaries` (empty_state) · `error_state` (empty_state).

Two distinct empties: `search_no_results` renders inside `content` when the filter matches
nothing; `empty_beneficiaries` is the zero-payee state. Conflating them would tell a PSU with
five payees that they have none.

## 3. State model — `BeneficiariesViewModel`

**Fields:** `accountId: String` · `uiState: BeneficiariesUiState`  · **Default:** `Loading`
**UiState:** `Loading` · `Content` · `Empty` · `Error`
**Error kinds:** `TokenExpiredError` · `ConsentRevokedError` · `RateLimitedError` ·
`NetworkError` · `ServerError`
**Actions:** `RetryLoad` · `Search` (client-side filter — no API round-trip)
**Events:** none (`E = Nothing`) · **DI:** `SavedStateHandle` · `BeneficiariesRepository`

Stateless-gateway repository: the ViewModel owns the `ScreenDataStream`; `RetryLoad` calls
`stream.refresh()`. Structural empty via `emptyIfContent { it.isEmpty() }`.

## 4. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `account-detail` | Beneficiaries Explore option | `beneficiaries` (accountId) |
| top-app-bar leading | back | `account-detail` |
| `view_consents_button` | 403 ConsentRevoked | `consent-list` |

**Gated chip** — Beneficiaries is offered on every product *except* a credit card.

## 5. API dependencies

| ID | Method | Path | Permission | Response DTO |
|---|---|---|---|---|
| `beneficiaries-list` | GET | `/accounts/{AccountId}/beneficiaries` | ReadBeneficiariesDetail | `OBReadBeneficiary5` |

### Error matrix

| HTTP | Kind | Retry? | Recovery |
|---|---|:--:|---|
| 401 | `TokenExpiredError` | ✅ | Retry re-fetches; VM clears the stale token |
| 403 | `ConsentRevokedError` | ✗ | **View Consents** → consent-list |
| 429 | `RateLimitedError` | ✅ | exponential back-off |
| 500 | `ServerError` | ✅ | Retry |
| — | `NetworkError` | ✅ | Retry |

Recovery is differentiated: Retry for transient failures, View Consents for 403. A single
generic Retry would loop forever on a revoked consent.

## 6. Design tokens

`list_item` two-line with a leading initials `avatar` (`aria_hidden` — decorative, the row's
accessibility label carries the content), `chip` scheme label, `search_bar`.
Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 7. Test mapping

TC-BEN-001 list renders five payees · 002 loading · 003 zero-payee empty · 004 401 + Retry ·
005 back → account-detail · 006 **search by creditor name** · 007 search no-results *within*
content · 008 403 + View Consents · 009 avatar initials · 010 **search by payment reference**
→ `feature/beneficiaries/src/commonTest/.../BeneficiariesViewModelTest.kt` +
`androidUnitTest/.../BeneficiariesScreenRobolectricTest.kt`.

Ships Roborazzi goldens. Its `build.gradle.kts:38-58` is the fuller reference block — it wires
Roborazzi **and** the `*ScreenUiTest`/`*ActionTest` exclusion filter.

## 8. Notes

`docs.yaml` declares `flow_ref: recurring-and-statements` — one of only 9 of 23 features that
declare one.
