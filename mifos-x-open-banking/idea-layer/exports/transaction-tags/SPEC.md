# Feature Specification — Transaction Tags & Notes

| Field | Value |
|---|---|
| Feature | transaction-tags |
| Name | Transaction Tags & Notes |
| Flavor | consumer |
| Status | designed |
| Quality Score | 88 |
| Contract Version | 1.1.0 |

---

## Overview

The Transaction Tags & Notes screen is a detail-layer screen (accessible from transaction-detail) that allows consumers to enrich a specific transaction with metadata. For the sample transaction — Whole Foods Market debit of £67.84 on 23 May 2026 — the user can manage up to five colour-coded tag chips (#groceries, #work-expense, #rent, #holiday, #gym), add a private multi-line note, and attach a receipt image via gallery picker or camera. Tags are persisted to OBP via the transaction metadata API. A full-width "Save" button commits all changes; on success a green banner appears for 1 800 ms before auto-navigating back to transaction-detail. The top app bar provides a "Clear All" destructive action.

---

## Screens

| Screen ID | Name | Route | Archetype | Scroll |
|---|---|---|---|---|
| transaction-tags | Transaction Tags & Notes | /transaction-tags/{transactionId} | detail_screen | vertical |

---

## Components

| ID | Type | Description |
|---|---|---|
| transaction_header_card | box | Deep purple (#1800B1) header card; tap navigates to transaction-detail |
| txn_merchant | text | "Whole Foods Market" — title_large, white, semi-bold |
| txn_amount | text | "-£67.84" — display_small, white, bold |
| txn_date | text | "23 May 2026 · 14:32" — body_medium, #C5B8FF |
| tags_section_label | text | "Tags" — title_medium, semi-bold section heading |
| tags_hint_text | text | "Tap a tag to remove it" — body_small, #888888 hint |
| tags_chips_row | stack | Horizontal scrollable row of existing tag chips (spacing 8, overflow scroll_horizontal) |
| tag_chip_groceries | box | "#groceries" — bg #E8F5E9, text #2E7D32; tap removes tag |
| tag_chip_work_expense | box | "#work-expense" — bg #E3F2FD, text #1565C0; tap removes tag |
| tag_chip_rent | box | "#rent" — bg #FFF3E0, text #E65100; tap removes tag |
| tag_chip_holiday | box | "#holiday" — bg #F3E5F5, text #6A1B9A; tap removes tag |
| tag_chip_gym | box | "#gym" — bg #FCE4EC, text #AD1457; tap removes tag |
| add_tag_row | stack | Horizontal row containing add_tag_input + add_tag_button |
| add_tag_input | input | Outlined field, leading label_outlined icon, placeholder "#groceries, #holiday…"; focused border #1800B1 in edit_mode |
| add_tag_button | button | "Add" filled #1800B1; triggers add_tag action |
| notes_divider | divider | 1dp #F0F0F0 separator |
| notes_section_label | text | "Notes" — title_medium, semi-bold section heading |
| notes_text_area | input | Outlined multi-line text area, min_height 100, placeholder "e.g. Weekly shop — bought extra for bank holiday" |
| receipt_divider | divider | 1dp #F0F0F0 separator |
| receipt_section_label | text | "Receipt" — title_medium, semi-bold section heading |
| receipt_attachment_area | box | Dashed-border drop zone (radius 16, #DDDDDD); tap triggers pick_image_from_gallery |
| receipt_placeholder_icon | icon | receipt_long_outlined 36dp, #BBBBBB, centred |
| receipt_placeholder_text | text | "Tap to attach a receipt image" — body_medium, #AAAAAA, centred |
| camera_button | button | "Take Photo" outlined (#008B8B) with camera_alt leading icon |
| save_button | button | "Save" filled #1800B1, full width, label_large; action save_metadata → transaction-detail |
| save_success_banner | box | "#E8F5E9 banner — "Tags and notes saved"; role status; visible in save_success state only |
| save_success_icon | icon | check_circle_outlined 20dp, #2E7D32 |

---

## States

| ID | Trigger | Description |
|---|---|---|
| loading | Screen enters; metadata API in flight | Header card visible; skeleton placeholders for tags and notes sections |
| view_tags | Metadata loaded successfully | Full tags (2 of 5 chips shown), notes, receipt sections rendered; save button enabled |
| edit_mode | User focuses add_tag_input or notes_text_area | All 5 tag chips shown; add_tag_input border changes to #1800B1 (2dp); keyboard visible |
| save_success | save_metadata completes successfully | Success banner shown; auto-navigates to transaction-detail after 1 800 ms |
| error | OBP API call fails | Header card only; cloud_off error icon + "Unable to load metadata" message + retry button |

---

## State Model

**ViewModel:** `TransactionTagsViewModel`

### State Fields

| Name | Type | Default |
|---|---|---|
| transaction | TransactionDetail? | null |
| tags | List\<TransactionTag\> | emptyList() |
| noteText | String | "" |
| tagInputText | String | "" |
| attachedImages | List\<TransactionImage\> | emptyList() |
| isSaving | Boolean | false |
| uiState | TransactionTagsUiState | Loading |
| error | UiError? | null |

### Error Codes

| Field | Code | Message |
|---|---|---|
| global | LOAD_FAILED | Unable to load transaction metadata. Please try again. |
| save_tag | TAG_SAVE_FAILED | Could not add tag. Please try again. |
| save_note | NOTE_SAVE_FAILED | Could not save note. Please try again. |
| save_image | IMAGE_SAVE_FAILED | Could not attach image. Please try again. |
| tag_validation | TAG_EMPTY | Tag cannot be empty. Type a tag name like #groceries. |
| tag_validation | TAG_DUPLICATE | That tag is already added to this transaction. |

### Events

`MetadataLoaded`, `TagAdded(value: String)`, `TagRemoved(value: String)`, `NoteChanged(text: String)`, `ImagePicked(uri: String)`, `CameraCaptured(uri: String)`, `SaveClicked`, `SaveComplete`, `RetryLoad`, `InputFocused(field: String)`, `InputBlurred`

### Actions

`add_tag`, `remove_tag`, `focus_tag_input`, `focus_notes`, `pick_image_from_gallery`, `open_camera`, `save_metadata`, `clear_all_metadata`, `navigate_to_transaction_detail`

### DI Dependencies

`TransactionMetadataRepository`, `ImageRepository`

---

## Navigation

| From | To | Trigger | Type |
|---|---|---|---|
| top app bar back arrow | transaction-detail | navigate_back | pop |
| transaction_header_card | transaction-detail | navigate_to_transaction_detail | push |
| save_button | transaction-detail | save_metadata (post save_success + 1 800 ms) | pop |
| go_to_transactions deep-link | transactions | go_to_transactions | push |
| go_to_home deep-link | home | go_to_home | push |

---

## API Endpoints

| Endpoint | Auth | Purpose |
|---|---|---|
| GET /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags | DirectLogin | Fetch existing tags on screen load |
| POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags | DirectLogin | Add new tag when user taps "Add" |
| DELETE /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags/{tagId} | DirectLogin | Remove a tag when user taps an existing chip |
| POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/comments | DirectLogin | Persist the notes text area content |
| POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/images | DirectLogin | Attach receipt image URL to transaction |

---

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| primary | #1800B1 | Header card background, Add button, Save button |
| on_primary | #FFFFFF | All text on primary surfaces |
| primary_light | #C5B8FF | Transaction date on dark header |
| surface | #FFFFFF | Screen background |
| green_tag | #E8F5E9 / #2E7D32 | #groceries chip |
| blue_tag | #E3F2FD / #1565C0 | #work-expense chip |
| orange_tag | #FFF3E0 / #E65100 | #rent chip |
| purple_tag | #F3E5F5 / #6A1B9A | #holiday chip |
| pink_tag | #FCE4EC / #AD1457 | #gym chip |
| teal_action | #008B8B | Camera button |
| success_surface | #E8F5E9 | Save success banner |
| success_on | #2E7D32 | Save success icon + text |
| divider | #F0F0F0 | Section separators |
| error | #BA1A1A | Error state |

---

*Generated by /idea export | 2026-05-25*
