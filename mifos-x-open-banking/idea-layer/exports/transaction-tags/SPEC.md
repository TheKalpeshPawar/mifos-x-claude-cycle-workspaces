# Feature Specification — Transaction Tags & Notes

| Field | Value |
|---|---|
| Feature | transaction-tags |
| Name | Transaction Tags & Notes |
| Flavor | consumer |
| Status | enriched |
| Quality Score | 78 |

---

## Overview

The Transaction Tags & Notes screen is a detail-layer screen (accessible from transaction detail) that allows consumers to enrich a specific transaction with metadata. For the sample transaction — Whole Foods Market debit of £67.84 on 23 May 2026 — the user can manage tags (displayed as dismissible chips), add a private note in a multi-line text area, and attach a receipt image via gallery picker or camera. Existing tags "Groceries" and "Organic" are shown. All metadata is persisted to OBP via the transaction metadata API (tags, comments, images). A persistent "Save" button commits all changes. The top app bar includes a "Clear All" destructive action.

---

## Screens

| Screen ID | Name | Route | Archetype | Scroll |
|---|---|---|---|---|
| transaction-tags | Transaction Tags & Notes | /transaction-tags/{transactionId} | detail_screen | vertical |

---

## Components

| ID | Type | Description |
|---|---|---|
| transaction_header_card | box | Deep purple (#1800B1) header card showing merchant, amount and date |
| txn_merchant | text | "Whole Foods Market" title_large, white, semi-bold |
| txn_amount | text | "-£67.84" display_small, white, bold |
| txn_date | text | "23 May 2026 · 14:32" body_medium, #C5B8FF (light lavender) |
| tags_section_label | text | "Tags" section heading title_medium, semi-bold |
| tags_chips_row | stack | Horizontal scrollable row of existing tag chips |
| tag_chip_groceries | box | "Groceries" chip — #E8F5E9 bg, #2E7D32 text; tap removes tag |
| tag_chip_organic | box | "Organic" chip — #E8F5E9 bg, #2E7D32 text; tap removes tag |
| add_tag_input | input | Outlined text field with label_outlined leading icon; placeholder "Add a tag..." |
| add_tag_button | button | "Add" filled #1800B1; adds tag from input field |
| notes_section_label | text | "Notes" section heading title_medium, semi-bold |
| notes_text_area | input | Outlined multi-line text area, min height 100, placeholder "Add a private note about this transaction..." |
| receipt_section_label | text | "Receipt" section heading title_medium, semi-bold |
| receipt_attachment_area | box | Dashed-border drop zone (radius 16, #DDDDDD border) for receipt images |
| receipt_placeholder_text | text | "Tap to attach a receipt image" body_medium, #AAAAAA, centered |
| camera_button | button | "Take Photo" outlined (#008B8B teal) with camera_alt leading icon |
| save_button | button | "Save" filled #1800B1, full width, large — bottom of screen |

---

## States

| ID | Trigger | Description |
|---|---|---|
| loading | Screen enters; metadata API in flight | Header card visible with merchant/amount/date; skeleton content for tags and notes |
| content | Metadata loaded | Full tags, notes, receipt sections rendered |
| error | API failure | Header card; error state with cloud_off icon and retry button |

---

## State Model

**ViewModel:** `TransactionTagsViewModel`

### State Fields

| Name | Type | Default |
|---|---|---|
| transaction | TransactionDetail? | null |
| tags | List\<String\> | emptyList() |
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

### Events
`MetadataLoaded`, `TagAdded(value: String)`, `TagRemoved(value: String)`, `NoteChanged(text: String)`, `ImagePicked(uri: String)`, `CameraCaptured(uri: String)`, `SaveClicked`, `SaveComplete`, `RetryLoad`

### Actions
`add_tag`, `remove_tag`, `focus_tag_input`, `focus_notes`, `pick_image_from_gallery`, `open_camera`, `save_metadata`, `clear_all_metadata`

### DI Dependencies
`TransactionMetadataRepository`, `ImageRepository`

---

## Navigation

| From | To | Trigger | Type |
|---|---|---|---|
| top app bar back | transaction-detail | Back arrow | pop |
| save_button | transaction-detail | Save tap (on success) | pop |

---

## API Endpoints

| Endpoint | Auth | Purpose |
|---|---|---|
| GET /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags | DirectLogin | Fetch existing tags for the transaction |
| POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags | DirectLogin | Add a new tag to the transaction |
| POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/comments | DirectLogin | Add a private note/comment to the transaction |
| POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/images | DirectLogin | Attach a receipt image URL to the transaction |

---

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| primary | #1800B1 | Header card background, add tag button, save button |
| on_primary | #FFFFFF | Header text, button text |
| primary_light | #C5B8FF | Transaction date text on dark header |
| surface | #FFFFFF | Screen background for content sections |
| green_tag | #E8F5E9 / #2E7D32 | Tag chip background/text |
| teal_action | #008B8B | Camera button border/text |
| error | #BA1A1A | Error state |
| on_surface_variant | #AAAAAA | Receipt placeholder text |

---

*Generated by /idea export | 2026-05-25*
