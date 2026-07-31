# Payment status — Visual Mockup

> Auto-generated from `screens/payment-status/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-30
> Content: `screens/payment-status/demo-data.yaml` — HSBC-sandbox-shaped OBIE fixtures

---

## Screen: Payment status

**Archetype** `detail_screen` · **Initial state** `loading` · **States** `loading · content · error`

Three states, not four. There is no `empty`: a payment id either resolves or it does not, and a
`404` / `U011` is an **error**, not an absence. Contrast `product`, where a 404 legitimately maps
to empty because "this account has no product terms" is a real answer.

### Resolved app shell (RULE-APP-SHELL-001)

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **visible** — Pay tab active | `ui.yaml#shell.bottom_navigation_visible: true` |
| Top app bar | **visible**, title `{strings.payment_status.screen_title}` | `ui.yaml#shell.top_app_bar_visible: true` |
| Top app bar leading | **back** — pushed screen, unlike its send-money parent | `ui.yaml#shell.top_app_bar_leading: back` |
| FAB | **absent** | `ui.yaml#shell.fab_visible: false` |

---

## State: loading

```
┌─────────────────────────────────────────┐
│  ←  Payment status                      │  top-bar with back_button
├─────────────────────────────────────────┤
│                                          │
│                  ( ◌ )                   │  progress_indicator, circular
│                                          │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ■ Pay │ ☐ More   │
└─────────────────────────────────────────┘
```

### Component hierarchy

```
payment-status/
├── TopAppBar
│   ├── back_button: icon_button (arrow_back)
│   └── title: "Payment status"
├── Content (centered)
│   └── progress_indicator: circular
└── BottomNav (Pay active)
```

**Interactions** — `back_button` only. Leaving is always safe: tracking is read-only, so departing
has no effect on settlement.

---

## State: content — disposition `in_progress`

The default and most frequent case. `AcceptedSettlementInProcess` is what a **successful** submit
returns, so this is what the PSU sees first.

```
┌─────────────────────────────────────────┐
│  ←  Payment status                      │
├─────────────────────────────────────────┤
│  ┌──────────────────────────────────┐   │
│  │ ⏱  In progress                    │   │  status_chip — schedule + label
│  └──────────────────────────────────┘   │  secondaryContainer
│                                          │
│  ┌──────────────────────────────────┐   │  payment_summary, card
│  │ Amount                           │   │
│  │   £850.00                        │   │  mono, neutral, unsigned
│  │                                  │   │
│  │ To                               │   │
│  │   Jameson Lettings               │   │
│  │                                  │   │
│  │ Reference                        │   │
│  │   RENT-FLAT12                    │   │
│  │                                  │   │
│  │ From                             │   │
│  │   Current account ·· 3349        │   │
│  │                                  │   │
│  │ Submitted                        │   │
│  │   30 Jul 2026, 10:44             │   │
│  └──────────────────────────────────┘   │
│                                          │
│  Accepted by the bank. The money has     │  in_progress_note
│  not moved yet — this can take a few     │  visible only while in_progress
│  moments to settle.                       │
│                                          │
│  [          Refresh          ]           │  refresh_button, tonal
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ■ Pay │ ☐ More   │
└─────────────────────────────────────────┘
```

### Component hierarchy

```
payment-status/ (disposition: InProgress)
├── TopAppBar → back_button + "Payment status"
├── ScrollContent
│   ├── status_chip: chip (variant ← content.disposition | chipVariant)
│   ├── payment_summary: card
│   │   └── 5 label/value pairs from the echoed Data.Initiation
│   ├── in_progress_note: text        [conditional — isInProgress]
│   └── refresh_button: button (tonal) [conditional — isInProgress]
└── BottomNav (Pay active)
```

| Element | Token | Notes |
|---|---|---|
| Chip container | `payment_disposition.in_progress.container` | `secondaryContainer` |
| Chip on-container | `payment_disposition.in_progress.on_container` | `onSecondaryContainer` |
| Chip icon | `schedule` | **mandatory** — colour is never the sole signal |
| Contrast | measured | 7.22:1 vs target 4.5 — pass |
| Card | `surfaceContainer`, radius `medium`, elevation `level1` | |
| Amount | mono, `semantic.money.neutral` | **unsigned** — a payment amount is not a signed ledger movement |
| Note text | `bodyMedium` on `onSurfaceVariant` | |

**Both the chip and the note carry the truthfulness invariant in words.** The chip says "In
progress"; the note says the money has not moved yet. Per
`payment_disposition._contract.colour_is_never_the_only_signal`, that redundancy is deliberate —
it is what makes the invariant auditable by reading rather than by inspecting a hex value.

`in_progress` is **not** `primary`, because primary is the credit colour in this system and would
read as *money arrived*.

**Interactions**

| Component | Action | Effect | Notes |
|---|---|---|---|
| `refresh_button` | `refresh_status` | `call_api` | manual re-poll; **hidden once terminal** because the status can no longer change |
| `back_button` | `navigate_back` | `navigate` | → `send-money` |

The ViewModel also re-polls automatically on a **backing-off interval** while in progress, and
stops the instant a terminal disposition is reached. The poll never runs on a terminal status.

---

## State: content — disposition `terminal_success`

```
┌─────────────────────────────────────────┐
│  ←  Payment status                      │
├─────────────────────────────────────────┤
│  ┌──────────────────────────────────┐   │
│  │ ✓  Settled                        │   │  check_circle, primaryContainer
│  └──────────────────────────────────┘   │
│                                          │
│  ┌──────────────────────────────────┐   │  payment_summary (unchanged)
│  │ Amount        £850.00            │   │
│  │ To            Jameson Lettings   │   │
│  │ Reference     RENT-FLAT12        │   │
│  │ From          Current ·· 3349    │   │
│  │ Submitted     30 Jul 2026, 10:44 │   │
│  └──────────────────────────────────┘   │
│                                          │
│                                          │  no note, no refresh — terminal
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ■ Pay │ ☐ More   │
└─────────────────────────────────────────┘
```

| Element | Token | Value |
|---|---|---|
| Chip container | `payment_disposition.terminal_success.container` | `primaryContainer` |
| Chip on-container | `payment_disposition.terminal_success.on_container` | `onPrimaryContainer` |
| Icon | `check_circle` | |
| Contrast | measured | 7.27:1 — pass |

Trust-blue, **not green**. DESIGN.md is explicit: *"a settled payment gets the trust-blue chip, not
a green tick and not a celebration."* Both `in_progress_note` and `refresh_button` disappear —
their `visibility_condition` is `isInProgress`, and a settled payment has nothing left to refresh.

---

## State: content — disposition `terminal_failure`

```
┌─────────────────────────────────────────┐
│  ←  Payment status                      │
├─────────────────────────────────────────┤
│  ┌──────────────────────────────────┐   │
│  │ ⊗  Rejected                       │   │  error icon, errorContainer
│  └──────────────────────────────────┘   │
│                                          │
│  ┌──────────────────────────────────┐   │  payment_summary (unchanged)
│  │ Amount        £850.00            │   │
│  │ To            Jameson Lettings   │   │
│  │ ...                              │   │
│  └──────────────────────────────────┘   │
│                                          │
│  [       Start a new payment       ]     │  new_payment_button, filled
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ■ Pay │ ☐ More   │
└─────────────────────────────────────────┘
```

| Element | Token | Value |
|---|---|---|
| Chip container | `payment_disposition.terminal_failure.container` | `errorContainer` |
| Chip on-container | `payment_disposition.terminal_failure.on_container` | `onErrorContainer` |
| Icon | `error` | |
| Contrast | measured | 7.24:1 — pass |

The summary card is **still shown**. A rejected payment is not a blank screen — the PSU needs to
see what was attempted.

**Interactions**

| Component | Action | Target | Notes |
|---|---|---|---|
| `new_payment_button` | `navigate` | **`send-money`** | opens with a **cleared** form |

Deliberately a fresh payment, not a resubmit: the app never silently re-sends an instruction the
bank rejected. The PSU re-enters it, which is a conscious act.

### Unknown-status policy

An OBIE status outside the mapped vocabulary renders as **in_progress** — never as success or
failure. Failing open toward "still working" is the only safe guess
(`payment_disposition._contract.unknown_status_policy`).

---

## State: error

```
┌─────────────────────────────────────────┐
│  ←  Payment status                      │
├─────────────────────────────────────────┤
│                                          │
│                  ( ! )                   │  error_outline, error, 64dp
│                                          │
│      Couldn't load this payment           │
│                                          │
│   Payment not found                       │  ← error.message
│                                          │
│                                          │  NO retry — not retryable
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ■ Pay │ ☐ More   │
└─────────────────────────────────────────┘
```

### Retry is conditional, and three of four types do not get it

| Error type | Trigger | `retry_button` | Why |
|---|---|:---:|---|
| `TokenExpired` | 401 | **shown** | transient; a token refresh fixes it |
| `NetworkError` | IOException / timeout | **shown** | transient |
| `PaymentNotFound` | 404 / `U011` | **hidden** | terminal — the id will not start existing |
| `ConsentRevoked` | 403 | **hidden** | informational; **does not undo a settled payment** |

`ConsentRevoked` is the subtle one. A revoked consent removes the app's *right to read*, not the
payment itself — money already sent stays sent. Offering Retry would imply the payment is in
question when only visibility is.

`refresh_status` is a **pure read**, so retrying it cannot affect the payment — unlike send-money's
retry, which re-sends a write and depends on the idempotency key for safety.

| Element | Token | Notes |
|---|---|---|
| Icon | `error` | 64dp |
| Title | `headlineMedium`, centred | |
| Message | `bodyMedium` on `onSurfaceVariant` | verbatim OBIE `Errors[].Message` |

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| payment-status | `send-money` | `back_button`, and `new_payment_button` after a rejection |

`send-money` resolves to an existing `screens/` directory. `payment-status` is reached **from**
send-money's success state carrying `DomesticPaymentId` (`PMT-812774903-01`).

---

## Implementation status

**SPECIFICATION ONLY.** No `feature/payment-status` module exists in source. Depends on
`core/network/api/Pisp.kt` (absent) for `GET /domestic-payments/{PaymentId}`. Unlike send-money
this screen performs no writes, so it needs **no** detached JWS and **no** idempotency key — only
the payments-scope token and the API surface.
