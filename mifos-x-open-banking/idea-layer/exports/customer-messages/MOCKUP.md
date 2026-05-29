# MOCKUP — Customer Messages

**Archetype:** index_list
**Shell:** Field Officer flavor — no global bottom navigation on this screen; accessed via customer-detail / application-detail / kyc-review push navigation.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│                                     │
│  Messages              [  5 unread ]│  ← headline_large #4C662B + badge skeleton (#E1E4D5, 12dp radius)
│                                     │
│  ┌─────────────────────────────┐    │  ← Search bar skeleton (#E1E4D5, 28dp radius, 16dp horiz margin)
│  │ ████████████████████████    │    │
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │  ← Thread skeleton 1 (#E1E4D5, 12dp radius, 14dp pad)
│  │ [●●] ████████████  ████████ │    │  ← Avatar circle + name skeleton + time skeleton
│  │      █████████████████████  │    │  ← Preview text skeleton
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │  ← Thread skeleton 2
│  │ [●●] ████████████  ████████ │    │
│  │      █████████████████████  │    │
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │  ← Thread skeleton 3
│  │ [●●] ████████████  ████████ │    │
│  │      █████████████████████  │    │
│  └─────────────────────────────┘    │
│                                     │
│                      [✏ New Message]│  ← Extended FAB #4C662B, 6dp elevation, bottom-right
└─────────────────────────────────────┘
```

**Layout notes:** Title row always visible. Unread badge shimmers (skeleton, 12dp radius). Three thread card skeletons fill the list area with #E1E4D5 placeholder blocks at 12dp radius, matching the content card dimensions. FAB always present. shimmer_duration short4 = 200ms; reduced-motion uses static placeholder.

---

## Screen: content

```
┌─────────────────────────────────────┐
│                                     │
│  Messages           [● 5 unread]    │  ← headline_large Outfit 32sp #4C662B wt700 + badge: #BA1A1A fill 12dp radius
│                                     │     badge text: label_medium Outfit 12sp #FFFFFF wt700
│  ┌─────────────────────────────┐    │  ← Search bar: filled, #F9FAEF bg, 28dp radius, search icon
│  │ 🔍  Search messages...      │    │     16dp horiz margin, 12dp bottom margin
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │  ← Thread 1 (UNREAD): #CDEDA3 fill, 12dp radius, 1dp elev
│  │                             │    │     14dp pad, 16dp horiz margin, 8dp bottom margin
│  │  [JM]  John Mwangi   2 min ago  │  ← Avatar: #4C662B circle 44×44dp, "JM" label_large #FFFFFF wt700
│  │        Please send me the   │    │     Name: title_small Outfit 14sp #1A1C16 wt700
│  │        account statement…●  │    │     Time: body_small Outfit 12sp #4C662B wt600
│  │                             │    │     Preview: body_medium Outfit 14sp #1A1C16, maxLines 1 ellipsis
│  └─────────────────────────────┘    │     Unread dot: #4C662B fill 5dp radius 10×10dp (trailing)
│                                     │
│  ┌─────────────────────────────┐    │  ← Thread 2 (READ): #FFFFFF fill, 12dp radius, 1dp elev
│  │                             │    │     1dp border #E1E4D5, 16dp horiz margin, 8dp bottom margin
│  │  [SO]  Sarah Odhiambo  1 hr ago │  ← Avatar: #386663 circle 44×44dp, "SO" label_large #FFFFFF wt700
│  │        Thank you for         │    │     Name: title_small Outfit 14sp #1A1C16 wt600
│  │        approving my applic…  │    │     Time: body_small Outfit 12sp #44483D
│  │                             │    │     Preview: body_medium Outfit 14sp #44483D, maxLines 1 ellipsis
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │  ← Thread 3 (READ): #FFFFFF fill, 12dp radius, 1dp elev
│  │                             │    │     1dp border #E1E4D5, 16dp horiz margin, 8dp bottom margin
│  │  [PK]  Peter Kamau   Yesterday  │  ← Avatar: #44483D circle 44×44dp, "PK" label_large #FFFFFF wt700
│  │        When can I expect     │    │     Name: title_small Outfit 14sp #1A1C16 wt600
│  │        my card to arrive?    │    │     Time: body_small Outfit 12sp #44483D
│  │                             │    │     Preview: body_medium Outfit 14sp #44483D, maxLines 1 ellipsis
│  └─────────────────────────────┘    │
│                                     │
│                      [✏ New Message]│  ← Extended FAB: #4C662B fill, #FFFFFF text label_medium, edit icon
│                                     │     shape extended_fab, 6dp elevation, 24dp bottom / 16dp right
└─────────────────────────────────────┘
```

**Layout notes:**
- Screen background: #F9FAEF (background token).
- Title row: 16dp horizontal pad, 20dp top / 8dp bottom padding, horizontal space-between.
- Unread badge: #BA1A1A fill (error token), 12dp radius, 10dp horiz / 4dp vert padding — reflects live unread_count derived from API.
- Thread 1 (unread): #CDEDA3 fill (primary_container), top border #C5C8BA (outline_variant). Unread dot: 10×10dp circle #4C662B appended to preview row.
- Threads 2 & 3 (read): #FFFFFF fill (surface), border #E1E4D5 (surface_variant). No unread dot.
- All thread cards: 12dp radius (radius.md), 1dp elevation (elevation.level1), 14dp padding, 8dp bottom margin.
- Avatar circles: 44×44dp, 22dp radius. Colors: John Mwangi → #4C662B (primary); Sarah Odhiambo → #386663 (secondary); Peter Kamau → #44483D (on_surface_variant, contrast-fix per REG-001).
- FAB: bottom-right anchored, always visible across all content states.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│                                     │
│  Messages              [● 0]        │  ← badge shows 0 or hides (empty state)
│                                     │
│  ┌─────────────────────────────┐    │  ← Search bar still visible
│  │ 🔍  Search messages...      │    │
│  └─────────────────────────────┘    │
│                                     │
│                                     │
│                                     │
│          ┌──────────┐               │
│          │ [message]│               │  ← message icon (icon-2xl 48dp), #4C662B on #F0F1E6 bg
│          └──────────┘               │
│                                     │
│           No Messages               │  ← title_medium Outfit 16sp #1A1C16, center
│                                     │
│  Start a conversation by composing  │  ← body_medium Outfit 14sp #44483D, center, 32dp horiz pad
│  a new message to a customer        │
│                                     │
│                                     │
│                      [✏ New Message]│  ← FAB remains — primary CTA in empty state
└─────────────────────────────────────┘
```

**Layout notes:** Scroll padding 32dp. Empty state icon: `message`, icon-2xl (48dp), centered. Text center-aligned. FAB is the primary call to action to exit the empty state — compose first message.

---

## Screen: error

```
┌─────────────────────────────────────┐
│                                     │
│  Messages                           │  ← title row visible, badge may show stale count
│                                     │
│  ┌─────────────────────────────┐    │  ← Error banner: #FFDAD6 fill (error_container), 12dp radius
│  │ ⚠  Could not load messages. │    │     error_outline icon #BA1A1A (error token)
│  │    Please try again.        │    │     body_medium Outfit 14sp #410002 (on_error_container)
│  │                             │    │
│  │        [  Retry  ]          │    │  ← outlined button #4C662B, retry action
│  └─────────────────────────────┘    │
│                                     │
│                                     │
│                      [✏ New Message]│  ← FAB remains visible
└─────────────────────────────────────┘
```

**Layout notes:** 16dp horizontal padding. Error banner card: #FFDAD6 fill, 12dp radius, 16dp padding. Retry button: outlined, #4C662B — dispatches RetryLoad → loadMessages(). FAB still accessible so officers can compose even if the thread list fails to load.

---

## Screen: compose_sheet (dialog overlay on content/empty)

```
┌─────────────────────────────────────┐
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ │  ← Scrim #000000 at reduced opacity
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ │
│  ┌─────────────────────────────┐   │
│  │  New Message                │   │  ← title_medium Outfit 16sp #1A1C16 wt700, heading level 2
│  │                             │   │
│  │  ┌───────────────────────┐  │   │  ← compose_customer_select: outlined autocomplete
│  │  │ Customer              │  │   │     placeholder "Search customers…"
│  │  └───────────────────────┘  │   │     12dp bottom margin
│  │                             │   │
│  │  ┌───────────────────────┐  │   │  ← compose_subject_input: outlined text field
│  │  │ Subject               │  │   │     placeholder "Account query, Document request…"
│  │  └───────────────────────┘  │   │     12dp bottom margin
│  │                             │   │
│  │  ┌───────────────────────┐  │   │  ← compose_message_input: outlined textarea
│  │  │ Message               │  │   │     minLines 4, maxLines 8
│  │  │                       │  │   │     placeholder "Type your message to the customer…"
│  │  │                       │  │   │     16dp bottom margin
│  │  └───────────────────────┘  │   │
│  │                             │   │
│  │  ┌─────────────────────────┐ │  │  ← send_message_button: filled, #4C662B, #FFFFFF text, full width
│  │  │      Send Message       │ │  │     label_medium Outfit 12sp, height 40dp (button.height_default)
│  │  └─────────────────────────┘ │  │
│  └─────────────────────────────┘   │
└─────────────────────────────────────┘
```

**Layout notes:** Dialog type (not bottom_sheet — per REG-001 fix). #FFFFFF fill, 20dp border radius, 20dp internal padding. Keyboard shortcut Escape dismisses. Scrim blocks interaction with thread list underneath. `isSending=true` disables `send_message_button` and shows inline progress indicator.

---

## Design Checklist (Figma / Stitch)

- [ ] "Messages" heading — headline_large (Outfit 32sp/400), #4C662B, weight 700; 16dp horizontal / 20dp top pad
- [ ] Unread count badge — #BA1A1A fill, 12dp radius, 10dp horiz + 4dp vert padding; "5 unread" label_medium (Outfit 12sp) #FFFFFF weight 700
- [ ] Search bar — filled variant, #F9FAEF background, 28dp radius, search prefix icon, 16dp horizontal margin, placeholder "Search messages…"
- [ ] Unread thread card (thread_1) — #CDEDA3 fill, 12dp radius, 14dp padding, 1dp border #C5C8BA, 1dp elevation
- [ ] Read thread cards (thread_2, thread_3) — #FFFFFF fill, 12dp radius, 14dp padding, 1dp border #E1E4D5, 1dp elevation
- [ ] John Mwangi avatar — #4C662B circle 44×44dp, 22dp radius; "JM" label_large #FFFFFF weight 700
- [ ] Sarah Odhiambo avatar — #386663 circle 44×44dp; "SO" label_large #FFFFFF weight 700
- [ ] Peter Kamau avatar — #44483D circle 44×44dp (on_surface_variant — contrast fix per REG-001); "PK" label_large #FFFFFF weight 700
- [ ] Thread name (unread) — title_small (Outfit 14sp/500) #1A1C16 weight 700
- [ ] Thread name (read) — title_small (Outfit 14sp/500) #1A1C16 weight 600
- [ ] Thread time (unread) — body_small (Outfit 12sp) #4C662B weight 600
- [ ] Thread time (read) — body_small (Outfit 12sp) #44483D
- [ ] Message preview (unread) — body_medium (Outfit 14sp/400) #1A1C16, maxLines 1, ellipsis overflow
- [ ] Message preview (read) — body_medium (Outfit 14sp/400) #44483D, maxLines 1, ellipsis overflow
- [ ] Unread dot on thread_1 — #4C662B fill, 5dp radius, 10×10dp, trailing in preview row
- [ ] New Message FAB — extended_fab shape, #4C662B fill, #FFFFFF text + edit icon, 6dp elevation, bottom_right 24dp/16dp margin
- [ ] Compose dialog — #FFFFFF fill, 20dp border radius, 20dp internal padding, dialog type (not bottom_sheet)
- [ ] Compose fields — outlined variant; Customer (autocomplete), Subject (text), Message (textarea minLines 4 maxLines 8)
- [ ] Send Message button — filled #4C662B, #FFFFFF text, full width, 40dp height
- [ ] Loading state — skeleton shimmer blocks #E1E4D5 at 12dp radius for thread cards; badge shimmer; short4 (200ms) duration
- [ ] Empty state — message icon 48dp (#4C662B), center; "No Messages" title_medium #1A1C16; body_medium subtitle #44483D center
- [ ] Error state — #FFDAD6 banner, error_outline icon #BA1A1A, "Retry" outlined button #4C662B
- [ ] Screen background — #F9FAEF (background token) in content state
- [ ] All text — Outfit typeface throughout. Touch targets minimum 48dp. 8dp grid spacing system.

---

_Generated by /idea export | 2026-05-30_
