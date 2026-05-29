# SPEC — Standing Orders

| Field         | Value                     |
|---------------|---------------------------|
| Feature       | standing-orders           |
| Flavor        | consumer                  |
| Status        | approved                  |
| Quality Score | 93                        |
| ViewModel     | StandingOrdersViewModel   |

---

## Overview

The Standing Orders screen is the Consumer persona's hub for viewing and managing all recurring payment instructions linked to the user's account. It presents a scrollable list of standing-order cards — each showing the beneficiary name, amount, frequency, next payment date, and status badge — alongside inline edit and delete actions. An Extended FAB anchors to the bottom-right for creating new orders. The screen supports loading, populated-list, empty, and error states. Active orders display in white elevated cards; paused orders use a muted outlined variant on `#F9FAEF`. Data is managed via POST (OBP has no GET-list endpoint; standing orders are created and list is inferred from transaction history).

---

## Screens

| ID              | Name            | Route             | Layout | Scroll   |
|-----------------|-----------------|-------------------|--------|----------|
| standing-orders | Standing Orders | /standing-orders  | Column | Vertical |

**Shell:** Top app bar with back arrow + filter action. No bottom navigation bar.

| Element         | Value                                |
|-----------------|--------------------------------------|
| Title           | "Standing Orders"                    |
| Navigation icon | arrow_back                           |
| Action 1        | filter_list → filter_standing_orders |

---

## Components

| ID                        | Type   | Description                                                                                             |
|---------------------------|--------|---------------------------------------------------------------------------------------------------------|
| title_count_row           | stack  | Horizontal row — screen title + active count chip; align center, padding_bottom 16dp                   |
| standing_orders_title     | text   | "Standing Orders" — Outfit/headline_large, color `#4C662B`                                             |
| active_count_chip         | box    | "3 active" — background `#CDEDA3`, radius 12, 10dp H-padding, text `#4C662B`, Outfit/label_medium SemiBold |
| standing_order_rent       | box    | Rent Payment card — `#FFFFFF`, radius 16, elevation 2, border `#F9FAEF`; tappable → standing-order-detail |
| rent_header_row           | stack  | Row: rent_title + rent_active_badge (space_between, align flex_start)                                   |
| rent_title                | text   | "Rent Payment" — Outfit/title_medium SemiBold, `#1A1C16`                                              |
| rent_active_badge         | box    | "Active" — background `#CDEDA3`, radius 10, text `#4C662B`, Outfit/label_small                        |
| rent_beneficiary          | text   | "To: Landlord Holdings Ltd" — Outfit/body_medium, `#44483D`                                           |
| rent_amount_row           | stack  | Row: rent_amount + rent_next_date (space_between, align center)                                         |
| rent_amount               | text   | "£1,200 / month" — Outfit/body_large SemiBold, `#4C662B`                                             |
| rent_next_date            | text   | "Next: 1 Jun 2026" — Outfit/body_small, `#44483D`                                                    |
| rent_actions_row          | stack  | Row of action icons — flex_end, padding_top 16dp                                                       |
| rent_edit_icon            | icon   | edit_outlined 22dp, `#4C662B`, 8dp padding; navigates to standing-order-edit                          |
| rent_delete_icon          | icon   | delete_outlined 22dp, `#BA1A1A`, 8dp padding; triggers delete confirmation dialog                     |
| standing_order_netflix    | box    | Netflix Subscription card — same elevated white variant                                                  |
| netflix_title             | text   | "Netflix Subscription" — Outfit/title_medium SemiBold, `#1A1C16`                                     |
| netflix_active_badge      | box    | "Active" — background `#CDEDA3`, text `#4C662B`                                                       |
| netflix_amount            | text   | "£15.99 / month" — Outfit/body_large SemiBold, `#4C662B`                                             |
| netflix_next_date         | text   | "Next: 7 Jun 2026" — Outfit/body_small, `#44483D`                                                    |
| netflix_edit_icon         | icon   | edit_outlined 22dp, `#4C662B`                                                                          |
| netflix_delete_icon       | icon   | delete_outlined 22dp, `#BA1A1A`                                                                        |
| standing_order_gym        | box    | Gym Membership card — outlined variant, background `#F9FAEF`, border `#E1E4D5`, radius 16 (paused)    |
| gym_title                 | text   | "Gym Membership" — Outfit/title_medium SemiBold, `#44483D` (muted = paused)                           |
| gym_paused_badge          | box    | "Paused" — background `#F9FAEF`, text `#44483D`                                                       |
| gym_amount                | text   | "£45.00 / month" — Outfit/body_large SemiBold, `#44483D` (muted)                                     |
| gym_next_date             | text   | "Next: 15 Jun 2026 (Paused)" — Outfit/body_small, `#44483D`                                          |
| gym_edit_icon             | icon   | edit_outlined 22dp, `#4C662B`                                                                          |
| gym_delete_icon           | icon   | delete_outlined 22dp, `#BA1A1A`                                                                        |
| create_standing_order_fab | button | Extended FAB — "Create Standing Order", background `#4C662B`, white text, leading icon `add`, radius 16, elevation 6 |

---

## States

| ID      | Trigger                         | Description                                                                          |
|---------|---------------------------------|--------------------------------------------------------------------------------------|
| loading | Screen entry / RefreshTriggered | Title row visible; 3 skeleton shimmer cards replace list                             |
| content | OrdersLoaded success            | Full list: count chip + all 3 order cards + FAB                                      |
| empty   | No orders returned              | Title only; repeat_off icon, "No standing orders", "Set up recurring payments…"; FAB |
| error   | LOAD_FAILED                     | Title only; cloud_off icon, "Unable to load standing orders", retry button; FAB      |

---

## State Model

**ViewModel:** `StandingOrdersViewModel`
**Screen State Type:** `StandingOrdersUiState`

| Name            | Type                    | Default     |
|-----------------|-------------------------|-------------|
| standingOrders  | List\<StandingOrder\>   | emptyList() |
| activeCount     | Int                     | 0           |
| selectedOrderId | String                  | ""          |
| uiState         | StandingOrdersUiState   | Loading     |

**Events:** `OrdersLoaded`, `ViewOrderClicked`, `EditOrderClicked`, `DeleteOrderClicked`, `DeleteOrderConfirmed`, `CreateOrderClicked`, `FilterChanged`, `RefreshTriggered`

**Actions:** `view_standing_order`, `edit_standing_order`, `delete_standing_order`, `create_standing_order`, `filter_standing_orders`

**DI Dependencies:** `StandingOrderRepository`, `AccountRepository`

**Errors:**
- `LOAD_FAILED`: "Unable to load standing orders. Please try again."
- `DELETE_FAILED`: "Could not delete standing order. Please try again."
- `CREATE_FAILED`: "Could not create standing order. Please try again."

---

## Navigation

| From            | To                    | Trigger                           | Type  |
|-----------------|-----------------------|-----------------------------------|-------|
| standing-orders | standing-order-detail | Tap any order card                | push  |
| standing-orders | standing-order-edit   | Tap edit icon on any order        | push  |
| standing-orders | (create flow)         | Tap create_standing_order_fab     | push  |
| standing-orders | accounts              | Back arrow (top bar)              | pop   |

---

## API Endpoints

| Endpoint                                                                          | Auth        | Tag             | Purpose                                                                    |
|-----------------------------------------------------------------------------------|-------------|-----------------|----------------------------------------------------------------------------|
| POST /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/owner/standing-order         | DirectLogin | Standing-Orders | Create a new standing order (POST-only; no GET list — derived from history)|

---

## Design Tokens

| Token                          | Value   | Usage                                                                  |
|--------------------------------|---------|------------------------------------------------------------------------|
| color.light.primary            | #4C662B | Title text, active badge text, amount text, edit icon, FAB background  |
| color.light.primary_container  | #CDEDA3 | Active badge background, count chip background                         |
| color.light.error              | #BA1A1A | Delete icon color                                                      |
| color.light.surface            | #FFFFFF | Active order card background                                           |
| color.light.background         | #F9FAEF | Screen background, paused card background                              |
| color.light.surface_variant    | #E1E4D5 | Paused card border                                                     |
| color.light.on_surface         | #1A1C16 | Active order title text                                                |
| color.light.on_surface_variant | #44483D | Beneficiary text, next-date text, paused title + amount + date text    |
| typography.headline_large      | —       | Screen title "Standing Orders" (32sp/400)                              |
| typography.title_medium        | —       | Order name labels (16sp/500)                                           |
| typography.body_large          | —       | Amount + frequency text (16sp/400)                                     |
| typography.body_medium         | —       | Beneficiary name (14sp/400)                                            |
| typography.body_small          | —       | Next payment date (12sp/400)                                           |
| typography.label_medium        | —       | Count chip "3 active" (12sp/500)                                       |
| typography.label_small         | —       | Status badges Active / Paused (11sp/500)                               |
| radius.lg                      | 16dp    | Order card border radius, FAB radius                                   |
| elevation.level2               | 3dp     | Active order card shadow                                               |
| spacing.md                     | 16dp    | Card internal padding, section gaps                                    |
| spacing.sm                     | 8dp     | Badge inner padding, action icon padding                               |
| spacing.xs                     | 4dp     | Badge vertical padding                                                 |

---

_Generated by /idea export | 2026-05-29_
