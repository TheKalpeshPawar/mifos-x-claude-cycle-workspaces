# SPEC — Direct Debits

| Field         | Value                    |
|---------------|--------------------------|
| Feature       | direct-debits            |
| Flavor        | consumer                 |
| Status        | approved                 |
| Quality Score | 97                       |
| ViewModel     | DirectDebitsViewModel    |

---

## Overview

The Direct Debits screen is the central mandate management surface for Consumer persona users. It lists all active and cancelled direct debit mandates set up against the user's primary account — Netflix (£15.99/month), Spotify (£10.99/month), and a cancelled PureGym membership (£29.99/month). Each mandate card shows merchant name, status badge, amount with frequency, next collection date, and OBP mandate reference. An active count chip ("3 active") sits beside the screen title. A floating action button lets users set up new mandates. Tapping a card navigates to the detail screen. A confirmation dialog guards the destructive cancel action with a scrim overlay. Data is fetched from OBP Direct-Debit endpoints on screen entry and on retry.

---

## Screens

| ID            | Name          | Route           | Layout | Scroll   |
|---------------|---------------|-----------------|--------|----------|
| direct-debits | Direct Debits | /direct-debits  | Column | Vertical |

**Shell:** Top app bar ("Direct Debits") with back arrow and overflow menu. No bottom navigation bar.

| Shell Element        | Type | Value                                    |
|----------------------|------|------------------------------------------|
| Top app bar title    | text | "Direct Debits"                          |
| Navigation icon      | icon | arrow_back → navigate_back               |
| Overflow action      | icon | more_vert → open_direct_debit_options    |

---

## Components

| ID                      | Type    | Description                                                                                                         |
|-------------------------|---------|---------------------------------------------------------------------------------------------------------------------|
| title_count_row         | stack   | Horizontal row containing screen title + active count chip; 20dp horizontal padding, 16dp vertical padding         |
| direct_debits_title     | text    | "Direct Debits" — Outfit/headline_large, #4C662B, bold                                                             |
| active_count_chip       | box     | "3 active" — #CDEDA3 fill, #4C662B text, 12dp radius, 10dp horizontal pad, Outfit/label_medium semibold            |
| direct_debit_netflix    | box     | Netflix mandate card — #FFFFFF fill, 16dp radius, 2dp elevation, 20dp horizontal margin, 12dp bottom margin        |
| netflix_header_row      | stack   | Horizontal row: merchant name (left) + status badge (right)                                                        |
| netflix_payee           | text    | "Netflix" — Outfit/title_medium, #1A1C16, semibold                                                                 |
| netflix_active_badge    | box     | "Active" — #CDEDA3 fill, #4C662B text, 10dp radius, Outfit/label_small                                             |
| netflix_amount_row      | stack   | Horizontal row: amount (left) + next date (right)                                                                  |
| netflix_amount          | text    | "£15.99 / month" — Outfit/body_large, #4C662B, semibold                                                            |
| netflix_next_date       | text    | "Next: 3 Jun 2026" — Outfit/body_small, #44483D                                                                    |
| netflix_mandate_ref     | text    | "Ref: DD-NF-20240301" — Outfit/label_small, #44483D                                                                |
| direct_debit_spotify    | box     | Spotify mandate card — #FFFFFF fill, 16dp radius, 2dp elevation, 20dp horizontal margin                            |
| spotify_header_row      | stack   | Horizontal row: merchant name + status badge                                                                       |
| spotify_payee           | text    | "Spotify" — Outfit/title_medium, #1A1C16, semibold                                                                 |
| spotify_active_badge    | box     | "Active" — #CDEDA3 fill, #4C662B text, Outfit/label_small                                                          |
| spotify_amount_row      | stack   | Horizontal row: amount + next date                                                                                 |
| spotify_amount          | text    | "£10.99 / month" — Outfit/body_large, #4C662B, semibold                                                            |
| spotify_next_date       | text    | "Next: 12 Jun 2026" — Outfit/body_small, #44483D                                                                   |
| spotify_mandate_ref     | text    | "Ref: DD-SP-20231115" — Outfit/label_small, #44483D                                                                |
| direct_debit_gym        | box     | PureGym cancelled mandate — #F9FAEF fill, #E1E4D5 border, 16dp radius, 0dp elevation — muted styling              |
| gym_header_row          | stack   | Horizontal row: merchant name + cancelled badge                                                                    |
| gym_payee               | text    | "PureGym" — Outfit/title_medium, #44483D semibold (greyed out for cancelled state)                                 |
| gym_cancelled_badge     | box     | "Cancelled" — #F9FAEF fill, #44483D text, 10dp radius, Outfit/label_small                                          |
| gym_amount              | text    | "£29.99 / month" — Outfit/body_large, #44483D, normal weight (muted)                                               |
| gym_mandate_ref         | text    | "Ref: DD-GYM-20220601" — Outfit/label_small, #E1E4D5                                                               |
| cancel_confirm_dialog   | dialog  | Modal — #FFFFFF fill, 20dp radius, 8dp elevation, 24dp padding; keyboard: Escape closes                           |
| cancel_dialog_title     | text    | "Cancel Direct Debit?" — Outfit/headline_small, #1A1C16, bold                                                      |
| cancel_dialog_body      | text    | "Netflix (DD-NF-20240301) will stop collecting payments. This cannot be undone." — Outfit/body_medium, #44483D     |
| cancel_confirm_cta      | button  | "Yes, Cancel Mandate" — filled, #BA1A1A fill, #FFFFFF text, 12dp radius, full width                               |
| cancel_dismiss_cta      | button  | "Keep Mandate" — outlined, #4C662B border + text, 12dp radius, full width                                          |
| setup_direct_debit_fab  | button  | "Set Up Direct Debit" — FAB, #4C662B fill, add leading icon, 16dp radius, 6dp elevation, floating                 |

---

## States

| ID             | Trigger                              | Description                                                                                |
|----------------|--------------------------------------|--------------------------------------------------------------------------------------------|
| loading        | Screen entry / RetryLoad             | Title row visible; 3 skeleton cards (height 110dp each) shimmer in mandate list            |
| populated      | API returns mandates                 | All 3 mandate cards (Netflix, Spotify, PureGym) + active count chip + FAB visible         |
| empty          | API returns empty mandate list       | Title + FAB + empty state (wallet icon, "No direct debits set up", setup instruction copy)|
| cancel_confirm | User triggers cancel action          | Full mandate list behind 50% alpha scrim overlay + cancel confirmation dialog              |
| error          | Network or auth failure              | Title + FAB + error state (cloud_off icon, "Unable to load direct debits", retry button)  |

---

## State Model

**ViewModel:** `DirectDebitsViewModel`
**Screen State Type:** `DirectDebitsUiState`

| Name              | Type                    | Default        |
|-------------------|-------------------------|----------------|
| directDebits      | List\<DirectDebit\>     | emptyList()    |
| activeCount       | Int                     | 0              |
| uiState           | DirectDebitsUiState     | Loading        |
| selectedMandate   | DirectDebit?            | null           |
| showCancelDialog  | Boolean                 | false          |
| error             | UiError?                | null           |

**Events:** `DirectDebitsLoaded`, `ViewDirectDebitClicked`, `SetUpDirectDebitClicked`, `CancelDirectDebitClicked`, `CancelConfirmed`, `CancelDismissed`, `RefreshTriggered`, `RetryLoad`

**Actions:** `view_direct_debit`, `setup_direct_debit`, `confirm_cancel_direct_debit`, `dismiss_cancel_dialog`, `open_direct_debit_options`

**DI Dependencies:** `DirectDebitRepository`, `AccountRepository`

**Errors:**
- `LOAD_FAILED`: "Unable to load direct debits. Please try again."
- `CANCEL_FAILED`: "Could not cancel mandate. Please try again."
- `CREATE_FAILED`: "Could not set up direct debit. Please try again."

---

## Navigation

| From          | To                  | Trigger                              | Type    |
|---------------|---------------------|--------------------------------------|---------|
| direct-debits | direct-debit-detail | Mandate card tap (any of 3)          | push    |
| direct-debits | direct-debits       | cancel_confirm_cta tap (mandate cancelled + reload) | replace |
| direct-debits | accounts            | navigate_back (top app bar arrow)    | pop     |
| direct-debits | standing-orders     | nav_standing_orders                  | push    |
| direct-debits | cards               | nav_cards                            | push    |
| direct-debits | account-detail      | nav_account_detail                   | push    |
| direct-debits | home                | nav_home                             | push    |

---

## API Endpoints

| Endpoint                                                                              | Auth        | Tag          | Purpose                                    |
|---------------------------------------------------------------------------------------|-------------|--------------|--------------------------------------------|
| GET /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/owner/direct-debits              | DirectLogin | Direct-Debit | Retrieve all mandates for the account      |
| POST /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/owner/direct-debit              | DirectLogin | Direct-Debit | Create a new direct debit mandate          |

---

## Design Tokens

| Token                              | Value     | Usage                                                               |
|------------------------------------|-----------|---------------------------------------------------------------------|
| colors.light.primary               | #4C662B   | Title text, active badge text, active amounts, FAB fill, dismiss CTA|
| colors.light.primary_container     | #CDEDA3   | Active count chip fill, active status badge fill                    |
| colors.light.background            | #F9FAEF   | Screen base, cancelled card fill, cancelled badge fill              |
| colors.light.surface               | #FFFFFF   | Active mandate card fill, cancel dialog fill                        |
| colors.light.surface_variant       | #E1E4D5   | Cancelled card border, cancelled mandate ref text color             |
| colors.light.on_surface            | #1A1C16   | Active payee names, dialog title                                    |
| colors.light.on_surface_variant    | #44483D   | Next-date text, mandate refs, cancelled payee, cancelled amount     |
| colors.light.error                 | #BA1A1A   | Cancel confirm CTA background                                       |
| colors.light.on_error              | #FFFFFF   | Cancel confirm CTA text                                             |
| typography.headline_large          | Outfit 32sp | Screen title                                                      |
| typography.headline_small          | Outfit 24sp/600 | Cancel dialog title                                           |
| typography.title_medium            | Outfit 16sp/500 | Mandate merchant names                                        |
| typography.body_large              | Outfit 16sp/400 | Mandate amounts                                               |
| typography.body_medium             | Outfit 14sp/400 | Cancel dialog body                                            |
| typography.body_small              | Outfit 12sp/400 | Next collection dates                                         |
| typography.label_medium            | Outfit 12sp/500 | Active count chip                                             |
| typography.label_small             | Outfit 11sp/500 | Status badges, mandate reference IDs                          |
| radius.md                          | 12dp      | Active count chip, cancel confirm buttons                           |
| radius.lg                          | 16dp      | Mandate cards, FAB                                                  |
| elevation.level2                   | 3dp       | Active mandate cards                                                |
| elevation.level4                   | 8dp       | Cancel confirmation dialog                                          |

---

_Generated by /idea export | 2026-05-29_
