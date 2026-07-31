# Consent callback — Feature Specification

> Generated from `screens/consent-callback/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `a5072ad77719`
> Endpoints: 2 · DTOs: 2 · Components: 6 · Test scenarios: 6

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

Return leg from HSBC's authorisation portal. Validates the FAPI `state` parameter and the
hybrid-flow `id_token` nonce on arrival, surfacing `security_error` immediately on mismatch.
Handles OAuth error redirects (`error=access_denied`) **without attempting token exchange**.
On a valid code it exchanges for a PSU bearer token (authorization_code grant,
`private_key_jwt` client auth) and stores tokens in encrypted storage.

| Attribute | Value |
|---|---|
| Feature ID | `consent-callback` |
| Cluster | consent |
| Priority | must (FR-002) |
| Status | approved · quality 95 |
| Archetype | empty_state |
| Source module | `feature/consent-callback` — **implemented** |

Headless: renders progress and terminal states only. It is the **AIS** analogue of the PISP
`payment-consent` — see that feature's SPEC §1 for the deliberate divergences.

## 2. Screen inventory

Six components, all state surfaces: `loading_layout` (stack), `success_layout` (stack),
`awaiting_state`, `error_state`, `access_denied_state`, `security_error_state` (empty_state ×4).

No form, no interactive input — every affordance is a terminal-state CTA.

## 3. State model — `ConsentCallbackViewModel`

**State fields:** `uiState: ConsentCallbackUiState`
**State defaults:** `uiState = Loading` (`initial_state: loading`)

| UiState | Meaning |
|---|---|
| `Loading` | auth-code exchange and consent-status poll in flight |
| `Awaiting` | consent still `AwaitingAuthorisation` after exchange |
| `Content` | consent confirmed `Authorised` — auto-advances |
| `AccessDenied` | HSBC redirect carried `error=access_denied` |
| `SecurityError` | FAPI `state` or `id_token` nonce mismatch |
| `Error` | token exchange failed |

**Actions:** `ProcessCallback` · `PollConsentStatus` · `NavigateRetry` · `NavigateLogin`
**Events:** none (`E = Nothing`) — navigation is the screen's job
**DI:** `ConsentCallbackRepository` · `ConsentSession` · `redirectUri`

### Ordering invariant

`AccessDenied` and `SecurityError` are detected **before** any token exchange is attempted.
An authorisation code is single-use with a short TTL; spending it on a redirect that was
already going to be rejected destroys the PSU's only recovery path.

### Session invariant

Persisting the PSU tokens is what flips `ConsentSession.isActive()`, and the root navigator
derives the app-open route from it — so writing tokens tears this screen down. The consent is
therefore recorded (`saveConsentMeta`) **before** the tokens are persisted; recording
afterwards would be cancelled mid-write.

A successful token exchange already proves authorisation, so the flow does not gate on the
consent-status poll — the poll only supplies the expiry, best-effort. (Contrast
`payment-consent`, where the equivalent poll **is** load-bearing.)

## 4. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `hsbc_oauth_redirect` | deep link carrying `?code=&id_token=&state=` or `?error=` | `consent-callback` |
| — | consent confirmed `Authorised` | `accounts` |
| — | PSU rejected consent / token exchange failed | `login` |
| — | PSU chose not to share at the HSBC portal | `login` |
| — | FAPI state mismatch | `login` |

Entry is **not a tap** — the per-platform `ConsentRedirectBus` (Android `onCreate`/`onNewIntent`,
desktop loopback, iOS bridge) republishes the redirect into the composition.

## 5. API dependencies

| ID | Method | Path | Auth | Response DTO |
|---|---|---|---|---|
| `fapi-token-exchange` | POST | `/v1.1/oauth2/token` | `private_key_jwt` form body | `OAuthTokenResponse` |
| `consent-status` | GET | `/account-access-consents/{ConsentId}` | CC bearer | `OBReadConsentResponse1` |

Full contracts in `API.md`.

### Error matrix

| Condition | UiState | Retry offered? |
|---|---|---|
| `error=access_denied` in redirect | `AccessDenied` | ✗ — a deliberate PSU choice |
| `state` or `id_token` nonce mismatch | `SecurityError` | ✗ — possible CSRF or crossed authorisation |
| token exchange failure | `Error` | ✅ → `login` |
| consent still `AwaitingAuthorisation` | `Awaiting` | ✅ — poll again |

## 6. Design tokens

`design-tokens.yaml` 2.1.0 — state surfaces only. `SecurityError` and `AccessDenied` both use
`error`-variant `empty_state`, distinguished by icon and copy rather than colour, consistent
with the system-wide "colour is never the only signal" rule.
Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 7. Test mapping

| TC | Assertion | Expected path |
|---|---|---|
| TC-CALLBACK-001 | loading during exchange + status poll | `feature/consent-callback/src/commonTest/.../ConsentCallbackViewModelTest.kt` |
| TC-CALLBACK-002 | success on `Authorised`, auto-advance | ↑ |
| TC-CALLBACK-003 | empty on still-`AwaitingAuthorisation` | ↑ |
| TC-CALLBACK-004 | error on rejection / exchange failure | ↑ |
| TC-CALLBACK-005 | access-denied state on `error=access_denied` | `desktopTest/.../ConsentCallbackStepsUiTest.kt` |
| TC-CALLBACK-006 | security-error on state/nonce mismatch | `androidUnitTest/.../ConsentCallbackStepsRobolectricTest.kt` |

## 8. Notes

This is the one feature module with **no** `androidInstrumentedTest` block — it is the
headless-composable shape, tested via `desktopTest` `runComposeUiTest` plus Robolectric.
Copying its `build.gradle.kts` for a screen feature yields one that cannot compile an
instrumented test.

`docs.yaml` declares no `flow_ref` despite `flows/onboarding-consent.yaml` existing.
