# MOCKUP — Securing Payment (Payment Authorise Handoff)

**Archetype:** loading
**Shell:** No top app bar. No bottom navigation. Full-screen takeover (mobile only, 390px baseline).
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: preparing

```
┌─────────────────────────────────────┐
│                                     │  ← No top app bar — full-screen takeover
│                                     │
│              [🏛]                   │  ← handoff_bank_icon: account_balance, 80dp, #4C662B
│                                     │
│   Getting your payment ready        │  ← handoff_title: Outfit/headline_small, #1A1C16, center
│        to authorise                 │
│                                     │
│   You'll authorise this payment     │  ← handoff_message: body_medium, #44483D, center
│   directly with HSBC. Your          │     security explainer — credentials never entered
│   username, password and security   │     in this app; payment only sent after approval
│   codes are never entered in this   │
│   app — and the payment is only     │
│   sent once you've approved it.     │
│                                     │
│  ┌───────────────────────────────┐  │  ← handoff_summary_card: #FFFFFF, 16dp radius
│  │          £250.00              │  │     1dp #CDEDA3 border, spacing.md padding
│  │       To Jordan Avery         │  │     handoff_amount_value: display_small, #4C662B, bold
│  │  Authorising securely with    │  │     handoff_payee_value: body_large, #1A1C16
│  │    HSBC Open Banking          │  │     handoff_securing_label: body_small, #44483D
│  └───────────────────────────────┘  │
│                                     │
│              (  ◌  )                │  ← handoff_spinner: circular indeterminate, 32dp, #4C662B
│                                     │
│   Encrypted connection ·            │  ← handoff_security_note: body_small, #74796D, center
│   You can return here anytime       │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Background #F9FAEF throughout all states. Column layout, center-aligned both axes, spacing.lg padding.
- Bank icon (`account_balance`) 80dp, #4C662B. No logo image — icon only.
- Summary card: #FFFFFF fill, 16dp radius, 1dp #CDEDA3 border, spacing.md padding. Groups amount + payee + securing label.
- Amount rendered in Outfit/display_small (36sp), #4C662B, bold 700.
- Payee "To Jordan Avery" in Outfit/body_large (16sp), #1A1C16.
- Securing label in Outfit/body_small (12sp), #44483D.
- Spinner: indeterminate circular, 32dp, #4C662B — replaces the "Continue to HSBC" button in this state.
- Security note below spinner in Outfit/body_small, #74796D.

---

## Screen: redirecting

```
┌─────────────────────────────────────┐
│                                     │  ← No top app bar
│                                     │
│              [🏛]                   │  ← handoff_bank_icon: account_balance, 80dp, #4C662B
│                                     │
│    Taking you to HSBC to           │  ← handoff_title: overridden in redirecting state
│    authorise this payment           │     Outfit/headline_small, #1A1C16, center
│                                     │
│   You'll authorise this payment     │  ← handoff_message (same copy, always visible)
│   directly with HSBC. Your          │
│   username, password and security   │
│   codes are never entered in this   │
│   app — and the payment is only     │
│   sent once you've approved it.     │
│                                     │
│  ┌───────────────────────────────┐  │  ← handoff_summary_card: same as preparing state
│  │          £250.00              │  │
│  │       To Jordan Avery         │  │
│  │  Authorising securely with    │  │
│  │    HSBC Open Banking          │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← handoff_continue_button (replaces spinner here)
│  │      Continue to HSBC         │  │     filled, #4C662B bg, #FFFFFF text
│  └───────────────────────────────┘  │     Outfit/label_large, 8dp radius, match_parent
│                                     │     manual fallback if auto-launch was blocked
│   Encrypted connection ·            │  ← handoff_security_note
│   You can return here anytime       │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Title copy changes to "Taking you to HSBC to authorise this payment" — other components identical to `preparing`.
- Spinner is replaced by the "Continue to HSBC" filled button (the auto-launch has already been attempted). Button launches the same external HSBC authorise URL in the system browser / Custom Tab.
- Tapping "Continue to HSBC" emits `ContinueClicked` → `LaunchAuthorize(authorizeUrl)` — the app leaves the screen; deep-link `org.mifos.openbanking://oauth/callback` returns to `auth-callback`.
- The summary card remains visible so the PSU knows which payment they are about to approve at HSBC.

---

## Screen: error

```
┌─────────────────────────────────────┐
│                                     │  ← No top app bar
│                                     │
│              [🏛]                   │  ← handoff_bank_icon: account_balance, 80dp, #4C662B
│                                     │
│   Couldn't start authorisation      │  ← handoff_title: error override, Outfit/headline_small
│                                     │     #1A1C16, center
│                                     │
│  ┌───────────────────────────────┐  │  ← handoff_error_card: #FFDAD6 bg, 8dp radius
│  │  [!] We couldn't reach HSBC   │  │     handoff_error_icon: error, 20dp, #BA1A1A
│  │  to authorise your payment.   │  │     handoff_error_message: body_small, #410002
│  │  No money has left your       │  │     (role alert — announced by screen readers)
│  │  account. Please check your   │  │
│  │  connection and try again.    │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← handoff_retry_button: filled, #4C662B bg
│  │           Try again           │  │     #FFFFFF text, 8dp radius, match_parent
│  └───────────────────────────────┘  │     emits RetryClicked → re-stages the consent
│                                     │
│             Cancel                  │  ← handoff_cancel_link: text button, #386663
│                                     │     min_height 44dp — navigates to payment-declined
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Error card: #FFDAD6 background, 8dp radius, spacing.md padding. Error icon (`error` glyph, 20dp, #BA1A1A) leading the message text.
- Error message copy: "We couldn't reach HSBC to authorise your payment. No money has left your account. Please check your connection and try again." — Outfit/body_small, #410002.
- "Try again" button: filled, #4C662B bg, #FFFFFF text, match_parent width — re-runs consent staging from scratch (returns screen to `preparing`).
- "Cancel" link: text button, #386663 text, Outfit/label_large, min_height 44dp — navigates to `payment-declined` (the shared payment-not-completed recovery screen). No charge was made.
- Summary card is hidden in this state — the error card takes its position.

---

## Design Checklist (Figma / Stitch)

- [ ] No top app bar, no bottom navigation — full-screen takeover
- [ ] Background #F9FAEF across all states
- [ ] Bank icon: `account_balance`, 80dp, #4C662B, center-aligned
- [ ] Title: Outfit/headline_small (24sp), #1A1C16, center; content changes per state
- [ ] Security explainer body: Outfit/body_medium (14sp), #44483D, center; always visible in `preparing` + `redirecting`
- [ ] Summary card: #FFFFFF fill, 16dp radius, 1dp #CDEDA3 border, spacing.md padding
- [ ] Amount in summary card: Outfit/display_small (36sp), #4C662B, bold 700, center
- [ ] Payee in summary card: Outfit/body_large (16sp), #1A1C16, center
- [ ] Securing label in summary card: Outfit/body_small (12sp), #44483D, center
- [ ] `preparing` state: spinner (circular indeterminate, 32dp, #4C662B) below summary card
- [ ] `redirecting` state: "Continue to HSBC" filled button (#4C662B bg, #FFFFFF text, 8dp radius, match_parent) replaces spinner
- [ ] Security note: Outfit/body_small (12sp), #74796D, center; visible in `preparing` + `redirecting`
- [ ] `error` state: error card (#FFDAD6 bg, 8dp radius); error icon (20dp, #BA1A1A) + message text (#410002); no summary card
- [ ] "Try again" button (error state): filled, #4C662B bg, #FFFFFF text, 8dp radius, match_parent
- [ ] "Cancel" link (error state): text button, #386663, Outfit/label_large, min_height 44dp
- [ ] All text Outfit typeface. Touch targets min 44dp. Mobile only, 390px baseline.

---

_Generated by /idea export | 2026-06-14_
