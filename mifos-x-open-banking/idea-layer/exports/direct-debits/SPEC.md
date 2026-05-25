# Direct Debits — Feature Specification

| Field | Value |
|---|---|
| Feature | direct-debits |
| Flavor | consumer |
| Status | designed |
| Quality Score | 88 |
| Contract Version | 1.1.0 |

---

## Overview

The Direct Debits screen displays all direct debit mandates (active and cancelled) for the consumer's account. Unlike standing orders (user-initiated recurring payments), direct debits are authorised by the account holder but executed by the payee on agreed collection dates. The screen lists mandates with payee name, collection amount, frequency, next collection date, status badge, and mandate reference. Users can view mandate details, cancel active mandates via a confirmation dialog, and set up new direct debits via a floating action button.

Mandate cancellation is a destructive, irreversible action — a confirmation dialog guards it. Cancelled mandates remain visible in a muted style for audit traceability.

---

## Screens

| Screen ID | Route | Layout | Scroll |
|---|---|---|---|
| direct-debits | /direct-debits | index_list | vertical |

**Shell:** Back navigation (`arrow_back` → accounts). Top app bar titled "Direct Debits" with `more_vert` overflow action. No bottom navigation.

---

## Components

| ID | Type | Description |
|---|---|---|
| title_count_row | stack | Horizontal header row containing title and active-count chip |
| direct_debits_title | text | "Direct Debits", headline_large, #1800B1, bold |
| active_count_chip | box | "3 active" — #E8F5E9 background, #4CAF50 text, label_medium semibold, r=12dp |
| direct_debit_netflix | box | Tappable card for Netflix mandate — white card, elevation 2, r=16dp |
| netflix_header_row | stack | Horizontal row: merchant name left, status badge right |
| netflix_payee | text | "Netflix", title_medium, #111111, semibold |
| netflix_active_badge | box | "Active" — #E8F5E9/#4CAF50, label_small, r=10dp |
| netflix_amount_row | stack | Horizontal row: amount left, next-date right |
| netflix_amount | text | "£15.99 / month", body_large, #1800B1, semibold |
| netflix_next_date | text | "Next: 3 Jun 2026", body_small, #888888 |
| netflix_mandate_ref | text | "Ref: DD-NF-20240301", label_small, #AAAAAA |
| direct_debit_spotify | box | Tappable card for Spotify mandate — white card, elevation 2, r=16dp |
| spotify_header_row | stack | Horizontal row: merchant name left, status badge right |
| spotify_payee | text | "Spotify", title_medium, #111111, semibold |
| spotify_active_badge | box | "Active" — #E8F5E9/#4CAF50, label_small, r=10dp |
| spotify_amount_row | stack | Horizontal row: amount left, next-date right |
| spotify_amount | text | "£10.99 / month", body_large, #1800B1, semibold |
| spotify_next_date | text | "Next: 12 Jun 2026", body_small, #888888 |
| spotify_mandate_ref | text | "Ref: DD-SP-20231115", label_small, #AAAAAA |
| direct_debit_gym | box | Tappable card for PureGym mandate (cancelled) — muted #FAFAFA background, no elevation |
| gym_header_row | stack | Horizontal row: merchant name left, cancelled badge right |
| gym_payee | text | "PureGym", title_medium, #888888, semibold (greyed out) |
| gym_cancelled_badge | box | "Cancelled" — #F5F5F5/#9E9E9E, label_small, r=10dp |
| gym_amount | text | "£29.99 / month", body_large, #AAAAAA, normal weight |
| gym_mandate_ref | text | "Ref: DD-GYM-20220601", label_small, #CCCCCC |
| cancel_confirm_dialog | dialog | Modal confirmation dialog for mandate cancellation — r=20dp, elevation 8 |
| cancel_dialog_title | text | "Cancel Direct Debit?", headline_small, #111111, bold |
| cancel_dialog_body | text | Dynamic: "{merchantName} ({mandateRef}) will stop collecting payments. This cannot be undone." |
| cancel_confirm_cta | button | "Yes, Cancel Mandate" — filled, #D32F2F, full-width, r=12dp |
| cancel_dismiss_cta | button | "Keep Mandate" — outlined, #1800B1, full-width, r=12dp |
| setup_direct_debit_fab | button | FAB "Set Up Direct Debit" — #1800B1, add icon, elevation 6, r=16dp |

---

## States

| State ID | Trigger | Visible Components |
|---|---|---|
| loading | Screen entry, before API response | title_count_row, direct_debits_title; skeleton list (3 cards, 110dp height each) |
| populated | API returns mandate list | All mandate cards (Netflix, Spotify, PureGym), title row with active_count_chip, setup FAB |
| empty | API returns zero mandates | title_count_row, direct_debits_title, setup FAB; empty state: account_balance_wallet icon + "No direct debits set up" |
| cancel_confirm | User taps cancel on active mandate | Full populated list visible + modal dialog overlay (50% dimmed background) with cancel_confirm_dialog components |
| error | API call fails | title_count_row, direct_debits_title, setup FAB; error state: cloud_off icon + "Unable to load direct debits" + retry button |

### State Transitions

```
Screen Entry → loading
loading → populated   (API success, mandates present)
loading → empty       (API success, no mandates)
loading → error       (API failure)
populated → cancel_confirm  (user taps "Cancel mandate" action on active card)
cancel_confirm → populated  (user taps "Keep Mandate" / cancel API success)
cancel_confirm → populated  (confirm_cancel_direct_debit → reload)
error → loading       (RetryLoad event)
populated → loading   (RefreshTriggered event)
```

---

## State Model

**ViewModel:** `DirectDebitsViewModel`

| Field | Type | Default | Description |
|---|---|---|---|
| directDebits | List\<DirectDebit\> | emptyList() | Full mandate list from OBP API |
| activeCount | Int | 0 | Count of mandates with status active |
| uiState | DirectDebitsUiState | Loading | Controls which state layout is rendered |
| selectedMandate | DirectDebit? | null | Mandate selected for cancellation confirmation |
| showCancelDialog | Boolean | false | Drives cancel_confirm dialog visibility |
| error | UiError? | null | Error details for error state display |

**Events:**

| Event | Trigger |
|---|---|
| DirectDebitsLoaded | API response received |
| ViewDirectDebitClicked | Mandate card tapped |
| SetUpDirectDebitClicked | FAB tapped |
| CancelDirectDebitClicked | Cancel action triggered on a mandate |
| CancelConfirmed | "Yes, Cancel Mandate" button tapped |
| CancelDismissed | "Keep Mandate" button tapped |
| RefreshTriggered | Pull-to-refresh gesture |
| RetryLoad | Retry button tapped in error state |

**Actions:**

| Action | Handler |
|---|---|
| view_direct_debit | Navigate to direct-debit-detail bottom sheet |
| setup_direct_debit | Open new mandate setup bottom sheet |
| confirm_cancel_direct_debit | Call DELETE API, reload mandate list |
| dismiss_cancel_dialog | Set showCancelDialog = false, clear selectedMandate |
| open_direct_debit_options | Open top bar overflow menu |

**DI Dependencies:** DirectDebitRepository, AccountRepository

**Error Codes:**

| Field | Code | Message |
|---|---|---|
| global | LOAD_FAILED | "Unable to load direct debits. Please try again." |
| cancel | CANCEL_FAILED | "Could not cancel mandate. Please try again." |
| create | CREATE_FAILED | "Could not set up direct debit. Please try again." |

---

## Navigation

| From | To | Trigger | Type |
|---|---|---|---|
| direct-debits | direct-debit-detail | Tap mandate card (view_direct_debit) | bottom sheet |
| direct-debits | (setup sheet) | Tap FAB (setup_direct_debit) | bottom sheet |
| direct-debits | direct-debits | confirm_cancel_direct_debit | reload in-place |
| direct-debits | accounts | arrow_back / navigate_back | pop |

---

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| primary | #1800B1 | Title text, amount text, FAB background, outlined button border |
| active_badge_bg | #E8F5E9 | Active status badge background |
| active_badge_text | #4CAF50 | Active status badge text |
| cancelled_badge_bg | #F5F5F5 | Cancelled status badge background |
| cancelled_badge_text | #9E9E9E | Cancelled status badge text |
| surface | #FFFFFF | Active mandate card background |
| surface_muted | #FAFAFA | Cancelled mandate card background |
| card_border | #F0F0F0 | Active card border |
| card_border_muted | #E0E0E0 | Cancelled card border |
| label_muted | #888888 | Next-date text, greyed payee name |
| label_faint | #AAAAAA | Mandate reference text (active) |
| label_ghost | #CCCCCC | Mandate reference text (cancelled) |
| destructive | #D32F2F | Cancel confirm CTA background |
| background | #FCF8FF | Screen background |

---

## Content Data (Populated State)

| Mandate | Merchant | Amount | Frequency | Next Date | Status | Mandate Ref |
|---|---|---|---|---|---|---|
| 1 | Netflix | £15.99 | Monthly | 3 Jun 2026 | Active | DD-NF-20240301 |
| 2 | Spotify | £10.99 | Monthly | 12 Jun 2026 | Active | DD-SP-20231115 |
| 3 | PureGym | £29.99 | Monthly | — (cancelled) | Cancelled | DD-GYM-20220601 |

Active count chip: "3 active"

---

## Accessibility

- All mandate cards have descriptive `content_description` including payee, amount, frequency, next date, status, and mandate reference.
- Status badges carry `role: status` for screen reader announcement.
- Cancel confirm dialog has `role: dialog` — focus traps inside when open.
- Cancel CTA: "Confirm cancellation of direct debit mandate" (destructive action is announced).
- FAB: "Set up a new direct debit" (imperative description).

---

*Generated by /idea export | 2026-05-25*
