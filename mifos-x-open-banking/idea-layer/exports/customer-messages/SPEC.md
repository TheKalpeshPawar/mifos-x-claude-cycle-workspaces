# SPEC — Customer Messages

| Field         | Value                          |
|---------------|--------------------------------|
| Feature       | customer-messages              |
| Flavor        | fieldOfficer                   |
| Status        | approved                       |
| Quality Score | 97                             |
| ViewModel     | CustomerMessagesViewModel      |

---

## Overview

Customer Messages is the thread-based messaging center for Field Officer users. It displays all customer communication threads in a scrollable index list, with unread count badge, full-text search, and compose sheet for initiating new messages. The screen provides quick visual differentiation between unread threads (highlighted with `#CDEDA3` background and green unread dot) and read threads (white card). Field officers can search across threads, open individual conversations, and compose new messages directly from this screen. The FAB triggers a compose dialog with customer autocomplete, subject, and message body fields. Data is fetched via the OBP Customer-Messages API on screen entry.

---

## Screens

| ID                      | Name             | Route              | Layout | Scroll   |
|-------------------------|------------------|--------------------|--------|----------|
| customer-messages-main  | Messaging Center | /customer-messages | Column | Vertical |

**Shell:** Field Officer bottom navigation bar (5 items — Messages tab active)

| Nav Item     | ID               | Icon         | Target               | Badge |
|--------------|------------------|--------------|----------------------|-------|
| Dashboard    | nav_dashboard    | dashboard    | fo-dashboard         | true  |
| Customers    | nav_customers    | people       | customer-search      | false |
| Applications | nav_applications | description  | account-applications | true  |
| Messages     | nav_messages     | mail         | customer-messages    | true  |
| More         | nav_more         | more_vert    | settings             | false |

---

## Components

| ID                      | Type   | Description                                                                                               |
|-------------------------|--------|-----------------------------------------------------------------------------------------------------------|
| messages_title_row      | box    | Horizontal header row: "Messages" title + unread badge; pad H16/T20/B8; space-between                    |
| messages_title          | text   | "Messages" — Outfit/headline_large, #4C662B, weight 700                                                   |
| unread_count_badge      | box    | #BA1A1A bg, radius 12, pad H10/V4; shows unread count from API                                            |
| unread_count_text       | text   | "5 unread" — Outfit/label_medium, #FFFFFF, weight 700                                                     |
| search_bar              | input  | Filled search, #F9FAEF bg, radius 28, pad H16, placeholder "Search messages…", leading search icon        |
| thread_1                | box    | Unread card — #CDEDA3 bg, radius 12, pad 14, 1dp #C5C8BA border; John Mwangi thread                      |
| thread_1_avatar         | box    | 44×44 circle, #4C662B fill, "JM" initials (Outfit/label_large, #FFFFFF, w700)                            |
| thread_1_name           | text   | "John Mwangi" — Outfit/title_small, #1A1C16, weight 700                                                   |
| thread_1_time           | text   | "2 min ago" — Outfit/body_small, #4C662B, weight 600                                                     |
| thread_1_preview        | text   | "Please send me the account statement for…" — Outfit/body_medium, #1A1C16, maxLines 1, ellipsis           |
| thread_1_unread_dot     | box    | 10×10 circle, #4C662B fill — unread indicator dot                                                         |
| thread_2                | box    | Read card — #FFFFFF bg, radius 12, pad 14, 1dp #E1E4D5 border; Sarah Odhiambo thread                     |
| thread_2_avatar         | box    | 44×44 circle, #386663 fill, "SO" initials (Outfit/label_large, #FFFFFF, w700)                            |
| thread_2_name           | text   | "Sarah Odhiambo" — Outfit/title_small, #1A1C16, weight 600                                                |
| thread_2_time           | text   | "1 hr ago" — Outfit/body_small, #44483D                                                                   |
| thread_2_preview        | text   | "Thank you for approving my application!" — Outfit/body_medium, #44483D, maxLines 1                       |
| thread_3                | box    | Read card — #FFFFFF bg, radius 12, pad 14, 1dp #E1E4D5 border; Peter Kamau thread                        |
| thread_3_avatar         | box    | 44×44 circle, #44483D fill, "PK" initials (Outfit/label_large, #FFFFFF, w700)                            |
| thread_3_name           | text   | "Peter Kamau" — Outfit/title_small, #1A1C16, weight 600                                                   |
| thread_3_time           | text   | "Yesterday" — Outfit/body_small, #44483D                                                                  |
| thread_3_preview        | text   | "When can I expect my card to arrive?" — Outfit/body_medium, #44483D, maxLines 1                          |
| new_message_fab         | button | Extended FAB bottom-right: "New Message", edit icon, #4C662B bg, #FFFFFF text, elevation 6, margin B24/R16|
| compose_sheet           | box    | Dialog: #FFFFFF bg, radius 20, pad 20 — compose heading + customer autocomplete + subject + body + send   |
| compose_heading         | text   | "New Message" — Outfit/title_medium, #1A1C16, weight 700                                                  |
| compose_customer_select | input  | Outlined autocomplete "Customer" — placeholder "Search customers…"                                        |
| compose_subject_input   | input  | Outlined text "Subject" — placeholder "Account query, Document request…"                                  |
| compose_message_input   | input  | Outlined textarea "Message" — placeholder "Type your message to the customer…", minLines 4, maxLines 8    |
| send_message_button     | button | Filled full-width "Send Message" — #4C662B bg, #FFFFFF text                                               |

---

## States

| ID      | Trigger                  | Description                                                                              |
|---------|--------------------------|------------------------------------------------------------------------------------------|
| loading | Screen entry             | Skeleton shimmer replacing thread cards; title row and search bar remain visible          |
| content | API load success         | All threads rendered with real names, previews, timestamps; FAB active; badge populated  |
| empty   | Zero message threads     | Empty state: forum icon + "No Messages" title + "Start a conversation by composing…"     |
| error   | Network or API failure   | Error banner with retry action; no thread data shown                                     |

---

## State Model

**ViewModel:** `CustomerMessagesViewModel`
**Screen State Type:** `CustomerMessagesScreenState`

| Name            | Type                     | Default     |
|-----------------|--------------------------|-------------|
| threads         | List\<MessageThread\>    | emptyList() |
| searchQuery     | String                   | ""          |
| filteredThreads | List\<MessageThread\>    | emptyList() |
| unreadCount     | Int                      | 0           |
| isComposeOpen   | Boolean                  | false       |
| composeDraft    | MessageComposeDraft?     | null        |
| isSending       | Boolean                  | false       |

**Events:** `ThreadOpened`, `MessageSent`, `SearchExecuted`, `ComposeOpened`, `ComposeDismissed`

**Actions:** `open_thread`, `new_message`, `send_message`, `search`, `search_customer`

**DI Dependencies:** `CustomerMessagingRepository`, `CustomerSearchService`

**Errors:**
- `LOAD_FAILED`: "Could not load messages. Please try again."
- `SEND_FAILED`: "Message could not be sent. Check your connection."
- `NETWORK_UNAVAILABLE`: "No internet connection. Messages may be delayed."

---

## Navigation

| From               | To                   | Trigger                         | Type    |
|--------------------|----------------------|---------------------------------|---------|
| customer-messages  | john_mwangi_thread   | thread_1 tap (open_thread)      | push    |
| customer-messages  | sarah_odhiambo_thread| thread_2 tap (open_thread)      | push    |
| customer-messages  | peter_kamau_thread   | thread_3 tap (open_thread)      | push    |
| customer-messages  | compose_sheet        | new_message_fab tap             | modal   |
| customer-messages  | customer-messages    | send_message_button tap         | dismiss |
| customer-messages  | fo-dashboard         | nav_dashboard bottom tab        | tab     |
| customer-messages  | customer-search      | nav_customers bottom tab        | tab     |
| customer-messages  | account-applications | nav_applications bottom tab     | tab     |
| customer-messages  | settings             | nav_more bottom tab             | tab     |

---

## API Endpoints

| Endpoint                                                                   | Auth        | Tag               | Purpose                                    |
|----------------------------------------------------------------------------|-------------|-------------------|--------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/customers/{customerId}/messages             | DirectLogin | Customer-Messages | Fetch all message threads for this officer |
| POST /obp/v4.0.0/banks/{bankId}/customers/{customerId}/messages            | DirectLogin | Customer-Messages | Send new message to customer               |

---

## Design Tokens

| Token                         | Value   | Usage                                                              |
|-------------------------------|---------|--------------------------------------------------------------------|
| color.light.primary           | #4C662B | Title text, unread timestamp, unread dot, FAB background, send btn  |
| color.light.secondary         | #386663 | Sarah Odhiambo avatar fill                                         |
| color.light.primary_container | #CDEDA3 | Unread thread card background                                      |
| color.light.error             | #BA1A1A | Unread count badge background                                      |
| color.light.on_surface_variant| #44483D | Peter Kamau avatar, read timestamps, read previews                 |
| color.light.on_surface        | #1A1C16 | Thread names, unread preview text                                  |
| color.light.surface           | #FFFFFF | Read thread cards, compose dialog background                       |
| color.light.background        | #F9FAEF | Screen background, search bar fill                                 |
| color.light.outline_variant   | #C5C8BA | Unread thread card border                                          |
| color.light.surface_variant   | #E1E4D5 | Read thread card border                                            |
| typography.headline_large     | —       | "Messages" screen title                                            |
| typography.title_small        | —       | Customer name in thread row                                        |
| typography.title_medium       | —       | Compose dialog heading                                             |
| typography.body_medium        | —       | Message preview text, compose fields                               |
| typography.body_small         | —       | Thread timestamps                                                  |
| typography.label_medium       | —       | Unread count badge text                                            |
| typography.label_large        | —       | Avatar initials                                                    |
| radius.md                     | 12dp    | Thread cards                                                       |
| radius.xl                     | 24dp    | Compose dialog                                                     |

---

_Generated by /idea export | 2026-05-29_
