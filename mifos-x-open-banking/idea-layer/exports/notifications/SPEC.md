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

The Notifications screen is a push notification inbox for the Consumer persona, presenting a chronological categorised feed of account events. Notifications are grouped into two time-bucketed sections — **Today** (unread, `#CDEDA3` bg cards) and **Earlier** (read, `#FFFFFF` bg cards) — so users instantly see what requires attention. Four real notification items span three semantic categories: payment (unread: payment received from James Wilson £50; read: salary £3,200 from Acme Ltd), security (unread: KYC verified), and system (read: Netflix direct debit mandate £15.99/month). Push delivery is via Firebase Cloud Messaging (FCM) + OBP Signal API. The screen includes a "Mark All Read" inline text button and top app bar actions (done_all and tune). The top app bar navigation icon is a back arrow.

---

## Screens

| ID            | Name          | Route          | Layout     | Scroll   |
|---------------|---------------|----------------|------------|----------|
| notifications | Notifications | /notifications | index_list | Vertical |

**Shell:** Top app bar ("Notifications", back arrow, done_all action, tune action). No bottom navigation bar.

---

## Components

| ID                          | Type   | Description                                                                                                                           |
|-----------------------------|--------|---------------------------------------------------------------------------------------------------------------------------------------|
| notifications_title         | text   | "Notifications" — headline_large, `#4C662B`, bold                                                                                    |
| mark_all_read_button        | button | "Mark All Read" — text variant, `#386663` text, label_medium, 0dp horizontal padding                                                 |
| section_today_label         | text   | "Today" — label_medium, `#44483D`, semibold, 16dp horizontal padding                                                                 |
| notification_payment_james  | box    | **Unread payment.** `#CDEDA3` bg, 1dp `#CDEDA3` border, 16dp radius, 16dp padding, 20dp horizontal margin, 8dp bottom. Taps → transaction-detail. Green 44×44 avatar circle (`#4C662B`) + arrow_downward icon (22dp, white). "Payment received" (body_medium, `#1A1C16`, semibold) + "Payment of £50.00 received from James Wilson" (body_small, `#44483D`) + "10 min ago" (label_small, `#44483D`). Unread dot: 10×10 circle, `#4C662B` |
| notification_kyc_approved   | box    | **Unread security.** Same unread styling as above. Taps → kyc-review (cross-persona deep link). Green 44×44 circle (`#4C662B`) + verified_user icon. "KYC verification approved" (body_medium semibold) + "Your identity has been verified. You now have full access to all account features." (body_small, `#44483D`) + "1 hr ago". Unread dot: `#4C662B` |
| section_earlier_label       | text   | "Earlier" — label_medium, `#44483D`, semibold, 16dp horizontal padding                                                               |
| notification_netflix_mandate| box    | **Read system.** `#FFFFFF` bg, 1dp `#F9FAEF` border, same radius/padding/margin. Taps → accounts. Teal 44×44 circle (`#386663`) + autorenew icon. "Direct debit mandate created" (body_medium, `#44483D`, semibold) + "Direct debit mandate created for Netflix — £15.99/month from your Current Account." (body_small, `#44483D`) + "3 hr ago". No unread dot |
| notification_salary_credited| box    | **Read payment.** `#FFFFFF` bg styling. Taps → transaction-detail. Green 44×44 circle (`#4C662B`) + arrow_downward icon. "Salary credited" (body_medium, `#44483D`, semibold) + "£3,200.00 from Acme Ltd has been credited to your Current Account." (body_small, `#44483D`) + "Yesterday". No unread dot |

---

## States

| ID        | Trigger                               | Description                                                                              |
|-----------|---------------------------------------|------------------------------------------------------------------------------------------|
| loading   | Screen mounts; DB query in flight     | Title row visible; 4 shimmer skeleton cards (skeleton_count: 4)                         |
| populated | Notifications loaded                  | Title + mark_all_read + Today section (2 unread) + Earlier section (2 read) + spacer    |
| empty     | No notifications in DB                | Title visible; notifications_none_outlined 48dp icon + "You're all caught up" + "No new notifications…" |
| error     | DB or FCM failure                     | Title visible; cloud_off icon + "Unable to load notifications" + "Check your connection" + retry button |

---

## State Model

**ViewModel:** `NotificationsViewModel`
**Screen State Type:** `NotificationsUiState`

| Name          | Type                      | Default      |
|---------------|---------------------------|--------------|
| notifications | List\<NotificationItem\>  | emptyList()  |
| unreadCount   | Int                       | 0            |
| uiState       | NotificationsUiState      | Loading      |
| error         | UiError?                  | null         |

**Events:** `NotificationsLoaded`, `NotificationOpened(notificationId: String, category: NotificationCategory)`, `MarkAllReadClicked`, `MarkAllReadComplete`, `RetryLoad`, `NotificationSettingsOpened`

**Actions:** `open_notification(notificationId: String)`, `mark_all_read()`, `open_notification_settings()`

**DI Dependencies:** `NotificationRepository`, `SignalRepository`

**Errors:**
- `LOAD_FAILED`: "Unable to load notifications. Please try again."

---

## Navigation

| From                        | Action                     | Target           | Category | Type            |
|-----------------------------|----------------------------|------------------|----------|-----------------|
| notification_payment_james  | open_notification          | transaction-detail | payment | push            |
| notification_kyc_approved   | open_notification          | kyc-review       | security | push (cross-persona deep link) |
| notification_netflix_mandate| open_notification          | accounts         | system   | push            |
| notification_salary_credited| open_notification          | transaction-detail | payment | push            |
| top app bar tune            | open_notification_settings | settings         | —        | push            |
| top app bar back arrow      | navigate_back              | home             | —        | pop             |

---

## API Endpoints

| Endpoint                                | Auth        | Tag    | Purpose                                           |
|-----------------------------------------|-------------|--------|---------------------------------------------------|
| GET /obp/v6.0.0/signal/channels         | DirectLogin | Signal | List available FCM push notification channels     |

Local Room DB provides the notification feed offline-first; `NotificationRepository` persists FCM push payloads to Room and exposes a Flow for the ViewModel. No remote list-notifications REST endpoint; signal/channels provides the channel registry only.

---

## Design Tokens

| Token                         | Value     | Usage                                                                         |
|-------------------------------|-----------|-------------------------------------------------------------------------------|
| color.light.primary           | #4C662B   | Screen title, unread notification icon circles, unread dot indicator         |
| color.light.primary_container | #CDEDA3   | Unread notification card background and border                               |
| color.light.secondary         | #386663   | "Mark All Read" text button, Netflix/system icon circle                       |
| color.light.surface           | #FFFFFF   | Read notification card background                                             |
| color.light.background        | #F9FAEF   | Screen background, read card border (near-invisible flush)                   |
| color.light.on_surface        | #1A1C16   | Unread notification title text (semibold)                                    |
| color.light.on_surface_variant| #44483D   | Section labels, notification message text, timestamps                        |
| typography.headline_large     | —         | "Notifications" screen title                                                 |
| typography.body_medium        | —         | Notification title line (semibold)                                           |
| typography.body_small         | —         | Notification message body text                                               |
| typography.label_medium       | —         | Section labels ("Today", "Earlier"), Mark All Read button                    |
| typography.label_small        | —         | Notification timestamps                                                      |
| spacing.md                    | 16dp      | Notification card internal padding, section label horizontal padding         |
| radius.xl                     | 24dp      | Notification card corner radius (16dp per source — closest token)            |

---

_Generated by /idea export | 2026-05-29_
