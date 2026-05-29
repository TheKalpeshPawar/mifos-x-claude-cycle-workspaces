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

The Customer Messages screen is the Messaging Center for Field Officer persona users. It displays all customer communication threads in a scrollable index_list with an unread count badge (5 unread, #BA1A1A fill), a search bar for filtering messages, and individual thread cards showing customer initials avatar, name, message preview, and timestamp. Unread threads render on a #CDEDA3 (primary_container) background with a green unread dot; read threads use #FFFFFF (surface). A floating extended FAB ("New Message", edit icon) opens a compose dialog with customer autocomplete, subject, and message body fields. Data is fetched from the OBP Customer Messages API on screen entry. Supports loading/content/empty/error states with skeleton shimmer, empty illustration, and retry banner respectively.

---

## Screens

| ID                       | Name              | Route              | Layout | Scroll   |
|--------------------------|-------------------|--------------------|--------|----------|
| customer-messages-main   | Messaging Center  | /customer-messages | Column | Vertical |

**Shell:** Field-officer flavor. No bottom navigation declared on this screen; navigated to from customer-detail, application-detail, and kyc-review flows.

---

## Components

| ID                      | Type   | Description                                                                                                          |
|-------------------------|--------|----------------------------------------------------------------------------------------------------------------------|
| messages_title_row      | box    | Horizontal row, space-between, 16dp horizontal pad, 20dp top / 8dp bottom — contains title + unread badge           |
| messages_title          | text   | "Messages" — Outfit/headline_large, #4C662B, weight 700, heading level 1                                            |
| unread_count_badge      | box    | #BA1A1A fill, 12dp radius, 10dp horizontal / 4dp vertical padding — derived from obp_get_customer_messages unread_count |
| unread_count_text       | text   | "5 unread" — Outfit/label_medium, #FFFFFF, weight 700                                                               |
| search_bar              | input  | Search type, filled variant, placeholder "Search messages…", search prefix icon, #F9FAEF bg, 28dp radius, 16dp horiz margin / 12dp bottom margin |
| thread_1                | box    | Unread thread: #CDEDA3 fill, 12dp radius, 14dp padding, 16dp horiz margin, 8dp bottom margin, 1dp elevation, #C5C8BA border — John Mwangi |
| thread_1_avatar         | box    | #4C662B fill, 22dp radius, 44×44dp, initials "JM" (label_large, #FFFFFF, weight 700)                               |
| thread_1_name           | text   | "John Mwangi" — Outfit/title_small, #1A1C16, weight 700                                                             |
| thread_1_time           | text   | "2 min ago" — Outfit/body_small, #4C662B, weight 600                                                                |
| thread_1_preview        | text   | "Please send me the account statement for…" — Outfit/body_medium, #1A1C16, maxLines 1, ellipsis                    |
| thread_1_unread_dot     | box    | #4C662B fill, 5dp radius, 10×10dp — unread indicator                                                               |
| thread_2                | box    | Read thread: #FFFFFF fill, 12dp radius, 14dp padding, 16dp horiz margin, 8dp bottom margin, 1dp elevation — Sarah Odhiambo |
| thread_2_avatar         | box    | #386663 fill, 22dp radius, 44×44dp, initials "SO" (label_large, #FFFFFF, weight 700)                               |
| thread_2_name           | text   | "Sarah Odhiambo" — Outfit/title_small, #1A1C16, weight 600                                                          |
| thread_2_time           | text   | "1 hr ago" — Outfit/body_small, #44483D                                                                             |
| thread_2_preview        | text   | "Thank you for approving my application!" — Outfit/body_medium, #44483D, maxLines 1, ellipsis                      |
| thread_3                | box    | Read thread: #FFFFFF fill, 12dp radius, 14dp padding, 16dp horiz margin, 8dp bottom margin, 1dp elevation — Peter Kamau |
| thread_3_avatar         | box    | #44483D fill (on_surface_variant), 22dp radius, 44×44dp, initials "PK" (label_large, #FFFFFF, weight 700)           |
| thread_3_name           | text   | "Peter Kamau" — Outfit/title_small, #1A1C16, weight 600                                                             |
| thread_3_time           | text   | "Yesterday" — Outfit/body_small, #44483D                                                                            |
| thread_3_preview        | text   | "When can I expect my card to arrive?" — Outfit/body_medium, #44483D, maxLines 1, ellipsis                          |
| new_message_fab         | button | Extended FAB — "New Message", edit icon, #4C662B fill, #FFFFFF text, position bottom_right, 24dp bottom / 16dp right margin, 6dp elevation |
| compose_sheet           | box    | Dialog type, #FFFFFF fill, 20dp radius, 20dp padding, conditionally visible — compose new message                   |
| compose_heading         | text   | "New Message" — Outfit/title_medium, #1A1C16, weight 700, heading level 2                                           |
| compose_customer_select | input  | Outlined autocomplete, label "Customer", placeholder "Search customers…", 12dp bottom margin                         |
| compose_subject_input   | input  | Outlined text, label "Subject", placeholder "Account query, Document request…", 12dp bottom margin                  |
| compose_message_input   | input  | Outlined textarea, label "Message", placeholder "Type your message to the customer…", minLines 4, maxLines 8        |
| send_message_button     | button | "Send Message" — filled, #4C662B fill, #FFFFFF text, full width                                                     |

---

## States

| ID      | Trigger                                          | Description                                                                                              |
|---------|--------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| loading | Screen entry / network retry                     | Skeleton shimmer (short4 = 200ms, reduced-motion: static placeholder). Scroll vertical, showShimmer true |
| content | obp_get_customer_messages returns threads        | Full thread list with search bar, unread badge, and FAB. Background #F9FAEF                              |
| empty   | API returns zero threads                         | "No Messages" title, "Start a conversation by composing a new message to a customer" subtitle, message icon, FAB still visible |
| error   | LOAD_FAILED / NETWORK_UNAVAILABLE                | Error banner with "Could not load messages. Please try again." and retry action                           |

---

## State Model

**ViewModel:** `CustomerMessagesViewModel`
**Screen State Type:** `CustomerMessagesScreenState`

| Name            | Type                       | Default     |
|-----------------|----------------------------|-------------|
| threads         | List\<MessageThread\>      | emptyList() |
| searchQuery     | String                     | ""          |
| filteredThreads | List\<MessageThread\>      | emptyList() |
| unreadCount     | Int                        | 0           |
| isComposeOpen   | Boolean                    | false       |
| composeDraft    | MessageComposeDraft?       | null        |
| isSending       | Boolean                    | false       |

**Errors:** `LOAD_FAILED`, `SEND_FAILED`, `NETWORK_UNAVAILABLE`

**Events:** `ThreadOpened`, `MessageSent`, `SearchExecuted`, `ComposeOpened`, `ComposeDismissed`

**Actions:** `open_thread`, `new_message`, `send_message`, `search`, `search_customer`

**DI Dependencies:** `CustomerMessagingRepository`, `CustomerSearchService`

---

## Navigation

| From              | To                      | Trigger                          | Type   |
|-------------------|-------------------------|----------------------------------|--------|
| customer-messages | john_mwangi_thread      | thread_1 tap (open_thread)       | push   |
| customer-messages | sarah_odhiambo_thread   | thread_2 tap (open_thread)       | push   |
| customer-messages | peter_kamau_thread      | thread_3 tap (open_thread)       | push   |
| customer-messages | compose_sheet           | new_message_fab tap (new_message)| dialog |
| customer-messages | customer-messages       | send_message_button tap          | dismiss dialog |
| search_bar        | search_results          | search action                    | filter |
| compose_customer_select | customer search   | search_customer action           | inline |

---

## API Endpoints

| Endpoint                                                                    | Auth        | Tag               | Purpose                                               |
|-----------------------------------------------------------------------------|-------------|-------------------|-------------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/customers/{customerId}/messages              | DirectLogin | Customer-Messages | Fetch all message threads; derives unread_count       |
| POST /obp/v4.0.0/banks/{bankId}/customers/{customerId}/messages             | DirectLogin | Customer-Messages | Send new message to customer from compose dialog      |

---

## Design Tokens

| Token                              | Value     | Usage                                                                      |
|------------------------------------|-----------|----------------------------------------------------------------------------|
| colors.light.primary               | #4C662B   | Title text, time label on unread thread, thread_1 avatar, unread dot, FAB fill, send button fill |
| colors.light.primary_container     | #CDEDA3   | Unread thread card fill (thread_1)                                          |
| colors.light.secondary             | #386663   | thread_2 avatar fill                                                        |
| colors.light.error                 | #BA1A1A   | Unread count badge fill                                                     |
| colors.light.on_error              | #FFFFFF   | Unread count badge text                                                     |
| colors.light.background            | #F9FAEF   | Screen background (content state), search bar fill                          |
| colors.light.surface               | #FFFFFF   | Read thread cards (thread_2, thread_3), compose dialog fill                 |
| colors.light.on_surface            | #1A1C16   | Thread names, message preview text (unread thread), compose heading         |
| colors.light.on_surface_variant    | #44483D   | thread_3 avatar fill, read thread timestamp, read thread preview text       |
| colors.light.surface_variant       | #E1E4D5   | Read thread card border                                                     |
| colors.light.outline_variant       | #C5C8BA   | Unread thread card border                                                   |
| typography.headline_large          | Outfit 32sp/400 | "Messages" screen title                                               |
| typography.title_small             | Outfit 14sp/500 | Thread customer names                                                  |
| typography.title_medium            | Outfit 16sp/500 | Compose dialog heading                                                 |
| typography.body_medium             | Outfit 14sp/400 | Message preview text                                                   |
| typography.body_small              | Outfit 12sp/400 | Thread timestamps                                                       |
| typography.label_medium            | Outfit 12sp/500 | Unread count badge text, FAB label                                     |
| radius.md                          | 12dp      | Thread card corners, unread badge corners                               |
| radius.xl                          | 24dp      | Compose dialog corners (20dp — near xl)                                 |
| radius.pill                        | 999dp     | Search bar (28dp radius)                                                |
| elevation.level1                   | 1dp       | Thread cards                                                            |
| elevation.level3                   | 6dp       | New Message FAB                                                         |
| motion.duration.short4             | 200ms     | Skeleton shimmer duration                                               |

---

_Generated by /idea export | 2026-05-30_
