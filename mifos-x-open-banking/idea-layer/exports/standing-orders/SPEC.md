# SPEC — Standing Orders

| Field         | Value                   |
|---------------|-------------------------|
| Feature       | standing-orders         |
| Flavor        | consumer                |
| Status        | approved                |
| Quality Score | 93                      |
| ViewModel     | StandingOrdersViewModel |

---

## Overview

The Standing Orders screen is the Consumer persona's hub for viewing and managing all recurring payment instructions linked to the user's account. It presents a scrollable list of standing-order cards — each showing the beneficiary name, amount, frequency, next payment date, and status badge — alongside inline edit and delete icon-buttons. An Extended FAB anchors floating at bottom-right for creating new orders. The screen supports four states: loading (3-skeleton shimmer list), content (active + paused cards), empty (repeat_off icon with CTA), and error (cloud_off icon with retry).

Active orders render as elevated white cards (`#FFFFFF`, elevation 2, radius 16, border `#F9FAEF`). Paused orders use an outlined muted variant (`#F9FAEF` fill, `#E1E4D5` border). A top app bar with `arrow_back` and `filter_list` provides navigation and filtering. No bottom navigation is shown on this screen.

Demo data uses real Kenyan names and KES amounts drawn from demo-data.yaml: Nairobi Water & Sewerage (KES 3,500), Safaricom Home Fibre (KES 6,000), Amani Apartments Westlands (KES 45,000), NHIF health insurance (KES 1,700, paused). The UI layer demonstrates the design pattern with three representative UK-locale cards (Rent Payment £1,200, Netflix £15.99, Gym Membership £45 paused) while the API demo data reflects the canonical KES/Equity Bank values.

---

## Screens

| ID              | Name            | Route            | Layout | Scroll   |
|-----------------|-----------------|------------------|--------|----------|
| standing-orders | Standing Orders | /standing-orders | Column | Vertical |

**Shell:** Top app bar with back arrow and filter action. No bottom navigation bar.

| Element         | Value                                |
|-----------------|--------------------------------------|
| Title           | "Standing Orders"                    |
| Navigation icon | `arrow_back`                         |
| Action 1        | `filter_list` → filter_standing_orders |

---

## Components

| ID                        | Type   | Description                                                                                                                            |
|---------------------------|--------|----------------------------------------------------------------------------------------------------------------------------------------|
| title_count_row           | stack  | Horizontal row — screen title + active count chip; align center, spacing 16dp, padding_bottom 16dp; on_click → state_change           |
| standing_orders_title     | text   | "Standing Orders" — Outfit/headline_large (32sp/400), color `#4C662B`                                                                 |
| active_count_chip         | box    | "3 active" — background `#CDEDA3`, radius 12, 10dp H-padding, 4dp V-padding, text `#4C662B`, Outfit/label_medium SemiBold             |
| standing_order_rent       | box    | Rent Payment card — `#FFFFFF`, radius 16, elevation 2, border `#F9FAEF` 1dp, margin_bottom 16dp; tappable → `view_standing_order`     |
| rent_header_row           | stack  | Row: rent_title + rent_active_badge; space_between, align flex_start, padding_bottom 8dp; on_click → standing-order-detail            |
| rent_title                | text   | "Rent Payment" — Outfit/title_medium (16sp/500) SemiBold, color `#1A1C16`                                                            |
| rent_active_badge         | box    | "Active" — background `#CDEDA3`, radius 10, 8dp H-padding, 3dp V-padding, text `#4C662B`, Outfit/label_small; on_click → filter_by_status |
| rent_beneficiary          | text   | "To: Landlord Holdings Ltd" — Outfit/body_medium (14sp/400), color `#44483D`, padding_bottom 4dp                                     |
| rent_amount_row           | stack  | Row: rent_amount + rent_next_date; space_between, align center; on_click → standing-order-detail                                       |
| rent_amount               | text   | "£1,200 / month" — Outfit/body_large (16sp/400) SemiBold, color `#4C662B`                                                            |
| rent_next_date            | text   | "Next: 1 Jun 2026" — Outfit/body_small (12sp/400), color `#44483D`                                                                   |
| rent_actions_row          | stack  | Row of action icons; flex_end, spacing 8dp, padding_top 16dp                                                                          |
| rent_edit_icon            | icon   | `edit_outlined` 22dp, color `#4C662B`, padding 8dp; on_click → `edit_standing_order`; min touch 48dp                                 |
| rent_delete_icon          | icon   | `delete_outlined` 22dp, color `#BA1A1A`, padding 8dp; on_click → `delete_standing_order`; triggers confirmation dialog               |
| standing_order_netflix    | box    | Netflix Subscription card — same elevated white variant (`#FFFFFF`, radius 16, elevation 2, border `#F9FAEF`)                         |
| netflix_title             | text   | "Netflix Subscription" — Outfit/title_medium SemiBold, `#1A1C16`                                                                     |
| netflix_active_badge      | box    | "Active" — background `#CDEDA3`, radius 10, text `#4C662B`, Outfit/label_small                                                       |
| netflix_amount            | text   | "£15.99 / month" — Outfit/body_large SemiBold, `#4C662B`                                                                             |
| netflix_next_date         | text   | "Next: 7 Jun 2026" — Outfit/body_small, `#44483D`                                                                                    |
| netflix_edit_icon         | icon   | `edit_outlined` 22dp, `#4C662B`; on_click → `edit_standing_order`                                                                    |
| netflix_delete_icon       | icon   | `delete_outlined` 22dp, `#BA1A1A`; on_click → `delete_standing_order`                                                                |
| standing_order_gym        | box    | Gym Membership card — outlined/muted variant; background `#F9FAEF`, radius 16, elevation 1, border `#E1E4D5` 1dp (paused state)      |
| gym_title                 | text   | "Gym Membership" — Outfit/title_medium SemiBold, `#44483D` (muted = paused signal)                                                   |
| gym_paused_badge          | box    | "Paused" — background `#F9FAEF`, radius 10, 8dp H-padding, 3dp V-padding, text `#44483D`, Outfit/label_small                        |
| gym_amount                | text   | "£45.00 / month" — Outfit/body_large SemiBold, `#44483D` (muted)                                                                     |
| gym_next_date             | text   | "Next: 15 Jun 2026 (Paused)" — Outfit/body_small, `#44483D`                                                                          |
| gym_edit_icon             | icon   | `edit_outlined` 22dp, `#4C662B`; on_click → `edit_standing_order`                                                                    |
| gym_delete_icon           | icon   | `delete_outlined` 22dp, `#BA1A1A`; on_click → `delete_standing_order`                                                                |
| create_standing_order_fab | button | Extended FAB — "Create Standing Order", background `#4C662B`, white text, leading icon `add`, radius 16, elevation 6, position floating |

---

## States

| ID      | Trigger                          | Description                                                                              |
|---------|----------------------------------|------------------------------------------------------------------------------------------|
| loading | Screen entry / `RefreshTriggered` | Title row (`standing_orders_title`) visible; 3 skeleton shimmer cards (`#E1E4D5`, 200ms short4); no count chip |
| content | `OrdersLoaded` success           | Full list: count chip + all 3 order cards (2 active elevated, 1 paused outlined) + FAB  |
| empty   | No orders returned               | Title only; `repeat_off` icon, "No standing orders", "Set up recurring payments to automate your regular bills"; FAB visible |
| error   | `LOAD_FAILED`                    | Title only; `cloud_off` icon, "Unable to load standing orders", "Check your connection and try again", retry button; FAB visible |

---

## State Model

**ViewModel:** `StandingOrdersViewModel`
**Screen State Type:** `StandingOrdersUiState`

| Name            | Type                   | Default     |
|-----------------|------------------------|-------------|
| standingOrders  | List\<StandingOrder\>  | emptyList() |
| activeCount     | Int                    | 0           |
| selectedOrderId | String                 | ""          |
| uiState         | StandingOrdersUiState  | Loading     |

**Events:** `OrdersLoaded`, `ViewOrderClicked`, `EditOrderClicked`, `DeleteOrderClicked`, `DeleteOrderConfirmed`, `CreateOrderClicked`, `FilterChanged`, `RefreshTriggered`

**Actions:** `view_standing_order`, `edit_standing_order`, `delete_standing_order`, `create_standing_order`, `filter_standing_orders`

**DI Dependencies:** `StandingOrderRepository`, `AccountRepository`

**Errors:**

| Field  | Code          | Message                                        |
|--------|---------------|------------------------------------------------|
| global | LOAD_FAILED   | "Unable to load standing orders. Please try again." |
| delete | DELETE_FAILED | "Could not delete standing order. Please try again." |
| create | CREATE_FAILED | "Could not create standing order. Please try again." |

---

## Navigation

| From            | To                    | Trigger                           | Type |
|-----------------|-----------------------|-----------------------------------|------|
| standing-orders | standing-order-detail | Tap any order card (rent_header_row / rent_amount_row) | push |
| standing-orders | standing-order-edit   | Tap edit icon on any order card   | push |
| standing-orders | (create flow)         | Tap `create_standing_order_fab`   | push |
| standing-orders | (previous screen)     | Back arrow in top app bar         | pop  |

---

## API Endpoints

| Endpoint                                                                    | Auth        | Tag             | Purpose                                                                     |
|-----------------------------------------------------------------------------|-------------|-----------------|-----------------------------------------------------------------------------|
| POST /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/owner/standing-order   | DirectLogin | Standing-Orders | Create a new standing order (OBP is POST-only; list is inferred from transaction history) |

---

## Design Tokens

| Token                          | Value   | Usage                                                                        |
|--------------------------------|---------|------------------------------------------------------------------------------|
| colors.light.primary           | #4C662B | Screen title, active badge + chip text, amount text (active), edit icons, FAB background |
| colors.light.primary_container | #CDEDA3 | Active badge background, active count chip background                        |
| colors.light.error             | #BA1A1A | Delete icon color                                                            |
| colors.light.surface           | #FFFFFF | Active order card background                                                 |
| colors.light.background        | #F9FAEF | Screen background, paused card background, paused badge background           |
| colors.light.surface_variant   | #E1E4D5 | Paused card border color                                                     |
| colors.light.on_surface        | #1A1C16 | Active order title text (Rent Payment, Netflix Subscription)                 |
| colors.light.on_surface_variant| #44483D | Beneficiary text, next-date text, paused title + amount + date text          |
| typography.headline_large      | Outfit 32sp/400 | Screen title "Standing Orders"                                         |
| typography.title_medium        | Outfit 16sp/500 | Order name labels (Rent Payment, Netflix Subscription, Gym Membership) |
| typography.body_large          | Outfit 16sp/400 | Amount + frequency ("£1,200 / month")                                  |
| typography.body_medium         | Outfit 14sp/400 | Beneficiary name ("To: Landlord Holdings Ltd")                         |
| typography.body_small          | Outfit 12sp/400 | Next payment date ("Next: 1 Jun 2026")                                 |
| typography.label_medium        | Outfit 12sp/500 | Count chip "3 active"                                                  |
| typography.label_small         | Outfit 11sp/500 | Status badges "Active" / "Paused"                                      |
| radius.lg                      | 16dp    | Order card radius, FAB radius                                                |
| elevation.level2               | 3dp     | Active order card shadow                                                     |
| elevation.level1               | 1dp     | Paused order card shadow                                                     |
| spacing.md                     | 16dp    | Card internal padding, card margin_bottom, section gaps                      |
| spacing.sm                     | 8dp     | Badge H-padding, action icon padding, action row spacing                     |
| spacing.xs                     | 4dp     | Badge V-padding, beneficiary padding_bottom                                  |
| iconography.icon-sm            | 20dp    | Action icons (edit_outlined, delete_outlined at 22dp — nearest: icon-sm)     |
| motion.duration.short4         | 200ms   | Skeleton shimmer animation duration                                          |

---

_Generated by /idea export | 2026-05-30_
