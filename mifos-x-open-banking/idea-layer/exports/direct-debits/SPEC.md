# SPEC — Direct Debits

| Field         | Value                   |
|---------------|-------------------------|
| Feature       | direct-debits           |
| Flavor        | consumer                |
| Status        | approved                |
| Quality Score | 97                      |
| ViewModel     | DirectDebitsViewModel   |

---

## Overview

The Direct Debits screen is an `index_list` screen listing all recurring payment mandates authorised on the account. A "Direct Debits" headline in `#4C662B` (`Outfit/headline_large`, bold) sits alongside an active-count chip (`#CDEDA3` fill, `Outfit/label_medium`) showing how many mandates are currently running — e.g. "3 active". Each mandate is represented as a card (`#FFFFFF`, 16dp radius, 2dp elevation) showing the payee name, a status pill (green "Active" or grey "Cancelled"), the formatted amount and frequency (e.g. "£15.99 / month"), the next scheduled collection date, and the OBP mandate reference (e.g. "Ref: DD-NF-20240301").

Demo mandates: Netflix (£15.99 / month, Active, next 3 Jun 2026, DD-NF-20240301), Spotify Premium (£10.99 / month, Active, next 12 Jun 2026, DD-SP-20231115), and PureGym (£29.99 / month, Cancelled, DD-GYM-20220601 — muted `#F9FAEF` card styling). A floating "Set Up Direct Debit" FAB (`#4C662B`, 16dp radius) is always visible. Tapping an active mandate's card opens the detail/cancel sheet. A "Cancel Direct Debit?" confirmation dialog guards the destructive cancel action — it shows the mandate merchant and reference, a red "Yes, Cancel Mandate" CTA (`#BA1A1A`), and a "Keep Mandate" outlined dismissal button. Data is loaded from the OBP Direct-Debit endpoints. The screen has 5 states: `loading`, `populated`, `empty`, `cancel_confirm`, and `error`.

---

## Screens

| ID             | Name          | Route           | Layout | Scroll   |
|----------------|---------------|-----------------|--------|----------|
| direct-debits  | Direct Debits | /direct-debits  | Column | Vertical |

**Shell:** Top app bar — title "Direct Debits", navigation icon `arrow_back` (navigates back to accounts), overflow `more_vert` action. No bottom navigation bar on this screen.

---

## Components

| ID                    | Type   | Description                                                                                                      |
|-----------------------|--------|------------------------------------------------------------------------------------------------------------------|
| title_count_row       | stack  | Horizontal row; 12dp spacing; 20dp h-pad, 16dp v-pad; contains screen title + active count chip               |
| direct_debits_title   | text   | "Direct Debits" — Outfit/headline_large, #4C662B, bold; heading role                                           |
| active_count_chip     | box    | "3 active" — #CDEDA3 fill, 12dp radius, 10dp h-pad, 4dp v-pad; Outfit/label_medium, #4C662B, semibold; data-driven from `activeCount` |
| direct_debit_netflix  | box    | Netflix mandate card — #FFFFFF fill, 16dp radius, 2dp elevation, 16dp pad, 20dp h-margin, 12dp bottom-margin; taps navigate to direct-debit-detail |
| netflix_header_row    | stack  | Horizontal, space-between, flex-start align — payee name + status badge                                         |
| netflix_payee         | text   | "Netflix" — Outfit/title_medium, #1A1C16, semibold                                                             |
| netflix_active_badge  | box    | "Active" — #CDEDA3 fill, 10dp radius, 8dp h-pad, 3dp v-pad; Outfit/label_small, #4C662B                       |
| netflix_amount_row    | stack  | Horizontal, space-between, center align, 4dp top-pad — amount string + next-date                               |
| netflix_amount        | text   | "£15.99 / month" — Outfit/body_large, #4C662B, semibold                                                        |
| netflix_next_date     | text   | "Next: 3 Jun 2026" — Outfit/body_small, #44483D                                                                |
| netflix_mandate_ref   | text   | "Ref: DD-NF-20240301" — Outfit/label_small, #44483D                                                            |
| direct_debit_spotify  | box    | Spotify mandate card — same card style as Netflix; Active state                                                 |
| spotify_header_row    | stack  | Horizontal, space-between, flex-start align                                                                     |
| spotify_payee         | text   | "Spotify" — Outfit/title_medium, #1A1C16, semibold                                                             |
| spotify_active_badge  | box    | "Active" — #CDEDA3 fill, 10dp radius; Outfit/label_small, #4C662B                                              |
| spotify_amount_row    | stack  | Horizontal, space-between, 4dp top-pad                                                                          |
| spotify_amount        | text   | "£10.99 / month" — Outfit/body_large, #4C662B, semibold                                                        |
| spotify_next_date     | text   | "Next: 12 Jun 2026" — Outfit/body_small, #44483D                                                               |
| spotify_mandate_ref   | text   | "Ref: DD-SP-20231115" — Outfit/label_small, #44483D                                                            |
| direct_debit_gym      | box    | PureGym mandate card — #F9FAEF fill (muted, cancelled), 16dp radius, 0dp elevation, 1dp #E1E4D5 border         |
| gym_header_row        | stack  | Horizontal, space-between, flex-start align                                                                     |
| gym_payee             | text   | "PureGym" — Outfit/title_medium, #44483D (greyed), semibold                                                    |
| gym_cancelled_badge   | box    | "Cancelled" — #F9FAEF fill, 10dp radius, 8dp h-pad; Outfit/label_small, #44483D                               |
| gym_amount            | text   | "£29.99 / month" — Outfit/body_large, #44483D, normal weight (muted)                                           |
| gym_mandate_ref       | text   | "Ref: DD-GYM-20220601" — Outfit/label_small, #E1E4D5                                                           |
| cancel_confirm_dialog | dialog | Destructive action guard — 20dp radius, #FFFFFF fill, 8dp elevation, 24dp h+v pad; shown in `cancel_confirm` state |
| cancel_dialog_title   | text   | "Cancel Direct Debit?" — Outfit/headline_small, #1A1C16, bold                                                  |
| cancel_dialog_body    | text   | "Netflix (DD-NF-20240301) will stop collecting payments. This cannot be undone." — Outfit/body_medium, #44483D; merchant + ref injected from selected mandate |
| cancel_confirm_cta    | button | "Yes, Cancel Mandate" — filled, #BA1A1A bg, #FFFFFF text, 12dp radius, full-width; triggers OBP cancel + list reload |
| cancel_dismiss_cta    | button | "Keep Mandate" — outlined, #4C662B border + text, 12dp radius, full-width; closes dialog with no side effects  |
| setup_direct_debit_fab| button | "Set Up Direct Debit" — filled FAB, #4C662B, 16dp radius, add icon, elevation 6dp, floating; always visible   |

---

## States

| ID             | Trigger                                   | Description                                                                                                          |
|----------------|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| loading        | Screen entry / RetryLoad                  | Title row visible; 3 skeleton cards (110dp height each, #E1E4D5, 16dp radius) shimmer for 200ms (short4); no chip   |
| populated      | Data load success with ≥1 mandate         | Full list: active count chip + all mandate cards (Netflix, Spotify, PureGym) + FAB                                   |
| empty          | Data load success with 0 mandates         | Title row + empty state: `account_balance_wallet` icon, "No direct debits set up", help copy + FAB                  |
| cancel_confirm | User taps cancel on an active mandate     | `populated` layout + modal overlay (50% scrim) + cancel confirmation dialog with merchant + ref                      |
| error          | Network or auth failure                   | Title row + `cloud_off` icon error state: "Unable to load direct debits", "Check your connection and try again" + Retry button + FAB |

---

## State Model

**ViewModel:** `DirectDebitsViewModel`
**Screen State Type:** `DirectDebitsUiState`

| Name             | Type                    | Default       |
|------------------|-------------------------|---------------|
| directDebits     | List\<DirectDebit\>     | emptyList()   |
| activeCount      | Int                     | 0             |
| uiState          | DirectDebitsUiState     | Loading       |
| selectedMandate  | DirectDebit?            | null          |
| showCancelDialog | Boolean                 | false         |
| error            | UiError?                | null          |

**Events:** `DirectDebitsLoaded`, `ViewDirectDebitClicked`, `SetUpDirectDebitClicked`, `CancelDirectDebitClicked`, `CancelConfirmed`, `CancelDismissed`, `RefreshTriggered`, `RetryLoad`

**Actions:** `view_direct_debit`, `setup_direct_debit`, `confirm_cancel_direct_debit`, `dismiss_cancel_dialog`, `open_direct_debit_options`

**DI Dependencies:** `DirectDebitRepository`, `AccountRepository`

**Errors:**
- `LOAD_FAILED`: "Unable to load direct debits. Please try again."
- `CANCEL_FAILED`: "Could not cancel mandate. Please try again."
- `CREATE_FAILED`: "Could not set up direct debit. Please try again."

---

## Navigation

| From          | To                   | Trigger                                         | Type   |
|---------------|----------------------|-------------------------------------------------|--------|
| direct-debits | direct-debit-detail  | Tap active mandate card (`view_direct_debit`)   | push   |
| direct-debits | direct-debits        | `confirm_cancel_direct_debit` (reload)          | reload |
| direct-debits | accounts             | `navigate_back` (top bar back arrow)            | pop    |
| direct-debits | home                 | `nav_home`                                      | tab    |
| direct-debits | standing-orders      | `nav_standing_orders`                           | push   |
| direct-debits | cards                | `nav_cards`                                     | push   |
| direct-debits | account-detail       | `nav_account_detail`                            | push   |

---

## API Endpoints

| Endpoint                                                                               | Auth        | Tag           | Purpose                                        |
|----------------------------------------------------------------------------------------|-------------|---------------|------------------------------------------------|
| GET /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/owner/direct-debits               | DirectLogin | Direct-Debit  | Retrieve all mandates for the account          |
| POST /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/owner/direct-debit              | DirectLogin | Direct-Debit  | Create a new direct debit mandate              |

---

## Design Tokens

| Token                             | Value           | Usage                                                                          |
|-----------------------------------|-----------------|--------------------------------------------------------------------------------|
| colors.light.primary              | #4C662B         | Screen title, active count chip text, active badge text, active amount text, FAB bg, Keep Mandate border + text |
| colors.light.primary_container    | #CDEDA3         | Active count chip fill, Active status badge fill                               |
| colors.light.error                | #BA1A1A         | "Yes, Cancel Mandate" CTA background                                           |
| colors.light.on_error             | #FFFFFF         | "Yes, Cancel Mandate" CTA text                                                 |
| colors.light.surface              | #FFFFFF         | Active mandate card fill, cancel dialog background                             |
| colors.light.background           | #F9FAEF         | Screen base, Cancelled mandate card fill, Cancelled badge fill                 |
| colors.light.on_surface           | #1A1C16         | Active payee names (Netflix, Spotify), cancel dialog title                     |
| colors.light.on_surface_variant   | #44483D         | Next-date text, mandate ref text (active), cancel dialog body, gym payee text, gym badge text, gym amount |
| colors.light.surface_variant      | #E1E4D5         | Cancelled mandate card border                                                  |
| typography.headline_large         | Outfit 32sp/400 | Screen title "Direct Debits"                                                   |
| typography.headline_small         | Outfit 24sp/600 | Cancel dialog title "Cancel Direct Debit?"                                     |
| typography.title_medium           | Outfit 16sp/500 | Mandate payee names (Netflix, Spotify, PureGym)                                |
| typography.body_large             | Outfit 16sp/400 | Mandate amount strings (£15.99 / month)                                        |
| typography.body_medium            | Outfit 14sp/400 | Cancel dialog body copy                                                        |
| typography.body_small             | Outfit 12sp/400 | Next collection date strings                                                   |
| typography.label_medium           | Outfit 12sp/500 | Active count chip text "3 active"                                              |
| typography.label_small            | Outfit 11sp/500 | Status badge labels ("Active", "Cancelled"), mandate reference strings         |
| radius.md                         | 12dp            | Cancel CTA buttons                                                             |
| radius.lg                         | 16dp            | Active mandate cards, FAB                                                      |
| radius.xl                         | 24dp            | Cancel confirm dialog                                                          |
| elevation.level1                  | 1dp             | Active mandate cards (source specifies 2dp)                                    |
| elevation.level3                  | 6dp             | FAB                                                                            |
| elevation.level4                  | 8dp             | Cancel confirm dialog                                                          |
| motion.duration.short4            | 200ms           | Skeleton shimmer duration on loading state                                     |

---

_Generated by /idea export | 2026-05-30_
