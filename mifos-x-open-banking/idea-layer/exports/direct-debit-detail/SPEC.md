# SPEC.md — direct-debit-detail

| Field | Value |
|---|---|
| Feature | direct-debit-detail |
| Flavor | consumer |
| Status | approved |
| Quality | 93 |
| ViewModel | DirectDebitDetailViewModel |
| Archetype | detail_screen |

---

## Overview

The Direct Debit Detail screen presents the full lifecycle view of a single standing order (direct debit mandate). Users can inspect mandate metadata — counterparty, amount, frequency, schedule — and review the most recent payment transactions against that mandate. A destructive cancel action is available for active mandates, gated behind a confirmation dialog to prevent accidental termination.

The screen is reached by tapping a mandate row in the Direct Debits list and receives `bankId`, `accountId`, and `standingOrderId` as navigation arguments.

---

## Screens

| Screen ID | Title | Archetype | Shell |
|---|---|---|---|
| direct-debit-detail | Direct Debit Detail | detail_screen | Top app bar "Direct Debit Detail" + back arrow; no bottom nav |

---

## Components

| Component | Type | State(s) | Notes |
|---|---|---|---|
| MandateHeaderCard | card | content | Counterparty name, status chip, amount + currency |
| MandateMetaSection | section_group | content | Frequency, start date, next payment date, reference |
| RecentPaymentsList | list | content, empty | Scrollable list of Payment rows with date + amount |
| PaymentRow | list_item | content | Date, amount, status badge |
| CancelMandateButton | button_destructive | content | Visible only when status ∈ {active, pending}; triggers confirmation dialog |
| CancelConfirmDialog | dialog | content | "Cancel this direct debit?" with Confirm / Dismiss actions |
| LoadingSkeleton | skeleton | loading | Full-page shimmer matching content layout |
| ErrorState | error_state | error | Icon + message + "Retry" button |
| EmptyState | empty_state | empty | "No mandate found" illustration + message |
| TopAppBar | app_bar | all | Back arrow, title "Direct Debit Detail" |

---

## States

| State | Trigger | Description |
|---|---|---|
| loading | Screen enter / retry | Full-page skeleton shimmer while LoadMandate in flight |
| content | LoadMandate success | Mandate header, meta section, recent payments list, cancel button if applicable |
| error | LoadMandate failure (network / 401 / 403 / 404) | Error state with retry; 404 shows "Mandate not found" copy |
| empty | LoadMandate returns no mandate data | Empty state illustration |

### Cancel Sub-States (within content state)

| Sub-State | Trigger | Description |
|---|---|---|
| content.idle | Default | Cancel button enabled |
| content.confirm_dialog | CancelMandateButton tapped | Confirmation dialog visible |
| content.cancelling | Confirm tapped | Button replaced by inline spinner |
| content.cancel_success | DELETE success | Snackbar "Direct debit cancelled", navigate back |
| content.cancel_error | DELETE failure | Snackbar error, dialog dismissed, button re-enabled |

---

## State Model

```
DirectDebitDetailUiState
  ├── Loading
  ├── Error(message: String, retryable: Boolean)
  ├── Empty
  └── Content(
        mandate: MandateDetail,
        recentPayments: List<Payment>,
        cancelState: CancelState
      )

CancelState
  ├── Idle
  ├── ConfirmDialog
  ├── Cancelling
  ├── CancelSuccess
  └── CancelError(message: String)

MandateDetail(
  standingOrderId: String,
  bankId: String,
  accountId: String,
  counterpartyName: String,
  amountValue: Double,
  amountCurrency: String,
  frequency: String,        // WEEKLY | MONTHLY | QUARTERLY | ANNUALLY
  startDate: String,        // ISO-8601
  nextPaymentDate: String,  // ISO-8601
  status: MandateStatus,    // active | pending | cancelled | suspended
  reference: String
)

Payment(
  paymentId: String,
  date: String,
  amountValue: Double,
  amountCurrency: String,
  status: PaymentStatus     // completed | failed | pending
)
```

---

## Navigation

| Action | Destination | Method |
|---|---|---|
| Back arrow tap | DirectDebits list | popBackStack() |
| Cancel success | DirectDebits list | popBackStack() after snackbar |
| Error on non-404 | Stay on screen | Show error state |

**Incoming arguments:** `bankId: String`, `accountId: String`, `standingOrderId: String`

---

## Dependencies

| Module | Role |
|---|---|
| accounts | Account context resolution |
| direct-debits | Standing order domain model + repository |
| shared-core | Network layer, error handling, formatting utilities |
| obp-auth | Auth token injection, 401 refresh handling |
