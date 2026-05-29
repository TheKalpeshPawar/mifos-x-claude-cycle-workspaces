# MOCKUP — My Cards

**Archetype:** index_list
**Shell:** Top app bar ("My Cards", no back icon, notifications_outlined action) + bottom navigation bar (Home/Accounts/Pay/Cards/More). Cards active.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│  My Cards              [🔔]         │  ← Top app bar, headline_large #4C662B
├─────────────────────────────────────┤
│                                     │
│  ┌─────────────────────────────┐    │  ← Skeleton card chip #E1E4D5, 20dp radius, 200dp tall
│  │ ████████████████████████    │    │
│  │ ████████████████████████    │    │
│  │ ████████████████████████    │    │
│  │ ████████████████████████    │    │
│  └─────────────────────────────┘    │
│                                     │
│  ██████  ██████  ██████  ██████     │  ← Skeleton quick actions (4 buttons)
│                                     │
│  ████████████████████████████████   │  ← Skeleton transactions header
│                                     │
│  ┌───────────────────────────────┐  │  ← Skeleton txn row 1
│  │ ██████████████████  ████████  │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← Skeleton txn row 2
│  │ ██████████████████  ████████  │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← Skeleton txn row 3 (skeleton_count: 3)
│  │ ██████████████████  ████████  │  │
│  └───────────────────────────────┘  │
│                                     │
├─────────────────────────────────────┤
│  [🏠] [💳*] [💸] [💳] [•••]        │  ← Bottom nav, Cards active (#DCE7C8 indicator pill)
└─────────────────────────────────────┘
```

**Layout notes:** Skeleton shimmer uses #E1E4D5 (surface_variant) with 200ms (short4) animation; reduced_motion_fallback renders static placeholder blocks. No quick-action interactivity or transactions visible during loading.

---

## Screen: content

```
┌─────────────────────────────────────┐
│  My Cards              [🔔]         │  ← Top app bar
├─────────────────────────────────────┤
│                                     │
│  ◀ ┌──────────────────────────────┐ ▶│  ← Carousel, horizontal scroll, 16dp spacing
│    │  •••• •••• •••• 4521         │  │  ← title_large, #FFFFFF, monospace
│    │                              │  │    Card chip: #4C662B gradient, 320×200dp
│    │  ALEX JOHNSON      [Active]  │  │  ← body_large #CDEDA3 uppercase | chip #4C662B
│    │                     [VISA]   │  │  ← Visa logo 56×20dp #FFFFFF tint
│    └──────────────────────────────┘  │
│                                     │
│  ┌──────────────────────────────┐   │  ← (card 2 — partially visible, snap on scroll)
│  │  •••• •••• •••• 7834        …   │  ← #386663 gradient (secondary)
│  │  ALEX JOHNSON      [Frozen]  …  │  ← Frozen chip #C5C8BA fill
│  │                  [Mastercard]…  │  ← Mastercard logo 48×30dp
│  └──────────────────────────────…  │
│                                     │
│  ┌──────────────────────────────────┐│  ← Quick actions row, space-evenly
│  │ [❄️ Freeze] [⚙ Set Limit]       ││
│  │ [🔑 View PIN] [⚠ Report Lost]   ││  ← Report Lost: icon+text #BA1A1A
│  └──────────────────────────────────┘│
│                                     │
│  Card Transactions                  │  ← title_large, #1A1C16, weight 600
│                                     │
│  ┌───────────────────────────────┐  │  ← Netflix row: #FFFFFF, 12dp radius, 1dp elev
│  │  Netflix          −£15.99    │  │  ← merchant body_large #1A1C16 | amount #BA1A1A w500
│  │  20 May 2026                 │  │  ← body_small, #44483D
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  Tesco Express    −£34.56    │  │
│  │  19 May 2026                 │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  Uber             −£12.40    │  │
│  │  18 May 2026                 │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  Amazon.co.uk     −£67.99    │  │
│  │  17 May 2026                 │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  Starbucks         −£5.85    │  │
│  │  17 May 2026                 │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌─────────────────────────────────┐│  ← Order New Card: outlined, #4C662B, full-width
│  │  [+] Order New Card             ││  ← label_large, 14dp vertical padding, 12dp radius
│  └─────────────────────────────────┘│
│                                     │
├─────────────────────────────────────┤
│  [🏠] [⚖] [💸] [💳*] [•••]        │  ← Cards tab active (#DCE7C8 pill indicator)
└─────────────────────────────────────┘
```

**Layout notes:**
- Card chips: 320×200dp, 20dp radius, elevation 8. Debit Visa: #4C662B solid (diagonal gradient start+end same). Business Mastercard: #386663 diagonal gradient.
- Carousel snaps at start alignment. Second card partially visible (~15dp) to hint scrollability.
- Quick action buttons: vertical layout (icon above label), 8dp padding, 48dp minimum touch target. Report Lost uses #BA1A1A for both icon (report_problem) and text — visually communicates destructive action.
- View PIN button requires `BiometricAuthUseCase` — displayed as enabled but triggers biometric prompt on tap.
- Transaction rows: all amounts in #BA1A1A (debit sign). No credit transactions in the card-linked demo data.
- Order New Card button: full-width, outlined style (#4C662B border + text), add_card leading icon. Visible in content, empty, and implicitly accessible in error state via nav.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│  My Cards              [🔔]         │
├─────────────────────────────────────┤
│                                     │
│                                     │
│                                     │
│       [credit_card_off icon]        │  ← icon-2xl (48dp), #44483D
│                                     │
│         No cards yet                │  ← title_large, #1A1C16, center
│                                     │
│   Order your first Mifos card to    │  ← body_medium, #44483D, center
│   start making payments             │
│                                     │
│  ┌─────────────────────────────────┐│
│  │  [+] Order New Card             ││  ← outlined, #4C662B, full-width
│  └─────────────────────────────────┘│
│                                     │
│                                     │
├─────────────────────────────────────┤
│  [🏠] [⚖] [💸] [💳*] [•••]        │
└─────────────────────────────────────┘
```

**Layout notes:** Empty state centres vertically in available space between top bar and bottom nav. Only cards_title (in top bar) and order_new_card_button visible per state model. Icon uses icon-2xl token (48dp). No carousel, quick actions, or transaction rows shown.

---

## Screen: error

```
┌─────────────────────────────────────┐
│  My Cards              [🔔]         │
├─────────────────────────────────────┤
│                                     │
│                                     │
│                                     │
│         [cloud_off icon]            │  ← icon-2xl (48dp), #44483D
│                                     │
│       Unable to load cards          │  ← title_large, #1A1C16, center
│                                     │
│   Check your connection and         │  ← body_medium, #44483D, center
│   try again                         │
│                                     │
│         [   Retry   ]               │  ← outlined button, #4C662B, center
│                                     │
│                                     │
├─────────────────────────────────────┤
│  [🏠] [⚖] [💸] [💳*] [•••]        │
└─────────────────────────────────────┘
```

**Layout notes:** Error state mirrors empty state layout. Only cards_title visible per state model (show_retry_button: true). Retry triggers `RetryLoad` event → re-calls `GET /obp/v5.1.0/cards`.

---

## Design Checklist (Figma / Stitch)

- [ ] Top app bar: "My Cards" title, no back arrow, notifications_outlined action icon (24dp), #F9FAEF background, 56dp height
- [ ] cards_title in top bar: headline_large (Outfit 32sp/400), #4C662B
- [ ] Card carousel: horizontal scroll, 16dp item gap, snap-start, cards 320×200dp
- [ ] Debit Visa chip: #4C662B solid fill (gradient start=end), 20dp radius, elevation 8, 24dp padding
- [ ] Card number: title_large (Outfit 22sp), #FFFFFF, monospace font, 4dp letter-spacing
- [ ] Cardholder name: body_large (Outfit 16sp), #CDEDA3, uppercase transform
- [ ] Active chip: #4C662B fill, 12dp radius, #FFFFFF label_small text
- [ ] Visa logo: 56×20dp, fit scale, #FFFFFF tint — bottom-right of card
- [ ] Mastercard chip: #386663 gradient fill, 20dp radius, elevation 8
- [ ] Frozen chip: #C5C8BA fill (#outline_variant token), 12dp radius, #FFFFFF label_small text
- [ ] Mastercard logo: 48×30dp, fit scale — bottom-right of card (no tint)
- [ ] Quick actions row: 4 vertical-layout text buttons, space-evenly, 48dp min touch target
- [ ] Freeze/Set Limit/View PIN icons+text: #4C662B. Report Lost icon+text: #BA1A1A
- [ ] Card Transactions header: title_large (22sp), #1A1C16, weight 600, 20dp top padding
- [ ] Transaction rows: #FFFFFF fill, 12dp radius, elevation 1, 1dp #F9FAEF border, 16dp horizontal/14dp vertical padding
- [ ] All transaction amounts: body_large (16sp), #BA1A1A, weight 500 (all are debits in this feature)
- [ ] Transaction dates: body_small (12sp), #44483D
- [ ] Order New Card: outlined, #4C662B border + text, full-width, 12dp radius, 14dp vertical padding, add_card leading icon, label_large
- [ ] Empty state: credit_card_off icon 48dp (#44483D), "No cards yet" title_large center, message body_medium center, Order New Card CTA
- [ ] Error state: cloud_off icon 48dp (#44483D), "Unable to load cards" title_large center, message + Retry outlined button
- [ ] Skeleton shimmer: #E1E4D5 blocks (surface_variant), 200ms short4 animation, 20dp radius for card skeleton, 12dp for txn skeletons
- [ ] Bottom nav: 5 tabs, Cards active with #DCE7C8 indicator pill, 80dp height, Outfit labels
- [ ] All text: Outfit typeface. Touch targets 48dp minimum. 16dp horizontal content padding.

---

_Generated by /idea export | 2026-05-30_
