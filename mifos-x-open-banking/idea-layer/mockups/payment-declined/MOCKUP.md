# MOCKUP — Payment Not Completed (Payment Declined)

**Archetype:** error
**Shell:** No top app bar. No bottom navigation. Terminal screen — back-stack terminated.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: content (PSU declined / access_denied)

```
┌─────────────────────────────────────┐
│                                     │  ← No top app bar — terminal screen
│                                     │
│                ╳                    │  ← declined_icon: cancel, 88dp, #BA1A1A, center
│                                     │
│      Payment not completed          │  ← declined_title: headline_medium, #1A1C16
│                                     │     bold 700, center
│   Good news: no money has left      │  ← declined_assurance: title_small, #386663
│         your account.               │     semibold 600, center — promoted above explanation
│                                     │
│   You didn't finish authorising     │  ← declined_message: body_medium, #44483D, center
│   this payment at HSBC, so it       │
│   wasn't sent. You can review the   │
│   details below and try again.      │
│                                     │
│  ┌───────────────────────────────┐  │  ← declined_details_card: #FFFFFF, 16dp radius
│  │          £250.00              │  │     1dp #FFDAD6 border, spacing.md padding
│  │  To Jordan Avery —            │  │     declined_amount_value: display_small, #1A1C16
│  │  Barclays Bank UK             │  │     bold 700 — neutral, not error-red
│  │  ────────────────────────     │  │     declined_payee_value: body_large, #44483D
│  │  Reason  Authorisation        │  │     declined_reason_row: space_between row
│  │          cancelled at HSBC    │  │     visible only when reason != null
│  └───────────────────────────────┘  │     reason label: body_medium #44483D
│                                     │     reason value: body_medium #1A1C16 bold 500
│  ┌───────────────────────────────┐  │  ← declined_reasons_card: #FFFFFF, 16dp radius
│  │  This can happen if:          │  │     title_small, #1A1C16, bold 700; role heading
│  │  • You chose to cancel on     │  │     three body_medium, #44483D items
│  │    the HSBC approval screen   │  │     no bullet icons — rendered as spaced text rows
│  │  • The approval timed out     │  │
│  │    before it was confirmed    │  │
│  │  • HSBC couldn't confirm the  │  │
│  │    payment from your account  │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← declined_try_again_button: filled, #4C662B bg
│  │           Try again           │  │     #FFFFFF text, 12dp radius, match_parent
│  └───────────────────────────────┘  │     pops to send-money-confirm
│                                     │
│           Back to home              │  ← declined_done_button: text button, #386663
│                                     │     match_parent — navigates to home dashboard
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Background #F9FAEF. Column layout, center-aligned, spacing.lg padding.
- Cancel icon (`cancel`): 88dp, #BA1A1A — error-coloured but rendered at calm scale, no animation.
- Assurance line (#386663, Outfit/title_small, semibold) is placed **before** the explanation — the user reads "no money has left your account" before the reason.
- Details card: #FFFFFF fill, 16dp radius, 1dp #FFDAD6 border, spacing.md padding. Amount in **neutral** #1A1C16 (not #BA1A1A) — reinforces "not charged".
- Reason row is a horizontal `Row` with `space_between`. Hidden (`visible_when: reason != null`) when no reason is available.
- Reasons card: #FFFFFF, 16dp radius. Three text items with spacing.xs bottom padding each.
- "Try again" button: filled, #4C662B bg, #FFFFFF text, 12dp radius, match_parent.
- "Back to home" text button: #386663, match_parent. No `declined_status_note` in this state.

---

## Screen: error (unexpected / technical decline)

```
┌─────────────────────────────────────┐
│                                     │  ← No top app bar
│                                     │
│                ╳                    │  ← declined_icon: cancel, 88dp, #BA1A1A
│                                     │
│      Payment not completed          │  ← declined_title (same as content state)
│                                     │
│   Good news: no money has left      │  ← declined_assurance (#386663, semibold)
│         your account.               │
│                                     │
│   You didn't finish authorising     │  ← declined_message (same body_medium #44483D)
│   this payment at HSBC, so it       │
│   wasn't sent. You can review the   │
│   details below and try again.      │
│                                     │
│  ┌───────────────────────────────┐  │  ← declined_details_card (same as content state)
│  │          £250.00              │  │
│  │  To Jordan Avery —            │  │
│  │  Barclays Bank UK             │  │
│  │  ────────────────────────     │  │
│  │  Reason  Authorisation        │  │
│  │          cancelled at HSBC    │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← declined_reasons_card (same three items)
│  │  This can happen if:          │  │
│  │  • You chose to cancel on the │  │
│  │    HSBC approval screen       │  │
│  │  • The approval timed out     │  │
│  │    before it was confirmed    │  │
│  │  • HSBC couldn't confirm the  │  │
│  │    payment from your account  │  │
│  └───────────────────────────────┘  │
│                                     │
│  Reference: access_denied           │  ← declined_status_note: body_small, #44483D, center
│  (consent RJCT)                     │     muted technical reference — additional in error variant
│                                     │
│  ┌───────────────────────────────┐  │  ← declined_try_again_button
│  │           Try again           │  │
│  └───────────────────────────────┘  │
│                                     │
│           Back to home              │  ← declined_done_button
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Identical to the `content` state with one addition: `declined_status_note` is shown between the reasons card and the CTAs. Content: "Reference: access_denied (consent RJCT)" — Outfit/body_small (12sp), #44483D, center, spacing.lg bottom padding. This note is surfaced only when `isUnexpectedError = true` to help support agents identify the specific error code without alarming typical users.

---

## Design Checklist (Figma / Stitch)

- [ ] No top app bar, no bottom navigation — terminal screen
- [ ] Background #F9FAEF across both states
- [ ] Cancel icon: `cancel`, 88dp, #BA1A1A, centred, no animation
- [ ] Title "Payment not completed": Outfit/headline_medium (28sp), #1A1C16, bold 700, centre
- [ ] Assurance "Good news: no money has left your account.": Outfit/title_small, #386663, semibold 600, centre — placed BEFORE the message
- [ ] Body message: Outfit/body_medium (14sp), #44483D, centre
- [ ] Details card: #FFFFFF fill, 16dp radius, 1dp #FFDAD6 border, 16dp padding
- [ ] Amount in details card: Outfit/display_small (36sp), #1A1C16, bold 700 — NOT error red
- [ ] Payee in details card: Outfit/body_large (16sp), #44483D, centre
- [ ] Reason row: `space_between` horizontal row; hidden when reason is null
- [ ] Reason label "Reason": Outfit/body_medium, #44483D
- [ ] Reason value "Authorisation cancelled at HSBC": Outfit/body_medium, #1A1C16, bold 500, align end
- [ ] Reasons card: #FFFFFF fill, 16dp radius; heading Outfit/title_small bold; three body_medium #44483D items
- [ ] `error` state only: `declined_status_note` body_small #44483D between reasons card and CTAs
- [ ] "Try again" button: filled, #4C662B bg, #FFFFFF text, 12dp radius, match_parent
- [ ] "Back to home" button: text variant, #386663, match_parent
- [ ] All text Outfit. Touch targets min 48dp. Mobile only, 390px baseline.

---

_Generated by /idea export | 2026-06-14_
