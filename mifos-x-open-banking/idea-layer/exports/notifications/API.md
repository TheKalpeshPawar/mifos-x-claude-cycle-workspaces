# API Reference — Notifications

| Field | Value |
|---|---|
| Feature | notifications |
| Base URL | https://apisandbox.openbankproject.com |
| Auth Scheme | DirectLogin (header: `DirectLogin token=<token>`) |
| Local Storage | Room DB (offline-first) |
| Push Transport | Firebase Cloud Messaging (FCM) |

---

## Overview

The Notifications screen uses a **three-layer data strategy**:

1. **FCM push delivery** — remote notifications arrive at the device via Firebase Cloud Messaging. The FCM registration token is obtained on app start and registered with the OBP Signal API.
2. **Room DB persistence** — every received notification is written to a local `notifications` table immediately on receipt. The UI reads exclusively from Room (offline-first); the backend is never queried directly for the notification list.
3. **Mark-as-read sync** — read state is updated locally first (optimistic), then synced to the backend via a POST endpoint.

---

## Firebase Cloud Messaging — Push Registration

**Mechanism:** Firebase SDK (`firebase-messaging` KMP/Android)

| Step | Detail |
|---|---|
| Token acquisition | `FirebaseMessaging.getInstance().token` on app launch |
| Token registration | POST to OBP Signal subscription endpoint (see below) |
| Message receipt | `FirebaseMessagingService.onMessageReceived` → parse payload → write to Room |
| Foreground display | NotificationCompat.Builder with channel ID per category |

### FCM Notification Payload Shape

```json
{
  "notification_id": "ntf_james_wilson_20260525_001",
  "category": "payment",
  "title": "Payment received",
  "body": "Payment of £50.00 received from James Wilson",
  "deep_link_target": "transaction-detail",
  "deep_link_params": {
    "transaction_id": "txn_jw_20260525_001"
  },
  "timestamp": "2026-05-25T09:50:00Z"
}
```

**Notification categories and their FCM channel IDs:**

| Category | Channel ID | Channel Name | Importance |
|---|---|---|---|
| payment | `ch_payment` | Payment Alerts | HIGH |
| security | `ch_security` | Security & Identity | MAX |
| system | `ch_system` | Account Updates | DEFAULT |

---

## OBP Signal API — Channel Registration

### GET /obp/v6.0.0/signal/channels

**Purpose:** List all real-time push notification channels available to the authenticated user. Called on app launch to verify FCM channel subscriptions are current.

**Auth:** `DirectLogin token=<token>`

#### Response

```json
{
  "channels": [
    {
      "channel_id": "ch_payment",
      "name": "payment_received",
      "description": "Incoming payment and credit notifications",
      "created_at": "2026-01-15T10:00:00Z"
    },
    {
      "channel_id": "ch_security",
      "name": "kyc_status",
      "description": "Identity verification and security alerts",
      "created_at": "2026-01-15T10:00:00Z"
    },
    {
      "channel_id": "ch_system",
      "name": "mandate_events",
      "description": "Direct debit mandate creation and cancellation events",
      "created_at": "2026-01-15T10:00:00Z"
    }
  ]
}
```

#### Response Fields

| Field | Type | Description |
|---|---|---|
| channels | List\<SignalChannel\> | Array of available notification channel objects |
| channel_id | String | Unique channel identifier used as FCM Android channel ID |
| name | String | Machine-readable event type name |
| description | String | Human-readable description of delivered events |
| created_at | String | ISO 8601 timestamp of channel creation |

#### Error Codes

| Code | Key | Meaning |
|---|---|---|
| 401 | USER_NOT_LOGGED_IN | DirectLogin token missing or expired |
| 403 | INSUFFICIENT_AUTHORISATION | Token lacks Signal scope |

---

## Room DB — Local Notification Store

**Purpose:** Offline-first read of notification items. The UI never waits for a network call to render the notification list.

### Table: `notifications`

| Column | Type | Description |
|---|---|---|
| id | TEXT PRIMARY KEY | FCM message ID / `notification_id` from payload |
| category | TEXT | payment, security, system |
| title | TEXT | Notification title (e.g. "Payment received") |
| body | TEXT | Full notification body text |
| deep_link_target | TEXT | Screen slug for tap navigation (e.g. "transaction-detail") |
| deep_link_params | TEXT | JSON-encoded params for the target screen |
| timestamp | INTEGER | Unix epoch ms of event |
| is_read | INTEGER | 0 = unread, 1 = read |
| created_at | INTEGER | Row insert time (Unix epoch ms) |

### DAO Operations

```kotlin
@Query("SELECT * FROM notifications ORDER BY timestamp DESC")
fun getAllNotifications(): Flow<List<NotificationEntity>>

@Query("SELECT COUNT(*) FROM notifications WHERE is_read = 0")
fun getUnreadCount(): Flow<Int>

@Query("UPDATE notifications SET is_read = 1 WHERE id = :id")
suspend fun markAsRead(id: String)

@Query("UPDATE notifications SET is_read = 1")
suspend fun markAllAsRead()
```

---

## Mark-as-Read — Backend Sync

### POST /obp/v6.0.0/notifications/{notification_id}/mark-read

**Purpose:** Sync read state to the backend after optimistic local update in Room. Called per-notification when user taps, or in batch when "Mark All Read" is triggered.

**Auth:** `DirectLogin token=<token>`

**Path Parameters:**

| Parameter | Type | Description |
|---|---|---|
| notification_id | String | The `notification_id` from the FCM payload |

**Request Body:** (empty — the action is idempotent)

**Response:**

```json
{
  "notification_id": "ntf_james_wilson_20260525_001",
  "is_read": true,
  "updated_at": "2026-05-25T10:05:00Z"
}
```

**Error Codes:**

| Code | Key | Meaning |
|---|---|---|
| 401 | USER_NOT_LOGGED_IN | DirectLogin token missing or expired |
| 404 | NOTIFICATION_NOT_FOUND | notification_id not recognised |

**Offline handling:** If the POST fails (no connectivity), the local Room update is preserved. A background sync job retries mark-read calls when connectivity is restored (WorkManager `MarkReadSyncWorker`).

---

## Data Flow Summary

```
FCM push arrives
      │
      ▼
FirebaseMessagingService.onMessageReceived()
      │
      ├─► Parse payload → NotificationEntity
      ├─► Insert into Room DB (is_read = 0)
      └─► Show system notification (NotificationCompat)

User opens Notifications screen
      │
      ▼
NotificationsViewModel collects Room Flow<List<NotificationEntity>>
      │
      └─► UI renders (loading → populated / empty / error)

User taps a notification card
      │
      ├─► Room: UPDATE is_read = 1 (optimistic)
      ├─► Navigate to deep_link_target
      └─► Background: POST /notifications/{id}/mark-read

User taps "Mark All Read"
      │
      ├─► Room: UPDATE all is_read = 1
      └─► Background: POST mark-read for each unread id (batch)
```

---

## Repository Interface

```kotlin
interface NotificationRepository {
    fun getNotifications(): Flow<List<NotificationItem>>
    fun getUnreadCount(): Flow<Int>
    suspend fun markAsRead(notificationId: String)
    suspend fun markAllAsRead()
}
```

---

_Generated by /idea export | 2026-05-29_
