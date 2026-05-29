# SPEC — Meetings

| Field         | Value              |
|---------------|--------------------|
| Feature       | meetings           |
| Flavor        | fieldOfficer       |
| Status        | approved           |
| Quality Score | 97                 |
| ViewModel     | MeetingsViewModel  |

---

## Overview

The Meetings screen is the field officer's scheduling hub — a weekly calendar strip and a chronological meeting list for the selected day. The 7-day strip allows day-by-day filtering; Wednesday 21 is the selected day in the default state, shown with `#4C662B` fill and white text. Three meeting cards display time, meeting type chip (Online/In-Person/Phone), customer name, duration, and location with a colored left 4dp accent border differentiating type. Online meetings expose "Join" (filled) and "Notes" (outlined) action buttons inline. A floating extended FAB (calendar_add icon) opens a dialog form for scheduling new meetings with customer autocomplete, date/time picker, duration select, type select, and notes textarea. The screen is navigated to from the Field Officer dashboard.

---

## Screens

| ID             | Name              | Route     | Layout     | Scroll   |
|----------------|-------------------|-----------|------------|----------|
| meetings-main  | Meeting Scheduler | /meetings | index_list | Vertical |

**Shell:** Field Officer flavor — Top app bar with "Meetings" title and back arrow. Field Officer bottom navigation bar (5 tabs).

| Nav Item     | ID                | Icon        | Target               |
|--------------|-------------------|-------------|----------------------|
| Dashboard    | nav_dashboard     | dashboard   | fo-dashboard         |
| Customers    | nav_customers     | people      | customer-search      |
| Applications | nav_applications  | description | account-applications |
| Messages     | nav_messages      | mail        | customer-messages    |
| More         | nav_more          | more_vert   | settings             |

---

## Components

| ID                      | Type   | Description                                                                                                                                       |
|-------------------------|--------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| meetings_title          | text   | "Meetings · May 2026" — headline_large, `#4C662B`, weight 700, 20dp horizontal padding, 20dp top, 12dp bottom                                    |
| week_strip_calendar     | stack  | Horizontal 7-day strip, 12dp horizontal padding, 4dp gap. Each day-pill: 8dp vertical, 10dp horizontal padding, 12dp radius. Mon/Tue/Thu–Sun: `#F9FAEF` bg. Wed (selected): `#4C662B` bg |
| day_mon                 | box    | Mon · 19 — "Mon" label_small `#44483D`, "19" body_large `#1A1C16` bold                                                                          |
| day_tue                 | box    | Tue · 20 — "Tue" label_small `#44483D`, "20" body_large `#1A1C16` bold                                                                          |
| day_wed                 | box    | **Selected** — Wed · 21 — `#4C662B` bg, "Wed" label_small `#CDEDA3`, "21" body_large `#FFFFFF` weight 700                                       |
| day_thu                 | box    | Thu · 22 — "Thu" label_small `#44483D`, "22" body_large `#1A1C16` bold                                                                          |
| day_fri                 | box    | Fri · 23 — "Fri" label_small `#44483D`, "23" body_large `#1A1C16` bold                                                                          |
| day_sat                 | box    | Sat · 24 — "Sat" label_small `#44483D`, "24" body_large `#44483D` bold (weekend muted)                                                          |
| day_sun                 | box    | Sun · 25 — "Sun" label_small `#44483D`, "25" body_large `#44483D` bold (weekend muted)                                                          |
| today_button            | button | Text button, `#4C662B` text, "Today" — 16dp horizontal padding, 4dp bottom margin. Jumps calendar to current date                               |
| upcoming_section_header | text   | "3 meetings this week" — title_medium, `#1A1C16`, 16dp horizontal padding, 8dp top, 10dp bottom                                                  |
| meeting_card_1          | box    | White card (12dp radius, 16dp padding, 16dp margin-horizontal, 10dp margin-bottom, elevation 2, 4dp left accent `#4C662B`). 10:00 AM "Account Opening Meeting" with John Mwangi, 1 hr, Google Meet. "Online" chip (`#CDEDA3` bg, `#4C662B` text). [Join] filled button + [Notes] outlined button |
| meeting_card_2          | box    | White card (4dp left accent `#386663`). 2:00 PM "KYC Review" with Sarah Odhiambo, 30 min, Nairobi Branch, Kimathi St. "In-Person" chip (`#DCE7C8` bg, `#386663` text). No inline actions |
| meeting_card_3          | box    | White card (4dp left accent `#E8A317`). "Tomorrow · 11:00 AM" "New Prospect — Introductory Call" with Peter Kamau, Referral from Equity Bank. "Phone" chip (`#CDEDA3` bg, `#44483D` text) |
| schedule_meeting_fab    | button | Extended FAB, `#4C662B` bg, `#FFFFFF` text, calendar_add icon, "Schedule Meeting", bottom-right, 24dp bottom margin, 16dp right margin, elevation 6 |
| create_meeting_sheet    | box    | Dialog (20dp radius, `#FFFFFF`, 20dp padding). Contains: "Schedule Meeting" title (title_medium bold) + customer autocomplete + date/time outlined input (calendar_today suffix icon) + duration select (15min/30min/45min/1hr/1.5hr/2hr) + meeting type select (In-Person/Online Google Meet/Phone Call) + notes textarea (3–6 lines) + "Confirm Meeting" filled button `#4C662B` |

---

## States

| ID      | Trigger                            | Description                                                                      |
|---------|------------------------------------|----------------------------------------------------------------------------------|
| loading | Screen entry                       | Shimmer skeleton for 7 day-pill strip, section header, and 3 meeting card stubs |
| content | Meetings loaded                    | Calendar strip + 3 meeting cards visible; bg `#F9FAEF`                           |
| empty   | No meetings for selected week      | Empty state: event_available icon + "No Meetings Scheduled" + subtitle + FAB     |
| error   | API call fails                     | Error banner with retry; 16dp padding                                            |

---

## State Model

**ViewModel:** `MeetingsViewModel`
**Screen State Type:** `MeetingsScreenState`

| Name                | Type           | Default        |
|---------------------|----------------|----------------|
| meetings            | List\<Meeting\>| emptyList()    |
| selectedDate        | LocalDate      | LocalDate.today|
| filteredMeetings    | List\<Meeting\>| emptyList()    |
| isScheduleSheetOpen | Boolean        | false          |
| scheduleDraft       | MeetingDraft?  | null           |
| isSubmitting        | Boolean        | false          |

**Events:** `DaySelected`, `MeetingSelected`, `MeetingScheduled`, `MeetingJoined`, `SheetOpened`, `SheetDismissed`

**Actions:** `select_day(date: LocalDate)`, `jump_to_today()`, `view_meeting_detail(meetingId: String)`, `join_meeting(url: String)`, `schedule_meeting()`, `confirm_meeting(draft: MeetingDraft)`, `open_date_picker()`, `open_duration_picker()`, `open_type_picker()`, `search_customer(query: String)`

**DI Dependencies:** `MeetingsRepository`, `CalendarService`, `CustomerSearchService`

**Errors:**
- `LOAD_FAILED`: "Could not load meetings. Check your connection and try again."
- `SCHEDULE_FAILED`: "Could not schedule meeting. Check your connection and try again."
- `NETWORK_UNAVAILABLE`: "No network connection."

---

## Navigation

| From     | To                      | Trigger                         | Type     |
|----------|-------------------------|---------------------------------|----------|
| meetings | google_meet_link        | meeting_1_join_button tap       | external |
| meetings | meeting_notes_account_opening | meeting_1_notes_button tap | push     |
| meetings | meeting_account_opening | meeting_card_1 tap              | push     |
| meetings | meeting_kyc_review      | meeting_card_2 tap              | push     |
| meetings | meeting_new_prospect    | meeting_card_3 tap              | push     |
| meetings | create_meeting_sheet    | schedule_meeting_fab tap        | dialog   |
| meetings | meetings                | confirm_meeting_button tap (success) | dismiss dialog |

---

## API Endpoints

| Endpoint                                 | Auth        | Tag      | Purpose                                             |
|------------------------------------------|-------------|----------|-----------------------------------------------------|
| GET /obp/v3.1.0/banks/{bankId}/meetings  | DirectLogin | Meetings | Load all meetings for bank; filter client-side by selectedDate |
| POST /obp/v3.1.0/banks/{bankId}/meetings | DirectLogin | Meetings | Create new meeting with creator + invitees + purpose_id |

---

## Design Tokens

| Token                         | Value     | Usage                                                                       |
|-------------------------------|-----------|-----------------------------------------------------------------------------|
| color.light.primary           | #4C662B   | Title, selected day bg, online meeting left accent and time, Join button, FAB bg, today button text, confirm button |
| color.light.primary_container | #CDEDA3   | Selected day label, Online chip bg, Phone chip bg (shared with primary_container) |
| color.light.secondary         | #386663   | In-person meeting left accent and time label                                |
| color.light.secondary_container | #DCE7C8 | In-person chip bg, nav active indicator                                     |
| color.pending                 | #E8A317   | Phone/upcoming meeting card left accent border                              |
| color.light.surface           | #FFFFFF   | Meeting cards, create meeting dialog                                        |
| color.light.background        | #F9FAEF   | Screen background, unselected day pill bg                                   |
| color.light.on_surface        | #1A1C16   | Meeting title text, date number (active)                                    |
| color.light.on_surface_variant| #44483D   | Day strip labels, meeting customer/details text, weekend date numbers       |
| color.light.on_primary        | #FFFFFF   | Selected day date number, FAB text, Join button text                        |
| typography.headline_large     | —         | "Meetings · May 2026" screen title                                          |
| typography.title_medium       | —         | Upcoming section header, create meeting dialog title                        |
| typography.title_small        | —         | Meeting card title text                                                     |
| typography.label_large        | —         | Meeting time in cards (weight 700)                                          |
| typography.label_medium       | —         | Join/Notes button text                                                      |
| typography.label_small        | —         | Day strip abbreviations, meeting type chip text                             |
| typography.body_large         | —         | Day date numbers in strip                                                   |
| typography.body_medium        | —         | Meeting customer + duration + location                                      |
| spacing.md                    | 16dp      | Card horizontal margin, section header padding                              |
| spacing.sm                    | 8dp       | Gap between Join/Notes buttons                                              |
| radius.md                     | 12dp      | Meeting card border-radius, day pill radius                                 |
| elevation.level2              | 3dp       | Meeting card elevation                                                      |

---

_Generated by /idea export | 2026-05-29_
