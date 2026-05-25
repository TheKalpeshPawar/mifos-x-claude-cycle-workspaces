# Mockup Specification: Meetings

| Field | Value |
|---|---|
| Feature | meetings |
| Flavor | fieldOfficer |
| Archetype | index_list |

---

## Screen Layout

```
[ Status Bar ]
[ "Meetings · May 2026" ]          ← headline_large #1800B1 w700, ph:16 pt:20 pb:12
[ WEEK STRIP CALENDAR ]            ← horizontal 7-day strip, ph:12 pb:12, gap:4
  [Mon][Tue][Wed*][Thu][Fri][Sat][Sun]
  19   20   21    22   23   24   25
  (*) Wed selected = bg:#1800B1, date white, label #B0B8FF
      Others      = bg:#F0F0F0, date #1A1A1A, label #666666
      Weekend     = #BDBDBD date, #999999 label (muted)
[ Today ] ← text button #1800B1, ph:16 mb:4
[ "3 meetings this week" ]         ← title_medium #1A1A1A ph:16 pt:8 pb:10
──────────────────────────────────────────────────
┌─ MEETING CARD 1 (ONLINE) ───────────────────────┐  bg:#FFFFFF br:12 elevation:2
│ ◼ 4px #1800B1 left accent                       │  mh:16 mb:10 p:16
│                                                 │
│ "10:00 AM"         [Online] #EEF0FF chip        │
│   label_large #1800B1 w700    label_small #1800B1│
│ "Account Opening Meeting" title_small #1A1A1A w700│
│ "John Mwangi · 1 hr · Google Meet" body_medium #666│
│ [▶ Join] [📝 Notes]                             │
│  filled #1800B1  outlined #1800B1               │
└──────────────────────────────────────────────────┘
┌─ MEETING CARD 2 (IN-PERSON) ────────────────────┐  bg:#FFFFFF br:12 elevation:2
│ ◼ 4px #008B8B left accent                       │  mh:16 mb:10 p:16
│                                                 │
│ "2:00 PM"          [In-Person] #E0F7FA chip     │
│   label_large #008B8B w700    label_small #006064│
│ "KYC Review" title_small #1A1A1A w700           │
│ "Sarah Odhiambo · 30 min · Nairobi Branch, Kimathi St" │
└──────────────────────────────────────────────────┘
┌─ MEETING CARD 3 (PHONE) ────────────────────────┐  bg:#FFFFFF br:12 elevation:2
│ ◼ 4px #FF8F00 left accent                       │  mh:16 mb:10 p:16
│                                                 │
│ "Tomorrow · 11:00 AM"  [Phone] #FFF8E1 chip     │
│   label_large #FF8F00 w700    label_small #E65100│
│ "New Prospect — Introductory Call" title_small w700│
│ "Peter Kamau · Referral from Equity Bank" #666  │
└──────────────────────────────────────────────────┘
──────────────────────────────────────────────────
[ FAB: [calendar_add] Schedule Meeting ]  ← extended FAB, bg:#1800B1, bottom-right

  === SCHEDULE BOTTOM SHEET (when FAB tapped) ===
┌─────────────────────────────────────────────────┐
│  ── (drag handle) ──                            │
│  Schedule Meeting          title_medium #1A1A1A │
│  ┌─ Customer ────────────────────────────────┐  │
│  │  Search customers...     autocomplete     │  │
│  └───────────────────────────────────────────┘  │
│  ┌─ Date & Time ─────────────────────────────┐  │
│  │  22 May 2026 · 10:00 AM    [calendar] ▸  │  │
│  └───────────────────────────────────────────┘  │
│  ┌─ Duration ─────────────────────────────── ▾┐ │
│  │  30 minutes (select: 15/30/45/1hr/1.5/2hr) │ │
│  └────────────────────────────────────────────┘ │
│  ┌─ Meeting Type ─────────────────────────── ▾┐ │
│  │  In-Person / Online (Google Meet) / Phone  │ │
│  └────────────────────────────────────────────┘ │
│  ┌─ Notes ─────────────────────────────────────┐│
│  │  Agenda, location details, documents...    ││
│  │  (min 3 lines, max 6 lines textarea)       ││
│  └───────────────────────────────────────────┘ │
│  [ Confirm Meeting ] ← filled #1800B1 full-width│
└─────────────────────────────────────────────────┘
  bg:#FFFFFF, br top:20, p:20
```

---

## Components

### Week Strip Calendar
- **Container:** Horizontal stack, 7 equally-spaced day tiles, padding_horizontal:12, gap:4
- **Day tile (default):** bg:#F0F0F0, border_radius:12, padding 8px vertical / 10px horizontal, vertical stack (label + date)
  - Label: label_small #666666 (weekdays), #999999 (weekends)
  - Date: body_large #1A1A1A weight 600 (weekdays), #BDBDBD (weekends)
- **Selected day tile (Wed 21):** bg:#1800B1; label "Wed" #B0B8FF; date "21" #FFFFFF weight 700
- Tapping any day fires `select_day` event → updates `selectedDate` → re-filters `filteredMeetings`

### Meeting Cards

**Shared structure:**
- bg:#FFFFFF, border_radius:12, elevation:2, padding:16, margin_horizontal:16, margin_bottom:10
- 4px colored left border (accent varies by type)
- Header row: time label (label_large, bold, accent color) + type chip (right-aligned)
- Title: title_small #1A1A1A weight 700, margin_bottom:2
- Detail line: body_medium #666666 with customer name, duration, location/platform

**Card 1 (Account Opening — Online):**
- Left accent: #1800B1; time: "10:00 AM" #1800B1
- Chip: bg:#EEF0FF, text "Online" #1800B1, label_small weight 600
- Actions row: [▶ Join] filled #1800B1 with video_call icon; [📝 Notes] outlined #1800B1 with note icon

**Card 2 (KYC Review — In-Person):**
- Left accent: #008B8B; time: "2:00 PM" #008B8B
- Chip: bg:#E0F7FA, text "In-Person" #006064

**Card 3 (Prospect Call — Phone, Tomorrow):**
- Left accent: #FF8F00; time: "Tomorrow · 11:00 AM" #FF8F00
- Chip: bg:#FFF8E1, text "Phone" #E65100

### Schedule Bottom Sheet
- Customer: autocomplete with live search from CustomerSearchService
- Date/Time: outlined field with calendar_today suffix icon; tapping opens native date+time picker
- Duration: select dropdown with options 15 min, 30 min, 45 min, 1 hour, 1.5 hours, 2 hours
- Meeting Type: select dropdown with In-Person, Online (Google Meet), Phone Call
- Notes: outlined textarea, 3 min / 6 max lines, placeholder "Agenda, location details, documents to bring..."
- Confirm button: filled #1800B1 full-width

---

## Interaction Patterns

| Element | Gesture | Result |
|---|---|---|
| Day tile in strip | Tap | Updates selectedDate; re-filters meeting list for that day |
| Today button | Tap | Jumps selectedDate to today; scrolls strip to today's tile |
| Meeting card (any) | Tap | Pushes to meeting detail view |
| [Join] button (card 1) | Tap | Opens Google Meet link via deep link / external browser |
| [Notes] button (card 1) | Tap | Pushes to meeting notes detail view |
| Schedule Meeting FAB | Tap | Opens create_meeting_sheet bottom sheet |
| Confirm Meeting | Tap | Validates form; submits POST API; closes sheet; refreshes list |
| Swipe down on sheet | Gesture | Dismisses sheet (SheetDismissed event) |

**Loading:** Meeting card areas show shimmer with card-shaped skeletons. Week strip tiles appear as grey rounded rectangles.

**Empty state:** Centered icon (event_available), "No Meetings Scheduled" in title_large, "Tap the button below to schedule your first meeting for this week" in body_medium #757575. Schedule Meeting FAB remains visible.

---

## Content Data

| Card | Time | Title | Customer | Duration | Venue/Type |
|---|---|---|---|---|---|
| Card 1 | 10:00 AM | Account Opening Meeting | John Mwangi | 1 hr | Google Meet (Online) |
| Card 2 | 2:00 PM | KYC Review | Sarah Odhiambo | 30 min | Nairobi Branch, Kimathi St (In-Person) |
| Card 3 | Tomorrow 11:00 AM | New Prospect — Introductory Call | Peter Kamau | — | Referral from Equity Bank (Phone) |

**Week strip data:**
| Day | Date | Meeting count |
|---|---|---|
| Mon | 19 | 0 |
| Tue | 20 | 1 |
| Wed | 21 | 2 (selected) |
| Thu | 22 | 1 |
| Fri | 23 | 0 |
| Sat | 24 | 0 (weekend, muted) |
| Sun | 25 | 0 (weekend, muted) |

---

## Design Notes

**Color-coded meeting types:** The 4px left border accent and the time label color are always the same hue — #1800B1 for online, #008B8B for in-person, #FF8F00 for phone. This creates a perceptual grouping so officers can scan meeting type before reading text.

**Calendar strip interaction:** The strip is a row of tappable day tiles acting as a tab group (role: tablist). The selected state inverts the color — white text on brand purple — creating a strong selected indicator without a complex focus ring.

**"Tomorrow" label:** Meeting card 3 shows "Tomorrow · 11:00 AM" instead of a date number, matching how humans communicate near-future meetings ("I have a call tomorrow") and reducing cognitive overhead of date-to-day translation.

**Join button placement:** Only meeting_card_1 has the [Join] button because it is an online meeting. In-person and phone meetings show no Join button. The [Notes] button is available on all meeting types but shown only on card 1 in the current data set — implementation should show Notes on all cards.

**OBP API nested body:** The POST /meetings body requires deeply nested `creator` and `invitees[].contact_details` objects. The ViewModel's `MeetingDraft` should map cleanly to this shape; consider a dedicated `MeetingDraftMapper` to avoid exposing OBP schema details to the UI layer.

**Accessibility:** Each meeting card has a full-sentence contentDescription (e.g. "10:00 AM Account Opening Meeting with John Mwangi, 1 hour, Online Google Meet"). Day tiles have contentDescription including meeting count (e.g. "Wednesday 21, selected, 2 meetings"). FAB has contentDescription "Schedule a new meeting."

---
_Generated by /idea export | 2026-05-25_
