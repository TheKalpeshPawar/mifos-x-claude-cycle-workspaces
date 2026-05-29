# SPEC — Meetings

| Field         | Value               |
|---------------|---------------------|
| Feature       | meetings            |
| Flavor        | fieldOfficer        |
| Status        | approved            |
| Quality Score | 97                  |
| ViewModel     | MeetingsViewModel   |

---

## Overview

The Meetings screen is the primary scheduling surface for Field Officer persona users. It presents a horizontal week-strip calendar at the top (Mon–Sun day pills, one selected at a time) and a chronological list of meeting cards for the selected day below. Wednesday 21 is the default selected day, shown with `#4C662B` fill and white text; weekend days (Sat/Sun) use `#44483D` muted date numbers. Each meeting card shows the meeting time, type chip (Online / In-Person / Phone), meeting title, customer name, duration, and venue/platform with a 4dp colored left accent border differentiating type. Online meetings expose "Join" (filled) and "Notes" (outlined) action buttons inline. A floating "Schedule Meeting" extended FAB at bottom-right opens a dialog sheet with customer autocomplete, date/time picker, duration select, type select, and a notes textarea. The screen maps to OBP endpoints `GET /obp/v3.1.0/banks/{bankId}/meetings` (load list) and `POST /obp/v3.1.0/banks/{bankId}/meetings` (create meeting). All four UI states are covered: loading (skeleton shimmer), content (week strip + 3 cards), empty (event_available icon + CTA), and error (retry banner).

---

## Screens

| ID             | Name               | Route      | Layout     | Scroll   |
|----------------|--------------------|------------|------------|----------|
| meetings-main  | Meeting Scheduler  | /meetings  | index_list | Vertical |

**Shell:** Field Officer flavor — bottom navigation bar (4 tabs: Home, Accounts, Payments, Profile). Meetings is reachable from the Field Officer home dashboard; no dedicated nav tab.

---

## Components

| ID                            | Type   | Description                                                                                                                                            |
|-------------------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| meetings_title                | text   | "Meetings · May 2026" — Outfit/headline_large, #4C662B, w700, 16dp h-pad, 20dp top, 12dp bottom; heading L1                                          |
| week_strip_calendar           | stack  | Horizontal strip, 12dp h-pad, 12dp bottom-pad, 4dp gap, space-between — 7 day-pill boxes (role: tablist); loads from obp_get_meetings                 |
| day_mon                       | box    | Mon · 19 — #F9FAEF fill, 12dp radius, 8/10dp v/h pad; on_click→select_day(monday)                                                                    |
| day_mon_label                 | text   | "Mon" — Outfit/label_small, #44483D, 2dp margin-bottom                                                                                                 |
| day_mon_date                  | text   | "19" — Outfit/body_large, #1A1C16, w600                                                                                                                |
| day_tue                       | box    | Tue · 20 — #F9FAEF fill, 12dp radius; on_click→select_day(tuesday)                                                                                    |
| day_tue_label                 | text   | "Tue" — Outfit/label_small, #44483D                                                                                                                    |
| day_tue_date                  | text   | "20" — Outfit/body_large, #1A1C16, w600                                                                                                                |
| day_wed                       | box    | Wed · 21 (SELECTED) — #4C662B fill, 12dp radius; role: tab; selected=true; on_click→select_day(wednesday)                                             |
| day_wed_label                 | text   | "Wed" — Outfit/label_small, #CDEDA3 (inverted on selected bg)                                                                                          |
| day_wed_date                  | text   | "21" — Outfit/body_large, #FFFFFF, w700                                                                                                                |
| day_thu                       | box    | Thu · 22 — #F9FAEF fill; on_click→select_day(thursday)                                                                                                 |
| day_thu_label                 | text   | "Thu" — Outfit/label_small, #44483D                                                                                                                    |
| day_thu_date                  | text   | "22" — Outfit/body_large, #1A1C16, w600                                                                                                                |
| day_fri                       | box    | Fri · 23 — #F9FAEF fill; on_click→select_day(friday)                                                                                                  |
| day_fri_label                 | text   | "Fri" — Outfit/label_small, #44483D                                                                                                                    |
| day_fri_date                  | text   | "23" — Outfit/body_large, #1A1C16, w600                                                                                                                |
| day_sat                       | box    | Sat · 24 — #F9FAEF fill; on_click→select_day(saturday)                                                                                                 |
| day_sat_label                 | text   | "Sat" — Outfit/label_small, #44483D                                                                                                                    |
| day_sat_date                  | text   | "24" — Outfit/body_large, #44483D, w600 (weekend muted)                                                                                                |
| day_sun                       | box    | Sun · 25 — #F9FAEF fill; on_click→select_day(sunday)                                                                                                  |
| day_sun_label                 | text   | "Sun" — Outfit/label_small, #44483D                                                                                                                    |
| day_sun_date                  | text   | "25" — Outfit/body_large, #44483D, w600 (weekend muted)                                                                                                |
| today_button                  | button | "Today" — text variant, #4C662B text, 16dp h-pad, 4dp margin-bottom; on_click→jump_to_today(current_day)                                             |
| upcoming_section_header       | text   | "3 meetings this week" — Outfit/title_medium, #1A1C16, 16dp h-pad, 8dp top, 10dp bottom; heading L2; derives count from obp_get_meetings              |
| meeting_card_1                | box    | #FFFFFF card, 12dp radius, 16dp pad, 16dp h-margin, 10dp margin-bottom, elev 2, 4dp left border #4C662B; on_click→view_meeting_detail(meeting_account_opening) |
| meeting_1_header              | stack  | Horizontal, space-between, flex-start — time + type chip row                                                                                          |
| meeting_1_time                | text   | "10:00 AM" — Outfit/label_large, #4C662B, w700                                                                                                        |
| meeting_1_type_chip           | box    | #CDEDA3 fill, 12dp radius, 10dp h-pad, 4dp v-pad; role: status                                                                                        |
| meeting_1_type_text           | text   | "Online" — Outfit/label_small, #4C662B, w600                                                                                                           |
| meeting_1_title               | text   | "Account Opening Meeting" — Outfit/title_small, #1A1C16, w700, 2dp margin-bottom                                                                      |
| meeting_1_customer            | text   | "John Mwangi · 1 hr · Google Meet" — Outfit/body_medium, #44483D, 10dp margin-bottom                                                                  |
| meeting_1_actions             | stack  | Horizontal, 8dp gap — Join + Notes buttons                                                                                                             |
| meeting_1_join_button         | button | "Join" — filled, #4C662B bg, #FFFFFF text, video_call icon, 16/6dp h/v pad, 8dp radius, label_medium; on_click→join_meeting(google_meet_link)         |
| meeting_1_notes_button        | button | "Notes" — outlined, #4C662B border+text, note icon, 16/6dp h/v pad, 8dp radius; on_click→view_meeting_detail(meeting_notes_account_opening)           |
| meeting_card_2                | box    | #FFFFFF card, 12dp radius, 16dp pad, 16dp h-margin, 10dp margin-bottom, elev 2, 4dp left border #386663; on_click→view_meeting_detail(meeting_kyc_review) |
| meeting_2_header              | stack  | Horizontal, space-between, flex-start                                                                                                                  |
| meeting_2_time                | text   | "2:00 PM" — Outfit/label_large, #386663, w700                                                                                                          |
| meeting_2_type_chip           | box    | #DCE7C8 fill, 12dp radius, 10dp h-pad, 4dp v-pad; role: status                                                                                        |
| meeting_2_type_text           | text   | "In-Person" — Outfit/label_small, #386663, w600                                                                                                        |
| meeting_2_title               | text   | "KYC Review" — Outfit/title_small, #1A1C16, w700, 2dp margin-bottom                                                                                   |
| meeting_2_customer            | text   | "Sarah Odhiambo · 30 min · Nairobi Branch, Kimathi St" — Outfit/body_medium, #44483D                                                                  |
| meeting_card_3                | box    | #FFFFFF card, 12dp radius, 16dp pad, 16dp h-margin, 10dp margin-bottom, elev 2, 4dp left border #E8A317; on_click→view_meeting_detail(meeting_new_prospect) |
| meeting_3_header              | stack  | Horizontal, space-between, flex-start                                                                                                                  |
| meeting_3_time                | text   | "Tomorrow · 11:00 AM" — Outfit/label_large, #44483D, w700 (a11y-fixed from #E8A317 — was ≤1.68:1 on white, FAIL; #44483D ≥7.25:1 PASS)              |
| meeting_3_type_chip           | box    | #CDEDA3 fill, 12dp radius, 10dp h-pad, 4dp v-pad; role: status                                                                                        |
| meeting_3_type_text           | text   | "Phone" — Outfit/label_small, #44483D, w600 (a11y-fixed from #E8A317)                                                                                  |
| meeting_3_title               | text   | "New Prospect — Introductory Call" — Outfit/title_small, #1A1C16, w700, 2dp margin-bottom                                                              |
| meeting_3_customer            | text   | "Peter Kamau · Referral from Equity Bank" — Outfit/body_medium, #44483D                                                                               |
| schedule_meeting_fab          | button | "Schedule Meeting" — extended FAB, #4C662B bg, #FFFFFF text, calendar_add icon, position bottom-right, 24dp bottom/16dp right margin, elev 6; on_click→schedule_meeting(create_meeting_sheet) |
| create_meeting_sheet          | box    | Dialog, #FFFFFF, 20dp radius, 20dp pad, conditionalVisible; keyboard shortcut: Escape→dismiss; binds to obp_create_meeting                             |
| create_sheet_heading          | text   | "Schedule Meeting" — Outfit/title_medium, #1A1C16, w700, 16dp margin-bottom; heading L2                                                               |
| meeting_customer_autocomplete | input  | "Customer" — outlined, autocomplete, placeholder "Search customers...", 12dp margin-bottom; on_click→search_customer                                   |
| meeting_date_picker           | input  | "Date & Time" — outlined, text, placeholder "22 May 2026 · 10:00 AM", suffix: calendar_today, 12dp margin-bottom; on_click→open_date_picker           |
| meeting_duration_select       | input  | "Duration" — outlined, select (15 min / 30 min / 45 min / 1 hr / 1.5 hrs / 2 hrs), 12dp margin-bottom; on_click→open_duration_picker                 |
| meeting_type_select           | input  | "Meeting Type" — outlined, select (In-Person / Online (Google Meet) / Phone Call), 12dp margin-bottom; on_click→open_type_picker                     |
| meeting_notes_input           | input  | "Notes" — outlined, textarea, placeholder "Agenda, location details, documents to bring...", 3–6 lines, 16dp margin-bottom                            |
| confirm_meeting_button        | button | "Confirm Meeting" — filled, #4C662B bg, #FFFFFF text, fillWidth; on_click→confirm_meeting(meetings)                                                   |

---

## States

| ID      | Trigger                               | Description                                                                                                   |
|---------|---------------------------------------|---------------------------------------------------------------------------------------------------------------|
| loading | Screen entry / RetryLoad              | skeleton (count 7) for week strip; skeleton (count 1) for section header; skeleton (count 3) for meeting cards; shimmer_duration: short4 (200ms) |
| content | obp_get_meetings success              | Title + week strip + "3 meetings this week" header + 3 meeting cards + schedule FAB; bg #F9FAEF              |
| empty   | obp_get_meetings returns empty list   | Title + week strip visible; empty state box: event_available icon + "No Meetings Scheduled" + "Tap the button below to schedule your first meeting for this week" + FAB |
| error   | obp_get_meetings network/auth failure | Title + week strip visible; error banner: "Could not load schedule. Please try again." + retry; 16dp padding |

---

## State Model

**ViewModel:** `MeetingsViewModel`
**Screen State Type:** `MeetingsScreenState`

| Name                | Type             | Default          |
|---------------------|------------------|------------------|
| meetings            | List\<Meeting\>  | emptyList()      |
| selectedDate        | LocalDate        | LocalDate.today  |
| filteredMeetings    | List\<Meeting\>  | emptyList()      |
| isScheduleSheetOpen | Boolean          | false            |
| scheduleDraft       | MeetingDraft?    | null             |
| isSubmitting        | Boolean          | false            |

**Events:** `DaySelected`, `MeetingSelected`, `MeetingScheduled`, `MeetingJoined`, `SheetOpened`, `SheetDismissed`

**Actions:** `select_day(target: String)`, `jump_to_today()`, `view_meeting_detail(meetingId: String)`, `join_meeting(url: String)`, `schedule_meeting()`, `confirm_meeting(draft: MeetingDraft)`, `open_date_picker()`, `open_duration_picker()`, `open_type_picker()`, `search_customer(query: String)`

**DI Dependencies:** `MeetingsRepository`, `CalendarService`, `CustomerSearchService`

**Errors:**
- `LOAD_FAILED`: "Could not load meetings. Check your connection and try again."
- `SCHEDULE_FAILED`: "Could not schedule meeting. Check your connection and try again."
- `NETWORK_UNAVAILABLE`: "No network connection."

---

## Navigation

| From     | To                             | Trigger                                          | Type     |
|----------|--------------------------------|--------------------------------------------------|----------|
| meetings | meeting-detail                 | meeting_card_1 tap → view_meeting_detail(meeting_account_opening)  | push     |
| meetings | meeting-detail                 | meeting_card_2 tap → view_meeting_detail(meeting_kyc_review)       | push     |
| meetings | meeting-detail                 | meeting_card_3 tap → view_meeting_detail(meeting_new_prospect)     | push     |
| meetings | meeting-detail (notes)         | meeting_1_notes_button tap → view_meeting_detail(meeting_notes_account_opening) | push |
| meetings | external: google_meet_link     | meeting_1_join_button tap → join_meeting(google_meet_link)         | external |
| meetings | create_meeting_sheet (dialog)  | schedule_meeting_fab tap → schedule_meeting      | dialog   |
| meetings | meetings (reload)              | confirm_meeting_button tap → confirm_meeting on success            | dismiss  |
| meetings | customer-detail                | customer-detail dependency                       | push     |
| meetings | customer-messages              | customer-messages dependency                     | push     |

---

## API Endpoints

| Endpoint                                          | Auth        | Tag      | Purpose                                                                  |
|---------------------------------------------------|-------------|----------|--------------------------------------------------------------------------|
| GET /obp/v3.1.0/banks/{bankId}/meetings           | DirectLogin | Meetings | Fetch all meetings for bank; client-side filter by selectedDate          |
| POST /obp/v3.1.0/banks/{bankId}/meetings          | DirectLogin | Meetings | Create meeting — requires creator + invitees nested contact_details body |

---

## Design Tokens

| Token                              | Value          | Usage                                                                                             |
|------------------------------------|----------------|---------------------------------------------------------------------------------------------------|
| colors.light.primary               | #4C662B        | Screen title, selected day pill bg, meeting_1 time + chip text + left border, Join button bg, FAB bg, today button text, confirm button bg |
| colors.light.primary_container     | #CDEDA3        | meeting_1 type chip bg, meeting_3 type chip bg, selected day label text (inverted)               |
| colors.light.secondary             | #386663        | meeting_2 time color, meeting_2 chip text, meeting_2 left border                                 |
| colors.light.secondary_container   | #DCE7C8        | meeting_2 type chip bg (In-Person)                                                               |
| colors.light.pending               | #E8A317        | meeting_3 left border accent (visual-only — NOT used for text per a11y fix A11Y-002)             |
| colors.light.background            | #F9FAEF        | Screen base, unselected day pill bg                                                              |
| colors.light.surface               | #FFFFFF        | Meeting card fill, dialog sheet fill                                                             |
| colors.light.on_surface            | #1A1C16        | Meeting card titles, selected-day date numbers (unselected), section header                      |
| colors.light.on_surface_variant    | #44483D        | Day strip labels (Mon/Tue…), customer/duration/venue lines, meeting_3 time + chip text (a11y fix) |
| colors.light.on_primary            | #FFFFFF        | Selected Wed date number, FAB label, Join button text, confirm button text                       |
| typography.headline_large          | Outfit 32sp    | "Meetings · May 2026" screen title                                                               |
| typography.title_medium            | Outfit 16sp/500| "3 meetings this week" header, dialog "Schedule Meeting" heading                                 |
| typography.title_small             | Outfit 14sp/500| Meeting card title text (Account Opening Meeting, KYC Review, New Prospect…)                    |
| typography.label_large             | Outfit 14sp/500| Meeting time stamps per card                                                                     |
| typography.label_small             | Outfit 11sp/500| Type chip labels (Online / In-Person / Phone), day strip abbreviations                          |
| typography.label_medium            | Outfit 12sp/500| Join / Notes / confirm button text                                                               |
| typography.body_large              | Outfit 16sp/400| Day-number date text in week strip                                                               |
| typography.body_medium             | Outfit 14sp/400| Customer + duration + venue lines per card                                                       |
| radius.md                          | 12dp           | Day pills, meeting cards, type chips                                                             |
| radius.sm                          | 8dp            | Join / Notes action buttons                                                                      |
| radius.lg                          | 16dp           | Dialog sheet (source declares 20dp — nearest token; source-declared value used in codegen)       |
| elevation.level2                   | 3dp            | Meeting cards (source elevation: 2)                                                              |
| elevation.level3                   | 6dp            | Schedule Meeting extended FAB                                                                    |
| touchTargets.min_touch_target      | 48dp           | Day pill tap zones, meeting card, FAB, all buttons                                               |
| motion.duration.short4             | 200ms          | Skeleton shimmer duration for loading state                                                      |

---

_Generated by /idea export | 2026-05-30_
