# Consent detail — Feature Specification

> Generated from `screens/consent-detail/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `b6bb85d0ec32`
> Endpoints: 2 · DTOs: 1 · Components: 13 · Test scenarios: 11

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

Full consent detail: colour-coded OBIE status badge, all granted permissions with
human-readable labels, creation / expiry / transaction-from / transaction-to dates, an expiry
warning banner within 7 days, a 90-day reconfirm prompt, and a two-step destructive
**Revoke access** action.

| Attribute | Value |
|---|---|
| Feature ID | `consent-detail` |
| Cluster | consent |
| Priority | must (FR-008) |
| Status | approved · quality 95 |
| Archetype | detail_screen |
| Source module | `feature/consent-detail` — **implemented** |

**Revoke is the app's sole logout path.** It is not a back-navigation.

## 2. Screen inventory

| Component | Type | Bound states |
|---|---|---|
| `load_progress` · `revoke_progress` | progress_indicator ×2 | loading, revoking |
| `status_header_card` | card | content |
| `expiry_warning_banner` | card | content (≤7 days) |
| `dates_header` + `dates_list` | section_header, list | content |
| `reconfirm_button` | button | content |
| `permissions_header` + `permissions_list` | section_header, list | content |
| `revoke_button` | button | content |
| `revoke_confirm_dialog` | dialog | revoke_confirm |
| `error_state` · `empty_state` | empty_state ×2 | error, empty |

## 3. State model — `ConsentDetailViewModel`

**State fields:** `consentId: String` (nav arg) · `uiState: ConsentDetailUiState`
**State defaults:** `uiState = Loading` (`initial_state: loading`)

| UiState | Meaning |
|---|---|
| `Loading` | consent-status GET in flight |
| `Content` | status header, permissions, dates rendered |
| `RevokeConfirm` | dialog gate open — **no API call yet** |
| `Revoking` | lock-state; `AppLogout` running |
| `Empty` | consent resolves but carries no record |
| `Error` | typed failure |

**Error kinds:** `ConsentNotFoundError` · `ConsentRevokedError` · `ConsentExpiredError` ·
`TokenExpiredError` · `NetworkError` · `RevokeServerError`
**Actions:** `RetryLoad` · `ConfirmRevoke` · `DismissRevokeConfirm` · `ExecuteRevoke`
**Nav callbacks:** `onBack → popBackStack()` · `onReconfirm → LoginRenewRoute` ·
`onLoggedOut → bubbles to the root navigator, which returns the PSU to onboarding`
**DI:** `SavedStateHandle` · `ConsentDetailRepository` · `AppLogout`

### Two-step revoke — an irreversible-action surface

`ConfirmRevoke` opens the dialog gate and makes **no API call**. Only `ExecuteRevoke` moves to
the `Revoking` lock-state and calls the shared `AppLogout`. This matches the
`irreversible_action` contract in `design-tokens.yaml` 2.1.0: a distinct confirmation surface,
a same-weight escape ("Keep access"), and a locked CTA on tap.

### `AppLogout` — the one logout path

`core/data/.../user/AppLogout.kt`, Koin `single`. Runs in order:

1. best-effort `consentRevokeRepository.revokeConsent(consentId())` wrapped in `runCatching` —
   an expired / revoked / 404 / network consent still proceeds
2. `consentSession.forgetAll()` — removes the PSU tokens. **This is the actual logout**: the
   tokens live in secure `Settings` via `SettingsConsentSession`, not the DataStore `UserData`,
   so `clearUserData()` alone cannot sign the user out
3. `userDataRepository.clearUserData()` + `storeCacheManager.clearAll()`

Never re-implement this sequence for a new sign-out surface.

Navigation after logout is **explicit**: the event bubbles through `onLoggedOut` threaded
`RootNavScreen → authenticatedGraph → authenticatedNavbarGraph →
AuthenticatedNavbarNavigationScreen → consentDetailScreen`. Nothing observes the session
reactively, deliberately.

## 4. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `consent-list` | tap a consent card | `consent-detail` (consentId) |
| — | revoke succeeded | root navigator → `authGraph` (onboarding) |
| `reconfirm_button` | "Reconfirm before expiry" | `LoginRenewRoute` |

## 5. API dependencies

| ID | Method | Path | Auth | Response DTO |
|---|---|---|---|---|
| `consent-status` | GET | `/account-access-consents/{ConsentId}` | CC bearer | `OBReadConsentResponse1` |
| `consent-revoke` | DELETE | `/account-access-consents/{ConsentId}` | CC bearer | — (`204`) |

Full contracts in `API.md`.

### Error matrix

| HTTP | Kind | Retry? | Recovery |
|---|---|:--:|---|
| 404 on GET | `ConsentNotFoundError` | ✗ | Error state; treat as already gone |
| 403 / revoked | `ConsentRevokedError` | ✗ | Error state |
| expired | `ConsentExpiredError` | ✗ | reconfirm CTA |
| 401 | `TokenExpiredError` | ✅ | re-authenticate |
| 5xx on DELETE | `RevokeServerError` | ✅ | Retry the revoke |
| — | `NetworkError` | ✅ | Retry |
| **404 on DELETE** | — | — | **treated as already-revoked** — clean local state, not an error |

That last row matters: a consent the bank has already dropped should not block the PSU from
signing out.

## 6. Design tokens

`design-tokens.yaml` 2.1.0 — status badge colour-coded (`primary`=Authorised,
warning=Expired, `error`=Revoked/Rejected); `irreversible_action` governs the revoke gate.
Note the revoke CTA **is** `error`-coloured, unlike `send-money`'s confirm — revoking is
genuinely destructive of access, whereas a payment is an intended action.
Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 7. Test mapping

| TC | Assertion | Expected path |
|---|---|---|
| TC-CDETAIL-001 | content renders status header, permissions, all four dates | `feature/consent-detail/src/commonTest/.../ConsentDetailViewModelTest.kt` |
| TC-CDETAIL-002 | loading during consent-status GET | ↑ |
| TC-CDETAIL-003 | Revoke → `revoke_confirm`, **no API call** | ↑ |
| TC-CDETAIL-004 | "Keep access" returns to content unchanged | ↑ |
| TC-CDETAIL-005 | confirm → revoking → `AppLogout` | ↑ |
| TC-CDETAIL-006 | 404 on GET → error | ↑ |
| TC-CDETAIL-007 | revoke network failure → error with retry | ↑ |
| TC-CDETAIL-008 | **404 on DELETE = already-revoked**, clean local state | ↑ |
| TC-CDETAIL-009 | expired renders warning-colour chip | ↑ |
| TC-CDETAIL-010 | expiry banner within 7 days | ↑ |
| TC-CDETAIL-011 | empty when consent carries no record | `ConsentDetailScreenRobolectricTest.kt` |

Ships a Roborazzi screenshot suite with committed goldens.

## 8. Notes

`docs.yaml` declares no `flow_ref` despite `flows/consent-management.yaml` existing.
