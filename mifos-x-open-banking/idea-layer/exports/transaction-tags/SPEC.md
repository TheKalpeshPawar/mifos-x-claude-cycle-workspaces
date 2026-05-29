# SPEC — Transaction Tags & Notes

| Field         | Value                        |
|---------------|------------------------------|
| Feature       | transaction-tags             |
| Flavor        | consumer                     |
| Status        | approved                     |
| Quality Score | 99                           |
| ViewModel     | TransactionTagsViewModel     |

---

## Overview

The Transaction Tags & Notes screen lets the Consumer persona annotate a specific transaction with hashtag labels, a private free-text note, and a receipt image. It opens with a green hero header card showing the transaction details (Whole Foods Market, -£67.84, 23 May 2026 · 14:32). Below the header: a Tags section with existing chips (#groceries, #work-expense, etc.) and an add-tag input row; a Notes section with a multi-line text area; and a Receipt section with an image attachment zone and camera button. A full-width "Save" FilledButton commits all changes to OBP via the metadata API and auto-navigates back to Transaction Detail after a brief success banner. The screen has no bottom navigation. Five states: loading (skeleton), view_tags/content (loaded), edit_mode (input focused), save_success (auto-navigate after 1.8s), and error.

---

## Screens

| ID               | Name                    | Route                             | Layout | Scroll   |
|------------------|-------------------------|-----------------------------------|--------|----------|
| transaction-tags | Transaction Tags & Notes| /transaction-tags/{transactionId} | Column | Vertical |

**Shell:** Top app bar with back arrow + clear-all action. No bottom navigation bar.

| Element         | Value                    |
|-----------------|--------------------------|
| Title           | "Tags & Notes"           |
| Navigation icon | arrow_back               |
| Navigation action | navigate_back          |
| Action 1        | delete_outlined → clear_all_metadata |

---

## Components

| ID                       | Type    | Description                                                                                              |
|--------------------------|---------|----------------------------------------------------------------------------------------------------------|
| transaction_header_card  | box     | Green hero card, bg `#4C662B`, radius 20dp, padding H 20dp/V 20dp, margin H 20dp/top 16dp              |
| txn_merchant             | text    | "Whole Foods Market" — Outfit/title_large SemiBold, `#FFFFFF`                                          |
| txn_amount               | text    | "-£67.84" — Outfit/display_small Bold, `#FFFFFF`                                                       |
| txn_date                 | text    | "23 May 2026 · 14:32" — Outfit/body_medium, `#CDEDA3`                                                 |
| tags_section_label       | text    | "Tags" — Outfit/title_medium SemiBold, `#1A1C16`, padding H 20dp                                      |
| tags_hint_text           | text    | "Tap a tag to remove it" — Outfit/body_small, `#44483D`, padding H 20dp                               |
| tags_chips_row           | stack   | Horizontal scrollable row of existing tag chips; loading: skeleton 3 chips; error: banner; empty: inline guidance |
| tag_chip_groceries       | box     | "#groceries" — bg `#CDEDA3`, radius 20dp, padding H 12/V 6, text `#4C662B`, label_medium; tap → remove_tag |
| tag_chip_work_expense    | box     | "#work-expense" — bg `#DCE7C8`, radius 20dp, text `#386663`, label_medium; tap → remove_tag           |
| tag_chip_rent            | box     | "#rent" — bg `#CDEDA3`, radius 20dp, text `#44483D` (A11Y fix), label_medium; tap → remove_tag        |
| tag_chip_holiday         | box     | "#holiday" — bg `#CDEDA3`, radius 20dp, text `#4C662B`, label_medium; tap → remove_tag               |
| tag_chip_gym             | box     | "#gym" — bg `#CDEDA3`, radius 20dp, text `#BA1A1A`, label_medium; tap → remove_tag                   |
| add_tag_row              | stack   | Horizontal row: add_tag_input + add_tag_button; padding H 20dp                                         |
| add_tag_input            | input   | Outlined, border `#E1E4D5`, radius 12dp, label_outlined leading icon; placeholder "#groceries, #holiday…"; flex: 1 |
| add_tag_button           | button  | "Add" — filled `#4C662B`/white, radius 12dp, label_medium; triggers add_tag action                    |
| notes_divider            | divider | `#F9FAEF` 1dp divider, margin H 20dp                                                                   |
| notes_section_label      | text    | "Notes" — Outfit/title_medium SemiBold, `#1A1C16`, padding H 20dp                                     |
| notes_text_area          | input   | Outlined multiline, border `#E1E4D5`, radius 12dp, min-height 100dp; placeholder "e.g. Weekly shop — bought extra for bank holiday"; bound to obp_transaction_comment_add |
| receipt_divider          | divider | `#F9FAEF` 1dp divider, margin H 20dp                                                                   |
| receipt_section_label    | text    | "Receipt" — Outfit/title_medium SemiBold, `#1A1C16`, padding H 20dp                                   |
| receipt_attachment_area  | box     | bg `#F9FAEF`, radius 16dp, `#E1E4D5` 1dp dashed border, padding 24dp, centred; tap → pick_image_from_gallery; bound to obp_transaction_image_add |
| receipt_placeholder_icon | icon    | receipt_long_outlined 36dp, `#44483D`, centred                                                         |
| receipt_placeholder_text | text    | "Tap to attach a receipt image" — Outfit/body_medium, `#44483D`, centred                              |
| camera_button            | button  | "Take Photo" — outlined, border `#386663`, text `#386663`, radius 12dp, camera_alt leading icon       |
| save_button              | button  | "Save" — filled `#4C662B`/white, radius 14dp, label_large, full-width margin H 20dp; triggers save_metadata → transaction-detail |
| save_success_banner      | box     | bg `#CDEDA3`, radius 12dp, padding H 16/V 12, margin H 20dp; auto-dismiss; role status               |
| save_success_icon        | icon    | check_circle_outlined 20dp, `#4C662B`, margin_right 8dp                                               |

---

## States

| ID           | Trigger                                     | Description                                                                             |
|--------------|---------------------------------------------|-----------------------------------------------------------------------------------------|
| loading      | ScreenOpened                                | Green hero visible; 3 skeleton shimmer items replace tags/notes sections; Save hidden   |
| view_tags    | MetadataLoaded (2 existing tags)            | Hero + Tags (2 chips) + add row + Notes + Receipt + Save; read-only                    |
| content      | MetadataLoaded (alias for view_tags)        | Same as view_tags — default loaded state                                                |
| edit_mode    | InputFocused on add_tag_input               | Hero + 5 chips + add row (focused border `#4C662B` 2dp) + Notes + Receipt + Save      |
| save_success | SaveComplete                                | Success banner + 3 tags retained in view; auto-navigate to transaction-detail at 1.8s  |
| empty        | No tags on this transaction                 | Hero + Tags label + add row + Notes + Save; empty state guidance in chips row          |
| error        | LOAD_FAILED                                 | Hero visible; cloud_off icon, "Unable to load metadata", retry button; Save hidden     |

---

## State Model

**ViewModel:** `TransactionTagsViewModel`
**Screen State Type:** `TransactionTagsUiState`

| Name           | Type                    | Default     |
|----------------|-------------------------|-------------|
| transaction    | TransactionDetail?      | null        |
| tags           | List\<TransactionTag\>  | emptyList() |
| noteText       | String                  | ""          |
| tagInputText   | String                  | ""          |
| attachedImages | List\<TransactionImage\>| emptyList() |
| isSaving       | Boolean                 | false       |
| uiState        | TransactionTagsUiState  | Loading     |
| error          | UiError?                | null        |

**Events:** `MetadataLoaded`, `TagAdded(value)`, `TagRemoved(value)`, `NoteChanged(text)`, `ImagePicked(uri)`, `CameraCaptured(uri)`, `SaveClicked`, `SaveComplete`, `RetryLoad`, `InputFocused(field)`, `InputBlurred`

**Actions:** `add_tag`, `remove_tag`, `focus_tag_input`, `focus_notes`, `pick_image_from_gallery`, `open_camera`, `save_metadata`, `clear_all_metadata`, `navigate_to_transaction_detail`

**DI Dependencies:** `TransactionMetadataRepository`, `ImageRepository`

**Errors:**
- `LOAD_FAILED`: "Unable to load transaction metadata. Please try again."
- `TAG_SAVE_FAILED`: "Could not add tag. Please try again."
- `NOTE_SAVE_FAILED`: "Could not save note. Please try again."
- `IMAGE_SAVE_FAILED`: "Could not attach image. Please try again."
- `TAG_EMPTY`: "Tag cannot be empty. Type a tag name like #groceries."
- `TAG_DUPLICATE`: "That tag is already added to this transaction."

---

## Navigation

| From             | To                 | Trigger                             | Type |
|------------------|--------------------|--------------------------------------|------|
| transaction-tags | transaction-detail | Back arrow / navigate_back           | pop  |
| transaction-tags | transaction-detail | save_metadata → SaveComplete (1.8s)  | pop  |
| transaction-tags | transaction-detail | Tap transaction_header_card          | push |
| transaction-tags | transactions       | go_to_transactions deep-link         | push |
| transaction-tags | home               | go_to_home deep-link                 | push |

---

## API Endpoints

| Endpoint                                                                                                              | Auth        | Tag                  | Purpose                          |
|-----------------------------------------------------------------------------------------------------------------------|-------------|----------------------|----------------------------------|
| GET /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags                  | DirectLogin | Transaction-Metadata | Fetch existing tags              |
| POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags                 | DirectLogin | Transaction-Metadata | Add a tag                        |
| DELETE /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/tags/{tagId}       | DirectLogin | Transaction-Metadata | Remove a tag                     |
| POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/comments             | DirectLogin | Transaction-Metadata | Save private note (comment)      |
| POST /obp/v1.2.1/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/metadata/images               | DirectLogin | Transaction-Metadata | Attach receipt image by URL      |

---

## Design Tokens

| Token                          | Value   | Usage                                                               |
|--------------------------------|---------|---------------------------------------------------------------------|
| color.light.primary            | #4C662B | Hero bg, tag chip text, add-tag button bg, save button bg, success icon |
| color.light.primary_container  | #CDEDA3 | Tag chips bg (#groceries, #holiday, #gym), success banner bg       |
| color.light.secondary          | #386663 | #work-expense chip text, camera button border + text               |
| color.light.secondary_container| #DCE7C8 | #work-expense chip background                                      |
| color.light.error              | #BA1A1A | #gym chip text, error icon                                         |
| color.light.on_primary         | #FFFFFF | Hero text (merchant, amount), add button text, save button text    |
| color.light.primary_container  | #CDEDA3 | Transaction date text on hero (light green on dark green)          |
| color.light.background         | #F9FAEF | Screen bg, receipt attachment area bg                              |
| color.light.surface_variant    | #E1E4D5 | Input field borders, receipt attachment area border                |
| color.light.on_surface         | #1A1C16 | Section labels                                                     |
| color.light.on_surface_variant | #44483D | Hint text, #rent tag text, placeholder text                        |
| typography.title_large         | —       | Merchant name (22sp/600)                                           |
| typography.display_small       | —       | Transaction amount (32sp/SemiBold)                                 |
| typography.body_medium         | —       | Transaction date, receipt placeholder (14sp/400)                   |
| typography.title_medium        | —       | Section headings Tags / Notes / Receipt (16sp/500)                 |
| typography.body_small          | —       | Tags hint text (12sp/400)                                          |
| typography.label_medium        | —       | Tag chip text, add button text (12sp/500)                          |
| typography.label_large         | —       | Save button text (14sp/500)                                        |
| radius.xl                      | 20dp    | Transaction header card, tag chips                                 |
| radius.lg                      | 16dp    | Receipt attachment area                                            |
| radius.md                      | 12dp    | Add tag input, add button, notes text area, camera button          |
| radius.sm                      | 14dp    | Save button (spec: 14dp)                                           |
| spacing.md                     | 16dp    | Card padding, section margins                                      |
| spacing.sm                     | 8dp     | Between chips, tag row spacing                                     |

---

_Generated by /idea export | 2026-05-29_
