# Consent list — Feature Specification

> Generated from `screens/consent-list/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `30c96226cc2a`
> Endpoints: 1 · DTOs: 1 · Components: 10 · Test scenarios: 8

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

Consent management list, reachable from More → Settings → Consents. Partitions locally-stored
HSBC consents into **Active** (`Authorised`) and **History** (`Expired`/`Revoked`) sections
separated by a divider. Active cards show the OBIE status chip, permission count, expiry
countdown and connection date. At ≤14 days to expiry a reconfirm urgency chip renders on the
card and a warning banner appears at the top of the list.

| Attribute | Value |
|---|---|
| Feature ID | `consent-list` |
| Cluster | consent |
| Priority | must (FR-008) |
| Status | approved · quality 95 |
| Archetype | index_list |
| Source module | `feature/consent-list` — **implemented** |

**Single current consent in practice.** The screen reads `session.consentId()` — the current
connection only; there is no device-side consent history. `null` → Empty "Connect HSBC".

## 2. Screen inventory

| Component | Type | Bound states |
|---|---|---|
| (unnamed) | progress_indicator | loading |
| `reconfirm_banner` | banner | content (≤14 days to expiry) |
| `active_section_label` + `active_consents_list` | text, list | content |
| `section_divider` | divider | content |
| `history_section_label` + `history_consents_list` | text, list | content |
| `empty_state` · `error_state` · `auth_error_state` | empty_state ×3 | empty, error, error_auth |

## 3. State model — `ConsentListViewModel`

**State fields:** `consents: List<OBReadConsentResponse1>` · `uiState: ConsentListUiState`
**State defaults:** `uiState = Loading` (`initial_state: loading`)

| UiState | Meaning |
|---|---|
| `Loading` | consent-status fetch in flight |
| `Content` | active + history partitions rendered |
| `Empty` | no local consent id — offer "Connect HSBC" |
| `Error` | generic non-auth failure |
| `ErrorAuth` | **dedicated** 401 state with a sign-in-again CTA |

**Error kinds:** `NetworkError` · `TokenExpiredSession` · `ConsentStatusServerError`
**Actions:** `RetryLoad`
**Nav callbacks** (host-owned, not action members): `onBack → popBackStack()` ·
`onNavigateToDetail(consentId)` · `onConnectBank → LoginRenewRoute` ·
`onReauthenticate → LoginRenewRoute`
**DI:** `ConsentDetailRepository` · `ConsentSession`

`ErrorAuth` is a separate UiState rather than an `Error` variant because its recovery differs
in kind: a 401 needs re-authentication, not a retry of the same call.

## 4. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `app_shell_more_menu` | More / Settings → Consents | `consent-list` |
| consent card tap | active or history | `consent-detail` (consentId) |
| `empty_state` CTA | "Connect HSBC" | `user-onboarding` / `LoginRenewRoute` |
| `auth_error_state` CTA | "Sign in again" | `login` |

Reconfirm / renew all route to `LoginRenewRoute` — the login screen reached **inside** the
authenticated host, without the onboarding intro.

## 5. API dependencies

| ID | Method | Path | Auth | Response DTO |
|---|---|---|---|---|
| `consent-status` | GET | `/account-access-consents/{ConsentId}` | CC bearer | `OBReadConsentResponse1` |

Full contract in `API.md`.

### Error matrix

| HTTP | Kind | UiState | Recovery |
|---|---|---|---|
| 401 | `TokenExpiredSession` | `ErrorAuth` | Sign in again → `login` |
| 5xx | `ConsentStatusServerError` | `Error` | Retry |
| — | `NetworkError` | `Error` | Retry |
| — (no local consentId) | — | `Empty` | Connect HSBC |

## 6. Design tokens

`design-tokens.yaml` 2.1.0 — OBIE status chip colour-coded per consent state; `banner` for the
≤14-day reconfirm warning; `divider` separating Active from History. Note the divider here is
a deliberate exception to the system's usual whitespace-over-rules grouping, because the two
partitions carry different semantics rather than being a continuation.
Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 7. Test mapping

| TC | Assertion | Expected path |
|---|---|---|
| TC-CLIST-001 | authorised card renders all required fields | `feature/consent-list/src/commonTest/.../ConsentListViewModelTest.kt` |
| TC-CLIST-002 | loading during consent-status | ↑ |
| TC-CLIST-003 | empty when no local consent ids | ↑ |
| TC-CLIST-004 | generic error on non-auth failure | ↑ |
| TC-CLIST-005 | card tap → consent-detail | ↑ |
| TC-CLIST-006 | ≤14 days shows reconfirm urgency chip | ↑ |
| TC-CLIST-007 | expired consent falls into History below the divider | ↑ |
| TC-CLIST-008 | **401 shows the dedicated auth error state**, not generic | `ConsentListScreenRobolectricTest.kt` |

Ships a Roborazzi screenshot suite with committed goldens under
`src/androidUnitTest/screenshots/`.

## 8. Notes

`docs.yaml` declares no `flow_ref` despite `flows/consent-management.yaml` existing.
