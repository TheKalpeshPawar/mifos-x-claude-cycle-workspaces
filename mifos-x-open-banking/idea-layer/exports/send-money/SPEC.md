# Send money — Feature Specification

> Generated from `screens/send-money/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `3c3369f29335`
> Endpoints: 3 · DTOs: 5 · Components: 15 · Test scenarios: 12

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let `/kmp-viewmodel-gen`, `/kmp-screen-gen` and `/verify --tests` consume
this file alone.

## 1. Overview

Consumer-initiated domestic payment (PISP) against the HSBC UK Personal sandbox. The PSU pays
a person from one of their own authorised accounts. Fills the Pay bottom-nav tab, which today
renders `PlaceholderScreen("Pay")` via `SendMoneyRoute`.

| Attribute | Value |
|---|---|
| Feature ID | `send-money` |
| Flow | `send-money-payment` |
| Cluster | payment-initiation |
| Priority | must (FR-012, FR-015, FR-016, FR-017) |
| Status | enriched · quality 88 |
| Release phase | P3 (planned) |
| Archetype | form |

**This is the app's first write surface.** Every other feature is read-only AIS.

### Consumer-context constraint (the decision this feature turns on)

`Risk.PaymentContextCode` MUST be `TransferToThirdParty` or `TransferToSelf`. The four
merchant contexts are forbidden, as are `MerchantCategoryCode`,
`MerchantCustomerIdentification` and `DeliveryAddress`. HSBC's Postman examples use the
merchant shape — copying them models the wrong application.
Verified: `payment-initiation-4.0-personal.yaml:2281-2299` (`OBInternalPaymentContext1Code`)
and `:2244-2280` (`OBRisk1` declares no required properties).

## 2. Screen inventory

Single screen, three steps within `content`:

| Step | Purpose | Key components |
|---|---|---|
| Recipient | choose funding account, then payee | `debtor_account_selector`, `creditor_selector`, `manual_creditor_button`, `manual_sort_code`, `manual_account_number` |
| Amount | amount + optional reference | `amount_field`, `reference_field`, `review_button` |
| Review | confirm before money moves | `review_summary`, `confirm_button`, `cancel_button` |

Plus `progress_indicator` (loading), `submitting_indicator`, `payment_success` (+ `view_payment_status_button`), `error_state` (+ `retry_button`, `reauthorise_button`, `view_consents_button`, `edit_amount_button`).

## 3. State model — `SendMoneyViewModel`

`BaseViewModel<SendMoneyState, SendMoneyEvent, SendMoneyAction>`

**State fields:** `uiState: SendMoneyUiState` · `idempotencyKey: String`

**State defaults:** `uiState = Loading` · `idempotencyKey` generated once when the form is
first completed, then reused across every retry and the eventual submit.

| UiState | Payload |
|---|---|
| `Loading` | — |
| `Content` | `step(Recipient\|Amount\|Review)`, `debtorAccounts`, `beneficiaries`, `debtorAccountId?`, `creditor?`, `amountMinorUnits`, `amountLabel`, `reference?`, `validationError?` |
| `Submitting` | `stage(StagingConsent\|AwaitingAuthorisation\|SubmittingPayment)`, `consentId?` |
| `Success` | `paymentId`, `statusLabel`, `amountLabel`, `creditorName` |
| `Error` | `type: SendMoneyErrorKind`, `message`, `supportReference?` |

**Actions:** `SelectDebtorAccount` · `SelectCreditor` · `EnterAmount` · `ReviewPayment` ·
`ConfirmAndStageConsent` · `SubmitPayment` · `RetrySubmit` · `CancelPayment` · `BackStep`

**Events (non-`Nothing`):** `LaunchAuthorisation(url)` — the Screen opens the browser, not the
ViewModel · `PaymentSucceeded(paymentId)`

**DI:** `SendMoneyRepository` · `AccountsRepository` (shipped) · `BeneficiariesRepository` (shipped)

**Validation** (`amount_field`, on-change-after-first-blur): `InvalidAmount` (not a positive
integer of minor units) · `AmountNotPositive` (≤ 0) · `ExceedsAvailableBalance`. Blocks advance.

## 4. Navigation

| Origin | Trigger | Target |
|---|---|---|
| app-shell Pay tab | tab tap | `send-money` (replaces `SendMoneyRoute` placeholder) |
| `confirm_button` | consent staged (201, AwaitingAuthorisation) | `payment-consent` (consentId) |
| `payment-consent` | authorisation complete | back to `send-money` → SubmitPayment |
| `view_payment_status_button` | success state | `payment-status` (paymentId) |
| `view_consents_button` | 403 ConsentRevoked | `consent-list` |
| `edit_amount_button` | U014 / InsufficientFunds | self → Amount step, selections preserved |

## 5. API dependencies

| ID | Method | Path | Auth | JWS | Idempotency |
|---|---|---|---|:--:|:--:|
| `domestic-payment-consent-create` | POST | `/domestic-payment-consents` | CC token, scope=payments | ✅ | ✅ |
| `domestic-payment-funds-confirmation` | GET | `/domestic-payment-consents/{ConsentId}/funds-confirmation` | PSU token | — | — |
| `domestic-payment-submit` | POST | `/domestic-payments` | PSU token | ✅ | ✅ |

DTOs: `OBWriteDomesticConsent4` · `OBWriteDomesticConsentResponse5` · `OBWriteDomestic2` ·
`OBWriteDomesticResponse5` · `OBWriteFundsConfirmationResponse1`. Full contracts in `API.md`.

### Error matrix

| Code | Kind | Retry? | User message key | Recovery |
|---|---|:--:|---|---|
| 400 U019 | `SignatureMissing` | ✗ | `error.send_money.signature_missing` | none — implementation fault; show OB envelope Id |
| 400 U009 | `ConsentNotAuthorised` | ✗ | `error.send_money.consent_not_authorised` | Re-authorise → `payment-consent` |
| 400 U008 | `ConsentMismatch` | ✗ | `error.send_money.consent_mismatch` | discard, restart form |
| 400 U014 | `OutsideControlParameters` | ✗ | `error.send_money.outside_limits` | back to Amount step |
| 400 U002 | `InvalidField` | ✗ | `error.send_money.invalid_field` | back to Recipient step |
| 401 | `TokenExpired` | ✅ | `error.send_money.token_expired` | Retry after refresh |
| 403 | `ConsentRevoked` | ✗ | `error.send_money.consent_revoked` | View Consents |
| 429 | `RateLimited` | ✅ | `error.send_money.rate_limited` | back-off |
| — | `InsufficientFunds` | ✗ | `error.send_money.insufficient_funds` | back to Amount step |
| — | `NetworkError` | ✅ | `error.send_money.network_error` | Retry (idempotency-safe) |

**Retry is duplicate-safe by construction:** the same `x-idempotency-key` plus the same body
returns the original result rather than creating a second payment.

## 6. Design tokens

`design-tokens.yaml` 2.1.0 — `form.amount_field` (mono `headlineSmall`, non-editable currency
prefix, minor-unit contract) · `form.field` (outline default/focus/error, error text) ·
`form.validation` (on-change-after-first-blur) · `irreversible_action` (review surface, CTA
names action + amount, same-weight escape, lock-on-tap) · `semantic.money`.
Confirm CTA is `primary`, **not** `error` — red frames an intended payment as danger.
Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 7. Test mapping

| TC | Assertion | Expected path |
|---|---|---|
| TC-SEND-001 | recipient step renders accounts + payees | `feature/send-money/src/commonTest/.../SendMoneyViewModelTest.kt` |
| TC-SEND-002 | loading state | ↑ |
| TC-SEND-003 | amount exceeds balance blocks advance | ↑ |
| TC-SEND-004 | zero amount rejected | ↑ |
| TC-SEND-005 | **consumer Risk shape, no merchant fields** | ↑ |
| TC-SEND-006 | own-account → `TransferToSelf` | ↑ |
| TC-SEND-007 | U019 non-recoverable, no Retry | ↑ |
| TC-SEND-008 | U009 offers Re-authorise not Retry | ↑ |
| TC-SEND-009 | U014 returns to Amount, selections kept | ↑ |
| TC-SEND-010 | **retry reuses idempotency key** | ↑ |
| TC-SEND-011 | FundsAvailable=false blocks submit | ↑ |
| TC-SEND-012 | success → payment-status | `SendMoneyScreenRobolectricTest.kt` |

## 8. Implementation prerequisites (P3 — blocking)

Not per-feature work; all four gate the whole phase:
1. `core/network/api/Pisp.kt` — absent (only `Aisp.kt`, `OAuth.kt` ship)
2. Detached JWS (PS256, `b64:false` + `crit`) — extend the existing `signPs256`
3. `x-idempotency-key` generation, persisted across retries
4. payments-scope client-credentials token path (`OAuth.kt` mints `accounts` only)

Wire models for `domesticPayment` already ship at
`core/network/model/pisp/domesticPayment/` (request + response, serialization-tested,
all-nullable so the consumer shape serializes without change) — consumed by nothing.

**Regulatory:** PISP is a distinct FCA permission from AISP. Sandbox unaffected; production
payment initiation would require payment-initiation authorisation. ADR required.
