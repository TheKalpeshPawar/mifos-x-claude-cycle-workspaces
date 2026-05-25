# Feature Specification — Notifications

| Field | Value |
|---|---|
| Feature | notifications |
| Name | Notifications |
| Flavor | consumer |
| Status | designed |
| Quality Score | 88 |

---

## Overview

The Notifications screen is a push notification inbox presenting a chronological, categorised feed of account events for the Mifos X Open Banking consumer. Notifications are grouped into two time-bucketed sections — **Today** (unread, purple-tinted cards) and **Earlier** (read, white cards) — so users can instantly see what requires attention versus what has already been acknowledged.

Four real notification items are rendered in the populated state, spanning three semantic categories:

- **payment** — "Payment of £50.00 received from James Wilson" (unread, Today); "£3,200.00 from Acme Ltd credited" (read, Earlier)
- **security** — "KYC verification approved" (unread, Today)
- **system** — "Direct debit mandate created for Netflix £15.99/month" (read, Earlier)

Push delivery is powered by Firebase Cloud Messaging (FCM). Notification items are persisted to a local Room database for offline-first retrieval. A "Mark All Read" action is available in both the top app bar (done_all icon) and as an inline text button. The screen supports four UI states: loading, populated, empty, and error.

---

## Screens

| Screen ID | Name | Route | Archetype | Scroll |
|---|---|---|---|---|
| notifications | Notifications | /notifications | index_list | vertical |

---

## Shell

| Element | Value |
|---|---|
| Top app bar title | "Notifications" |
| Navigation icon | arrow_back → navigate_back |
| Action 1 | done_all — mark_all_read |
| Action 2 | tune — open_notification_settings |
| Bottom nav | hidden |

---

## Components

### Header Row

| ID | Type | Description |
|---|---|---|
| title_action_row | stack | Horizontal, space-between, center-aligned, padding horizontal 20, top 16, bottom 8 |
| notifications_title | text | "Notifications" headline_large, #1800B1, bold |
| mark_all_read_button | button | "Mark All Read" text variant, #008B8B teal, label_medium |

### Section Headers

| ID | Type | Description |
|---|---|---|
| section_today_label | text | "Today" label_medium, #888888, semi-bold, padding horizontal 20 |
| section_earlier_label | text | "Earlier" label_medium, #888888, semi-bold, padding horizontal 20, padding top 12 |

### Notification Card — Payment from James Wilson (Unread, payment)

| ID | Type | Description |
|---|---|---|
| notification_payment_james | box | Unread card — #F0EDFF bg, #D4C8FF border 1dp, radius 16, padding 16, margin horizontal 20, bottom 8. Taps → transaction-detail |
| payment_james_icon_bg | box | 44x44 circle, #4CAF50 green background |
| payment_james_icon | icon | arrow_downward, 22dp, #FFFFFF |
| payment_james_title | text | "Payment received" body_medium, #111111, semi-bold |
| payment_james_message | text | "Payment of £50.00 received from James Wilson" body_small, #444444 |
| payment_james_time | text | "10 min ago" label_small, #888888 |
| unread_dot_payment_james | box | 10x10 circle, #1800B1 — unread indicator, role: status |

### Notification Card — KYC Verification Approved (Unread, security)

| ID | Type | Description |
|---|---|---|
| notification_kyc_approved | box | Unread card — same style as above. Taps → kyc-review (cross-persona deep link) |
| kyc_approved_icon_bg | box | 44x44 circle, #1800B1 primary blue background |
| kyc_approved_icon | icon | verified_user, 22dp, #FFFFFF |
| kyc_approved_title | text | "KYC verification approved" body_medium, #111111, semi-bold |
| kyc_approved_message | text | "Your identity has been verified. You now have full access to all account features." body_small, #444444 |
| kyc_approved_time | text | "1 hr ago" label_small, #888888 |
| unread_dot_kyc | box | 10x10 circle, #1800B1 — unread indicator, role: status |

### Notification Card — Netflix Direct Debit Mandate (Read, system)

| ID | Type | Description |
|---|---|---|
| notification_netflix_mandate | box | Read card — #FFFFFF bg, #F0F0F0 border 1dp, radius 16, padding 16, margin horizontal 20, bottom 8. Taps → accounts |
| netflix_mandate_icon_bg | box | 44x44 circle, #008B8B teal background |
| netflix_mandate_icon | icon | autorenew, 22dp, #FFFFFF |
| netflix_mandate_title | text | "Direct debit mandate created" body_medium, #555555, semi-bold |
| netflix_mandate_message | text | "Direct debit mandate created for Netflix — £15.99/month from your Current Account." body_small, #777777 |
| netflix_mandate_time | text | "3 hr ago" label_small, #AAAAAA |

### Notification Card — Acme Ltd Salary Credited (Read, payment)

| ID | Type | Description |
|---|---|---|
| notification_salary_credited | box | Read card — same style as Netflix card. Taps → transaction-detail |
| salary_credited_icon_bg | box | 44x44 circle, #4CAF50 green background |
| salary_credited_icon | icon | arrow_downward, 22dp, #FFFFFF |
| salary_credited_title | text | "Salary credited" body_medium, #555555, semi-bold |
| salary_credited_message | text | "£3,200.00 from Acme Ltd has been credited to your Current Account." body_small, #777777 |
| salary_credited_time | text | "Yesterday" label_small, #AAAAAA |

---

## States

| ID | Trigger | Visible Components | Notes |
|---|---|---|---|
| loading | Screen mounts; Room DB query in flight | title_action_row, notifications_title | 4 skeleton cards shown (shimmer) |
| populated | Notifications loaded from Room DB | All components across both sections | Today = unread; Earlier = read |
| empty | No notifications in DB | title_action_row, notifications_title | Empty state: notifications_none_outlined icon, "You're all caught up", "No new notifications. We'll let you know about payments, alerts and updates." |
| error | Room DB error or FCM registration failure | title_action_row, notifications_title | Error state: cloud_off icon, "Unable to load notifications", "Check your connection and try again", retry button |

---

## State Model

**ViewModel:** `NotificationsViewModel`

### State Fields

| Name | Type | Default |
|---|---|---|
| notifications | List\<NotificationItem\> | emptyList() |
| unreadCount | Int | 0 |
| uiState | NotificationsUiState | Loading |
| error | UiError? | null |

### Error Codes

| Field | Code | Message |
|---|---|---|
| global | LOAD_FAILED | Unable to load notifications. Please try again. |

### Events

`NotificationsLoaded`, `NotificationOpened(notificationId: String, category: NotificationCategory)`, `MarkAllReadClicked`, `MarkAllReadComplete`, `RetryLoad`, `NotificationSettingsOpened`

### Actions

`open_notification`, `mark_all_read`, `open_notification_settings`

### DI Dependencies

`NotificationRepository`, `SignalRepository`

---

## Navigation

| From | Action | Target | Category | Type |
|---|---|---|---|---|
| notification_payment_james | open_notification | transaction-detail | payment | push |
| notification_kyc_approved | open_notification | kyc-review | security | push (cross-persona deep link) |
| notification_netflix_mandate | open_notification | accounts | system | push |
| notification_salary_credited | open_notification | transaction-detail | payment | push |
| top app bar tune | open_notification_settings | settings | — | push |
| top app bar back arrow | navigate_back | home | — | pop |

---

## Category — Icon Colour Semantics

| Category | Icon | Colour | Meaning |
|---|---|---|---|
| payment (incoming) | arrow_downward | #4CAF50 green | Money received — positive financial event |
| security | verified_user | #1800B1 primary | Identity / trust signal |
| system | autorenew | #008B8B teal | Recurring mandate, scheduled action |

---

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| primary | #1800B1 | Notifications title, KYC icon, unread dot |
| on_primary | #FFFFFF | Icon colour on coloured circles |
| unread_bg | #F0EDFF | Unread card background (soft purple) |
| unread_border | #D4C8FF | Unread card border |
| surface | #FFFFFF | Read card background |
| surface_border | #F0F0F0 | Read card border |
| success | #4CAF50 | Payment received / salary icon circle |
| teal | #008B8B | Direct debit / mandate icon circle; Mark All Read text |
| on_surface_variant | #888888 | Section labels, unread timestamp |
| on_surface_muted | #AAAAAA | Read notification timestamp |
| section_label_top | 12dp | Padding top before Earlier section label |

---

## API Endpoints

| Endpoint | Auth | Purpose |
|---|---|---|
| GET /obp/v6.0.0/signal/channels | DirectLogin | List available FCM push notification channels |
| GET notifications (Room DB) | local | Load persisted notification items offline-first |
| POST /notifications/{id}/mark-read | DirectLogin | Sync read state to backend after local update |

---

*Generated by /idea export | 2026-05-25*
