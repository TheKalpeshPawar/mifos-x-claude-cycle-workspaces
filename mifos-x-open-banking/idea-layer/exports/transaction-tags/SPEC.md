# SPEC — Transaction Tags & Notes

| Field         | Value                          |
|---------------|--------------------------------|
| Feature       | transaction-tags               |
| Flavor        | consumer                       |
| Status        | approved                       |
| Quality Score | 99                             |
| ViewModel     | TransactionTagsViewModel       |

---

## Overview

Transaction Tags & Notes is a detail-screen feature accessible from the transaction detail view. It allows a Consumer persona user to annotate any transaction with free-form hashtag tags (#groceries, #work-expense, #rent, #holiday, #gym), a private text note, and a receipt image attachment. The top app bar shows "Tags & Notes" with a back arrow (`navigate_back` to `transaction-detail`) and a "Clear all" delete icon (`clear_all_metadata`). A green transaction header card (#4C662B) shows the merchant name ("Whole Foods Market"), debit amount ("−£67.84"), and timestamp ("23 May 2026 · 14:32"). Below that, horizontally scrollable tag chips allow removing existing tags with a single tap; an outlined text input + filled "Add" button lets the user append new tags. A multiline notes text area captures a private annotation. A dashed receipt attachment area with a camera button lets users attach an image from gallery or take a photo. A full-width green "Save" button persists tags, notes, and images via OBP Transaction Metadata endpoints and navigates back to `transaction-detail`. On successful save a green banner ("Tags and notes saved") briefly appears before auto-navigation (1800 ms delay). Data is loaded via the OBP v1.2.1 Transaction Metadata API: GET tags, POST tag, DELETE tag, POST comment, POST image. Seven states: loading, view_tags, edit_mode, save_success, content, empty, error.

---

## Screens

| ID               | Name                     | Route                               | Layout | Scroll   | ViewModel                  |
|------------------|--------------------------|-------------------------------------|--------|----------|----------------------------|
| transaction-tags | Transaction Tags & Notes | /transaction-tags/{transactionId}   | Column | Vertical | TransactionTagsViewModel   |

**States handled:** loading, view_tags, edit_mode, save_success, content, empty, error

**Shell:** Top app bar — title "Tags & Notes", `arrow_back` → `navigate_back` → `transaction-detail`. Top-right `delete_outlined` action → `clear_all_metadata`. No bottom navigation.

---

## Components

| ID                        | Type    | Description                                                                                                                       |
|---------------------------|---------|-----------------------------------------------------------------------------------------------------------------------------------|
| transaction_header_card   | box     | `#4C662B` bg, 20dp radius, 20dp padding all, 20dp H margin, 16dp top margin, 20dp bottom margin; `role: region`; `on_click: navigate_to_transaction_detail → transaction-detail` |
| txn_merchant              | text    | "Whole Foods Market" — Outfit/title_large SemiBold, `#FFFFFF`, pb 8dp                                                            |
| txn_amount                | text    | "−£67.84" — Outfit/display_small Bold, `#FFFFFF`, pb 4dp                                                                         |
| txn_date                  | text    | "23 May 2026 · 14:32" — body_medium, `#CDEDA3`                                                                                   |
| tags_section_label        | text    | "Tags" — Outfit/title_medium SemiBold, `#1A1C16`, px 20, pb 10dp; `role: heading`                                                |
| tags_hint_text            | text    | "Tap a tag to remove it" — body_small, `#44483D`, px 20, pb 8dp                                                                  |
| tags_chips_row            | stack   | Horizontal scroll, 8dp H padding, pb 12dp; `role: list`; bound to `obp_transaction_tags_get`; loading: 3 skeleton chips; error: banner with retry; empty: box with `label_outlined` icon |
| tag_chip_groceries        | box     | "#groceries" — `#CDEDA3` bg, 20dp radius, 12dp H / 6dp V padding, `#4C662B` label_medium; `on_click: remove_tag`; `role: button`  |
| tag_chip_work_expense     | box     | "#work-expense" — `#DCE7C8` bg, 20dp radius, `#386663` label_medium; `on_click: remove_tag`; `role: button`                      |
| tag_chip_rent             | box     | "#rent" — `#CDEDA3` bg, 20dp radius, `#44483D` label_medium (a11y-corrected from #E8A317 for ≥7.25:1 on #CDEDA3); `on_click: remove_tag` |
| tag_chip_holiday          | box     | "#holiday" — `#CDEDA3` bg, 20dp radius, `#4C662B` label_medium; `on_click: remove_tag`                                           |
| tag_chip_gym              | box     | "#gym" — `#CDEDA3` bg, 20dp radius, `#BA1A1A` label_medium; `on_click: remove_tag`                                               |
| add_tag_row               | stack   | Horizontal, 8dp gap, px 20, pb 20dp, centre-aligned; `role: row`                                                                 |
| add_tag_input             | input   | Outlined, `#E1E4D5` border, 12dp radius, 14dp H/V padding, flex 1, leading `label_outlined` icon; placeholder "#groceries, #holiday…"; `on_click: focus_tag_input`; `role: textbox` |
| add_tag_button            | button  | "Add" — filled, `#4C662B` bg / `#FFFFFF` text, 12dp radius, 16dp H / 12dp V padding, label_medium; `on_click: add_tag`            |
| notes_divider             | divider | `#F9FAEF`, 1dp, 20dp H margin, 20dp bottom margin; `role: none`                                                                   |
| notes_section_label       | text    | "Notes" — Outfit/title_medium SemiBold, `#1A1C16`, px 20, pb 10dp; `role: heading`                                               |
| notes_text_area           | input   | Outlined multiline, `#E1E4D5` border, 12dp radius, 14dp H/V padding, min 100dp height, px 20, mb 20dp; placeholder "e.g. Weekly shop — bought extra for bank holiday"; bound to `obp_transaction_comment_add`; loading/error/empty component_states |
| receipt_divider           | divider | Same style as notes_divider                                                                                                       |
| receipt_section_label     | text    | "Receipt" — Outfit/title_medium SemiBold, `#1A1C16`, px 20, pb 10dp; `role: heading`                                             |
| receipt_attachment_area   | box     | `#F9FAEF` bg, 16dp radius, `#E1E4D5` border 1dp dashed, 24dp padding, px 20, mb 12dp, items centred; `role: button`; bound to `obp_transaction_image_add`; loading/error/empty component_states |
| receipt_placeholder_icon  | icon    | `receipt_long_outlined`, 36dp, `#44483D`, self-aligned centre, mb 8dp; decorative (`role: none`)                                  |
| receipt_placeholder_text  | text    | "Tap to attach a receipt image" — body_medium, `#44483D`, centred                                                                |
| camera_button             | button  | "Take Photo" — outlined, `#386663` border+text, 12dp radius, leading `camera_alt`, 20dp H / 12dp V padding, label_medium; `on_click: open_camera` |
| save_button               | button  | "Save" — filled, `#4C662B` bg / `#FFFFFF` text, 14dp radius, 24dp H / 16dp V padding, label_large, full-width, mb 32dp; `on_click: save_metadata → transaction-detail` |
| save_success_banner       | box     | "Tags and notes saved" — `#CDEDA3` bg, 12dp radius, 16dp H / 12dp V padding, px 20, mb 16dp; `role: status`; visible in `save_success` state only |
| save_success_icon         | icon    | `check_circle_outlined`, 20dp, `#4C662B`, mr 8dp; decorative (`role: none`)                                                      |

---

## States

| ID           | Trigger                                                          | Description                                                                                          |
|--------------|------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| loading      | Screen entry — OBP metadata fetch in flight                      | Skeleton shimmer for tags/notes/receipt sections; `shimmer_duration: short4`; save button hidden     |
| view_tags    | Tags, notes and receipt loaded — read-only before editing        | 2 tag chips shown (#groceries, #work-expense); save button enabled                                  |
| edit_mode    | User types a new tag or focuses notes input                      | 5 tag chips shown; `add_tag_input` border turns `#4C662B` 2dp; keyboard visible                     |
| save_success | Save completed — brief banner before auto-navigate              | Success banner + icon; auto-navigate to `transaction-detail` after 1800 ms                           |
| content      | Alias for view_tags — default loaded state                       | Same layout as view_tags; 2 chips; save button enabled                                               |
| empty        | No tags on the transaction yet                                   | Empty state: hint message "No tags created yet. Add a tag to categorize your transactions."; save button enabled |
| error        | OBP API call failed                                              | Error state with `cloud_off` icon, "Unable to load metadata", "Could not load tags and notes. Check your connection and try again.", retry button; save button hidden |

---

## State Model

**ViewModel:** `TransactionTagsViewModel`
**Screen State Type:** `TransactionTagsUiState`

| Name           | Type                    | Default        |
|----------------|-------------------------|----------------|
| transaction    | `TransactionDetail?`    | `null`         |
| tags           | `List<TransactionTag>`  | `emptyList()`  |
| noteText       | `String`                | `""`           |
| tagInputText   | `String`                | `""`           |
| attachedImages | `List<TransactionImage>`| `emptyList()`  |
| isSaving       | `Boolean`               | `false`        |
| uiState        | `TransactionTagsUiState`| `Loading`      |
| error          | `UiError?`              | `null`         |

**Events:** `MetadataLoaded`, `TagAdded(value: String)`, `TagRemoved(value: String)`, `NoteChanged(text: String)`, `ImagePicked(uri: String)`, `CameraCaptured(uri: String)`, `SaveClicked`, `SaveComplete`, `RetryLoad`, `InputFocused(field: String)`, `InputBlurred`

**Actions:** `add_tag`, `remove_tag`, `focus_tag_input`, `focus_notes`, `pick_image_from_gallery`, `open_camera`, `save_metadata`, `clear_all_metadata`, `navigate_to_transaction_detail`

**DI Dependencies:** `TransactionMetadataRepository`, `ImageRepository`

**Errors:**

| Field          | Code              | Message                                                                   |
|----------------|-------------------|---------------------------------------------------------------------------|
| global         | LOAD_FAILED       | "Unable to load transaction metadata. Please try again."                  |
| save_tag       | TAG_SAVE_FAILED   | "Could not add tag. Please try again."                                    |
| save_note      | NOTE_SAVE_FAILED  | "Could not save note. Please try again."                                  |
| save_image     | IMAGE_SAVE_FAILED | "Could not attach image. Please try again."                               |
| tag_validation | TAG_EMPTY         | "Tag cannot be empty. Type a tag name like #groceries."                   |
| tag_validation | TAG_DUPLICATE     | "That tag is already added to this transaction."                          |

---

## Navigation

| From             | To               | Trigger                                                    | Type    |
|------------------|------------------|------------------------------------------------------------|---------|
| transaction-tags | transaction-detail | Top app bar back arrow → `navigate_back`               | pop     |
| transaction-tags | transaction-detail | `save_metadata` on success (after 1800ms banner delay) | pop     |
| transaction-tags | transaction-detail | Tap `transaction_header_card`                          | push    |

---

## API Endpoints

| Endpoint                                                                                                                      | Method | Auth        | Tag                  | Purpose                            |
|-------------------------------------------------------------------------------------------------------------------------------|--------|-------------|----------------------|------------------------------------|
| GET /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags                         | GET    | DirectLogin | Transaction-Metadata | Load existing tags for transaction |
| POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags                        | POST   | DirectLogin | Transaction-Metadata | Add a new tag                      |
| DELETE /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags/{tagId}              | DELETE | DirectLogin | Transaction-Metadata | Remove a tag                       |
| POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/comments                    | POST   | DirectLogin | Transaction-Metadata | Save a transaction note            |
| POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/images                      | POST   | DirectLogin | Transaction-Metadata | Attach a receipt image             |

---

## Design Tokens

| Token                          | Value     | Usage                                                               |
|--------------------------------|-----------|---------------------------------------------------------------------|
| colors.light.primary           | `#4C662B` | Transaction header card bg, save button fill, selected chip colors  |
| colors.light.on_primary        | `#FFFFFF` | Save button text, "Add" button text                                 |
| colors.light.primary_container | `#CDEDA3` | Tag chip backgrounds, save success banner bg                        |
| colors.light.secondary         | `#386663` | Camera button border+text, #work-expense chip bg via `#DCE7C8`     |
| colors.light.on_surface        | `#1A1C16` | Section headings (title_medium)                                     |
| colors.light.on_surface_variant| `#44483D` | Hint text, #rent chip label (a11y-corrected), receipt placeholder   |
| colors.light.error             | `#BA1A1A` | #gym chip label                                                     |
| colors.light.surface_variant   | `#E1E4D5` | Input border (default), dividers                                    |
| colors.light.background        | `#F9FAEF` | Screen bg, dividers                                                 |
| typography.display_small       | Outfit Bold 36sp | Transaction amount                                          |
| typography.title_large         | Outfit SemiBold 22sp | Merchant name                                           |
| typography.title_medium        | Outfit SemiBold 16sp | Section headings                                        |
| typography.body_medium         | Outfit Regular 14sp | Date, receipt placeholder, notes input                  |
| typography.label_medium        | Outfit Medium 12sp | Tag chip labels, "Add" button label                      |
| typography.label_large         | Outfit Medium 14sp | "Save" button label                                      |
| typography.body_small          | Outfit Regular 12sp | Hint text                                               |
| radius.md                      | 12dp      | Input fields, "Add" button, camera button                          |
| radius.lg                      | 16dp      | Receipt attachment area                                             |
| radius.xl                      | 20dp      | Transaction header card, tag chips                                  |
| touchTargets.min_touch_target  | 48dp      | All interactive elements                                            |

---

_Generated by /idea export | 2026-06-02_
