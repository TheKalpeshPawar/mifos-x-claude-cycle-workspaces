# Send money — Visual Mockup

> Auto-generated from `screens/send-money/ui.yaml` + `docs.yaml` by `/idea-feature-mockup`
> Design tokens: `design-system/design-tokens.yaml` (2.1.0) · Design system: Trust Blue 1.1.0
> Generated: 2026-07-31
> Content: `screens/send-money/demo-data.yaml` — HSBC-sandbox-shaped OBIE fixtures, no placeholders

---

## Screen: Send money

**Archetype** `form` · **Initial state** `loading` · **States** `loading · content · submitting · success · error`

### Resolved app shell (RULE-APP-SHELL-001)

Applies to **every** variant below unless a variant note overrides it:

| Shell element | Resolved value | Source |
|---|---|---|
| Bottom navigation | **visible** — Pay tab active (tab 3 of 4: Home · Accounts · Pay · More) | `ui.yaml#shell.bottom_navigation_visible: true` |
| Top app bar | **visible**, title `{strings.send_money.screen_title}` | `ui.yaml#shell.top_app_bar_visible: true` |
| Top app bar leading | **none** — no back arrow; this is a tab root, not a pushed screen | `ui.yaml#shell.top_app_bar_leading: none` |
| FAB | **absent** | `ui.yaml#shell.fab_visible: false` |

Send-money is the only multi-step form in the app, and it is a **tab root**. Step regression is
therefore the `back_step` action and the `cancel_button`, never the app bar — there is no leading
icon to press. The step indicator is textual per DESIGN.md ("the step indicator is textual, not a
decorative progress bar, in keeping with the low-motion dial").

---

## State: loading

Initial fetch of debtor accounts (`AccountsRepository`) and saved payees (`BeneficiariesRepository`).

```
┌─────────────────────────────────────────┐
│  Send money                             │  top-bar, no leading icon
├─────────────────────────────────────────┤
│                                          │
│                                          │
│                  ( ◌ )                   │  progress_indicator, circular
│                                          │
│                                          │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ■ Pay │ ☐ More   │  bottom-nav, Pay active
└─────────────────────────────────────────┘
```

### Component hierarchy

```
send-money/
├── TopAppBar
│   └── title: "Send money"
├── Content (centered)
│   └── progress_indicator: circular
└── BottomNav (Pay active)
```

| Component | Token | Value |
|---|---|---|
| Indicator colour | `primary` | brand trust-blue |
| Screen padding | `spacing.screen_padding` | 16dp |
| Surface | `surface` | screen background |

**Interactions** — none. No cancel affordance during the initial load; the tab bar remains live.

---

## State: content — Step 1 of 3, Recipient

`visibility_condition: {content.step | isRecipient}`

```
┌─────────────────────────────────────────┐
│  Send money                             │
├─────────────────────────────────────────┤
│  Step 1 of 3 · Recipient                 │  textual step indicator
│                                          │
│  ── Pay from ─────────────────────────   │
│  ┌──────────────────────────────────┐   │
│  │ Current account ·· 3349          │   │  debtor_account_row
│  │ £21,530.92 available             │   │
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │
│  │ BMM ACCOUNT ·· 3695              │   │
│  │ £482.10 available                │   │
│  └──────────────────────────────────┘   │
│                                          │
│  ── Pay to ───────────────────────────   │
│  ┌──────────────────────────────────┐   │
│  │ Jameson Lettings                 │   │  creditor_row
│  │ Sort Code · 40-12-09 65872310    │   │
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │
│  │ John Sharma                      │   │
│  │ Sort Code · 23-05-80 11223344    │   │
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │
│  │ EDF Energy                       │   │
│  │ Sort Code · 60-00-01 99887766    │   │
│  └──────────────────────────────────┘   │
│                                          │
│  Enter details manually                  │  manual_creditor_button, text
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ■ Pay │ ☐ More   │
└─────────────────────────────────────────┘
```

**No saved payees** (`{content.beneficiaries | isEmpty}`) — the "Pay to" list is replaced by
`no_saved_payees`; everything else on the step is unchanged:

```
│  ── Pay to ───────────────────────────   │
│                                          │
│              ( people icon )             │  no_saved_payees, empty_state
│           No saved payees yet            │  title
│   You have not saved anyone to pay.      │  body
│   Enter their account details below      │
│   to send money.                         │
│                                          │
│  Enter details manually                  │  manual_creditor_button — STILL VISIBLE
```

This is an INLINE empty inside `content`, not a screen-level `empty` state, and the
distinction is the whole point. `manual_creditor_button` renders for the entire recipient
step regardless of the payee list, so a first-time payer already has a working path. A
screen-level empty state would black out a usable screen and strand them. The affordance
explains the blank and points at the path that already exists — it does not gate anything.

**Manual entry revealed** (`{content.manualEntryVisible}`) — appends below the text button:

```
│  ┌ Sort code ───────────────────────┐   │  manual_sort_code, text_field
│  │ 40-12-09                         │   │  input_type number, max 8
│  └──────────────────────────────────┘   │
│  ┌ Account number ──────────────────┐   │  manual_account_number
│  │ 65872310                         │   │  input_type number, max 8
│  └──────────────────────────────────┘   │
```

### Component hierarchy

```
send-money/ (step: Recipient)
├── TopAppBar → "Send money"
├── form_step_indicator: step_indicator (textual, spans all 3 steps)
├── ScrollContent
│   ├── debtor_account_selector: list (vertical, items ← content.debtorAccounts)
│   │   └── debtor_account_row: list_item (two_line) ×2
│   ├── creditor_selector: list (vertical, items ← content.beneficiaries)
│   │   └── creditor_row: list_item (two_line) ×3
│   ├── no_saved_payees: empty_state          [when content.beneficiaries isEmpty]
│   ├── manual_creditor_button: button (text)
│   ├── manual_sort_code: text_field        [conditional]
│   └── manual_account_number: text_field   [conditional]
└── BottomNav (Pay active)
```

| Element | Token | Notes |
|---|---|---|
| Row min height | `accessibility.min_touch_target_dp` | 48dp |
| Row headline | `bodyLarge` | account/payee display name |
| Row supporting | `bodyMedium` on `onSurfaceVariant` | balance / scheme + identification |
| Balance figure | `semantic.money.neutral` + mono | **unsigned** — an available balance is not a transaction |
| Field radius | `form.field.radius` | 8dp — tighter than a card's 12dp |
| Field min height | `form.field.min_height_dp` | 56dp |
| Field outline | `form.field.outline_default` | focus → `outline_focus`, 2dp |

**Interactions**

| Component | Action | Effect | Result |
|---|---|---|---|
| `debtor_account_row` | `select_debtor_account` | `transform_state` | records `debtorAccountId`; unlocks the creditor picker |
| `creditor_row` | `select_creditor` | `transform_state` | records the payee **and advances to Step 2** |
| `manual_creditor_button` | `show_manual_creditor_entry` | `transform_state` | reveals the two fields |
| `manual_sort_code` / `manual_account_number` | `update_manual_sort_code` / `..._account_number` | on_change | live field capture |

Selecting a **saved payee advances the step**; selecting a debtor account does not. That asymmetry
is deliberate — the funding account is a precondition, the payee is the step's completion.

---

## State: content — Step 2 of 3, Amount

`visibility_condition: {content.step | isAmount}`

```
┌─────────────────────────────────────────┐
│  Send money                             │
├─────────────────────────────────────────┤
│  Step 2 of 3 · Amount                    │
│                                          │
│  ┌ Amount ──────────────────────────┐   │  amount_field
│  │ £  850.00                        │   │  mono, headlineSmall
│  └──────────────────────────────────┘   │  £ prefix is NOT editable
│                                          │
│  ┌ Reference (optional) ────────────┐   │  reference_field, max 35
│  │ RENT-FLAT12                      │   │
│  └──────────────────────────────────┘   │
│                                          │
│  [       Review payment       ]          │  review_button, filled
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ■ Pay │ ☐ More   │
└─────────────────────────────────────────┘
```

**Validation error** (`{content.validationError}` non-null) — from `_test_fixtures.amount_exceeds_balance`,
£850.00 against the BMM account's £482.10:

```
│  ┌ Amount ──────────────────────────┐   │  outline_error, 2dp
│  │ £  850.00                        │   │
│  └──────────────────────────────────┘   │
│  Amount exceeds available balance        │  error_text, bodySmall
│                                          │
│  [       Review payment       ]          │  DISABLED — 38% opacity
```

| Element | Token | Notes |
|---|---|---|
| Amount typography | `form.amount_field.typography` | `headlineSmall`, mono |
| Currency prefix | `onSurfaceVariant` | never part of the editable value |
| Error outline | `form.field.outline_error` | 2dp |
| Error text | `form.field.error_text` | `bodySmall` |
| Disabled CTA | `form.field.disabled_opacity` | 0.38 |
| Validation timing | `form.validation.timing` | `on_change_after_first_blur` |

**Interactions**

| Component | Action | Effect | Notes |
|---|---|---|---|
| `amount_field` | `enter_amount` (`minorUnits`) | on_change | held as **minor units**; displayed formatted |
| `reference_field` | `enter_reference` | on_change | max 35 — OBIE `Unstructured` limit |
| `review_button` | `review_payment` | `transform_state` | `enabled_condition: {content.validationError | isNull}` |

`form.validation.blocks_advance: true` — the CTA is disabled, not merely warned against. Validation
fires only after the first blur, so a half-typed `8` is never flagged as wrong mid-keystroke.

---

## State: content — Step 3 of 3, Review

`visibility_condition: {content.step | isReview}` · governed by `irreversible_action`

```
┌─────────────────────────────────────────┐
│  Send money                             │
├─────────────────────────────────────────┤
│  Step 3 of 3 · Review                    │
│                                          │
│  ┌──────────────────────────────────┐   │  review_summary, review_card
│  │ From                             │   │  review_from_row · info_row
│  │   Current account ·· 3349        │   │
│  │ ──────────────────────────────── │   │
│  │ To                               │   │  review_to_row · info_row
│  │   Jameson Lettings               │   │
│  │   40-12-09 65872310              │   │  secondary, mono
│  │ ──────────────────────────────── │   │
│  │ Amount                           │   │  review_amount_row · emphasis
│  │   £850.00                        │   │  mono
│  │ ──────────────────────────────── │   │
│  │ Reference                        │   │  review_reference_row
│  │   RENT-FLAT12                    │   │  blank → explicit "None"
│  └──────────────────────────────────┘   │
│                                          │
│  [        Send £850.00        ]          │  confirm_button — names action + amount
│              Cancel                      │  cancel_button — same-weight escape
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ■ Pay │ ☐ More   │
└─────────────────────────────────────────┘
```

This variant satisfies all four `irreversible_action.requirements`:

1. **Distinct review surface** listing every committed value — `review_summary`, typed
   `review_card` (`trust_critical`), holding four labelled `info_row` children. Nothing
   summarised or truncated, and no free text: every payment fact is a label/value pair, so
   there is no way to render a commitment the PSU cannot read back. Until 2026-07-31 this
   was a bare `card` with no children at all — the surface existed but showed nothing.
2. **CTA states action + amount** — "Send £850.00", not "Confirm".
3. **Same-weight escape adjacent** — `cancel_button`, never a lone destructive button.
4. **CTA locks on tap** — transitions to `submitting`; double-submission impossible from the UI.

| Element | Token | Notes |
|---|---|---|
| Card container | `surfaceContainer`, radius `medium` (12dp), elevation `level1` | `review_card` component spec |
| Amount figure | mono, `semantic.money.neutral` | unsigned — the direction is stated by "From/To", not by colour |
| Confirm CTA | **`primary`**, radius `full` | `irreversible_action.colour_note`: deliberately NOT `error` |

Red would frame a payment the customer *intends* as a danger; the system reserves red for genuine
failure. The weight comes from the review surface and the amount in the label, not alarm colour.

**Interactions**

| Component | Action | Effect | Notes |
|---|---|---|---|
| `confirm_button` | `confirm_and_stage_consent` | `call_api` | POST `/domestic-payment-consents`, payments-scope token, detached PS256 JWS, stable idempotency key; `Risk.PaymentContextCode: TransferToThirdParty`, **no merchant fields**; emits `LaunchAuthorisation` |
| `cancel_button` | `cancel_payment` | `transform_state` | returns to Step 1; nothing sent yet, so no revocation call |

---

## State: submitting

Covers three stages behind one indicator: `StagingConsent` → `AwaitingAuthorisation` → `SubmittingPayment`.

```
┌─────────────────────────────────────────┐
│  Send money                             │
├─────────────────────────────────────────┤
│                                          │
│                  ( ◌ )                   │  submitting_indicator
│                                          │
│         Staging your payment…            │  ← submitting.stage
│                                          │
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ■ Pay │ ☐ More   │
└─────────────────────────────────────────┘
```

`AwaitingAuthorisation` is the leg where the PSU leaves the app — the ViewModel emits
`LaunchAuthorisation` and the **Screen** opens the browser, matching how `transaction-detail`
emits `CopyToClipboard` rather than touching the platform itself. On return, the payment is
submitted reusing the same idempotency key.

**Interactions** — none. The state is a lock, which is requirement 4 of `irreversible_action`.

---

## State: success

```
┌─────────────────────────────────────────┐
│  Send money                             │
├─────────────────────────────────────────┤
│                                          │
│                  ( ✓ )                   │  check_circle
│                                          │
│         Payment submitted                 │
│                                          │
│   £850.00 to Jameson Lettings is being   │
│   processed. It has been accepted but    │
│   not yet settled.                        │
│                                          │
│  ┌──────────────────────────────────┐   │
│  │ ⏱  In progress                    │   │  status chip — schedule icon
│  └──────────────────────────────────┘   │  secondaryContainer, NOT primary
│                                          │
│  [     View payment status     ]         │  view_payment_status_button
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ■ Pay │ ☐ More   │
└─────────────────────────────────────────┘
```

**The most important variant in this feature.** A successful submit returns
`AcceptedSettlementInProcess` (`demo-data.yaml#payment_submit_response`) — accepted, **not settled**.

The chip therefore renders `semantic.payment_disposition.in_progress`:

| Property | Token | Value |
|---|---|---|
| Container | `payment_disposition.in_progress.container` | `secondaryContainer` |
| On-container | `payment_disposition.in_progress.on_container` | `onSecondaryContainer` |
| Icon | `schedule` | required — colour is never the sole signal |
| Label | "In progress" | required alongside the icon (WCAG 1.4.1) |
| Contrast | measured | 7.22:1, target 4.5 — pass |

`in_progress` is deliberately **not** `primary`: primary is already the credit colour in this
system, so a primary chip would read as *money arrived*. Slate reads as *working*.

The body copy says "accepted but not yet settled" in words. Per
`payment_disposition._contract.colour_is_never_the_only_signal`, that text is what makes the
truthfulness invariant auditable — a reviewer can read the label and see whether the screen is
claiming a settlement it does not have. The `check_circle` glyph confirms *submission*, and the
chip immediately qualifies it; the two are never read apart.

**Interactions**

| Component | Action | Target | Notes |
|---|---|---|---|
| `view_payment_status_button` | `navigate` | **`payment-status`** | carries the returned `DomesticPaymentId` (`PMT-812774903-01`) so the PSU can track settlement |

---

## State: error

Typed PISP failures, with recovery differentiated by OBIE error code. Fixtures from
`demo-data.yaml#error_fixtures`.

```
┌─────────────────────────────────────────┐
│  Send money                             │
├─────────────────────────────────────────┤
│                                          │
│                  ( ! )                   │  error_outline, error
│                                          │
│         Payment not sent                  │
│                                          │
│   Payment outside control parameters     │  ← error.message (U014)
│                                          │
│  [        Edit amount        ]           │  conditional per error.type
├─────────────────────────────────────────┤
│  ☐ Home │ ☐ Accounts │ ■ Pay │ ☐ More   │
└─────────────────────────────────────────┘
```

### Recovery affordances — mutually exclusive by `error.type`

| Button | `visibility_condition` | Error codes | Action |
|---|---|---|---|
| `retry_button` | `{error.type | isRetryable}` | `TokenExpired` 401 · `RateLimited` 429 · `NetworkError` | `retry_submit` — **reuses the same idempotency key** |
| `reauthorise_button` | `{error.type | isConsentNotAuthorised}` | `U009` | navigate → `payment-consent` |
| `view_consents_button` | `{error.type | isConsentRevoked}` | 403 | navigate → `consent-list` |
| `edit_amount_button` | `{error.type | isOutsideControlParameters}` | `U014` · `InsufficientFunds` | `back_step` to Step 2 |

Exactly one is visible at a time. Three error types deliberately offer **no** affordance:

- **`SignatureMissing` (U019)** — a missing detached JWS is an implementation fault, not something
  a customer can act on. Retrying re-sends the same unsigned request. This is the error the app
  will hit on *every* PISP write until `x-jws-signature` ships.
- **`ConsentMismatch` (U008)** — the staged consent and the submitted order disagree; the only
  correct move is to discard and restart, not to retry a mismatched pair.
- **`InvalidField` (U002)** — the offending field is named by `Path`; the PSU corrects it upstream.

`retry_submit` reusing the idempotency key is what makes retry-after-network-drop safe: the bank
returns the original result rather than creating a second payment.

| Element | Token | Notes |
|---|---|---|
| Icon | `error` | 64dp |
| Title | `headlineMedium`, centred | |
| Message | `bodyMedium` on `onSurfaceVariant` | verbatim OBIE `Errors[].Message` |
| Retry CTA | `primary`, radius `full` | error-red is reserved for the icon, not the escape |

---

## Cross-screen references

| From | To | Trigger |
|---|---|---|
| send-money | `payment-status` | `view_payment_status_button` after a successful submit |
| send-money | `payment-consent` | `reauthorise_button` on U009 |
| send-money | `consent-list` | `view_consents_button` on 403 |

All three resolve to existing `screens/` directories.

---

## Implementation status

**SPECIFICATION ONLY.** No `feature/send-money` module exists in source; the Pay tab still renders
`PlaceholderScreen("Pay")`. Blocking work: `core/network/api/Pisp.kt`, detached JWS
(`x-jws-signature`, PS256, `b64:false` + `crit`), `x-idempotency-key`, and a caller passing
`ConsentCreationScope.PAYMENTS`. This mockup describes intended design, not shipped behaviour.
