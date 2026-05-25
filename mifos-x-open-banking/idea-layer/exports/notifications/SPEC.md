# Feature Specification — Notifications

| Field | Value |
|---|---|
| Feature | notifications |
| Name | Notifications |
| Flavor | consumer |
| Status | enriched |
| Quality Score | 78 |

---

## Overview

The Notifications screen presents a chronological feed of account alerts and app notifications for the Mifos X consumer. Three notification types are shown in the enriched state: a salary credit from Acme Ltd (£3,200.00, unread — highlighted purple background with unread dot), a Council Tax direct debit reminder (£148.00 due 1 June 2026, read), and a Dining Out budget alert (97% used, £5.00 remaining, read). Each notification card has a color-coded icon circle and navigates to the relevant screen on tap (transactions, direct-debits, pfm-dashboard respectively). Notification delivery is powered by OBP Signal channels. A "Mark All Read" action is available in both the top app bar and inline.

---

## Screens

| Screen ID | Name | Route | Archetype | Scroll |
|---|---|---|---|---|
| notifications | Notifications | /notifications | index_list | vertical |

---

## Components

| ID | Type | Description |
|---|---|---|
| notifications_title | text | "Notifications" headline_large, #1800B1, bold |
| mark_all_read_button | button | "Mark All Read" text button, #008B8B teal |
| notification_payment_received | box | Unread card (#F0EDFF bg, #D4C8FF border, radius 16) — salary credit notification |
| payment_received_icon_bg | box | 44x44 circle, #4CAF50 green background, arrow_downward icon |
| payment_received_title | text | "Payment received" body_medium, #111111, semi-bold |
| payment_received_message | text | "Your salary of £3,200.00 from Acme Ltd has been credited to your account." body_small, #444444 |
| payment_received_time | text | "2 min ago" label_small, #888888 |
| unread_dot_payment | box | 10x10 circle, #1800B1 — unread indicator |
| notification_direct_debit | box | Read card (#FFFFFF bg, radius 16) — Council Tax DD reminder |
| direct_debit_icon_bg | box | 44x44 circle, #008B8B teal, schedule icon |
| direct_debit_notif_title | text | "Direct debit reminder" body_medium, #555555, semi-bold |
| direct_debit_notif_message | text | "Your Council Tax direct debit of £148.00 will be collected on 1 June 2026." body_small, #777777 |
| direct_debit_notif_time | text | "3 hr ago" label_small, #AAAAAA |
| notification_budget_alert | box | Read card (#FFFFFF bg, radius 16) — Dining Out budget alert |
| budget_alert_icon_bg | box | 44x44 circle, #FF9800 orange, warning_amber_outlined icon |
| budget_alert_title | text | "Budget alert" body_medium, #555555, semi-bold |
| budget_alert_message | text | "Your Dining Out budget is 97% used. Only £5.00 remaining this month." body_small, #777777 |
| budget_alert_time | text | "Yesterday" label_small, #AAAAAA |

---

## States

| ID | Trigger | Description |
|---|---|---|
| loading | Screen enters; API call in flight | Header row visible; 4 skeleton cards shown |
| content | Notifications loaded | All 3 notification cards rendered with correct read/unread states |
| empty | No notifications exist | Header; empty state "You're all caught up" with notifications_none_outlined icon |
| error | Network or API failure | Header; error state with cloud_off icon and retry button |

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
`NotificationsLoaded`, `NotificationOpened(notificationId: String)`, `MarkAllReadClicked`, `MarkAllReadComplete`, `RetryLoad`

### Actions
`open_notification`, `mark_all_read`, `open_notification_settings`

### DI Dependencies
`NotificationRepository`, `SignalRepository`

---

## Navigation

| From | To | Trigger | Type |
|---|---|---|---|
| notification_payment_received | transactions | Notification tap | push |
| notification_direct_debit | direct-debits | Notification tap | push |
| notification_budget_alert | pfm-dashboard | Notification tap | push |
| top app bar tune icon | settings | open_notification_settings | push |
| top app bar back arrow | home | navigate_back | pop |

---

## API Endpoints

| Endpoint | Auth | Purpose |
|---|---|---|
| GET /obp/v6.0.0/signal/channels | DirectLogin | List real-time push notification channels (Signal API) |

---

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| primary | #1800B1 | Title, unread dot indicator |
| on_primary | #FFFFFF | Icon colours on coloured circle backgrounds |
| unread_bg | #F0EDFF | Unread notification card background (soft purple) |
| unread_border | #D4C8FF | Unread notification card border |
| surface | #FFFFFF | Read notification card background |
| success | #4CAF50 | Payment received icon circle |
| teal | #008B8B | Direct debit icon circle, Mark All Read text |
| warning | #FF9800 | Budget alert icon circle |
| on_surface_variant | #888888 | Unread notification timestamp |
| on_surface_muted | #AAAAAA | Read notification timestamp |

---

*Generated by /idea export | 2026-05-25*
