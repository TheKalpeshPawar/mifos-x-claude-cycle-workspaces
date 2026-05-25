# Mockup Specification: Agent Registration

| Field | Value |
|---|---|
| Feature | agent-registration |
| Flavor | fieldOfficer |
| Archetype | form |

---

## Screen Layout

```
[ Top App Bar ]  ← back arrow left / "Agent Registration" title / no actions
──────────────────────────────────────────────────
[ "Agent Registration" ]     ← headline_large #1800B1 bold, ph:20 pt:16 pb:4
[ "Register to become an authorised Mifos field agent" ]
                              ← body_medium #666666 ph:20 pb:24

  === IDLE / SUBMITTING STATE ===

[ "Legal Name" ] ← label_medium #444444 semibold ph:20 pb:6
┌──────────────────────────────────────────────────┐
│  Enter your full legal name            outlined  │  border #CCCCCC br:12, ph:14 pv:14
└──────────────────────────────────────────────────┘
[ "Mobile Phone Number" ] ← label_medium #444444 ph:20 pb:6
┌─────────┐ ┌──────────────────────────────────────┐
│  +254   │ │  712 345 678            phone kbd    │
│ #F5F5F5 │ │  br:12 border #CCCCCC               │
└─────────┘ └──────────────────────────────────────┘
  mh:20 mb:16, gap:8, row layout
[ "Agent Number" ] ← label_medium #444444 ph:20 pb:6
┌──────────────────────────────────────────────────┐
│  e.g. AGT-2026-00142                   outlined  │  border #CCCCCC br:12
└──────────────────────────────────────────────────┘
[ "Operating Currency" ] ← label_medium #444444 ph:20 pb:6
┌───────────────────────────────────────── ▾ ──────┐
│  Select currency                       combobox  │  border #CCCCCC br:12
└──────────────────────────────────────────────────┘
                                         (options: EUR, GBP, KES, USD)
[ Register as Agent ]      ← filled #1800B1 white, full-width, label_large
                             corner_radius:14 pv:16, mh:20 mb:32, elevation:2
[ By registering, you agree to the Mifos Agent Terms and Conditions ]
                           ← body_small #888888 centered ph:20 pb:24

  === PENDING_APPROVAL STATE ===

┌─────────────────────────────────────────────────┐
│ ⏳ Pending Approval                              │  bg:#FFF8E1 br:14
│    Your agent application is under review.      │  border #FFD54F
│    You will be notified once confirmed.          │  mh:20 mb:20
└─────────────────────────────────────────────────┘
  (form fields shown read-only, Register button hidden)

  === CONFIRMED STATE ===

┌─────────────────────────────────────────────────┐
│ ✓ Agent Confirmed                               │  bg:#E8F5E9 br:14
│   You are registered as an active Mifos         │  border #A5D6A7
│   field agent. Access all agent features.       │  mh:20 mb:20
└─────────────────────────────────────────────────┘
  (form fields hidden, Register button hidden)
──────────────────────────────────────────────────
```

---

## Components

### Title + Subtitle Block
- **Title:** headline_large (32sp), color #1800B1, bold; padding_horizontal:20 padding_top:16
- **Subtitle:** body_medium (14sp), color #666666; padding_horizontal:20 padding_bottom:24
- Establishes the screen purpose before the first form field

### Field Label Style (repeated pattern)
- label_medium (12sp), color #444444, semibold
- padding_horizontal:20 padding_bottom:6
- Always sits immediately above its input field

### Phone Row (composite)
- **Prefix box:** bg:#F5F5F5, border_radius:12, border #CCCCCC 1px; content "+254"; body_medium semibold #333333; fixed width ~56px; padding 14px/14px
- **Phone input:** flex:1, outlined variant, same border_radius and padding; keyboard_type: phone; placeholder "712 345 678"
- Row has gap:8, margin_horizontal:20

### Currency Selector
- Outlined input with trailing expand_more icon (#CCCCCC)
- On tap: bottom sheet or dialog picker with options: EUR, GBP, KES, USD
- Default hint "Select currency" in #AAAAAA

### Register Button
- Filled, background #1800B1, text white, full-width (mh:20), label_large
- corner_radius:14, padding_vertical:16, elevation:2
- **Submitting state:** Shows CircularProgressIndicator inline; text hidden; all inputs disabled

### Status Banners
- **Pending:** bg:#FFF8E1, corner_radius:14, border #FFD54F 1px; hourglass_empty icon (22px, #F57F17); title "Pending Approval" body_medium #F57F17 semibold; body "Your agent application is under review…" body_small #795548
- **Confirmed:** bg:#E8F5E9, corner_radius:14, border #A5D6A7 1px; verified_outlined icon (22px, #4CAF50); title "Agent Confirmed" body_medium #2E7D32 semibold; body "You are registered as an active Mifos field agent…" body_small #388E3C

---

## Interaction Patterns

| Element | Gesture | Result |
|---|---|---|
| Legal Name input | Tap | Focus; text keyboard opens |
| Phone Number input | Tap | Focus; phone keyboard (numeric) opens |
| Agent Number input | Tap | Focus; text keyboard opens |
| Currency selector | Tap | Opens picker (bottom sheet) with EUR / GBP / KES / USD |
| Register as Agent | Tap | Validates all fields; on pass: submits API; button shows loader |
| Back arrow (top bar) | Tap | Pops to fo-dashboard |

**Validation feedback:** Inline error messages appear below each field on failed submit — red (#BA1A1A) label_small text. Field border changes to error color.

**Error snackbar:** For global errors (409 AGENT_ALREADY_EXISTS, 403), a snackbar appears at the bottom: "Registration failed. Please check your details and try again."

---

## Content Data

| Field | Sample Value |
|---|---|
| Legal Name placeholder | "Enter your full legal name" |
| Phone prefix | +254 (Kenya) |
| Phone placeholder | 712 345 678 |
| Agent number placeholder | AGT-2026-00142 |
| Currency options | EUR, GBP, KES, USD |
| Default currency | KES |
| Terms notice | "By registering, you agree to the Mifos Agent Terms and Conditions" |

---

## Design Notes

**Form layout:** All fields use a consistent labeled-above pattern (not floating labels) for maximum legibility on small screens. The label sits 6px above the input border for clear visual grouping.

**Phone composite field:** The +254 prefix box is visually distinct (grey background, slightly shorter appearance) from the input area, making the country code read as static metadata rather than an editable field — matching UX conventions from mobile banking apps in East Africa.

**Currency selector as combobox:** The expand_more icon signals the dropdown affordance. Options are limited to 4 (EUR, GBP, KES, USD) — no free-text entry — so a simple spinner/dropdown is appropriate over autocomplete.

**State transitions:** The screen transitions are inline (no navigation). The status banner replaces/overlays the submission area without leaving the screen, giving the officer immediate confirmation without losing context about what they submitted.

**Accessibility:** All inputs have content_description and hint text. The status banners have role: status. The register button has content_description "Submit agent registration form."

---
_Generated by /idea export | 2026-05-25_
