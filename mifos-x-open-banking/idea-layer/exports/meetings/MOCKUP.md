# MOCKUP — Meetings

**Archetype:** index_list
**Shell:** No top app bar (screen-level title rendered inline). Field Officer flavor — bottom navigation bar (Home / Accounts / Payments / Profile tabs).
**Accent:** #4C662B (Earth-green primary). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│                                     │
│  ████████████████████████           │  ← Title skeleton (shimmer, #E1E4D5)
│                                     │
│  ┌──┐ ┌──┐ ┌──┐ ┌──┐ ┌──┐ ┌──┐ ┌──┐ │  ← 7 day-pill skeletons (count: 7)
│  └──┘ └──┘ └──┘ └──┘ └──┘ └──┘ └──┘ │    #E1E4D5, 12dp radius, shimmer
│                                     │
│  ████████████████████               │  ← Section header skeleton (count: 1)
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ████████     ███████████     │  │  ← Meeting card skeleton 1 (count: 3)
│  │  ██████████████████████████   │  │    #E1E4D5, 12dp radius, shimmer
│  │  ████████████  ████████       │  │    shimmer_duration: short4 (200ms)
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████     ███████████     │  │  ← Meeting card skeleton 2
│  │  ██████████████████████████   │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████     ███████████     │  │  ← Meeting card skeleton 3
│  │  ██████████████████████████   │  │
│  └───────────────────────────────┘  │
│                                     │
├─────────────────────────────────────┤
│   [Home] [Accounts] [Pay] [Profile] │  ← Bottom nav
└─────────────────────────────────────┘
```

**Layout notes:** Skeleton shimmer uses #E1E4D5 (surface_variant). Week strip shows 7 pill-shaped skeleton blocks with 4dp gap. Three meeting card skeletons represent time+chip row + title row + customer row. reduced_motion_fallback: static_placeholder.

---

## Screen: content

```
┌─────────────────────────────────────┐
│                                     │
│  Meetings · May 2026                │  ← headline_large (Outfit 32sp), #4C662B, w700
│                                     │    16dp h-pad, 20dp top, 12dp bottom
│  ┌─────────────────────────────────┐│
│  │Mon  Tue [Wed] Thu  Fri  Sat  Sun││  ← week_strip_calendar — 7 day pills
│  │ 19   20 [21]  22   23   24   25 ││    12dp h-pad, 4dp gap, space-between
│  └─────────────────────────────────┘│    label_small (day) + body_large (date)
│                                     │
│  Today                              │  ← today_button — text variant, #4C662B
│                                     │    (jumps strip to current date)
│  3 meetings this week               │  ← upcoming_section_header
│                                     │    title_medium (Outfit 16sp/500), #1A1C16
│                                     │    16dp h-pad, 8dp top, 10dp bottom
│  ┌───────────────────────────────┐  │
│  ║ 10:00 AM      [Online]        ║  │  ← meeting_card_1
│  │ Account Opening Meeting       │  │    ║ = 4dp left border #4C662B
│  │ John Mwangi · 1 hr · Google   │  │    Time: label_large #4C662B w700
│  │ Meet                          │  │    [Online] chip: #CDEDA3 bg, #4C662B text
│  │ [▶ Join]  [📝 Notes]          │  │    Title: title_small #1A1C16 w700
│  └───────────────────────────────┘  │    Customer: body_medium #44483D
│                                     │    Join: filled #4C662B; Notes: outlined #4C662B
│  ┌───────────────────────────────┐  │
│  ║ 2:00 PM       [In-Person]     ║  │  ← meeting_card_2
│  │ KYC Review                    │  │    ║ = 4dp left border #386663
│  │ Sarah Odhiambo · 30 min ·     │  │    Time: label_large #386663 w700
│  │ Nairobi Branch, Kimathi St    │  │    [In-Person] chip: #DCE7C8 bg, #386663 text
│  └───────────────────────────────┘  │    Title: title_small #1A1C16 w700
│                                     │    Customer/venue: body_medium #44483D
│  ┌───────────────────────────────┐  │
│  ║ Tomorrow · 11:00 AM   [Phone] ║  │  ← meeting_card_3
│  │ New Prospect — Introductory   │  │    ║ = 4dp left border #E8A317 (amber — visual only)
│  │ Call                          │  │    Time: label_large #44483D w700 (a11y fix)
│  │ Peter Kamau · Referral from   │  │    [Phone] chip: #CDEDA3 bg, #44483D text (a11y fix)
│  │ Equity Bank                   │  │    Title: title_small #1A1C16 w700
│  └───────────────────────────────┘  │    Customer: body_medium #44483D
│                                     │
│                    [📅 Schedule Meeting] │  ← schedule_meeting_fab (extended FAB)
│                                     │    #4C662B bg, #FFFFFF text, calendar_add icon
│                                     │    bottom-right: 24dp bottom, 16dp right, elev 6
├─────────────────────────────────────┤
│   [Home] [Accounts] [Pay] [Profile] │  ← bottom nav, 80dp height, #F9FAEF bg
└─────────────────────────────────────┘
```

**Layout notes:**
- Screen background: #F9FAEF (warm off-white).
- Week strip day pills: unselected = #F9FAEF bg, #1A1C16/#44483D text; selected (Wed) = #4C662B bg, #CDEDA3 label, #FFFFFF date, w700.
- Weekend dates (Sat 24, Sun 25): body_large #44483D (muted).
- Meeting cards: #FFFFFF fill, 12dp radius, 16dp h-margin, 16dp internal pad, 10dp bottom-margin, elevation 2.
- Left accent borders: meeting_1 #4C662B, meeting_2 #386663, meeting_3 #E8A317 (border only — NOT used for text).
- A11y fix (A11Y-002): meeting_3 time + chip text use #44483D instead of #E8A317 (#E8A317 ratio ≤1.68:1 on white — FAIL; #44483D ≥7.25:1 — PASS).
- Join button (meeting_1): filled #4C662B, video_call icon, 16/6dp h/v pad, 8dp radius, label_medium.
- Notes button (meeting_1): outlined #4C662B, note icon, same size.
- Extended FAB: fixed bottom-right; text + calendar_add icon; elevation 6 (level3).

---

## Screen: content (Schedule Dialog open)

```
┌─────────────────────────────────────┐
│  [... content dimmed by scrim ...]  │  ← #000000 scrim at ~40% opacity
│                                     │
│  ╔═════════════════════════════════╗ │
│  ║  Schedule Meeting               ║ │  ← create_meeting_sheet dialog
│  ║  ─────────────────────────────  ║ │    #FFFFFF, 20dp radius, 20dp pad
│  ║  ┌─────────────────────────┐   ║ │    title_medium #1A1C16 w700, 16dp margin-bottom
│  ║  │ Customer          ⌄     │   ║ │  ← meeting_customer_autocomplete (outlined)
│  ║  │ Search customers...     │   ║ │    placeholder body_medium #44483D
│  ║  └─────────────────────────┘   ║ │
│  ║  ┌─────────────────────────┐   ║ │
│  ║  │ Date & Time        📅   │   ║ │  ← meeting_date_picker (outlined + suffix icon)
│  ║  │ 22 May 2026 · 10:00 AM  │   ║ │    suffix: calendar_today #44483D
│  ║  └─────────────────────────┘   ║ │
│  ║  ┌─────────────────────────┐   ║ │
│  ║  │ Duration           ⌄    │   ║ │  ← meeting_duration_select (outlined select)
│  ║  │ 30 minutes              │   ║ │    options: 15min / 30min / 45min / 1hr / 1.5hr / 2hr
│  ║  └─────────────────────────┘   ║ │
│  ║  ┌─────────────────────────┐   ║ │
│  ║  │ Meeting Type       ⌄    │   ║ │  ← meeting_type_select (outlined select)
│  ║  │ Online (Google Meet)    │   ║ │    options: In-Person / Online (Google Meet) / Phone Call
│  ║  └─────────────────────────┘   ║ │
│  ║  ┌─────────────────────────┐   ║ │
│  ║  │ Notes                   │   ║ │  ← meeting_notes_input (outlined textarea)
│  ║  │ Agenda, location        │   ║ │    3–6 lines; placeholder body_medium #44483D
│  ║  │ details, documents...   │   ║ │
│  ║  └─────────────────────────┘   ║ │
│  ║  ┌─────────────────────────┐   ║ │
│  ║  │    Confirm Meeting      │   ║ │  ← confirm_meeting_button
│  ║  └─────────────────────────┘   ║ │    filled, #4C662B bg, #FFFFFF text, fillWidth
│  ╚═════════════════════════════════╝ │
└─────────────────────────────────────┘
```

**Layout notes:** Dialog sits on scrim; Escape key dismisses. Loading indicator shown inside dialog while POST is in-flight. Each input uses outlined variant (4dp radius per text_field token), 56dp field height, 12dp margin-bottom between fields (16dp before confirm button). All labels in label_small (Outfit 11sp/500) with on_surface_variant #44483D.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│                                     │
│  Meetings · May 2026                │  ← Title unchanged
│                                     │
│  ┌─────────────────────────────────┐│
│  │Mon  Tue [Wed] Thu  Fri  Sat  Sun││  ← Week strip unchanged (still navigable)
│  └─────────────────────────────────┘│
│  Today                              │
│                                     │
│                                     │
│           [event_available]         │  ← event_available icon, icon-2xl (48dp), #75796C centered
│                                     │
│       No Meetings Scheduled         │  ← title_medium (Outfit 16sp/500), #1A1C16, center
│                                     │
│  Tap the button below to schedule   │
│  your first meeting for this week   │  ← body_medium (Outfit 14sp/400), #44483D, center
│                                     │
│                                     │
│                    [📅 Schedule Meeting] │  ← FAB still visible + accessible
│                                     │
├─────────────────────────────────────┤
│   [Home] [Accounts] [Pay] [Profile] │
└─────────────────────────────────────┘
```

**Layout notes:** Empty state body: 32dp padding, showEmptyState: true. icon: event_available (icon-2xl 48dp), title: "No Meetings Scheduled", subtitle: "Tap the button below to schedule your first meeting for this week". Week strip remains functional to allow day navigation. FAB persists so user can immediately schedule.

---

## Screen: error

```
┌─────────────────────────────────────┐
│                                     │
│  Meetings · May 2026                │  ← Title unchanged
│                                     │
│  ┌─────────────────────────────────┐│
│  │Mon  Tue [Wed] Thu  Fri  Sat  Sun││  ← Week strip preserved
│  └─────────────────────────────────┘│
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ⚠ Could not load schedule.   │  │  ← banner (error type)
│  │    Please try again.          │  │    error_outline icon, #BA1A1A
│  │                               │  │    body_medium #1A1C16
│  │         [  Retry  ]           │  │  ← outlined button #4C662B
│  └───────────────────────────────┘  │
│                                     │
├─────────────────────────────────────┤
│   [Home] [Accounts] [Pay] [Profile] │
└─────────────────────────────────────┘
```

**Layout notes:** Error state: 16dp screen padding, showErrorBanner: true. Banner component (registered) with retry: true. Week strip preserved so user can attempt a different day. No FAB shown during error state (cannot schedule without meeting list context).

---

## Design Checklist (Figma / Stitch)

- [ ] Screen title "Meetings · May 2026" — headline_large (Outfit 32sp), #4C662B, weight 700; 16dp h-pad, 20dp top, 12dp bottom
- [ ] 7-day week strip: selected pill (Wed 21) = #4C662B bg, #CDEDA3 label, #FFFFFF date w700; unselected = #F9FAEF bg, #44483D label, #1A1C16 date w600
- [ ] Weekend day dates (Sat/Sun): #44483D (muted) instead of #1A1C16
- [ ] "Today" text button: #4C662B text, text variant (no bg)
- [ ] "3 meetings this week" section header — title_medium (Outfit 16sp/500), #1A1C16
- [ ] meeting_card_1: #FFFFFF fill, 12dp radius, 2dp elev, 4dp left border #4C662B; time "10:00 AM" label_large #4C662B w700
- [ ] meeting_card_1 Online chip: #CDEDA3 bg, #4C662B text, label_small, 12dp radius
- [ ] meeting_card_1 "Account Opening Meeting" — title_small #1A1C16 w700
- [ ] meeting_card_1 customer "John Mwangi · 1 hr · Google Meet" — body_medium #44483D
- [ ] meeting_card_1 Join button: filled #4C662B, video_call icon, label_medium; Notes button: outlined #4C662B, note icon
- [ ] meeting_card_2: 4dp left border #386663; time "2:00 PM" label_large #386663 w700
- [ ] meeting_card_2 In-Person chip: #DCE7C8 bg, #386663 text, label_small, 12dp radius
- [ ] meeting_card_3: 4dp left border #E8A317 (border only); time "Tomorrow · 11:00 AM" label_large #44483D w700 (a11y fix)
- [ ] meeting_card_3 Phone chip: #CDEDA3 bg, #44483D text (a11y fix — NOT #E8A317 on any text)
- [ ] Extended FAB "Schedule Meeting": #4C662B bg, #FFFFFF text, calendar_add icon, bottom-right, elev 6 (level3)
- [ ] Schedule dialog: #FFFFFF, 20dp radius, 5 outlined inputs (Customer/Date/Duration/Type/Notes), Confirm button fillWidth #4C662B
- [ ] Skeleton shimmer on loading: #E1E4D5, 7 pill skeletons + 1 header + 3 card skeletons, shimmer_duration 200ms
- [ ] Empty state: event_available icon 48dp #75796C, "No Meetings Scheduled" title_medium, subtitle body_medium #44483D
- [ ] Error state: error banner with retry button outlined #4C662B
- [ ] All text: Outfit typeface. Minimum text size 14sp. Touch targets 48dp minimum. 16dp standard h-padding.

---

_Generated by /idea export | 2026-05-30_
