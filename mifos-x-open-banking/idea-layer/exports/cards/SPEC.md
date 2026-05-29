# SPEC — My Cards

| Field         | Value          |
|---------------|----------------|
| Feature       | cards          |
| Flavor        | consumer       |
| Status        | approved       |
| Quality Score | 93             |
| ViewModel     | CardsViewModel |

---

## Overview

My Cards is the card management hub for Consumer persona users. It displays a horizontally scrollable carousel of payment cards — each rendered as a branded card chip (320×200dp, 20dp radius, elevation 8) showing the masked card number, cardholder name, network logo (Visa / Mastercard), and a status chip (Active / Frozen). Below the carousel, four quick action buttons (Freeze, Set Limit, View PIN, Report Lost) provide inline card controls without navigating away. A Card Transactions section lists the five most recent card-linked transactions (Netflix −£15.99, Tesco Express −£34.56, Uber −£12.40, Amazon.co.uk −£67.99, Starbucks −£5.85), each tappable to transaction-detail. An "Order New Card" outlined button anchors the foot of the scroll. The screen uses the 5-tab bottom navigation bar with Cards active. Card data is fetched from `GET /obp/v5.1.0/cards` on screen entry and on retry. The demo data profile is three Kenyan open-banking cards: KCB Visa Classic Debit, Equity Mastercard Gold Credit, and Co-op Visa Debit (disabled).

---

## Screens

| ID    | Name     | Route  | Layout | Scroll   |
|-------|----------|--------|--------|----------|
| cards | My Cards | /cards | Column | Vertical |

**Shell:** Top app bar (title "My Cards", navigation_icon null, actions: notifications_outlined → open_notifications) + bottom navigation bar (5 tabs, Cards active by default).

| Nav Item | ID           | Icon            | Target     | Active |
|----------|--------------|-----------------|------------|--------|
| Home     | nav_home     | home            | home       | false  |
| Accounts | nav_accounts | account_balance | accounts   | false  |
| Pay      | nav_pay      | send            | send-money | false  |
| Cards    | nav_cards    | credit_card     | cards      | true   |
| More     | nav_more     | more_horiz      | settings   | false  |

---

## Components

| ID                        | Type   | Description                                                                                                              |
|---------------------------|--------|--------------------------------------------------------------------------------------------------------------------------|
| cards_title               | text   | "My Cards" — Outfit/headline_large (32sp), #4C662B, 4dp bottom padding, heading role                                    |
| card_carousel             | stack  | Horizontal scroll container — 16dp item spacing, 8dp vertical/4dp horizontal padding, min-item 280dp, snap-start        |
| card_debit_visa           | box    | Mifos Debit Visa — #4C662B diagonal gradient, 20dp radius, elevation 8, 320×200dp, 24dp padding; tap → card-detail      |
| card_debit_number         | text   | "•••• •••• •••• 4521" — Outfit/title_large, #FFFFFF, monospace, 4dp letter-spacing                                     |
| card_debit_name           | text   | "Alex Johnson" — Outfit/body_large, #CDEDA3, uppercase transform                                                        |
| card_debit_active_chip    | box    | "Active" status chip — #4C662B fill, 12dp radius, 10dp horizontal/4dp vertical padding, #FFFFFF/label_small text        |
| visa_logo_debit           | image  | Visa network logo — 56×20dp, fit, #FFFFFF tint                                                                          |
| card_business_mastercard  | box    | Mifos Business Mastercard — #386663 diagonal gradient, 20dp radius, elevation 8, 320×200dp, 24dp padding; tap → card-detail |
| card_business_number      | text   | "•••• •••• •••• 7834" — Outfit/title_large, #FFFFFF, monospace, 4dp letter-spacing                                     |
| card_business_frozen_chip | box    | "Frozen" status chip — #C5C8BA fill, 12dp radius, 10dp horizontal/4dp vertical padding, #FFFFFF/label_small text        |
| mastercard_logo           | image  | Mastercard network logo — 48×30dp, fit                                                                                   |
| quick_actions_row         | stack  | Horizontal, space-evenly justify, 20dp top/8dp bottom padding — 4 quick action buttons                                  |
| freeze_unfreeze_action    | button | "Freeze" — text variant, ac_unit icon #4C662B, #4C662B text, vertical layout, 8dp padding, label_small                 |
| set_limit_action          | button | "Set Limit" — text variant, tune icon #4C662B, #4C662B text, vertical layout, 8dp padding, label_small                 |
| view_pin_action           | button | "View PIN" — text variant, password icon #4C662B, #4C662B text, vertical layout, 8dp padding; requires biometric auth  |
| report_lost_action        | button | "Report Lost" — text variant, report_problem icon #BA1A1A, #BA1A1A text, vertical layout, 8dp padding                  |
| card_transactions_header  | text   | "Card Transactions" — Outfit/title_large, #1A1C16, weight 600, 20dp top/8dp bottom padding, heading role               |
| card_tx_netflix           | box    | Netflix transaction row — #FFFFFF fill, 12dp radius, elevation 1, 16dp horizontal/14dp vertical padding, 1dp #F9FAEF border; tap → transaction-detail |
| card_tx_netflix_amount    | text   | "−£15.99" — Outfit/body_large, #BA1A1A, weight 500                                                                     |
| card_tx_netflix_date      | text   | "20 May 2026" — Outfit/body_small, #44483D                                                                              |
| card_tx_tesco             | box    | Tesco Express transaction row — #FFFFFF, 12dp radius, elevation 1, 16dp/14dp padding; tap → transaction-detail          |
| card_tx_tesco_amount      | text   | "−£34.56" — Outfit/body_large, #BA1A1A, weight 500                                                                     |
| card_tx_uber              | box    | Uber transaction row — #FFFFFF, 12dp radius, elevation 1, 16dp/14dp padding; tap → transaction-detail                   |
| card_tx_uber_amount       | text   | "−£12.40" — Outfit/body_large, #BA1A1A, weight 500                                                                     |
| card_tx_amazon            | box    | Amazon.co.uk transaction row — #FFFFFF, 12dp radius, elevation 1, 16dp/14dp padding; tap → transaction-detail           |
| card_tx_amazon_amount     | text   | "−£67.99" — Outfit/body_large, #BA1A1A, weight 500                                                                     |
| card_tx_starbucks         | box    | Starbucks transaction row — #FFFFFF, 12dp radius, elevation 1, 16dp/14dp padding; tap → transaction-detail              |
| card_tx_starbucks_amount  | text   | "−£5.85" — Outfit/body_large, #BA1A1A, weight 500                                                                      |
| order_new_card_button     | button | "Order New Card" — outlined, #4C662B border + text, 12dp radius, 14dp vertical padding, full-width, add_card icon, label_large |

---

## States

| ID      | Trigger                      | Description                                                                                                      |
|---------|------------------------------|------------------------------------------------------------------------------------------------------------------|
| loading | Screen entry / RetryLoad     | cards_title visible; carousel, quick actions, and transaction list replaced by skeleton shimmer (short4=200ms duration, static placeholder for reduced motion; skeleton_count: 3) |
| content | Data load success            | Full carousel (2 cards) + quick actions row + 5 transaction rows + Order New Card button all visible             |
| empty   | GET /cards returns zero items| cards_title + credit_card_off empty state icon + "No cards yet" title + "Order your first Mifos card to start making payments" message + Order New Card CTA |
| error   | Network or auth failure      | cards_title + cloud_off error icon + "Unable to load cards" title + "Check your connection and try again" message + Retry button |

---

## State Model

**ViewModel:** `CardsViewModel`
**Screen State Type:** `CardsUiState`

| Name             | Type                | Default     |
|------------------|---------------------|-------------|
| cards            | List\<Card\>        | emptyList() |
| selectedCardId   | String              | ""          |
| cardTransactions | List\<Transaction\> | emptyList() |
| uiState          | CardsUiState        | Loading     |

**Events:** `CardSelected`, `FreezeCardClicked`, `SetLimitClicked`, `ViewPinClicked`, `ReportLostClicked`, `OrderNewCardClicked`, `TransactionClicked`

**Actions:** `navigate`, `toggle_freeze_card`, `open_set_limit_sheet`, `reveal_pin`, `report_card_lost`, `order_card`

**DI Dependencies:** `CardRepository`, `TransactionRepository`, `BiometricAuthUseCase`

**Errors:**
- `global / LOAD_FAILED`: "Unable to load your cards. Please try again."
- `freeze / FREEZE_FAILED`: "Card freeze operation failed. Please contact support."

---

## Navigation

| From  | To                 | Trigger                              | Type |
|-------|--------------------|--------------------------------------|------|
| cards | card-detail        | card_debit_visa tap                  | push |
| cards | card-detail        | card_business_mastercard tap         | push |
| cards | transaction-detail | card_tx_netflix tap                  | push |
| cards | transaction-detail | card_tx_tesco tap                    | push |
| cards | transaction-detail | card_tx_uber tap                     | push |
| cards | transaction-detail | card_tx_amazon tap                   | push |
| cards | transaction-detail | card_tx_starbucks tap                | push |
| cards | home               | nav_home bottom tab tap              | tab  |
| cards | accounts           | nav_accounts bottom tab tap          | tab  |
| cards | send-money         | nav_pay bottom tab tap               | tab  |
| cards | settings           | nav_more bottom tab tap              | tab  |

**Flows:** consumer-banking
**Journey:** consumer-cards-financing

---

## API Endpoints

| Endpoint                | Auth        | Tag   | Purpose                                    |
|-------------------------|-------------|-------|--------------------------------------------|
| GET /obp/v5.1.0/cards   | DirectLogin | Cards | Fetch all payment cards for the current user |

---

## Design Tokens

| Token                           | Value           | Usage                                                                                             |
|---------------------------------|-----------------|---------------------------------------------------------------------------------------------------|
| colors.light.primary            | #4C662B         | cards_title, Visa card gradient, Active chip fill, freeze/limit/pin icon+text                    |
| colors.light.primary_container  | #CDEDA3         | Cardholder name text on Visa card (on-card secondary text)                                        |
| colors.light.secondary          | #386663         | Mastercard gradient fill                                                                          |
| colors.light.outline_variant    | #C5C8BA         | Frozen status chip fill                                                                           |
| colors.light.error              | #BA1A1A         | All debit amounts (−£15.99, −£34.56, −£12.40, −£67.99, −£5.85), Report Lost icon+text           |
| colors.light.surface            | #FFFFFF         | Transaction row fill                                                                              |
| colors.light.background         | #F9FAEF         | Screen base, transaction row border                                                               |
| colors.light.on_surface         | #1A1C16         | card_transactions_header                                                                          |
| colors.light.on_surface_variant | #44483D         | Transaction date lines                                                                            |
| typography.headline_large       | Outfit 32sp/400 | cards_title                                                                                       |
| typography.title_large          | Outfit 22sp/400 | Masked card numbers on chip face, card_transactions_header                                        |
| typography.body_large           | Outfit 16sp/400 | Transaction amounts, cardholder name (ALEX JOHNSON)                                               |
| typography.body_small           | Outfit 12sp/400 | Transaction date lines                                                                            |
| typography.label_large          | Outfit 14sp/500 | Order New Card button label                                                                       |
| typography.label_small          | Outfit 11sp/500 | Status chips (Active / Frozen), quick action button labels                                        |
| radius.md                       | 12dp            | Transaction rows, status chips, Order New Card button                                             |
| radius.xl                       | 24dp            | Payment card chips (source: 20dp, nearest token xl=24)                                           |
| elevation.level4                | 8dp             | Payment card chips                                                                                |
| elevation.level1                | 1dp             | Transaction rows                                                                                  |
| motion.duration.short4          | 200ms           | Skeleton shimmer (loading state)                                                                  |
| touchTargets.min_touch_target   | 48dp            | Quick action buttons (vertical layout, 8dp padding minimum)                                       |

---

_Generated by /idea export | 2026-05-30_
