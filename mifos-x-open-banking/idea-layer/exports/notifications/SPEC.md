# SPEC — Notifications

| Field         | Value                      |
|---------------|----------------------------|
| Feature       | notifications              |
| Flavor        | consumer                   |
| Status        | approved                   |
| Quality Score | 95                         |
| ViewModel     | NotificationsViewModel     |

---

## Overview

The Notifications screen is an `index_list` archetype screen displaying real-time push notification events for the Consumer persona. It is reachable via the top app bar back-nav from any primary screen. The top app bar shows "Notifications" as title with a back arrow, a "Mark all as read" icon (done_all), and a "Notification settings" icon (tune). There is no bottom navigation bar on this screen.

Notifications are grouped into two time-based sections: **Today** and **Earlier**. Each notification card carries a 44×44dp coloured icon circle, a title, a body message, a relative timestamp, and — if unread — a 10dp green dot indicator. Unread cards use `#CDEDA3` (primary_container) fill; read cards use `#FFFFFF` (surface) fill with an `#F9FAEF` border.

Three FCM-sourced notification categories are represented:
- **payment** — "Payment received" from James Wilson (£50.00, `arrow_downward` icon, unread, Today) and "Salary credited" from Acme Ltd (£3,200.00, `arrow_downward` icon, read, Earlier)
- **security** — "KYC verification approved" (identity verified, full account access, `verified_user` icon, unread, Today)
- **system** — "Direct debit mandate created" for Netflix (£15.99/month, `autorenew` icon, read, Earlier)

Tapping a notification navigates to the category-specific target screen: payment → transaction-detail, security → kyc-review (cross-persona deep link), system → accounts. A top-bar "Mark All Read" text button and a top-bar action (done_all) both trigger `mark_all_read`. Signal channel configuration is fetched from OBP `GET /obp/v6.0.0/signal/channels`; the notification list itself is managed via `NotificationRepository`.

---

## Screens

| ID            | Name          | Route          | Layout | Scroll   |
|---------------|---------------|----------------|--------|----------|
| notifications | Notifications | /notifications | Column | Vertical |

**Shell:** Top app bar only — no bottom navigation.

| App Bar Element   | Icon/Action              | Behaviour                              |
|-------------------|--------------------------|----------------------------------------|
| Navigation icon   | arrow_back               | `navigate_back` → home                 |
| Title             | "Notifications" (static) | Screen heading                         |
| Action 1          | done_all                 | `mark_all_read` all notification items |
| Action 2          | tune                     | `open_notification_settings`           |

---

## Components

| ID                           | Type   | Description                                                                                                       |
|------------------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| title_action_row             | stack  | Horizontal, space-between, 20dp h-pad, 16dp top / 8dp bottom — contains notifications_title + mark_all_read_button|
| notifications_title          | text   | "Notifications" — Outfit/headline_large, #4C662B, bold; heading role                                             |
| mark_all_read_button         | button | "Mark All Read" — text variant, #386663, Outfit/label_medium; triggers `mark_all_read`                           |
| section_today_label          | text   | "Today" — Outfit/label_medium, #44483D, semibold; heading role; 16dp h-pad, 8dp top, 4dp bottom                  |
| notification_payment_james   | box    | Unread payment card: #CDEDA3 fill, 16dp radius, 16×14dp padding, 20dp h-margin, 8dp bottom margin; taps → transaction-detail |
| payment_james_row            | stack  | Horizontal, 12dp spacing, flex_start — icon container + text column + unread dot                                  |
| payment_james_icon_bg        | box    | 44×44dp circle, #4C662B fill, 22dp radius — wraps arrow_downward icon                                            |
| payment_james_icon           | icon   | arrow_downward, 22dp, #FFFFFF — "Incoming payment"                                                                |
| payment_james_text_col       | stack  | Vertical, flex:1 — contains title + message + timestamp                                                           |
| payment_james_title          | text   | "Payment received" — Outfit/body_medium, #1A1C16, semibold                                                       |
| payment_james_message        | text   | "Payment of £50.00 received from James Wilson" — Outfit/body_small, #44483D; xs top+bottom padding               |
| payment_james_time           | text   | "10 min ago" — Outfit/label_small, #44483D                                                                        |
| unread_dot_payment_james     | box    | 10×10dp circle, #4C662B fill, 5dp radius; align_self: flex_start, 4dp top margin; status role                    |
| notification_kyc_approved    | box    | Unread security card: #CDEDA3 fill, 16dp radius — taps → kyc-review (cross-persona deep link)                    |
| kyc_approved_row             | stack  | Horizontal, 12dp spacing, flex_start                                                                              |
| kyc_approved_icon_bg         | box    | 44×44dp circle, #4C662B fill — wraps verified_user icon                                                           |
| kyc_approved_icon            | icon   | verified_user, 22dp, #FFFFFF                                                                                      |
| kyc_approved_text_col        | stack  | Vertical, flex:1                                                                                                  |
| kyc_approved_title           | text   | "KYC verification approved" — Outfit/body_medium, #1A1C16, semibold                                              |
| kyc_approved_message         | text   | "Your identity has been verified. You now have full access to all account features." — Outfit/body_small, #44483D |
| kyc_approved_time            | text   | "1 hr ago" — Outfit/label_small, #44483D                                                                          |
| unread_dot_kyc               | box    | 10×10dp circle, #4C662B fill, 5dp radius; flex_start, 4dp top margin; status role                                |
| section_earlier_label        | text   | "Earlier" — Outfit/label_medium, #44483D, semibold; heading role; 16dp h-pad, 8dp top, 4dp bottom                |
| notification_netflix_mandate | box    | Read system card: #FFFFFF fill, 16dp radius, #F9FAEF border (1dp) — taps → accounts                              |
| netflix_mandate_row          | stack  | Horizontal, 12dp spacing, flex_start                                                                              |
| netflix_mandate_icon_bg      | box    | 44×44dp circle, #386663 fill — wraps autorenew icon (secondary colour, system category)                           |
| netflix_mandate_icon         | icon   | autorenew, 22dp, #FFFFFF                                                                                          |
| netflix_mandate_text_col     | stack  | Vertical, flex:1                                                                                                  |
| netflix_mandate_title        | text   | "Direct debit mandate created" — Outfit/body_medium, #44483D, semibold                                           |
| netflix_mandate_message      | text   | "Direct debit mandate created for Netflix — £15.99/month from your Current Account." — Outfit/body_small, #44483D |
| netflix_mandate_time         | text   | "3 hr ago" — Outfit/label_small, #44483D                                                                          |
| notification_salary_credited | box    | Read payment card: #FFFFFF fill, 16dp radius, #F9FAEF border (1dp) — taps → transaction-detail                   |
| salary_credited_row          | stack  | Horizontal, 12dp spacing, flex_start                                                                              |
| salary_credited_icon_bg      | box    | 44×44dp circle, #4C662B fill — wraps arrow_downward icon                                                          |
| salary_credited_icon         | icon   | arrow_downward, 22dp, #FFFFFF                                                                                     |
| salary_credited_text_col     | stack  | Vertical, flex:1                                                                                                  |
| salary_credited_title        | text   | "Salary credited" — Outfit/body_medium, #44483D, semibold                                                         |
| salary_credited_message      | text   | "£3,200.00 from Acme Ltd has been credited to your Current Account." — Outfit/body_small, #44483D                 |
| salary_credited_time         | text   | "Yesterday" — Outfit/label_small, #44483D                                                                         |
| bottom_spacer                | spacer | 24dp height — prevents content clipping at scroll end                                                             |

---

## States

| ID        | Trigger                          | Description                                                                                                          |
|-----------|----------------------------------|----------------------------------------------------------------------------------------------------------------------|
| loading   | Screen entry / RetryLoad         | title_action_row + notifications_title visible; 4 skeleton notification cards; shimmer short4 (200ms); reduced_motion_fallback: static_placeholder |
| populated | Data load success                | Full list: section_today_label + 2 unread cards (payment_james, kyc_approved) + section_earlier_label + 2 read cards (netflix_mandate, salary_credited) + mark_all_read_button enabled |
| empty     | No notifications in repository   | title_action_row + notifications_title + empty state: icon `notifications_none_outlined`, title "You're all caught up", message "No new notifications. We'll let you know about payments, alerts and updates." |
| error     | Network / repository failure     | title_action_row + notifications_title + error state: icon `cloud_off`, title "Unable to load notifications", message "Check your connection and try again" + Retry button                                        |

---

## State Model

**ViewModel:** `NotificationsViewModel`
**Screen State Type:** `NotificationsUiState`

| Name          | Type                     | Default      |
|---------------|--------------------------|--------------|
| notifications | List\<NotificationItem\> | emptyList()  |
| unreadCount   | Int                      | 0            |
| uiState       | NotificationsUiState     | Loading      |
| error         | UiError?                 | null         |

**Events:** `NotificationsLoaded`, `NotificationOpened(notificationId: String, category: NotificationCategory)`, `MarkAllReadClicked`, `MarkAllReadComplete`, `RetryLoad`, `NotificationSettingsOpened`

**Actions:** `open_notification`, `mark_all_read`, `open_notification_settings`

**DI Dependencies:** `NotificationRepository`, `SignalRepository`

**Errors:**
- `LOAD_FAILED` (global): "Unable to load notifications. Please try again."

---

## Navigation

| From          | To                 | Trigger                                                      | Category | Type |
|---------------|--------------------|--------------------------------------------------------------|----------|------|
| notifications | transaction-detail | `open_notification` tap on payment-category card             | payment  | push |
| notifications | kyc-review         | `open_notification` tap on security/identity card            | security | push |
| notifications | accounts           | `open_notification` tap on system/mandate card               | system   | push |
| notifications | settings           | `open_notification_settings` top-bar icon or action          | —        | push |
| notifications | home               | `navigate_back` top-bar arrow_back icon                      | —        | pop  |

---

## API Endpoints

| Endpoint                            | Auth        | Tag    | Purpose                                                  |
|-------------------------------------|-------------|--------|----------------------------------------------------------|
| GET /obp/v6.0.0/signal/channels     | DirectLogin | Signal | List FCM push notification channels for subscription setup |

---

## Design Tokens

| Token                            | Value         | Usage                                                                                      |
|----------------------------------|---------------|--------------------------------------------------------------------------------------------|
| colors.light.primary             | #4C662B       | Screen title text, unread icon-circle fill (payment + KYC + salary), unread dot fill      |
| colors.light.primary_container   | #CDEDA3       | Unread notification card fill (payment_james, kyc_approved)                                |
| colors.light.secondary           | #386663       | "Mark All Read" button text; netflix_mandate_icon_bg fill (system category distinction)    |
| colors.light.surface             | #FFFFFF       | Read card fill (netflix_mandate, salary_credited)                                          |
| colors.light.background          | #F9FAEF       | Screen base + read card border colour                                                      |
| colors.light.on_surface          | #1A1C16       | Unread card title text (payment_james_title, kyc_approved_title)                           |
| colors.light.on_surface_variant  | #44483D       | Section labels, notification body messages, timestamps; read card title text               |
| colors.light.on_primary          | #FFFFFF       | Icon fill on all coloured icon containers                                                  |
| typography.scale.headline_lg     | Outfit 32sp/400 | Screen title "Notifications" (bold weight override per ui.yaml)                          |
| typography.scale.label_md        | Outfit 12sp/500 | "Mark All Read" button + section labels "Today" / "Earlier"                              |
| typography.scale.body_md         | Outfit 14sp/400 | Notification item title (semibold weight override)                                       |
| typography.scale.body_sm         | Outfit 12sp/400 | Notification body messages                                                               |
| typography.scale.label_sm        | Outfit 11sp/500 | Relative timestamps ("10 min ago", "1 hr ago", "3 hr ago", "Yesterday")                 |
| radius.lg                        | 16dp          | Notification card corner radius                                                             |
| spacing.md                       | 16dp          | Horizontal content padding, section label h-pad                                             |
| spacing.sm                       | 8dp           | Section label top padding, icon container spacing                                           |
| spacing.xs                       | 4dp           | Message vertical padding, unread dot top margin                                             |
| spacing.lg                       | 24dp          | Bottom spacer height                                                                        |
| motion.duration.short4           | 200ms         | Loading skeleton shimmer animation duration                                                 |

---

_Generated by /idea export | 2026-05-30_
