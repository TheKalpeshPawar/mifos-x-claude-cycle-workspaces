# Mockup: Agent Registration

| Field | Value |
|---|---|
| Feature | agent-registration |
| Flavor | fieldOfficer |
| Archetype | form |
| Route | /agent-registration |
| Scroll | vertical |

---

## Screen Layout

### Chrome

- **Top App Bar**: Title "Agent Registration" (#1800B1 headline style), left-aligned back arrow (`arrow_back`) navigating to `fo-dashboard`. No bottom navigation bar.
- **Safe area**: Respected top and bottom.
- **Scroll**: Full screen scrollable column — content scrolls under the pinned top app bar.

### Scrollable Content Column (idle state, top-to-bottom)

```
┌────────────────────────────────────────┐
│ ← Agent Registration          [AppBar] │
├────────────────────────────────────────┤
│                                        │
│  Agent Registration          [H.Large] │  ← #1800B1 bold, px 20, pt 16
│  Register to become an authorised OBP  │  ← body_medium #666666, px 20
│  field agent with your bank            │
│                                        │
│  Legal Name                 [label_md] │  ← #444444 semibold
│ ┌──────────────────────────────────┐   │
│ │ e.g. Priya Chakraborty          │   │  ← outlined input, radius 12
│ └──────────────────────────────────┘   │
│                                        │
│  Mobile Phone Number        [label_md] │
│ ┌────────┐ ┌──────────────────────┐   │
│ │  +254  │ │ 712 345 678          │   │  ← prefix box + phone input
│ └────────┘ └──────────────────────┘   │
│                                        │
│  Agent Number               [label_md] │
│ ┌──────────────────────────────────┐   │
│ │ e.g. AGT-2026-00142             │   │  ← outlined input, radius 12
│ └──────────────────────────────────┘   │
│                                        │
│  Operating Currency         [label_md] │
│ ┌──────────────────────── ⌄ ───────┐   │
│ │ Select currency                  │   │  ← combobox, trailing expand_more
│ └──────────────────────────────────┘   │
│                                        │
│  Supported Services         [label_md] │
│ ┌──────────────┐ ┌─────────────────┐  │
│ │ Cash Deposit │ │ Cash Withdrawal │  │  ← chip_group, wrap layout
│ └──────────────┘ └─────────────────┘  │
│ ┌────────────────┐ ┌──────────────┐   │
│ │ Account Opening│ │ Bill Payment │   │
│ └────────────────┘ └──────────────┘   │
│ ┌───────────────┐                      │
│ │ Fund Transfer │                      │
│ └───────────────┘                      │
│                                        │
│  Commission Rate (%)        [label_md] │
│ ┌────────────────────────── % ──────┐  │
│ │ e.g. 1.5                          │  │  ← decimal input, trailing % icon
│ └───────────────────────────────────┘  │
│                                        │
│ ┌──────────────────────────────────┐   │
│ │       Register as Agent          │   │  ← filled #1800B1, full width
│ └──────────────────────────────────┘   │
│                                        │
│  By registering, you agree to the      │  ← body_small #888888, centered
│  Mifos Agent Terms and Conditions      │
│                                        │
└────────────────────────────────────────┘
```

---

## State-by-State Visual Description

### loading

**Entry point.** Screen shows only the top app bar and the loading section below the title. The form is not rendered.

```
  Agent Registration               ← headline_large #1800B1

          ◌                        ← loading_indicator size 48 #1800B1, centered
                                     animate: spin continuously

  Checking registration status…   ← body_medium #888888, centered
```

The spinner runs while the pre-flight `GET /agents/me` call resolves. No form fields, no button. Accessibility: `progressbar` role, `live: polite`.

---

### idle

**Default form state.** All inputs are empty and enabled. No error messages. No status banner. The "Register as Agent" button is visible and active.

Chip appearance: each service chip shows #EEF0FF background, #1800B1 text and border — none selected initially.

---

### submitting

**OBP call in flight.** Visually identical to idle, except:
- All inputs (`legal_name_input`, `phone_number_input`, `agent_number_input`, `currency_select`, `commission_rate_input`) are disabled — rendered with reduced opacity.
- Service chips are non-interactive (tap has no effect).
- "Register as Agent" button shows an inline circular progress indicator replacing the label text. Button remains #1800B1 filled.

No modal or overlay. The form remains visible beneath the loading button so the officer can see the data they submitted.

---

### validation_error

**Client-side rejection.** Triggered when the officer taps "Register as Agent" with missing or invalid fields. Form re-enables immediately.

Inline error text appears directly beneath each offending input, in #B00020 body_small with `role: alert` and `live: assertive`.

```
  Legal Name
 ┌──────────────────────────────────┐
 │ (empty)                          │  ← border turns #B00020
 └──────────────────────────────────┘
  Legal name is required            ← #B00020 body_small, assertive

  Mobile Phone Number
 ┌───────┐ ┌────────────────────────┐
 │ +254  │ │ (empty)                │  ← phone input border turns #B00020
 └───────┘ └────────────────────────┘
  Enter a valid 9-digit phone number ← #B00020 body_small, assertive

  Agent Number
 ┌──────────────────────────────────┐
 │ (empty)                          │  ← border turns #B00020
 └──────────────────────────────────┘
  Agent number is required          ← #B00020 body_small, assertive

  Operating Currency
 ┌──────────────────────── ⌄ ───────┐
 │ Select currency                  │  ← border turns #B00020
 └──────────────────────────────────┘
  Select an operating currency      ← #B00020 body_small, assertive
```

No global banner. The scroll position may auto-scroll to the first error field.

---

### pending_approval

**Bank review in progress.** Shown when OBP returns `is_pending_agent: true` (either via pre-flight check or immediately after a new submission).

```
  Agent Registration               ← headline_large #1800B1

 ┌──────────────────────────────────┐
 │ ⧗  Pending Approval             │  ← amber box, bg #FFF8E1, border #FFD54F
 │    Your agent application is     │    icon: hourglass_empty #F57F17
 │    under review. You will be     │    title: body_medium #F57F17 semibold
 │    notified once your bank       │    message: body_small #795548
 │    confirms your registration.   │
 └──────────────────────────────────┘

  Legal Name
 ┌──────────────────────────────────┐
 │ Priya Chakraborty                │  ← inputs disabled (read-only style)
 └──────────────────────────────────┘
  ... (all form fields shown, all disabled) ...

  [Register as Agent button is hidden]
```

The form fields display the previously submitted values in a disabled/read-only style. No submit button. No terms notice.

---

### confirmed

**Registration approved.** Shown when OBP returns `is_confirmed_agent: true`. Form inputs are hidden entirely — only the success card and the dashboard CTA are shown.

```
  Agent Registration               ← headline_large #1800B1

 ┌──────────────────────────────────┐
 │ ✓  Agent Confirmed              │  ← green box, bg #E8F5E9, border #A5D6A7
 │    You are registered as an      │    icon: verified_outlined #4CAF50
 │    active Mifos field agent.     │    title: body_medium #2E7D32 semibold
 │    You can now onboard           │    message: body_small #388E3C
 │    customers and process         │
 │    transactions.                 │
 └──────────────────────────────────┘

 ┌──────────────────────────────────┐
 │         Go to Dashboard          │  ← filled #1800B1, full width, elevation 2
 └──────────────────────────────────┘
```

Tapping "Go to Dashboard" fires `navigate_to_dashboard` — navigates to `fo-dashboard`.

---

### error

**OBP API failure.** Shown when the POST call returns a 4xx or 5xx error. A global red error banner appears at the top of the form; all inputs re-enable for the officer to retry.

```
  Agent Registration               ← headline_large #1800B1
  Register to become an authorised OBP field agent with your bank

 ┌──────────────────────────────────┐
 │ ⚠  Registration failed. Please  │  ← error box, bg #FFEBEE, border #EF9A9A
 │    check your details and try   │    icon: error_outline #B00020 (decorative)
 │    again.                       │    message: body_small #B00020
 └──────────────────────────────────┘

  Legal Name
 ┌──────────────────────────────────┐
 │ Priya Chakraborty                │  ← inputs re-enabled, values preserved
 └──────────────────────────────────┘
  ... (full form visible and interactive) ...

 ┌──────────────────────────────────┐
 │       Register as Agent          │  ← button re-enabled for retry
 └──────────────────────────────────┘
  By registering, you agree to the Mifos Agent Terms and Conditions
```

The error message is dynamic — driven by `error.message` from the `UiError` in ViewModel state. For `AGENT_ALREADY_EXISTS`, the error is rendered inline at the `agent_number_error` field (not the global banner) via `validationErrors["agent_number"]`.

---

## Interaction Patterns

### Chip Multi-Select (Supported Services)

- Chips render in a wrapping flow layout with 8dp spacing.
- **Unselected**: background #EEF0FF, text and border #1800B1.
- **Selected**: background #1800B1, text #FFFFFF, no visible border.
- Tapping a chip fires `ServiceToggled(service: String)`.
- Multiple chips can be selected simultaneously. At least one must be selected to pass validation.
- Chip order (left-to-right, top-to-bottom): Cash Deposit → Cash Withdrawal → Account Opening → Bill Payment → Fund Transfer.

### Form Validation on Submit

1. Officer taps "Register as Agent".
2. ViewModel fires `SubmitClicked`.
3. `ValidationService.validate(state)` checks all required fields and formats.
4. If any error: `validationErrors` map populated → `uiState = ValidationError` → screen re-renders with inline error messages. No API call made.
5. If all valid: `isSubmitting = true` → `uiState = Submitting` → OBP POST called.
6. On `RegistrationSuccess`: `isSubmitting = false` → uiState transitions to `PendingApproval` or `Confirmed`.
7. On `RegistrationFailed`: `isSubmitting = false` → `error` populated → `uiState = Error`.

### Currency Picker

- Tapping `currency_select` fires `open_currency_picker` → `CurrencyPickerOpened` event.
- A bottom sheet (or dialog) presents the four options: EUR — Euro, GBP — British Pound, KES — Kenyan Shilling, USD — US Dollar.
- On selection, `CurrencySelected(value)` updates the ViewModel.
- The selected currency label replaces the placeholder text in the input.

### Phone Number Composition

- The `+254` country code prefix is a static non-interactive display box (not an input).
- The officer types only the 9-digit number into `phone_number_input`.
- On submit, the ViewModel composes `"+254" + phoneNumber.trim()` before sending to OBP.

### Loading State Pre-flight

- On screen mount, `isLoading = true` immediately renders the `loading` state.
- `AgentRepository.getMyAgentStatus(bankId)` is called.
- 404 (no record) → `StatusCheckSuccess(isPending=false, isConfirmed=false)` → renders `idle`.
- Status found → `StatusCheckSuccess(isPending, isConfirmed)` → renders `pending_approval` or `confirmed` directly.
- Any 5xx → `StatusCheckFailed` → renders `idle` (fail-open).

---

_Generated by /idea export | 2026-05-25_
