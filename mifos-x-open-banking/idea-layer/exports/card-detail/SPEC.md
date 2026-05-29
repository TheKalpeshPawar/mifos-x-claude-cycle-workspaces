# SPEC — Card Detail

| Field         | Value               |
|---------------|---------------------|
| Feature       | card-detail         |
| Flavor        | consumer            |
| Status        | designed            |
| Quality Score | 93                  |
| ViewModel     | CardDetailViewModel |

---

## Overview

The Card Detail screen provides full management controls for a single payment card in the Mifos X Open Banking consumer app. A 340×210dp earth-green (#4C662B diagonal gradient) card visual is presented at the top, showing the masked PAN ("•••• •••• •••• 4521"), cardholder name ("ALEX JOHNSON"), expiry date ("09/29"), and Visa network logo — all in white or #CDEDA3. A biometric-gated "Show card details" link allows the user to reveal the full PAN and CVV. Below the card visual, a white surface row shows the card's live active status with a toggleable switch. A Spending Limits section presents editable daily (£2,500) and monthly (£10,000) limits in a white container, each row having an edit icon. At the base of the scrollable column, three action buttons handle card management: "Freeze Card" (amber outlined, reversible), "Report Lost/Stolen" (red outlined, destructive), and "View Transactions" (text, navigates to the transactions screen). In the frozen state, the card visual shows a "#C5C8BA80" "FROZEN" overlay and the freeze button switches to "Unfreeze Card". Demo data: KCB Visa Classic Debit Card for JOHN K MWANGI (card ending 3421, expiry 2028-05-31).

---

## Screens

| ID          | Name        | Route           | Layout       | Scroll   |
|-------------|-------------|-----------------|--------------|----------|
| card-detail | Card Detail | /cards/{cardId} | detail_screen| Vertical |

**Shell:** Top app bar ("Card Details") with arrow_back navigation icon and more_vert overflow action. No bottom navigation bar.

| Element         | Detail                               |
|-----------------|--------------------------------------|
| top_bar.title   | "Card Details"                       |
| navigation_icon | arrow_back                           |
| action          | more_vert → open_card_options_menu   |
| bottom_nav      | false                                |

---

## Components

| ID                       | Type  | Description                                                                                                            |
|--------------------------|-------|------------------------------------------------------------------------------------------------------------------------|
| card_visual              | box   | #4C662B diagonal gradient, 340×210dp, border_radius 20dp, elevation 12dp, 24dp padding, auto horizontal margin; taps to trigger card_flip action |
| card_number_display      | text  | "•••• •••• •••• 4521" — title_large (22sp/400), #FFFFFF, monospace, letter_spacing 4                                  |
| cardholder_name          | text  | "ALEX JOHNSON" — body_large (16sp/400), #CDEDA3, uppercase, letter_spacing 1                                           |
| card_expiry              | text  | "09/29" — body_medium (14sp/400), #CDEDA3, monospace                                                                  |
| card_network_logo        | image | Visa logo, 60×22dp, #FFFFFF tint, content_scale fit                                                                   |
| reveal_card_details_link | link  | "Show card details" — label_large (14sp/500), #4C662B, underline, center-aligned; triggers biometric auth reveal       |
| card_status_row          | stack | Horizontal, space-between, center-aligned; white surface (radius 12dp, elevation 1dp, 16dp vertical × 20dp horizontal padding) |
| card_status_label        | text  | "Card Active" — body_large (16sp/400), #1A1C16, weight 500                                                             |
| card_status_switch       | input | Switch variant; checked: #4C662B (active), unchecked: #44483D; triggers toggle_card_status                             |
| limits_section           | box   | White surface container, radius 12dp, elevation 1dp, 20dp horizontal × 16dp vertical padding, #F9FAEF border           |
| limits_section_title     | text  | "Spending Limits" — title_medium (16sp/500), #1A1C16, weight 600                                                       |
| daily_limit_row          | stack | Horizontal, space-between, center-aligned, 10dp vertical padding; tappable — edit_limit action                         |
| daily_limit_label        | text  | "Daily limit" — body_medium (14sp/400), #44483D                                                                        |
| daily_limit_value        | text  | "£2,500" — body_large (16sp/400), #1A1C16, weight 500                                                                  |
| daily_limit_edit_icon    | icon  | edit icon, 20dp, #4C662B; triggers edit_limit                                                                          |
| limits_divider           | divider | #F9FAEF, 1dp thickness                                                                                               |
| monthly_limit_row        | stack | Horizontal, space-between, center-aligned, 10dp vertical padding; tappable — edit_limit action                         |
| monthly_limit_label      | text  | "Monthly limit" — body_medium (14sp/400), #44483D                                                                      |
| monthly_limit_value      | text  | "£10,000" — body_large (16sp/400), #1A1C16, weight 500                                                                 |
| monthly_limit_edit_icon  | icon  | edit icon, 20dp, #4C662B; triggers edit_limit                                                                          |
| freeze_card_button       | button | "Freeze Card" — outlined, #E8A317 border, #44483D text (a11y fix: 8.91:1 contrast vs. original #E8A317 2.17:1 FAIL), ac_unit leading icon, full-width, radius 12dp |
| report_lost_button       | button | "Report Lost/Stolen" — outlined, #BA1A1A border + text, report_problem leading icon, full-width, radius 12dp           |
| view_transactions_button | button | "View Transactions" — text variant, #4C662B, receipt_long leading icon, full-width, radius 12dp; navigates to transactions |

---

## States

| ID      | Trigger                              | Description                                                                                                                                  |
|---------|--------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| loading | Screen entry                         | Shimmer skeleton for card visual (340×210dp) + 4 skeleton field placeholders; all interactive components hidden; shimmer_duration: short4 (200ms) |
| content | Card data loaded, card is active     | Full card visual, reveal link visible, switch checked (active), full limits section, Freeze Card + Report Lost + View Transactions buttons     |
| frozen  | isFrozen: true                       | Card visual has #C5C8BA80 "FROZEN" overlay; switch unchecked; reveal link hidden; Freeze button → "Unfreeze Card" (#4C662B border + text, lock_open icon); limits rows hidden |
| error   | LOAD_FAILED API error                | credit_card_off icon, "Unable to load card details", "Please try again or contact support", retry button                                     |
| empty   | Card record not found / cancelled    | credit_card_off icon, "Card information not available", "No card data was found. The card may have been cancelled or removed from your account.", back button |

---

## State Model

**ViewModel:** `CardDetailViewModel`
**Screen State Type:** `CardDetailUiState`

| Name           | Type              | Default   |
|----------------|-------------------|-----------|
| cardId         | String            | ""        |
| cardNumber     | String            | ""        |
| cardholderName | String            | ""        |
| expiryDate     | String            | ""        |
| cardNetwork    | CardNetwork       | Visa      |
| isActive       | Boolean           | true      |
| isFrozen       | Boolean           | false     |
| dailyLimit     | String            | "£2,500"  |
| monthlyLimit   | String            | "£10,000" |
| isRevealed     | Boolean           | false     |
| uiState        | CardDetailUiState | Loading   |

**Events:** `CardLoaded`, `RevealCardDetailsRequested`, `BiometricAuthSucceeded`, `BiometricAuthFailed`, `CardStatusToggled`, `EditLimitClicked`, `FreezeCardClicked`, `ReportLostClicked`, `ViewTransactionsClicked`

**Actions:** `reveal_card_details()`, `toggle_card_status()`, `edit_limit()`, `freeze_card()`, `report_lost()`, `navigate(target)`, `open_card_options_menu()`

**DI Dependencies:** `CardRepository`, `BiometricAuthUseCase`, `CardLimitRepository`

**Errors:**
- `LOAD_FAILED`: "Unable to load card details. Please try again."
- `FREEZE_FAILED`: "Failed to freeze card. Please contact support."
- `REPORT_FAILED`: "Failed to report card. Please call 0800 123 456."

---

## Navigation

| From        | To           | Trigger                           | Type |
|-------------|--------------|-----------------------------------|------|
| card-detail | cards        | Top app bar arrow_back press      | pop  |
| card-detail | transactions | view_transactions_button tap      | push |

---

## API Endpoints

| Endpoint                                       | Auth        | Tag   | Purpose                           |
|------------------------------------------------|-------------|-------|-----------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/cards/{cardId} | DirectLogin | Cards | Load full card details for screen |

---

## Design Tokens

| Token                           | Value      | Usage                                                                        |
|---------------------------------|------------|------------------------------------------------------------------------------|
| colors.light.primary            | #4C662B    | Card visual gradient, reveal link color, edit icons, View Transactions text  |
| colors.light.primary_container  | #CDEDA3    | Cardholder name + expiry text on card, Unfreeze button border + text         |
| colors.light.on_primary         | #FFFFFF    | Masked PAN text on card, Visa logo tint                                      |
| colors.light.error              | #BA1A1A    | Report Lost/Stolen button border and text                                    |
| colors.light.pending            | #E8A317    | Freeze Card button border                                                    |
| colors.light.on_surface         | #1A1C16    | "Card Active" label, limit values (£2,500 / £10,000), top bar title          |
| colors.light.on_surface_variant | #44483D    | Limit row labels ("Daily limit", "Monthly limit"), Freeze button text (a11y) |
| colors.light.surface            | #FFFFFF    | Card status row background, limits section background                        |
| colors.light.background         | #F9FAEF    | Screen background, limits section border                                     |
| colors.light.outline_variant    | #C5C8BA    | Frozen card overlay (#C5C8BA at 50% opacity — #C5C8BA80)                    |
| typography.title_large          | Outfit 22sp/400 | Masked PAN on card visual                                               |
| typography.title_medium         | Outfit 16sp/500 | "Spending Limits" section header                                        |
| typography.body_large           | Outfit 16sp/400 | Cardholder name on card, "Card Active" label, daily/monthly limit values |
| typography.body_medium          | Outfit 14sp/400 | Card expiry, limit row label text                                       |
| typography.label_large          | Outfit 14sp/500 | "Show card details" link, action button text                            |
| radius.xl                       | 24dp       | Card visual border (20dp in source — closest token; codegen uses explicit 20) |
| radius.md                       | 12dp       | Card status row, limits section, action button corner radius                 |
| elevation.level5                | 12dp       | Card visual drop shadow                                                      |
| elevation.level1                | 1dp        | Card status row and limits section shadow                                    |
| motion.duration.short4          | 200ms      | Skeleton shimmer duration in loading state                                   |

---

_Generated by /idea export | 2026-05-30_
