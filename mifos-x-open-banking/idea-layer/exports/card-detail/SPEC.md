# SPEC — Card Detail

| Field         | Value                  |
|---------------|------------------------|
| Feature       | card-detail            |
| Flavor        | consumer               |
| Status        | approved               |
| Quality Score | 93                     |
| ViewModel     | CardDetailViewModel    |

---

## Overview

The Card Detail screen provides full management controls for a single payment card. An enlarged green card visual displays the masked PAN, cardholder name, expiry, and network logo, with a biometric-gated "Show card details" link to reveal the full PAN and CVV. Below the card, a live active/frozen status toggle and a Spending Limits section show daily (£2,500) and monthly (£10,000) limits each with an edit shortcut. Destructive actions — Freeze Card and Report Lost/Stolen — use amber and red outlined buttons respectively. A text button navigates to all transactions for the card.

---

## Screens

| ID          | Name        | Route            | Layout        | Scroll   |
|-------------|-------------|------------------|---------------|----------|
| card-detail | Card Detail | /cards/{cardId}  | detail_screen | Vertical |

**Shell:** Top app bar ("Card Details") with back arrow and more_vert overflow action. No bottom navigation bar.

| Element         | Detail                          |
|-----------------|---------------------------------|
| top_bar.title   | "Card Details"                  |
| navigation_icon | arrow_back                      |
| action          | more_vert → open_card_options_menu |
| bottom_nav      | false                           |

---

## Components

| ID                       | Type    | Description                                                                                                         |
|--------------------------|---------|---------------------------------------------------------------------------------------------------------------------|
| card_visual              | box     | #4C662B gradient card (340×210dp, radius 20, elevation 12, 24dp padding); taps to flip state                       |
| card_number_display      | text    | "•••• •••• •••• 4521" — title_large, #FFFFFF, monospace, letter-spacing 4                                          |
| cardholder_name          | text    | "ALEX JOHNSON" — body_large, #CDEDA3, uppercase, letter-spacing 1                                                  |
| card_expiry              | text    | "09/29" — body_medium, #CDEDA3, monospace                                                                           |
| card_network_logo        | image   | Visa logo, 60×22dp, white tinted, content_scale fit                                                                 |
| reveal_card_details_link | link    | "Show card details" — label_large, #4C662B, underline, center-aligned; triggers biometric auth                     |
| card_status_row          | stack   | Horizontal (space-between) white container (radius 12, elevation 1, 16dp padding) — label + toggle switch          |
| card_status_label        | text    | "Card Active" — body_large, #1A1C16, weight 500                                                                    |
| card_status_switch       | input   | Switch: #4C662B when checked (active), #44483D when unchecked                                                       |
| limits_section           | box     | White container (radius 12, elevation 1, 20dp padding) for spending limits                                         |
| limits_section_title     | text    | "Spending Limits" — title_medium, #1A1C16, weight 600                                                              |
| daily_limit_row          | stack   | Horizontal (space-between, 10dp vertical padding) — label + value + edit icon; tappable                            |
| daily_limit_label        | text    | "Daily limit" — body_medium, #44483D                                                                               |
| daily_limit_value        | text    | "£2,500" — body_large, #1A1C16, weight 500                                                                         |
| daily_limit_edit_icon    | icon    | edit icon, 20dp, #4C662B; triggers edit_limit action                                                               |
| monthly_limit_row        | stack   | Horizontal (space-between, 10dp vertical padding) — label + value + edit icon; tappable                            |
| monthly_limit_label      | text    | "Monthly limit" — body_medium, #44483D                                                                             |
| monthly_limit_value      | text    | "£10,000" — body_large, #1A1C16, weight 500                                                                        |
| monthly_limit_edit_icon  | icon    | edit icon, 20dp, #4C662B; triggers edit_limit action                                                               |
| freeze_card_button       | button  | "Freeze Card" — outlined, #E8A317 border, #44483D text (a11y fix), ac_unit icon, full-width, radius 12            |
| report_lost_button       | button  | "Report Lost/Stolen" — outlined, #BA1A1A border/text, report_problem icon, full-width, radius 12                   |
| view_transactions_button | button  | "View Transactions" — text variant, #4C662B, receipt_long icon, full-width; navigates to transactions              |

---

## States

| ID      | Trigger                                     | Description                                                                                          |
|---------|---------------------------------------------|------------------------------------------------------------------------------------------------------|
| loading | Screen entry                                | Skeleton card visual (340×210dp) + 4 skeleton field rows; no interactive elements                    |
| content | Card data loaded, card is active            | Full card visual, active switch checked, limits section, Freeze + Report buttons, View Transactions  |
| frozen  | Card is frozen (isFrozen: true)             | Card visual shows grey (#C5C8BA80) "FROZEN" overlay; switch unchecked; Freeze → "Unfreeze Card" (#4C662B border/text); reveal_card_details_link hidden |
| error   | API failure (LOAD_FAILED)                   | credit_card_off icon, "Unable to load card details", "Please try again or contact support", retry    |
| empty   | Card record not found                       | credit_card_off icon, "Card information not available", "No card data found", back button            |

---

## State Model

**ViewModel:** `CardDetailViewModel`
**Screen State Type:** `CardDetailUiState`

| Name            | Type             | Default  |
|-----------------|------------------|----------|
| cardId          | String           | ""       |
| cardNumber      | String           | ""       |
| cardholderName  | String           | ""       |
| expiryDate      | String           | ""       |
| cardNetwork     | CardNetwork      | Visa     |
| isActive        | Boolean          | true     |
| isFrozen        | Boolean          | false    |
| dailyLimit      | String           | "£2,500" |
| monthlyLimit    | String           | "£10,000"|
| isRevealed      | Boolean          | false    |
| uiState         | CardDetailUiState| Loading  |

**Events:** `CardLoaded`, `RevealCardDetailsRequested`, `BiometricAuthSucceeded`, `BiometricAuthFailed`, `CardStatusToggled`, `EditLimitClicked`, `FreezeCardClicked`, `ReportLostClicked`, `ViewTransactionsClicked`

**Actions:** `reveal_card_details()`, `toggle_card_status()`, `edit_limit()`, `freeze_card()`, `report_lost()`, `navigate()`, `open_card_options_menu()`

**DI Dependencies:** `CardRepository`, `BiometricAuthUseCase`, `CardLimitRepository`

**Errors:**
- `LOAD_FAILED`: "Unable to load card details. Please try again."
- `FREEZE_FAILED`: "Failed to freeze card. Please contact support."
- `REPORT_FAILED`: "Failed to report card. Please call 0800 123 456."

---

## Navigation

| From        | To           | Trigger                       | Type |
|-------------|--------------|-------------------------------|------|
| card-detail | cards        | Top app bar back arrow        | pop  |
| card-detail | transactions | view_transactions_button tap  | push |

---

## API Endpoints

| Endpoint                                       | Auth        | Tag   | Purpose                             |
|------------------------------------------------|-------------|-------|-------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/cards/{cardId} | DirectLogin | Cards | Load full card details for screen   |

---

## Design Tokens

| Token                           | Value     | Usage                                                               |
|---------------------------------|-----------|--------------------------------------------------------------------|
| colors.light.primary            | #4C662B   | Card visual background, reveal link, edit icons, View Transactions  |
| colors.light.primary_container  | #CDEDA3   | Cardholder name and expiry text on card (semi-transparent feel)    |
| colors.light.on_primary         | #FFFFFF   | Card PAN and full cardholder text                                  |
| colors.light.error              | #BA1A1A   | Report Lost/Stolen button border and text                          |
| colors.light.pending            | #E8A317   | Freeze Card button border                                          |
| colors.light.on_surface         | #1A1C16   | Card Active label, limit values                                    |
| colors.light.on_surface_variant | #44483D   | Limit label text, Freeze button text (a11y fix from #E8A317)       |
| colors.light.surface            | #FFFFFF   | Card status row and limits section background                      |
| colors.light.background         | #F9FAEF   | Screen background                                                  |
| colors.light.outline_variant    | #C5C8BA   | Frozen card overlay color (50% opacity applied client-side)        |
| typography.title_large          | 22sp/400  | Masked PAN on card visual                                          |
| typography.body_large           | 16sp/400  | Cardholder name on card, Card Active label, limit values           |
| typography.body_medium          | 14sp/400  | Limit row labels (Daily limit, Monthly limit)                      |
| typography.label_large          | 14sp/500  | Freeze Card and Report Lost button text, View Transactions         |
| radius.xl                       | 24dp      | Card visual corners (20dp in YAML — close to xl)                   |
| radius.md                       | 12dp      | Card status row, limits section, action button corners             |
| elevation.level5                | 12dp      | Card visual shadow                                                  |
| elevation.level1                | 1dp       | Card status row and limits section shadow                          |

---

_Generated by /idea export | 2026-05-29_
