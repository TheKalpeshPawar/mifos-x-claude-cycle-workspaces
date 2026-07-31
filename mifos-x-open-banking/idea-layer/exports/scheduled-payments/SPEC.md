# Scheduled payments — Feature Specification

> Generated from `screens/scheduled-payments/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `bde6567a0e34`
> Endpoints: 1 · DTOs: 1 · Components: 5 · Test scenarios: 8

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

Read-only list of future-dated one-off scheduled payments from `OBReadScheduledPayment3`.
Shows payee, instructed amount, formatted scheduled date, a `ScheduledType` chip (Execution
date / Arrival date) and the destination identifier.

| Attribute | Value |
|---|---|
| Feature ID | `scheduled-payments` · Flow `recurring-and-statements` · Cluster payments-context |
| Priority | should (FR-006) · Status approved · quality 96 |
| Archetype | index_list · Route `ScheduledPaymentsRoute(accountId: String)` |
| Source module | `feature/scheduled-payments` — **implemented** |

**The plainest single-stream template of the five** — six components, no search, no summary
row. Start here when scaffolding a new account-scoped list, and note it is now a *complete*
gated template: it declares the `unsupported` state its two gated siblings declare.

## 2. Screen inventory

`progress_indicator` · `back_button` · `scheduled_payments_list` ·
`empty_scheduled_payments` · `unsupported_scheduled_payments` · `error_state`.

`unsupported_scheduled_payments` was added on 2026-07-30 (`/idea-heal` → enrich loop, closing
`DISCOVERY:scheduled-payments:missing-unsupported-state`). Until then this feature declared
**no `unsupported` state** even though its store *is* capability-gated, so a `U000` refusal
fell through to the ordinary — and explicitly retriable — error path, unlike `direct-debits`
and `standing-orders`. The cause was the 2026-07-28 reverse sync, which back-filled the state
into those two siblings from source and missed this one.

> **Idea-layer only, as of this export.** The state is declared here; source
> (`ScheduledPaymentsUiState`) still ships four states and still routes `U000` to
> `NetworkError`. Until `/implement` lands step 3, a PSU on a credit card continues to see a
> Retry that cannot succeed. Do not read this section as an implementation claim.

## 3. State model — `ScheduledPaymentsViewModel`

**Fields:** `accountId` · `uiState: ScheduledPaymentsUiState` · **Default:** `Loading`
**UiState (declared):** `Loading` · `Content` · `Empty` · `Unsupported` · `Error`
**UiState (in source today):** `Loading` · `Content` · `Empty` · `Error` — `Unsupported` pending
**Error kinds:** `TokenExpired` · `ConsentRevoked` · `RateLimited` · `NetworkError` — **all four
retriable**, which is exactly why a `U000` must NOT reach them
**Actions:** `RetryLoad` · **Events:** none · **DI:** `SavedStateHandle` · `ScheduledPaymentsRepository`

Stateless-gateway repository; ViewModel owns the stream; `RetryLoad → stream.refresh()`;
structural empty via `emptyIfContent { it.isEmpty() }`.

## 4. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `account-detail` | Scheduled Explore option | `scheduled-payments` (accountId) |
| top-app-bar leading | back | `account-detail` |

**Gated chip** — `ScheduledPayments` = `ALL_PRODUCTS − CreditCard`, i.e.
{PersonalCurrentAccount, Savings, ForeignCurrency}. It is the **mirror of Statements**, which
is credit-card-only: a credit card is the one product that hides Scheduled and shows Statements.

Shipped by **repointing an existing `navigateFromChip` branch** off a dead placeholder — the
`ScheduledPayments` chip member already existed, so the suites asserting all nine chips in
declaration order stayed green. That is the cheap path for a new gated screen.

## 5. API dependencies

| ID | Method | Path | Permission | Response DTO |
|---|---|---|---|---|
| `scheduled-payments-list` | GET | `/accounts/{AccountId}/scheduled-payments` | ReadScheduledPaymentsDetail | `OBReadScheduledPayment3` |

Full contract in `API.md`.

## 6. Design tokens

`list_item`, `chip` for `ScheduledType`, `amount` mono. Dates formatted in the ViewModel as
`EEE d MMM yyyy`. Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 7. Test mapping

TC-SP-001 payments render · 002 loading · 003 empty · 004 401 + Retry · 005 back ·
006 403 consent-revoked message · 007 **`ScheduledType=Arrival` renders "Arrival date" chip** ·
008 `CreditorAccount.Identification` (sort code + account number) rendered
→ `feature/scheduled-payments/src/commonTest/.../ScheduledPaymentsViewModelTest.kt` +
Robolectric + instrumented. Ships Roborazzi goldens.

## 8. Notes

`docs.yaml` declares `flow_ref: recurring-and-statements`.
