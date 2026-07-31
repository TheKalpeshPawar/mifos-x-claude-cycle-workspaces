# Payment status — Feature Specification

> Generated from `screens/payment-status/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `6d8300925fe7`
> Endpoints: 1 · DTOs: 1 · Components: 8 · Test scenarios: 8

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

Settlement tracking for a submitted domestic payment. Reads
`GET /domestic-payments/{PaymentId}` and renders the payment's current status alongside the
echoed Initiation — amount, payee, reference, funding account.

**Why it exists:** a successful submit almost never means the money has landed. HSBC returns
`AcceptedSettlementInProcess`, and terminal `AcceptedSettlementCompleted` arrives later.
Without this screen the PSU is told "sent" and given no way to find out whether it settled.

| Attribute | Value |
|---|---|
| Feature ID | `payment-status` |
| Flow | `send-money-payment` |
| Cluster | payment-initiation |
| Priority | must (FR-014) |
| Status | enriched · quality 88 |
| Release phase | P3 (planned) |
| Archetype | detail_screen |

## 2. Screen inventory

Single screen. Components: `progress_indicator` (loading), `back_button`, `status_chip`,
`payment_summary`, `in_progress_note`, `refresh_button` (in-progress only),
`new_payment_button` (terminal-failure only), `error_state` (+ `retry_button`).

## 3. State model — `PaymentStatusViewModel`

`BaseViewModel<PaymentStatusState, Nothing, PaymentStatusAction>`

**State fields:** `paymentId: String` (nav arg) · `uiState: PaymentStatusUiState`
**State defaults:** `uiState = Loading`

| UiState | Payload |
|---|---|
| `Loading` | — |
| `Content` | `statusCode`, `disposition(InProgress\|TerminalSuccess\|TerminalFailure)`, `statusLabel`, `amountLabel`, `creditorName`, `referenceLabel?`, `debtorAccountLabel`, `submittedAtLabel` |
| `Error` | `type: PaymentStatusErrorKind`, `message` |

**Error kinds:** `PaymentNotFound` · `TokenExpired` · `ConsentRevoked` · `NetworkError`
**Actions:** `RefreshStatus` · `StartNewPayment`
**Nav callbacks:** `onBack → popBackStack()` · `onStartNewPayment → navigate(SendMoneyRoute)`
**DI:** `SavedStateHandle` (paymentId) · `PaymentStatusRepository`

### Truthfulness invariant

**The UI must never describe an in-progress payment as sent, complete, or successful.**
Collapsing the disposition to a boolean would tell a PSU their money had moved when it had
not — a false statement about their finances, not a cosmetic bug. Enforced by TC-PSTAT-002
and TC-PSTAT-003.

### Status → disposition map

| Disposition | OBIE statuses | Poll? |
|---|---|:--:|
| `in_progress` | `AcceptedSettlementInProcess`, `AcceptedWithoutPosting`, `Pending` | ✅ |
| `terminal_success` | `AcceptedSettlementCompleted`, `AcceptedCreditSettlementCompleted` | ✗ |
| `terminal_failure` | `Rejected` | ✗ |

**Unknown status → `in_progress`, and keep polling.** Failing open toward "still working" is
safer than declaring an unmapped code a success or a failure.

### Poll contract

Runs only while `disposition == in_progress`; stops the instant a terminal disposition
arrives, and never starts on one. Initial 3000ms, ×1.5 backoff capped at 30000ms, max
duration 600000ms. On `429`: double the interval and keep the last known status on screen.
Polling a terminal status is pure waste and an easy way to earn a rate limit.

## 4. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `send-money` | View status on success state | `payment-status` (paymentId) |
| app-shell Pay tab | most recent payment still in progress | `payment-status` (paymentId) |
| `back_button` | top-app-bar leading | back — read-only, departure has no effect on settlement |
| `new_payment_button` | `Rejected` status | `send-money` with a cleared form |

`new_payment_button` opens a **fresh instruction**, deliberately not a resubmit — a rejected
payment must not be retried against the same consent.

## 5. API dependencies

| ID | Method | Path | Auth | JWS | Idem |
|---|---|---|---|:--:|:--:|
| `domestic-payment-read` | GET | `/domestic-payments/{DomesticPaymentId}` | CC token, scope=payments | — | — |

DTO: `OBWriteDomesticResponse5`. Full contract in `API.md`.

A pure read — no JWS and no idempotency key, unlike the two `send-money` writes. Readable on
the client-credentials payments token, so tracking survives expiry of the single-payment PSU
token obtained during authorisation.

### Error matrix

| HTTP | Kind | Retry? | Message key | Recovery |
|---|---|:--:|---|---|
| 404 / 400 `U011` | `PaymentNotFound` | ✗ | `error.payment_status.not_found` | Back — the resource does not exist |
| 401 | `TokenExpired` | ✅ | `error.payment_status.token_expired` | Retry after re-mint |
| 403 | `ConsentRevoked` | ✗ | `error.payment_status.consent_revoked` | informational only |
| 429 | — | ✅ | — | back off, keep last known status rendered |
| — | `NetworkError` | ✅ | `error.payment_status.network_error` | Retry |

`ConsentRevoked` copy must **not** imply the money came back — a revoked consent does not
reverse a payment that already settled.

## 6. Design tokens

`design-tokens.yaml` 2.1.0 — `semantic.payment_disposition` is this screen's defining token:

| Disposition | Role | Container / on-container | Icon | Contrast |
|---|---|---|---|---|
| in_progress | `secondary` | `#D3E5F5` / `#384956` | `schedule` | 7.22:1 |
| settled | `primary` | `#C9E6FF` / `#004B6F` | `check_circle` | 7.27:1 |
| rejected | `error` | `#FFDAD6` / `#93000A` | `error` | 7.24:1 |

In-progress is deliberately **not** `primary` — primary is the credit colour in this system,
so a primary chip would read as "money arrived". **Colour is never the only signal:** every
disposition carries its icon *and* its text label (WCAG 1.4.1), which is also what makes the
truthfulness invariant auditable.
Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 7. Test mapping

| TC | Assertion | Expected path |
|---|---|---|
| TC-PSTAT-001 | echoed Initiation renders | `feature/payment-status/src/commonTest/.../PaymentStatusViewModelTest.kt` |
| TC-PSTAT-002 | **in-progress never described as sent/complete** | ↑ |
| TC-PSTAT-003 | only settled renders terminal success | ↑ |
| TC-PSTAT-004 | polling stops on terminal disposition | ↑ |
| TC-PSTAT-005 | polling never starts when first read is terminal | ↑ |
| TC-PSTAT-006 | unknown status fails open to in_progress | ↑ |
| TC-PSTAT-007 | rejected offers new payment, not resubmit | ↑ |
| TC-PSTAT-008 | not-found is terminal, no Retry | `PaymentStatusScreenRobolectricTest.kt` |

## 8. Data-flow notes

`cache_strategy: memory` — a short in-memory cache so back-navigation does not re-hit the
network. Room persistence is deliberately **not** used: a payment status written to disk could
outlive the consent that permitted the read and be shown as current when hours stale. This
matches every consent-scoped store in the app being `createMemoryStore` rather than
`createStore`.

## 9. Implementation prerequisites

Shares the four P3 blockers in `exports/send-money/SPEC.md#8`. This feature needs only two of
them — `Pisp.kt` and the payments-scope token path; it makes no write, so the JWS signer and
idempotency handling are not on its critical path.
