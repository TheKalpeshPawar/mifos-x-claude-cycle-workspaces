# Mockup: Agent Registration

| Field     | Value                        |
|-----------|------------------------------|
| Feature   | agent-registration           |
| Flavor    | fieldOfficer                 |
| Archetype | form                         |
| Route     | /agent-registration          |
| ViewModel | AgentRegistrationViewModel   |
| Scroll    | vertical                     |
| States    | loading, idle, content, submitting, validation_error, pending_approval, confirmed, error, empty |

---

## Screen Layout

### Chrome

- **Top App Bar**: Title "Agent Registration" (`Outfit/title_large`, `#1A1C16`), left-aligned `arrow_back` icon navigating to `fo-dashboard`. No bottom navigation bar.
- **Safe area**: Respected top and bottom.
- **Scroll**: Full screen scrollable column — content scrolls under the pinned top app bar.

---

## State: loading

```
┌────────────────────────────────────────┐
│ ← Agent Registration          [AppBar] │
├────────────────────────────────────────┤
│                                        │
│  Agent Registration          [H.Large] │  ← #4C662B bold, px 20
│                                        │
│              ◌  (48dp spinner)         │  ← #4C662B circular
│      Checking registration status…    │  ← body_medium #44483D, center
│                                        │
└────────────────────────────────────────┘
```

Pre-flight OBP status check is in-flight. Form is hidden. `isLoading=true`.

---

## State: idle / content

Full registration form ready. No error messages shown. `isLoading=false`.

```
┌────────────────────────────────────────┐
│ ← Agent Registration          [AppBar] │
├────────────────────────────────────────┤
│                                        │
│  Agent Registration          [H.Large] │  ← #4C662B, Outfit/headline_large, px 20
│  Register to become an authorised OBP  │  ← body_medium #44483D, px 20, pb 24
│  field agent with your bank            │
│                                        │
│  Legal Name              [label_medium]│  ← #44483D semibold, px 20, pb 6
│ ┌──────────────────────────────────┐   │
│ │ e.g. Priya Chakraborty           │   │  ← outlined #E1E4D5 border, 12dp radius
│ └──────────────────────────────────┘   │
│                                        │
│  Mobile Phone Number     [label_medium]│  ← #44483D semibold, px 20, pb 6
│ ┌───────┐ ┌────────────────────────┐   │
│ │ +254  │ │ 712 345 678            │   │  ← prefix box #F9FAEF + phone input
│ └───────┘ └────────────────────────┘   │
│                                        │
│  Agent Number            [label_medium]│  ← #44483D semibold, px 20, pb 6
│ ┌──────────────────────────────────┐   │
│ │ e.g. AGT-2026-00142              │   │  ← outlined #E1E4D5 border, 12dp radius
│ └──────────────────────────────────┘   │
│                                        │
│  Operating Currency      [label_medium]│  ← #44483D semibold, px 20, pb 6
│ ┌──────────────────────────────── ▼┐   │
│ │ Select currency                  │   │  ← combobox, expand_more trailing icon
│ └──────────────────────────────────┘   │
│                                        │
│  Supported Services      [label_medium]│  ← #44483D semibold, px 20
│ ┌──────────────┐ ┌──────────────────┐  │
│ │ Cash Deposit │ │ Cash Withdrawal  │  │  ← wrap chip group
│ └──────────────┘ └──────────────────┘  │
│ ┌────────────────┐ ┌──────────────┐    │
│ │ Account Opening│ │ Bill Payment │    │  ← unselected: #CDEDA3 bg / #4C662B text
│ └────────────────┘ └──────────────┘    │  ← selected: #4C662B bg / #FFFFFF text
│ ┌───────────────┐                      │
│ │ Fund Transfer │                      │
│ └───────────────┘                      │
│                                        │
│  Commission Rate (%)     [label_medium]│  ← #44483D semibold, px 20, pb 6
│ ┌────────────────────────────────── %┐ │
│ │ e.g. 1.5                           │ │  ← decimal input, percent trailing icon
│ └────────────────────────────────────┘ │
│                                        │
│ ┌──────────────────────────────────┐   │
│ │      Register as Agent   [filled]│   │  ← #4C662B bg / #FFFFFF, full width
│ └──────────────────────────────────┘   │
│  By registering, you agree to the     │  ← body_small #44483D, center
│  Mifos Agent Terms and Conditions      │
└────────────────────────────────────────┘
```

---

## State: submitting

OBP registration call in flight. Same layout as `idle` but inputs disabled and button shows loading indicator.

- All input fields: `enabled=false`
- `register_agent_button`: loading spinner replaces label text
- `terms_notice`: visible

---

## State: validation_error

One or more fields failed client-side validation. Inline error messages appear below each invalid field.

```
│  Legal Name              [label_medium]│
│ ┌──────────────────────────────────┐   │  ← border turns #BA1A1A
│ │ (empty)                          │   │
│ └──────────────────────────────────┘   │
│  Legal name is required      [alert]   │  ← body_small #BA1A1A, live: assertive
│                                        │
│  Mobile Phone Number     [label_medium]│
│ ┌─────┐ ┌──────────────────────────┐   │  ← border turns #BA1A1A
│ │+254 │ │ (invalid)                │   │
│ └─────┘ └──────────────────────────┘   │
│  Enter a valid 9-digit phone number    │  ← body_small #BA1A1A, live: assertive
```

Repeat pattern for `agent_number_error` and `currency_error`. `register_agent_button` re-enabled; `inputs_enabled=true`.

---

## State: pending_approval

OBP returned `is_pending_agent=true`. Form is read-only; Register button hidden.

```
┌────────────────────────────────────────┐
│ ← Agent Registration          [AppBar] │
├────────────────────────────────────────┤
│  Agent Registration          [H.Large] │
│                                        │
│ ┌──────────────────────────────────┐   │
│ │ ⏳ Pending Approval   [semibold] │   │  ← #CDEDA3 bg, #E8A317 border (1dp)
│ │    Your agent application is     │   │  ← body_small #44483D
│ │    under review. You will be     │   │
│ │    notified once your bank       │   │
│ │    confirms your registration.   │   │
│ └──────────────────────────────────┘   │
│                                        │
│  Legal Name           [disabled input] │
│  Mobile Phone Number  [disabled input] │
│  Agent Number         [disabled input] │
│  Operating Currency   [disabled input] │
│  Supported Services   [read-only chips]│
│  Commission Rate      [disabled input] │
│                                        │
│  (Register as Agent button hidden)     │
│  (terms_notice hidden)                 │
└────────────────────────────────────────┘
```

---

## State: confirmed

OBP returned `is_confirmed_agent=true`. Form inputs hidden; CTA navigates to FO dashboard.

```
┌────────────────────────────────────────┐
│ ← Agent Registration          [AppBar] │
├────────────────────────────────────────┤
│  Agent Registration          [H.Large] │
│                                        │
│ ┌──────────────────────────────────┐   │
│ │ ✓ Agent Confirmed     [semibold] │   │  ← #CDEDA3 bg, #CDEDA3 border, #4C662B text
│ │   You are registered as an active│   │  ← body_small #4C662B
│ │   Mifos field agent. You can now │   │
│ │   onboard customers and process  │   │
│ │   transactions.                  │   │
│ └──────────────────────────────────┘   │
│                                        │
│ ┌──────────────────────────────────┐   │
│ │       Go to Dashboard    [filled]│   │  ← #4C662B bg / #FFFFFF, full width
│ └──────────────────────────────────┘   │
└────────────────────────────────────────┘
```

---

## State: error

OBP API returned 4xx/5xx on registration POST. Global error banner above the re-enabled form.

```
│ ┌──────────────────────────────────┐   │
│ │ ⚠ Registration failed. Please   │   │  ← #CDEDA3 bg, #BA1A1A border
│ │   check your details and try     │   │  ← body_small #BA1A1A, role: alert
│ │   again.                         │   │
│ └──────────────────────────────────┘   │
│                                        │
│  (Full form re-rendered, inputs enabled)│
│ ┌──────────────────────────────────┐   │
│ │      Register as Agent   [filled]│   │
│ └──────────────────────────────────┘   │
```

---

## State: empty

OBP returns no valid bank context for the current user. Form unavailable.

```
┌────────────────────────────────────────┐
│ ← Agent Registration          [AppBar] │
├────────────────────────────────────────┤
│  Agent Registration          [H.Large] │
│                                        │
│  (empty state)                         │
│  Registration form not available       │
└────────────────────────────────────────┘
```

---

## Design Token Reference

| Token                   | Value     | Applied to                                          |
|-------------------------|-----------|-----------------------------------------------------|
| primary                 | `#4C662B` | Title, confirmed text/icon, filled buttons, selected chips |
| primary_container       | `#CDEDA3` | Status banners bg, unselected chips                 |
| on_surface_variant      | `#44483D` | Subtitle, labels, pending/confirmed body text       |
| error                   | `#BA1A1A` | Validation errors, error banner border + icon       |
| surface_variant         | `#E1E4D5` | Input border (default state)                        |
| background              | `#F9FAEF` | Screen bg, phone prefix box                         |
| on_surface              | `#1A1C16` | Phone prefix text                                   |
| pending_accent          | `#E8A317` | Pending banner border                               |

---

_Generated by /idea export | 2026-06-02_
