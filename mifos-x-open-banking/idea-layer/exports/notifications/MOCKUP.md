# MOCKUP — Notifications

**Archetype:** index_list
**Shell:** Top app bar ("Notifications", back arrow, done_all + tune actions). No bottom navigation bar.
**Accent:** #4C662B (Earth-green primary). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Notifications     ✓  🔧          │  ← TopAppBar: back + done_all + tune
├─────────────────────────────────────┤
│                                     │
│  Notifications                      │  ← headline_large #4C662B bold
│                                     │
│  ██████  (skeleton)                 │  ← "Today" label skeleton
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ○  ██████████████████        │  │  ← Card skeleton row 1 (shimmer)
│  │     ████████████████████████  │  │
│  │     ████████                  │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ○  ██████████████████        │  │  ← Card skeleton row 2
│  │     ████████████████████████  │  │
│  │     ████████                  │  │
│  └───────────────────────────────┘  │
│  ██████  (skeleton)                 │  ← "Earlier" label skeleton
│  ┌───────────────────────────────┐  │
│  │  ○  ██████████████████        │  │  ← Card skeleton row 3
│  │     ████████████████████████  │  │
│  │     ████████                  │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ○  ██████████████████        │  │  ← Card skeleton row 4
│  │     ████████████████████████  │  │
│  │     ████████                  │  │
│  └───────────────────────────────┘  │
└─────────────────────────────────────┘
```

---

## Screen: populated (Primary)

```
┌─────────────────────────────────────┐
│ ←  Notifications     ✓  🔧          │  ← TopAppBar
├─────────────────────────────────────┤
│                                     │
│  Notifications          Mark All Read│  ← headline_large #4C662B bold
│                          text #386663│
│                                     │
│  Today                              │  ← label_medium #44483D semibold
│                                     │
│  ┌───────────────────────────────┐  │  ← UNREAD card #CDEDA3 bg, 16dp radius
│  │  ●↓  Payment received      ●  │  │    Icon circle #4C662B, arrow_down white
│  │      Payment of £50.00         │  │    Title: body_medium #1A1C16 semibold
│  │      received from James Wilson│  │    Msg: body_small #44483D
│  │      10 min ago                │  │    Time: label_small #44483D
│  └───────────────────────────────┘  │    Unread dot: 10×10 #4C662B (top-right)
│                                     │
│  ┌───────────────────────────────┐  │  ← UNREAD card #CDEDA3 bg
│  │  ●✓  KYC verification       ●  │  │    Icon circle #4C662B, verified_user white
│  │      approved                  │  │
│  │      Your identity has been    │  │
│  │      verified. Full access.   │  │
│  │      1 hr ago                  │  │
│  └───────────────────────────────┘  │
│                                     │
│  Earlier                            │  ← label_medium #44483D semibold
│                                     │
│  ┌───────────────────────────────┐  │  ← READ card #FFFFFF bg, 1dp #F9FAEF border
│  │  ⊙↻  Direct debit mandate     │  │    Icon circle #386663, autorenew white
│  │      created                   │  │    Title: body_medium #44483D semibold
│  │      Direct debit for Netflix  │  │    Msg: body_small #44483D
│  │      — £15.99/mo from Current  │  │
│  │      Account. 3 hr ago         │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← READ card #FFFFFF bg
│  │  ⊙↓  Salary credited          │  │    Icon circle #4C662B, arrow_down white
│  │      £3,200.00 from Acme Ltd   │  │    Title: body_medium #44483D semibold
│  │      has been credited to your │  │
│  │      Current Account. Yesterday│  │
│  └───────────────────────────────┘  │
│                                     │  ← 24dp bottom spacer
└─────────────────────────────────────┘
```

**Layout notes:**
- Title + Mark All Read: horizontal row, space-between, 20dp horizontal padding, 16dp top, 8dp bottom.
- Section labels: 16dp horizontal padding, 8dp top, 4dp bottom.
- Notification cards: 20dp horizontal margin, 8dp bottom margin, 16dp padding, 16dp radius.
- Unread cards: `#CDEDA3` bg, 1dp `#CDEDA3` border.
- Read cards: `#FFFFFF` bg, 1dp `#F9FAEF` border.
- Icon circles: 44×44dp, category-colored. Icon inside: 22dp white symbol.
- Content column: flex 1, vertical stack: title (semibold) + message + time.
- Unread dot: 10×10dp circle `#4C662B`, align_self: flex_start, margin_top 4dp, trailing.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Notifications     ✓  🔧          │
├─────────────────────────────────────┤
│                                     │
│  Notifications                      │
│                                     │
│                                     │
│             🔔                      │  ← notifications_none_outlined 48dp #75796C
│                                     │
│         You're all caught up        │  ← headline_small #1A1C16 centered
│                                     │
│   No new notifications. We'll let  │  ← body_medium #44483D centered
│   you know about payments, alerts   │
│   and updates.                      │
│                                     │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Icon + messages vertically centered in viewport (Column with alignment center).

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Notifications     ✓  🔧          │
├─────────────────────────────────────┤
│                                     │
│  Notifications                      │
│                                     │
│               ☁                     │  ← cloud_off icon 48dp #BA1A1A, centered
│                                     │
│   Unable to load notifications      │  ← headline_small #1A1C16 centered
│   Check your connection and         │
│   try again                         │  ← body_medium #44483D centered
│                                     │
│  ┌───────────────────────────────┐  │
│  │            Retry              │  │  ← Filled #4C662B
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar: back arrow + "Notifications" + done_all action + tune action
- [ ] No bottom navigation bar (shell: bottom_nav: false)
- [ ] "Notifications" headline_large `#4C662B` bold
- [ ] "Mark All Read" text button `#386663`, label_medium
- [ ] "Today" / "Earlier" section labels: label_medium `#44483D` semibold, 16dp padding
- [ ] Unread cards: `#CDEDA3` background, 1dp `#CDEDA3` border, 16dp radius
- [ ] Read cards: `#FFFFFF` background, 1dp `#F9FAEF` border, 16dp radius
- [ ] Icon circles: 44×44dp filled circle (payment: `#4C662B`, security: `#4C662B`, system: `#386663`)
- [ ] Unread dot: 10×10dp `#4C662B` circle, trailing position
- [ ] Notification title: body_medium semibold (`#1A1C16` unread, `#44483D` read)
- [ ] Notification body: body_small `#44483D`
- [ ] Timestamp: label_small `#44483D`
- [ ] Loading: 4 shimmer skeleton cards matching notification card proportions
- [ ] Empty state: notifications_none_outlined 48dp icon + two-line message
- [ ] Error state: cloud_off icon + message + retry button
- [ ] All text Outfit typeface; 20dp horizontal screen padding
