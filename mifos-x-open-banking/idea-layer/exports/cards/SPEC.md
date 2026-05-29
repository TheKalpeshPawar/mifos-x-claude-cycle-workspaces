# SPEC — My Cards

| Field         | Value            |
|---------------|------------------|
| Feature       | cards            |
| Flavor        | consumer         |
| Status        | approved         |
| Quality Score | 93               |
| ViewModel     | CardsViewModel   |

---

## Overview

The My Cards screen is the central hub for payment card management in the Mifos X Open Banking consumer app. All of the user's cards appear in a horizontally-scrollable carousel with full-bleed card visuals and contextual status chips (Active: #4C662B; Frozen: #C5C8BA). Below the carousel, four quick-action buttons offer Freeze, Set Limit, View PIN, and Report Lost shortcuts without leaving the screen. A chronological card transaction list follows, showing recent spend entries (Netflix £15.99, Tesco £34.56, Uber £12.40, Amazon £67.99, Starbucks £5.85) each navigating to transaction-detail. An "Order New Card" outlined button appears at the bottom for card provisioning.

---

## Screens

| ID    | Name     | Route  | Layout     | Scroll   |
|-------|----------|--------|------------|----------|
| cards | My Cards | /cards | index_list | Vertical |

**Shell:** Bottom navigation bar visible (consumer app-shell). Top app bar ("My Cards") with notifications_outlined action.

| Nav Item | ID           | Icon              | Target     |
|----------|--------------|-------------------|------------|
| Home     | nav_home     | home              | home       |
| Accounts | nav_accounts | account_balance   | accounts   |
| Pay      | nav_pay      | send              | send-money |
| Cards    | nav_cards    | credit_card       | cards      |
| More     | nav_more     | more_horiz        | settings   |

---

## Components

| ID                         | Type   | Description                                                                                                   |
|----------------------------|--------|---------------------------------------------------------------------------------------------------------------|
| cards_title                | text   | "My Cards" — headline_large, #4C662B, role heading                                                            |
| card_carousel              | stack  | Horizontal scroll container (min_item 280dp, 16dp gap, snap start) for card visuals                           |
| card_debit_visa            | box    | #4C662B gradient card (320×200dp, radius 20, elevation 8, 24dp padding); taps → card-detail                  |
| card_debit_number          | text   | "•••• •••• •••• 4521" — title_large, #FFFFFF, monospace, letter-spacing 4                                    |
| card_debit_name            | text   | "Alex Johnson" — body_large, #CDEDA3, uppercase                                                               |
| card_debit_active_chip     | box    | "Active" badge (#4C662B bg, #FFFFFF text, radius 12, 10dp hpad, 4dp vpad, label_small)                        |
| visa_logo_debit            | image  | Visa logo, 56×20dp, white tinted, content_scale fit                                                           |
| card_business_mastercard   | box    | #386663 gradient card (320×200dp, radius 20, elevation 8); taps → card-detail                                 |
| card_business_number       | text   | "•••• •••• •••• 7834" — title_large, #FFFFFF, monospace, letter-spacing 4                                    |
| card_business_frozen_chip  | box    | "Frozen" badge (#C5C8BA bg, #FFFFFF text, radius 12, label_small)                                             |
| mastercard_logo            | image  | Mastercard logo, 48×30dp, content_scale fit                                                                   |
| quick_actions_row          | stack  | Horizontal (evenly spaced) quick action buttons below carousel                                                |
| freeze_unfreeze_action     | button | "Freeze" — text, ac_unit icon, #4C662B icon/text, label_small, vertical orientation                          |
| set_limit_action           | button | "Set Limit" — text, tune icon, #4C662B icon/text, label_small, vertical orientation                          |
| view_pin_action            | button | "View PIN" — text, password icon, #4C662B icon/text, label_small, vertical orientation                       |
| report_lost_action         | button | "Report Lost" — text, report_problem icon, #BA1A1A icon/text, label_small, vertical orientation              |
| card_transactions_header   | text   | "Card Transactions" — title_large, #1A1C16, weight 600, role heading                                          |
| card_tx_netflix            | box    | White card (radius 12, elevation 1) — "Netflix", -£15.99, 20 May 2026; taps → transaction-detail             |
| card_tx_netflix_amount     | text   | "-£15.99" — body_large, #BA1A1A, weight 500                                                                   |
| card_tx_netflix_date       | text   | "20 May 2026" — body_small, #44483D                                                                           |
| card_tx_tesco              | box    | White card — "Tesco Express", -£34.56; taps → transaction-detail                                              |
| card_tx_tesco_amount       | text   | "-£34.56" — body_large, #BA1A1A, weight 500                                                                   |
| card_tx_uber               | box    | White card — "Uber", -£12.40, 18 May 2026; taps → transaction-detail                                         |
| card_tx_uber_amount        | text   | "-£12.40" — body_large, #BA1A1A, weight 500                                                                   |
| card_tx_amazon             | box    | White card — "Amazon.co.uk", -£67.99, 17 May 2026; taps → transaction-detail                                 |
| card_tx_amazon_amount      | text   | "-£67.99" — body_large, #BA1A1A, weight 500                                                                   |
| card_tx_starbucks          | box    | White card — "Starbucks", -£5.85, 17 May 2026; taps → transaction-detail                                     |
| card_tx_starbucks_amount   | text   | "-£5.85" — body_large, #BA1A1A, weight 500                                                                    |
| order_new_card_button      | button | "Order New Card" — outlined, #4C662B border/text, add_card icon, full-width, radius 12                        |

---

## States

| ID      | Trigger                  | Description                                                                                         |
|---------|--------------------------|-----------------------------------------------------------------------------------------------------|
| loading | Screen entry             | Title visible; skeleton carousel + skeleton quick-action row + skeleton list (3 items)              |
| content | API data loaded          | Full carousel, quick actions, 5 transaction rows, order button                                      |
| empty   | No cards returned        | credit_card_off icon, "No cards yet", "Order your first Mifos card to start making payments", order button |
| error   | API failure (LOAD_FAILED)| cloud_off icon, "Unable to load cards", "Check your connection and try again", retry button         |

---

## State Model

**ViewModel:** `CardsViewModel`
**Screen State Type:** `CardsUiState`

| Name             | Type               | Default      |
|------------------|--------------------|--------------|
| cards            | List\<Card\>       | emptyList()  |
| selectedCardId   | String             | ""           |
| cardTransactions | List\<Transaction\>| emptyList()  |
| uiState          | CardsUiState       | Loading      |

**Events:** `CardSelected`, `FreezeCardClicked`, `SetLimitClicked`, `ViewPinClicked`, `ReportLostClicked`, `OrderNewCardClicked`, `TransactionClicked`

**Actions:** `navigate()`, `toggle_freeze_card()`, `open_set_limit_sheet()`, `reveal_pin()`, `report_card_lost()`, `order_card()`

**DI Dependencies:** `CardRepository`, `TransactionRepository`, `BiometricAuthUseCase`

**Errors:**
- `LOAD_FAILED`: "Unable to load your cards. Please try again."
- `FREEZE_FAILED`: "Card freeze operation failed. Please contact support."

---

## Navigation

| From  | To               | Trigger                           | Type |
|-------|------------------|-----------------------------------|------|
| cards | card-detail      | card_debit_visa tap               | push |
| cards | card-detail      | card_business_mastercard tap      | push |
| cards | transaction-detail | Any transaction row tap         | push |
| bottom nav | home        | nav_home tab tap                  | tab  |
| bottom nav | accounts    | nav_accounts tab tap              | tab  |
| bottom nav | send-money  | nav_pay tab tap                   | tab  |
| bottom nav | settings    | nav_more tab tap                  | tab  |

---

## API Endpoints

| Endpoint                  | Auth        | Tag   | Purpose                                         |
|---------------------------|-------------|-------|-------------------------------------------------|
| GET /obp/v5.1.0/cards     | DirectLogin | Cards | Fetch all user payment cards for carousel       |

---

## Design Tokens

| Token                           | Value     | Usage                                                              |
|---------------------------------|-----------|--------------------------------------------------------------------|
| colors.light.primary            | #4C662B   | Screen title, debit Visa card gradient, Active chip, action icons, Order New Card border |
| colors.light.secondary          | #386663   | Business Mastercard card gradient                                  |
| colors.light.primary_container  | #CDEDA3   | Cardholder name text on Debit Visa card                            |
| colors.light.on_primary         | #FFFFFF   | PAN text, Active chip text, Visa logo tint                         |
| colors.light.error              | #BA1A1A   | All debit transaction amounts, Report Lost action icon/text        |
| colors.light.outline_variant    | #C5C8BA   | Frozen badge background                                            |
| colors.light.on_surface         | #1A1C16   | "Card Transactions" section heading                                |
| colors.light.on_surface_variant | #44483D   | Transaction date text                                              |
| colors.light.surface            | #FFFFFF   | Transaction card backgrounds                                       |
| colors.light.background         | #F9FAEF   | Screen background                                                  |
| typography.headline_large       | 32sp/400  | "My Cards" screen title                                            |
| typography.title_large          | 22sp/400  | Section heading "Card Transactions", PAN on card                   |
| typography.body_large           | 16sp/400  | Transaction merchant names, debit amounts, cardholder name         |
| typography.body_small           | 12sp/400  | Transaction dates                                                  |
| typography.label_small          | 11sp/500  | Card status chip text, quick-action button labels                  |
| radius.xl                       | 24dp      | Card visual corners (20dp in YAML)                                 |
| radius.md                       | 12dp      | Transaction card corners, status chip corners, order button corners|
| elevation.level3                | 6dp       | Card visual elevation (8dp in YAML)                                |
| elevation.level1                | 1dp       | Transaction row card elevation                                     |

---

_Generated by /idea export | 2026-05-29_
