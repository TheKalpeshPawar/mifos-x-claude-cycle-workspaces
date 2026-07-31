# Payment consent — Feature Specification

> Generated from `screens/payment-consent/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `64c86ff15dcb`
> Endpoints: 3 · DTOs: 2 · Components: 5 · Test scenarios: 8

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

Return leg of the PISP app-to-app authorisation. The direct analogue of the shipped
`consent-callback`, but on `scope=payments` against a domestic-payment-consent rather than an
account-access-consent. `send-money` owns the outbound launch; this feature owns everything
after HSBC redirects back. Headless — renders progress and terminal error only, never a form.

| Attribute | Value |
|---|---|
| Feature ID | `payment-consent` |
| Flow | `send-money-payment` |
| Cluster | payment-initiation |
| Priority | must (FR-013) |
| Status | enriched · quality 88 |
| Release phase | P3 (planned) |
| Archetype | empty_state |

### Why this is not `consent-callback`

`consent-callback` persists PSU tokens on success, which flips `ConsentSession.isActive()` and
re-routes the app to Home. A payment authorisation must not do that — it authorises one
payment, not a data-sharing session, and the app is already signed in.

| | `consent-callback` (AIS) | `payment-consent` (PISP) |
|---|---|---|
| scope | `openid accounts` | `payments` |
| consent resource | `/aisp/account-access-consents/{id}` | `/pisp/domestic-payment-consents/{id}` |
| token handling | persisted → flips `isActive()` | **in-memory only, single payment** |
| on success | route to Home | emit event → `send-money` submits |
| status poll | best-effort (supplies expiry) | **load-bearing** — submit fails U009 unless `AUTH` |

**Reused verbatim:** `PendingAuthStore` state/nonce contract (single-use `consume()`), the
per-platform `ConsentRedirectBus`, the OAuth token-exchange call shape.
**Must not reuse:** `ConsentSession` token persistence, the post-success route to Home.

## 2. Screen inventory

Single headless screen. Components: `authorising_indicator` + `progress_detail`
(validating/exchanging/checking), `check_again_button` (checking only), `authorised_state`,
`error_state` (+ `restart_authorisation_button`, `abandon_button`).

## 3. State model — `PaymentConsentViewModel`

`BaseViewModel<PaymentConsentState, PaymentConsentEvent, PaymentConsentAction>`

**State fields:** `uiState: PaymentConsentUiState` · `consentId: String`
**State defaults:** `uiState = Validating` (there is no `Loading` — see §7)

| UiState | Meaning |
|---|---|
| `Validating` | checking state/nonce against the pending authorisation |
| `Exchanging` | authorisation code → PSU access token |
| `Checking` | polling consent status until `AUTH` |
| `Authorised` | consentId + payment-scoped token ready to hand back |
| `Error` | `type: PaymentConsentErrorKind`, `message` |

**Error kinds:** `StateMismatch` · `NoPendingAuthorisation` · `CodeExpired` ·
`ConsentRejected` · `AuthorisationTimedOut` · `NetworkError`

**Actions:** `CheckAgain` · `RetryAuthorisation` · `AbandonPayment`
**Events (non-`Nothing`):** `Authorised(consentId, token)` · `RestartAuthorisation` · `Abandoned`

Success is handed back as an **event, not a navigation**, so `send-money` retains the
idempotency key and the byte-identical staged Initiation it must resend.

**DI:** `SavedStateHandle` (consentId) · `PaymentConsentRepository` · `PendingAuthStore` (shipped)

### Ordering invariant

Validate → exchange → poll, in that order. Validating before exchanging matters because an
authorisation code is single-use with a 30–60s TTL: spending it on a request that was going to
be rejected anyway destroys the PSU's only recovery path.

### Token invariant

The token from `payment-token-exchange` is held in memory for the life of this payment and is
**never** written to `ConsentSession`. Persisting it would overwrite the AIS session token and
conflate a one-payment authorisation with a data-sharing session. Enforced by TC-PCON-007.

## 4. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `send-money` | HSBC redirect after SCA (via `ConsentRedirectBus`) | `payment-consent` (consentId) |
| — | consent reaches `AUTH` | event `Authorised` → `send-money` submits |
| `restart_authorisation_button` | CodeExpired / TimedOut / NetworkError | `send-money` (re-stage + relaunch) |
| `abandon_button` | any error | `send-money` (consent left unauthorised, expires on its own) |

Entry is **not a tap** — the app left for the browser and the per-platform redirect bus
republishes the return into the composition.

## 5. API dependencies

| ID | Method | Path | Auth |
|---|---|---|---|
| `payment-authorize-redirect` | GET | `/v1.1/oauth2/authorize` | none (browser redirect) |
| `payment-token-exchange` | POST | `/v1.1/oauth2/token` | `private_key_jwt` in form body |
| `payment-consent-status` | GET | `/domestic-payment-consents/{ConsentId}` | CC token, scope=payments |

DTOs: `OAuthTokenResponse` · `OBWriteDomesticConsentResponse5`. Full contracts in `API.md`.

**Poll contract:** interval 1500ms, deadline 45000ms, terminal success `AUTH`, terminal
failure `RJCT`, on deadline → `AuthorisationTimedOut`.

### Error matrix

| Condition | Kind | Restartable? | Message key |
|---|---|:--:|---|
| state or nonce mismatch | `StateMismatch` | ✗ | `error.payment_consent.state_mismatch` |
| `PendingAuthStore.consume()` null | `NoPendingAuthorisation` | ✗ | `error.payment_consent.no_pending` |
| 400 `invalid_grant` | `CodeExpired` | ✅ | `error.payment_consent.code_expired` |
| `Status == RJCT` | `ConsentRejected` | ✗ | `error.payment_consent.rejected` |
| poll deadline elapsed at `AWAU` | `AuthorisationTimedOut` | ✅ | `error.payment_consent.timed_out` |
| IOException / timeout | `NetworkError` | ✅ | `error.payment_consent.network_error` |

`ConsentRejected` is terminal on purpose — the PSU made a deliberate choice at the bank, and
offering Restart would nag them to re-approve something they just refused.

## 6. Design tokens

`design-tokens.yaml` 2.1.0 — inherits the `state_submitting` / `state_success` surfaces added
in 1.1.0. No payment-disposition chip here (that is `payment-status`). Progress detail text is
`bodyMedium` on `onSurfaceVariant`; motion stays at dial 2 (subtle fade only).
Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 7. Test mapping

| TC | Assertion | Expected path |
|---|---|---|
| TC-PCON-001 | happy path → `Authorised` event | `feature/payment-consent/src/commonTest/.../PaymentConsentViewModelTest.kt` |
| TC-PCON-002 | state mismatch rejected **before** token exchange | ↑ |
| TC-PCON-003 | nonce mismatch rejected after exchange | ↑ |
| TC-PCON-004 | missing pending auth — no network call at all | ↑ |
| TC-PCON-005 | expired code offers Restart | ↑ |
| TC-PCON-006 | `RJCT` terminal, no Restart offered | ↑ |
| TC-PCON-007 | **zero writes to `ConsentSession`** | ↑ |
| TC-PCON-008 | poll deadline → timeout, not a hang | ↑ |

## 8. Known deviation — STATE-001

States are `validating/exchanging/checking/authorised/error`; there is no literal `loading` or
`content`. A strict STATE-001 reading fails this. SCREEN_SCHEMA declares state vocabulary
per-feature with custom states allowed and lists `validating`/`checking` in its `any_of`;
`validating` is the loading analogue and `authorised` the content analogue. Recorded as an
accepted warning in `state/DESIGN_VALIDATION.yaml#F-003` with a bias disclosure, since the
screen and the adjudication share an author.

## 9. Implementation prerequisites

Shares the four P3 blockers listed in `exports/send-money/SPEC.md#8`. Specific to this
feature: the payments-scope client-credentials path is required for the status poll, and the
`ConsentRedirectBus` needs a payment-redirect channel alongside the existing AIS one.
