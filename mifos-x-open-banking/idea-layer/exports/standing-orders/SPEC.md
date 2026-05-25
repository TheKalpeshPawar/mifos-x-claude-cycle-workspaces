# Standing Orders — Feature Specification

| Field | Value |
|---|---|
| Feature | standing-orders |
| Flavor | consumer |
| Status | enriched |
| Quality Score | 80 |

---

## Overview

The Standing Orders screen lists all recurring payment instructions set up by the user, showing each order's beneficiary, amount per period, status (Active / Paused), and next scheduled payment date. Users can view, edit, or delete existing standing orders and create new ones via a floating action button. The screen uses an index_list archetype with status-badge differentiation and row-level action icons.

---

## Screens

| Screen ID | Route | Layout | Scroll |
|---|---|---|---|
| standing-orders | /standing-orders | index_list | vertical |

**Shell:** Back navigation (arrow_back). Top bar "Standing Orders" with `filter_list` action. No bottom navigation.

---

## Components

| ID | Type | Description |
|---|---|---|
| title_count_row | stack | Horizontal row: title + active count chip |
| standing_orders_title | text | "Standing Orders", headline_large, #1800B1 |
| active_count_chip | box | "3 active" — #E8F5E9 background, #4CAF50 text, r=12dp |
| standing_order_rent | box | Card for "Rent Payment" — Active, £1,200/month |
| rent_title | text | "Rent Payment", title_medium, semibold |
| rent_active_badge | box | "Active" badge — #E8F5E9/#4CAF50 |
| rent_beneficiary | text | "To: Landlord Holdings Ltd" |
| rent_amount | text | "£1,200 / month", #1800B1, semibold |
| rent_next_date | text | "Next: 1 Jun 2026", body_small |
| rent_edit_icon | icon | `edit_outlined`, 22dp, #1800B1 |
| rent_delete_icon | icon | `delete_outlined`, 22dp, #FF5252 |
| standing_order_netflix | box | Card for "Netflix Subscription" — Active, £15.99/month |
| netflix_title | text | "Netflix Subscription", title_medium, semibold |
| netflix_active_badge | box | "Active" badge — #E8F5E9/#4CAF50 |
| netflix_amount | text | "£15.99 / month", #1800B1, semibold |
| netflix_next_date | text | "Next: 7 Jun 2026" |
| netflix_edit_icon | icon | `edit_outlined`, 22dp, #1800B1 |
| netflix_delete_icon | icon | `delete_outlined`, 22dp, #FF5252 |
| standing_order_gym | box | Card for "Gym Membership" — Paused, £45.00/month |
| gym_title | text | "Gym Membership", title_medium, #888888 (dimmed) |
| gym_paused_badge | box | "Paused" badge — #F5F5F5/#9E9E9E |
| gym_amount | text | "£45.00 / month", #9E9E9E (dimmed) |
| gym_next_date | text | "Next: 15 Jun 2026 (Paused)", #BBBBBB |
| gym_edit_icon | icon | `edit_outlined`, 22dp, #1800B1 |
| gym_delete_icon | icon | `delete_outlined`, 22dp, #FF5252 |
| create_standing_order_fab | button | Floating action button — "Create Standing Order", #1800B1, r=16dp |

---

## States

| State ID | Trigger | Description |
|---|---|---|
| loading | Screen entry | Title row visible, skeleton list (3 items) |
| content | API data loaded | Full list of standing orders with FAB |
| empty | No standing orders | repeat_off icon, "No standing orders", "Set up recurring payments to automate your regular bills", FAB visible |
| error | API failure | cloud_off icon, "Unable to load standing orders", "Check your connection and try again", retry button, FAB visible |

---

## State Model

**ViewModel:** `StandingOrdersViewModel`

| Field | Type | Default |
|---|---|---|
| standingOrders | List\<StandingOrder\> | emptyList() |
| activeCount | Int | 0 |
| selectedOrderId | String | "" |
| uiState | StandingOrdersUiState | Loading |

**Events:** OrdersLoaded, ViewOrderClicked, EditOrderClicked, DeleteOrderClicked, DeleteOrderConfirmed, CreateOrderClicked, FilterChanged, RefreshTriggered

**Actions:** view_standing_order, edit_standing_order, delete_standing_order, create_standing_order, filter_standing_orders

**DI Dependencies:** StandingOrderRepository, AccountRepository

**Error Codes:**

| Field | Code | Message |
|---|---|---|
| global | LOAD_FAILED | "Unable to load standing orders. Please try again." |
| delete | DELETE_FAILED | "Could not delete standing order. Please try again." |
| create | CREATE_FAILED | "Could not create standing order. Please try again." |

---

## Navigation

| From | To | Trigger | Type |
|---|---|---|---|
| standing-orders | (detail sheet) | Tap standing order card | bottom sheet |
| standing-orders | (create sheet) | Tap FAB | bottom sheet |

---

## API Endpoints

| Endpoint | Auth | Purpose |
|---|---|---|
| POST /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/owner/standing-order | DirectLogin | Create a new standing order (POST-only; list via transaction history) |

---

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| primary | #1800B1 | Title, amounts, edit icons, FAB |
| active_badge_bg | #E8F5E9 | Active status badge background |
| active_badge_text | #4CAF50 | Active status badge text |
| paused_badge_bg | #F5F5F5 | Paused badge background |
| paused_badge_text | #9E9E9E | Paused badge text and dimmed content |
| delete_icon | #FF5252 | Delete icon color |
| surface | #FFFFFF | Active order card background |
| surface_dimmed | #FAFAFA | Paused order card background |
| card_border | #F0F0F0 | Active card border |
| paused_border | #E0E0E0 | Paused card border (slightly stronger) |

---

*Generated by /idea export | 2026-05-25*
