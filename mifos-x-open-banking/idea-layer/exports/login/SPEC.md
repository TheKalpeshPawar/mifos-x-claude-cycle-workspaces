# Login — Feature Specification

> Generated from `screens/login/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `e38de56e4e0b`
> Endpoints: 1 · DTOs: 2 · Components: 14 · Test scenarios: 8

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

OAuth/FAPI initiation. Displays the OBIE read permissions being staged in `OBReadConsent1` so
the PSU understands what HSBC will ask them to approve. On "Continue to HSBC" the app POSTs
consent-create (client_credentials grant), builds a PS256-signed FAPI 1.0 Advanced `/authorize`
URL (`response_type=code id_token`) and launches an app-to-app redirect for SCA and account
selection.

| Attribute | Value |
|---|---|
| Feature ID | `login` |
| Cluster | consent |
| Priority | must (FR-001, FR-002) |
| Status | approved · quality 95 |
| Archetype | login |
| Source module | `feature/login` — **implemented** |

**Two routes ship from one screen:** `LoginRoute` (onboarding entry) and `LoginRenewRoute`
(reached inside the authenticated host from Consents, without the onboarding intro).

## 2. Screen inventory

| Component | Type | Bound states |
|---|---|---|
| `loading_indicator` + `loading_label` | progress_indicator, text | loading |
| `authorising_spinner` + `authorising_label` + `authorising_hint` | progress_indicator, text ×2 | authorising |
| `hsbc_explainer_card` | card | content |
| `permissions_header` + `permissions_list` | section_header, list | content |
| `consent_validity_note` + `consent_expiry_display` | text ×2 | content |
| `continue_hsbc_button` · `cancel_button` | button ×2 | content |
| `error_state` · `login_empty_state` | empty_state ×2 | error, empty |

## 3. State model — `LoginViewModel`

**State fields:** `uiState: LoginUiState`
**State defaults:** `uiState = Content` (`initial_state: content` — the permission list is
static config, so there is no cold-start fetch)

| UiState | Meaning |
|---|---|
| `Loading` | consent-create POST in flight |
| `Content` | permissions rendered, CTA enabled |
| `Authorising` | holding UI after the app-to-app redirect fires |
| `Empty` | no OBIE permissions configured — CTA suppressed |
| `Error` | consent-create failed |

**Actions:** `LoadPermissionsConfig` · `StartOAuth` · `Cancel` · `Retry`
**Events:** none — navigation is the screen's job (`E = Nothing`)
**DI:** `LoginRepository` · `BrowserLauncher` · `PendingAuthStore`

`StartOAuth` stashes `state`, `nonce` and `consentId` in `PendingAuthStore` **before**
launching the browser — `consent-callback` consumes them single-use on the return leg.

## 4. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `user-onboarding` | "Connect with HSBC" | `login` |
| app-shell (authenticated) | Consents → Connect / reconfirm / renew | `LoginRenewRoute` |
| `continue_hsbc_button` | consent staged, authorize URL built | HSBC browser → `consent-callback` |
| `cancel_button` | Cancel | `user-onboarding` |

## 5. API dependencies

| ID | Method | Path | Auth | Response DTO |
|---|---|---|---|---|
| `consent-create` | POST | `/account-access-consents` | CC token | `OBReadConsentResponse1` |

Request DTO `OBReadConsent1`. Full contracts in `API.md`.

### Error matrix

| Condition | UI | Recovery |
|---|---|---|
| consent-create failure | `Error` | Retry re-issues consent-create |
| network failure | `Error` with user-friendly copy | Retry |
| no OBIE permissions configured | `Empty` | CTA suppressed — cannot stage an empty consent |

## 6. Design tokens

`design-tokens.yaml` 2.1.0 — `card` on `surfaceContainer` for the explainer, `section_header`
(`titleSmall`/`onSurfaceVariant`) for the permissions group, `button_filled` (`primary`, pill)
for the CTA. Motion stays at dial 2. Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 7. Test mapping

| TC | Assertion | Expected path |
|---|---|---|
| TC-LOGIN-001 | all 10 OBIE read permissions + consent validity render | `feature/login/src/commonTest/.../LoginViewModelTest.kt` |
| TC-LOGIN-002 | loading during consent-create | ↑ |
| TC-LOGIN-003 | error on consent-create failure, friendly copy | ↑ |
| TC-LOGIN-004 | Cancel → onboarding | ↑ |
| TC-LOGIN-005 | success stores ConsentId, transitions to authorising | ↑ |
| TC-LOGIN-006 | authorising holding UI after FAPI redirect | ↑ |
| TC-LOGIN-007 | network error message | ↑ |
| TC-LOGIN-008 | empty state prevents consent-create with no permissions | `LoginScreenRobolectricTest.kt` |

## 8. Notes

`docs.yaml` declares no `flow_ref`. The onboarding-consent flow exists at
`flows/onboarding-consent.yaml` but is not back-referenced from this feature — one of 14
features in that condition (see `/idea-data-flow` flow_ref coverage finding).
